# **Shell**

[toc]
##  基本命令

### 1.which   

查看shell使用的路径

### 2.where  

查看shell所有的路径

### 3.echo   

返回输入值/如果是变量，会返回路径（冒号外加汉字只返回汉字）

### 4.history  

查看过去的命令历史，输入数字可以查看条数（histoty -5 可查看过去的五条）

### 5.data   

查看日期，不是内建命令

### 6.pwd   

显示当前所在目录        

   shell当前工作路径的节选

| .    当前目录   |
| --------------- |
| ..   上一个目录 |
| …  上上一个目录 |
| -   前一个目录  |
| ～ 家目录       |



### 7.cd     

改变shell工作目录/与shell当前路径可结合使用

### 8.ls     

**列出当前文件夹所有文件 **

  ls -a   列出包括隐藏的文件

  ls -l    查看权限

### 9.cat   

 显示一个文件内容

### 10.clear  

清空

### 11.mkdir 

当前目录创建文件夹

### 12.touch 

创建文本文件

### 13.rm    

从硬盘移除文件（不可在回收站找回）

   rm -d  移除文件夹

   rm -rf  ⚠️慎用，删库跑路

### 14.mv   

移动文件  

   （mv  xxxx  zzz）  是将xxx移动到zzz

### 15.cp  

复制文件

   （cp  xxxx  zzz）  将xxx复制且改名为zzz

### 16.man  

查看帮助文档

   —help （两个’’-‘’，man无法使用的备用）

### 17.ps kill

关于进程，ps查看，可以百度作用







## 其他Shell操作



### **1.输出流重定义**

**在终端用命令创建本文及添加内容/echo**

**需要注意初次添加和再次添加的区别**

```shell
 touch wm.txt
 vim wm.txt
```

添加完文本后再次添加，一种是vim进去继续添加，另外一种是echo xxx >> wm.txt 这表示将xxx添加进wm.txt文本的末尾

### **2.⌃D**

退出当前的shell

### **3.文件和文件夹权限**

**1.chmod**

使用`chmod`修改文件和文件夹权限（`chmod`,`change mode`,修改文件，文件夹权限）

- **文字设定法**

```shell
$ chmod [u][g][o][a]  [+|-|=] [rwx] file
$ chmod  ug+w,O-x              a.txt  # owner及同组增加写权限，其他用户删除执行权限
```
`u`：owner		`g`:同组用户		`o`:其他用户		`a`:所有用户

`r`:  read		  `w`:write				`x`:excute		

- **数字设定法**

```shell
$ chmod [mode] file
$ chmod  644   my.txt  #owner可读写，同组和其他用户只可读
```

`mode`为3位八进制数，每位由各权限按权重相加得到。从左往右owner、同组、其他用户权限

`rwx`对应的权重分别是`4`,`2`,`1`

`rwx`分别占据三位

```shell
u = 6 = 4+2 = r+w #owner可读可写
```

**注：**在使用此命令是，权限少给一点



**2.xattr**

macOS 中安装一些修改版或破解版软件，由于系统识别到这个 app 可能有问题所以给它加上了 com.apple.quarantine 隔离属性阻止了他的运行。
如果我们需要运行它，就需要删除 app 的 com.apple.quarantine 属性，可以使用 xattr 来处理。

```shell
例子:xmind无法打开
sudo xattr -r -d com.apple.quarantine /Applications/XMind.app
```



### 4.查看Dns
- **使用命令 nslookup**

```shell
$ nslookup store.chanjet.com
```

-  **查看文件/etc/resolv.conf**
```shell
$ cat /etc/resolv.conf
```





## shell脚本















