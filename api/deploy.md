


    
#  打包生成APP：A.云打包 B.本地打包

## A. 云打包生成APP

### 云打包APK
#### `提示：每次打包或生成补丁前，需要生成app资源`
#### `提示：云打包大约需要1-2分钟下载资料到本地`

##### `[步骤]`1. HbuiderX菜单 -> 发行 -> 本地打包 -> 生成app资源
##### `[步骤]`2. HbuiderX菜单 -> 运行 -> 运行到终端 -> 生成APK


#### 自定义manifest.json文件
```js
{		
	"name" : "app名称",
	"appid" : "__UNI__xxxx", /* 一定要改!!!!! */
	"appkey" : "去Hbuilder官方申请!去官方申请!去官方申请",
	/* appkey去官方申请： https://nativesupport.dcloud.net.cn/AppDocs/usesdk/appkey */
	"package" : "com.xxxx.yyy", 

	"logo" : "static/logo.png", /* APP图标，不要改名*/
	"splash" : "static/splash.png", /* 开屏等待页广告，不要改名 */

	"versionName" : "1.0.37", /* 版本号，用于热补丁更新 */
	"versionCode" : 10037,   /* 版本号，用于热补丁更新 */
    "deploy" : "release",     /* 生成正式版APK：release, 调试版基座：debug */
    "encryption": "yes",  /* 是否加密脚本(默认是)*/

}
```

* appid: 在manifest操作界面上生成
* appkey: 去Hbuider官方网址申请： https://nativesupport.dcloud.net.cn/AppDocs/usesdk/appkey
* package: app的包名， 如果要一个手机上安装多个程序，需要修改这个
* SHA1,SHA256,MD5:  申请appkey的时候需要用到，目前是固定值

证书指纹:  


| key | value |
| --- | --- |
| MD5|  BA:A8:08:A4:09:90:BF:AD:12:AD:F3:E6:77:B6:00:BE|
| SHA1 | BF:28:B5:FB:9D:A3:20:27:28:FD:51:77:59:9B:F4:BA:23:E8:A1:88|
|SHA256| 37:6D:A6:C3:BC:D3:F4:A3:FE:65:ED:8C:FD:0C:82:58:EE:6E:43:72:5F:7A:AE:D1:3C:9D:CF:A8:15:76:7E:A3|



* logo:  APP的图片(路径是死的)
* splash: 程序启动的时候的等待页面图片(路径是死的)
* versionCode: 当前版本号
* deploy:  app的发行类型，正式版release，还是调试基座：debug

```
⚠️ 提示：打包的时候，会自动生成最新的热补丁
⚠️ 提示：每次打包前，一定要记得上述[步骤1]
```


## B. 本地(离线)打包，基座源码

### 离线打包，基座源码


⚠️  感谢uni-app官方提供源码⚠️ 

```
链接: https://pan.baidu.com/s/1W0IEokddywK5iqoIx7biKw?pwd=1234 
提取码: 1234
```
#### 1. 用安卓开发环境Android Studio 打开源码
#### 2. 将你uni源码或加密后的代码(包括aj代码)，放到 assets目录中
#### 3. 运行Android Studio打包功能

## 声明
```
⚠️ 声明：
由于安卓开发环境受各种因素影响，操作起比较困难。
请自行解决问题或与其他开发者交流，QQ群:322962890
作者精力有限，在这里无法提供详细的说明文档。
```
```
⚠️ 警告：本项目仅供大家学习交流，请勿用于非法目的 ⚠️
⚠️ 警告：本项目之衍生产品，其用途均与本项目作者无关。 ⚠️
⚠️ 警告：此为开放源码，没有针对任何目标程序；
任何人都可以使用本源码，原作者均不知晓本源码的续用途。 ⚠️
```

