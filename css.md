# 用多重背景单标签实现气泡按钮点击效果

# 使用css 径向渐变实现舞台灯光聚焦效果
html 代码如下：
```
<div class="light-container"></div>
```

css 代码如下：
```
.light-container {
  width: 200px;
  height: 200px;
  background-color: black;
  background-image: radial-gradient(
    circle at 50% 50%,
    rgba(255, 255, 255, 0.5) 0%,
    rgba(255, 255, 255, 0.05) 70%,
    rgba(255, 255, 255, 0.01) 80%
  );
  background-size: 50% 50%;
  background-position: center;
}
```

# 使用 线性渐变实现顶部滚动进度条
html 代码如下：
```
<div class="box">Start editing to see some magic happen!Start editing to see some magic happen!Start editing to see some magic happen!...</div>
```
css 代码如下：
```
.box {
  position: relative;
  padding: 50px;
  font-size: 24px;
  line-height: 30px;
  background-image: linear-gradient(to right top, green 50%, #eee 50%);
  background-repeat: no-repeat;
  background-size: 100% calc(100% - 100vh + 5px);
  z-index: 1;
}

.box::after {
  content: "";
  position: fixed;
  top: 5px;
  left: 0;
  bottom: 0;
  right: 0;
  background: #fff;
  z-index: -1;
}
```
当内容出现滚动条后，可以看到顶部出现滚动条。

# 使用 线性渐变 实现线条 border 效果
html 代码如下：
```
<div class="border-effect"></div>
```
css 代码如下：
```
.border-effect {
  width: 200px;
  height: 200px;
  border: 10px solid;
  border-image: linear-gradient(
    to right,
    #000 0%,
    orange 30%,
    #000 50%,
    yellow 80%,
    blue 90%,
    green 100%
  );
  border-image-slice: 1;
}
```

# 使用 css 线性渐变实现箭头符号
html 代码如下：
```
<div className="arrow"></div>
```
css 代码如下：
```
.arrow {
  position: relative;
  width: 100px;
  height: 100px;
}

.arrow::before,
.arrow::after {
  content: "";
  position: absolute;
  top: 50%;
  width: 50%;
  height: 2px;
  background-color: #000;
}

.arrow::before {
  left: 0;
  transform-origin: top right;
  transform: rotate(45deg);
  background: linear-gradient(to right, red 0%, transparent 100%);
}

.arrow::after {
  right: 0;
  transform-origin: top left;
  transform: rotate(-45deg);
  background: linear-gradient(to left, green 0%, transparent 100%);
}
```

# 使用 渐变实现 TV 噪音动画

# 使用 background-attachment 实现毛玻璃效果 

可以通过设置一个带有背景图片的元素，并将其覆盖在页面的其他内容上面。使用 position: fixed 和 top: 0 等属性来实现这一点。

html 代码如下：
```
<div>
  <h2>
    Start editing to see some magic happen!
  </h2>
  <div class="bg"></div>
</div>
```

css 代码如下：
```
...

.bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  background-image: url("https://xx.com/bg.png");
  background-size: cover;
  filter: blur(10px); // 使用 filter 属性来创建毛玻璃效果
  background-attachment: fixed; // 由于元素设置了 position: fixed 和 z-index: -1，它会出现在页面的顶部并位于其他内容的后面。可以使用 background-attachment 属性来指定背景图像的滚动行为。通过将其设置为 fixed，可以使背景图像保持固定，不随页面滚动而移动。
}
```

# 实现 Google LOGO 

html 代码如下：
```
  <div class="logo">
      <span class="g">G</span>
      <span class="o1">o</span>
      <span class="o2">o</span>
      <span class="g">g</span>
      <span class="l">l</span>
      <span class="e">e</span>
    </div>
```
css 代码如下： 
```
.logo {
  font-size: 80px;
  letter-spacing: -2px；
  font-weight: 700;
  font-family: Ebrima,Arial,Helvetica, Sans-Serif;
}

span.g{
  color: rgb(66,133,244);
}
span.o1{
  color: rgb(234,67,53);
}
span.o2{
  color: rgb(251,188,5);
}
span.l{
  color: rgb(52,168,83);
}
span.e{
  color: rgb(234,67,53);
  display:inline-block;   /*设置元素旋转*/
  transform:rotate(-15deg);

}
```

# 使用 div 标签实现抖音 LOGO

