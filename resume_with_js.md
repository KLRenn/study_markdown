### target，currentTarget

function(x){
x.target
// 用户点击的对象
x.currentTarget
// 事件 绑定/监听的对象

// 实际被点击执行的对象 和 被绑定/监听的对象
}

### nodeType



### 页面加载时等待动画

```html
//html
<div id="webWelcome" class="webWelcome">
  <div class="loading"></div>
</div>

```

```css
//css
.webWelcome {
  width: 200px;
  height: 200px;
  border: 1px solid blue;
  position: relative;
}
// 利用伪元素创建动画
// 在loading的内容(内容为空，所以重叠)前后生成元素，
// 并将其中一个设置延迟
.loading::before,.loading::after {
  content: '';
  position: absolute;
  width: 20px;
  height: 20px;
  background: black;
  border-radius: 50%;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
  animation: s 2s linear infinite;
}

.webWelcome::after {
  animation-delay: 1s;
}

@keyframes s {
  0% {
    width: 0px;
    height: 0px;
    opacity: 1;
  }

  100% {
    width: 100px;
    height: 100px;
    opacity: 0;
  }
}
.webWelcome{
    display : none ;
    position : fixed ;
    top : 0 ; left: 0 ; width : 100% ; height : 100% ;
    background : #888 ;
    z-index : 1 ;
    justify-content : center ;
    align-items : center ;
}
.webWelcome .active{
    display : flex ;
}

```

#### 设置 webWelcome 持续时间
由于页面加载时间过短，页面等待动画不能加载，所以
```css
设置 webWelcome 短暂出现的条件

.site-welcome {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #888;
        z-index: 1;
        justify-content: center;
        align-items: center;
      }
.site-welcome.active{
    display:flex;
}

```
 `</body>`前（即`<body>`末尾）设置 webWelcome 去除 .active 的 setTimeout 函数

```js
<script>
setTimeout(() => {
    webWelcome.classList.remove('active')
}, 3000);
</script>
```


### topNavBar 及 sticky 动画

sticky_navbar
向下滚动时，导航条由半透明变实体并停留在顶部
导航条 padding 在向下滚动时缩小，达到动画效果，并且导航条下方出现阴影


```js
js
window.scrollY
//当前视口距离网页顶部的像素值
id.classList.add('sticky)
id.classList.remove('sticky)
querySelector('css选择器').classList.add('')
getElementsByxxx().classList.add('')
//添加或移除某个 id 的 class 值

```

##### topNavBar 及 sticky 动画 css

```js
css
.topNavBar {
  padding: 20px 0 20px 0;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  color: #b7b7b7;
}// 未粘滞导航条

.topNavBar.sticky {
  background: rgb(255, 255, 255);
  padding: 10px 0 10px 0;
  z-index: 1;

  box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
  color: #3d4451;
  animation:  barani  0.8s  ;
}// 粘滞时导航条
@keyframes barani {
  0%{
    padding: 20px 0 20px 0;
    opacity: 0;
  }
  100%{
    padding: 10px 0 10px 0;
    background: white;
    opacity: 1;
  }
}// 变化动画


// 当鼠标悬浮于导航条栏目时，；具体栏目下方出现虚拟的动态高亮条
// .topNavBar nav > ul > li > a:hover ::after
// li 包括 a 和 submenu，所以当鼠标停留在 li 内，<a>底部高亮条不会消失
.topNavBar li>a {
  font-size: 12px;
  color: inherit;
  font-weight: bold;
  border-top: 3px solid transparent;
  border-bottom: 3px solid transparent;
  padding-top: 5px;
  padding-bottom: 5px;
  display: block;
  position: relative;

}
.topNavBar nav > ul > li:active > a ::after
{
    content : '' ;
    display : block ;
    position : absolute ;
    top : 100% ;
    animation : menuSlide .5s ;
}
@keyframs menuSlide {
    0%{
        width : 0 ;
    }
    100%{
        width : 100% ;
    }
}

```

##### topNavBar 及 sticky 动画 js

```js
html
<section class="" id="siteSkills" >

</section>
```

```js
js
window.onscroll = function(topNavBar_sticky_or_not){
// 滚动条往下滑导航条固定
    if (window.scrollY > 0) {
        topNavBar.classList.add('sticky')
    }else{
        topNavBar.classList.remove('sticky')
    }
}
```




```css
css
.topNavBar { padding : 20px 0 ; position: fixed ;
top : 0 ; left : 0 ; width : 100% ; transition : all 0.8s ;
color : #b7b7b7 ;
}
.topNavBar .sticky{background : white ; padding : 10px 0;
z-index : 1 ; box-shadow : 0 0 10px rgba( 0,0,0,0.25 );
color : #3d4451;
}
.topNavBar-inner { padding : 0 16px ; }
.topNavBar nav { padding-top : 5px ; }
.topNavBar nav >ul { list-style : none ; margin : 0 ; padding : 0 ; }
.topNavBar nav >ul >li { float : left ; margin-left : 17px ; margin-right : 17px ; }
.topNavBar nav > ul > li > a { font-size : 12px ; color : inherit ; font-weight : bold ;
border-top : ??? ; padding-top : 5px ; padding-bottom : 5px ; display : block ;
}
```

