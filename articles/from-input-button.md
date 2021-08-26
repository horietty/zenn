---
title: "inputにフォーカスしているときにEnterキー押下で意図しないbuttonが発火してしまう時の対処法"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","HTML","form","input"]
published: true
---

# 事象の前提
下記の様な構成で適当なinputにフォーカスしてEnterキーを押下すると意図しないbuttonが発火してしまう
```
<!-- HTML -->
<form onsubmit='submitClick()'>
  <div>text</div>
  <input type='text' style='display: block; margin-bottom: 10px'>

  <div>radio</div>
  <input type='radio' style='display: block; margin-bottom: 10px'>
  
  <div>checkbox</div>
  <input type='checkbox' style='display: block; margin-bottom: 10px'>
  
  <div>textarea</div>
  <textarea style='display: block; margin-bottom: 10px'></textarea>
  <!-- Enter で発火させたくないbutton-->
  <button onclick='buttonClick()'>button</button>
  <button>submitbutton</button>
</form>

<!-- script -->
function buttonClick() {
  event.preventDefault();
  console.log('click');
};

function submitClick() {
  event.preventDefault();
  console.log('submit');
};
```

# 原因と解決方法
## 原因
formの仕様でinputフォーカス時にenter押下すると最も近いbutton(submit)が発火してしまうのが原因。
buttonタグは初期値が`type='submit'`なので、今回の様にenterキーで発火させたくないbuttonに`type='button'`をつける。
form内にbuttonが複数ある場合は明示的にどのボタンにもtype指定をしておくのが良い。

# サンプル
参考までに色々なinput typeのサンプルです
textareaはenter押下=改行なので他の様にbuttonがはっかすることはありませんでした。

### [formサンプル1](https://runstant.com/horieyuto/projects/2dc706f3)(バグるバージョン)
### [formサンプル2](https://runstant.com/horieyuto/projects/f4f3b41f)(修正バージョン)