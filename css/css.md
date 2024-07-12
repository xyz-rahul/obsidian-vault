# CSS
[CSS-Tricks - Tips, Tricks, and Techniques on using Cascading Style Sheets.](https://css-tricks.com/)
## Display
### Display Properties

- **inline-block**: Behaves like an inline element but each child is treated as block
	- takes content space + left + right + top + bottom apply on each child 

- **inline**: takes content space; top + bottom changes does not apply 
- **block**: takes full space on main axis (from left to right); left + right + top + bottom apply
- **inline-block**: Content space with block-like styling for children.
- **Grid**: 2D layout

### Flexbox
![[Pasted image 20240607192939.png]]

flex-direction
### Flexbox Properties

`flex-direction: row | column` direction of the main axis

**justify-content** align items perpendicular to main axis
`justify-content: center | start | end | space-around | space-between | space-evenly | order | flex-start | flex-end | strech ` direction of the main axis

**align-items** align items perpendicular to cross axis
**align-content**: for multi-line
`align-items: strech | center | start | end `
[align-items - CSS: Cascading Style Sheets | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)

- **flex-wrap**: Controls whether items wrap onto multiple lines.
- **flex-grow**: rate to grow flex items.
- **flex-shrink**: rate to shrink flex items. 
- **flex-basis**: Defines the default size of an element before the remaining space is distributed.

- **order**: Sets the order in which a flex item appears in the flex container.

- **align-self**: Allows the default alignment to be overridden for individual flex items.

## Sizing Units
**absolute**
in: inches (1in = 96px)
px: pixels (1px= 1/96th of 1in) 

**relative**
rem: relative to root font
em: relative to current font 
vw: viewport width
vh: viewport height
%: height, width of parent

## Positioning
**relative**: normal workflow + left, right, top, bottom from current pos
**static**: normal workflow + ~~left, right, top, bottom~~ not apply
**sticky**: normal workflow + then offset relative to its _nearest scrolling ancestor_ and _containing block_
**fixed**: ~~normal workflow~~ not apply + viewport
**absolute**: ~~normal workflow~~ not apply + parent relative container 

## Float and Clear 
usually to set paragraph and image

- **float**: Element floats to the left or right of its container.
- **clear**: Specifies what elements can float beside the cleared element and its content.

## Border Properties

- **border-style**
- **border-width**
- **border-color**
- **border**: Shorthand 
## CSS Box Model

- **box-sizing**: Defines how the width and height of an element are calculated.
`box-sizing: content-box| border-box`
## Responsive Design Breakpoints used by Tailwind

- **sm**: `@media (min-width: 640px) { ... }`
- **md**: `@media (min-width: 768px) { ... }`
- **lg**: `@media (min-width: 1024px) { ... }`
- **xl**: `@media (min-width: 1280px) { ... }`
- **2xl**: `@media (min-width: 1536px) { ... }`

## Box Shadow
`box-shadow: +x-axis | +y-axis | blur-radius | span-radius | color`

to combine two or more shadows
box-shadow: ==x-offset | y-offset | blur-radius | spread-radius | color== , x-offset | y-offset | blur-radius | spread-radius | color  , ==x-offset | y-offset | blur-radius | spread-radius | color==
repeat using ,
## CSS Animations
- `@keyframes`
- `animation-name`
- `animation-duration`
- `animation-delay`
- `animation-iteration-count`
- `animation-direction`
- `animation-timing-function`
- `animation-fill-mode`
- `animation`

```
@keyframes sun-rise {
  from {
    /* pushes the sun down past the viewport */
    transform: translateY(110vh);
  }
  to {
    /* returns the sun to its default position */
    transform: translateY(0);
  }
}
```

- **@keyframes**: Specifies the animation code.
- **animation-name**: Specifies the name of the @keyframes animation.
- **animation-duration**: Specifies how long time an animation should take to complete one cycle.
- **animation-delay**: Specifies a delay for the start of an animation.
- **animation-iteration-count**: Specifies the number of times an animation should be played.
- **animation-direction**: Specifies whether an animation should be played forwards, backwards or in alternate cycles.
- **animation-timing-function**: Specifies the speed curve of the animation.
- **animation-fill-mode**: Specifies a style for the element when the animation is not playing.
- **animation**: A shorthand property for setting all the animation properties.

[animation - CSS: Cascading Style Sheets | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/CSS/animation)

# Transitions
Transitions enable you to define the transition between two states of an element. Different states may be defined using pseudo-classes like :hover or :active or dynamically set using JavaScript.


.target {
  font-size: 14px;
  transition: font-size 4s 1s;
}

.target:hover {
  font-size: 36px;
}

- `transition`
- `transition-delay`
- `transition-duration`
- `transition-property`
- `transition-timing-function`

## Transform
```css
div.a {  transform: rotate(20deg);}  
  
div.b {  transform: skewY(20deg);}  
  
div.c {  transform: scaleY(1.5);}
```

# Pseudo classes and elements
Here are the key points from the current page, focusing on the important terms:


- **Pseudo Classes**: Includes `:visited`, `:hover`, `:active`, `:focus`, `:first-child`, `:last-child`, and `:nth-child()` for styling different states of elements.
- **Pseudo Elements**: Such as `::after`, `::before`, `::first-letter`, `::first-line`, `::marker`, and `::selection` for styling specific parts of elements.

# GRID
- **GRID Layout**: 2D layout 
```
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  grid-auto-rows: minmax(100px, auto);
}
```

`grid-template-rows: repeat(auto-fit, minmax(200px,500px))`
or 
 `grid-auto-rows: minmax(100px, auto);`

[minmax() - CSS: Cascading Style Sheets | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/CSS/minmax)


to span from one col to another (or rows)
```
.one {
  grid-column: 1 / 3;
  grid-row: 1;
}
```



## css combinator
- descendant selector (space)
- child selector (>)
- adjacent sibling selector (+)
- general sibling selector (~)



css specificity
1. Element
2. Class selectors
3. ID Selectors
4. Inline styles
5. !important

## Calculating Specificity

The actual specificity of a group of nested selectors takes some calculating. You can give every **ID selector** (“#whatever”) a value of **100**, every **class selector** (“.whatever”) a value of **10** and every **HTML selector** (“whatever”) a value of **1**. When you add them all up, hey presto, you have a specificity value.

- [`p`](https://htmldog.com/references/html/tags/p/) has a specificity of **1** (1 HTML selector)
- `div p` has a specificity of **2** (2 HTML selectors, 1+1)
- `.tree` has a specificity of **10** (1 class selector)
- `div p.tree` has a specificity of **12** (2 HTML selectors + a class selector, 1+1+10)
- `#baobab` has a specificity of **100** (1 id selector)
- `body #content .alternative p` has a specificity of **112** (HTML selector + id selector + class selector + HTML selector, 1+100+10+1)

So if all of these examples were used, `div p.tree` (with a specificity of 12) would win out over `div p` (with a specificity of 2) and `body #content .alternative p` would win out over all of them, **regardless of the order**.

# inheritance
initial sets to default by css

first initial then browser then user authored css is applied

initial | inherit | unset

The _initial CSS_ keyword applies the initial (or default) value of a property to an element

The **`unset`** CSS keyword resets a property to its inherited value if the property naturally inherits from its parent, and to its [initial value](https://developer.mozilla.org/en-US/docs/Web/CSS/initial_value) if not. In other words, it behaves like the [`inherit`](https://developer.mozilla.org/en-US/docs/Web/CSS/inherit) keyword in the first case, when the property is an [inherited property](https://developer.mozilla.org/en-US/docs/Web/CSS/Inheritance#inherited_properties), and like the [`initial`](https://developer.mozilla.org/en-US/docs/Web/CSS/initial) keyword in the second case, when the property is a [non-inherited property](https://developer.mozilla.org/en-US/docs/Web/CSS/Inheritance#non-inherited_properties).


![[Pasted image 20240613162429.png]]
[Logical Properties  |  web.dev](https://web.dev/learn/css/logical-properties)


# object-fit
[object-fit - CSS: Cascading Style Sheets | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)