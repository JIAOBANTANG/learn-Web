<p align="center">
	<img src="https://github.com/JIAOBANTANG/learn-Web/raw/master/images/learn.png" width="600"/>
</p>


# HTML基础
## 什么是HTMl
`HTML(Hypertext Markup Language)即超文本标记语言`
2014年HTML定稿

## HTML特点
- HTML不需要编译，直接由浏览器运行
- HTML文件是一个文本文件
- HTML文件必须使用html或者xml为文件后缀
- HTML大小写不敏感
## HTML基本结构
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
~~~
## HTMl标签
*语法*：`<标签名> </标签名>`
*例如*：`<html> </html>`
*规范*：
- 1.<>括起来
- 2.一般成对出现，分开始标签和结束标签,结束标签比开始标签多了一个/
- 3.单标签：没有结束标签 `<hr/>`
## HTML元素
*从开始标签到结束标签的所有代码，称为HTML元素。*
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <p>这是我的第一个网页</p>
</body>
</html>
~~~
## HTML标签属性
*语法*：`<标签名 属性名1="值" 属性名2="值" ... > ….. </标签名>`
## HTML注释
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <p>这是我的第一个网页</p>
    <!--这里是注释 我不会在网页中显示-->
</body>
</html>
~~~

## DOCTYPE文档类型声明 网页编码
~~~html
<!DOCTYPE html> <!--声明必须放在HTML文档第一行 声明是html文档-->
<html lang="en">
<head>
    <meta charset="UTF-8"><!--声明页面编码档-->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <p>这是我的第一个网页</p>
    <!--这里是注释 我不会在网页中显示-->
</body>
</html>
~~~


## 文字和段落标签
*标题标签*：`<h1></h1>~<h5></h5>`
*段略标签*：`<p></p>`
段略标签有align对齐属性
- `<p align="left">左对齐内容</p>` <p align="left">左对齐内容</p>
- `<p align="right">右对齐内容</p>` <p align="right">右对齐内容</p>
- `<p align="center">居中对齐内容</p>`  <p align="center">居中对齐内容</p>
- `<p align="justify">对行进行伸展，这样每行都可以有相等的长度</p>`<p align="justify">对行进行伸展，这样每行都可以有相等的长度</p>
*换行标签*：`<br/>`
*水平线*：`<hr/>`

属性
- width 设置水平线宽度，可以是像素或百分比
- color 水平线颜色
- align 设置水平线居中
- noshade 设置水平线无阴影
~~~html
<!--我是居中对齐的一条线-->
 <hr width="1000" color="pink" align="center" >
~~~
*特殊符号*
- `&lt;` < 小于号或显示标记
- `&gt;` > 大于号或显示标记
- `&reg;` ® 已注册
- `&copy;` © 版权
- `&trade;` ™ 商标
- `&nbsp;` Space 不断行的空白

## 列表标签
*无序列表*
type 属性
- dics 圆点
- square 正方形
- circle 空心圆
~~~html
<ul type="circle">
    <li>列表项</li>
    <li>列表项</li>
    ……
</ul>
~~~


*有序列表*
type 属性
- 1 数字1,2...
- a 小写字母a,b...
- A ...
- i 小写罗马字母
- I 大写罗马字母

~~~html
<ol type="I">
    <li>列表项</li>
    <li>列表项</li>
……
</ol>
~~~

*定义列表*
~~~html
<dl>
    <dt>定义列表项</dt>
    <dd>列表项描述</dd>
    <dd>列表项描述</dd>
    <dt>定义列表项</dt>
    <dd>列表项描述</dd>
……
</dl>
~~~
## 图像和超链接标签
### 图像
*语法* `<img src=“” alt=“” …/>`
*img属性* 
- Src（必写） URL 显示图像的URL
- alt 文字 图像替代文本
- height 数值和百分比 图像的高
- width 数值和百分比 图像的宽

### 超链接
*语法* `< a href=“”>内容</a>`
*属性* 
- href 链接地址
- target 链接的目标窗口 _self、_blank、_top、_parent
- title 链接提示文字
- name 链接命名

#### 锚点
##### 同一页面
~~~html
    <a href="#锚1" >一锚</a>
    <a href="#锚2" >二锚</a>
    <a href="#锚3" >三锚</a>
    ...
    <a name="锚1" href="">一锚</a>
    <a name="锚2" href="">二锚</a>
    <a name="锚3" href="">三锚</a>
~~~

##### 不同页面
~~~html
    <a href="网页名称#锚1" >一锚</a>
    <a href="网页名称#锚2" >二锚</a>
    <a href="网页名称#锚3" >三锚</a>
    ...
~~~
#### 电子邮箱链接
`< a href=“mailto:邮件地址”>……</a>`
mailto 四个常用的参数
- subject -- 代表邮件的标题
- body -- 代表邮件的内容
- cc -- 代表一个抄送对象
- bcc -- 代表一个暗送对象
~~~html
< a href="mailto:jiaobantang@gmail.com?subject=你好啊&body=啥都没有?cc=你的邮箱">给不发送一封简单邮件</a>
~~~
## 表格
~~~html
    <table border="1"> <!--表格 -->
        <caption>我是标题</caption><!--表格标题 居中显示-->
        <tr><!--行-->
            <th><!--表头-->
                列名
            </th>
            <th>
                我是表头
            </th>
        </tr>
        <tr>
            <td><!--单元格-->
                我知道
            </td>
            <td>
                我知道
            </td>
        </tr>
    </table>
~~~
### table 属性
`border：`表格边框 cellspacing：单元格间的间距
`cellpadding：`单元格的内容与其边框的内边距 align：表格的对齐方式，通常是left，center，right
`bgcolor：`表格的背景颜色 background：表格的背景图片
`width：`表格宽度 height：表格高度
`border-collaspe：`collaspe：边框合并，不叠加 cellspacing：0：边框合并，但合并之后的边框宽度等于前两个边框宽度之和
### 单元格属性
`width：`单元格宽度height：单元格高度
`align：`单元格内文本的对齐方式,通常是左，中，右 left，center，right
`valign：`单元格内文本的对齐方式,通常是上，中，下 top，middle，bottom
`nowrap：`在为设置单元格宽度时，当文本长度宽于单元格宽度，将要换行时，该标签会使其不换行

### 单元格跨行跨列
`rowspan：`跨行标签，表示跨了多少行
`colspan：`跨列标签，表示跨了多少列
