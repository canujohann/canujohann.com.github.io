---
layout: post
title: "Laravel+heroku"
description: ""
category: 
tags: [heroku,laravel,php]
---
{% include JB/setup %}

### Herokuにlavarelアプリをデプロイ

##### .gitignoreの更新

+ composer.lockを.gitignoreファイルから削除


##### Procfile追加

herokuにPHPアプリとして認識されるように、Procfileを追加します。

```
web: vendor/bin/heroku-php-apache2 public
```

##### Mysql設定

Herokuのmysqlプラグイン(無料版)をインストール：

```
$ heroku addons:add cleardb
```

DBの設定ファイルを更新します。上記プラグインをインストールすることによって
**CLEARDB\_DATABASE\_URL**という環境変数が自動的に追加されます。この変数の中にDB情報が入ってます。

> database.php

```php
$url = parse_url(getenv("CLEARDB_DATABASE_URL"));

$host = $url["host"];
$username = $url["user"];
$password = $url["pass"];
$database = substr($url["path"], 1);

'mysql' => array(
      'driver'    => 'mysql',
      'host'      => $host,
      'database'  => $database,
      'username'  => $username,
      'password'  => $password,
      'charset'   => 'utf8',
      'collation' => 'utf8_unicode_ci',
      'prefix'    => '',
  )
```
> 注意点：DB情報を変更すると、ローカルで起動しなくなる！

##### git レポの初期化

```
$ git init
$ git add .
$ git commit -m "Initial commit"
```

##### Herokuアプリの作成+デプロイ

```
$ heroku create
$ git push heroku master
```

> DB migration

```
$ heroku run php /app/artisan migrate
```


#### 参照

[mattstauffer](http://mattstauffer.co/blog/installing-a-laravel-app-on-heroku)

