
# vue与控制脚本的交互 

建议先大致了解Vue项目结构后进行

```
* 项目主体UI：pages/   各种UI样式举例(可忽略)
* 项目主体UI：pages/robots/		2个启动界面举例 
* 项目AJ脚本：static/robots/	(默认)用于存放控制脚本代码
```

## 从UI启动控制脚本(举例)

### 项目文件

不想看例子的人，请直接看这两个路径的源码

```
pages/robots/
static/robots/
```
#### 【第1步】. 新建robotjs脚本： 
` 在项目路径~/static/robots下新建文件demo.js `

```js
launchApp("微信"); 
click("发现"); 
click("朋友圈");
desc("评论").findOne().click();
click("赞");
```
 

#### 【第2步】. 修改UI界面内容 

页面: pages/index/index.vue

```html
<template>
<view> 
	<button class="cu-btn bg-green shadow" @tap="start">启动</button>
	<button class="cu-btn bg-green shadow" @tap="stop">停止</button>
</view>
</template>
<script> 
var {autojs} = require('robot-tools');
export default {
    methods: {
        start() {
            autojs.start({
                file: 'demo.js', //文件路径为./static/robots/demo.js 
            });
        },
        stop(){
          autojs.stop();
        }
    }
}
</script>
```
#### 【第3步】 从Hbuilder中启动app，

```
菜单：运行/手机或模拟器/选择你的手机
```
```
(此时手机上会自动安装调试app)，
APP启动后，请为这个app授权”无障碍“，”悬浮窗“，”从后台启动”
```
 

## QQ群：  820320773
 
```js
  如果喜欢这个项目，可以请赠我一包华子 
```




