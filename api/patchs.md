# 热更新
## 0. 准备补丁
### HbuiderX生成加密的补丁文件
修改manifest.json文件的版本号

#### `[步骤]`1. HbuiderX菜单 -> 发行 -> 本地打包 -> 生成app资源
#### `[步骤]`2. HbuiderX菜单 -> 运行 -> 运行到终端 -> 生成热补丁


## 1. 直接升级(快捷）

```js
// 直接升级
require('robot-tools').version.checkThenInstall();

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
