后端人员修改了protos,前端应该注意点什么？

1.确认对方修改或新增了什么？

2.工具的使用：

​	1、保证工具选择的protos是对应上当前项目的protos

​	2.  svn上的项目地址，可以自行下载，使用。（注意，创建时下载的目录，避免直接拉到文件夹的目录）；

​	3. 导出protos,是会生成ptotos.ts这个类，值得注意的是，如果导出接口，是不会覆盖原有的。具体是什么样子：

也就是，需要自行修改对应的接口，出现报错信息，（接口报错）要跟后端确认，相关传参，数据类型等信息方可排出错误。 

3.关于接口的理解：

接口，其实也是一个类，透过**配置相关库文件**之后，在前端项目中，直接，调用该类，便可以与后端的服务器进行通信。（数据接发）

**但是，具体怎样配置，这个要搞懂**