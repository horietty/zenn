---
title: "Heroku でダッシュボードから環境変数を設定する方法"
emoji: "🌀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","heroku", "environment"]
published: false
publication_name: "rabee"
---

## Heroku とは

まずはじめに、Herokuはクラウドベースのプラットフォーム・アズ・ア・サービス（PaaS）で、アプリケーションの開発、デプロイ、運用を簡単に行えます。多様なプログラミング言語をサポートし、Gitを使った簡単なデプロイが可能です。また、機能を追加するためのアドオンが用意されています。インフラの管理が不要なため、開発者はアプリケーション開発に集中できます。

[ドキュメント | Heroku Dev Center](https://devcenter.heroku.com/ja/categories/reference)

## 設定方法

今回はダッシュボードからの設定方法を紹介します。

1. [Heroku Dashboard](https://dashboard.heroku.com/apps)にアクセスし、ログインしてください。
2. アプリケーション一覧から、環境変数を変更したいアプリケーションを選択します。
3. 左側のナビゲーションバーで「Settings」（設定）タブをクリックします。
4. 「Config Vars」（環境変数）セクションまでページをスクロールし、「Reveal Config Vars」ボタンをクリックします。
  ![](/images/2023-04-27-17-54-15.png)
5. ここで、環境変数の追加、編集、削除が行えます。
  - 環境変数を追加する場合：「KEY」欄と「VALUE」欄にそれぞれ名前と値を入力し、「Add」ボタンをクリックします。
  - 環境変数を編集する場合：既存の「KEY」または「VALUE」をクリックし、新しい値に書き換えます。自動的に保存されます。
  - 環境変数を削除する場合：削除したい環境変数の右側にあるバツアイコンをクリックし、「Delete Config Var」ボタンをクリックします。
  ![](/images/2023-04-27-18-01-05.png)
  ![](/images/2023-04-27-18-03-15.png)


## 最後に
環境変数によって、色々挙動を変えている場合heroku と local で挙動が違う時はこの辺りが原因だったりするので、一度確認してみるといいかもしれません。