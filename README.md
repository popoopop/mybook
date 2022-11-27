# Gitbook入门



### 简介

> gitbook是一个使用markdown或html语法，结合git生态，创建电子书的node.js命令行工具。很多产品都可以用gitbook来做，比如电子书、说明文档、静态网站等，document everything 。gitbook serve 生成出来的_book文件，push到你的远程git仓库，然后部署成静态网站，任何人都可以用浏览器查看。

### 安装nodejs

> Node.js 是一个基于 Chrome V8 引擎的、服务端的JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的单线程模型，使其轻量又高效。Node.js 的第三方包管理器 npm，是全球最大的开源库生态系统。	 

* 安装nodejs

  [最后一个支持win7的nodejs，v13.14.0](https://nodejs.org/en/download/releases/)

  搜索 13.14.0版本，下载node-v13.14.0-x64.msi，双击开始安装。

  修改安装目录（如：D:\nodejs，默认在系统C盘%appdata%），一路next。

* 检查环境变量

  安装完成后，会自动添加路径到当前用户和系统环境变量。

  计算机-属性-高级系统设置-高级-环境变量，检查PATH是否包含 D:\nodejs; ，没有则手动添加进去。

* 检查版本号，确认安装成功

  Win+R 打开命令行窗口，输入 node -v 和 npm -v，显示版本号则说明安装成功。

  ```
    Microsoft Windows [版本 6.1.7601]
    版权所有 (c) 2009 Microsoft Corporation。保留所有权利。
  
    C:\Users\Administrator>node -v
    v13.14.0
  
    C:\Users\Administrator>npm -v
    6.14.4
  
    C:\Users\Administrator>
  ```

* 修改全局缓存和模块目录

  npm管理第三方插件包的目录（npm install [第三方包名称] [-g]）。

  默认在系统C盘%appdata%\npm，为了不占用系统盘空间，将其改到其他目录（如D:\nodejs）。

- 查看路径
  ```
  npm config get cache
  npm config get prefix
  ```
  
- 修改路径
  ```
  npm config set cache  "D:\nodejs\node_cache"
  npm config set prefix "D:\nodejs\node_global"
  ```
  
- 添加路径到系统环境变量PATH
  ```
  D:\nodejs\node_global;
  ```

### 安装gitbook
* 使用npm命令安装gitbook-cli。	
	```
  npm install gitbook-cli -g
	```

* 检查是否安装成功
	```
	gitbook -V
	```

### 安装gitbook插件

* 安装插件有三种方式 ：

  1、创建并编辑book.json，执行 gitbook install。

  2、使用命令 npm install gitbook-plugin-[插件] -g。

  3、GitHub下载插件源码目录，放到node_modules文件夹内。				
  	https://www.npmjs.com/package/gitbook-plugin-click-reveal

* 卸载插件
  
  1、npm uninstall -g [插件]
  
* 默认插件
  
  Gitbook默认带有7个插件：
  
  ```
  livereload：	GitBook实时加载
  highlight： 	代码高亮
  search： 	导航栏查询（不支持中文）
  lunr:		
  sharing：	右上角分享按钮
  fontsettings：字体设置（最上方的"A"符号）
  theme-defalut:
  ```
  
  如果要去除自带的插件，可以在book.json的插件名称前面加-，如：
  
  ```
  "plugins":[
    	"-search",
    	"-lunr"
  ]
  ```
  
* hide-element 插件示例

  隐藏不想看到的元素。如gitbook默认提示：Published with GitBook

  1、编辑book.json如下：

  ```
    {
        "plugins": [
            "hide-element"
        ],
        "pluginsConfig": {
            "hide-element": {
                "elements": [".gitbook-link"]
              }
          }
  }
  ```

  2、执行 gitbook install

### 制作电子书

* 目录初始化

  新建目录如d:\test，右键-Git Bash here 或 cmd命令行窗口并cd /d到上述目录，执行：

  ```
  gitbook init
  ```
  会生成README.md（说明文件）和UMMARY.md（目录文件）。每次修改.md需要再次执行gitbook init。
  
* 打包编译，生成静态网页
  ```
  gitbook build [--output=/输出到其他目录]
  ```
  将会在gitbook目录下生成**_book**文件夹，这就是我们的一个静态站点

* 编译生成静态站点，开启预览服务 
  ```
  gitbook serve [--port 端口]
  ```

  默认端口4000，浏览器中使用localhost:4000预览。若启动服务失败再try一次。按ctrl+c退出预览服务后，回到命令行可输入状态。
  
  目录预览
  ```
  .
  	> book.json		# 设置插件
  	> README.md		# 介绍文件
  	> SUMMARY.md 	# 目录文件
  ─styles
  	> website.css	# 设置样式
  ─chapter1			# 第一章文件夹
  	> chapter1.md	# 第一章文件
  	> section1.md
  	> section2.md
  ```

### 发布分享

> GitHub为每一个账号提供GitHub Pages站点服务（Hello World教程：https://pages.github.com/）， 步骤如下：

- 创建存储库

	GitHub网站创建一个与您的账号同名的**公共**存储库，格式为username.github.io 。如：https://github.com/popoopop/popoopop.github.io

- Clone到本地目录

	使用git clone命令，或者GitHub网站Code下拉按钮选择Open With GitHub Destop桌面程序，将远程存储库克隆到本地目录（如 D:\projects\popoopop.github.io\）。

- 本地目录创建index.html

    ```
    <!DOCTYPE html>
    <html>
    <body>
    <h1>Hello World</h1>
    <p>I'm hosted with GitHub Pages.</p>
    </body>
    </html>
    ```
	将index.html文件add到本地缓存区，并提交到远程存储库。

- 网页预览

	浏览器访问 https:// username.github.io 查看效果，如：https://popoopop.github.io/ ，网页生效时间最长需等待20分钟。

### 发布分享（单个仓库）

​	> GitHub也为每一个**公开**存储库提供gh-pages网页预览服务，步骤如下：

 * 进入本地存储库

   如 cd D:\projects\mybook

 * 初始化目录

   git init

 * 创建gh-pages分支

   git checkout --orphan gh-pages

 * 添加文件到暂存区

   git add .

 * 添加提交信息

   git commit -m "create gh-pages xxxxx"

 * 推送到远程仓库

   git push origin gh-pages

   这时刷新github仓库就可以看到gh-pages分支了。

 * 定制gh-pages网页

   github网站打开mybook仓库，选择gh-pages分支，点击setting，打开左侧栏Code and automation下的Pages页。

   右侧可以看到我们的网页地址（生效时间可能需要几分钟）：

   ```
   Your site is ready to be published at https://popoopop.github.io/mybook/
   ```
   
   设置Source，选择Branch:gh-pages分支，Save。
   
   自由选择一个GitHub自带的主题。
   
   如果有自己的域名，可以在Custom domain中设置。
   
   等待几分钟之后，浏览器打开：https://popoopop.github.io/mybook/ 预览。

参考：https://www.cnblogs.com/yuxiaole/p/9346160.html
### MakeDown
> Markdown 是一种轻量级标记语言，只要纯文本编写，加上点标记符，就能转成格式文档（如 HTML 富文本）。

* 下载MD编辑器（typora）
	
	[最后一个typora免费版v1.0.0](https://dqunying2.jb51.net/201904/tools/Typora64_jb51.rar)
	
* 常用语法
	
	```
	# 一级标题
	## 二级标题
	*斜体*
	**粗体**
	* 无序符号
	- 无序符号
	> 引用
	```
	
	```
	`行内代码`
	```
	
	````
	```
	代码块
	```
	````
	
* 引用
	
	```
	这里引用了一个文献。[<sup>1</sup>](#refer-anchor-1)
	#### 参考文献
	<div id="refer-anchor-1"></div>
	- [1] [百度学术](http://xueshu.baidu.com/)
	<div id="refer-anchor-2"></div>
	- [2] [维基百科](https://en.wikipedia.org/wiki/Main_Page)
	```
	
	这里引用了一个文献。[<sup>1</sup>](#refer-anchor-1)
	##### 参考文献
	<div id="refer-anchor-1"></div>
	- [1] [百度学术](http://xueshu.baidu.com/)
	<div id="refer-anchor-2"></div>
	- [2] [维基百科](https://en.wikipedia.org/wiki/Main_Page)
