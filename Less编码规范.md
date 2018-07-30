# Less 编码规范
## 一、代码书写规范
### 1.代码格式
#### 1.1 文件

- [建议]：采用 UTF-8 编码，在 CSS 代码头部顶格使用：

```
@charset "utf-8";
```

#### 1.2 缩进

- [强制]：用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
- #### 1.3 规则声明块

- [强制]：为了获得更准确的错误报告，每条声明都应该独占一行。
- [强制]：在规则声明块的左大括号 { 前加一个空格。
- [强制]：在样式属性的冒号 : 后面加上一个空格，前面不加空格。
- [强制]：在每条样式后面都以分号 ; 结尾。
- [强制]：规则声明块的右大括号 } 独占一行。
- [强制]：每个规则声明间用空行分隔。
- [强制]：所有最外层引号使用单引号 ‘ 。
- [强制]：当一个属性有多个属性值时，以逗号 , 分隔，每个逗号后添加一个空格，当单个属性值过长时，每个属性值独占一行

完整示例如下：


```
.g-footer,
.g-header {
    position: relative;
}

.g-content {
    background: linear-gradient(135deg,deeppink25%,transparent25%) -50px0,
                linear-gradient(225deg,deeppink25%,transparent25%) -50px0,
                linear-gradient(315deg,deeppink25%,transparent25%),
                linear-gradient(45deg,deeppink25%,transparent25%);
}

.g-content::before {
    content: '';
}
```


## 2.语法
### 2.1 class命名

- [强制]：class命名只能出现小写英文和破折号 -连接 ，不允许下划线_ 和 驼峰命名法 。(例: anole-btn)原因如下：
> 1.-符合英文语义化，- 标识连子符，_是强调符号；
> 
> 2._underline 选择器命名，在IE6中无效；
> 
> 3.驼峰和 _都不利于SEO搜索引擎检索切词，驼峰无法切成单词，_ 谷歌会切漏关键词；
> 
> 4.输入的时候少按一个shift键，且Google、Yahoo、淘宝、豆瓣在他们的新CSS代码规范中推荐使用 -作为className分隔符。
[强制]：class 名称应当尽可能短，并且意义明确。
[建议]：基于最近的父 class 或基本（base） class 作为新 class 的前缀。
#### 2.2 选择器

- [建议]：少用#，少用*，少用标签选择器
> CSS的渲染方式是“从右往左”渲染的，就拿#header a{}举例，先渲染页面上所有的a签，再去寻找id为header的元素。
- [建议]：避免使用属性选择器

```
#header {
    height: 1rem;  // 推荐用 .header 可以复用，且#选择器权重高，应按需使用，不能滥用
}

#header *{
    padding:0 .3rem;  // 会去遍历所有标签，影响性能
}

#header a {
    font-size:0.28rem; // 同样会去遍历所有<a>标签，影响性能
}
```

#### 2.3 CSS权重优先级
- [理解]：!important > 内联 > # > . > 属性选择器 input[name=''] > 标签选择器 input > *


#### 2.4 CSS执行顺序
- [理解]：行内 > 内联 > 外部引用

#### 2.5 避免使用 !important
- [强制]：除去某些极特殊的情况，尽量不要不要使用 !important。
> !important 的存在会给后期维护以及多人协作带来噩梦般的影响。
> 当存在的样式覆盖层叠时，如果你发现新定义的一个样式无法覆盖一个旧的样式，只有加上 !important 才能生效时，是因为你新定义的选择器的优先级不够旧样式选择器的优先级高。所以，合理的书写新样式选择器，是完全可以规避一些看似需要使用 !important 的情况的。

#### 2.6 样式属性顺序
- [强制]：相关的属性声明应当归为一组，并按照下面的顺序排列：

 
```
1.Positioning Model (布局方式、位置）

2.Box Model (盒模型)

3.Typographic (文本排版)

4. Visual (视觉外观)
```

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。


```
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  margin： 10px;
  padding: 10px;
  overflow: hidden;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  word-wrap: nowrap;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  list-style: none;
  transform: translateX(-50%);
  transition: top .4s ease;
  animation:mymove 5s infinite;

  /* Misc */
  opacity: 1;
  cursor: pointer;
}
```

