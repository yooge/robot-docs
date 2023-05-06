# Q & A

## 问题交流QQ群：714554851

 

## 1.运行基座时报错：Robot对象不存在
  初始化项目环境配置 不对：
  手机上未安装正确的调试基座，会提示Robot对象不存在
  请参考：[Demo,调试,运行](hbuilder.html#hbuilder_1) 

## 2.打包异常
  1. 本项目仅供学习交流，不提供打包技术支持 [deploy.html](deploy.html)
  2. 离线打包，请学者自行研究方法，不提供技术支持
  
## 3. Auto.js自带的模块和函数中没有的功能如何实现

由于Auto.js支持直接调用Android的API，对于Auto.js没有内置的函数，可以直接通过修改Android代码为JavaScript代码实现。例如旋转图片的Android代码为：
```
import android.graphics.Bitmap;
import android.graphics.Matrix;

public static Bitmap rotate(final Bitmap src,
                            final int degrees,
                            final float px,
                            final float py) {
    if (degrees == 0) return src;
    Matrix matrix = new Matrix();
    matrix.setRotate(degrees, px, py);
    Bitmap ret = Bitmap.createBitmap(src, 0, 0, src.getWidth(), src.getHeight(), matrix, true);
    return ret;
}
```
转换为JavaScript的代码后为：
```
importClass(android.graphics.Bitmap);
importClass(android.graphics.Matrix);

function rotate(src, degrees, px, py){
    if (degrees == 0) return src;
    var matrix = new Matrix();
    matrix.setRotate(degrees, px, py);
    var ret = Bitmap.createBitmap(src, 0, 0, src.getWidth(), src.getHeight(), matrix, true);
    return ret;
}
```
有关调用Android和Java的API的更多信息，参见[Work with Java](https://developer.mozilla.org/zh-CN/docs/Mozilla/Projects/Rhino/Scripting_Java)。