# Advanced Selectors
[TOC]
## 01 Compound Selector

- Combines multiple simple selectors, without spaces, not separated by a combinator.
- Type selector or universal selector must come first.
- Only one type selector is allowed.

```css
/* Element with class */
div.container { }

/* Element with multiple classes */
button.btn.primary { }

/* Element with ID and class */
input#email.required { }
```

## 02 Selector List

- A list of selectors separated by commas.
- Applies the same styles to multiple selectors 
- Example: Use in CSS reset

```css
/* Multiple selectors */
h1, h2, h3 {
  font-family: Arial, sans-serif;
}

/* Mix of different selector types */
.header, #nav, footer {
  background-color: #333;
}
```

## 03 Combinators

### 01 Descendant Combinator

- Selects all descendants (space separator).
- Note: descendants are not limited to direct child.

```css
/* All <p> inside <article>, at any depth */
article p {
  line-height: 1.6;
}

/* All <span> inside elements with class .highlight */
.highlight span {
  color: yellow;
}
```

### 02 Child Combinator

- Selects direct children only (`>` separator).

```css
/* Only direct <li> children of <ul> */
ul > li {
  list-style: disc;
}

/* Direct <p> children of .container */
.container > p {
  margin-bottom: 20px;
}
```

### 03 Next-sibling Combinator

- Selects the immediately following sibling (`+` separator).

```css
/* <p> immediately after <h2> */
h2 + p {
  font-weight: bold;
}

/* Label immediately after checkbox */
input[type="checkbox"] + label {
  margin-left: 5px;
}
```

### 04 Subsequent-sibling Combinator

Selects all following siblings (`~` separator) that are preceded by another element.

```css
/* Select all <p> that follow <h2> (same parent) */
h2 ~ p {
  color: #666;
}

/* Select all images after the first paragraph */
p ~ img {
  display: block;
  width: 50px;
  height: 50px;
}
```

## 04 Pseudo-Classes

- A keyword added to the selector to let us select elements based on information outside of the document tree.
- Example, a specific state of the selected element.

### 01 User Action Pseudo-Classes

- Target elements based on user interaction.

```css
/* Hover state */
a:hover {
  text-decoration: underline;
}

/* Active state (being clicked) */
button:active {
  transform: scale(0.98);
}

/* Focus state (keyboard/click focus) */
input:focus {
  outline: 2px solid blue;
}
```

### 02 Location Pseudo-Classes

- Target elements based on URL/location.

```css
/* Unvisited links */
a:link {
  color: blue;
}

/* Visited links */
a:visited {
  color: purple;
}
```

Note: 
> - When styling links, we must style it in the following order:
> - `:link`, `:visited`, `:hover`, `:active` (LOVE-HATE)
> - So that it will work properly.

```css
/* Unvisited links */
a:link {
  color: blue;
}

/* Visited links */
a:visited {
  color: purple;
}

/* Hovered links */
a:hover {
  /* Styles... */
}

/* Active links */
a:active {
  /* Styles... */
}
```

### 03 Input Pseudo-Classes

- Target form elements based on their state.

```css
/* Checked checkboxes/radios */
input:checked {
  accent-color: green;
}

/* Required fields */
input:required {
  border-left: 3px solid red;
}
```

### 04 Tree-Structural Pseudo-Classes

- Target elements based on their position in the DOM tree.

#### 01 `:first-child` & `:last-child`
- `:first-child`: Select the first element among siblings.
- `:last-child`: Select the last element among siblings.

#### 02 `:nth-child` & `:nth-last-child`

- `:nth-child(n)`: Select elements that are the n-th child of its parent.
- `:nth-last-child(n)`: Select elements that are the n-th child of its parent, counted from the end.
- Values:
  - `n`: integer value (1-based)
  - `An+B`: n starts from 0
  - `Keywords`: `odd`, `even`

#### 03 `:nth-of-type` & `:nth-last-of-type`

- `:nth-of-type(n)`: Select the n-th element of each tag type among its sibling.
- `:nth-last-of-type(n)`: Select the n-th element of each tag type among its sibling, counting from the end.
- Values:
  - `n`: integer value (1-based)
  - `An+B`: n starts from 0
  - `Keywords`: `odd`, `even`

#### 04 `:only-child`

> Note: text nodes do not count as elements.

