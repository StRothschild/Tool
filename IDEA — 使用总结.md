## IDEA 使用总结

- #### Compile & Rebuild & Make
  ##### Compile：对选定的目标（Java 类文件），进行强制性编译，不管目标是否是被修改过。
  ##### Rebuild：对选定的目标（Project），进行强制性编译，不管目标是否是被修改过，由于 Rebuild 的目标只有 Project，所以 Rebuild 每次花的时间会比较长。
  ##### Make：使用最多的编译操作。对选定的目标（Project 或 Module）进行编译，但只编译有修改过的文件，没有修改过的文件不会编译，这样平时开发大型项目才不会浪费时间在编译过程中。





---
- #### 快捷键
  ##### Ctrl + Z                    撤销上一步
  ##### Ctrl + shift + Z            撤销上一步的操作（可以撤销 Ctrl + Z）
  ##### Ctrl + Y                    在 IDEA 中是删除当前行， 在 Eclipse 中相当于 IDEA 中的 Ctrl + shift + Z  

  ##### Ctrl + E：                  弹出最近编辑的文件列表
  ##### Ctrl + R：                  替换文本
  ##### Ctrl + F：                  查找当前文档
  ##### Ctrl + Shift + F：          查找整个工程
  ##### Ctrl + N：                  查找类
  ##### Ctrl + Shift + N：          查找文件

  ##### Ctrl + Home：               到达文件顶部
  ##### Ctrl + End：                到达文件底部

  ##### Ctrl + /：                  使用单行注释符（'//'）
  ##### Ctrl + Shift + /：          使用多行注释符（'\/* \*/'）
  ###### 这里需要注意，HTML 的注释方式是 \<!-- 注释内容 -->，FTL 的注释方式是 <#-- 注释内容 -->

  ##### Ctrl + Shift + V：          打开剪贴板
  ##### Ctrl + alt + 方向键：       跳到 上/下 一步所在的位置

  ##### Ctrl + Alt + L：            代码自动格式化   
  ##### Ctrl + Alt + H：            打开当前方法的调用树/被调用树 

  ##### Ctrl + Shift + F9           重新编译当前文件
  ##### Ctrl + F9                   重新编译当前项目   







---
- #### 端口冲突
  ##### 通过命令  netstat -o  查询当前端口的占用情况和PID
  ##### 通过命令  taskkill /PID XXX 来结束 PID 为 XXX 的进程（taskkill /F /PID XXX 表示强制终止）






---
- #### 调试
  ##### F7：进入到本行调用的函数体中
  ##### F8：执行到下一行
  ##### F9：执行到下一个断点

  ##### Alt + F7：查找当前选中的方法的被调用情况
  ##### Alt + F8：在当前断点处打开调试框，可以进行变量调试
  ##### Alt + F9：执行到光标所在点。这个操作很容易出现程序执行完，但还没有到达光标位置的情况（光标位置在当前断点上方）。这样的话，由于本次 debug 没有结束，下次再开始 debug 时就无法进入断点。所以尽量别用这个功能。





---
- #### 控制台 log 输出长度控制
  ##### IDEA 控制台可以保留的输出大小默认为 1024 KB，如果要取消这个大小（长度）限制，可以更改 IDEA 的配置文件。

  ##### IDEA 的配置文件 idea.properties 在安装目录下的 bin 目录中，修改文件中 idea.cycle.buffer.size 的值为 disabled，保存重启 IDES 即可。





---
- #### 设置 indent（缩进）
  ##### IDEA 的缩进是根据文件类型来设置的，不同的文件类型可以设置不同的缩进方案，一般是 2 space 或者是 4 space。
  ##### File ——> settings  ——> Settings  ——> Editor ——> Code Style






---
- #### 识别没有内置的文件类型
  > 部分自定义或罕见的文件类型，在 IDEA 中无法识别时，可以自定这些文件类型和识别方式。

  ##### 1. File ——> settings ——> Editor ——> File Types
  ##### 2. 在上半部分中选择将要把文件识别成的目标类型，下半部分选择文件类型
  ##### 3. 例如：上半部分选择 text, 下半部分添加 \*.mcss。则原来不识别的 mcss 文件就会被识别成 text 文件。




---
- #### 重置某文件的类型
  > 如果错误的定义了某文件的类型，通过删除再重新创建同名文件的方法来改正是无效的，IDEA依然会将该文件识别为之前定义的文件类型。

  ##### 1. File ——> settings ——> Editor ——> File Types
  ##### 2. 在下半部分的 Registered Patterns 中删除该文件名，生效后 IDEA 会重新识别该文件。







---
- #### Ctrl + Shift + N 查找文件失效
  ##### 通过 Ctrl + Shift + N 来查找文件失效（文字显示红色），是由于非正常关闭造成的索引失效。可以通过 File ——> Invalidate Caches/Restart 来清理缓存并重启来解决这个问题。
