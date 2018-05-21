---
title: iconfont在vue里配置组件方法
date: 2018-01-17 22:11:31
categories: vue
---

icon在网页里使用的比较多、今天学习到了怎么在Vue里写一个自动化icon的组件


### iconfont网站

[iconfont-阿里巴巴矢量图标库](https://http://iconfont.cn/)

首先要知道这个网站、里面全都是图标、非常多、应该可以满足大多数时候的需求


### SvgIcon的组件

代码如下：

``` <template>
  <svg :class="svgClass" aria-hidden="true">
    <use :xlink:href="iconName"></use>
  </svg>
</template>

<script>
  export default {
    name: 'svg-icon',
    props: {
      iconClass: {
        type: String,
        required: true
      },
      className: {
        type: String
      }
    },
    computed: {
      iconName() {
        return `#icon-${this.iconClass}`
      },
      svgClass() {
        if (this.className) {
          return 'svg-icon ' + this.className
        } else {
          return 'svg-icon'
        }
      }
    }
  }
</script>

<style scoped>
  .svg-icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }
</style>
```

### icons文件夹

目录结构如下：

```
├── icons  
│    ├── svg   
│         ├── xxx.svg  
│         ├── xxx.svg  
│    ├── index.js  

```

svg文件夹是放下载下来的icon的

index.js文件是配置

### index.js

代码入下：

``` 
import Vue from 'vue'
import SvgIcon from '@/components/SvgIcon'// svg组件
import generateIconsView from '../views/IconLib/generateIconsView.js'

// 全局注册
Vue.component('svg-icon', SvgIcon)

const requireAll = requireContext => requireContext.keys().map(requireContext)
const req = require.context('./svg', false, /\.svg$/)
const iconMap = requireAll(req);

// 这里是为后面做准备的
generateIconsView.generate(iconMap)
```

### 使用icon
1. 创建文件夹svg-icon
2. 在svg-icon里新建index.vue文件
3. 再新建一个generateIconsView.js文件

index.vue文件代码如下：

```<template>
  <div class="icons-container">
    <div class="icons-wrapper">
      <div v-for="item of iconsMap" :key="item">
          <div class="icon-item">
            <svg-icon :icon-class="item" />
            <span>{{item}}</span>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import icons from './generateIconsView'

export default {
  name: 'icons',
  data() {
    return {
      iconsMap: []
    }
  },
  mounted() {
    const iconsMap = icons.state.iconsMap.map((i) => {
      return i.default.id.split('-')[1]
    })
    this.iconsMap = iconsMap
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.icons-container {
  margin: 10px 20px 0;
  overflow: hidden;
  .icons-wrapper {
    margin: 0 auto;
  }
  .icon-item {
    margin: 20px;
    height: 110px;
    text-align: center;
    width: 110px;
    float: left;
    font-size: 30px;
    color: #24292e;
    cursor: pointer;
  }
  span {
    display: block;
    font-size: 24px;
    margin-top: 10px;
  }
}
</style>

```

generateIconsView.js文件代码入下：
 

```
const data = {
  state: {
    iconsMap: []
  },
  generate(iconsMap) {
    this.state.iconsMap = iconsMap
  }
}

export default data

```

注意：此处的generate函数就是上面icons文件夹下index.js里面写好的函数、在icons/index.js里引入generateIconsView.js、然后写好generate函数、generateIconsView.js再调用

### 引入svg-sprite-loader

```
	npm install svg-sprite-loader --save
```

然后在build/webpack.base.conf.js文件里添加代码如下：

```
		//---- 此处新增start ----
		{
        test: /\.svg$/,
        loader: 'svg-sprite-loader',
        include: [resolve('src/icons')],
        options: {
          symbolId: 'icon-[name]'
        }
      },
      //---- 此处新增end ----
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        
        //---- 此处新增start ----
        exclude: [resolve('src/icons')],
        //---- 此处新增end ----
        
        options: {
          limit: 10000,
          name: utils.assetsPath('img/[name].[hash:7].[ext]')
        }
      },
```

至此、就已经大功告成了、可以在页面上愉快的引入各种自己喜欢的icon了

## 结语

### 虽然自己慢慢的写出来了、但是大多数还是参照着大神@*花裤衩*的教程来的、需要多写多练习、不然很容易就忘记了  

### **最后**  大神的教程在这里：[手摸手，带你优雅的使用 icon](https://segmentfault.com/a/1190000012213278)