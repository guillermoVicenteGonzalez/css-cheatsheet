# CSS cheatsheet

## Selectors

Selectors are css expressiones we use to target html elements and give them style

## tag selector.

We can target html elements by their tag.

```css
div{
    /*css code*/
}
```

This hovewer will be applied to every div

## class selector

html elements can have one or more classes specified to target them. The class selector in css is preceded by the dot "." character

```html
<div class="miClase"></div>
<style>
    .miClase{
        /*css code*/
    }
</style>
```

## Id selector

Html elements can have an id. They can only have 1 id and it has to be unique, no other element can share it.

```html
<div id="#miId"></div>
<style>
    #miId{
        /*css code*/
    }
</style>
```

## Attribute selector.

We can also target html elements based on the value of their attributes

```html
<input type="text">
<style>
    [type="text"]{
        /*CSS code*/
    }
</style>
```

## Specificity

It measures how specific a css selector is. The more specific a selector is, the more precedence it will have.

Specificity is measured by three numbers in the following format (0,0,0):

- Each tag selector present in a rule will increase the rightmost number by 1.
  
- Each class seelctor present in a rule will increase the middle number by 1
  
- Each id selector present in a rule will increase the leftmost number by 1.
  
- Styles declared inline have precedence over all the previous
  
- the !important keyword outclassses everything
  

```scss
//specificity (0,0,1)
div{}

//specificity (0,1,0)
.container{}

//specificity (1,0,1)
#myId{}
```

The numbers in the specificity index are computed from right to left. This means that a rule with a specificity of (0,0,99) will be overwritten by another one with a specificity of (0,1,0).

- (0,0,99) < (0,1,0)

What this means in general is

- `important > inline > id > class > tag`

## Combination of selectors

Selectors can be combined to obtain more complex and more specific (literally and figuratively) rules.

This rule targets only the containers that are divs and have the id = myId (redudant but whatever)

```scss
div.container#myId{
    /*CSS code*/
}
```

As stated before, the rule is more specific as it narrows the elements target by it, this also is translated to the "technical" specificity, this selector has a specificity of (1,1,1)

We can be as creative as we want, for example, if we have this rule

```scss
//(0,1,1)
p.paragraph{
    color:blue;
}
```

And want it overwritten without using id or adding classes to the html, we could create the following rule

```scss
// (0,3,0)
.paragraph.paragraph.paragrahp{
    color:red;
}
```

## Combinators

Special selectors that target elements based on their relationships between them. They are used next to a normal selector There are four

- ` `: "space". The descendant selectors. Acts upon every descendant of a class
  
- `>`: Child selector. Acts upon the direct children of an element (not grandchildren)
  
- `+`: Adjacent sibling. Acts upon siblings that are right next to the element
  
- `~` : General sibling: Acts upon every sibling of an element
  

### Examples

Selects the direct children (in this case child) with the class child of the container element

```html
<div class="container">
    <span class="child"></span>
</div>

<style>

.container > .child{

}
</style>
```

Selects every **descendant** with a class of `child` inside the `container` element (or elements).

```html
<div class="container">
    <div class="child">
        <div class="child"></div>
        <div class="child"></div>
    </div>
</div>

<style>

.container  .child{

}
</style>
```

Selects every sibling of the container element, eg every element at the same level

```html
<div class="container"> 
</div> 
<div id="sibling-1"></div>
<div id="sibling-2"></div>
<div id="sibling-3"></div>
<style> 
.container ~ div{ 
}
</style>
```

Selects **Only** The first sibling

```html
<div class="container"> 
</div> 
<div id="sibling-1"></div>
<div id="sibling-2"></div> <!--Not selected-->
<div id="sibling-3"></div> <!--Not selected-->
<style> 
.container + div{ 
}
</style>
```

## Pseudo classses

Most of them (the most common) target elements when they are in a special state, for example when the cursor is on top of the element (hover).

They are used by writing : right next to the selector we want to apply it it, for example, `.button:hover`

