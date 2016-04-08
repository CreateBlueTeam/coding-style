#CSS规范
共同维护前端团队样式表文件

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
│   ├── theme.css
│   ├── m_theme.css
│   ├── theme.min.css
│   ├── m_theme.min.css
│   ├── awesome.css
│   ├── awesome.min.css
├── js/
│   ├── entry.js
└── fonts/
    ├── FontAwesome.otf
    ├── fontawesome-webfont.eot
    ├── fontawesome-webfont.svg
    ├── fontawesome-webfont.ttf
    ├── fontawesome-webfont.woff
    └── fontawesome-webfont.woff2
    ...
````

#代码规范

####分类
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
