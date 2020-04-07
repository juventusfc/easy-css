# @rule

## @charset

提示浏览器或其他应用该 CSS 文件的编码方式

## @import

引入另一个 css 文件。

```css
@import [ <url> | <string> ] [ supports(
    [ <supports-condition> | <declaration> ]
  ) ]? <media-query-list>?;

// first.css
@import "second.css";
```

当 HTML 中引入 first.css 后，会先发起对 first.css 的请求，之后发起对 second.css 的请求。而不是一开始两个 css 文件会自动合并。;

## @media

对设备类型进行判断，从而应用不同的 CSS。media 区块内，是普通规则。[具体应用可参考](http://jsfiddle.net/DrSRT/)

```css
@media print {
  body {
    font-size: 10pt;
  }
}

@media screen and (min-width: 761px) {
  body {
    background-color: white;
  }
}
```

## @page

分页媒体(如打印机)访问页面时的表现设置。

```css
@page {
  margin-top: 800px;
  margin-bottom: 8em;
}
```

## @counter-style

产生一种数据，用于定义列表项的表现。注意，只有少部分浏览器实现了这个功能。其他浏览器只能用已经定义好的 list-style。

```html
<style>
  @counter-style thumbs {
    system: cyclic;
    symbols: "\1F44D";
    suffix: " ";
  }
  ul {
    list-style: thumbs;
  }
</style>
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Coca Cola</li>
</ul>
```

## @keyframes

产生一种数据，用于定义动画关键帧。下面的代码，Forza Juventus!!这些文本会从屏幕右边移动到屏幕左边。

```html
<style>
  p {
    animation-duration: 3s;
    animation-name: slidein;
  }

  @keyframes slidein {
    from {
      margin-left: 100%;
      width: 300%;
    }

    to {
      margin-left: 0%;
      width: 100%;
    }
  }
</style>
<p>Forza Juventus!!</p>
```

## @fontface

fontface 用于定义一种字体，icon font 技术就是利用这个特性来实现的。

```html
<html>
  <head>
    <title>Web Font Sample</title>
    <style type="text/css" media="screen, print">
      @font-face {
        font-family: "Bitstream Vera Serif Bold";
        src: url("https://mdn.mozillademos.org/files/2468/VeraSeBd.ttf");
        font-family: "Dokdo", cursive;
      }

      body {
        font-family: "Bitstream Vera Serif Bold", serif;
      }
    </style>
  </head>
  <body>
    This is Bitstream Vera Serif Bold.
  </body>
</html>
```

注意，由于 mdn 网站的设置，上面的代码会遇到跨域问题，会导致 Bitstream Vera Serif Bold 字体不能下载。

### 网页上设置字体的方法

网页上设置字体的方法有两种

```html
<!-- 方法1： 使用 Google Fonts 等直接加载 -->
<html>
  <head>
    <title>Web Font Sample</title>
    <link
      href="https://fonts.googleapis.com/css?family=Dokdo"
      rel="stylesheet"
    />
    <style type="text/css" media="screen, print">
      body {
        font-family: "Dokdo", serif;
      }
    </style>
  </head>
  <body>
    This is Bitstream Vera Serif Bold.
  </body>
</html>
```

```html
<!-- 方法2： 使用 @font-face 加载 -->
<html>
  <head>
    <title>Web Font Sample</title>
    <style type="text/css" media="screen, print">
      @font-face {
        font-family: "Dokdo";
        font-style: normal;
        font-weight: 400;
        src: local("Dokdo Regular"), local("Dokdo-Regular"),
          url(https://fonts.gstatic.com/s/dokdo/v5/esDf315XNuCBLxLtiPaOtdRpYPXHdpW00KL0ZuekhgFC8gZJqn5HNGTt9CSypPToQl4.119.woff2)
            format("woff2");
        unicode-range: U+20-22, U+27-2a, U+2c-38, U+3a-3b, U+3f, U+41-47,
          U+4a-4c, U+4f-5d, U+61-7b, U+7d, U+a1, U+ab, U+ae, U+b7, U+bb, U+bf,
          U+2013-2014, U+201c-201d, U+2122, U+ac00, U+ace0, U+ae30, U+b2e4,
          U+b85c, U+b9ac, U+c0ac, U+c2a4, U+c2dc, U+c774, U+c778, U+c9c0, U+d558;
      }
      body {
        font-family: "Dokdo", serif;
      }
    </style>
  </head>
  <body>
    This is Bitstream Vera Serif Bold.
  </body>
</html>
```

## @supports

检查环境特性,与 media 类似。

```html
<html>
  <head>
    <title>Sample</title>
    <style type="text/css">
      * {
        box-sizing: border-box;
        font-family: Arial, sans-serif;
      }

      .container {
        max-width: 80%;
        height: auto;
        background-color: #084f66;
        margin: 0 auto;
        padding: 0;
      }

      .artwork {
        margin: 0;
        padding: 0;
        background: linear-gradient(rgb(12, 185, 242), rgb(6, 49, 64));
      }

      img {
        display: block;
        width: 100%;
        height: auto;
      }

      /* If the browser supports blending, this rule set will be applied */
      @supports (mix-blend-mode: overlay) {
        .artwork img {
          mix-blend-mode: overlay;
        }
      }

      /* If the browser doesn't support blending, the rule set below will be applied */
      @supports not (mix-blend-mode: overlay) {
        .artwork img {
          opacity: 0.5;
        }
      }
    </style>
  </head>
  <body>
    <div class="container">
      <article class="artwork">
        <img
          src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/123941/artwork.jpg"
          alt="artwork"
        />
      </article>
    </div>
  </body>
</html>
```

上面代码在各个浏览器的表现：

- Chrome: 支持@supports, 支持 mix-blend-mode: overlay
- Edge: 支持@supports,不支持 mix-blend-mode: overlay
- IE: 不支持@supports

## @namespace

用于跟 XML 命名空间配合的一个规则，表示内部的 CSS 选择器全都带上特定命名空间。

## @viewport

用于设置视口的一些特性，不过兼容性目前不是很好，多数时候被 html 中的 `<meta name="viewport" content="width=device-width, initial-scale=1.0" />` 代替。