### 导航条二级栏目由左向右渐变出现

```js
js
[弃用]
// 寻找导航条中li的下一非ul节点并设置鼠标事件
let aTags = document.getElementsByClassName('menuTigger')
for (let i = 0; i < aTags.length; i++) {
    aTags[i].onmouseenter = function(x){
        let a = x.currentTarget;
        let brother = a.nextSibling;
        // while (brother.nodeType === 3)
        // .tagName() 返回大写字符串
        // brother.tagName.tolowerCase() 由于 文本的tagName() 返回 undefined，
        // 此时 toLowerCase() 会发生错误
        while (brother.tagName.toLowerCase() !== 'ul' )
        {
            brother = brother.nextSibling;
        }
        console.log(brother);
    }
    aTags[i].onmouseleave = function () {
        console.log('mouseleave');
    }
}
```


```js
js
// 导航条的二级菜单 submenu
//<topNavBar>
//  <nav class="menu" style="float : right ; " >
//      <ul class="clearfix" >
//          <li>
//  <a href="#siteabout" >关于</a><a href="#siteskills">技能</a>
//   <li>                           <li>
//   <li>                           <li>
//   <li>                           <li>
//
```
![图 2](../../images/6514efc1e7072ee937366bd2126699d890e5dafb9ab4581f7f525636fa76b095.png)

```css


//鼠标悬浮 nav 具体栏目 作品 博客 时，nav 下方出现 submenu
.topNavBar nav>ul>li {
  float: left;
  margin-left: 17px;
  margin-right: 17px;
  position: relative;
  display: block;
}
.topNavBar .submenu {
  display: none;
  position: absolute;
  right: 0;
  top: 100%;
  background: white;
  color: #3d4451;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
}

.topNavBar .lii.active>.submenu {
  display: block;
  animation: submenuSlide .3s;
}

@keyframes submenuSlide {
  0% {
    margin-right: 30px;
  }

  100% {
    margin-right: 0px;
  }
}
// 绝对定位
.topNavBar .submenu > li {
    white-space : nowrap ;
    // 阻止 li 压缩使 width 缩小
    padding : 5px 10px ;
}

```
```js


// 把导航条中的li设置鼠标移动事件，
// 移入 li 的范围则li加上active，移出则去除active
let aTags = document.querySelectorAll('nav.menu > ul > li')
for (let i = 0 ; i < liTags.length ; i ++){
    liTags[i].onmouseenter = function(x){
        x.currentTarget.classList.add('active')
    }
    liTags[i].onmouseleave = function(x){
        x.currentTarget.classList.remove('active')
    }
}
```


### 点击导航条上具体栏目时滚动条移动至指定位置

auto scroll smoothly


