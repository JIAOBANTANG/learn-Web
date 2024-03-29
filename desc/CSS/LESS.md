![](image/a498eee.gif)
# LESS
>[文章出处](https://juejin.im/post/5a2bc28f6fb9a044fe464b19)
## 前言
### css短板

为前端学习者的我们 或多或少都要学些 CSS ，它作为前端开发的三大基石之一，时刻引领着 Web 的发展潮向。 而 CSS 作为一门标记性语言，可能 给初学者第一印象 就是简单易懂，毫无逻辑，不像编程该有的样子。在语法更新时，每当新属性提出，浏览器的兼容又会马上变成绊脚石，可以说 CSS 短板不容忽视。

问题的诞生往往伴随着技术的兴起， 在 Web 发展的这几年， 为了让 CSS 富有逻辑性，短板不那么严重，涌现出了 一些神奇的预处理语言。 它们让 CSS 彻底变成一门 可以使用 变量 、循环 、继承 、自定义方法等多种特性的标记语言，逻辑性得以大大增强。

### 预处理语言的诞生
其中 就我所知的有三门语言：`Sass`、`Less` 、`Stylus` 。
1. Sass 诞生于 2007 年，Ruby 编写，其语法功能都十分全面，可以说 它完全把 CSS 变成了一门编程语言。另外 在国内外都很受欢迎，并且它的项目团队很是强大 ，是一款十分优秀的预处理语言。
2. Stylus 诞生于 2010 年，来自 Node.js 社区，语法功能也和 Sass 不相伯仲，是一门十分独特的创新型语言。
3. Less 诞生于 2009 年，受Sass的影响创建的一个开源项目。 它扩充了 CSS 语言，增加了诸如变量、混合（mixin）、函数等功能，让 CSS 更易维护、方便制作主题、扩充（引用于官网）。
### 选择预处理语言

这是一个十分纠结的问题。


1. 在我看来，这就好比 找女朋友，有人喜欢 贤惠安静的，就有人喜欢 活泼爱闹的，各有各的爱好，可晚上闭灯后 其实都差不多，所以你不用太过纠结。当然了 ，首先 你要有女朋友。


2. 在网上讨论看来，Sass 与 Stylus 相比于 Less 功能更为丰富，但对于学习成本以及适应时间 ，Less 稍胜一筹，这也是我选择 Less 的原因。


3. Less 没有去掉任何 CSS 的功能，而是在现有的语法上，增添了许多额外的功能特性，所以学习 Less 是一件非常舒服的事情。


如果你之前没有接触过预处理语言，纠结应该学哪一个，不如先看看 下面 Less 的介绍，我相信你会爱上它的。

### 使用Less的前奏
使用 Less 有两种方式
1. 在页面中引入Less.js
- 可在[官网](http://lesscss.org/)下载
- 或使用CDN
~~~html
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js"></script>
~~~
需要注意的是，link 标签一定要在 Less.js 之前引入，并且 link 标签的 rel 属性要设置为stylesheet/less。
~~~html
 <link rel="stylesheet/less" href="style.less">
 <script src="less.min.js"></script>
~~~
2. 在命令行使用npm全局安装
~~~shell
npm install -g less
~~~
具体使用命令
~~~shell
$ lessc styles.less > styles.css
~~~
假如还有问题，[官网](https://less.bootcss.com/)已经有了明确的步骤。

如果你在本地环境，可以使用第一种方式，非常简单；但在生产环境中，性能非常重要，最好使用第二种方式。

3. 编辑器中安装Less插件

## 正文
下面我将简介 Less 的功能特性。
### 变量
我们常常在 CSS 中 看到同一个值重复多次，这样难易于代码维护。 理想状态，应是下面这样：
~~~js
function $($selector){
  return document.querySelector($selector)
}
const bgColor="skyblue";
$(".post-content").style.cssText="background-color:"+bgColor
$("#wrap").style.cssText="background-color:"+bgColor
$(".arctive").style.cssText="background-color:"+bgColor
~~~
只要我们修改 bgColor这一个变量， 整个页面的背景颜色都会随之改变。
而 Less 中的变量十分强大，可化万物，值得一提的是，其变量是常量 ，所以只能定义一次，不能重复使用。
#### 1. 值变量(掌握)
~~~less
/* Less */
@color: #999;
@bgColor: skyblue;//不要添加引号
@width: 50%;
#wrap {
  color: @color;
  background: @bgColor;
  width: @width;
}
/* 生成后的 CSS */
#wrap {
  color: #999;
  background: skyblue;
  width: 50%;
}
~~~
以 @ 开头 定义变量，并且使用时 直接 键入 @名称。
在平时工作中，我们就可以把 常用的变量 封装到一个文件中，这样利于代码组织维护。
~~~less
@lightPrimaryColor: #c5cae9;
@textPrimaryColor: #fff;
@accentColor: rgb(99, 137, 185);
@primaryTextColor: #646464;
@secondaryTextColor: #000;
@dividerColor: #b6b6b6;
@borderColor: #dadada;
~~~
#### 2.选择器变量(掌握)
让选择器变成动态
~~~less
/* Less */
@mySelector: #wrap;
@Wrap: wrap;
@{mySelector}{ //变量名 必须使用大括号包裹
  color: #999;
  width: 50%;
}
.@{Wrap}{
  color:#ccc;
}
#@{Wrap}{
  color:#666;
}