#### 2.7 缩写与省略
- [强制]：字体顺序：font-style | font-variant | 
```
font-weight | font-size | line-height | font-family
font-style: normal;
font-variant: small-caps;
font-weight: bold;
font-size: 14px;
line-height: 1.5em;
font-family: 'Microsoft YaHei','arial','verdana';
font:normal small-caps bold 14px/1.5em 'Microsoft YaHei','arial','verdana';
```
- [强制]：背景顺序：background-color | background-image | background-repeat | background-attachment | background-position

```
background-color: #F00;
background-image: url(header_bg.gif);
background-repeat: no-repeat;
background-attachment: fixed;
background-position: left top;
background: #F00 url(header_bg.gif) no-repeat fixed left top;
```

- [强制]：外边距和内边距：margin&padding

```
margin: 8px;
 
margin: 4px 0 1.5em -12px;

padding: 1px 2px 3px;
```
- [强制]：列表样式：list-style-type | list-style-position | list-style-image

```
list-style-type: square;
list-style-position: outside;
list-style-image: url(bullet.gif);
list-style: square outside url(bullet.gif);
```

- [强制]：边框顺序：border-width | border-style | 
border-color
```
border-width :1px;
border-style: solid;
border-color: #CCC;
border: 1px solid #CCC;
```
- [强制]：当属性值或颜色参数为 0 – 1 之间的数时，省略小数点前的 0 。

```
color: rgba(255, 255, 255, 0.5);
color: rgba(255, 255, 255, .5);
```

- [强制]：当长度值为 0 时省略单位。

```
margin: 0px auto;
margin: 0 auto;
```

- [强制]：十六进制的颜色属性值使用小写和尽量简写。

```
color: #ffcc00;
color: #fc0;
```

#### 2.8 合理使用使用引号

在某些样式中，会出现一些含有空格的关键字或者中文关键字。

- [强制]：font-family 内使用引号。当字体名字中间有空格，中文名字体及 Unicode 字符编码表示的中文字体，为了保证兼容性，都建议在字体两端添加单引号(或者双引号)：

```
body {
    font-family: 'Microsoft YaHei','黑体-简','\5b8b\4f53';
}
```

- [强制]：background-image 的 url 内使用引号。如果路径里面有空格，旧版 IE 是无法识别的，会导致路径失效，建议不管是否存在空格，都添加上单引号(或者双引号)：

```
div {
    background-image: url('...');
}
```

#### 2.9注释

单行注释

- [强制]：星号与内容之间必须保留一个空格。

```
/* 表格隔行变色 */
```

多行注释

- [强制]：星号要一列对齐，星号与内容之间必须保留一个空格。

```
/**
* Sometimes you need to include optional context for the entire component. 
Do that up here if it's important enough.
*/
```

规则声明块内注释

- [强制]：使用 // 注释，// 后面加上一个空格，注释独立一行。

```
.g-footer {
    border: 0;
    // ....
}
```

文件注释

- [推荐]：文件顶部必须包含文件注释，用 @name 标识文件说明。星号要一列对齐，星号与内容之间必须保留一个空格，标识符冒号与内容之间必须保留一个空格。

```
/**
* @name: 文件名或模块名
* @description: 文件或模块描述
* @author: author-name(mail-name@domain.com)
*          author-name2(mail-name2@domain.com)
* @update: 2018-08-08 10:08
*/
```

> @description为文件或模块描述。</br>
> @update为可选项，建议每次改动都更新一下。

当该业务项目主要由固定的一个或多个人负责时，需要添加@author标识，一方面是尊重劳动成果，另一方面方便在需要时快速定位责任人


### 3.less编码
#### 3.1 文件导入（Importing）

- [强制]：使用 @import (reference) 导入其他less文件，避免导入的样式文件foo.less代码重复打包到最终的css文件中

```
@import (reference) "foo.less";
```

我们用vd生成的项目，已经将CSS公共解决方案文件rework.less集成到node_modules中，如下调用

```
@import (reference) "~rework.less/rework";
@import "~sprite.less";

.placeholder {
  &-404 {
    h3 {
      .text-replace();  // 调用rework样式
      .sprite(@404-slogan); 
  }
}
```

