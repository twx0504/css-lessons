# Font, Text & List Properties

## Font

### 1. color
> In real world project, we do not use color name because we want to specify more precise color.
- Color name `red` (Only for learning / testing purpose.)
- Hexadecimal color code `#f40` or `#cc0066` / `#c06` (brief form)
- rgb `rgb(255, 0, 0)`
- rgba `rgba(255, 0, 0, 0.5)` (compatible starting from IE9)
- etc.

### 2. font-size
> How do we make the font size below 12px?
- Unit can be px, %, rem, em, vw, vh.
- `px`:
  - Default browser font-size is 16px.
  - Browser supports the minimum 12px font size. Font size set below 12px will be default to 12px.
- `%`:
  - Relative to parent font-size.
- `em`: 
  - Relative to parent font-size.

**%**:

```css
/* % */
.parent {
    font-size: 20px;
}

p {
    font-size: 200%; /* (20px * 200) / 100 = 40px */
}
```

**em**:

```css
/* em */
.parent {
    font-size: 20px;
}

p {
    font-size: 2em; /* 20px * 2 = 40px */
}
```

### 3. font-weight

- Set the weight of the font.

**Keywords**:
- `normal`: equivalent to 400 (Default).
- `bold`: equivalent to 700.
- numbers: ranged between 1 - 1000. as long as the weight is supported.

| Value | Keyword Name | CSS Keyword Support |
| ----- | ------------ | ------------------- |
| 100   | Thin         | ✗                   |
| 200   | Extra Light  | ✗                   |
| 300   | Light        | ✗                   |
| 400   | Normal       | ✓ `normal`          |
| 500   | Medium       | ✗                   |
| 600   | Semi Bold    | ✗                   |
| 700   | Bold         | ✓ `bold`            |
| 800   | Extra Bold   | ✗                   |
| 900   | Black        | ✗                   |
| 950   | Extra Black  | ✗                   |

- Relative to parent (rare):
  - `lighter`: lighter than parent. (More Chinese fonts do not support.)
  - `bolder`: bolder than parent. (More Chinese fonts do not support.)

| Inherited value | bolder | lighter |
| --------------- | ------ | ------- |
| 100             | 400    | 100     |
| 200             | 400    | 100     |
| 300             | 400    | 100     |
| 400             | 700    | 100     |
| 500             | 700    | 100     |
| 600             | 900    | 400     |
| 700             | 900    | 400     |
| 800             | 900    | 700     |
| 900             | 900    | 700     |

### 4. font-style

value:
  - normal (Default)
  - italic
  - oblique `<deg>`

### 5. font-family

- Font-family by default is depending on user agent (browsers) 
- Use quote ("") for font-family name that contains multiple words, or doesn't have hyphen(-) 
  -     1. "Segoe UI" (more than one word and without hyphen)
  -     2. sans-serif (contains hyphen)
  -     3. Arial (single word)    
- For Chinese font, quotes must be used 
  - 1. "宋体" (Chinese font)

```css
p {
  font-family: Arial;
}

/* With fallbacks */
p {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
```

### 6. @font-face (Custom Font)

> Check the format on caniuse.com

Types of font format:
1. woff2: most modern browsers support. It has superior compression (30% or more smaller than woff), good for website loading speed and reducing network bandwidth.
2. woff: Most browsers support including IE ver. 9 - 11, except very old versions.
3. ttf: All browsers support. It has bigger size, slower loading speed on the web.
4. svg: deprecated. Most modern browsers do not support except Safari.
5. eot: Only IE ver. 6 - 11 supports.

**Best Practice:**
1. Without considering IE: woff2
2. For legacy support: woff2 + woff

**Warning:**
1. Some fonts have copyright, do not simply use it for commercial.
2. Non-copyrighted fonts: Google Font, Iconfont, etc.
3. Download font files for your project, don't use font provided by CDN.

```css
@font-face {
  font-family: xxx;
  src: url(xxx);
}
```
### 7. font shorthand