```html
<button class="btn"></button>
<style>
    .btn{
        background-color:red;
    }

    .btn:hover{
        background-color:blue;
        transform:scale(1.5);
    }
</style>
```

### Other pseudo classes ?

There are other pseudo classes that act as logical operators or as more specific rules. There are too many to cover in this cheatseet but some of them are.

- `:not(parameter)` : Selects elements that are not of the rule passed as parameter
  
  ```html
  <div class="container example"> <!--Not selected-->
  <div class="container">
  <input class="container"> <!--Not selected-->
  <style>
  .container:not(.example):not(input){
      /*CSS code*/
  }
  </style>
  ```
  
- `:has(rule)` : Acts upon elements that have a child of the characteristics specified inside the rule parameter.
  
  ```html
  <div class="container"></div> <!--Not selected-->
  <div class="container">
      <p class="article"></p>
  </div>
  
  <style>
      .container:has(.article){
  
      }
  </style>
  ```
  

## Pseudo elements

Target concrete parts of the element they select. They are used by writing two sets of ":" after the rule, for example: `.container::first-letter` targets the first letter of an element with a class of container.

The most common ones are `::after` and `::before` . They create html elements after and before an element. **In order to work they need the `content` property to be specified**

This rule creates an `::after` element right after the container element

```scss
.container::after{
    content:""
    display:block;
    width:400px;
    height:400px;
}
```

### At rules

Css declarations that start with the "@" symbol. Their purposes are varied, the most popular ones are @media, as they are a group of conditional rules that are applied depending on the device's characteristics

#### Viewport media queries.

using at rules, we can change our css depending on the size of the viewport. For that we use max width and min width

- max-width: x -> The rule will be applied for viewport sizes <= x
  
- min-width: x -> The rule will be applied for viewport sizes >= x
  

For example, the container element will be red for viewport size from <= 1250px;

```css
.container{
     background-color:green;   
}

@media (max-width: 1250px){
    .container{
        background-color:red;
    }
}
```

## Box model

Css uses the box model according to which, each element is a box with several different parts

- Content: The core of the box. Where the content is (duh)
  
- padding: space between the content and the border (kinda like an inner margin)
  
- border: The border that encloses the box
  
- margin: space between the border and other elements
  

### Box sizing

By default, the box sizing property of all elements (or almost all) is set to `box-sizing: content-box`.

What this means is that every sizing related property is added separately. In other words, if we create a container with a width and heigth of 200px and add a padding of 20px, the resulting container will have a width and height = 220px;

```scss
//The total size of this box is 220px;
.box-content-container{
  box-sizing:content-box; //by default
  width:200px;
  height:200px;
  background-color:red;
  padding:10px
}
```

However we can use `box-sizing: content-box;` so that if we specify a width of 200px, the whole box will end up taking that size **After** the margin calculations

```scss
//The total size of this box is 200px;
.box-content-container{
  box-sizing:border-box; //by default
  width:200px;
  height:200px;
  background-color:red;
  padding:10px
}
```

## Block, inline and inline-block elements

### Block

By default, most elements (like divs) will have the `display:block;` property. This means that they will behave like blocks that stack on top of each other.

Even if we have 2 blocks with width of 200px and our viewport is 1920px eg, it fits both, as they are blocks, they will be stacked on top of each other.

### inline

Inline elements (such as span or other text tags) will not be stacked on top of each other like blocks. They will just take as much space as they need and leave the rest for other inline elements. The downside is that their size cannot be modified with `width / height`

### Inline-block

The fusion of both. Inline-block elements will not stack on top of each other, they share horizontal space, and can have their sizes altered through css properties

## Flexbox

Flexbox is a layout model that places elements in a container and aligns them or modifies its size according to two axis, the main axis and the cross axis.

Elements will be placed alongisde the main axis, by default this is the horizontal one, so elements will be placed next to each other

To create a flex container we use

```scss
.flex-container{
    display:flex;
}
```