html 代码如下：
```
<div class="logo-douyin">
  <div class="logo"></div>
  <div class="logo logo-red"></div>
</div>
```
css 代码如下：
```
.logo-douyin {
  position: relative;
  width: 200px;
  padding: 100px;
  margin: 100px auto;
}

.logo {
  position: absolute;
  top: 0;
  left: 0;
  width: 47px;
  height: 218px;
  z-index: 1;
  background: #24f6f0;
  mix-blend-mode: lighten;
}
.logo::after {
  content: '';
  position: absolute;
  width: 140px;
  height: 140px;
  border: 40px solid #24f6f0;
  border-top: 40px solid transparent;
  border-right: 40px solid transparent;
  border-left: 40px solid transparent;
  top: -110px;
  right: -183px;
  border-radius: 100%;
  transform: rotate(45deg);
  z-index: -10;
}
.logo::before {
  content: '';
  position: absolute;
  width: 100px;
  height: 100px;
  border: 47px solid #24f6f0;
  border-top: 47px solid transparent;
  border-radius: 50%;
  top: 121px;
  left: -147px;
  transform: rotate(45deg);
}

.logo-red {
  left: 10px;
  top: 10px;
  background: #fe2d52;
  z-index: 100;
  animation: move-to-mix-blend 6s infinite;
}
.logo-red::before {
  border: 47px solid #fe2d52;
  border-top: 47px solid transparent;
}
.logo-red::after {
  border: 40px solid #fe2d52;
  border-right: 40px solid transparent;
  border-top: 40px solid transparent;
  border-left: 40px solid transparent;
}

@keyframes move-to-mix-blend {
  0% {
    transform: translate(200px);
  }
  50% {
    transform: translate(0px);
  }
  100% {
    transform: translate(0px);
  }
}
```
摘自： https://juejin.cn/post/7016611927111499813

# 使用 box-shadow 实现霓虹氖灯文字效果

```
.circle {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  box-shadow: 0 0 20px #fff,
              0 0 30px #fff,
              0 0 40px #fff,
              0 0 70px #ff00de,
              0 0 80px #ff00de,
              0 0 100px #ff00de,
              0 0 150px #ff00de;
}
```

# 使用阴影实现文字的 3D 氖灯效果

可以使用文本阴影属性来实现:

```
text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #fff, 0 0 40px #ff00de, 0 0 70px #ff00de, 0 0 80px #ff00de, 0 0 100px #ff00de, 0 0 150px #ff00de;
```
注意：阴影效果可能会影响文本的可读性，因此请考虑使用对比鲜明的颜色和清晰的字体以确保效果的可读性。

# 使用 box-shadow / 渐变实现内切角 

- box-shadow

要使用 box-shadow 属性来实现内切角，可以按照以下步骤操作：

1.创建一个带有内切角的元素。

2.使用 box-shadow 属性来模拟内切角的效果。可以通过在 box-shadow 中使用 inset 关键字来创建一个内阴影。接下来，需要使用偏移量、模糊半径和扩展半径来定义阴影的大小和位置。要实现内切角效果，需要在第一个阴影中使用负的水平和垂直偏移量，并使用正的扩展半径来确保阴影完全覆盖内切角。

```
.box {
  width: 200px;
  height: 200px;
  background-color: #f00;
  box-shadow: -20px 20px 0 20px #fff inset;
}
```

- 渐变

要使用渐变来实现内切角，可以按照以下步骤操作：

1.创建一个带有内切角的元素。

2.使用渐变来在内切角处添加渐变效果。可以使用 linear-gradient 或 radial-gradient，具体取决于您希望实现的效果。通过在渐变中使用与元素背景色相同的颜色，可以创建一个平滑的过渡效果。

3.使用 clip-path 属性将元素剪裁成所需的形状。可以使用 polygon() 函数来创建一个多边形形状，该函数需要提供每个顶点的 x 和 y 坐标。

```
.box {
  width: 200px;
  height: 200px;
  background-color: #f00;
  background-image: linear-gradient(to bottom right, transparent 0%, transparent 50%, #fff 50%, #fff 100%);
  clip-path: polygon(0 0, 180px 0, 200px 20px, 200px 180px, 180px 200px, 0 200px, 0 0);
}
```

# 新特性 @property 的解读

