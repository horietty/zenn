---
title: "Stripe のテスト環境構築とダッシュボードから設定できること"
emoji: "💰"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","Javascript","Stripe","subscription"]
published: true
publication_name: "rabee"
---

## 始めに
今回は決済プラットフォームとして有名な Stripe の導入方法とダッシュボードから設定できることを紹介します。
Stripe にはテスト環境と本番環境があり、この記事ではテスト環境での検証方法を紹介します。
その他に自分の備忘録として、api やテスト環境注意点、できることを雑多に書いていこうと思います。
使用言語は Javascript で、簡易的にテストを行うためフロントにサーバー側のコードも記述しています。
[Stripe](https://stripe.com/jp?utm_campaign=JP_JA_Search_Brand_Stripe_EXA-19310753508&utm_medium=cpc&utm_source=google&ad_content=643624446228&utm_term=stripe&utm_matchtype=e&utm_adposition=&utm_device=c&gclid=Cj0KCQjwu-KiBhCsARIsAPztUF0xrl2UQXkmq27O6QBNdDw_wV4EW0WaFQkiMG-UDsZ0Ey_L7cZ4JvwaApRMEALw_wcB)

## テスト環境の作成と検証方法
1. [Stripeの公式ウェブサイト](https://stripe.com/) にアクセスし、「Start now」ボタンをクリックしてアカウント作成ページに移動します。

2. 必要な情報（名前、メールアドレス、パスワード）を入力し、「Create your Stripe account」ボタンをクリックしてアカウントを作成します。

3. アカウント作成後、Stripeダッシュボードにログインします。

4. ダッシュボードの右上にあるメニューから、「Developers」＞「API keys」を選択し、テスト用のAPIキー（Publishable KeyとSecret Key）をメモします。
![](/images/2023-05-09-13-22-18.png)
![](/images/2023-05-09-13-25-16.png)

5. [Stripeの公式ドキュメント](https://stripe.com/docs) を参照し、必要な機能やAPIに関する情報を確認します。

6. あなたの開発環境にStripeのSDKをインストールします。例えば、Node.jsの場合は、以下のコマンドを実行します。

```
npm install stripe
```

7. あなたのプロジェクトにStripeのAPIキーを設定します。例えば、Node.jsの場合は以下のように記述します。

```javascript
const stripe = require('stripe')('YOUR_STRIPE_SECRET_API_KEY');
```

8. 必要な機能（チェックアウト、サブスクリプションなど）を実装し、テスト用のAPIキーを使用して動作確認を行います。

9. 必要に応じて、[テストカード番号](https://stripe.com/docs/testing#cards) を使用して、さまざまなシナリオをテストします。


## ダッシュボードでできること

### カスタマーポータルや checkout 画面のレイアウト変更
以下がカスタマイズ可能な項目です（checkout にはタイポグラフィーやスタイルの設定も可能です ）
- アイコン
- ロゴ
- ブランドカラー
- アクセントカラー

![](/images/2023-05-09-15-03-52.png)

### 商品の追加
stripeから商品を追加する際に以下のようなパターンを作成することができます。
- 一つの商品に、複数のplan(購入形態、料金プラン)を設定できる。
![](/images/2023-05-09-15-14-13.png)
- トライアル期間を設定することができる
![](/images/2023-05-09-15-14-39.png)

### ドメイン変更
課金オプションですが、checkout ドメインや Stripe からのメールドメインは変更することができます。
![](/images/2023-05-09-15-16-26.png)

### メールのテスト配信
テスト環境では何かをトリガーにしたメールは送られませんが、ダッシュボードからメールのテスト配信ができます。
これにより実際に送られてくるメールがどのようなものか確認することができます。

## カスタマーポータルへの遷移方法（api）
通常、カスタマーポータルへの遷移は Stripe からのメールを介してワンタイムのリンクを踏むことで遷移しますが、[api](https://stripe.com/docs/api/customer_portal/sessions/create) でワンタイムURL を発行して遷移することも可能です。

## 支払い方法の削除
ユーザの支払い方法を削除する際、その支払い方法で決済をしているサブスクリプションには自動でデフォルトの支払い方法が割り当てられるので非常に優秀です。
![](/images/2023-05-09-15-28-56.png)

## checkout sessions create の注意点
Stripe の決済ページへのリンクを生成する [checkout sessions create](https://stripe.com/docs/api/checkout/sessions/create) api では複数の商品、複数の決済方法を指定することができますが。以下の注意が必要です。
- 商品の決済期間が同一であること
  - 例えば、支払い期間が月次の商品と年次の商品は同時に購入することができません。
- 商品の通貨と、決済方法の通貨が同一であること
  - 日本円の設定しかない商品を、ドル等で決済することはできません。

## サブスクリプション比例配分の仕組み（日割り/秒割り）
サブスクリプションの数量やグレードを変更した場合、その月の残り日数分の料金を日割りで計算して支払いを行います。
[ドキュメント](https://stripe.com/docs/billing/subscriptions/prorations)

## 最後に
特に後半は自分の備忘録として書いてしまったので、見ていただいた方の役に立つかわかりませんが、Stripe は非常に優秀な決済プラットフォームなので、ぜひ使ってみてください。