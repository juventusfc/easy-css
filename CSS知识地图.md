## 颜色

在 CSS 中，表示颜色可以用如下方法：

- 颜色名

  在 CSS 中可以直接使用颜色名来设置各种颜色。比如：red、orange、yellow、blue、green ......但是在 css 中直接使用颜色名是非常的不方便。

- RGB

  - RGB 通过三种颜色的不同浓度来调配出不同的颜色
  - R red，G green ，B blue
  - 每一种颜色的范围在 0 - 255 (0% - 100%) 之间
  - 语法：`RGB(红色数字,绿色数字,蓝色数字)`

- RGBA:

  - 就是在 RGB 的基础上增加了一个 A， 表示不透明度
  - 需要四个值，前三个和 RGB 一样，第四个表示不透明度。1 表示完全不透明，0 表示完全透明，.5 表示半透明。

- 十六进制的 RGB

  - 语法：`#红色绿色蓝色`
  - 颜色浓度通过 `00` - `ff`
  - 如果颜色两位两位重复可以进行简写

    `#aabbcc` --> `#abc`

- HSL 或 HSLA

  H 表示色相(0 - 360)，S 表示饱和度，颜色的浓度 0% - 100%，L 表示亮度，颜色的亮度 0% - 100%。语法为：`HSL(色相值,饱和度值,亮度值)`。

## 字体

字体相关的样式：

- `color` 用来设置字体颜色
- `font-size` 字体的大小
- `font-family` 字体族（字体的格式）。可选值：

  - `serif` 衬线字体族
  - `sans-serif` 非衬线字体族
  - `monospace` 等宽字体族
  - `某种特定的字体`

  指定字体的类别后，运行浏览器的电脑上如果有这种字体，就会自动使用该类别下的字体。`font-family` 可以同时指定多个字体，多个字体间使用 `,` 隔开。字体生效时优先使用第一个，第一个无法使用则使用第二个，以此类推。

- `font-face` 可以将服务器中的字体直接提供给用户去使用。

  ```css
  @font-face {
    font-family: "my-font";
    src: url("./font/ZCOOLKuaiLe-Regular.ttf") format("truetype");
  }

  font-family: myfont;
  ```

  使用 `font-face` 存在的问题：

  - 加载速度：由于要从服务器下载，如果网速慢，会发现字体会有一个变化过程。
  - 版权：很多字体是收费的。由于用户是在你的服务器上下载的，所以你的服务器侵犯了字体作者的知识产权。
  - 字体格式：老的浏览器可能识别不了。

## 图标字体

在网页中经常需要使用一些图标，可以通过图片来引入图标，但是图片大小本身比较大，并且非常的不灵活。在使用图标时，我们还可以将图标直接设置为字体，然后通过 `font-face` 的形式来对字体进行引入。这样我们就可以通过使用字体的形式来使用图标。

比较有名的图标字体库是 `fontawesome`。 使用步骤为：

