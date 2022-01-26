# css course

## basics

### what is css

cascade style sheet

### selectors

`h1, h2 {}` --> both elements
`ul li {}` --> li child of ul

- top to bottom

`ul li {}` --> higher precedence because more specific
`li {}`

`.container {}` --> class selector
`#first-item {}` --> for ids

- precedence: id > class > specific selector > general selector

`input[type="email"] {}` --> select `<input type="email"></input>`


### combinators

`section p` --> descentant combinator
`section > p` --> immediate child combinator
`section + p` --> ADIACENT SIBLING select first immediately following sibling
`section ~ p` --> GENERAL SIBLING - select all following sibling

focus: `h2 + p` --> paragraph placed exactly after heading2


### colors

- name
- rgb(a)
- hex

Recommendations: 
- don't use red
- green is resful
- blue relaxes 
- choose right dominant color and color shcme
- find right background color


### text-formatting 1

`p` default size is 16px

`text-align` defaults to left
`display: block` full width

`display: inline` it takes only width required

`text-align` properties DO NOT work for `inline` elements!!

To handle this problem use a `div` outside the `p`


### text-formatting 2

[ GENERIC | FONT ] 
1. Serif | Times New Roman, Georgia, etc.
2. Sans-Serif | Helvetica, Verdana, etc.
3. Cursive | Brush Script, Mistral, etc.
4. Monospace | Courier New, Lucida Bright, etc.
5. Fantasy | ...

`font-family: Test, Helvetica, sans-serif` --> Use 'Test', fallback to 'Helvetica', fallback to 'sans-serif'

You can also use Google Fonts: 
1. copying the link in the `head`
2. copying the `@import` string in our css

`font-style: italic` --> or `normal` etc.

### box-model

Margin / Border / Padding / Content

