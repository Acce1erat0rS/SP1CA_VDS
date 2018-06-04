# SP1CA_VDS

## 文件内容介绍：
Bootstrap(Build_17615.1).exe 导引程序，用于协调多进程
Client Release 客户端的Release版本程序，但是似乎需要一些动态库
实习文档：系统的各个文档，每个功能的流程图在详细设计中
总体流程及模块设计在概要设计说明书中
OS_Project:客户端控制台窗口项目，使用VS2015开发
Bootstrapper Project：导引程序项目，使用VS2015开发

请先启动Bootstrap后再开启Client，并等待Client全部关闭后再推出Bootstrap程序

## 实现亮点：
### 多用户登录系统

实现了多用户，每个用户有用户名与密码，密码在文件系统中按照hash处理之后的值存放与比对，同时在输入密码的时候专门实现了密码字符的遮盖，同时可以支持退格。
### 密码加密存储
密码采用BKDRhash函数处理，没有将用户的密码直接存储到虚拟磁盘中。

### 文件权限系统
同时模仿linux的权限系统，每个文件用一个3位八进制整形存储所有者，所属群组以及所有人的权限。同时实现了更改权限指令。

### 多线程的实现
并行处理采用了共享内存的方式，其中bootstrapper开启了一块名字为SignalVariable的共享内存空间，之后每一个新开启的客户端在试图读取，写入文件的时候都会检查这个共享变量并对其进行加锁。访问完文件后进行解锁。

### 相对完整的用户界面
设计并实现了大量的指导文本与语句，并对控制台进行了初步的美化，专门设计了一个logo。同时对命令行开头部分，模仿Linux的shell将当前用户以及当前路径的信息嵌入了进去。

### 多种的路径寻址方式
支持相对路径与绝对路径，同时支持各种的不同表示（注：绝对路径在系统中以\\开头）。
