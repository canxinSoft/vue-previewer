# vue-preview-deleter

基于vue2.0的图片预览与删除组件 

[DEMO](http://jaywii.github.io/private/vue-previewer-demo/index.html)

可以自定义删除图片的回调函数，在点击删除图片的操作时，回调函数将根据`removeInside`的值来返回不同的参数，参数包括操作结果 `result` 和 具体数据 `data`：

1. 当 `removeInside` 为 `true` 时：`data`将返回所删元素的索引`index`,所删元素`removeTarget`,和删除元素后的列表`fileList`，此时应在回调函数内将返回的新的数组赋值到`imgs`上；
2. 当 `removeInside` 为 `false` 时：`data`将返回所删元素的索引`index`,所删元素`removeTarget`,和原始列表`fileList`，此时应在回调函数内进行删除操作，并重新对`imgs`赋值；

文档：<a href="https://github.com/JayWii/vue-previewer">https://github.com/JayWii/vue-previewer</a>  

## Install
```
npm install vue-preview-deleter --save
```

## Usage

```js
// main.js
import VuePreviewer from 'vue-preview-deleter'
Vue.use(VuePreviewer)
```

```html
<!-- component.vue -->
<template>
  <div id="app">
    <!--一般使用 -->
    <vue-previewer :imgs="imgs" @onRemove="handleRemove" @onClose="closeHandler"></vue-previewer>
    <!--slot引入图片上传元素 -->
    <!--
    <vue-previewer :imgs="imgs" @onRemove="handleRemove" @onClose="closeHandler">
        <div slot="uploader">图片上传元素或其他任意你想插入到图片list尾部的元素</div>
    </vue-previewer> 
    -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      imgs: [
        {
          src: 'https://farm4.staticflickr.com/3894/15008518202_b016d7d289_b.jpg',
          author: 'Folkert Gorter',
          desc: 'This is dummy caption.'
        },
        {
          src: 'https://farm6.staticflickr.com/5584/14985868676_4b802b932a_b.jpg'
        },
        {
          src: 'https://farm4.staticflickr.com/3920/15008465772_383e697089_b.jpg',
          author: 'Folkert Gorter2',
          desc: 'It\'s a dummy caption. He who searches for meaning here will be sorely disappointed.'
        }
      ]
    }
  },
  methods: {
    closeHandler () {
      console.log('cloooooose')
    },
    handleRemove (index, fileList, target) {
      this.imgs = fileList
    }
  }
}
</script>

```


### options
1. **imgs** - 图片文件或链接列表，可传入File，url，base64
    - **type**: Array
    - **required** : true
2. **width** - 每个图片单元的宽高（为保证图片呈现为方形，高度等于宽度），单位是px
    - **type**: Number
    - **required** : false
    - **default** : 80
3. **margin** - 每个图片单元的上外边距和右外边距，单位是px
    - **type**: Number
    - **required** : false
    - **default** : 10
4. **radius** - 每个图片单元的圆角值，单位是px
    - **type**: Number
    - **required** : false
    - **default** : 5
5. **removeEnable** - 是否可进行删除图片操作，假如为false，则点击图片直接查看大图
    - **type**: Boolean
    - **required** : false
    - **default** : true
6. **removeInside** - 删除图片的操作实际是在组件外处理还是组件内处理
    - **type**: Boolean
    - **required** : false
    - **default** : true
7. **deleteBtnColor** - 删除按钮的颜色
    - **type**: String
    - **required** : false
    - **default** : '#e12e2e'
8. **previewBtnColor** - 预览按钮的颜色
    - **type**: String
    - **required** : false
    - **default** : '#3caaff'
9. **type** - 传入的列表值类型，分为两个值：`file` 和 `url` （base64也用url）
    - **type**: String
    - **required** : false
    - **default** : 'url'
10. **srcName** - 传入的链接字段名
    - **type**: String
    - **required** : false
    - **default** : 'src'


### callBack
1. **onRemove** - 删除之后的回调函数
    - **type**: Function
    - **required** : false


### License
 MIT

### 致谢

> vue-picture-preview