1. [下载](https://fontawesome.com/)
2. 解压
3. 将 css 和 webfonts 移动到项目中
4. 将 all.css 引入到网页中
5. 使用图标字体

   - 直接通过类名来使用图标字体

     ```css
     <i class="fas fa-cat"></i>
     ```

   - 通过伪元素来设置图标字体

     1. 通过 before 或 after 选中要设置图标的元素
     2. 在 content 中设置字体的编码
     3. 设置字体的样式

     ```css
     li::before {
       content: "\f1b0";
       font-family: "Font Awesome 5 Brands";
     }
     ```

   - 通过实体来使用图标字体，语法为 `&#x图标的编码;`。

     ```html
     <span class="fas">&#xf0f3;</span>
     ```

## 行高

行高指的是文字占有的实际高度。通过 `line-height` 来设置行高。行高可以直接指定一个大小（px em），也可以直接为行高设置一个整数， 如果是一个整数的话，行高将会是 `font-size`（字体大小） 的指定的倍数。

字体框就是字体存在的格子，设置 `font-size` 实际上就是在设置字体框的高度，行高会在字体框的上下平均分配。

可以将行高(line-height)设置为和高度(height)一样的值，使单行文字在一个元素中垂直居中。

行高还能用来设置文字的行间距，`行间距 = 行高 - 字体大小`。

## 字体其他

`font-weight` 字重 字体的加粗。可选值：

- `normal` 默认值 不加粗
- `bold` 加粗

`font-style` 字体的风格。可选值有：

- `normal` 正常的
- `italic` 斜体

## 文本的样式

- `text-align` 文本的水平对齐。可选值：

  - `left` 左侧对齐
  - `right` 右对齐
  - `center` 居中对齐
  - `justify` 两端对齐

- `vertical-align` 设置子元素相对于父元素的垂直对齐的方式。可选值：

  - `baseline` 默认值 基线对齐
  - `top` 顶部对齐
  - `bottom` 底部对齐
  - `middle` 居中对齐

- `text-decoration` 设置文本修饰。可选值：

  - `none` 什么都没有
  - `underline` 下划线
  - `line-through` 删除线
  - `overline` 上划线

- `white-space` 设置网页如何处理空白。可选值：

  - `normal` 正常
  - `nowrap` 不换行
  - `pre` 保留空白

## 背景

- `background-color` 设置背景颜色
- `background-image` 设置背景图片

  可以同时设置背景图片和背景颜色，这样背景颜色将会成为图片的背景色。如果背景的图片小于元素，则背景图片会自动在元素中平铺将元素铺满；如果背景的图片大于元素，将会一个部分背景无法完全显示；如果背景图片和元素一样大，则会直接正常显示。

  通过渐变可以设置一些复杂的背景颜色，可以实现从一个颜色向其他颜色过渡的效果。渐变是图片，需要通过 `background-image` 来设置。

  - `linear-gradient` 线性渐变，颜色沿着一条直线发生变化
  - `radial-gradient` 径向渐变(放射性的效果)

- `background-repeat` 用来设置背景的重复方式。可选值：

  - `repeat` 默认值 ， 背景会沿着 x 轴 y 轴双方向重复
  - `repeat-x` 沿着 x 轴方向重复
  - `repeat-y` 沿着 y 轴方向重复
  - `no-repeat` 背景图片不重复

- `background-position` 用来设置背景图片的位置。

  - 通过 top left right bottom center 几个表示方位的词来设置背景图片的位置。使用方位词时必须要同时指定两个值，如果只写一个则第二个默认就是 center。
  - 通过偏移量来指定背景图片的位置：水平方向的偏移量，垂直方向变量。

- 设置背景的范围

  - `background-clip` 可选值：

    - `border-box` 默认值，背景会出现在边框的下边
    - `padding-box` 背景不会出现在边框，只出现在内容区和内边距
    - `content-box` 背景只会出现在内容区

  - `background-origin` 背景图片的偏移量计算的原点
    - `padding-box` 默认值，background-position 从内边距处开始计算
    - `content-box` 背景图片的偏移量从内容区处计算
    - `border-box` 背景图片的变量从边框处开始计算

- `background-size` 设置背景图片的大小。

  - 第一个值表示宽度，第二个值表示高度。如果只写一个，则第二个值默认是 auto
  - cover 图片的比例不变，将元素铺满
  - contain 图片比例不变，将图片在元素中完整显示

- `background-attachment` 背景图片是否跟随元素移动。可选值：

  - `scroll` 默认值 背景图片会跟随元素移动
  - `fixed` 背景会固定在页面中，不会随元素移动

图片属于网页中的外部资源，外部资源都需要浏览器单独发送请求加载，浏览器加载外部资源时是按需加载的，用则加载，不用则不加载。

可以将多个小图片统一保存到一个大图片中，然后通过调整 `background-position` 来显示的图片，这样图片会同时加载到网页中 就可以有效的避免出现闪烁的问题。这个技术在网页中应用十分广泛，被称为 CSS-Sprite，也就是雪碧图。

## 表格样式

- `border-spacing` 指定边框之间的距离
- `border-collapse` 设置边框的合并
