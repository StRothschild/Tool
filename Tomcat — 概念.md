## Tomcat 的概念

- #### Artifact 的概念
  ##### Artifact 可以理解为 tomcat 用于部署的一个包。主要有两种模式 war 和 war explorded。war 模式：将 WEB 工程以包的形式上传到服务器。war exploded 模式：将WEB工程以当前文件夹的位置关系上传到服务器。

  ##### 1. war模式这种可以称之为是发布模式，看名字也知道，这是先打成war包，再发布；

  ##### 2. war exploded模式是直接把文件夹、jsp页面 、class 等转移到 Tomcat 部署文件夹里面，进行加载部署。因此这种方式支持热部署，一般在开发的时候也是用这种方式。
