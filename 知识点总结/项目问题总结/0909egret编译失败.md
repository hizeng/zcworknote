##### 1.[启动调试失败 TypeError: Cannot read property 'exitCode' of null](https://bbs.egret.com/thread-49288-1-1.html)

解决方法：

在白鹭自带的编译器直接构建，清理项目 具体原因不明

//项目中现在存在很多，由于版本升级导致再编译阶段出现太多不明原因的报错 0924



**2.Property 'bitmapData' does not exist on type 'Image'. Did you mean '$bitmapData'?**

**Property '$bitmapData' does not exist on type 'Image'. Did you mean 'bitmapData'?**

神奇报错:

解决方案：将eui.image类型，改为any类型；

