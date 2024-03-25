---
title: "時間経過によって変わる人気ロジックの実装"
emoji: "⬆️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","backend","popular","go","time"]
published: true
publication_name: "rabee"

---

## 今回の話

サービス内で`人気のXX`や`急上昇のXX`などのロジックが必要なことがあるかと思います。
とてもシンプルな形であれば、何かのイベントが発生したら人気度を上げることで実現できますが、仕様によっては時間経過によって変化する必要があるかもしれません。
今回はそのようなケースを想定して、時間経過によって変わる人気ロジックの実装方法をご紹介します。

## 設計
- 1ランクの単位(RankBase)を`60*60*1000` とする（1時間）
- 最大値（MaxRank）を定義（これを定義しておかないと、ある一点からずっと人気のXX が作れてしまう可能性があるため）
- イベントごとに weight を決める（例えば、いいねは 1、コメントは 2 など）
  - 例) - 閲覧 ... 1、お気に入り ... 6、コメント ... 4、フォロー ... 24

## コード

```go
// Rank の計算
func AddRank(rank int64, weight int) int64 {
	// rank の最小値考慮
	now := // 現在時刻を unixtime で取得
	if rank < now {
		rank = now
	}
	rank += int64(weight * RankBase)

	// rank の最大値考慮
	maxRank := now + int64(MaxRank)
	if rank > maxRank {
		rank = maxRank
	}

	return rank
}
```

unixtime で取得した現在時刻を基準に、weight に応じて rank を加算しているため、時間経過によって rank が変化します。
AddRank が呼ばれるのはイベントが発生した時なので、取得する際に rank 降順で取得することで、人気のXX などを実現できます。

## 最後に
単純に rank を加算していくだけでも`人気のXX`の実現は可能ですが、ずっと`人気のXX`が変わらないと言う事態が起きがちなので、現在時刻を基準とすることでより直近の人気度を反映させることができます。