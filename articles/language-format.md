---
title: "めちゃくちゃ簡易的に複数言語で表示できるページを作る"
emoji: "🛩"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","language","localize","Navigator"]
published: true
---
# 今回作りたいもの
- 日本語、英語、中国語で表示される簡易的なページ
- selectboxで言語選択もできる

# サンプル
### [簡易多言語対応](https://runstant.com/horieyuto/projects/cc9517f1)

# やっていること
- Navigator.language で言語を取得
- 言語に応じた文言を表示する
- 今用意している3ヶ国語以外の時はデフォルト(ja)を表示する
- selectboxで更新した時はcurrentLanguageを更新

# 最後に
題名の通りとても簡易的ですがこんな感じで実装できます
情報量が多いページだと文言の用意が大変になりますがお問い合わせフォームなんかを自作するときには使えるかと
