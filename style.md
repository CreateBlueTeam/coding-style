#CSS规范
前端团队共同维护样式表文件

#版本
1.0.0

#维护内容
**重置样式表**

- `reset.css`

**UI样式表**

- `global.css`

**皮肤样式表**

- `theme.css` 

**引用字体库**

- [`awesome.css`](http://fontawesome.dashgame.com/)

**图片**

- `images`

#文件结构
````
public/
├── css/
│   ├── reset.css
│   ├── m_reset.css
│   ├── reset.min.css
│   ├── m_reset.min.css
│   ├── global.css
│   ├── m_global.css
│   ├── global.min.css
│   ├── m_global.min.css
│   ├── index.css
│   ├── theme.css
│   ├── m_theme.css
│   ├── theme.min.css
│   ├── m_theme.min.css
│   ├── awesome.css
│   ├── awesome.min.css
├── js/
│   ├── entry.js
├── images/
│   ├── logo.png
└── fonts/
    ├── FontAwesome.otf
    ├── fontawesome-webfont.eot
    ├── fontawesome-webfont.svg
    ├── fontawesome-webfont.ttf
    ├── fontawesome-webfont.woff
    └── fontawesome-webfont.woff2
    ...
````

#代码规范(参考[nec](http://nec.netease.com/)方案)

**文件引用顺序**

按照CSS的性质和用途，将CSS文件分成“公共型样式”、“特殊型样式”、“皮肤型样式”，并以此顺序引用（按需求决定是否添加版本号）。

1. 公共型样式：包括了以下几个部分：“标签的重置和设置默认值”、“统一调用背景图和清除浮动或其他需统一处理的长样式”、“网站通用布局”、“通用模块和其扩展”、“元件和其扩展”、“功能类样式”、“皮肤类样式”。

2. 特殊型样式：当某个栏目或页面的样式与网站整体差异较大或者维护率较高时，可以独立引用一个样式：“特殊的布局、模块和元件及扩展”、“特殊的功能、颜色和背景”，也可以是某个大型控件或模块的独立样式。

3. 皮肤型样式：如果产品需要换肤功能，那么我们需要将颜色、背景等抽离出来放在这里。
```html
<link href="assets/css/global.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/index.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/skin.css" rel="stylesheet" type="text/css"/>
```
**CSS内部的分类**

1. 重置 `reset` 和默认 `base tags` ：消除默认样式和浏览器差异，并设置部分标签的初始样式，以减少后面的重复劳动
2. 布局 `grid` `.g-` ：将页面分割为几个大块，通常有头部、主体、主栏、侧栏、尾部等！
3. 模块 `module` `.m-`：比如导航、登录、注册、各种列表、评论、搜索等！
4. 元件 `unit` `.u-` ：被重复用于各种模块中！比如按钮、输入框、loading、图标等！
5. 功能 `function` `.f-` ：使用率较高的样式,按需使用，具有固定样式表现
6. 皮肤 `skin` `.s-` ：抽离皮肤型的样式，通常为文字色、背景色（图）、边框色等，非换肤型网站通常只提取文字色！
7. 状态 `.z-` ：为状态类样式加入前缀，统一标识，方便识别，她只能组合使用或作为后代出现`.u-ipt.z-hover{} .m-list li.z-current{}`
```css
/* 重置 */
div,p,ul,ol,li {
    margin: 0;
    padding: 0;
}
/* 默认 */
strong,em {
    font-style: normal;
    font-weight: bold;
}
/* 布局 */
.g-sd { 
    float: left; 
    width: 300px;
}
/* 模块 */
.m-logo {
    width: 200px;
    height: 50px;
}
/* 元件 */
.u-btn {
    height: 20px;
    border: 1px solid #333;
}
/* 功能 */
.f-tac {
    text-align: center;
}
.f-cl { 
    content: ''; 
    display: bolck;
    height: 0;
    overflow: visible;
    clear: both;
}
/* 皮肤 */
.s-fc,
a.s-fc:hover { color: #fff; }
/* 状态 */
.u-ipt.z-on {
    display: list-item;
}
```

**命名书写**

- 全部小写英文字母书写
- class选择器用 `-` 链接
- 模块、布局等区分必须添加注释,单独一行
- 命名简短、符合语义
- 组件样式带上组件名
- 多个样式隔行书写、多个选择器隔行书写
- 开头的 `{` 距离选择器一个半角空格
- 结束的 `}` 单独一行并贴紧IDE
- 样式书写顺序 `显示属性` > `自身属性` > `文本及修饰属性`
- 样式尽量使用简写方式
- 先写带有浏览器私有标志的，后写W3C标准的
- 尽量不写,少些Hack

```css
/* head */

.g-header {
    height: 50px;
    background-color: #5ac990;
    color: #fff;
}
.g-container {
    position: relative;
    width: 1000px;
    margin: 0 auto;
}
.logo {
    padding: 5px 0;
}
.g-header .g-nav {
    float: right;
    height: 100%;
}
.g-header .m-nav {
    margin-right: 100px;
}

/* nav */

.m-nav > li {
    position: relative;
    float: left;
    padding: 0 5px;
}
.g-header .m-nav a {
    display: block;
    padding: 10px 25px;
    font-weight: 400;
    font-size: 16px;
    line-height: 30px;
    /*background: #4ba422;*/
}
```

**语义化**

**布局 `.g-`**

文档 `doc` `doc`

头部 `head` `hd`

主体 `body` `bd`

尾部 `foot` `ft`

主栏 `main` `mn`

主栏子容器 `mainc` `mnc`

侧栏 `side` `sd`

侧栏子容器 `sidec` `sdc`

盒容器 `wrap/box` `wrap/box`

    
    
**模块 `.m-` 元件 `.u-`**

导航 `nav` `nav`

子导航 `subnav` `snav`

面包屑 `crumb` `crm`

菜单 `menu` `menu`

选项卡 `tab` `tab`

标题区 `head/title` `hd/tt`

内容区 `body/content` `bd/cont`

列表 `list` `lst`

表格 `table` `tb`

表单 `form` `fm`

热点 `hot` `hot`

排行 `top` `top`

登录 `login` `log`

标志 `logo` `logo`

广告 `advertise` `ad`

搜索 `search` `sch`

幻灯 `slide` `sld`

提示 `tips` `tips`

帮助 `help` `help`

新闻 `news` `news`

下载 `download`	`dld`

注册 `regist` `reg`

投票 `vote` `vote`

版权 `copyright` `cprt`

结果 `result` `res`

标题 `title` `tt`

按钮 `button` `btn`

输入 `input` `ipt`

**功能 `.f-`**

浮动清除 `clearboth` `cl/clearfix`

向左浮动 `floatleft` `fl`

向右浮动 `floatright` `fr`

内联块级 `inlineblock` `ib`

文本居中 `textaligncenter` `tac`

文本居右 `textalignright` `tar`

文本居左 `textalignleft` `tal`

垂直居中 `verticalalignmiddle` `vam`

溢出隐藏 `overflowhidden` `hidden`

完全消失 `displaynone` `none/hide`

字体大小 `fontsize` `fs`

字体粗细 `fontweight` `fw`
    
**皮肤 `.s-`**

字体颜色 `fontcolor` `color`

背景 `background` `bg`

背景颜色 `backgroundcolor` `bgc`

背景图片 `backgroundimage` `bgi`

背景定位 `backgroundposition` `bgp`

边框颜色 `bordercolor` `bdc`
    
**状态 `.z-`**

选中 `selected` `sel`

当前 `current` `crt`

显示 `show` `show`

隐藏 `hide` `hide`

打开 `open` `open`

关闭 `close` `close`

出错 `error` `err`

不可用 `disabled` `dis`

**代码优化**

- 值缩写

```css
.m-title {
    padding: 5px 0 15px;
    -webkit-transition: width .5s linear;
}
```
- 避免耗性能的属性

```css
/* expression */
.class {
    width: expression( this.width > 100 ? '100px' : 'auto' );
}
/* filter */
.class {
    filter: alpha( opacity = 50 );
}
```

- 能用Css不用JavaScript
- 上线前,压缩文件
- 运用css sprite

待续...