- Font is the shorthand property for the following properties in this order:
1. font-stretch
2. font-style
3. font-variant
4. font-weight
5. font-size (must)
6. line-height
7. font-family (must)
- font-size and font-family must be specified in order for it to work.
- line-height must follow font-size `font-size/line-height`
- font-family must be the last property to write
- If the optional properties are not specified, default value will be used

```css
 p {
    /* Note: font size and font-family must   specified in order to work. */
    font: italic bold 20px/1.5 Arial;

    /* If the optional properties are not specifiedit will use default value */
    /* font: 20px Arial; */
}
```

**Best Practice:**
1. Set font (font-size, line-height, font-family, color, etc) uniformly on `<body>`

## Text

### 1. text-decoration

> Generally, we use `text-decoration` a lot.
> Use individual `text-decoration-xxx` properties only to override the default behavior if needed.

`text-decoration` is the shorthand property for the following properties:

1. text-decoration-line
   1. **none**
   2. **underline**
   3. **line-through**
   4. overline
   5. grammar-error
   6. spelling-error
2. text-decoration-style
   1. solid
   2. double
   3. dotted
   4. dashed
   5. wavy
3. text-decoration-color
4. text-decoration-thickness

```css
p.underline {
  text-decoration: underline;
}

h2.underline-wavy {  
  text-decoration: underline wavy: 
}

p.underline-overline {
  /* We can specify one or more lines */
  text-decoration: underline overline green;
}
```
### 2. text-indent

- Set the indentation of the first line of a block of text.
- Usually 2em indentation is set
- Values:
  - `<length>`: e.g., em, relative to the element’s own computed font-size.
  - `<percentage>`: relative to the containing block's width (parent content area excluding padding and border)

### 3. line-height

- Set the height of a line box in horizontal writing mode.
- Set the distance between lines of text.
- Block element: specify the preferred height of line boxes within the element.
- Inline non-replaced element: specify the line box height.
- values:
  - `<length>`: e.g., px
  - `<number>`: multiplied by the element's font size (preferred to avoid unexpected results due to inheritance)
  - `<percentage>`: relative to the element's own font-size
  - `normal`: depends on the user agent (~1.2, depending on the element's font-family)

**Best Practice:**
1. Set line-height with unitless number (preferrably 1.5) on `<body>`
   1. Good for accessibility
   2. Scale the line-height proportionately when the page is zoomed
2. Set line-height of an element equal to the element's own height to vertically center the single line of text.

### 4. text-align

- Controls the horizontal alignment of inline-level content inside a block element / table-cell box
- e.g., text, image

1. start / left
2. end / right
3. center
4. justify

### 5. word-spacing

- Set the space between words (e.g., English).
- Useless for chinese words.
- Values:
  - `normal`: based on current font / browser.
  - `<length>`: e.g., px, em

### 7. letter-spacing

- Set the space between text characters.
- Works for Chinese words!
- Values:
  - `normal`: based on current font / browser.
  - `<length>`: e.g., px, em

> - Note: 
> - Beware of value < 0 as the text may overlap, or go in the reverse order.
> - Useful if we want to achieve text animations.


## List

### 1. list-style-type

> Generally, we will remove list style.
> These list style cannot be customized, less flexible.
> Use spans if we want to customize the list style.

- Values:
  1. none (common - we want to remove list style)
  2. disc 
  3. circle 
  4. square 
  5. decimal 
  6. georgian 
  7. trad-chinese-informal 
  8. kannada 

```css
ul > li {
  list-style-type: none;
}
```

### 2. list-style-image

- Set an image as the list item marker.
- Problem: less flexible, we cannot change the size of image!

- Values:
  1. none
  2. `<url>`: using `url()`

```css
ul > li {
  list-style-image: url("xxx");
}
```

### 3. list-style-position

- Set the position of list item marker.
- Problem: less flexible, we cannot specify the exact value where the marker should be.

- Values:
  1. outside
  2. inside

```css
ul > li {
  list-style-position: inside;
}

```
### 4. list-style shorthand

> Usually, we will use this to remove the list item marker.

- This is the shorthand property of the following properties:

1. list-style-type
2. list-style-image
3. list-style-positoin

```css
ul > li {
  list-style: none;
}
```