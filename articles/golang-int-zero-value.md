---
title: "golang int64型のゼロ値は 0 を業務内で実感した話"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","backend","golang","int","zero-value"]
published: true
publication_name: "rabee"
---

## 今回の話

golang のさまざまな型の中で、 int(int64) のゼロ値が 0 であることはみなさんご存知かと思いますが、今回は初学者である私が業務内でゼロ値が0 であることを実感した話を書いていきます。

## 経緯

あるサービスの API で特定のコレクションからデータを取得しフロントに返す処理があるのですが、実際に叩いてみるとフィールドで定義している status が特定のもの(仮で `hoge`とします)だけレスポンスに含まれないという事象が起きました。

## 事象の解決
直近その API は改修が入っており取得方法を Firestore から直接取っていたのを algolia から IDs を取得して Firestore から一致するドキュメントのみ取得するように変更されていました。 
そのため、当初の予測では algolia → Firestore の取得処理で何か意図しない処理が入っているのではないかと考えていました。

まず初めに、弊社の環境だとステータス: `hoge` のものはインデックスさせないことが多いのでそこの確認をしましたがしっかりとインデックスされていました。

次に実際にlocal で動かしてみてどのタイミングでステータス: `hoge` が落ちるかの検証をし結果は以下でした。
- algolia から取得時 → ステータス: `hoge` のIDsが含まれている
- Firestore から取得時 → ステータス: `hoge` のものが含まれていない

上記の結果、Firestore から取得時にステータス: `hoge` のものが落ちているため、Firestore へのリクエスト内容を確認することにしました。
よくあるのがデータ取得時に特定のステータスのものは除外するような処理が入っていることがあるので、その辺りを確認しましたがそこは問題がありませんでした。

当初予測を立てていた箇所は全て問題なかったものの、原因の箇所は Firestore から取得する箇所というのはわかっていたのでさらにリクエストを確認すると一つ怪しい指定がありました。
**その指定が今回の題名である int64 に関連する部分**となるのですが、ドキュメントを取得する際に `int64` で定義されているフィールドが現在より前のものは取得しないように指定されていました。
int64 で定義されているフィールドはユーザーが特定の操作を行なったときのみ更新されるのですが、status: `hoge` の時はそこに値が入ることはなくゼロ値の考慮が漏れていました。
結果的にその指定を外すことで status: `hoge` のものも取得できるようになりました。

## 最後に
今回は文章のみで見づらく申し訳ございません。（半分戒めとして書いているのでご容赦ください）
なにも値が入らない = 特に考慮入れない ではなく、ゼロ値も考慮しておくことが重要だということを学びました。
また、考慮漏れは反省すべき点ですが、原因特定までの過程は悪くなかったなと思っているため、未熟さと成長を実感できる良い機会となりました。
