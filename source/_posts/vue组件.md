---
title: vue组件
date: 2018-01-25 17:29:14
categories: vue
---

### vue组件的一些记录

vue组件是vue里面比较重要的一个部分、一定要搞懂

### 组件之间的数据传递

写一个input组件、input的原生属性都需要用props声明出来
使用组件时的v-model双向绑定需要在组件里进行一个处理
代码如下： 

```
<template>
  <div>
    <input class="Input" :type="type" :placeholder="placeholder" :value="value" @input="$emit('input', $event.target.value)"/>
  </div>
</template>

<script>
  export default {
    name: 'Input',
    props: ['value', 'placeholder', 'type']
    data() {
      return {
      }
    },
    methods: {
   
    }
  }
</script>

```

然后就可以引入组件使用v-model进行数据的双向绑定了


写一个button组件、button的名字怎么写？
使用`<slot></slot>`就可以了、官方文档有写明
[vue组件——使用插槽分发内容](https://cn.vuejs.org/v2/guide/components.html#%E4%BD%BF%E7%94%A8%E6%8F%92%E6%A7%BD%E5%88%86%E5%8F%91%E5%86%85%E5%AE%B9)