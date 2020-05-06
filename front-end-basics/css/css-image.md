# 图片相关样式

## 展示图片

1. 设置背景图片;
2. 使用 &lt;image /&gt; 标签;
3. ::after 和 ::before 设置图片;
4. 鼠标 hover 自定义光标样式;
5. border-image 自定义边框图案;
6. list-style-image 设置列表项样式;

代码如下：

{% tabs %}
{% tab title="background" %}
```css
/* 居中不重复的背景图片 */
background: url(../asset/img/logo.jpg) no-repeat center;

/* x轴重复 */
background: url(../asset/img/logo.jpg) repeat-x;

/* background 是以下属性值的缩写
    img: 背景图片 
    color: 背景颜色 
    repeat: 定义图片重复的方式 可选值 repeat-x/repeat-y/repeat/space/round/no-repeat
    size: 背景图片大小 可选值 contain/cover/百分比/具体像素
    clip: 背景图片延伸到哪个位置 可选值 text/border-box/padding-box/content-box 
    origin: 背景图片相对于哪个区域开始摆放 border-box/padding-box/content-box
    attachment: 背景图片在视口内固定还是随包含它的区块滚动 scroll/fixed/local
    position: 相对origin为图片设置初始位置  left/bottom/top/right/center/百分比/具体像素
    position-x: 设置背景图片在水平方向的位置 left/center/right/百分比/具体像素
    position-y: 设置背景图片在垂直方向的位置 top/center/bottom/百分比/具体像素
*/
```
{% endtab %}

{% tab title="<img />" %}
```javascript
<image src="../asset/img/logo.jpg" alt="">
```
{% endtab %}

{% tab title="::after" %}
```css
div::after{
  content: url(../asset/img/logo.jpg);
}
```
{% endtab %}

{% tab title="hover" %}
```css
cursor: url(../asset/img/cursor.jpg) auto;
```
{% endtab %}

{% tab title="borderImage" %}
```css
/* border-image: source slice width outset repeat|initial|inherit; */
border: 10px solid transparent;
border-image: url(./images/logo.png) 30 30 10 round;
```
{% endtab %}

{% tab title="listStyleImage" %}
```css
/* 列表项标记样式 */
list-style-image: url(./images/checked.png);
```
{% endtab %}
{% endtabs %}

## 图片缩放

* 纯 CSS 实现图片缩放；

  ```css
  /* 方式一 */
  transform: scale(.8);

  /* 方式二 */
  zoom: 50%；
  ```

* 图片随鼠标滚轮缩放

  ```javascript
  /* html */
  <img src="./images/desktop.jpg" alt="" onmousewheel="return zoom(this)" />

  /* javascript */
  function zoom(el) {
      var zoom = parseInt(el.style.zoom, 10) || 100;
          zoom += event.wheelDelta / 100;
          console.log(event.wheelDelta);
          if (zoom > 0) {
              el.style.zoom = zoom + '%';
          }
      return false;
  }
  ```

## 图片填充设置

object-fit 可以设置替换元素 \(&lt;img /&gt; &lt;iframe&gt;...\) 的内容如何填充到容器中，在&lt;img /&gt; 元素中的使用如下:

```css
object-fit: contain;

/* object-fit 包含以下几种值, 
   fill: 默认值，填充，图片填满容器，可能会改变宽高比，导致图片拉伸;
   contain: 包含，整个图片会保持宽高比展示在容器中，可能会被缩放，部分背景会空白;
   cover: 覆盖，图片保持宽高比填满容器，图片可能会被裁剪;
   none: 保持图片原尺寸和比例;
   scale-down: 等比缩小，类似依次设置了 none 和 contain,最终展示尺寸较小的那个;
*/
```

## 图片位置设置

object-position 可以设置替换元素的内容在容器中的位置，可用 left、top 等方位值控制，也可以用具体的数值表示，在&lt;img /&gt; 元素中的使用如下:

```css
object-position: left top;

/* 
  object-position: 水平方向可能的值       垂直方向可能的值
  object-position: left/center/right   top/center/bottom;
  object-position: 10px 15px; 
  如果只设置了一个值，则默认另一个方向的值为 center    
  如：object-position: top; => object-position: center top;
*/
```

## 图片热区

定义：在图片中指定某个区域，当用户点击该区域内时可以链接跳转到指定页面。  
应用场景：中国地图图片点击具体的省份跳转到各省对应的官网。  
创建图片热区:

```javascript
/* 
  <area shape="rect/circle/poly" href="" coords="" target="_blank/_parent/_self/_top"> 
  shape: 规定区域的形状;  
  href: 目标 url;  
  coords: 坐标; shape="rect" => x1,y1,x2,y2; shape="circ" => x,y,radius
  target: 在何处打开目标 url
*/
<img src="../asset/images/china.jpg" usemap="#mapname"/>
<map name="mapname" id="mapname">
	<area shape="rect" href="" coords="0,0,50,50"/>
</map>
```

## 3 像素bug

描述：img 标签渲染之后下方会出现几个像素（谷歌是 4px, 火狐 3.5px）的空白；  
原因：img 是行内元素，默认display：inline; 它与文本的默认行为类似，下边缘是与基线对齐，而不是贴紧容器下边缘，所以会有几像素的空白；  
解决办法：

1. 把 img 设置为display: block;
2. 给 img 和其父元素都设置 vertical-align: top；让其 top 对齐而不是 baseline 对齐；
3. 给 img 父元素设置 line-height: 0;



