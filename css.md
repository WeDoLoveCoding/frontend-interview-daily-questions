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

# line-height VS vertical-align

`line-height` 和 `vertical-align` 都是用来控制元素在垂直方向上的布局，但它们的作用不同。

- `line-height` 用来设置行高，即文本行与行之间的垂直间距，它是应用于一个元素的文本内容的。当一个元素没有设置高度时，它的高度会根据文本内容和行高自适应，当行高小于字体大小时，文本会出现“溢出”现象。如果设置了 line-height，则元素的高度会随之改变，行高会影响元素内文本的对齐方式。

- `vertical-align` 则用于设置元素内行内元素（如文本、图片等）在垂直方向上的对齐方式。如果元素内没有行内元素，vertical-align 不会起作用。vertical-align 的属性值有多种，如 top、middle、bottom、baseline 等，它们分别代表了不同的垂直对齐方式。如果没有设置 vertical-align，默认为 baseline 对齐方式。

需要注意的是，line-height 和 vertical-align 的作用对象不同，line-height 作用于元素的文本内容，而 vertical-align 作用于元素内的行内元素。在实际的布局中，可以结合使用 line-height 和 vertical-align，来实现对文本和行内元素的精确控制。
