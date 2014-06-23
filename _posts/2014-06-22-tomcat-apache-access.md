---
layout: post
title: "tomcat・apache：アクセス計測"
description: "tomcat・apache：アクセス計測方法"
category: 
tags: [apache,tomcat]
---
{% include JB/setup %}


# tomcat・apache：アクセス計測

bashの基本コマンドで日付順でリストアップして、ユニックでまとめる：

```shell
awk '{print $4}' /your_log_file.log | cut -d: -f1 | sort | uniq -c | tr -d "["
```

crontabに入れて、自動的に送りましょう：

```shell
0 0 */5 * *   awk '{print $4}' /your_log_file.log | cut -d: -f1 | sort | uniq -c | tr -d "[" | mail -s "access for your site these 5 days" xxxx@gmail.com
```

> rogRotateの場合は適当にスクリプトを作ります　↓

```shell
#!/bin/bash
cd /var/logs/apache/
for f in `find . -name "your_file_pattern*"`
do
  number=`cat $f | wc -l`
  echo "$f : $n
done
```

専門じゃないので、いろいろ改善できると思いますが、今日はここまで・・

以上