We can align a flexbox's children with justify items and align items.

- `justify-content` : aligns the items in the main axis (by default the horizontal one)
  
- `align-items`: aligns the items according to the cross axis.
  

Justify-content can take the following properties

- `center`: centers the elements
  
- `start`: places the elements at the start of the container
  
- `end`: places the elements at the end of the container
  
- `space-around`: the space between items is the same, but the spacing between the edges of the container and the first and last items is half of the space between adjacent items
  
- `space-between`: items are distributed evenly with the first item being at the edge of the start of the container and the last at the end edge of the container (no space at the edges)
  
- `space-evenly`: The space between adjacent items and the edges is the same
  

### Main axis

By default, the main axis will be the horizontal one, or in other words, the `flex-direction` . To change it we use

```scss
.flex-container{
    flex-direction:row;
}
```

THe possible values are

- `row`: main axis is the horizontal
  
- `row-reverse`: main axis is horizontal + items are placed from right to left
  
- `column`: main axis is the vertical
  
- `column-reverse`: The main axis is the vertical + items are placed from bottom to top
  

### Flex items

Direct children of a flexbox container also have several properties they can use:

- `align-self`: Does the same as algin-items but to a single item
  
- `order`: by default each item has an order of 0. We can give indexes to items to order themselves
  
- `flex`: shorthand property for
  
  - `flex-grow`: defines if an item can grow and how much (0 means nothing)
    
  - `flex-shrink`: defines how much an item can shrink (0 means nothing)
    
  - `flex-basis`: base width / height (depending on main axis)
    

#### Flex grow

The flex grow property is relative to other flex items. If we have 2 items widht flex grows = 1 and 2 respectively, the item with flex grow = 2 will fill the container and the other one will take half that space

```scss
.flex-item-1{
    flex-grow:1; //fills the container
}

.flex-item-2{
    flex-grow:2; //fills half the container
}
```

## Grid

Allows to create grid like structures by specifying a number of rows and columns.

This example creates a grid with 3 columns of 10px, 20px and 50px of width each and 2 rows ow 100px and 200px of height respectively

```css
.grid-container{
    display:grid;
    grid-template-columns:10px, 20px, 50px;
    grid-template-rows: 100px 200px;
}
```

### Terminology

- **Grid tracks** lines that divide the layout. They can be rows or columns
  
- **Grid-cells** The items between grid-tracks
  

It is important to note that a grid with three elements reall has 4 columns (tracks). This is important to later position and span the elements

### Creating grids.

We specify the grid's number of rows and columns with `grid-template columns` and `grid-template-rows` . We can also specify those together with the`grid-template` property

```css
.container{
    display:grid;
    grid-template: 100px 200px / 1fr 1fr;
    /*equivalent to*/
    grid-template-rows: 100px 200px;
    grid-template-columns: 1fr 1fr;
}
```

To avoid repetition we can use the repeat function in css. The following example creates three columns of 10 pixels each

```css
.grid-container{
    display:grid;
    grid-template-columns:repeat(3,10px);
}
```

#### Implicit and explicit grids

The implicit grid is the one we create with the `grid-template-*` properties. If a grid contains more items than cells were defined, those items will become the explicit grid.

To control the explicit grid, eg how new items that don't fit are placed, first we must specify How they will be added, as rows or as columns. This is done with the `grid-auto-flow` property

```scss
.grid-container{
    display:grid;
    grid-auto-flow:row; //the new items will create a new row
    grid-auto-columns: 20px //each new row will take 20px
}
```

### Fractional units

When working with grids, we can use fractional units or `fr` to refer to a fraction of the grid container. They offer an advantage over percentage units. They take into account the gap property.

This way if we want 3 equal columns we use

```css
.grid-container{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```

To avoid repetition, we can use the repeat css function.

```css
.grid-container{
    display:grid;
    grid-template-columns:repeat(3,1fr);
}
```

### Grid-gap

We can apply spacing between grid items. This is done with the gap property. With gap we apply a common margin, but we can also apply different margins between rows and columns