/* 生成的 CSS */
#wrap{
  color: #999;
  width: 50%;
}
.wrap{
  color:#ccc;
}
#wrap{
  color:#666;
}
~~~

#### 3.属性变量(掌握)
可减少代码书写量
~~~less
/* Less */
@borderStyle: border-style;
@Soild:solid;
#wrap{
  @{borderStyle}: @Soild;//变量名 必须使用大括号包裹
}

/* 生成的 CSS */
#wrap{
  border-style:solid;
}

~~~

#### 4.url变量(掌握)
项目结构改变时，修改其变量即可。
~~~less
/* Less */
@images: "../img";//需要加引号
body {
  background: url("@{images}/dog.png");//变量名 必须使用大括号包裹
}

/* 生成的 CSS */
body {
  background: url("../img/dog.png");
}

~~~

#### 5.声明变量(掌握)
有点类似于 下面的 混合方法
- 结构: @name: { 属性: 值 ;};
- 使用：@name();
~~~less
/* Less */
@background: {background:red;};
#main{
    @background();
}
@Rules:{
    width: 200px;
    height: 200px;
    border: solid 1px red;
};
#con{
  @Rules();
}

/* 生成的 CSS */
#main{
  background:red;
}
#con{
  width: 200px;
  height: 200px;
  border: solid 1px red;
}
~~~
#### 6.运算变量(掌握)
~~~less
/* Less */
@width:300px;
@color:#222;
#wrap{
  width:@width-20;
  height:@width-20*5;
  margin:(@width-20)*5;
  color:@color*2;
  background-color:@color + #111;
}

/* 生成的 CSS */
#wrap{
  width:280px;
  height:200px;
  margin:1400px;
  color:#444;
  background-color:#333;
}
~~~

#### 变量作用域(了解)
一句话理解就是：就近原则，不要跟我提闭包。
借助官网的Demo
~~~less
/* Less */
@var: @a;
@a: 100%;
#wrap {
  width: @var;
  @a: 9%;
}

/* 生成的 CSS */
#wrap {
  width: 9%;
}
~~~


### 嵌套
#### 1. &的妙用(掌握)
& ： 代表的上一层选择器的名字，此例便是`header`
~~~less
/* Less */
#header{
  &:after{
    content:"Less is more!";
  }
  .title{
    font-weight:bold;
  }
  &_content{//理解方式：直接把 & 替换成 #header
    margin:20px;
  }
}
/* 生成的 CSS */
#header::after{
  content:"Less is more!";
}
#header .title{ //嵌套了
  font-weight:bold;
}
#header_content{//没有嵌套！
    margin:20px;
}
~~~
#### 2. 媒体查询(掌握)
在以往的工作中，我们使用 媒体查询，都要吧一个元素分开写
~~~css
#wrap{
  width:500px;
}
@media screen and (max-width:768px){
  #wrap{
    width:100px;
  }
}
~~~

less 提供了一个十分便捷的方式

~~~less
/* Less */
#main{
    //something...
    @media screen{
        @media (max-width:768px){
          width:100px;
        }
    }
    @media tv {
      width:2000px;
    }
}
/* 生成的 CSS */
@media screen and (maxwidth:768px){
  #main{
      width:100px; 
  }
}
@media tv{
  #main{
    width:2000px;
  }
}
~~~
唯一的缺点就是 每一个元素都会编译出自己 @media 声明，并不会合并。

