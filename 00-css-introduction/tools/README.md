# Tools

## Procedures

1. Product Manager provides prototype (business logics) to UI designer, frontend & backend developers.
    - Prototype Analysis
    - High-level & low-level design
    - System Design
    - Database design
    - System Architecture Design (User volume, extendable, concurrency, update, short-term, long-term)
    - API design
    - Frontend -> confirms the API specification with backend.
    - Frontend -> define the route (After API has been designed) ensures the fundamental architecture is set up. The business logic, server, and database connections should be fully functional.
3. push to the collaborative interface design tool (Figma) - improve efficiency - like GIT.
   - everyone will receive notifications when update is there.
4. gives to developers (frontend & backend) to develop webpages.


> Frontend developers must measure UI design with tools and ensure the measurements are correct.

## Length Units & Colors

### 1. Length

- most CSS properties are used to control the position and size, so their values must be a number + length unit.
- Two types of length units: 
    - absolute unit: **px**, pt, in, mm, cm
    
    - relative unit: relative to the font size of parent, the size of viewport, etc.
      - benefit: improve responsiveness.
      - rem (root font size), em (parent font size), vw (1% of viewport width), vh (1% pf viewport height), vmin (percentage the smallest of vw and vh), vmax (percentage the largest of vw and vh), ex (height of letter x), ch (width of 0), lh (line-height of element)

    
### 2. Colors

- 24-bit color depth is used by virtually every computer and phone display.

> color depth: the number of bits used to indicate the color of a single pixel

- There are three channels for R,G & B and each channel has 256 values.

```css
/* 
1 byte = 8 bits = 2^8 = 256 combinations

24 bit combinations = 2^24 = Three 8 bit colors = 256^3 = 16777216 ~= 16.7 million color combinations 
*/
```

**1. Color Keyword**
- `color: red;`

**2. RGB**
- `rgb(r, g, b)` each param ranged 0 - 255.
- e.g., rgb(0, 0, 0) is black.

**3. RGBA**
- with additional alpha channel determining transparency.
- `rgba(r, g, b, a)` where a ranged from 0 (transparent) - 1 (opaque - not letting light through).

**4. HEX - hexadecimal color**
- `#rrggbb` where rr, gg, bb ranged from 00 - ff
- e.g., #ff0000 is red.

**5. HSL - Hue, Saturation, and Lightnes**
- `hsla(hue, saturation, lightness, alpha)`
  - `hue` ranged from 0 - 360 deg where 0 is red, 120 is green, 240 is blue. 
  - `saturation` is percentage (%) where 0% is completely gray, while 100% is full color.
  - `lightness` is percentage (%) where 0% is dark, and 100% is full light.
  - alpha

## Types of UI Design Files

### Layout & UI Design Blueprint

- developers gains information about size, position, colors from UI design blueprint to complete the CSS Layout.

### What is Design Source Files?

- Not JPG, PNG, GIF format - they are just image format, to display the final result, not the design file.
- allows viewing all image layers, channels, guides, annotations, color modes, and other details.
- For the convenience of developers to control image and quickly get information.

### Types

- `.psd`: Photoshop
- `.sketch`:
- `.xd`: Adobe Xd (User experience design)
- `.fig`: Figma

> Frontend get information and slice images from UI source file provided by UI designer.

## Photoshop
- open `info` tab:
  - Window -> Info
- Quick Measurement of Distance:
    - use `move tool`.
    - select the item.
    - hold `ctrl` while moving your cursor to another item to measure the distance between them.
- Slice image
  - Edit -> Preferences -> General -> Plugins -> check `Enable Generator`
  - File -> Automate -> Generator Plugins -> check `Image Assets`
  - use `move tool` to select image.
  - go to `layers`, and click on the highlighted layer.
  - hide it to check if it is the one we want.
  - double click the name, and add `.png` to its back.
  - The image will be automated sliced and saved to the folder where your design file is located.
- Character Information
  - use `move tool` to select the text area.
  - on `Character` tab to view the info of font size, font weight, font family, line-height, letter spacing etc.