[Default style for HTML elements](https://www.w3schools.com/cssref/css_default_values.asp)

```
html {
  display: block;
}

body {
  display: block;
  margin: 8px;
}
```

`body { margin: 0; }` --> convenient method

`border: 5px #f00 solid` --> to use all three properties
`padding: 3px 4px 3px 2px` --> [top, right, bottom, left]
`padding: 10px 20px` --> [top&bottom, right&left]
`padding: 40px` --> all

`margin` --> works like padding syntactically

`box-sizing` --> 'content' is default, only content used to compute width and height, 'border' otherwise


### pseudo classes and elements

1. Pseudo Classes define special state of an element: `a:hover`
2. Pseudo Elements define style for specific parts of element: `h1::after`

#### pseudo classes

`a:link` --> normal state of 'a', before being visited
`a:visited` --> after being visited [some styles are restricted]
`a:hover` --> when hovering
`a:active` --> while being clicked

Use them in this order!

With bullet list `ul` use `list-style: none;` to get rid of bullet

`ul li:first-child` --> first child
`ul li:last-child` --> last child
`ul li:nth-child(2)`  --> nth child [not zero based like array]

#### pseudo elements

`h1::first-letter` --> awesome first letter modifier

`h1::before` --> modify before the element
`h1::before { content: "This is"; }` --> insert content before 

`h1::after { content: ", ok?"; }` --> insert content after element 


### measurement units

Absolute units:
- *Pixel (px)*
- Centimeter (cm)
- Millimeter (mm)
- Inch (in)
- Points (pt)
- Pica (pc)

Realtive Units:
- em --> 1em === closing element font-size (`html` has 16px)
- rem --> 1em === root element font-size (`html` always)
- vw
- vh
- % --> size with respect to the *closest parent element*


### positions

- Static
  - by default, not effected from top, left, etc.
  
- Relative: 
  - can be changed with top, left, etc
  - follows normal flow

- Absolute
  - positioned relative to the closest position parent element
  - need to put specify position -not static- to parent
  - jumps out from normal flow
  - `width` and `height`, if not defined, limit to content

To use `z-index` the position needs to be set as relative or absolute

- Fixed
  - relative to the viewport

- Sticky (new)
  - according to user scroll position
  - set `top: 0` to keep it on top of viewport
  - relative to its parent!


### overflow

Property for block level element on height property
- visible (default)
- hidden
- auto --> creates scrollbar in case of overflow
- scroll --> *always* creates scrollbar

- overflow-x
- overflow-y

### floats

floats are becoming less popular, because of flex and grid

a float element jumps out on the normal flow of page
to adjust it, in the container:
`.clearfix::after { content: ''; display:block; clear: both }`


## advanced CSS

### background 1

`background-image: url('img/image.jpg')` --> image is used as background

```
div {
  background-image: url('img/image.jpg');
  background-size: 200px;
  background-repeat: repeat-x;
}
```

default behaviour: start from top-left
`background-position: 50px 40px` --> change the 'start' of the image placement

`background-position: right 50px bottom 20px;` --> move from right/bottom

`background-position: 50% 50%` --> image is centered
`background-position: center` --> image is centered (same result)

`background-attachment: fixed` --> fixed wrt viewport

### background 2

`background-size: 300px 150px;` --> width and height, image is stretched
`background-size: 300px auto;` --> browser automatically fit to img size

`background-size: cover;` --> part of image can be clipped

`background-size: contain;` --> image is contained

`background-origin: padding-box;` --> default, invades padding 
other values are content-box or border-box

`background-clip: border-box;` --> default, starts display from border box
other values are content-box or padding-box

In short (cover needs the backslash):
`background: green url('img/image.jpg') no-repeat center fixed /cover`

multiple images
`background: url('img/image.jpg') no-repeat center fixed /cover, url('img/image.jpg') no-repeat center fixed /cover`


### gradients

`background-image: linear-gradient(yellow, blue);` 

`background-image: linear-gradient(to right, yellow, blue);` --> left2right
`to bottom` --> top2bottom
`to left bottom` --> from top-right corner to bottom left-corner

`background-image: linear-gradient(to right, blue, yellow, blue);` --> left2right

some tricks
`background: linear-gradient(rgba(255, 0, 0, 0.9), rgba(255, 0, 0, 0.2)), url('img/image.jpg') no-repeat center /cover;`


### shadows

`text-shadow: 50px 20px;` --> 50px w, 20px h

`text-shadow: 10px 20px 10px green;` --> 50px w, 20px h, 10px blurriness, color

`box-shadow: 5px 5px 10px #999;`


### transitions

1. transition-property *
2. transition-duration *
3. transition-delay (opt.)
4. transition-timing-function (opt.)

```
transition-property: width;
transition-duration: 1s;
```

on element not in hover state

`transition-timing-function` --> ease, ease-in, linear, etc

`transition: width 1s 0s ease` --> property, duration, delay, function

`transition: width 1s ease, baground-color 2s` --> no need for delay or function

`transition: all 1s` --> all properties

### transforms

`transform: translateX(200px)` --> move element on x direction
`transform: translate(100px, 200px)` --> move element on both direction

- rotate 
- scale (scaleX, scaleY)

- skew (skewX, skewY)

- rotateX, rotateY
- rotateZ


### animations

we must create keyframes

```
@keyframes my-animation {
  0% {
    left: 0;
    top: 0;
    background-color: orangered;
  }
  100% {
    left: 500px;
    top: 0;
    backround-color: green;
  }
}
```

and assign them to an object 

```
.box {
  animation-name: my-animation;
  animation-duration: 4s;
}
```

`animation-delay` --> like in tranisition
`animation-iteration-count` --> default 1, times the animation will run (infinity too)

`animation-direction` --> default 'normal', 'reverse', 'alternate'

`animation-timing-function` --> like in transition

`animation-fill-mode` --> how animation behaves when the animation ends
- 'forwards' --> stay where it finishes
- 'backwards

`animation: my-animation 2s ease-in 2s infinite alternate forwards` 


## flexbox

### what is flexbox

popular, easy, flexible
used to manage alignemt, direction and order in container

- flex container
- flex items

* main axes
* cross axes

- in container:
  1. `display: flex`
  2. `flex-direction: row`
  3. `flex-wrap: nowrap`

  4. `justify-content: flex-start`
  5. `align-items: stretch`
  6. `align-content: stretch`

- in items
  1. `order: 0`
  2. `align-self: auto`
  3. `flex-grow: 0`
  4. `flex-basis: auto`
  5. `flex-shrink: 1`


### flex container

display:
- flex --> display as a flex block
- inline-flex --> try to be inline without taking all width

flex-direction:
- row (and reverse)
- column (and reverse)

flex-wrap:
- no-wrap --> defaults
- wrap --> goes 'down'

short: `flex-flow: row wrap`

justify-content [along main axis]:
- flex-start --> defaults
- ...
- center
- space-between
- space-around --> adds padding at edges
- space-evenly --> spaces on edges equal to space inside

`justify-content` may not work in case of column, because flex takes as much space as needed, not more -if not specified-

align-items [along cross axis]:
- stretch (default)
- flex-start
- ...
- baseline --> of text inside

align-content [manage position *in case of wrap*]:
- stretch (default)
- center
- flex-start
- flex-end
- ...

### flex items

order [change position of items]
- 1 
- -1

align-self [change align-items for specific item]:
- auto
- stretch
- ...

flex-grow
- 0 --> default
- 1 --> size on growing
- 5 --> 5 times faster grow than 1

flex-shrink [opposite of flex-grow; on container nowrap]
- 1 --> default
- 0 --> item will not shrink
- ...

flex-basis [overwrite the width -row- or height -column-]
- auto
- 100px
- ...

short: `flex: 0 1 auto` --> flex-grow, flex-shrink, flex-basis


## responsive websites

`@media (max-width: 1200px) {}` ---> apply up to width 1200px


## CSS grid

### introduction

- CSS flexbox ---> 1-dimension
- CSS Grid ---> 2-dimension

1. Grid (Container)
2. Grid Items

- Grid lines: 1 more line than column/row

- Grid gutter (gap)


### how to create

`display: grid` --> in container

`grid-template-rows: 150px 150px;` --> row height 
`grid-template-columns: 120px 120px 120px;` --> column width

`grid-row-gap: 20px` 
`grid-column-gap: 20px` 

or `grid-gap: 20px (20px)` --> single line for gap

### fractional units

`grid-template-columns: 120px 120px auto;` --> the 'auto' column may grow

`grid-template-columns: 120px 120px 1fr;` --> 1fr is 'fraction' space
`grid-template-columns: 1fr 2fr 1fr;`

`grid-template-columns: repeat(3, 1fr)` --> shortcut all equal

`grid-template-columns: 50% repeat(2, 1fr)` --> shortcut half and rest
`grid-template-columns: 2fr repeat(2, 1fr)` --> shortcut 2|1|1


### positioning

in items:

`grid-column-start: 3` --> should start on column line 3
`grid-column-end: 4` --> should end on column 4
`grid-row-start: 2`
`grid-row-end: 3`

shortcut:
`grid-column: 2 / 3;` --> 2 is start, 3 is end
`grid-row: 2 / 3;`

short shortcut:
`grid-area: 2 / 2 / 3 / 3` --> line-0, column-0, line-1, column-1

if a cell is behind another we can use `z-index` WITHOUT the position-relative

`grid-column: 2 / -1;` --> 2 is start, -1 stands for 'the end' of grid

`grid-column: 1 / span 3` --> how many cells/fraction a cell will extend to


### naming grid items

`grid-template-rows: 1fr 1fr 1fr 1fr`

in container
`grid-template-rows: [header-start] 1fr [header-end main-start] 1fr 1fr [main-end box-start] 1fr [box-end footer-start] 1fr [footer-end]` ---> named grid

in header
`grid-row: header-start / header-end`

in container
`grid-template-columns: repeat(4, [col-start] 1fr [col-end])`


### naming grid areas

in container:
```
grid-template-areas:
        "header header header header"
        "sidebar main main main"
        "sidebar main main main"
        "sidebar box-1 box-2 box-3"
        "footer footer footer footer";
```

for empty cell use '.' (dot)

in items:
`grid-area: header;` ---> occupy all header


### implicit and explicit grids

implicit grid (in console developer dashed/solid lines)
`grid-auto-rows: 150px` --> set height of implicit rows

`grid-flow: column` --> from row to column implicit direction
`grid-auto-columns: 130px`

try to avoid them :)


