---
title: "Promise"
date: 2019-01-07T23:13:05+09:00
draft: false
---

## Promise
JavaScriptのPromiseについて勉強したので、その忘備録として学習メモを載っけます。

### 概要
JavaScriptには実行を止めるということが出来ない、なので長い処理を扱いたい場合はある処理を実行して、その後に続きの処理を行うというを順序を行うためにPromiseを利用する。<br>
promiseには３つの状態が存在する<br>
・unresolve 未解決 処理をが終わるのを待っている状態<br>
・resolved 成功　処理が終わって成功している状態<br>
・rejected 失敗 処理が終わって失敗している状態<br>

サンプルを下に記載

```JS
const promise = new Promise((resolve, reject) => {
  //成功時
  resolve();
  //失敗時 エラーをスローする
  reject();
});

promise
  //resolve時に実行される。
  //登録されているthenを全て呼び出す
  .then(() => console.log('成功です。'))
  .then(() => console.log('複数実行することも可能'))
  //reject時に実行される
  .catch(() => console.log('失敗しました'))
```

Promiseのユースケース
```JS
promise = new Promise((resolve, reject) => {
  //３秒後に実行
    setTimeout(() => {
        resolve();
    }, 3000)
});

promise
    .then(() => console.log('処理が完了しました。'))
    .catch(() => console.log('処理が失敗しました。'))
```
APIサーバーなどにリクエストを送ってその結果が返ってきてから次の処理を実行する時に利用される。


### fetch
fetchはpromiseを使用してAjaxのリクエストを行える

```JS
url = "https://jsonplaceholder.typicode.com/posts/";

fetch(url)
    .then(response => response.json())
    .then(data => console.log(data));
```
ただしfetchは使用しにくい部分がある。

```JS
//コードはエラーとなるが。。。
url = "https://jsonplaceholder.typicode.com/posts12345/";

fetch(url)
    //エラーだがこっちの処理が行われている
    .then(response => console.log(response))
    //catchのコンソールログが表示されない
    .catch(error => console.log('問題発生',error));

```

エラーだがcatchが実行されていないので分かりにくい。<br>
Ajaxのリクエストを行う場合はサードパーティのライブラリを使用する方が現状良い。<br>
サードパーティ製のライブラリの有名どころはエラーはcatchを通るようになっている。<br>