### 混合方法
#### 1. 无参数方法(掌握)
方法犹如 声明的集合，使用时 直接键入名称即可。
~~~less
/* Less */
.card { // 等价于 .card()
    background: #f6f6f6;
    -webkit-box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
    box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
}
#wrap{
  .card;//等价于.card();
}
/* 生成的 CSS */
#wrap{
  background: #f6f6f6;
  -webkit-box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
  box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
}
~~~

#### 2. 默认参数方法
- Less 可以使用默认参数，如果 没有传参数，那么将使用默认参数。
- `@arguments` 犹如 JS 中的 `arguments` 指代的是 全部参数。
- 传的参数中 必须带着单位。
~~~less
/* Less */
.border(@a:10px,@b:50px,@c:30px,@color:#000){
    border:solid 1px @color;
    box-shadow: @arguments;//指代的是 全部参数
}
#main{
    .border(0px,5px,30px,red);//必须带着单位
}
#wrap{
    .border(0px);
}
#content{
  .border;//等价于 .border()
}

/* 生成的 CSS */
#main{
    border:solid 1px red;
    box-shadow:0px,5px,30px,red;
}
#wrap{
    border:solid 1px #000;
    box-shadow: 0px 50px 30px #000;
}
#content{
    border:solid 1px #000;
    box-shadow: 10px 50px 30px #000;
}
~~~

#### 3. 方法的匹配模式(掌握)
与 面向对象中的多态 很相似
~~~less
/* Less */
.triangle(top,@width:20px,@color:#000){
    border-color:transparent  transparent @color transparent ;
}
.triangle(right,@width:20px,@color:#000){
    border-color:transparent @color transparent  transparent ;
}

.triangle(bottom,@width:20px,@color:#000){
    border-color:@color transparent  transparent  transparent ;
}
.triangle(left,@width:20px,@color:#000){
    border-color:transparent  transparent  transparent @color;
}
.triangle(@_,@width:20px,@color:#000){
    border-style: solid;
    border-width: @width;
}
#main{
    .triangle(left, 50px, #999)
}
/* 生成的 CSS */
#main{
  border-color:transparent  transparent  transparent #999;
  border-style: solid;
  border-width: 50px;
}
~~~
#### 4. 方法的命名空间(了解)
让方法更加规范
~~~less
/* Less */
#card(){
    background: #723232;
    .d(@w:300px){
        width: @w;
        
        #a(@h:300px){
            height: @h;//可以使用上一层传进来的方法
        }
    }
}
#wrap{
    #card > .d > #a(100px); // 父元素不能加 括号
}
#main{
    #card .d();
}
#con{
    //不得单独使用命名空间的方法
    //.d() 如果前面没有引入命名空间 #card ，将会报错
    
    #card; // 等价于 #card();
    .d(20px); //必须先引入 #card
}
/* 生成的 CSS */
#wrap{
  height:100px;
}
#main{
  width:300px;
}
#con{
  width:20px;
}
~~~
要点
- 在 CSS 中> 选择器，选择的是 儿子元素，就是 必须与父元素 有直接血源的元素。
- 在引入命令空间时，如使用 > 选择器，父元素不能加 括号。
- 不得单独使用命名空间的方法 必须先引入命名空间，才能使用 其中方法。
- 子方法 可以使用上一层传进来的方法
#### 5. 方法的条件筛选(了解)
less没有if else,可是它有 `when`

~~~less
/* Less */
#card{
    
    // and 运算符 ，相当于 与运算 &&，必须条件全部符合才会执行
    .border(@width,@color,@style) when (@width>100px) and(@color=#999){
        border:@style @color @width;
    }

    // not 运算符，相当于 非运算 !，条件为 不符合才会执行
    .background(@color) when not (@color>=#222){
        background:@color;
    }

    // , 逗号分隔符：相当于 或运算 ||，只要有一个符合条件就会执行
    .font(@size:20px) when (@size>50px) , (@size<100px){
        font-size: @size;
    }
}
#main{
    #card>.border(200px,#999,solid);
    #card .background(#111);
    #card > .font(40px);
}
/* 生成后的 CSS */
#main{
  border:solid #999 200px;
  background:#111;
  font-size:40px;
}
~~~
要点
- 比较运算有： > >= = =< <。
- = 代表的是等于
- 除去关键字 true 以外的值都被视为 false：

