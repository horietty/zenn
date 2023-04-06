---
title: "要素が画面内に入ったらアニメーション を実装する"
emoji: "🔍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","javascript","intersectionobserver","animation"]
published: true
publication_name: "rabee"

---

# 今回のゴール
要素が画面内に入ったらスタートするアニメーションを実装する

実装イメージ
https://www.opera-net.jp/
このサイトは画面内に入ると文字がふわっと出てくるが、今回は要素の色が変わる様に実装

# 技術
- HTML
- CSS
- javascript

# コード
```
<style>
  .box {
    width: 128;
    height: 128;
    background: red;
    margin-bottom: 32px;
    transition: 512ms
    opacity: 0;
  }
  
  
  .fadein-bottom {
    animation-name: fadeup;
    animation-duration: 1s;
    animation-fill-mode: forwards;
    background: blue;
  }
  
  @keyframes fadeup {
    0% {
      opacity: 0;
      transform: translateY(20px);
    }
    100% {
      opacity: 1;
      transform: translateY(0);
    }
  }

</style>
<body>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
  <div class='box' data-reveal-class='fadein-bottom'></div>
    
  <script>
    window.onload = function() {
      // data-reveal-class 属性が指定されている要素をすべて取得
      var elements = document.querySelectorAll('[data-reveal-class]');
      
      var observer = new IntersectionObserver( (entries, observer) => {
        // 監視対象で変化があったものすべてが entries に入ってくる
        entries.forEach(entry => {
          var target = entry.target;
          if (entry.isIntersecting) {
            target.classList.add(target.dataset.revealClass);
          }
          else {
            target.classList.remove(target.dataset.revealClass);
          }
        });
      });
      
      // すべての要素を監視対象にする
      Array.from(elements).forEach($elm => {
        observer.observe($elm);
      });
    };

  </script>
</body>
```

IntersectionObserverを使って対象の要素を監視します
対象の要素が画面内に入ったらアニメーションクラスをつけ、画面外に出たら外す対応で実現しています

### [サンプル](http://runstant.com/horieyuto/projects/41ca13b7)

script部分を関数化すれば必要な場所にだけ仕込むこともできるので使い回しも効きます