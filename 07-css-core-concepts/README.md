# CSS Property Value Processing
[CSS Property Value Processing](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Property_value_processing)
[Cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Introduction)
[Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Specificity)


- How browsers determine the final value for every CSS property:

## Step 1 Declared Values

- The browser takes all declared values (including conflicting ones) from CSS rules that apply to the element. 

## Step 2 Cascading (Resolve Conflicts)

> Conflicting styles: When more than one CSS declaration tries to set the same property on the same element.

- Cascade: An algorithm the browser uses to decide which style is applied to an element when there are conflicting styles.


### 2.1 Compare Origin and Importance

> Origin: Where the CSS comes from.
> Importance: Does the declaration have the `!important` flag?

| Precedence Order (low to high) | Origin                  | Importance   |
| ------------------------------ | ----------------------- | ------------ |
| 1                              | user-agent (browser)    | normal       |
| 2                              | user                    | normal       |
| 3                              | author (developer)      | normal       |
| 4                              | CSS keyframe animations |              |
| 5                              | author (developer)      | `!important` |
| 6                              | user                    | `!important` |
| 7                              | user-agent (browser)    | `!important` |
| 8                              | CSS transitions         |              |

### 2.2 Compare Specificity

- Specificity: an algorithm that calculates the weight of a CSS selector to determine which declaration wins when multiple rules target the same element.
- Specificity is calculated in this format: `(INLINE ,ID, CLASS, TYPE)`

| Selector Categories                                      | Specificity (Weight) |
| -------------------------------------------------------- | -------------------- |
| `Universal Selector (*)`, `Combinators (+, >, ~, space)` | 0,0,0,0              |
| `Type Selector`, `Pseudo-element`                        | 0,0,0,1              |
| `Class Selector`, `Attribute Selector`, `Pseudo-class`   | 0,0,1,0              |
| `ID Selector`                                            | 0,1,0,0              |
| `Inline Style`                                           | 1,0,0,0              |



**Special Cases:**

`:where()` - Always `0,0,0,0` (zero specificity)

```css
:where(#id, .class, p) { /* 0,0,0,0 - always zero */ }
```

`:is()`, `:has()`, `:not()` - Take highest parameter specificity, but the pseudo-class itself adds no weight

```css
:is(#id, p)   { /* 1,0,0,0 - takes #id */ }
:has(> .class) { /* 0,0,1,0 - takes .class */ }
:not(p)       { /* 0,0,0,1 - takes p */ }
```

### 2.3 Compare Order of Appearance

> Source order: the order in which CSS rules appear in our stylesheet(s), read from top to bottom.

- The last declaration in the source order wins.
- Only applies when: `Origin`, `importance`, AND `specificity` are all equal.

```css
p {
  color: red;   /* Lost - appears first */
}

p {
  color: blue;  /* Wins - appears last */
}
```

> Both selectors have identical specificity (`0,0,0,1`), so source order determines the winner.

## Step 3 Inheritance

- If properties of an element still have no values, and the property is inheritable, it will inherit values from its parent element.

**Inherited property:**
- Properties that automatically take the parent element's value when not explicitly set

- Examples:
  
| Category   | Examples                                                        |
| ---------- | --------------------------------------------------------------- |
| font       | `font-size`, `font-family`, `font-style`, `font`, `font-weight` |
| text       | `color`, `text-align`, `line-height`, `word-spacing`, etc.      |
| list       | `list-style`, `list-style-type`, etc.                           |
| cursor     | `cursor`                                                        |
| visibility | `visibility`                                                    |
|            |

**Non-inherited property:**
- Properties that do not automatically inherit from parent elements.
- If not set, they will use their initial value (Step 4).
- Example:

| Category  | Examples                                                                                                          |
| --------- | ----------------------------------------------------------------------------------------------------------------- |
| box-model | `display`, `margin`, `border`, `padding`, `width`, `height`, `min-width`, `max-width`, `min-height`, `max-height` |
| position  | `position`, `left`, `right`, `top`, `bottom`, `z-index`                                                           |
| float     | `float`, `clear`                                                                                                  |
| others    | `background`, `overflow`, `vertical-align`, etc                                                                   |

**`<a>` element**
- The color property is inheritable.
- User agent stylesheet provides a declared value for `<a>` element.
- Since `<a>` color already has a declared value (Step 1), inheritance (Step 3) does not occur even if the parent of `<a>` has declared color.


**line-height inheritance:**

- `<length>`: The absolute length is inherited as is. The element uses the exact same `<length>` as his parent's.
- `<unitless>`: The unitless number is inherited. The element uses `unitless * own font-size`
- `<percentage>`: The computed value (in px) is inherited. The element uses the inherited px value, regardless of its own font-size.

```css
.parent {
    font-size: 12px;
    /* 200% * 12px = 24px (note: 12px is from parent) */
    line-height: 200%;

    /* line-height: 2; */
    
    /* line-height: 50px; */
}

.child {
    font-size: 16px;
}
```

**font-related properties:**
- Set the font properties on the `<body>` element.

**Possible CSS Property Values:**
- `inherit`: always inherit from parent
- `initial`: always use default CSS value
- `unset`: inherit if possible, otherwise default


## Step 4 Use Initial Values

> The initial value of any property can be checked in MDN.

- If some properties still have no values, use the initial value.