在 CSS 中，@property 是一个新的特性，可以用来创建 CSS 属性（property）。这个特性目前处于实验性阶段，主要是为了方便创建自定义的 CSS 属性。
```
@property --primary-color {
  syntax: '<color>';
  initial-value: black;
  inherits: false;
}

.button {
  background-color: var(--primary-color);
  color: white;
}
```
在这个示例中，我们使用 @property 创建了一个自定义属性 --primary-color，它的值是颜色值（<color>）。我们还指定了它的初始值为 black，并且不会被继承。

在 .button 样式规则中，我们使用了 var() 函数引用这个自定义属性作为 background-color 属性的值。由于这个自定义属性是可重复使用的，我们可以在其他地方引用它，而不需要写出具体的颜色值。

需要注意的是，@property 只是定义了一个自定义属性，它并不会对页面的布局和样式产生直接的影响。因此，在使用 @property 的时候，需要考虑它的实际用途，以及如何将它与其他 CSS 特性结合使用。同时，需要注意浏览器的兼容性，目前还有一些浏览器不支持 @property 特性。

# 奇妙的 CSS 遮罩 mask 属性

mask 属性用于创建遮罩效果，可以将一个元素遮罩成任何形状，例如圆形、三角形、文本或自定义形状。mask 属性的使用方法与 clip-path 和 shape-outside 相似，可以使用 SVG 路径或 CSS 函数定义遮罩形状。与 clip-path 和 shape-outside 不同的是，mask 属性还可以使用图像或 SVG 元素作为遮罩，这使得我们可以创建出更加复杂的遮罩效果。

例子：
```
<div class="mask-example"></div>
```
```
/* 使用渐变作为遮罩: 这里渐变从上到下，逐渐从透明变成黑色，从而形成一个向下渐变的遮罩效果。 */
.mask-example {
  width: 200px;
  height: 200px;
  background-image: linear-gradient(to bottom, transparent, black);
  -webkit-mask-image: linear-gradient(to bottom, transparent, black);
  mask-image: linear-gradient(to bottom, transparent, black);
}

/* 使用 SVG 路径作为遮罩: 这里 mask.svg 是一个 SVG 文件，定义了一个自定义的形状。可以使用 mask.svg#id 指定 SVG 文件中的特定 ID */
.mask-example {
  width: 200px;
  height: 200px;
  -webkit-mask-image: url(mask.svg);
  mask-image: url(mask.svg);
}

/* 使用图像作为遮罩: 这里 mask.png 是一个 PNG 图像文件，它的颜色和透明度值将决定遮罩效果。图像中的非透明区域将显示元素的内容，而透明区域则将隐藏元素的内容 */
.mask-example {
  width: 200px;
  height: 200px;
  background-image: url(image.jpg);
  -webkit-mask-image: url(mask.png);
  mask-image: url(mask.png);
}
```

需要注意的是，mask 属性的浏览器支持度并不是非常好，需要仔细考虑兼容性和降级方案。

两种降级替代方案：

1. 使用 clip-path 或 shape-outside 替代。这两个属性也可以用来创建不同形状的遮罩效果，虽然不如 mask 属性灵活，但兼容性更好，可以在不支持 mask 属性的浏览器上显示相似的效果。

2. 使用图片作为背景。如果需要显示特定形状的元素，可以将形状保存为图像，并将其作为背景图片显示在元素上。虽然这种方法不如 mask 属性灵活，但它具有很好的兼容性，适用于所有浏览器。

代码：
```
/* 使用 clip-path 作为遮罩 */
.mask-example {
  width: 200px;
  height: 200px;
  background-color: red;
  -webkit-clip-path: circle(50% at 50%);
  clip-path: circle(50% at 50%);
}

/* 使用图片作为背景 */
.mask-example {
  width: 200px;
  height: 200px;
  background-image: url(shape.png);
  background-size: cover;
}
```

# 你不知道的 clip-path、shape-outside 属性

clip-path 属性指定一个剪切路径，可以将元素剪切成任何形状，例如圆形、三角形或自定义形状。clip-path 属性可以使用 SVG 路径或 CSS 函数定义剪切路径。

例子：让一张图片呈现为圆形
```
<img src="example.jpg" alt="Example Image">
```
```
img {
  clip-path: circle(50%);
}
```
这里，circle() 函数将图片剪切为圆形，半径为 50%，即图片的宽度和高度的一半。