- Select an **element** without any siblings.
- Similar to `:first-child:last-child` or `:nth-child(1):nth-last-child(1)`, but lower specificity.

```css
.box :only-child {
  color: red;
  background-color: tomato;
}
```

#### 05 `:root`

- Select the root element of the document.
- Represents `html` element.
- Higher specificity than `html` element.
- Useful for declaring global CSS variables / custom property.

```css
:root {
    --primary-clr: green;
    --main-font: 16px;
}
```

#### 06 `:empty`

- Select elements that have no child elements and no text nodes (including whitespace).
- Note: Comments / CSS `content` do not affect whether an element is empty or not.

```css
p:empty {
    background-color: tomato;
}
```

## 05 Pseudo Elements

- A keyword that let us style a specific part of the element.
- Some pseudo elements like `::before` and `::after` will create a virtual element that is not part of the DOM.
- So, we can't select pseudo elements using JavaScript.
  
> Note: `getComputedStyle` in JavaScript allows us to get the style of the pseudo element.

### 01 `::before` & `::after`

- Insert content before or after an element's content.
- Creates an inline pseudo-element by default.
- `content` must be specified, even if it is an empty string.
- Used for decorative purposes.

```css
/* Decorative elements */
.button::before {
  content: '';
  display: inline-block;
  width: 10px;
  height: 10px;
  background-color: green;
  border-radius: 50%;
  margin-right: 5px;
}

/* Clearfix */
.clearfix::after {
  content: '';
  display: block;
  clear: both;
}
```

### 02 `::placeholder`

- Styles the placeholder text in input fields (input / textarea).

```css
input::placeholder {
  color: #999;
  font-style: italic;
  opacity: 0.7;
}

textarea::placeholder {
  color: #aaa;
  font-size: 0.9em;
}
```

### 03 Other Pseudo-Elements
```css
/* Selected text */
::selection {
  background-color: yellow;
  color: black;
}

/* Marker (list bullets/numbers) */
li::marker {
  color: red;
  font-weight: bold;
}
```

## 06 Attribute Selectors

- Target elements based on their attributes.

| Forms          | Description                         |
| -------------- | ----------------------------------- |
| `[attr]`       | Has attribute                       |
| `[attr=val]`   | Exact match                         |
| `[attr=val i]` | Exact match, case-insensitive       |
| `[attr=val s]` | Exact match, case-sensitive         |
| `[attr^=val]`  | Starts with                         |
| `[attr$=val]`  | Ends with                           |
| `[attr*=val]`  | Contains substring                  |
| `[attr~=val]`  | Word match (space-separated values) |
| `[attr\|=val]` | Exact match or starts with `val-`   |

> Note: 
> - Without specifying `i` or `s` flag, the default case-sensitivity depends on the html attributes.
> - Case-insensitive attr: `type`
> - Case-sensitive attr: `class`

```css
/* Has attribute (any value) */
[disabled] {
  opacity: 0.5;
}

/* Exact match */
[type="text"] {
  border: 1px solid #ccc;
}

/* Starts with */
[href^="https"] {
  color: green;  /* External secure links */
}

/* Ends with */
[href$=".pdf"] {
  background: url('pdf-icon.png') no-repeat right;
}

/* Contains */
[class*="card"] {
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* Word match (space-separated) */
[class~="active"] {
  font-weight: bold;
}

/* Starts with (dash-separated) */
[lang|="en"] {
  /* Matches lang="en" or lang="en-US" */
  color: red;
}

/* Case-insensitive flag */
[type="text" i] {
  /* Matches TEXT, Text, text, etc. */
  background: white;
}

/* Case-sensitive flag */
a[href*="cAsE" s] {
  color: pink;
}

/* 
Note:
 - Attribute "type" is case insensitive by default
 - The following input[type="TEXT"] would still work.
 - To make it case-sensitive, use "s" flag.
 - Now, input[type="TEXT"] will only match if the element has type="TEXT".

 - Note: Class attribute's value is case-sensitive.
 */
input[type="TEXT" s] {
    background-color: blue;
}
```

### Combining Attribute Selectors

```css
/* Multiple attributes */
input[type="email"][required] {
  border-color: orange;
}

/* With other selectors */
a.external[target="_blank"]::after {
  content: ' ↗';
}
```