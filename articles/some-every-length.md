---
title: "javascript の some every を 空配列で実行した話"
emoji: "☀️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","javascript","some","every"]
published: true
---

## 今回の話

javascript の超便利メソッド some, every 自分も普段からよく使うのですが、空の配列で実行した時に期待する挙動と違うことがあり記事にしました。
百聞は一見に如かずということで早速コードとデモを次に記載します。

## コード

下記のコードでは some と every をそれぞれから配列で実行してその結果をコンソールに出力しています。

``` js
var hoge = [];
var fuga = 'aaaaaa';
var every_result_1 = hoge.every(h => h === fuga);
var some_result_1 = hoge.some(h => h === fuga);
console.log('every_result_1', every_result_1);
console.log('some_result_1', some_result_1);
```

出力結果

```
every_result_1 true
some_result_1 false
```

期待していた結果としては some every いずれも false が返ってくることだったのですが、ご覧のように every では true が返ってきています。
思わぬバグの原因になりかねないので、要注意です。

## デモ

### [some every テスト | Runstant](http://runstant.com/horieyuto/projects/9a99dc1f)
