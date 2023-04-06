---
title: "form 内に submit を複数配置するときのハック"
emoji: "🔘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","form","submit","onsubmit"]
published: true
publication_name: "rabee"

---

## 今回の話

何かの入力フォームを作るとき、form の submit を使ってバリデーションをかけたいが、押されたボタンによって処理変えたい場合の対処法

## コード

下記がコードになります
デモは最後にあるので css は割愛しますが、html での肝は enter押下時に発火させたい submit buttonが最初にない場合の考慮です
コードを見てもらえるとわかるのですが、html 上は存在するが、ユーザーからは見えない button を用意してあります
これは enter押下時に最初の submit button が発火するため、デフォルトの処理としたい buttonB とおなじ submit を発火させるためのものです。

```html
<div class='container p12'>
  <form onsubmit="onSubmit(event)">
    <div class="flex fm fbw mb12">
      <h2>form test</h2>
      <div class="flex fm">
        <button class="hide" type="submit"></button>
        <button class="button mr6" type="submit" onclick='{changeFlag()}'> buttonA</button>          
        <button class="button" type="submit"> buttonB</button>
      </div>
    </div>
    <input type="text" class="mb12" placeholder="text" required />
    <input type="number" placeholder="num" required />
  </form>
</div>
```

javascript は非常にシンプルで、buttonA が押された時はフラグを変えて、そのフラグによって onSbmit の処理を分岐しています。

```js
var isPostTemplate = false;
      
function onSubmit(e) {
  e.preventDefault();
  if (isPostTemplate) {
    console.log('buttonA');
    // フラグを戻す
    isPostTemplate = false;
  }
  else {
    console.log('buttonB');
  }
}

function changeFlag() {
  isPostTemplate = true;
}
```

## デモ
最後にデモもご用意してますので是非ご覧ください

### [form submit test | Runstant](http://runstant.com/horieyuto/projects/b55e762f)
