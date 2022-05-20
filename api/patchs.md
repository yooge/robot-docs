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
// 直接升级
require('robot-tools').version.checkThenInstall();

```

参数：

```js
const {version} = require('robot-tools');
version.checkThenInstall();  //检查并自动升级
version.checkThenInstall('加载中...');  //修改加载提示文字
version.checkThenInstall(false);   //无加载提示

//非debug环境(调试基座)才升级
if(version.isDebug == false){
	version.checkThenInstall(); 
};

```


## 2. 检查 & 更新

### 2.1 检查版本号
```
const {version} = require('robot-tools');

function checkVersion(){
	// #ifndef APP-PLUS
	return;
	// #endif
	plus.runtime.getProperty(plus.runtime.appid, (wgtinfo) => {
		var version_code = wgtinfo.version;
		console.log('当前程序的版本号:' + version_code); 
		console.log(wgtinfo); 
		console.log(plus.runtime);
		console.log(version.manifest());

		version.checkVersion(version.manifest().id, (res) => {
			console.log('最新补丁的版本号:' + res.version);
			if (version_code != res.version) {
				console.log('需要升级');
			} else {
				console.log('不升级');
			}
		});
	});
} 
```


### 2.2 执行升级

```html
<template> 
	<view class="cu-load load-modal" v-if="loadingModal"> 
		<image src="/static/logo.png" mode="aspectFit"></image>
		<view class="gray-text">{{LoadingText}}</view>
	</view>
	<button class="cu-btn bg-green shadow" @tap="upgrade">点我升级</button>
</template>
```

```js
const {version} = require('robot-tools');

export default {
	data:{loadingModal: false}, 
	methods:{
	   upgrade: function() {
		this.loadingModal = true;
		this.LoadingText = '升级中..';
		version.install((status) => {
			this.loadingModal = false;
		});
    }
};

```