shape-outside 属性指定一个形状，可以使得文本或其他元素避开指定形状的区域。该属性可以使用 CSS 函数或 SVG 路径来定义形状。

例子：让一段文本绕着一个形状排列
```
<div class="shape"></div>
```
```
.shape {
  float: left;
  width: 200px;
  height: 100px;
  shape-outside: rectangle(0, 0, 200px, 100px);
}

p {
  margin: 0;
}
```
这里，shape-outside 属性使用 rectangle() 函数指定一个矩形形状，并且 float 属性将矩形浮动在左侧。p 元素的 margin 设置为 0，以防止文本与矩形之间出现空白间隔。

使用 clip-path 和 shape-outside 属性可以创建出各种有趣的效果，例如让文本环绕在图片周围或者创建出复杂的形状。然而，这些属性的浏览器支持度并不是非常好，需要仔细考虑兼容性和降级方案。

# 真正了解 @font-face 的规则

@font-face 是一个 CSS 规则，它允许开发人员在网站上使用自定义字体。使用 @font-face 规则可以将自定义字体文件（通常是 .woff 或 .woff2 格式的字体文件）嵌入网页，使网页能够在用户的计算机上显示自定义字体，而不必依赖于用户计算机上已安装的字体。

以下是 @font-face 规则的基本语法：
```
@font-face {
  font-family: 'FontName';
  src: url('fontname.eot');
  src: url('fontname.eot?#iefix') format('embedded-opentype'),
       url('fontname.woff2') format('woff2'),
       url('fontname.woff') format('woff'),
       url('fontname.ttf') format('truetype'),
       url('fontname.svg#fontname') format('svg');
  font-weight: normal;
  font-style: normal;
}
```
- font-family：定义字体的名称，必须与 CSS 中其他字体使用的名称一致。
- src：定义字体文件的位置和格式。可以指定多个不同格式的字体文件，以便在不同的浏览器和设备上使用最适合的格式。
- font-weight：定义字体的粗细程度，通常为 normal 或 bold。
- font-style：定义字体的样式，通常为 normal 或 italic。
- 
在使用 @font-face 规则时，需要考虑以下几点：

1. 字体文件的大小应该尽可能小，以便减少加载时间。
2. 尽可能提供多个不同格式的字体文件，以便在不同的浏览器和设备上使用最适合的格式。
3. 在定义字体名称时，应该避免使用与系统默认字体名称相同的名称，以避免与系统默认字体发生冲突。
4. 需要确保字体文件的版权问题，只使用拥有版权的字体文件。

#### format 的作用是什么:

在 @font-face 规则中，format 属性用于指定字体文件的格式，以便浏览器可以选择最适合的字体格式进行下载和显示。这是因为不同的浏览器支持不同的字体格式。

以下是常见的几种字体文件格式及其对应的 MIME 类型和浏览器支持情况：

- format('woff2')：Web Open Font Format 2.0，MIME 类型为 font/woff2，现代浏览器均支持。
- format('woff')：Web Open Font Format，MIME 类型为 font/woff，现代浏览器均支持。
- format('truetype')：TrueType 字体格式，MIME 类型为 font/truetype，现代浏览器和老旧浏览器均支持。
- format('opentype')：OpenType 字体格式，MIME 类型为 font/opentype，现代浏览器和老旧浏览器均支持。
- format('embedded-opentype')：Embedded OpenType 字体格式，MIME 类型为 application/vnd.ms-fontobject，主要用于 IE8 及以下版本的浏览器。

通过指定多种字体文件格式和对应的 MIME 类型，浏览器可以自动选择最适合的字体格式进行下载和显示，从而提高页面加载速度和字体显示质量。


# 理解 font-size 与 ex/em/rem 的关系

font-size、ex、em 和 rem 都是用来设置 HTML 元素的文本大小的属性，它们之间有着一定的关系。

- font-size
font-size 是用来设置文本字体大小的属性。它的单位可以是像素、百分比、em 或 rem。其中，像素和百分比是绝对单位，而 em 和 rem 是相对单位。在使用 font-size 时，要注意单位的选择，因为不同的单位在不同的设备上可能会呈现不同的大小。

- ex 和 em
ex 和 em 都是相对单位，它们的大小是根据当前文本字体的大小而定的。其中，ex 的大小等于当前字体中小写字母 "x" 的高度，而 em 的大小等于当前字体中大写字母 "M" 的宽度。

