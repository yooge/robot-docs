 
# 用JS任意控制手机上的APP
 

## (10分钟就可以上手)

``` 
(10分钟就可以上手)
```
帮助开发者,快速生产友好的控制脚本程序
### 特性

#### 1. 全面支持 uni, VUE 与 aj 的生态 (信息量很大):  
#### 2. 代码加密,
#### 3. 项目自动部署，自动升级，或远程脚本
#### 4. 无目标APP限制
#### 5. 集成了流行的UI界面
#### 
## QQ群： 820320773

### 1. 对app的控制(10分钟就可以上手)
```js
launchApp("微信"); 
click("发现");
click("朋友圈");
sleep(3000);
click(desc("评论"));
```
[效果图1](http://robots.shen-x.com/static/git/1.jpg)，
[效果图2](http://robots.shen-x.com/static/git/3.jpg)，
[效果图3](http://robots.shen-x.com/static/git/6.jpg)，
[效果图4](http://robots.shen-x.com/static/git/5.jpg)，

<img src='http://robots.shen-x.com/static/git/1.jpg' width="100%">
<img src='http://robots.shen-x.com/static/git/9.png' width="200">
<img src='http://robots.shen-x.com/static/git/3.jpg' width="200">
<img src='http://robots.shen-x.com/static/git/8.png' width="200">
 

# 快速开始：
# 点这里 >>> [快速开始](https://github.com/yooge/robot/wiki/now-start)


## 开发环境
### 1. 下载安装开发工具[HbuilderX](https://www.dcloud.io/hbuilderx.html)
推荐下载使用`HbuilderX App开发版` 进行开发

### 2. 克隆或下载源码

#### a.示例项目(入门推荐) 
此方式为整个AJ_VUE演示项目，里面有Color UI组件库，演示，模板等，建议用户可以下载 此项目运行用于查看演示效果，通过里面的示例，可以快速掌握项目用法。

github地址(github)：[https://github.com/yooge/robot](https://github.com/yooge/robot)
	  
gitee地址[网速快]：[https://gitee.com/vnool/autojs-vue](https://gitee.com/vnool/autojs-vue)
	
直接下载zip包：
	  
#### b.空白项目(最小化项目，不含UI交互，高手使用)
 
  此连接为一个空白的AJ_VUE示例工程，无任何ui组件，熟练开发后使用
项目地址：请github搜索 autojs-vue-mini

## 运行示例项目
### 1. 初始化项目文件

#### `[步骤1]`1. HbuiderX菜单 -> 运行 -> 运行到终端 -> 1.初始化/依赖包
#### `[步骤2]`2. HbuiderX菜单 -> 运行 -> 运行到终端 -> 2.更新/安装基座

        
#### 2. 配置调试基座(手机上的app)
##### `[步骤3]` HbuiderX菜单 -> 运行 -> 手机或模拟器 -> 运行基座选择 -> 自定义基座

* 如果忘记勾选，会意外安装错误的手机程序，会提示Robot对象不存在

#### 3. 执行 (调试/运行)
##### `[步骤4]`3.1. 运行到手机 
##### 1. USB线连接手机(需ADB生效) 
##### 2. HbuiderX菜单 -> 运行 -> 手机或模拟器 -> 选择你的手机名字
		
运行到模拟器，wifi连接 (另外聊)

	
    
## 发布/升级，生成APK
### .
#### .
##### `[步骤]`1. HbuiderX菜单 -> 发行 -> 本地打包 -> 生成app资源
##### `[步骤]`2. HbuiderX菜单 -> 运行 -> 运行到终端 -> 生成APK


#### 自定义manifest.json文件
```js
{		
	"name" : "app名称",
	"appid" : "__UNI__xxxx", /* 一定要改!!!!! */
	"appkey" : "去官方申请962a0c8a982ae去官方申请",
	/* appkey去官方申请： https://nativesupport.dcloud.net.cn/AppDocs/usesdk/appkey */
	"package" : "com.xxxx.yyy", 
	"SHA1" : "BF:28:B5:FB:9D:A3:20:27:28:FD:51:77:59:9B:F4:BA:23:E8:A1:88", /* 固定值 */
	"logo" : "static/logo.png", /* APP图标，不要改名*/
	"splash" : "static/splash.png", /* 开屏等待页广告，不要改名 */

	"versionName" : "1.0.37", /* 版本号，用于热补丁更新 */
	"versionCode" : 10037,   /* 版本号，用于热补丁更新 */		
}
```

# vue与控制脚本的交互

建议先大致了解Vue项目结构后进行

```
* 项目主体UI：pages/   各种UI样式举例(可忽略)
* 项目主体UI：pages/robots/		2个启动界面举例 
* 项目AJ脚本：static/robots/	(默认)用于存放控制脚本代码
```

## 从UI启动控制脚本脚本(举例)
### 不想看例子的人，请直接看这两个路径的源码
```
pages/robots/
static/robots/
```
#### 【第1步】. 新建js脚本脚本： 在项目路径~/static/robots下新建文件demo.js
```js
launchApp("微信"); 
click("发现"); 
click("朋友圈");
desc("评论").findOne().click();
click("赞");
```
 

#### 【第2步】. 修改页面内容 pages/index/index.vue
```html
<template>
<view> 
	<button class="cu-btn bg-green shadow" @tap="test">启动</button>
	<button class="cu-btn bg-green shadow" @tap="stop">停止</button>
</view>
</template>
<script> 
var {autojs} = require('robot-tools');
export default {
    methods: {
        test() {
            var param = {
                file: 'demo.js', //文件路径为./static/robots/demo.js 
            }
            autojs.stop();
            autojs.start(param);
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
.

## 参数解释

### 在VUE页面，立即执行控制脚本代码
```js
var {autojs} = require('robot-tools');

//立即执行控制脚本脚本（无需js文件或执行js脚本，可立即执行本代码）
autojs.exec(function(){ 
    //在vue的代码文件里，直接执行脚本代码，
    console.log('开始振动 ');
	console.show();
	device.vibrate(2000);
    launchApp('抖音');
   //click('朋友圈');
});
//偶尔用一下，不要太依赖
//todo:
//1. 作用域在控制脚本内，此处暂不支持对VUE的访问，下一版补上；(如果需要访问VUE，看下面的start方法)
//2. 如果需要用require方法引用其他的js文件，请先用autojs.robot.setJsDir("/sdcard/")设置工作路径；
//   或者用autojs.init({file:'demo.js'})设置个假的文件，工作路径参考下文
```
### 执行控制脚本文件
```js
var {autojs} = require('robot-tools');
var param = { 
	file: 'demo.js', //[必选],脚本脚本(static/robots/demo.js)，或绝对路径/sdcard/xxx.js，或远程URL(也可以用发布的打包加密代码)
	vue:  this, //可选, 将本vue对象传递给脚本
	arguments: {}, //可选, json,传递给脚本的参数。[提示]如果不传递，则系统会默认使用'当时'的vue的data数据；
	onMessage: (data)=>{}, //可选,回调函数，脚本给VUE发送消息， 感觉快淘汰了
	start: ()=>{}, //可选,脚本启动事件
	finish: (obj)=>{},//可选,脚本执行完毕事件
	fail: (msg)=>{},//可选,脚本发生意外事件
}
/*

file:  
//1. 脚本脚本(static/robots/目录下的demo.js)，
//2. 或绝对路径/sdcard/xxx.js，
//3. 或远程URL(也可以用发布的打包加密代码)

arguments: 
//可选, json,传递给脚本的参数。
//可以在控制脚本脚本中用app.args获取
//如果不传递参数，则系统会默认传递'当时'的vue的$data数据；
//如果控制脚本想动态获取vue的$data的数据，请往下看
*/

//启动脚本
autojs.start(param); 

//停止脚本
autojs.stop();

//仅设置初始化参数，不执行代码
autojs.init(param); 
//根据上面设置好的参数，执行代码； 也可以在悬浮脚本上点启动按钮
autojs.start(); 

autojs.menu.show(); //显示悬浮脚本图标
autojs.menu.hide(); //隐藏悬浮脚本图标
autojs.menu.move(x,y); //移动悬浮脚本图标
autojs.menu.close(); //隐藏悬浮脚本图标
autojs.showMenu(param); //执行脚本并显示脚本图标

//在当前已经运行的脚本中，立即执行小段脚本(需要在xxx.js脚本启动后，再调用该方法)
autojs.eval(function(){ 
    //在vue的代码文件里，直接执行脚本代码，
   launchApp('抖音');
   sleep(4000);
   console.log(text('我'));
   //click('朋友圈');
});



//立即执行控制脚本脚本（代码可以是字符串）
autojs.exec(function(){
   console.log(device.getIMEI());
   launchApp('抖音'); 
 }
);
autojs.exec(
 `
   console.log(device.getIMEI());
   launchApp('抖音'); 
 `
);


var isEnabled = autojs.permission();//检查是否启动了无障碍

```
#### js脚本获取VUE发过来的参数(启动脚本时传递的)
```js
app.args //json对象, 
app.arguments  //参数字符串

//内置参数
app.args.scriptStartFrom //null 或 'menu'； 可以通过不同的启动方式，执行不同的代码
app.args._debug //调试模式，还是正式模式
```
#### js脚本给VUE层发消息
```js
app.post2host("hello vue"); 
//js脚本用这个方法给VUE层发消息,(在上面的onMessage中接收消息)
```

#### js脚本脚本直接访问VUE页面对象
```js
app.vue  //控制脚本直接访问vue的对象，上面传递进来的对象this(或别的对象)
app.vue.abc   //访问data里的abc变量
app.vue.abc = 999; //给data里面的abc赋值
app.vue.test() //访问VUE的methods里面的test函数。 此用法可以淘汰上面的onMessage回调

```
#### 例index.vue
```html
<template>
<view> 
	{{abc}}
</view>
</template>
<script> 
var {autojs} = require('robot-tools');
export default {
    data: {
        abc: 123
    }
    methods: {
        test() {
            console.log('autojs call test');
        }
    }
}
</script>
```




 
## QQ群：  820320773
 
```js
  如果喜欢这个项目，可以请赠我一包华子 
```



## 其他链接
[AutoJS](https://hyb1996.github.io/AutoJs-Docs/#/)：全接口支持

[VUE](https://cn.vuejs.org/)：著名的渐进式JavaScript框架(傻瓜->高手),

[color-Ui](http://demo.color-ui.com/)：优雅的前端视觉交互设计(默认内置，也可以换成其他UI框架)

[HTML5plus](http://www.html5plus.org/doc/)：让JS拥有与App一样的能力标准

[组件](https://uniapp.dcloud.io/component/README)，[API](https://uniapp.dcloud.io/api/README)，
[框架](https://uniapp.dcloud.io/collocation/App)：各种第三方的APP原生能力

[插件社区](https://ext.dcloud.net.cn/)，
[云开发](https://uniapp.dcloud.io/uniCloud/README)，
[uni开发者社群](https://dcloud.io/), 开发者600万+， 12亿手机端月活用户
