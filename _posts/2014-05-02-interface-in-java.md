---
layout: post
title: "Java : interfaces"
description: "java interface"
category: 
tags: [java]
---
{% include JB/setup %}

【javaのinterfaceって具体的にいつ使うんですか】と昨日新卒の方にきかれましたので、interfaceのよく見るパターンをまとめてみました。

<span class="alert">注意：初心者向けです！!</span>


###　定義

デベロッパにメソードを実装してもらいたい時にinterfaceを使います。

様々な使い方がありますが、よくみるものは：

1. ライフサイクル (lifecycle)
2. カールバック (callbacks)
3. イベントハンドラー (events handlers)


### ライフサイクル

ほとんどのフレームワークのControllerクラスはライフサイクルパターン（設計モデール）を採用しています。

> androidフレームワークの場合は：

![android lifecycle](http://s1.postimg.org/ejo1plbvj/p2_1.png "android lifecycle")

デベロッパにライフサイクルを守ってもらうために、interfaceを利用します。 

> 実装してもらいたいメソード

```java
public interface ActivityInterface {
	
	//一回目だけ実行
	void onCreate();
	
	//画面が表示される度に実行
	void onResume();
	
	//メモリが不足した時に実行
	void onDestroy();

}
```

> interfaceを実装したControllerクラス

```java
public class myActivity implements ActivityInterface {

	@Override
	public void onCreate() {
		System.out.println("onCreateが呼ばれた！");
	}

	@Override
	public void onResume() {
		System.out.println("onResumeが呼ばれた！");
	}

	@Override
	public void onDestroy() {
		System.out.println("onDestroyが呼ばれた！");
	}

}
```

### コールバック

処理スピードが遅かったり、別のthreadを使ったりするとcallbackを設定すると便利です。

例：音楽のダウンロード

> ダウンロード後に実装されるinterface

```java
public interface DownloadInterface {

	void onDownloadFinished(String fileName);
	
}

```

> ダウンロードされるオブジェクトクラス

```java
public class DownloadObject {

	public void download(String file, DownloadInterface callback){
		
		try {
			
			//データー処理
			Thread.sleep(1000);
			
			//callback
			callback.onDownloadFinished(file);
			
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
	
}
```

> ダウンロードが完了になったら、onDownloadFinishedが呼ばれる

```java
public class TestDownload {

	public static void main(String[] args) {
		
		//オブジェクト初期化
		DownloadObject object = new DownloadObject();
		
		//download method
		object.download("myMusic.mp3", new DownloadInterface(){

			@Override
			public void onDownloadFinished(String fileName) {
				//ダウンロード後 → 実行
				System.out.println(fileName + "がダウンロードされました");
			}
			
		});

	}
```


今回は匿名クラスを使いましたが、別で定義しても問題ないです！

### イベント

イベントでよく使われています (click, hover, double click, drag , drop, ...)

> androidのクリックイベント

```java
Button myButton = new Button();
myButton.setOnClickListener(new OnClickListener() {

	@Override
	public void onClick(View v) {
		// もっと見るクリック時
		System.out.println("クラックされました")
	}
});
```

以上！