### align grid items

how to place elements HORIZONTALLY
`justify-items: stretch` ---> default
- center
- start / end

how to place elements VERTICALLY
`align-items: stretch` ---> default
- center
- start / end

in items:
`justify-self` ---> individual HORIZONTAL alignment
`align-self` ---> individual VERTICAL alignment

to expand item across multiple cells use, f.i:
`grid-row: 2 / 4`
`grid-column: 1 / -1` 


### aligning grid tracks

moves all the trace
`justify-content: start` ---> default
- center, end
- space-between, space-around, space-evenly

(attention, because in flexbox it works slightly differently)
`align-content: start` ---> default
- center, end
- space-between, space-around, space-evenly


### min-content, max-content, minmax

`grid-template-columns: max-content 1fr 1fr`
make the first column large as the MAX width of the cells in the columns

`min-content`
wrap text in large cells, using min width as possible (without overflow)

`minmax(140px, 300px)` ---> avoid stretch and shrink over bounds


### auto-fill, auto-fit

`grid-template-columns: repeat(auto-fill, 80px)` ---> creates columns on the right if space if available

wrap in case of need, useful with responsive layouts

`grid-template-columns: repeat(auto-fit, 80px)` ---> creates the columns that could exist anyway, but with 0 width

`grid-template-columns: repeat(auto-fit, minmax(80px, 1fr))`



## furniture store

`repeat(auto-fit, minmax(5rem, 1fr));` in navigation bar

`display: inline-block;` ---> we can define width for inline-block


element to create underline effect
```
.first-nav-link::after {
  content: "";
  display: block;
  height: 0.1rem;
  background-color: #12376e;
}
```

`cubic-bezier(0.55, 0, 0.98, 0.54);` ---> slow to fast

`display: block` ---> to apply margin and padding

`visibility: hidden;`

centering
```
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

`width: 100%` on inline elements if they are positioned absolute


```
.slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

`border-radius: 50%;` ---> circle


button hover effect
`box-shadow: 0.2rem 0.2rem 1rem #777;`
`box-shadow: 0.2rem 0.2rem 2rem #777;`

`box-shadow: 0 1.5rem 6rem rgba(0, 0, 0, 0.3);` ---> nice card 

`<input type="text">` next to `<input type="submit">` ---> display flex on container

`<input type="checkbox" id="show-hide-forms">` ---> checkbox
`<label for="show-hide-forms" class="x-btn">&#10005;</label>` ---> on click, checkbox changes

`<input type="checkbox" id="show-hide-forms" hidden>` ---> the hidden trick