除了提供一些常用样式方案，rework.less中还包含了样式重置，中文网页排版样式，详情查阅源码。

> rework.less源码地址：https://github.com/yincw/rework.less3.2
#### 3.2 混合（Mixins）

- [理解]：将一组可以共用的样式属性，在其他样式规则中混合调用。

```
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}

#menu .list {
  color: #111;
  .bordered;
}

.post {
  color: red;
  .bordered;
}
```

#### 3.3 命名空间（Namespaces）和访问器（Accessors）

- [理解]：我们可以用Less中的命名空间为自己封装一些日常比较常用的类名，以便在其他组件中复用，又不产生冲突。

```
.bundle() {
    .button(@bg-color) {  // 本样式支持传参
        display: block;
        border: 1px solid black;
        background-color: @bg-color;
    }
    .tab {
        background-color: yellow
    }
    .citation {
        background-color: purple
    }
}

.header {
  color: orange;
  .bundle > .button(gray);  // 也可以写作 .bundle .button(gray)
}
```

#### 3.4 嵌套

- [理解]：通过嵌套来实现样式隔离：保证自己组件的样式不影响其他组件的样式，注意层级不要超过3级（影响性能）。

```
.product {
    padding-top: .5rem;
    width: e("calc(100% - 0.6rem)");  // 混合计算编译会忽略单位，解决方案1
    .product-list {
        margin-bottom: .2rem;
        width: calc(~"100% - 0.6rem");  // 混合计算编译会忽略单位，解决方案2
        &:after {
            content: "";
            display: block;
            visibility: hidden;
            clear: both;
            height: 0;
            line-height: 0;
        }
    }
}
```


## 二、代码组织规范
### 1.设计模式（方法论）相关
#### 1.1 CSS方法论
引用方法论是为了让CSS编码具有更好的可读性、维护性、扩展性、复用性。

- [理解]：DRY CSS: Don’t Repeat Your CSS。Less文件内部编码使用。

```
.red-btn,
.blue-btn,
.gray-btn {
    width: 100px;
    height: 36px;
    border: 0;
}
```

- [理解]：OOCSS: Object Oriented CSS。“面向对象的编程”，使样式的数据抽象化、模块化和继承。达到样式复用。

```
.f12 {
  font-size:12px
}
.size1of4 {
  width: 25%
}
.bgBlue {
  background:blue
}


<div className="f12 size1of4 bgBlue">OOCSS</div>
<div className="f12 bgBlue">OOCSS</div>
```

- [理解]：SMACSS：设计架构中推荐有这6类，

1.Base Styles：基础规范，它的定义不会用到class和ID。包含样式重置css reset、工具样式rework。

2.Layout Rules：布局规范，布局是一个网站的基本，SMACSS还约定了一个前缀 l-/layout- 来标识布局的class。


```
.layout-header {}
.layout-container {}
.layout-sidebar {}
.layout-content {}
.layout-footer {}
```

3.Module Rules：模块规范，将样式模块化就能达到复用和可维护的目的。SMACSS中的模块具有自己的一个命名，下属类皆有同一个前缀。


```
.todolist{}
.todolist-title{}
.todolist-image{}
.todolist-article{}
```

4.State Rules：状态规范，描述的是任一元素在特定状态下的外观。


```
// html
<div class="is-hidden">
    ...
</div>
// css
.is-hidden{
    display: none;
}
```

5.Theme Rules：主题规范，描述了页面主题外观，一般是指颜色、背景图。Theme Rules 可以修改前面 4个类别的样式，且应和前面4个类别分离开来（便于切换，也就是“换肤”）。

我们引用主题规范的思想，但是不必使用它的代码覆盖的实现方式。我们有更适合我们简便方式实现主题规范。

6.Changing State: 动态样式规范，我们静态CSS完成后，会有一些动态交互样式的覆盖行为。改变State Rules的样式属性。

#### 1.2 vd创建的项目实现方案：

1.在.vd文件夹中，project.json文件有配置主题样式的对象，配置好后可以全局引用。

project.json文件中定义主题样式：


