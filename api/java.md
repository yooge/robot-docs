# 与Java或Android交互
##  1. 直接使用Android的API
举例： 接受广播包
```js
const IntentFilter = android.content.IntentFilter;
const BroadcastReceiver = android.content.BroadcastReceiver;

var filter = new IntentFilter();
filter.addAction("android.net.conn.CONNECTIVITY_CHANGE"); // 监听网络变化
// 替换为其他的广播事件 
var receiver = new BroadcastReceiver({
	onReceive: function(context, intent) {
		console.log('监听到广播包: 网络变化');
		console.log(intent);
	}
});
context.registerReceiver(receiver, filter);

```

##  2. 加载Jar包 
* `path` {string} jar文件路径

加载目标jar文件，加载成功后将可以使用该Jar文件的类。
```
// 加载jsoup.jar到内存
runtime.loadJar("./jsoup.jar");
// 使用jsoup解析html类
importClass(org.jsoup.Jsoup);
log(Jsoup.parse(files.read("./test.html")));
```

(jsoup是一个Java实现的解析Html DOM的库，可以在[Jsoup](https://jsoup.org/download)下载)

## 3. 加载Dex包(path)
* `path` {string} dex文件路径

加载目标dex文件，加载成功后将可以使用该dex文件的类。

因为加载jar实际上是把jar转换为dex再加载的，因此加载dex文件会比jar文件快得多。可以使用Android SDK的build tools的dx工具把jar转换为dex。
