# Best Practice of Applying Negative Margin

## Features

when values are `negative`,
- `margin-left`: element moves to the left, the elements behind also move to the left.
- `margin-right`: element remains where it is, the element behind move to the left.
- `margin-top`: element moves to the top, the elements below also move to the top.
- `margin-bottom`: element remains where it is, the elements below move to the top.

### Negative Margin & Floated Element (Key for Layout)

Concept：
```html
<style>
    .box1, .box2 {
        width: 100px;
        height: 100px;
        float: left;
    }

    .box1 {
        /* .box1 will not move. */
        /* .box2 will be moved towards left. */
        /* This causes overlapping of .box2 on .box1. */

        /* When margin-right <= -100px, */
        /* Visually, .box1 width becomes 0px. */
        /* However, it's content remains the current width. */
        margin-right: -100px; 
    }
</style>
<body>
    
    <div class="box1">box1</div>
    <div class="box2">box2</div>
</body>

```
- when negative margin (e.g., margin-right) is applied opposite floated element (float: left),
- margin-right causes the elements behind floated element to move to the left, and causes overlapping.
- `visual hiding`: when the value of margin-right <= -floatedElementWidth, the floated element width becomes 0px visually. Though its content remains the current width (not 0px).


> **case 1: Container without adding padding left and right**
> > - Content Area is available, adjusting using `margin-left`.
```html
<style>

    .main, .box1, .box2 {
        float: left;
    }

    .main {
        width: 100%;
        height: 100px;
    }

    .box1, .box2 {
        width: 100px;
        height: 100px;
    }

    .box1 {
        background-color: red;
        
        margin-left: -100%;
    }

    .box2 {
        background-color: blue;
        /* Since the container without padding right, its content area is large enough to fit in .box2. */
        /* We can use margin-left that can moves .box2. */
        margin-left: -100px;
    }
</style>
<body>
    <div class="container">
        <div class="main"></div>
        <div class="box1">box1</div>
        <div class="box2">box2</div>
    </div>
</body>

```


> **case 2: Container Adding Padding Left and Right**
> > - visual hiding (0px) with `margin-right` 
> > - slight adjustment with `relative`
> > - prevent content overflow with `overflow: hidden`
```html
<style>
    body {
      margin: 0;
    }
    .container {
      /* Adding Left and Rigth Padding to Container */
      padding: 0 100px;
      overflow: hidden;
    }
    .main,
    .box1,
    .box2 {
      float: left;
    }
    .main {
      width: 100%;
      height: 100px;
      background-color: khaki;
    }
    .box1,
    .box2 {
      width: 100px;
      height: 100px;
    }
    .box1 {
      background-color: red;
      /* This place .box1 at the left edge of container content. */
      margin-left: -100%;
      /* We still need to manually adjust it to make .box1 entering padding-left area.  */
      position: relative;
      left: -100px;
    }
    .box2 {
      background-color: blue;
      /* Since padding-right is added, there's no space fitting .box2. */
      /* We applies the concept we learnt. */
      /* Reduce the .box2 to 0px (visually) */
      /* So, it can stay next to .main. */
      margin-right: -100px;
    }
</style>
<body>
    <div class="container">
      <div class="main"></div>
      <div class="box1">box1</div>
      <div class="box2">box2</div>
    </div>
</body>
```

## Rules of Margin Collapsing

- Both Negative, takes the largest absolute value (the most negative value).
- One Positive, One Negative, takes the sum.

**case 1: Siblings**

**case 2: Parent and Child**
Since both parent and child have margin-top, and the resulting margin causes both parent and child to move. (margin top affects self and the element behind.)


## Application

### 1. Equal Height Layout

solution 1: use of negative margin
```css
.container {
    /* 3. Hide the content of left that is exceeding container */
    overflow: hidden;
}

.left {
    /* 1. We add a lot of padding bottom to make left very tall. */
    padding-bottom: 2000px;
    /* 2. Use margin-bottom to pull back the 2000px so the left is again looks like before. */
    margin-bottom: -2000px;
}
```
solution 2: use of absolute positioning

```css
.container {
    position: relative;
}

.left {
    position: absolute;
    /* This makes sure the height of left expands based on its content. */
    top: 0;
    bottom: 0;
}
```

### 2. Single-Row Multi-column Grid

### 3. Overlapping Imgs

### 4. Centering (with Positioning)

### 5. Holy Grail Layout / Double Wing Layout