#### 6. 数量不定的参数(了解)
如果你希望你的方法接受数量不定的参数，你可以使用... ，犹如 ES6 的扩展运算符。
~~~less
/* Less */
.boxShadow(...){
    box-shadow: @arguments;
}
.textShadow(@a,...){
    text-shadow: @arguments;
}
#main{
    .boxShadow(1px,4px,30px,red);
    .textShadow(1px,4px,30px,red);
}

/* 生成后的 CSS */
#main{
  box-shadow: 1px 4px 30px red;
  text-shadow: 1px 4px 30px red;
}
~~~
#### 7. 方法使用important!(掌握)
使用方法 非常简单，在方法名后 加上关键字即可。
~~~less
/* Less */
.border{
    border: solid 1px red;
    margin: 50px;
}
#main{
    .border() !important;
}
/* 生成后的 CSS */
#main {
    border: solid 1px red !important;
    margin: 50px !important;
}
~~~
#### 8.循环方法(了解)
Less 并没有提供 for 循环功能，但这也难不倒 聪明的程序员，使用递归去实现。 下面是官网中的一个 Demo，模拟了生成栅格系统。
~~~less
/* Less */
.generate-columns(4);

.generate-columns(@n, @i: 1) when (@i =< @n) {
  .column-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}
/* 生成后的 CSS */
.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}
~~~
#### 9.属性拼接方法
`+_` 代表的是 空格；`+` 代表的是 逗号。

- 逗号
~~~less
/* Less */
.boxShadow() {
    box-shadow+: inset 0 0 10px #555;
}
.main {
  .boxShadow();
  box-shadow+: 0 0 20px black;
}
/* 生成后的 CSS */
.main {
  box-shadow: inset 0 0 10px #555, 0 0 20px black;
}
~~~
- 空格
~~~less
/* Less */
.Animation() {
  transform+_: scale(2);
}
.main {
  .Animation();
  transform+_: rotate(15deg);
}

/* 生成的 CSS */
.main {
  transform: scale(2) rotate(15deg);
}
~~~

#### 10. 实战技巧
下面是官网中的一个非常赞的 Demo
~~~less
/* Less */
.average(@x, @y) {
  @average: ((@x + @y) / 2);
}

div {
  .average(16px, 50px); // 调用 方法
  padding: @average;    // 使用返回值
}

/* 生成的 CSS */
div {
  padding: 33px;
}
~~~
可以说 Less 是一门优雅编程语言。

### 继承
extend 是 Less 的一个伪类。它可继承 所匹配声明中的全部样式。
#### 1. extend 关键字的使用(掌握)
~~~less
/* Less */
.animation{
    transition: all .3s ease-out;
    .hide{
      transform:scale(0);
    }
}
#main{
    &:extend(.animation);
}
#con{
    &:extend(.animation .hide);
}

/* 生成后的 CSS */
.animation,#main{
  transition: all .3s ease-out;
}
.animation .hide , #con{
    transform:scale(0);
}
~~~

#### 2. all 全局搜索替换(掌握)
使用选择器匹配到的 全部声明。
~~~less
/* Less */
#main{
  width: 200px;
}
#main {
  &:after {
    content:"Less is good!";
  }
}
#wrap:extend(#main all) {}

/* 生成的 CSS */
#main,#wrap{
  width: 200px;
}
#main:after, #wrap:after {
    content: "Less is good!";
}
~~~
#### 3. 减少代码的重复性(掌握)
从表面 看来，extend 与 方法 最大的差别，就是 extend 是同个选择器共用同一个声明，而 方法 是使用自己的声明，这无疑 增加了代码的重复性。

方法示例 与上面的 extend 进行对比：

~~~less
/* Less */
.Method{
  width: 200px;
  &:after {
      content:"Less is good!";
  }
}
#main{
  .Method;
}
#wrap{
  .Method;
}

