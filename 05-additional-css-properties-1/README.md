# Other Properties

## 1. Cursor

- Set the mouse cursor appearance when hovering over an element.
- Values:
  - Keywords: `pointer`, `move`, `text`, etc.
  - Custom: `cursor: url(path), fallback;`
  - Note: Use custom image as cursor appearance, fallback keyword must be provided in case custom image loading is failed.

```css
.box1 {
    cursor: pointer;
}

.box2 {
    cursor: url("./fish.ico"), auto;
}

```
## 2. Outline Shorthand

- Specify outline (A line drawn around an element, outside the border) of an element
- `outline: <width> <style> <color>;`
- Unlike borders, 
  - An outline doesn't take up space.
  - We cannot change style of any side of outline.
  - Less flexible than border (e.g., we can change border radius, but there's no outline radius).

- input elements usually have outline.


```css
.box {
    /* Syntax is similar to border */
    outline: 2px dashed blue;
}
```

**Equivalent to the following longhand properties:**
- Almost similar to border
1. `outline-width`
2. `outline-style`
3. `outline-color`

**Additional Property:**
1. `outline-offset`: Set the amount of space between an outline and the edge / border of an element. Default: 0

**Use Case:**

```css
input {
    /* We will remove the outline of input element most of the time. */
    outline: none;

    /* We can change the border-color when needed. */
    border-color: blue;
}
```


## 3. Overflow

> - Scroll container: an element in which content can be scrolled.
> - Only element with `overflow: clip;` is not a scroll container.
> - Overflow value other than `visble` and `clip` creates a new Block Formatting Context (BFC).
> > - One of the use case of BFC is to clear float.
> - JavaScript: `element.scrollTop` property can be used to scroll through the content in a scrolled container.

- Set the behaviour when the content does not fit in the element padding box (overflow).
- For block elements, flex containers, grid containers.
- values:
    - `visible`: Content overflows and is visible outside the box (default)
    - `hidden`: Overflow content is hidden, no scroll bar, but support programmatic scrolling
    - `scroll`: Display scrollbars whether or not the content is overflowing
    - `auto`: Display scrollbars only when content overflows
    - `clip`: Similar to `hidden`, but forbids programmatic scrolling



**Longhand Properties:**
1. `overflow-x`: Set horizontal overflow behavior
2. `overflow-y`: Set vertical overflow behavior

**Note:**
- The computed values of overflow-x and overflow-y are related
- If specified, use specified value.
- Certain combinations force the browser to modify the computed value.
- e.g., If one axis is 'visible', and the other axis is not 'visible', the 'visible' axis is converted to 'auto'.
- e.g., If one axis is 'clip', and the other is not 'clip', the 'clip' axis is converted to 'hidden'.

## 4. Vertical Align

> Note: 
> - `vertical-align` may not be able to vertically center an element precisely
> - Use `position` to adjust if needed
> - This property is rarely used now.
> - Modern ways of centering element uses `flexbox`.

- Set the vertical alignment of an inline level element / table cell box.
- Values:
  - Keywords (relative to parent):
    - `baseline`: Align element's baseline with parent's baseline (Default)
    - `top`: Align top of element's virtual area with top of line box
    - `bottom`: Align bottom of element's virtual area with bottom of line box
    - `middle`: Align middle of element (½ content area height) with baseline + ½ `x`-height of parent
    - `text-top`: Align top of element's virtual area with top of parent's content area
    - `text-bottom`: Align bottom of element's virtual area with bottom of parent's content area
    - `sub`: Lower baseline to subscript position
    - `super`: Raise baseline to superscript position
  - `<length>`: 
    - `element's baseline = parent's baseline + <length>`
    - `<length>` can be negative, represent opposite direction.
  - `<percentage>`:
    - `offset = <percentage> × parent's line-height`
    - `element's baseline = parent's baseline + offset`
    - - `<percentage>` can be negative, represent opposite direction.
> Virtual area = element's content area + gaps



