# CSS Basic

## Introduction

- not a programming language (that gives instructions).
- not a markup language (that represents structure of the document) either.
- a style sheet language that is used to selectively style HTML elements.

CSS & CSS3: CSS3 is the latest version of CSS, with more new features like animation, 3D effect, etc.

## Syntax of CSS Ruleset

CSS ruleset = selector + declaration block.

declaration = property + value / values.

```css
selector {
    /* This is a comment. */
    property1: value;
    property2: value1 value2;
}
```

## Comments in CSS


- comment: `/* comment */` in CSS. 
  - improve readability and maintainability of CSS code.
  - for own use or for others to understand the code.
- Hot Keys:
  - `Ctrl + /` OR
  - `Alt + Shift + A`


## How to Write CSS?

1. single line (not recommended)

```css
p {
    /* declarations written in one line, separate by a tab space. */
    color: red; font-size: 20px;
}
```

2. multi-line
- easy to read and modify.
```css
p {
    /* declarations written in separate new lines. */
    color: red;
    font-size: 20px;
}
```

## Adding CSS to Document (HTML)

> inline styles has higher specificity.
> external & internal stylesheet if there's style conflict:
> > - same specificity, the one comes behind win.
> > - different specificity, the one with higher specificity win.


### 1. Internal stylesheet

- write CSS within `<style>` in HTML `<head>`.
- use case: useful when you are not allowed to change the external stylesheets.
- drawbacks: repeated internal stylesheets & maintenance issues when a single change requires all other stylesheet to be updated manually.
- use cases: 
  - for simple cases / small project.
  - for website that requires high initial load speed e.g., Baidu

> Knowledge Point: 
> Check out [First ContentFul Paint](https://web.dev/articles/fcp) 
> HTTP request requires time - it might depend on network connection, and file size!.
> Internal stylesheet is already part of the HTML, which doesn't need to send out request!
> For visible part of the page, we might use internal stylesheet.
> Use external stylesheet for non-visible part of the page.
  
```html

<head>
    <!-- in HTMK5, type is optional, specifying the type of stylesheet. -->
    <!-- <style type="text/css">...</style> -->
    <style>
        p {
            color: red;
        }
    </style>
</head>

```

### 1. External stylesheet

- write CSS in a separate `.css` file and link it to HTML via `<link>` in HTML `<head>`
- recommended.
- applying a single stylesheet over multiple HTML web pages.

```html
<head>
    <!-- rel: relationship, telling the browser how this item is being linked to HTML.-->
    <!-- href: hypertext reference, specify the url / path of the linked resource. -->
    <link rel="stylesheet" href="css/index.css">
</head>
```

### 3. Inline style

- write on HTML element within a `style` attribute.
- only affect that element.
- usually use with `JS` to apply styles dynamically.
- drawback: mix structure and style.

```html

<p style="color: red; font-size: 20px">Lorem</p>

```

## Basic Selectors

Selectors are patterns used to match / select elements we want to style.

### 1. Type Selector / Tag Name Selector

- target all elements of a certain type.
- usage: use to reset default styles due to its large coverage.

```css
p {
    /* declaration... */
}
```
### 2. Id Selector

- target an element with specific id.
- id must be unique in a page. 
- select element via JS, only the first element with that id will be selected.
- use case: add id when we want to use Js to manipulate the element.

```css
#id {
    /* declaration... */
}
```

### 3. Class Selector (Commonly Used)

- target elements with the class name (content of class attribute)
- uses:
    - each element can have multiple classes, separated by a space.
    - similar class name can be used in multiple elements.
    - common styles can be put in a class selector to reduce the lines of code. (Atomic CSS)
- naming must be meaningful and descriptive.
```html
<style>
.class {
    /* declaration */
}
</style>

<body>
    <div class="box header font">Header</div>
    <div class="box main">Main</div>
    <div class="box footer">Footer</div>
</body>
```
#### Atomic Classes
- define utility classes for common styles such as font-size, text, font-color, line-height, etc.
- We can choose what utility classes we need to quickly add styles.
- usually, it is used in big projects.
- CSS Framework that use atomic classes [Tailwind](https://tailwindcss.com/)
- drawback: long class names, might be hard to read.

> All things has its flip sides!


### 4. Universal Selector (*)

- match elements of any type.
- there's performance overhead issue, generally it is not used in projects.
- for practice purposes, it is okay to use.

```css
/* Remove margin and padding of all elements. */
* {
    margin: 0;
    padding: 0;
}
```

### Specificity of Basic Selectors

- inline styles > id selectors > class selectors > type selectors

## Combinators

### 1. Descendant Combinator (Space)
- use to select elements that are descendants of another element.
- descendant is not necessary child. It can be grandchild, great-grandchild, etc.

```css
div p {

}

div p span {
    
}
```