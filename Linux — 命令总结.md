## Linux 命令总结

---
- #### 实时查看文件打印
  ##### tail -f filePath

---
- #### 删除文件
```
  rm -f filePath     // 强制删除文件
  rm -r dir          // 递归删除目录下所有文件，危险操作
```


---
- #### vim 浏览文件翻页
```
  ctrl + b     // back    上一页
  ctrl + f     // foward  下一页

  ctrl + u     // up      上半页
  ctrl + d     // down    下半页

  G            // 移动到文件底部
  gg           // 移动到文件顶部
```


---
- #### vim 搜索
```
  ？keyWord       // 从下往上搜索
  /keyWord        // 从上往下搜索

  n               // 下一个搜索到的关键字（方向根据上面提到的 ？和 / 来确定）
  N               // 上一个搜索到的关键字（方向根据上面提到的 ？和 / 来确定）

  :set hls        //  打开高亮
  :set nohls      //  关闭高亮
```
