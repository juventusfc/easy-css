# Flex 排版

正常流排版并不能解决所有的 CSS 排版问题。有时候，我们并不仅仅需要正常流提供的“改变文字和盒的相对位置，把它放到特定的版面中”这种功能，还需要“改变盒的大小，使得他们的结构保持固定”这种功能。Flex 排版应运而生。

## Flex 的设计

![flex](./images/flex.png)

Flex 排版的核心是 display:flex 和容器内子元素的 flex 属性，它们配合使用。具有 display:flex 的元素我们称为 flex 容器，它的子元素或者盒被称作 flex 项。

flex 项如果有 flex 属性，会根据 flex 方向代替宽 / 高属性，形成“填补剩余尺寸”的特性，这是一种典型的“根据外部容器决定内部尺寸”的思路，也是我们最常用的 Windows 和 Apple 窗口系统的设计思路。

## Flex 的原理

Flex 布局支持横向和纵向，这样我们就需要做一个抽象，我们把 Flex 延伸的方向称为“主轴”，把跟它垂直的方向称为“交叉轴”。这样，flex 项中的 width 和 height 就会称为交叉轴尺寸或者主轴尺寸。

而 Flex 又支持反向排布，这样，我们又需要抽象出交叉轴起点、交叉轴终点、主轴起点、主轴终点，它们可能是 top、left、bottom、right。

Flex 布局中有一种特殊的情况，那就是 flex 容器没有被指定主轴尺寸，这个时候，实际上 Flex 属性完全没有用了，所有 Flex 尺寸都可以被当做 0 来处理，Flex 容器的主轴尺寸等于其它所有 flex 项主轴尺寸之和。

Flex 排版的步骤主要包括：

1. 把 flex 项分行，有 Flex 属性的 flex 项可以暂且认为主轴尺寸为 0，所以，它可以一定放进当前行
2. 计算每个 flex 项主轴尺寸和位置
3. 计算 flex 项的交叉轴尺寸和位置

## Flex 的应用

垂直居中：

```html
<div id="parent">
  <div id="child"></div>
</div>
```

```css
#parent {
  display: flex;
  width: 300px;
  height: 300px;
  outline: solid 1px;
  justify-content: center;
  align-content: center;
  align-items: center;
}
#child {
  width: 100px;
  height: 100px;
  outline: solid 1px;
}
```

两列等高：

```html
<div class="parent">
  <div class="child" style="height:300px;"></div>
  <div class="child"></div>
</div>
<br />
<div class="parent">
  <div class="child"></div>
  <div class="child" style="height:300px;"></div>
</div>
```

```css
.parent {
  display: flex;
  width: 300px;
  justify-content: center;
  align-content: center;
  align-items: stretch;
}
.child {
  width: 100px;
  outline: solid 1px;
}
```

自适应宽：

```html
<div class="parent">
  <div class="child1"></div>
  <div class="child2"></div>
</div>
```

```css
.parent {
  display: flex;
  width: 300px;
  height: 200px;
  background-color: pink;
}
.child1 {
  width: 100px;
  background-color: lightblue;
}
.child2 {
  width: 100px;
  flex: 1;
  outline: solid 1px;
}
```

## Flex 的基本语法

### 容器属性

- flex-direction: 主轴的方向

  ```css
  .box {
    flex-direction: row | row-reverse | column | column-reverse;
  }
  ```

- flex-wrap: 如果一条轴线排不下所有 flex 项，如何换行

  ```css
  .box {
    flex-wrap: nowrap | wrap | wrap-reverse;
  }
  ```

- flex-flow：是 flex-direction 和 flex-wrap 的简写
- justify-content: flex 项在主轴上的对齐方式

  ```css
  .box {
    justify-content: flex-start | flex-end | center | space-between |
      space-around;
  }
  ```

- align-items：flex 项在交叉轴上的对齐方式

  ```css
  .box {
    align-items: flex-start | flex-end | center | baseline | stretch;
  }
  ```

- align-content： flex 项在多根轴线上的对齐方式

  ```css
  .box {
    align-content: flex-start | flex-end | center | space-between | space-around
      | stretch;
  }
  ```

### flex 项的属性

- order：flex 项目的排列顺序，数值越小，越靠前
- flex-grow: flex 项目的放大比例，默认为 0，即如果存在剩余空间，也不放大
- flex-shrink: flex 项目的缩小比例，默认为 1，即如果空间不足，该项目将缩小
- flex-basis:定义了在分配多余空间之前，flex 项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为 auto，即项目的本来大小

  ```css
  .item {
    flex-basis: <length> | auto;
  }
  ```

- flex: flex 属性是 flex-grow, flex-shrink 和 flex-basis 的简写，默认值为 0 1 auto
- align-self: 允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch

  ```css
  .item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
  }
  ```
