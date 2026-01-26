# Development Standards and Best Practices

## History

### 1. The Birth of HTML (Hypertext Markup Language)

- Tim Berners-Lee - the inventor of the World Wide Web
- 1991 - first website.
- only text and img.
- no styles!

### 2. The Birth of CSS

- 1994
- Hakon Wium Lie & Gijsbert (Bert) Bos

### 3. CSS Versions

- CSS1.0 -> CSS2.1 -> CSS3
- Until 2015, each CSS feature was separated and managed by levels (level1, 2, 3, ...)
- no more CSS4.0.
- Check each CSS features and levels here: [CSS Working Group Editor Drafts](https://drafts.csswg.org/)

### 4. Research Areas of CSS

- Visual Effects - animation, 3D, gradients etc... 
- Layouts - flex, grid, responsive
- Engineering / Tooling - Sass, Less, Postcss

## CSS File Organization & Functional Classification

### 1. CSS File Organization

- usually in medium to large projects
- global css / common css e.g., reset.css, media.css, common components, ...
- theme css e.g., theme-skyblue.css 
- page-specific css e.g., index.css (homepage), login.css (login page)

```html
<link href="./assets/css/global.css" rel="stylesheet" type="text/css" />
<link href="./assets/css/index.css" rel="stylesheet" type="text/css" />
<link href="./assets/css/theme.css" rel="stylesheet" type="text/css" />

```

### 2. Functional Classification

take common css as example:

- reset styles
- common layout styles
- common modules： larger reusable structure e.g., navigation bar, login, register, lists, comments, search
- reusable UI Elements: indivisible, relatively small unit (already smallest) e.g., buttons, input field, icon, loading spinner.
- common responsive system


### 3. Reset Default Styles

- reset.css
- normalize.css

### 4. Global / Common Layout

> based on layout strategies we chose: flex, grid, float, positioned, etc.

- two-column layout for PC
- Header-Content-Footer Layout for Mobile

### 5. Common Modules

- larger portion structure that can be used in many places.
- e.g., navigation bar, search, login, register, etc.
### 6. Reusable UI Elements

- the smallest unit of element that cannot be divided into smaller anymore. 
- commonly used in each module.
- e.g., buttons, inputs, etc.


### 7. Common Responsive System

- implement responsive layouts across different devices when a specific breakpoint is met.
- e.g., add floated elements, activate grid layouts, show or hide elements, adjust container width.

## Default Element (tag) Styles and Reset

- some HTML tags come with default styles (user agent)
    - body has `margin: 8px;`
    - ul has `margin: 16px 0;` & `padding-left: 40px;`
    - p has `margin: 16px 0;`
- these default styles might causes slight inconsistency / minor issues, it is best to reset them.
- CSS reset:
  - ```css
    /* Set all selector margin and padding to 0. */
    /* It is simple and safe, but it uses a lot of computing resources / power. */
    /* Not recommended on  large-scale websites like Taobao / YouTube */
    * {
        margin: 0;
        padding: 0;
    }
   ```
- [YUI Reset CSS](https://clarle.github.io/yui3/yui/docs/cssreset/)
- [Eric Meyer CSS Tools: Reset CSS](https://meyerweb.com/eric/tools/css/reset/)
- [Normalize css](https://github.com/necolas/normalize.css): preserve useful default styles unlike reset.css + ensure consistency across browsers + explanation comments.



## CSS Methodology

- best practice, designed by individuals and organizations, validated by many projects.
- involves structured naming convention, provide guidelines on how to organize CSS.
- improve performance, readability and maintainability. 

### 1. Object-Oriented CSS (OOCSS)

- 2009 - Nicole Sullivan.

- encourage code reuse by abstracting different features to reusable class-based modules (object).


- rule 1: separate structure (layout, size, position) & skin (colors, background-colors).

    ```html
    <style>
      .col {
        float: left;
        width: 200px;
      }
      .line {
        background: #f60;
      }
    </style>
    <div class="line col"></div>
    ```

- rule 2: separate container & content.
  - once child leaves the parent, it's still able to display correctly.
    ```html
    <style>
      .line {
        background: #f60;
      }
      .unit {
        width: 50%;
      }
    </style>
    <div class="line">
      <div class="unit"></div>
    </div>
    ```

*naming convention*:
- class name should be able to tell the purpose / usage, and make it common.
  - e.g., mod, complex, pop.
- if writing too semantic class name, it will be more specific to apply to somewhere else.

*drawbacks*:
- create HTML that is full of classes (as the styles becomes more and more atomic).
- avoid specificity by abandoning cascading. reduce the advantage of CSS combinators.
- less semantic naming due to the intention to make more general/common classes

To learn more about [Introduction to OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)

### 2. Block Element Modifier (BEM)

concept: use structured class name to tell the semantic of class and how it is related to other classes.

- parts:
  - block: meaningful standalone entity (the highest level abstraction) such as `header`, `container`, `menu`, `input` ...
  - element: part of block in which its semantic is tied to the block and can't exist on its own. Example, `menu item`, `list item`, `header title`, `checkbox caption`
  - modifier: state of block / element, used to change their appearance and behaviours, such as `highlighted`, `selected` ,`disabled`, `size big`, `color yellow`.

- naming convention:
  - block, element, modifier must be lowercased.
  - use classname selector `.header{}` only, no tag name `header{}` / ids `#header{}`.
  - each block should be independent and not depend on other block / element.
  - `.block__element--modifier`
  - e.g., `.top-nav__button--disabled`


- drawback:
  - abandon CSS cascading.
  - long and complex css class names.
  - require proper documentation to avoid readability issue (hard to read HTML structure)

To learn more about [BEM](https://getbem.com/introduction/)

### 3. Scalable and Modular Architecture for CSS (SMACSS)

- 2011 by Jonathan Snook
- core: categorization on the basis on OOCSS & BEM.
  - `base`: define default styles on html elements with element selector, attribute selector, pseudo class selector etc.
  - `layout`: divide page into sections.
  - `module`: a reusable modular part e.g., navigation bar, product list.
  - `state`: describe how layout or module will look like when in a particular state.
  - `theme`: similar to state, can be used to modify the styles of the aforementioned categories. e.g., link colors, layout methods.
- naming conventions (prefixes of categories):
  - base does not need as it is applied directly to element.
  - `l-` or `layout-` such as `.l-inline` or `.layout-grid`.
  - `m-` or name of itself such as `.m-profile` or `.field`.
  - `is-` such as `.is-collapsed` or `.is-active`
  - `theme-` such as `.theme-a-background` or `.theme-l-grid`.

> there's no strict rule of sticking to only single methodology. We can combine the advantage of each methodogy.
> Example, the first rule of OOCSS, naming convention of BEM, and prefixes of SMACSS.
> - base use SMACSS rule, layout and module use SMACSS prefixes.
> - use double underscores (`__`) to separate children, use `is-` for its state.
> - modifier can be started with prefix `is-`, combine with module with double dashed(`--`).
> maintain cascading at most one layer.

```html
<style>
  /* layout */
  .l-notice {
  }
  /* module */
  .m-notice {
  }
  /* combine module with state */
  .m-notice--is-active {
  }
  .m-notice__img {
  }
  /* One layer cascading */
  .m-notice__content h6 {
  }
  /* modifier start with is- */
  .is-important {
  }
</style>
<div class="m-notice l-notice">
  <img class="m-notice__img" />
  <div class="m-notice__content">
    <h6>......</h6>
    <h6 class="is-important">......</h6>
  </div>
</div>

```
> CSS methodology is not perfect. Naming is too long, hard to maintain. HTML is not brief.
> But it has advantages of its own. e.g., no conflict of styles in complex structure.


## Best Practice of Styles

- only class selectors, abandoning ID selector (due to non-reusable).
- simple semantic naming. e.g., `.m-abc` (x) vs `.m-navigation` (x) vs `.m-nav` (/).
- distinguish classes with same semantic meaning but different implementation by adding number or alphabet. e.g., `.m-list`, `.m-list-1`, `.m-list-2` they are list modules semantically but different implementation within.
- avoid pollution / being polluted. use child combinator `>` e.g., `.m-nav > li`, not `.m-nav li`.
- end the last value with a semicolon `;`. (note: withou `;` is ok but might cause problem e.g., in the case of minifying css.)
- ignore the unit of 0 value. e.g., 0px, 0em, 0% as 0 to save space and improve response time.
- write the properties based on how importance they are. e.g., `position / layout property` > `box model properties` > `text & other decoration properties`.
- format and align CSS properties with formatter plugin.