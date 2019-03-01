## Linux 基本概念和操作
> Linux 是源于 UNIX 的一种 UNIX-LIKE 系统


---
- #### 文件系统
  ##### Windows 系统的文件系统是FAT32/NTFS，而 Linux 系统的是 EXT4。两者不兼容，不能互相识别对方类型的数据。


---
- #### 用户权限
  ##### sudo (Superuser Do)
  ##### su (Switch User)



---
- #### pwd指令用于获取目前所在的工作目录的绝对路径



---
- #### 切换用户
  ```
  sudo -iu newUerName   // 切换到 newUserName 账户，用 exit 或 logout 退出  
  sudo                  // 暂时切换到超级用户，默认时间为15分钟   
  su newUserName        // 切换到 newUserName 账户  
  ```



---
- #### 根目录
  ##### cd /       进入根目录
  ##### cd ~       进入当前用户目录





---
- #### 清屏
  ##### Linux 下使用 clear (本质是翻页，向上翻依然存在记录)
  ##### Windows 下使用 cls




---
- #### Linux 中的引号
  ##### 在 shell 中双引号叫 soft quote，单引号叫 hard quote。
  ##### 双引号中的变量依然会被解析，而单引号会将所有内容解释成字符串。
  ```
  // 定义变量 name
  [root@linux ~]# name = foo
  [root@linux ~]# echo $name
  foo

  // 使用双引号
  [root@linux ~]# echo "$name"  
  foo

  // 使用单引号
  [root@linux ~]# echo '$name'
  $name
  ```





---
- #### 查看文件内容
  ##### cat filePath
  ```
  cat /etc/issue     // 查看服务器系统的发行版本
  ```






---
- #### 更改文件权限
  ##### chmod
  ```
  -rwxrwxrwx  其中，r=4, w=2, x=1
  chmod 777 fileName    // 三个数字分别表示User、Group、及Other的权限 7 表示 4+2+1。此命令赋予所有人，操作文件的所有权限 
  chmod 600 fileName    // -rw------- 文件拥有者可读写不可执行，其他人不可读写执行
  ```





---
- #### 实时查看文件打印
  ##### tail -f filePath




--- 
- #### 文本查找
  ```
  // 从 fileName 文件中过滤出带有关键词 'keyWords' 的记录，从上往下显示
  grep 'keyWords' filePath/fileName | head

  ```







---
- #### vim 浏览文件翻页
  ```
    ctrl + b     // back    往上一页
    ctrl + f     // foward  往下一页

    ctrl + u     // up      往上半页
    ctrl + d     // down    往下半页

    ctrl + e     // 往下一行
    ctrl + d     // 往上一行

    zz           // 光标所在行移到中间
    zb           // 光标所在行移到底部
    zt           // 光标所在行移到顶部

    G            // 移动到文件底部
    gg           // 移动到文件顶部
  ```




---
- #### vim 操作文本
  ##### vim 选择文本
  ```
    v           从光标当前位置开始，光标所经过的地方会被选中，再按一下 v 结束。
    V           从光标当前行开始，光标经过的行都会被选中，再按一下 Ｖ 结束。
    Ctrl + V    从光标当前位置开始，选中光标起点和终点所构成的矩形区域，再按一下 Ctrl + V 结束
  ```



---
- #### vim 搜索
  ```
    ?keyWord        // 从下往上搜索
    /keyWord        // 从上往下搜索

    n               // 下一个搜索到的关键字（方向根据上面提到的 ？和 / 来确定）
    N               // 上一个搜索到的关键字（方向根据上面提到的 ？和 / 来确定）

    :set hls        // 打开高亮
    :set nohls      // 关闭高亮
    
    set hlsearch    // 临时开启高亮，关闭文档后失效
  ```




---
- #### 查看文件大小
  ```
     df -h       // 用于显示目前在Linux系统上的文件系统的磁盘使用情况统计

     du -sh      // 用来查看当前文件或目录所占磁盘空间的大小

     // -h 代表用人类（human）可读单位展示结果
     // --max-depth=X    其中X用于指定深入的层数
     // -a或-all   用于详细列出目录和目录下子目录和文件占用磁盘空间的大小
     // -s或--summarize   仅显示当前目录总计大小

     stat fileName/folderName   // 查看文件/文件夹的基本信息，比如 大小、读写权限、创建/修改时间
  ```




---
- #### 删除文件
  ```
    rm -f filePath     // 强制删除文件
    rm -r dir          // 递归删除目录下所有文件，危险操作
  ```




---
- #### 查找文件
  ```
  　find / -name fileName          // -name 表示按照文件名查找
    find . -name name* -ls         // 查找当前目录下所有名字以 name 开头的文件，并显示其详细信息
    find /home -type d -delete     // -type 表示按照类型查找， d 表示目录， f 表示普通文件
  ```



---
- #### 查看端口状况
  ```
    netstat -apn | grep portNo     // 返回端口的使用情况
  ```




---
- #### 查看进程
  ```
    ps -ef | grep tomcat    // ps 表示 process 命令. e参数表示显示所有进程，f参数表示全格式展示结果
    
    以上命令返回格式如下：
    UID     // 用户ID、但输出的是用户名 
    PID     // 进程的ID 
    PPID    // 父进程ID 
    C       // 进程占用CPU的百分比 
    STIME   // 进程启动到现在的时间 
    TTY     // 该进程在那个终端上运行，若与终端无关，则显示? 若为pts/0等，则表示由网络连接主机进程。 
    CMD     // 命令的名称和参数
  ```
  
  

---
- #### 结束进程
  ```
    kill -9 PID   // 9 是发送给进程的一个信号，表示强制执行
  ```

---
- #### ping
  ```
   /* 只能用域名或IP */
   ping www.163.com      
   ping 10.160.18.44  

   /* 不可以跟上协议和端口 */
   ping http://www.163.com    // 报错
   ping 10.160.18.44:8080     // 报错
  ```
  
  
  
--- 
- #### telnet
  ```
  telnet 10.193.13.5 8080
  ```
