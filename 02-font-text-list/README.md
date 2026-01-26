# Font, Text & List Properties


## Font
### 1. color
> In real world project, we do not use color name because we want to specify more precise color.
- color name `red` (Only for learning / testing purpose.)
- hexadecimal color code `#f40` or `#cc0066` / `#c06` (brief form)
- rgb `rgb(255, 0, 0)`
- rgba `rgba(255, 0, 0, 0.5)` (compatible starting from IE9)
- etc.

### 2. font-size
> How do we make the font size below 12px?
- unit can be px, %, rem, em, vw, vh.
- px:
  - default browser font-size is 16px.
  - browser supports the minimum 12px font size. Font size set below 12px will be default to 12px.
- %:
  - relative to parent font-size.
```css
.parent {
    font-size: 20px;
}

p {
    font-size: 200%: /* (20px * 200) / 100 = 40px */
}
```

### 3. font-weight
keywords:
- normal: equivalent to 400.
- bold: equivalent to 700.
- relative to parent:
  - lighter: lighter than parent. (More Chinese fonts do not support.)
  - bolder: bolder than parent. (More Chinese fonts do not support.)

numbers: ranged between 1 - 1000. as long as the weight exists.
- 100
- 200
- 300
- 400 (Regular)
- 500 
- 600
- 700 (Bold)
- 800
- 900
- 1000
### 4. font-style
- normal
- italic
- oblique

### 5. font-family

### 6. @font-face (Custom Font)


## Text

### 1. text-decoration
### 2. text-indent
### 3. line-height
### 4. text-align
### 5. word-spacing
### 7. letter-spacing
### 8. text-align 

## Font Composite Properties


## List

### 1. list-style-type
### 2. list-style-image
### 3. list-style-position
### 4. list-style shorthand