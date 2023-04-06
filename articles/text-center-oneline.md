---
title: "テキストを一行の時は中央寄せ、二行以上の時は左よせにする方法"
emoji: "💡"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","HTML","text-aline","CSS"]
published: true
publication_name: "rabee"
---

# 今回対応したいこと
- テキストを表示する際一行の時は中央寄せ、二行の時は左よせにしたい。
- テキストごとにハードコーディングすれば簡単にできるが動的にテキストが変わるため一つのクラスでどちらにも対応できるようにする。

# 対応方法
今回は `margin-inline` と `max-inline-size` の組み合わせで対応したいと思います。
``` 
.text-oneline-center {
  margin-inline: auto;
  max-inline-size: max-content;
}
```

## サンプル
### [サンプル](https://runstant.com/horieyuto/projects/b26fc090)

サンプルを見てもらうとわかる通り要素内にテキストが収まる場合は左右に margin をとり中央寄せになります。
要素内に収まらない場合は marginはないので親要素の text-aline に準拠した出力となります。

## 最後に
今回もかなり細かいテクニックにはなりますが、ぜひ活用してみてください。

