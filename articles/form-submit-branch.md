---
title: "form 内に submit を複数配置するときのハック"
emoji: "🔘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","form","submit","onsubmit"]
published: true
---

## 今回の話

何かの入力フォームを作るとき、form の submit を使ってバリデーションをかけたいが、押されたボタンによって処理変えたい場合の対処法

## コード

下記がコードになります
デモは最後にあるので css は割愛しますが、html での肝は enter押下時に発火させたい submit buttonは 最初に持ってくることです。
コードを見てもらえるとわかるのですが、html 上は buttonB が最初に来ていますが、デモを見ていただくと buttonB が buttonA の後に来るようになっています。これは enter押下時に最初の submit button が発火するため、デフォルトの処理としたい buttonB を考慮したものとなります

``` html
<div class='container p12'>
  <form onsubmit="onSubmit(event)">
    <div class="flex fm fbw mb12">
      <h2>form test</h2>
      <div class="flex fm flex-row-reverse">
        <button class="button" type="submit"> buttonB</button>
        <button class="button mr6" type="submit" onclick='{changeFlag()}'> buttonA</button>          
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