```
"theme": {
  "hd": "2px",
  "primary-color": "#1890ff",
  "border-radius": "4px",
  "brand-primary": "#0b87fd",
  "brand-primary-tap": "#0b87fd"
}
```

button.less 文件直接引用，不需要import文件：


```
.anole {
    &-btn-primary {
        border-radius: @border-radius;
        background-color: @primary-color;
    }
}
```

2.引用Theme.less中定义的变量样式。

theme.less 文件定义：


```
@primary-color: #1890ff;
@title-color: #000;
@title-size: 0.36rem;
@text-color: #333;
@text-size: 0.28rem;
@bg-color: #f6f6f6;
```

button.less 文件引用：

```
@import 'theme.less';

.anole {
    &-btn-primary {
        color: @text-color;
        background-color: @primary-color;
    }
}
```

### 2.语法检测
第一步：项目根目录新建文件stylelint.config.js


```
module.exports = {
  "extends": "stylelint-config-standard",
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "node": true,
    "commonjs": true,
    "amd": true,
    "jest": true
  },
  "plugins": [
    // "stylelint-z-index-value-constraint",
  ],
  "rules": {
    // 缩进2个空格
    "indentation": [4, {
      "except": ["value"],
      "severity": "warning",
      "message": "Please use 2 spaces for indentation. Tabs make The Architect grumpy."
    }],
    // 小数前面的 0
    "number-leading-zero": "never",
    // 不允许空规则
    "block-no-empty": true,
    "max-empty-lines": 2,
    "color-no-invalid-hex": true,
    // 注释空行前
    "comment-empty-line-before": ["always", {
      "ignore": ["stylelint-commands", "between-comments"],
    }],
    // 注释空行后
    "declaration-colon-space-after": "always",
    // 排除前面空行
    "rule-empty-line-before": ["always", {
      "except": ["first-nested"],
      "ignore": ["after-comment"],
    }],
    // 单位白名单
    "unit-whitelist": ["rem", "%", "s", "deg", "px", "em", "vh", "vm"],
    // z-index 等级范围
    // "plugin/z-index-value-constraint": {
    //   "min": 0,
    //   "max": 999
    // }
  },
  "root": true
};
```

第二步：webpack.config.js中配置，安装依赖包
```
yarn add stylelint-webpack-plugin
```



```
import StyleLintPlugin from 'stylelint-webpack-plugin';

...

plugins：[
    ...,
    new StyleLintPlugin({
      context: "src",
      configFile: join(__dirname, './stylelint.config.js'),
      files: '**/*.less',
      failOnError: false,
      quiet: true,
      syntax: 'less'
    }),
    ...
]

...
```

###### 参考资料：
> 
> 史上最全的CSS hack方式一览：https://blog.csdn.net/freshlover/article/details/12132801
> 
> 前端工程师手册：https://leohxj.gitbooks.io/front-end-database/html-and-css-basic/css-write-and-name.html
> 
> 如何规范 CSS 的命名和书写？：https://www.zhihu.com/question/19586885
> 
> 猫哥_kaiye | 编程笔记：http://www.cnblogs.com/kaiye/archive/2011/06/13/3039046.html
> 
> 肯扑seoz928的博客： http://blog.sina.com.cn/s/blog_89aeb27f0100vk0o.html
> 
> 参考链接：https://github.com/cssmagic/blog/issues/42
> 
> DRY CSS：http://vanseodesign.com/css/dry-principles/
> 
> OOCSS: http://oocss.org/
> 
> SMACSS：https://smacss.com/
> 
> 参考Less.js中文网： http://lesscss.cn/features/#import-options-reference
> 
> web项目开发 之 前端规范 --- CSS编码规范：https://blog.csdn.net/xllily_11/article/details/51249120
> 
> 复杂应用的 CSS 性能分析和优化建议：http://www.orzpoint.com/profiling-css-and-optimization-notes/
> 
> 精简高效的CSS命名准则/方法：http://www.zhangxinxu.com/wordpress/2010/09/精简高效的css命名准则方法
> 
> stylelint：https://github.com/stylelint/stylelint/blob/master/docs/user-guide/rules.md
> 
> 在webpack中使用stylelint（一） Quick Start：https://www.jianshu.com/p/4ed317615152