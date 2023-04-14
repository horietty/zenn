---
title: "Milkdown エディター内の要素をクリックした時のハンドリング方法"
emoji: "🌀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rabee","frontend","milkdown", "markdown"]
published: true
publication_name: "rabee"
---

## Milkdown とは

Milkdown とは マークダウンエディターフレームワークです。React、Vue、Svelteなどのフロントエンドライブラリやフレームワークと簡単に統合できます。
最近 Milkdown を使って開発する機会があり、エディター内の要素をクリックした時のハンドリング方法を調べたのでメモとして残しておきます。

[Milkdown ドキュメント](https://milkdown.dev/)

## 対応したいこと

Milkdown はエディターを更新すると、即マークダウンの HTML に変換されます。
aタグも`[hogehoge](https://hogehoge.com)`と書くとすぐに変換されるのですが、デフォルトの挙動が同じタブ内で開くので、今回は別タブで開きたいと思います。

## 対応方法

このように書くと別タブで開きます。(該当箇所以外は削除しているのでこのままでは動かないですが...)

```js
// editor 初期化
const initializeEditor = async (element) => {
  editor = await Editor.make()
    .config((ctx) => {
      ctx.set(editorViewOptionsCtx, {
        handleDOMEvents: {
          click: handleElementClick,
        },
      });
    })
};

// クリックした時にaタグだったら別タブで開く
const handleElementClick = (view, event) => {
  if (event.target.tagName.toLowerCase() === 'a') {
    event.preventDefault();
    // 新しいタブでリンクを開く
    const href = event.target.getAttribute('href');
    window.open(href, '_blank');
  }
};
```

実装前のイメージだと listner に click イベントを登録して、aタグだったら別タブで開けないかなと思っていたのですが、
どうやら Milkdown の listner には click系のものがなかったので、handleDOMEvents に click イベントを登録することで実現できました。
ちなみに、handleDOMEvents で受け取っている view は 関数内では使用してないですが受け取らないと event.target が取得できなかったので、受け取っています。

## 最後に
短い記事にはなりますが、まだ Milkdown の情報は少ないので、ぜひ活用してみてください。
