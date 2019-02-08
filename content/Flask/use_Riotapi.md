---
title: "Use_Riotapi"
date: 2019-02-08T12:14:59+09:00
draft: false
---

## riotapiを使ってみたかった
もともとjavaScriptのReactを使って簡単なアプリケーションを作ろうと思い、どんなアプリケーションを作ろうか考えた時に、自分の好きなゲーム「League of Ledends」に使えるメモアプリを作ろうと考えた。<br>
「League of Ledends」通称LoLの開発元のRiot Gamesはriot_apiという試合のデータ等を取得できるAPIを公開している。今回はこれを使用したかった。<br>
最初はReactだけで実装できると考えて簡単にボタンを押したら、APIを叩いて情報を取ってくるものを作った。<br>

## 取って来れなかった。。。
実行してみるとエラーが出てきて取ってこれなかった。調べてみるとCROS関係で駄目みたいだ。CROS関係も勉強しないと。<br>
riot_apiをの使用規約にAPI_KEYを公開するなと書かれている。フロントにkeyを記述するとapi_keyを見られる可能性があるのでapiサーバー側がブロックするよう設定されているようだ。

## flaskを使用
中継apiサーバーを立てて、そのサーバーにriot_apiを叩いてもらうという構想に行き着いた。今回の構想はこうだ<br>
フロント => getリクエスト => 中継サーバー => getリクエスト => riot_api => josnを返す => 中継サーバー => jsonを整えたデータを返す => フロント<br>
という形だ。<br>
軽量のフレームワークは色々あるがpythonにはRiotWatcherというライブラリあるのでflaskを採用した。

## 実際にRiotApiを使用してみた
githubに上げる時にAPI_KEYを公開しないため.envファイルに環境変数を設定してそこを使用するという事をやりたかった。
まずは.envファイルを作りその中に
```
API_KEY = XXXXXXXXXXXXXXXXXXXXXXXXX
```
と記述<br>
settings.pyを作成し、settingsファイルが.envに入っているAPI_KEYを取ってくる処理を書く<br>
その際にはライブラリのpython-dotenvを使用する
```py
import os
from os.path import join.dirname
from dotenv import load_dotenv

dotenv_path = join(dirname(__file__), '.env')
load_dotenv(dotenv_path)

AP = os.environ.get("API_KEY")
```
実際にAPI_KEYを使用するファイルに記述する
```py
from flask import Flask, request, jsonify
from riotwatcher import RiotWatcher, ApiError
import json
import collections as cl 
import pprint 
import settings

API_KEY = settings.AP

watcher = RiotWatcher(API_KEY)
my_region = 'jp1'
me = watcher.summoner.by_name(my_region, 'zer08823')
print(me)
```
今回はriot_apiを使用してsummoner情報を取得する処理を書いてみた。<br>
実行してみるとapiから撮ってきたjsonが出力されるので.envのAPI_KEYを使用できている事が確認出来た

## 終わりに
javaScriptとReactを使用したアプリケーションを作ろうとと考えていたら、結果的にpythonをやるハメになったが、やはりアプリケーションを作るという目標があると勉強していても楽しい。<br>
アプリケーションを作っていけばいくほど知らない事が出てきて学習の必要性を感じるけど、一つ一つ潰していこう