```js
js
//               查找元素 | 当前监听的
// document.querySelector(x.currentTarget
// |属性为'href=#siteSkills'的  |获取元素到网页顶部的像素值
// .getAttribute('href'))        .offsetTop

let aTags = document.querySelectorAll('nav.menu > ul > li > a')
// 获取 nav 里的 a 标签
function animate(time) {
  requestAnimationFrame(animate);
  TWEEN.update(time);
}
requestAnimationFrame(animate);

for(let i=0; i<aTags.length; i++){
    // 设置 a 标签 鼠标点击事件
  aTags[i].onclick = function(x){
    x.preventDefault() // 阻止点击a标签的原始事件
    let a = x.currentTarget // 获取当前绑定/监听对象
    let href = a.getAttribute('href') //获取a标签的href属性'#siteAbout'
    let element = document.querySelector(href)// 根据href属性搜索元素
    let top = element.offsetTop
    // 获得对应元素距离页面顶部的像素值
    let currentTop = window.scrollY// 获取当前视口距离页面顶部的距离
    let targetTop = top - 80
    //设置跳转目标（距离顶部像素值），考虑到导航栏遮挡所以-80
    let s = targetTop - currentTop // 路程
    var coords = { y: currentTop}; // 起始位置
    var t = Math.abs((s/100)*300) // 时间
    if(t>500){ t = 500 } //设置跳转时间限制
    var tween = new TWEEN.Tween(coords) // 起始位置
      .to({ y: targetTop}, t) // 结束位置 和 时间
      .easing(TWEEN.Easing.Cubic.InOut) // 缓动类型
      .onUpdate(function() {
        // coords.y 已经变了
        window.scrollTo(0,coords.y) // 如何更新界面
      })
      .start(); // 开始缓动
    }
}
```
```js
let a = x.currentTarget ;
a.getAttribute('href');
// getAttribute('href') 得到 #siteSkills
console.log(a.href);
// 得到 127.0.0.1:3000#siteSkills
console.log(a.querySelector(href) );
// 得到 a 的元素信息<section class="" id="siteSkills" >
// </section>
console.log(a.getBoundingClientRect());
// 得到 li 的大小和 li 相对于视口的位置
console.log(a.offsetTop);
// 得到 li 到页面顶部的像素值
window.scrollTo(0 , top - 80 )
// 滚动条滑动到计算好的指定位置，但无动画

let n = 20 ; // 滚动条固定滑动次数
let t = 500 / n ; // 500ms 固定滑动总时长，t 每次固定滑动时间
let currentTop = window.scrollY ; // 当前视口距离页面的距离
let targetTop = top - 80 ; // 目标标签往上80px，即滚动条最终目的地到页面顶部的距离
let S = targetTop - currentTop ; // 滚动条需移动的距离
let s = S / n ; // 每次移动的像素值，n为固定值
let i = 0 ; // 移动计数器
let id = setInterval(() => { // 移动循环器
    if ( i === n){ // 移动次数达到指定值
        window.clearInterval(id); // 删除循环器
        return ; // 跳出循环
    }
    i = i + 1 ;
    window.scrollTo( 0 , currentTop + s * i) // 将视口以指定距离移动
}, t); // t 固定值，循环一次的时间，每次移动的时间
```
[张鑫旭-如何使用Tween.js各类原生动画运动缓动算法](https://www.zhangxinxu.com/wordpress/2016/12/how-use-tween-js-animation-easing/)

```js
js


let aTags = document.querySelectorAll('nav.menu > ul > li > a')

function animate(time) {
	requestAnimationFrame(animate)
	TWEEN.update(time)
}
requestAnimationFrame(animate)
// 设置 TWEEN.js 缓动

for (let i = 0 ; i < liTags.length ; i ++){
    aTags[i].onclick = function(x){
        x.preventDefault() ;
        // 阻止默认动作
        let top = document.querySelector(x.currentTarget.getAttribute('href')).offsetTop ;
        // 查找元素 | 当前监听的 | 属性为'href=#siteSkills'的 | 元素，获取元素到网页顶部的像素值

// 用 tween 实现视口的变速滑动
        let currentTop = window.scrollY ;
        let targetTop = top - 80 ;
        let s = targetTop - currentTop ;
        var coords = { y : currentTop } ;
        var t = Math.abs( s/100*300 ) ;
        if ( t > 500 ) { t = 500 }
        var tween = new TWEEN.Twen(coords) ;
            .to ( { y: targerTop} , t )
            .easing ( TWEEN.Easing.Quadratic.InOut ) // 选择变速模式
            .onUpdate (function() {
                window.scrollTo( 0 , coords.y)
            })
            .start() ;
    }
}
```

### 导航条`<a>`下方有高亮条表示当前页面位置，高亮条动态显示

导航栏的`<li>` ，`<section>`的`<h2>` 都有提示视口位置的高亮条
`<section>`里的元素出现动态阴影
    视口移动至下一个`<section>`，上一个动态消失，下一个动态出现
根据`<section>.offsetTop`+自身元素的高度 得到高亮条和阴影出现的范围
根据 `window.scrollY 总和` + `粘滞导航栏高度` 判断 当前视口位置

`<li>`从左往右动态显示，

`<h2>`从下往上动态显示
根据`<section>.offsetTop`+自身元素的高度 得到高亮条出现的范围

```js
js
let specialTags = document.querySelectorAll('[data-x]') ;
// 找到所有 含有属性 [data-x] 的div 并复制给 specialTags

for(let i = 0 ; i<specialTags;i++){
    console.log(specialTags[i].offsetTop);
}
```

### 页面下方出现的内容以动画形式加载
animate when scroll

```js
js
let specialTags = document.querySelectorAll(['date-x']) ;
//querySelectorAll(['date-x']
for(let i = 0 ; i<specialTags.length;i++){
    specialTags[i],classList.add('offset')
}

```
```css
css
[data-x].active {
    outline: 10px solid red ;
}
[data-x].offset{  // offset 即初始状态-初始关键帧
    transform: translateY(100px) ;
}
[data-x] {
    transform: translateY(0) ;
    transition: all 0.5s ;
}
@keyframes slideUp {
    0% {
        transform: translateY(-30px) ;
    }
    100% {
        transform: translateY(0) ;
    }
}

```
### 技能条动态显示
```css
css
section.skills .progressBar {
    height :5px ; background : #FAE1E1 ; border-radius : 2px ;
    width : 70% ; border-radius : 2px ; transform : translateX( 0 ) ;
    transition : all 1s ;
}
section.skills.offset .progress {
    transform : translateX(-100%) ;
// 设置关键帧,当该section处于offset状态,progress往左横向偏移自身100%width
}
```
侧边栏从右边出现
auto hide aside

无缝轮播

gapless slides

loading animation






