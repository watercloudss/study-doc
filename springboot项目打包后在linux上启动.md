# springboot项目打包后在linux上启动

### **第一种方式：**

**Java -jar 项目名.jar**

这种关闭XShell项目就自动停止了，测试使用，不常用。

 

### **第二种方式：**

**nohup java -jar 项目.jar --server.port=8080 > 日志名.log 2>&1 &**

- nohup：不挂断运行命令，退出账号之后继续运行相应的进程

- server.port：配置启动端口号

- demo.log：指定log文件

- 2>&1：2是标准错误，1是标准输出，>把标准错误重定向到标准输出，&相当于标准错误等效于标准输出，即把标准错误和标准输出同时输出到log文件中，可以使用vi或vim去查看运行日志