因此，如果要设置一个元素的文本大小为当前字体大小的两倍，可以使用 font-size: 2em;，或者使用 font-size: 200%;，因为 2em 和 200% 都是相对于当前字体大小而言的。

- rem
rem 也是相对单位，不过它的大小是相对于根元素的字体大小而定的。在 HTML 中，根元素指的是 <html> 元素。因此，如果要设置一个元素的文本大小为根元素字体大小的两倍，可以使用 font-size: 2rem;。

总之，font-size、ex、em 和 rem 都是用来设置 HTML 元素的文本大小的属性，它们之间的关系是相对的。

# CSS 层叠性

CSS层叠性（Cascading）是指在Web页面中，当多个CSS规则应用于同一元素时，浏览器会根据一定的优先级和规则来决定应用哪个规则。

具体来说，当多个规则选择器选中同一个元素时，浏览器会按照以下优先级进行处理：

- 重要性（!important）：被标记为重要的规则会覆盖其他规则。
- 显式权重（权重值）：权重值越大的规则优先级越高。
- 位置：后定义的规则会覆盖先定义的规则。
- 特殊性：选择器特殊性越高的规则优先级越高。

如果多个规则的优先级相同，则按照“就近原则”进行处理，即离被选择元素最近的规则会被应用。

# CSS 中的 z-index

z-index 是 CSS 属性之一，用于控制元素的堆叠顺序。它决定了元素在 z 轴（垂直于屏幕的轴）方向上的显示顺序，即哪个元素显示在顶部，哪个元素显示在底部。

z-index 属性的值是一个整数，通常为正整数，表示元素在堆叠顺序中的优先级。值越大的元素，显示在越上层。如果两个元素具有相同的 z-index 值，则它们的显示顺序将由它们在 HTML 中的顺序决定。

需要注意的是，只有定位元素（position 属性值为 relative、absolute 或 fixed）才能设置 z-index 属性。在没有设置定位的情况下，z-index 属性将无效。

# absolute 的 margin:auto 居中

margin: auto; 可以用于水平居中一个元素，但是要使其在绝对定位中居中，还需要将其父元素设置为相对定位，然后将该元素的左、右、上、下位置设置为 0，如下所示：
```
.parent {
  position: relative;
}

.child {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
}

```
这将使子元素在父元素中居中。但此方法只适用于已知宽高的元素，如果想要在不知道元素大小的情况下居中，应考虑使用 transform 属性。

# line-height 为何能让内联元素居中

line-height 属性可以让内联元素在其包含块内垂直居中，这是因为 line-height 指定了行框盒子的高度，而行框盒子的高度通常大于文本的实际高度。具体来说，行框盒子的高度是由以下三个部分组成：

- 文本的实际高度；
- 顶部内边距和顶部外边距的和；
- 底部内边距和底部外边距的和。

当 line-height 的值大于文本的实际高度时，行框盒子的高度就会增加，从而使得内联元素在其包含块内垂直居中。举个例子，如果一个内联元素的高度是 20px，而 line-height 的值为 30px，那么这个内联元素将会在垂直方向上居中，因为行框盒子的高度是 30px，比内联元素的高度要大。

需要注意的是，line-height 属性不是所有内联元素都可以使用的，只有在包含文本的内联元素才能使用。如果内联元素不包含文本，那么 line-height 属性将不起作用。

# border 的透明边框技巧

要创建一个透明边框，可以使用 CSS3 的 border 属性和 rgba() 函数

1. 使用 border 属性定义边框的宽度、样式和颜色

```
border: 1px solid #000;
```

2. 使用 rgba() 函数来定义颜色，并将 alpha 值设置为 0，表示完全透明

```
border-color: rgba(0, 0, 0, 0);
```

3.将边框的颜色与背景颜色匹配，这样边框看起来就像是透明的

```
border-color: rgba(255, 255, 255, 0);
background-color: #fff;
```

4. 使用 box-shadow 属性来创建一个看起来像边框的透明投影

```
box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.2);
```

这个技巧会在元素周围创建一个 1 像素的投影，看起来就像是边框。可以通过调整 box-shadow 的模糊度、偏移量和颜色来创建不同的效果。

# 正确理解 CSS 中的幽灵空白节点

在 CSS 中，幽灵空白节点通常指在 HTML 中没有明确写出的空白字符（例如空格、回车符等），但是这些空白字符会对页面的布局和样式产生影响。