```css
.grid-container{
    display:grid;
    gap:10px;
    row-gap:10px;
    column-gap:5px;
}
```

### Placing grid items.

We can specify a child element of a grid container which cell it has to occupy (in case the automatic order does not suit our needs). There are several properties to do so, but all of them work the same way as they are simply shorthands

- grid-area: `grid-area: row-start / column-start /row-end / column-end`
  
  - grid-row: `grid-row: row-start / row-end`
    
    - grid-row-start
      
    - grid-row-end
      
  - grid-column: `grid-column: column-start / column-end`
    
    - grid-column-start
      
    - grid-column-end
      

Be advised **the column /row end is non inclusive** This means that to place a cell in the 6th column we would use

```css
.grid-item{
    grid-column: 6 / 7;
}
```

#### Spanning grid items

We can span grid items so that they take more than one column / row of space. This is done by placing it in more than one cell

```css
.grid-item{
    grid-row:1 / 3;
}
```

This cell takes up 2 cells of space, as it spans from cell nº1 until the start of cell nº3

To make one cell take the whole row / column we use -1

```css
.grid-item{
    grid-row:1 / -1;
}
```

### Naming grid tracks

Using indexes to reference grid tracks can be cumbersome and may lead to unreadable code. To solve this we can name tracks when defining them by using []

```css
.grid-container{
    grid-template-rows: [header-start] 100px [header-end] 200px;
}
```

Then we can use those names to position cells.

```css
.header{
    grid-row: header-start / header-end;
}
```

### Grid alignment

We can use justify andalign properties just like in flexbox. There is a difference between justify / align items and justify / align content.

- justify-content: aligns horizontally the grid cells inside their container
  
- justify-items: aligns horizontally the **content** of the grid cells (and not the child item itself but the cell)
  

## Positions

By default, an elements `position` property is set to static. We can modify the position of non static elements with the `top`, `bottom`, `left` and `right` properties.

There are several types of positioning:

- `relative`: we can modify its position relative to its **Original position**
  
- `absolute`: we mopdify its position relative to its nearest positioned ancestor (an ancestor with the position property set to something other than static)
  
- `fixed`: positioned relative to the viewport.
  
- `sticky`: positioned normally until a threshold is passed, then positioned as fixed
  

### Absolute position

The element leaves the flow of the document. This means no space will be reserved for it and it will not push other elements. The use of z-index might be needed to avoid overlap.

We position the element in relation to its **Nearest positioned ancestor**. If there is none, the viewport is taken as reference

```html
<div class="container">
    <div class="abs-pos" />
</div>
<div class="modal" />

<style>
    .container{
        position:relative;
    }

    .abs-pos{
        /*positioned at the center of the container element*/
        position:absolute;
        top:50%;
        left:50%; 
    }

    .modal{
        /*Positioned relative to the viewport*/
        position:absolute; 
        top:50%;
    }    
</style>
```

### Fixed position

We position the element relative to the viewport **always**. As with absolute positioning, the element leaves the flow of the document and no space will be created for him.

### Sticky position

The element is positioned normally and follow the flow of the document. However, With top, left ... we create a threshol. When we scroll past that threshold, the element will be positioned **relative to its nearest block level ancestor** or the viewport by default

```html
<div class="layout-container">
  <div class="navbar-1"></div>
  <div class="navbar-2"></div>
  <div class="item"></div>
 ...
</div>
<style>
.layout-container{
  margin:auto;
  max-width:500px;
  max-height:300px;
  background-color:red;
  overflow:auto;
}

.item{
  margin:auto;
  margin-bottom:10px;
  width:50%;
  height:50px;
  background-color:green;
}

.navbar-2,
.navbar-1{
  width:100%;
  height:50px;
}

.navbar-1{
    background-color:black;
}

.navbar-2{
  background-color:#fff;
  position:sticky;
  top:0;
}
</style>
```

