---
title: "for in を使ったオブジェクトの比較"
emoji: "🔍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","javascript","object","comparison"]
published: true
---

# 今回のゴール
二つのオブジェクトを比較してkeyが一致するときvalueを比較する。
今回は比較して一致する場合はkeyごとオブジェクトから削除する。

# サンプル
[オブジェクト比較のサンプル](http://runstant.com/horieyuto/projects/5c55b19b)

`比較１`を実行するとobj1とobj2の比較を始めます
比較の結果`りんご`, `もも`が一致するので残りの昆虫たちが残ります。
```
<!-- 出力結果 -->
{
  "key2": "カブトムシ",
  "key3": "カマキリ",
  "key5": "てんとう虫"
}
```

続いて`比較2`を実行します。
比較2はobj2とobj3を比較しますがobj2は一度比較をした後なので最初のkey, valueではなくなっているため結果はこうなります。
```
<!-- 出力結果 -->
{
  "key1": "りんご",
  "key3": "消防車",
  "key4": "もも",
  "key5": "飛行機"
}
```

逆に`比較2` → `比較1`の順番で検証をするとこの様な結果になります
```
<!-- 比較2 -->
{
  "key3": "消防車",
  "key5": "飛行機"
}

<!-- 比較1 -->
{
  "key2": "カブトムシ",
  "key3": "カマキリ",
  "key5": "てんとう虫"
}
```


# コード
```
<body>
  <h1>オブジェクト比較</h1>
  <p>ボタンを押して比較実行！</p>
  <input type='button' value='比較１', onclick="compare1()">
  <input type='button' value='比較2', onclick="compare2()">
  
  <script>
    var obj1 = {
      key1: 'りんご',
      key2: 'ぶどう',
      key3: 'いちご',
      key4: 'もも',
      key5: 'すいか',
    };
    
    var obj2 = {
      key1: 'りんご',
      key2: 'カブトムシ',
      key3: 'カマキリ',
      key4: 'もも',
      key5: 'てんとう虫',
    };
    
    var obj3 = {
      key1: 'りんご',
      key2: 'カブトムシ',
      key3: '消防車',
      key4: 'もも',
      key5: '飛行機',
    }
    
    // obj1とobj2を比較して一致するkey,valueはobj2から削除
    function compare1() {
      for (var key in obj2) {
        if (obj2[key] === obj1[key]) {
          delete obj2[key];
        }
      }
      console.log(obj2);
    }
    
    // obj2とobj3を比較して一致するkey,valueはobj3から削除
    function compare2() {
      for (var key in obj3) {
        if (obj3[key] === obj2[key]) {
          delete obj3[key];
        }
      }
      console.log(obj3);
    }
    
  </script>
</body>
```
