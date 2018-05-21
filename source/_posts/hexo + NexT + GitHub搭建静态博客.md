---
layout: hexo
title: hexo + NexT + GitHub搭建静态博客
date: 2018-05-21 14:12:08
tags: hexo
---

### hexo + NexT + GitHub搭建静态博客了解一下

#### 先来了解一下hexo

```
	Hexo 是一个快速、简洁且高效的博客框架。
	Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
```

——来自hexo官网的解释

如官网所言、hexo是一个可以快速搭建博客的框架、直接使用markdown的语法来自动生成静态网页、内置很多主题、特效等、适合新手、小白，不需要会写代码也可以

#### hexo安装
前提条件：电脑中需要有node.js、git、npm环境

然后再命令行使用npm安装hexo  

```	
	$ npm install -g hexo-cli
```

#### 使用hexo建站
执行以下命令

```
	$ hexo init <folder>
	$ cd <folder>
	$ npm install
```

命令完成后会自动新建一些目录和文件、结构如下

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

`_config.yml`文件中可以修改大部分的配置、如网站标题、描述、您的名字、网站使用的语言等


#### 安装NexT
在命令行中输入指令  

```
	$ cd your-hexo-site
	$ git clone https://github.com/iissnan/hexo-theme-next themes/next
	
```

在`_config.yml`文件中找到theme字段、修改成next

然后进入hexo目录下输入指令`hexo server`启动hexo服务、当终端输出如下信息时说明成功：  

```
	INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
```

如果端口被占用可以输入指令：  


```
	$ hexo server -p 5000
```
来修改端口号

#### 设置GitHub Pages和hexo的准备工作
前提条件：已有GitHub账号并且了解GitHub

首先新建一个仓库、然后在settings里面找到GitHub Pages区域、在第一项里选择master branch、然后点击save

这样你就可以使用GitHub提供的服务器搭建网站

修改`_config.yml`文件中的代码如下：

```
	deploy:
	  type: git
	  repo: 这里填你的仓库地址
	  branch: master
```

在命令行中输入指令安装hexo-deployer-git自动部署发布工具：

```
	npm instal lhexo-deployer-git  --save
```

然后是最后一步了

#### 发布到GitHub上

输入指令  


```
	hexo clean && hexo g && hexo d
```

也可以拆分成三个指令  


```
	hexo clean
	hexo g
	hexo d
```

最后的最后说一下新建hexo文章、标签、分类等

新建一个hexo文章  


```
	hexo new 文章名
```