具体来说，当 HTML 中连续的多个空格或回车符被浏览器解析时，它们会被合并为一个空格字符，并且这个空格字符会被用于排版和布局。这就意味着，即使没有在 HTML 中写出任何空格或回车符，浏览器仍然会在页面中产生一些看不见的空白字符，这些空白字符被称为“幽灵空白节点”。

这些幽灵空白节点可能会对页面的布局和样式产生影响，因为它们占据了页面中的一些空间，可能会影响元素的对齐和排列。为了解决这个问题，可以使用 CSS 的一些技巧，如使用浮动、清除浮动等来控制幽灵空白节点的影响。

# 正确看待 margin 值合并

Margin 值合并是指当两个相邻的元素的 margin 值相遇时，它们之间的 margin 值将被合并为一个值，而不是简单相加。这个行为被称为 "margin 坍塌"。

Margin 坍塌是 CSS 中一个常见的现象，也是一个容易被忽略的细节。正确理解 margin 坍塌的行为可以让你更好地控制元素之间的间距，并且避免一些常见的布局问题。

在理解 margin 坍塌时，需要注意以下几点：

1. 坍塌只会发生在垂直方向上，水平方向上不会发生。

2. 坍塌只会发生在相邻的元素之间，如果中间隔着一个非空内容或者空白字符的元素，那么 margin 就不会坍塌。

3. 当两个 margin 值相等时，它们会坍塌成一个值；当它们不相等时，它们会取两个 margin 值中较大的那个值。

4. 如果一个元素的 margin-top 和 margin-bottom 都和相邻元素的 margin-top 或 margin-bottom 发生了坍塌，那么这两个值都会被坍塌，而不是只有其中一个。

总的来说，margin 坍塌是 CSS 中一个普遍存在的现象，对于正确布局元素是很重要的。理解 margin 坍塌的规则，可以帮助我们更好地控制元素之间的间距，从而实现更加优雅和灵活的布局。


# 深入理解 margin:auto

在CSS中，margin属性可以用来控制一个元素的外边距，而将margin设置为auto的效果是让该元素的外边距自动适应其父元素的尺寸。具体来说，margin:auto会使元素的左右外边距相等，并且使元素在水平方向上居中对齐。

以下是margin:auto的一些深入理解：

1. 只适用于块级元素

margin:auto只适用于块级元素，行内元素是不支持设置margin的。如果要在行内元素中使用margin，需要将其转换为块级元素，例如使用display:block或display:inline-block。

2. 水平居中对齐

将margin设置为auto会使元素在水平方向上居中对齐。这是因为当左右外边距都设置为auto时，浏览器会自动计算这两个外边距的值，使它们相等，从而实现水平居中对齐。

2. 垂直居中对齐

将margin设置为auto不会使元素在垂直方向上居中对齐。要在垂直方向上居中对齐，需要使用其他技巧，例如将元素的position属性设置为absolute，并且将top和bottom属性都设置为0，或者使用Flexbox或Grid布局等。

4. 对于有固定宽度的元素

对于有固定宽度的元素，将margin设置为auto可以使元素左右居中对齐。这是因为当元素的宽度已知时，浏览器会自动计算左右外边距的值，使它们相等，从而实现左右居中对齐。

5. 对于没有固定宽度的元素

对于没有固定宽度的元素，将margin设置为auto不会使元素左右居中对齐。这是因为当元素的宽度未知时，浏览器无法自动计算左右外边距的值，从而无法实现左右居中对齐。要在这种情况下实现居中对齐，需要使用其他技巧，例如使用Flexbox或Grid布局等。

# font-size 和 vertical-align 的隐秘联系

font-size 属性控制文本的字体大小，通常使用像素、点或 em 作为单位来指定。当在行内元素中设置 font-size 属性时，它会影响到该元素中的所有文本的大小，包括任何子元素中的文本。

vertical-align 属性控制行内元素的垂直对齐方式。该属性可接受多种值，包括 top、bottom、middle 等。对于 inline-block 元素和表格元素中的单元格，该属性可以用来控制它们在行内的垂直位置。

当 vertical-align 属性应用于行内元素时，该元素将与行内文本的基线对齐。基线是所有行内文本所处的虚拟线条，其底部对齐行内元素的底部，其顶部对齐行内元素的顶部。

