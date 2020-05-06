---
description: 本文记录一次创建vue项目的过程，教你从零开始搭建自己的项目
---

# vue项目搭建

前置条件：已安装 node.js 和 git

## 安装vue

```javascript
全局安装 vue-cli： npm install -g @vue/cli
查看版本: vue --version
```

## 创建项目

### 命令法创建

```javascript
vue create project-name
```

执行上面命令行弹出项目配置选项，按自己所需选择对应的配置

![&#x547D;&#x4EE4;&#x521B;&#x5EFA;](../../.gitbook/assets/tu-pian%20%281%29.png)

创建成功后定位到项目文件夹目录，执行  `npm run serve`   运行项目

> 注意：使用 cmd 命令面板选预设选项的时候有颜色提示，而git bash没有

### 图形工具创建

安装好vue之后，在cmd中定位到你想创建项目的文件夹下，输入 `vue ui` 出现图形化创建项目的引导图，然后按需选择配置项。

![](../../.gitbook/assets/tu-pian%20%282%29.png)

## 目录划分

* 视图页面放在 `pags` 或者 `views` 中 
* 静态文件放在 `static` 中 
* 资源文件放在`assets`中 
* 样式文件放在`styles`中 
* 辅助库放在`utils`中 
* 配置文件可以放在`config`或者`constants`中 
* vuex 的文件放在`stores`中，至于 getters, actions, mutation, modules 可以参考 vuex 的文档 
* 路由文件放在`routes`中 
* 所有组件放在`components`中 
* 共享代码也可以使用`shared`作为目录 
* 布局组件可以放在`layouts`目录中

## 引入三方库

### 引入 SCSS

1. 安装 scss： `npm install --save-dev sass-loader node-sass`
2. 在 `assets/style` 文件夹中新建公共样式的 scss 文件，如`_variables.scss`  `_mixins.scss`;
3. 把公共样式文件导入main.scss 文件；

   ```javascript
   /* main.scss */
   @import "./mixins";
   @import "./variables";
   ```

4. 在与 `src`平级的目录下新建 `vue.config.js` 文件并引用`main.scss`（该文件会自动被 @vue/cli-service 加载）

   ```javascript
   // vue.config.js
   const IS_PROD = ["production", "prod"].includes(process.env.NODE_ENV);
   module.exports = {
       publicPath: IS_PROD ? process.env.VUE_APP_PUBLIC_PATH : "./",
       devServer: {
           open: true
       },
       css: {
           extract: IS_PROD,
           sourceMap: false, // 是否为css开启sourceMap
           loaderOptions: {
               scss: {
                   // 向全局sass样式传入共享的全局变量, @是src的别名， $src可以配置图片cdn前缀
                   prependData: `
                       @import "@/assets/style/main.scss";
                       $src: "${process.env.VUE_APP_OSS_SRC}";
                       `
               }
           }
       }
   };
   ```

### 引入 element-ui

方法一： cmd 定位至项目目录下，执行命令 `vue add element`，选择全部引入或按需引入，然后重新启动项目，就可以看到效果了； 

方法二： cmd 定位至项目目录下，执行命令 `vue ui`，在图形化界面的插件页 -&gt; 点击右上角添加插件 -&gt; 搜索 `vue-cli-plugin-element` 加入；

使用时直接在组件中导入  `eg: import { Message } from 'element-ui';`

### 引入 icon-font

1. 将iconfont图标库\(阿里巴巴矢量图标库\)中项目的字体文件下载至本地 ；  
2. 在 asset 文件夹下新建 `fonts` 目录，把下载的  .eot、.svg、.ttf、.woff、.wiff2 字体文件放入 fonts目录中；
3. 在 asset 文件夹下新建`style/fonts.scss`, 把下载的字体文件 `demo_index.html` 使用步骤中的代码以及`iconfont.css` 中具体图标的样式代码拷贝过来，如下：

   ```css

   /* fonts.scss */
   @font-face {
       font-family: "iconfont";
       src: url('~@/assets/fonts/iconfont.eot'); /* IE9 */
       src: url('~@/assets/fonts/iconfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('~@/assets/fonts/iconfont.woff') format('woff'),
       url('~@/assets/fonts/iconfont.woff2') format('woff2'),
       url('~@/assets/fonts/iconfont.ttf') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
       url('~@/assets/fonts/iconfont.svg#iconfont') format('svg'); /* iOS 4.1- */
     }
  
     .iconfont {
       font-family: "iconfont" !important;
       font-size: 16px;
       font-style: normal;
       -webkit-font-smoothing: antialiased;
       -moz-osx-font-smoothing: grayscale;
     }
  
     .icon-comparison:before {
       content: "\e60e";
     }
  
     .icon-empty-data:before {
       content: "\e61e";
     }
     ...
   ```

4. 在`main.js`中导入 `font.scss`文件：`import './assets/style/fonts.scss';`

{% hint style="warning" %}
注意：这里遇到两个坑

坑一：第 3 步中 url 后面的字体文件路径原本用的是相对路径 ../fonts , 但运行后一直报错找不到字体文件，后改用 ~@/assets/fonts 解决， 详情参见[这篇文章](https://segmentfault.com/a/1190000016120011?utm_source=tag-newest)；

坑二：原本是将 fonts.scss 导入 main.scss ，但其他样式文件都成功编译了，就fonts.scss没有编译，然后用第 4 步的方法解决；
{% endhint %}



