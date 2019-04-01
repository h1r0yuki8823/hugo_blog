---
title: "user agent stylesheetを無効化したお話"
date: 2019-04-01T23:18:31+09:00
draft: false
---

## 小話
今、友人にサイトを作って欲しいと言われ簡単なサイトを作っている。簡単にwixのようなサイトを作成するサービスで済まそうと思ったけどもちょうどvueの教本が終わった所だったので、練習がてらVueを使用して作ってみることにした。<br>
今回はBootstrapのようなcssフレームワークを使用しないので教本を見ながらcssを設定している。<br>


## 四方に微妙な余白が
サイトが形になっていくと四方の余白があることに気づいた。<br>
![This is a image1](../images/css_space1.png)
chromeのelementsを見てみるとbodyにmarginが8px設定されていることが確認できる<br>
{{< figure src="/images/css_space2.png" title="Screenshot" class="center" width="320" height="640" >}}<br>
cssを探してみてもどこにもmargin:8px;という記述はない<br>

よくよくelementsをみていると user agent stylesheetと書かれている。

## user agent stylesheetとは?
user agent stylesheetはブラウザごとに定義されたデフォルトのcss設定のこと。<br>
このcssをリセットするためにはリセットCSSというものを使えば、ブラウザ固有のCSSの設定を上書きできる<br>
一応メリット、デメリットはあるみたいだ。<br>
 
 ### メリット
 <li>ブラウザごとのデザインを揃えることができる
 <li>自分でブラウザごとのCSSを書かなくて済む

 ### デメリット
 <li>CSSのコード量が多くなる
 <li>リセットして項目を自分で書く必要がある

 ## とはいえ
 デメリットがあるとはいえ世の中に公開されているwebサイトはほとんどリセットCSSを使用しているので素直に使用しよう

 ## 使用方法
 リセットcssには種類があるが今回はnormalize.cssを使用<br>
 [github](https://raw.githubusercontent.com/necolas/normalize.css/master/n)<br>
 githubのページにアクセスして表示されたコードをコピペしてhtmlファイルのheaderタグの中で使用<br>
 ```html
 <head>
  <meta charset="UTF-8">
  <title>Normalize</title>
  <!-- normalize.cssの読込 -->
  <link rel="stylesheet" href="normalize.css">

  <!-- 自身で作成したCSSファイルの読込 -->
  <link rel="stylesheet" href="style.css">
</head>
 ```
 
 ## vueの場合
 vue-cliを使用してnpmでインストールすることもできる<br>
 こっちの方が楽な気がする<br>
 ```
 $ npm install -D normalize.css
 ```

 インストールしたらルートとなるVueファイルで使用する
 ```JS
 <script>
 import 'normalize.css'

 export default{
     name: 'App'
 }
 </script>
 ```

 適応したものをみてみると。。。<br>
 {{< figure src="/images/css_space3.png" title="Screenshot" class="center" width="320" height="640" >}}<br>
余白が消えている<br>

elementsで確認してみると<br>
{{< figure src="/images/css_space4.png" title="Screenshot" class="center" width="320" height="640" >}}<br>
marginが無効化されているのが確認できた。<br>

## まとめ
サイトを作る上でhtmlとcssを知ることは重要だと感じた。<br>
bootstrapのようなcssフレームワークを使用する手もあったが今回は柔軟にデザインをしたいというのもあって使用はしなかった<br>
コンポーネントに関してもどこまでの粒度に細分化するか勝手がわからないので、アトミックデザインの勉強もしないとなぁ<br>
とりあえず完成を目指しましょう