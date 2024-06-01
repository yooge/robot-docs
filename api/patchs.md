# 热更新
## 0. 准备补丁
### HbuiderX生成加密的补丁文件
修改manifest.json文件的版本号

#### `[步骤]`1. HbuiderX菜单 -> 发行 -> 本地打包 -> 生成app资源
#### `[步骤]`2. HbuiderX菜单 -> 运行 -> 运行到终端 -> 3.生成热补丁


## 1. 自动升级(快捷）
* 在你的VUE项目中，加入如下代码；
* 那么当你的程序执行到这个代码的时候，你的APP应用，就会检查并自动升级。

```js
// 检查,直接升级
const {version} = require('robot-tools'); 

version.onReady = () => { 
	version.checkThenInstall();
};

```

参数：

```js
const {version} = require('robot-tools');
version.checkThenInstall();  //检查并自动升级，有提示文字
version.checkThenInstall('加载中...');  //修改加载提示文字
version.checkThenInstall(false);   //无加载提示， 等于version.install();

//非debug环境(调试基座)才升级
if(version.isDebug == false){
	version.checkThenInstall(); 
};

```


## 2. 先 检查, 然后升级

### 界面代码
```html
<template> 
	<view class="cu-load load-modal" v-if="loadingModal"> 
		<image src="/static/logo.png" mode="aspectFit"></image>
		<view class="gray-text">{{LoadingText}}</view>
	</view>
	<text>当前版本: {{currentVersion}}</text>
	<text>远程版本: {{remoteVersion}}</text>
	<button class="cu-btn bg-green shadow" @tap="upgrade">点我升级</button>
</template>
```
检查代码

```js
const {version, project} = require('robot-tools');

export default {
	data:   {loadingModal: false, currentVersion:'0.0.0',remoteVersion:''},
	created: function() {
	    var that = this;
		this.currentVersion = version.name;

		console.log("开始检查--->");
		version.checkVersion((res) => { 
			that.remoteVersion = res.version;
			if (version.name != res.version) {
				console.log('需要升级');
			} else {
				console.log('不升级');
			}
		});
	},
	methods:{
	   upgrade: function() {
	        console.log("开始升级--->");
			this.loadingModal = true;
			this.LoadingText = '升级中..';
			version.install((status) => {
				this.loadingModal = false;
			});
		} 
    }
};

```

## 3. 存储热补丁到自定义服务器
自定义服务器，请参考 [内核与打包](https://gitee.com/vnool/robot-tools)
### .


⚠️ 提示：APPID，版本号 ⚠️
``` 
const {version, project} = require('robot-tools');

A. project.manifest.id;  // 你代码的id (manifest里的)
A. project.manifest.appid; 
A. project.manifest.version.name; //你代码的版本号
A. project.manifest.version.code;
A. project.manifest; //打印一下看看
A. version.name;  //你代码的版本号 (manifest里的)

//----⚠️ 请用A，不要用B ⚠️----

B. plus.runtime.appid;
B. plus.runtime.versionCode;   //基座版本号(整数)
B. plus.runtime.version;      //基座版本号
B. plus.runtime.innerVersion;
B. plus.runtime.uniVersion;

// A是manifest.json里的内容
// B是基座的信息（调试环境和正式环境，信息不同）
// ⚠️ 请用A，不要用B ⚠️ 
```



 

