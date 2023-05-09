---
title: "Stripe のテスト環境構築とダッシュボードから設定できること"
emoji: "💰"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","Javascript","Stripe","subscription"]
published: false
publication_name: "rabee"
---

## 始めに
今回は決済プラットフォームとして有名な Stripe の導入方法とダッシュボードから設定できることを紹介します。
Stripe にはテスト環境と本番環境があり、この記事ではテスト環境での検証方法を紹介します。
使用言語は Javascript で、簡易的にテストを行うためフロントにサーバー側のコードも記述しています。
[Stripe](https://stripe.com/jp?utm_campaign=JP_JA_Search_Brand_Stripe_EXA-19310753508&utm_medium=cpc&utm_source=google&ad_content=643624446228&utm_term=stripe&utm_matchtype=e&utm_adposition=&utm_device=c&gclid=Cj0KCQjwu-KiBhCsARIsAPztUF0xrl2UQXkmq27O6QBNdDw_wV4EW0WaFQkiMG-UDsZ0Ey_L7cZ4JvwaApRMEALw_wcB)

## テスト環境の作成と検証方法
1. [Stripeの公式ウェブサイト](https://stripe.com/) にアクセスし、「Start now」ボタンをクリックしてアカウント作成ページに移動します。

2. 必要な情報（名前、メールアドレス、パスワード）を入力し、「Create your Stripe account」ボタンをクリックしてアカウントを作成します。

3. アカウント作成後、Stripeダッシュボードにログインします。

4. ダッシュボードの左上にあるメニューから、「Developers」＞「API keys」を選択し、テスト用のAPIキー（Publishable KeyとSecret Key）をメモします。
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


## ダッシュボードから設定できること

### カスタマーポータルや checkout 画面のレイアウト変更
以下がカスタマイズ可能な項目です（checkout にはタイポグラフィーやスタイルの設定も可能です ）
- アイコン
- ロゴ
- ブランドカラー
- アクセントカラー

![](/images/2023-05-09-15-03-52.png)