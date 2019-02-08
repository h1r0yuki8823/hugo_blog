---
title: "Class"
date: 2019-01-17T12:43:23+09:00
draft: False
---

## Class
JavaScriptのClassについて勉強したので、その忘備録として学習メモを載っけます。<br>
ES5まではクラス機能を使用するのにprototypeを使用して、複雑なコードを書かなければならなかったがES6からclass機能そのものが実装された。<br>
<br>
### classの基本構文
```JS
class Champion{
  name(){
    return 'ガレン'
  }
}


const champion = new Champion();
chamion.name(); //ガレン
```
### classの初期化
他の言語でいうinitializeの機能はconstructorを使用して行う<br>
```JS
class Champion{
  //初期化
  constructor({ role } ){
  	this.role = role;
  }
  name(){
    return 'ガレン';
  }
}

const champion = new Champion({ role: 'Top'});
champion //{"role":"Top"}
champion.name();//ガレン
```

### 継承

```JS
class Garen{
  constructor(options){
  	this.role = options.role;
  }
	useItem(){
  	return '黒斧';
  }
}

class Darius extends Garen {
  constructor(options){
    //Garenクラスのcontracterを初期化するためにsuperを記述
    super(options);
    this.type = options.type;
  }
  
  passive(){
  	return '大出血';
  }
};
const garen = new Garen({role:'top'});
const darius = new Darius({ type: 'fighter', role:'top'});
garen; // {"role":"top"}
darius; //{"role":"top","type":"fighter"}
darius.useItem(); //黒斧 GarenクラスのuseItem()を継承
darius.passive();
```

### 終わりに
JavaScriptでclassが実装されるまではprototypeというものを使用していたらしいが結構面倒な実装方法だなぁと記憶している。<br>ちゃんと勉強したわけではないのでそちらも余裕があれば確認しておこう<br>
今回サンプルコードを書くにあたってリーグオブレジェンドのキャラクター用語を使用して書いてみたが、知らない人からしたら、何が何だか分からないと思う。<br>
まあLoLをやってる人がたまたま見て面白いと思ってくれたら幸いです。<br>
※ガレンとかダリウスって黒斧使うっけ?
