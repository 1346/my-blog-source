---
title: 利用grunt-spritesmith自动生成雪碧图
date: 2018-04-12 11:20:12
categories: vue
---

### grunt-spritesmith自动生成雪碧图了解一下

#### 1、安装grunt

```
	npm install grunt -S
```

#### 2、再装一下grunt-spritesmith

```
	npm install grunt-spritesmith -S
```

#### 3、在根目录下新建Gruntfile.js文件

```
module.exports = function (grunt) {
    // Configure grunt
    grunt.initConfig({
      sprite:{
        all: {
        	src: 'src/assets/images/icons/*.*',		// 自己图片的路径（如果没有需自己新增）
          dest: 'src/assets/images/spritesheet.png',		// 雪碧图路径（自动生成）
          destCss: 'src/assets/css/sprites.css',		// 雪碧图css路径（自动生成）
          // imgPath: '',   // 雪碧图在css中的url引用路径
          // retinaImgPath: '',   // 两倍雪碧图在css中的url引用路径
          // cssVarMap: function(sprite) {
          //   sprite.name = 'm-ic-icon.m-ic-icon-' + sprite.name;  
          //   //定义图标class名称，例如 del.png对应 m-ic-icon.m-ic-icon-del（如果不写则默认为”icon-‘文件名’“）
          // }
        }
      }
    });
  
    // Load in `grunt-spritesmith`
    grunt.loadNpmTasks('grunt-spritesmith');
  };
  
```

#### 4、最后一步
在package.json文件中的dev指令中加入：

```
	grunt sprite
```
并且用 && 符号进行连接