因此，当我们将 vertical-align 属性应用于行内元素时，该元素的垂直位置将受到 font-size 属性的影响。例如，如果将 vertical-align: middle 应用于一个行内元素，而该元素的字体大小为 16px，则该元素将在行内的中心位置垂直居中，与行内文本的基线对齐。

综上所述，font-size 和 vertical-align 之间存在联系，它们共同决定了行内元素在垂直方向上的位置和对齐方式。

# line-height VS vertical-align

`line-height` 和 `vertical-align` 都是用来控制元素在垂直方向上的布局，但它们的作用不同。

- `line-height` 用来设置行高，即文本行与行之间的垂直间距，它是应用于一个元素的文本内容的。当一个元素没有设置高度时，它的高度会根据文本内容和行高自适应，当行高小于字体大小时，文本会出现“溢出”现象。如果设置了 line-height，则元素的高度会随之改变，行高会影响元素内文本的对齐方式。

- `vertical-align` 则用于设置元素内行内元素（如文本、图片等）在垂直方向上的对齐方式。如果元素内没有行内元素，vertical-align 不会起作用。vertical-align 的属性值有多种，如 top、middle、bottom、baseline 等，它们分别代表了不同的垂直对齐方式。如果没有设置 vertical-align，默认为 baseline 对齐方式。

需要注意的是，line-height 和 vertical-align 的作用对象不同，line-height 作用于元素的文本内容，而 vertical-align 作用于元素内的行内元素。在实际的布局中，可以结合使用 line-height 和 vertical-align，来实现对文本和行内元素的精确控制。

# 深入 line-height 的各类属性值

在CSS中，line-height属性用于设置行间距。除了常见的数值型属性值之外，line-height还支持其他类型的属性值，包括：

- 数值型属性值：

数值型属性值用于设置行高，可以是一个具体的像素值或百分比值。例如：line-height: 1.5;表示行高为当前字体大小的1.5倍。

- 百分比属性值：

百分比属性值用于设置行高，相对于当前字体大小的百分比值。例如：line-height: 150%;表示行高为当前字体大小的150%。

- 长度属性值：

长度属性值用于设置行高，可以是一个具体的像素值。例如：line-height: 24px;表示行高为24像素。

- 其他属性值：

除了数值型、百分比和长度属性值之外，line-height还支持其他属性值，包括：

1. normal：使用默认的行高，通常是当前字体大小的1.2倍。
2. inherit：继承父元素的行高属性值。
3. initial：使用默认的行高属性值。

另外，line-height还可以设置为一个无单位的值，如line-height: 1.5em;，此时行高将相对于当前元素的字体大小计算。

需要注意的是，在某些情况下，line-height属性值的不同可能会对页面布局产生影响。例如，当line-height的属性值小于当前字体大小时，可能会导致行高小于字体大小，从而导致文字的重叠或截断。因此，在设置line-height时需要注意其属性值的具体含义和影响。

# BFC/IFC/FFC/DFC 的原理

在CSS中，BFC，IFC，FFC，DFC是指CSS盒模型中的布局上下文，用于控制元素的布局和定位。它们的原理如下：

- BFC (Block Formatting Context):

BFC是一种页面布局方式，可以使一个块级元素的内部子元素在垂直方向上形成一个独立的渲染区域，并且与外部元素相互隔离。这意味着BFC内部的元素不会对外部元素造成影响，从而可以控制元素的布局和定位。BFC的创建方式包括浮动、绝对定位、块级格式化上下文等。

- IFC (Inline Formatting Context):

IFC是一种行内元素的布局方式，可以使一个行内元素的内部子元素在水平方向上形成一个独立的渲染区域。IFC内部的元素按照一定的规则进行排列，可以通过修改行内元素的样式属性来控制元素的布局和定位。

- FFC (Flex Formatting Context):

FFC是一种基于Flexbox的布局方式，可以使一个元素的内部子元素在水平和垂直方向上形成一个独立的渲染区域。FFC内部的元素按照Flexbox规则进行排列，可以通过修改Flexbox属性来控制元素的布局和定位。

- DFC (Grid Formatting Context):

DFC是一种基于Grid的布局方式，可以使一个元素的内部子元素在水平和垂直方向上形成一个独立的渲染区域。DFC内部的元素按照Grid规则进行排列，可以通过修改Grid属性来控制元素的布局和定位。
