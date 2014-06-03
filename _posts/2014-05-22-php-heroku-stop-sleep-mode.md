---
layout: post
title: "Herokuのスリープ状態対策 （PHPアプリ）"
description: "Herokuのスリープ状態対策 （PHPアプリ）"
category: 
tags: [heroku,laravel,php]
---
{% include JB/setup %}

## Herokuのスリープ状態対策 （PHPアプリ）

herokuの無料アカウントの場合はアプリ毎に一つのdynoが設定されていて、一時間以内にアクセスされなければスリープモードに入ってしまう（アクセスする時は正常モードに戻るまで凡そ30秒かかります）。無料アプリとはいえ、productionで利用していれば、致命的になりますので、対策を考えてみました。

Railsアプリは New relicプラグインをインストールすれば、簡単に防げますが、PHPの場合は対応していないため、pingでやります。

```
$ crontab -e 
*/45 * * * * ping -c 1 myserver.com > /dev/null 2>&1
```

45分間隔でpingするという簡単なやり方です！


kaffeineというサービスも存在してますが、実際に使ったことがありません！

[kaffeine](http://kaffeine.herokuapp.com/)