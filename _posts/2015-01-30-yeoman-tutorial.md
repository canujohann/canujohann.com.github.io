---
layout: post
title: "yeoman入門"
description: "yoemanでウエブプロジェクトを作りましょう"
category: 
tags: [apache,tomcat]
---
{% include JB/setup %}

Yeomanは、WebページやWebアプリケーションなどの制作を迅速にはじめることができ、制作中のいろいろな作業をサポートしてくれるツールセットです。
インストールして、実際にプロジェクトを作ってみましょう。


> インストール

```
#install grunt
npm install -g grunt-cli

#install yo with npm
npm install -g yo bower
```

> 必要なジェネレータのインストール

```
#install some Scaffolding 
npm install -g generator-webapp
npm install -g generator-angular
```

> プロジェクトディレクトリの作成(Scaffold)

```
#project creation
yo webapp
yo angular
```

> サーバー起動 (localhost:9000)

```
#launch server (Gruntfile included in project)
grunt server
```

## おまけコマンド

> bower

```
#search,add,update dependencies
 bower search <dep>
 bower install <dep>..<depN>
 bower list
 bower update <dep>
```

 > GULP / GRUNT

```
# サーバー起動
$ gulp serve / grunt serve

# 単体テスト
$ gulp test / grunt serve

# ビルド
$ gulp /grunt
```