---
layout: post
title: "jsでHTMLテンプレート"
description: "javascriptでHTMLテンプレートを作る方法"
category: 
tags: [js,html,jsrender,mustache,jquery]
---
{% include JB/setup %}

javascriptでHTMLを生成したい時は変数に入れて、DOMに挿入する：

```javascript
//変数に代入
var xx = "<div id='xxx'>hoge hoge</div><h1>hoge boke</h1>";

//jqueryのHMTLメッソードで挿入
$("#mydiv").html(xx);
```

しかし**HTMLが長ければ長いほど、管理しにくくなります**ので、**テンプレートエンジン**を利用するとよい！

一番メジャーなテンプレートエンジンは:

1. [jsRender](https://github.com/BorisMoore/jsviews.com)
2. [Mustache](http://mustache.github.io/)
3. [Underscore Templates](http://underscorejs.org/)
4. [Embedded JS Templates](http://embeddedjs.com/)
5. ...

今日はjqueryのプラグインとして自分で簡単なテンプレートエンジンを作ってみましょう！

先ずはテンプレートを扱うメッソードを作ります *jqueryのプラグインなので、extendsメッソードを利用*

```javascript

//jqueryプラグイン
$.fn.extend({

    //プラグイン名
    render:function( data ){
    
        //htmlメッソードでテンプレートの内容を取得
        var tmpl = this.html();
        
        //最終的にreturnされる値s
        var result = ""; 
        
        //引数を入れ替えるメッソード
        var create = function(t,d){
          var m = t.match(/\{\{(.+?)\}\}/g) || [], r = t;
          $.each( m, function(i,k){
              var v = d[ k.replace(/\{|\}/g, "") ];
              r = r.replace( k, ( v === undefined ) ? "" : v );
          });
          return r;
        };
        
        //引数がない場合
        if( data === undefined ){ return $( tmpl.replace(/\{\{(.+?)\}\}/g, "") ); }
        
        //引数は配列じゃない
        if( !(data instanceof Array) ){ return $( create(tmpl, data) ); }
        
        //引数は文字列
        $.each( data, function(i,o){ result += create(tmpl,o); } );
        
        return $(result);
    }
});
```

テンプレート自体を作ります。変数は**{{}}**で囲みます。

```html
<script type="text/html" id="template">
 <ul>
     <li> My name : {{name}} </li>
     <li> My age : {{age}} </li>
 </ul>
</script>
```
> typeの宣言はtext/htmlですよ！

メッソードを呼び出す:

```javascript
//単一オブジェクト
var data = { name:"johann", age:"28"};
$("#template").render(data).appendTo($("#Container"));
```

HTML

```html
<div> id="Container"></div>
```

## 参照サイト

[http://goo.gl/7l8hvM](http://blog.mach3.jp/2010/09/10/jquery-render-js.html)

以上！