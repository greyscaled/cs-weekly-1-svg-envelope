[![forthebadge](https://forthebadge.com/images/badges/fuck-it-ship-it.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/made-with-vue.svg)](https://forthebadge.com)

# SVG Envelope :envelope:
A simple SVG envelope with open and close animations wrapped in a `Vue` application.

[VIEW THE DEMO](https://vapurrmaid.github.io/cs-weekly-1-svg-envelope/)

## About
This is the first of a declared ~weekly effort called [Code Something Weekly](https://medium.com/@vapurrmaid/code-something-weekly-how-and-why-44640d279ca1).

I've never coded an SVG by hand before and came up with this small project as a first exercise.

The original ideas can be found on codepen, where they exist as **vanilla** projects without `Vue` etc.

- [envelope](https://codepen.io/vapurrmaid/pen/QBdxdR)
- [paper](https://codepen.io/vapurrmaid/pen/XBMJyv)


## Short Writeup
Most of the application's logic exists in `Envelope.vue` (a wrapper for Envelope svg) and `Paper.vue` (a wrapper for Paper svg). The rest is mostly `Vue` boiler plate, bootstrapped with `vue create`.

### SVGs, Scaling
If you take a look at `Envelope.vue`, you see:

```html
<svg
      class="svg-envelope"
      id="envelope"
      preserveAspectRatio="xMidYMid meet"
      height="400"
      width="400"
      viewbox="0 0 400 400"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:svg="http://www.w3.org/2000/svg">
```

`viewbox` and `preserveAspectRatio` are the attributes that allow the magic of SVG scaling to occur.

There's a helpful Stack Overflow thread [here](https://stackoverflow.com/questions/19484707/how-can-i-make-an-svg-scale-with-its-parent-container) and an insightful article [here](https://css-tricks.com/scale-svg/).

 - Imagine `viewbox` as a telescope. `viewbox` takes 4 arguments: `min-x`, `min-y`, `width`, `height`. The first two pan the telescope while the latter two zoom.

- `preserveAspectRatio` defines how to scale relative to `viewbox`. Thus it is a meaningless attribute without `viewbox`. There are many ways to scale as discussed on [mdn](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/preserveAspectRatio). `xMidYMid meet` is the default uniform scaling.

### Simple Shapes
Rectangles are fairly straightforward. Let's take a look at an example:

```html
<rect
  class="svg-envelope__bg"
  fill="rgba(255, 202, 40, .5)"
  height="100%"
  width="100%"
  rx="20"
  ry="20"
  x="0"
  y="0"/>
```

`fill`, `height` and `width` are fairly straight forward. `rx` and `ry` define the corner radius. `x` and `y` are the position relative to the `viewbox` coordinates (0,0 is upper left).

Circles are just as straightforward:
```html
<!-- Seal -->
<circle
  :class="{
    openSeal: open,
    closeSeal: isClosing
  }"
  @click.stop.prevent="sealClick"
  id="seal"
  cx="200"
  cy="200"
  r="40"
  stroke="transparent"
  fill="rgba(255, 79, 79, .8)"/>
```
**note:** `:class` and `@click` are specific to `Vue`.

Here `cx` and `cy` define the x,y coordinates of the center. `r` is the radius.

### Paths
Paths accept a string, `d` which defines the shape.

> **Note**: Commands are case-sensitive; an upper-case command specifies its arguments as absolute positions, while a lower-case command specified points relative to the current position.

```html
<!-- triangle/envelope -->
<path
  :class="{
    openLid: open,
    closeLid: isClosing
  }"
  id="triangle"
  d="M20 0 L 200 200 L 380 0 L 20 0"
  fill="rgba(255, 202, 40, .5)"
  stroke="transparent"/>
```

- M stands for move. Thus `M20 0` says move to coordinates x, y:(20, 0)
- L stands for line to. It draws a straight line from wherever you currently are to the coordinates supplied. In triangle above, `"L 200 200"` draws a straight line from (20, 0) to (200, 200).

- C (not shown here) is for Bezier curve. It takes 3 coordinates sets:
  - (x1, y1), (x2, y2), (x, y)
  - (x1, y1) and (x2, y2) are relative to the beginning and end point respectively. They're used to shape the curve slope. The final set of coordinates is where to draw the curve to.

See the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/d) on everything about the `d` string. (**aye carumba, I just said "the d"**).


### Groups and Render Order
It's helpful to group various parts of the svg together as a group (`<g></g>`) so that classes or animations can be applied to every child in the group.

There's no concept of `z-index` in SVG. Instead, the hierarchy is inferred from the order. Thus, you have to be cognizant of the order in which you write each part. Start from the background and work your way up (out of the page).


### Animations
SVG can be very easily animated from CSS. As this is a toy project, I didn't pull in any outside animation libraries. I decided to tinker around and write my own.

Let's take a look at the envelope "lid" (the triangle).

```html
<path
  :class="{
    openLid: open,
    closeLid: isClosing
  }"
  .../>
```

The `:class` syntax is understood as follows:
- the class `openLid` is only present when component state `open = true`
- the class `closeLid` is only present when component state `isClosing = true`

These classes are used to just invoke animations (`@keyframes`). Note that `forwards` used in `.openLid` means that the final state of the animation will persist. 

```css
/* lid/triangle animation classes */
.closeLid {
  animation: revRotX .5s ease-in;
}

.openLid {
  animation: rotX .5s ease-in forwards;
}

@keyframes revRotX {
  0% { transform: rotateX(180deg); }
  100% { transform: rotateX(0deg); }
}

@keyframes rotX {
  0% { transform: rotateX(0deg); }
  100% { transform: rotateX(180deg); }
}
```



## Issues, PRs
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
Feel free submit a PR or raise any issues. 