/* 生成的 CSS */
#main{
  width: 200px;
  &:after{
    content:"Less is good!";
  }  
}
#wrap{
  width: 200px;
  &:after{
    content:"Less is good!";
  }  
}
~~~
#### 4.要点
翻译官网
- 选择器和扩展之间 是允许有空格的：pre:hover :extend(div pre).
- 可以有多个扩展: pre:hover:extend(div pre):extend(.bucket tr) - 注意这与 pre:hover:extend(div pre, .bucket tr)一样。
- 这是不可以的，扩展必须在最后 : pre:hover:extend(div pre).nth-child(odd)。
- 如果一个规则集包含多个选择器，所有选择器都可以使用extend关键字。
### 导入
#### 1.导入less文件，可省略后缀(掌握)
~~~less
import "main"; 
//等价于
import "main.less";
~~~
#### 2. `@import`的文字可随意放置(了解)
~~~less
#main{
  font-size:15px;
}
@import "style";
~~~
#### reference(掌握)
Less 中 最强大的特性 使用 引入的 Less 文件，但不会 编译它。
~~~less
/* Less */
@import (reference) "bootstrap.less"; 

#wrap:extend(.navbar all){}
~~~

### 函数
#### 1.类型判断(扩展)
- isnumber
>判断给定的值 是否 是一个数字。
~~~less
isnumber(#ff0);     // false
isnumber(blue);     // false
isnumber("string"); // false
isnumber(1234);     // true
isnumber(56px);     // true
isnumber(7.8%);     // true
isnumber(keyword);  // false
isnumber(url(...)); // false
~~~
- iscolor
>判断给定的值 是否 是一个颜色。
- isurl
>判断给定的值 是否 是一个 url 。
#### 2.颜色操作(扩展)
- saturate
>增加一定数值的颜色饱和度。
- lighten
>增加一定数值的颜色亮度。
- darken
>降低一定数值的颜色亮度。
- fade
>给颜色设定一定数值的透明度。
- mix
>根据比例混合两种颜色。
#### 3. 数字函数(掌握)
- ceil
>向上取整。
- floor
>向下取整。
- percentage
>将浮点数转换为百分比字符串。
- round
>四舍五入。
- sqrt
>计算一个数的平方根。
- abs
>计算数字的绝对值，原样保持单位。
- pow
>计算一个数的乘方。
[了解更多](https://link.juejin.im/?target=http%3A%2F%2Flesscss.cn%2Ffunctions%2F)
### 其他
#### 1. 注释(扩展)
- /* */ CSS原生注释，会被编译在 CSS 文件中。
- /   / Less提供的一种注释，不会被编译在 CSS 文件中。

#### 2.避免编译(了解)
~~~less
/* Less */
#main{
  width:~'calc(300px-30px)';
}

/* 生成后的 CSS */
#main{
  width:calc(300px-30px);
}
~~~
结构：` ~' 值 '`

#### 3. 变量拼串(了解)
在平时工作中，这种需求 太常见了。 在下面例子中， 实现了不同的 transtion-delay、animation、@keyframes
~~~less
.judge(@i) when(@i=1){
  @size:15px;
}
.judge(@i) when(@i>1){
  @size:16px;
}
.loopAnimation(@i) when (@i<16) {

  .circle:nth-child(@{i}){
      .judeg(@i);
      border-radius:@size @size 0 0;
      animation: ~"circle-@{i}" @duration infinite @ease;
      transition-delay:~"@{i}ms";
  }
  @keyframes ~"circle-@{i}" {
      // do something...
  }
  .loopAnimation(@i + 1);
}
~~~
结构： `~"字符@{变量}字符"`
#### 4.使用js(扩展)
因为 Less 是由 JS 编写，所以 Less 有一得天独厚的特性：代码中使用 Javascript 。

~~~less
/* Less */
@content:`"aaa".toUpperCase()`;
#randomColor{
  @randomColor: ~"rgb(`Math.round(Math.random() * 256)`,`Math.round(Math.random() * 256)`,`Math.round(Math.random() * 256)`)";
}
#wrap{
  width: ~"`Math.round(Math.random() * 100)`px";
  &:after{
      content:@content;
  }
  height: ~"`window.innerHeight`px";
  alert:~"`alert(1)`";
  #randomColor();
  background-color: @randomColor;
}
/* 生成后的 CSS */

// 弹出 1
#wrap{
  width: 随机值（0~100）px;
  height: 743px;//由电脑而异
  background: 随机颜色;
}
#wrap::after{
  content:"AAA";
}
~~~