In this example, the layout container has enough content to have scroll, so once we scroll past the element, it will remain at the specified position.

## Variables (custom properties)

We can declare variables in css with the following syntax

```css
.myClass{
    --myVariable:10px;
}
```

Or with the @property rule, that allows more control

```css
@property --colorWhite{
    syntax:"<color>";
    inheritss:false;
    initial-value:#fff;
}
```

Then they can be used like this

```css
.myClass{
    background-color:var(--colorWhite);
}
```

Variables in css are inherited by children of the parent where they are declared. However, we can take advantage of that and define different values for the same variable in different areas

```html
<div class="container">
  <div class="parent">
    <div class="child"></div>
  </div>

  <div class="otherParent"></div>
</div>

<style>
.container{
  --bg-color:red;
}

.parent{
  --bg-color:blue;
}

.child{
  width:100px;
  height:100px;
  background-color:var(--bg-color);
}

.otherParent{
  width:100px;
  height:100px;
  background-color:var(--bg-color);
}
</style>
```

### How to center a div

This is a common joke made to begginer programmers (often in a condescending way).

Leaving all that apart, there isn't a single way of centering elements and depending on the context ones may be more desirable than others. Here are a few (although at the end all comes to knowing the baiscs and applying them creatively)

### Using flexbox

The most straightforward way. We make the parent of the element we want centered a flexbox container and center it horizontally and vertically with `justify-content` and `align-content`

```html
<div class="container">
    <div class="centered-element"></div>
</div>
<style>
.container{
    display:flex;
    justify-content:center;
    align-content:center;
}
</style>
```

### Using grid

The previous example also works with grid, but is way less scalable as if more items were added, we would have to specify more grid properties.

The only advantage grid might offer is the place items property that is a shorthand for the alignment on both axis.

```html
<div class="container">
    <div class="centered-element"></div>
</div>
<style>
.container{
    display:grid;
    place-items:center;
}
</style>
```

### Using justify / align self

We can use flexbox / grid containers but instead of setting the alignment of the children of the container, we align the items themselves.

```html
<div class="container">
  <div class="child"></div>
</div>
```

#### Using flexbox

```css
.container{
    display:flex;
    justify-content:center;
}

.child{
    align-self:center;
}
```

#### Using grid

```css
.container{
  display:grid;
}

.child{
  justify-self:center;
  align-self:center;
}
```

### Using margin

Often overlooked because of how straightforward using flexbox is, but sometimes just using margin can be more elegant

Block components will center themselves **horizontally** with `margin:auto` when their width is specific and does not fill the entire container.

```html
<div class="container">
    <div class="block"></div>
</div>

<style>
    .container{
        width:100vw;
        height:100vh;
    }

    .block{
        width:50%;
        margin:auto;
    }
</style>
```

### Using flexbox + margin

Instead of using the alignment properties we can just use a flex container and set its children's margin to auto. As simple as that.

```html
<div class="container">
  <div class="child"></div>
</div>

<style>
.container{
  display:flex;
}

.child{
  margin:auto;
}
</style>
```

### Using margin + position

Looks significantly uglier than the previous options but is a viable option nonetheless.

In this case we use a parent container with a position of relative and then we give the element we want to center a position of absolute so it is positioned relatively to its parent.

Lastly we set every position property to 0 and set margin to auto, and the element will center itself

```html
<div class="container">
  <div class="child"></div>
</div>

<style>
.container{
  position:relative
}

.child{
  position:absolute;
  top:0;
  bottom:0;
  left:0;
  right:0;
  background-color:green;
  width:50%;
  height:50%;
  margin:auto;
}
</style>
```

### Using transformations

This might be the most ugly way, buit it has its uses. We use position relative or absolute and then set the top and left (or bottom, right) properties to 50% eg, the center.

**However** This positions the origin of the component at the center. If it is a block it will place the top-left corner at the center of its parent element, so we need to **translate** it in both axis by **half** the dimensions of the block

## Css Reset

### 62.5% trick
