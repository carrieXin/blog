# CSS 代码规范

## 命名规范

类命使用中划线连接

```css
.header-title {
    
}
```

遵循 BEM 原则

B -&gt; Block 某个功能块的名称，eg: `.card`

E -&gt; Element 功能块中的元素 ，eg: `.card-body`

M -&gt; Modifier 元素对应的修饰符，eg: `.card-body-disabled`

## 属性顺序 

在写样式代码时要注意属性的书写顺序，提高可读性，一般情况下按照以下顺序来书写样式：

1. 定位属性（position / display / float / top / right / z-index）;
2. 盒子属性（width / height / border / padding / margin）; 
3. 文字属性（color / font-size / font-weight / letter-spacing）;
4. 其他属性（background / cursor / animation / transition）；

如果样式中有 `content` 属性，应该放在最前面

```css
.card {
    /* 定位属性 */
    position: relative;
    display: flex;
    overflow-y: auto;
    
    /* 盒子属性 */
    width: 100%;
    padding: 10px;
    border: 1px solid #333;
    
    /* 文字属性 */
    color: #333;
    font-size: 14px;
}

.rectangle::before {
        content: "密码";
        position: absolute;
    }

```

## 值与单位 

1. 数字为零时省略单位

   ```css
   /* good */
   padding: 10px 0;

   /* bad */
   padding: 10px 0px;
   ```

2. 小于 1 的小数省略前面的 0

   ```css
   /* good */
   opacity: .8;

   /* bad */
   opacity: 0.8;
   ```

3. url 里面的路径不需要用引号

   ```css
   /* good */
   background: url(../image/logo.png)

   /* bad */
   background: url("../image/logo.png")
   ```

## 注释规范

```css
// 单行注释, 编译后不会被保留

/* 多行注释 */

/**
 * 文件头部注释
 * ***********************************************
 * ***********************************************
 */
 
 /// scss 注释
 /// @name: 文件名称
 /// @author: 作者
 /// @example: 举例
 /// @link: http://sassdoc.com/annotations/#example
```



