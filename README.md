# Assignment-2: CSS

This repository contains my implementation of **Assignment-2: CSS**.

The main purpose of this assignment was not only to write CSS, but to
understand the different ways CSS can be applied, how a page can be
designed using Flexbox, how CSS custom properties work, and how a theme
switcher can be implemented using CSS only.

The assignment was completed in stages so that each part could be
understood and tested separately.

------------------------------------------------------------------------

## Assignment Requirements

### Part-I --- Week 1

1.  Use **external, internal and inline CSS** to format different
    paragraphs about yourself.
2.  Recreate a **Page Setup** window similar to a word processor and
    provide a theme selector.

### Part-II --- Week 2

Use a theme selector for the problem given in Assignment-1.

### Bonus Assignment

Make the Page Setup theme selector actually work using **CSS only**,
without JavaScript.

The bonus requires:

-   At least three themes.
-   Theme selection using radio buttons.
-   `:checked` pseudo-class.
-   Sibling combinator (`~` or `+`).
-   CSS custom properties (variables).
-   Smooth transitions.
-   Responsive design using Flexbox/Grid and at least one media query.

------------------------------------------------------------------------

# Project Structure

``` text
Assignment-2/
│
├── q1.html
├── style.css
│
├── q2.html
├── q2.css
│
└── README.md
```

------------------------------------------------------------------------

# Part-I --- Question 1

## Objective

Demonstrate the three ways of applying CSS:

1.  Inline CSS
2.  Internal CSS
3.  External CSS

Each paragraph is intentionally formatted differently so that the
difference can be seen visually.

------------------------------------------------------------------------

## Step 1 --- Create the HTML file

Create:

``` text
q1.html
```

The page contains three paragraphs. The first uses inline CSS, the
second uses internal CSS, and the third uses external CSS.

The external stylesheet is connected using:

``` html
<link rel="stylesheet" href="style.css">
```

------------------------------------------------------------------------

## Step 2 --- Create the external CSS file

Create:

``` text
style.css
```

The third paragraph is styled from this file.

Example:

``` css
.paragraph-three {
    background-color: #fff3e0;
    color: #e65100;
    text-align: right;
    font-family: "Trebuchet MS", sans-serif;
    font-size: 17px;

    padding: 18px;
    margin: 20px 0;
    border: 2px solid #ffb74d;
    border-radius: 10px;
}
```

------------------------------------------------------------------------

## Understanding the Three CSS Methods

### 1. Inline CSS

CSS is written directly inside the HTML element:

``` html
<p style="color: blue; font-size: 20px;">
```

This affects that particular element.

### 2. Internal CSS

CSS is written inside a `<style>` element:

``` html
<style>
    .paragraph-two {
        color: green;
    }
</style>
```

It is inside the HTML file but separate from the HTML element itself.

### 3. External CSS

CSS is written in a separate `.css` file:

``` css
.paragraph-three {
    color: orange;
}
```

The HTML connects to it using:

``` html
<link rel="stylesheet" href="style.css">
```

------------------------------------------------------------------------

## CSS Properties Used

The assignment specifically asks for properties such as:

``` css
background-color
color
text-align
font-family
font-size
```

Additional properties were used to improve visual appearance:

``` css
padding
margin
border
border-radius
```

### `padding`

Creates space inside the element.

### `margin`

Creates space outside the element.

### `border`

Creates a visible boundary around the element.

### `border-radius`

Rounds the corners of the element.

------------------------------------------------------------------------

# Part-I --- Question 2

## Objective

Create a Page Setup window similar to a word processor.

The interface contains:

-   Theme selector
-   Page Setup title
-   Close button
-   Orientation
-   Portrait/Landscape radio buttons
-   Paper Size dropdown
-   Page Colour selector
-   Top/Bottom/Left/Right margin inputs
-   OK button
-   Cancel button
-   Set as default button

------------------------------------------------------------------------

# Step 1 --- Build the HTML Structure

Create:

``` text
q2.html
```

The page is divided into logical sections:

``` text
body
│
├── Theme radio buttons
│
├── Theme selector
│
└── Page Setup
    │
    ├── Header
    │
    ├── Main Content
    │   ├── Left section
    │   │   ├── Orientation
    │   │   ├── Paper Size
    │   │   └── Page Colour
    │   │
    │   └── Right section
    │       └── Margins
    │
    └── Footer
        ├── OK
        ├── Cancel
        └── Set as default
```

The theme radio buttons are placed before the Page Setup window because
the CSS-only theme mechanism uses the sibling combinator.

------------------------------------------------------------------------

# Step 2 --- Radio Buttons and `name`

For the theme selector:

``` html
<input type="radio" id="light" name="theme" checked>
<input type="radio" id="dark" name="theme">
<input type="radio" id="contrast" name="theme">
```

`type="radio"` makes the input a radio button.

The same:

``` html
name="theme"
```

puts all three radio buttons into the same group.

Therefore only one theme can be selected at a time.

The `checked` attribute selects the initial theme:

``` html
<input type="radio" id="light" name="theme" checked>
```

------------------------------------------------------------------------

# Step 3 --- Page Setup Layout Using Flexbox

The main content contains two sections:

``` html
<div class="left-section">
    ...
</div>

<div class="right-section">
    ...
</div>
```

The parent uses:

``` css
.window-content {
    display: flex;
}
```

This places the two sections beside each other.

Both sections use:

``` css
.left-section,
.right-section {
    flex: 1;
}
```

This gives them equal available space.

The gap between them is controlled with:

``` css
gap: 40px;
```

------------------------------------------------------------------------

# Step 4 --- CSS Custom Properties

Instead of writing different colour rules repeatedly for every theme,
CSS variables are used.

Example:

``` css
.page-setup {
    --bg: #ffffff;
    --fg: #212529;
    --border: #dee2e6;

    --accent-ok: #2563eb;
    --accent-cancel: #dc3545;
    --accent-default: #198754;
}
```

The variables are then used with:

``` css
background-color: var(--bg);
color: var(--fg);
border-color: var(--border);
```

This makes changing the theme easier.

------------------------------------------------------------------------

# Step 5 --- CSS-only Theme Switching

The theme selector does not use JavaScript.

The mechanism is:

``` text
User selects radio button
        ↓
Radio button becomes :checked
        ↓
:checked selector becomes active
        ↓
Sibling combinator (~) finds Page Setup
        ↓
CSS custom properties are changed
        ↓
The Page Setup window changes theme
```

For example:

``` css
#dark:checked ~ .page-setup {
    --bg: #222831;
    --fg: #eeeeee;
    --border: #555555;

    --accent-ok: #00adb5;
    --accent-cancel: #ff6b6b;
    --accent-default: #4caf50;
}
```

For the high-contrast theme:

``` css
#contrast:checked ~ .page-setup {
    --bg: #000000;
    --fg: #ffffff;
    --border: #ffffff;

    --accent-ok: #ffff00;
    --accent-cancel: #ff0000;
    --accent-default: #00ff00;
}
```

The Light theme acts as the default theme.

------------------------------------------------------------------------

# Why Does `~` Work?

The HTML structure is intentionally arranged like this:

``` text
body
│
├── #light
├── #dark
├── #contrast
├── .theme-selector
└── .page-setup
```

Therefore:

``` css
#dark:checked ~ .page-setup
```

means:

> If `#dark` is checked, select the later sibling `.page-setup`.

The `~` combinator cannot select a parent.

For example, this does **not** work:

``` css
#dark:checked ~ body
```

because `body` is the parent of `#dark`, not its sibling.

------------------------------------------------------------------------

# Step 6 --- Hiding the Theme Radio Buttons

The actual theme radio inputs are hidden:

``` css
input[name="theme"] {
    display: none;
}
```

The labels are connected to them using `for`:

``` html
<label for="dark">Dark</label>
```

and:

``` html
<input type="radio" id="dark" name="theme">
```

Therefore clicking the visible "Dark" label still selects the hidden
radio button.

------------------------------------------------------------------------

# Step 7 --- Smooth Theme Transition

The assignment requires the theme change to happen smoothly.

Transitions were added:

``` css
transition:
    background-color 0.3s ease,
    color 0.3s ease,
    border-color 0.3s ease;
```

Instead of changing immediately, the colours fade into the new theme.

------------------------------------------------------------------------

# Step 8 --- Responsive Design

The Page Setup window initially uses:

``` css
.page-setup {
    width: 700px;
}
```

This works well on a desktop but may be too wide for a small screen.

Therefore a media query is used:

``` css
@media (max-width: 750px) {

    .page-setup {
        width: 90%;
    }

    .window-content {
        flex-direction: column;
        gap: 25px;
    }
}
```

When the screen width becomes 750px or less:

-   The Page Setup window becomes 90% of the available width.
-   The left and right sections are stacked vertically.
-   The layout becomes easier to use on smaller screens.

A second media query handles very small screens:

``` css
@media (max-width: 500px) {

    .window-header {
        padding: 15px 18px;
        font-size: 18px;
    }

    .window-content {
        padding: 18px;
    }

    .window-footer {
        padding: 14px 18px;
        flex-direction: column;
        gap: 12px;
    }

    input[type="number"] {
        width: 90px;
    }
}
```

------------------------------------------------------------------------

# How to Run the Assignment on Another Laptop

No special framework or package installation is required.

## Requirements

A modern web browser such as:

-   Google Chrome
-   Microsoft Edge
-   Mozilla Firefox

A code editor is recommended, such as Visual Studio Code.

------------------------------------------------------------------------

## Step 1 --- Download or Clone the Repository

Using Git:

``` bash
git clone <repository-url>
```

Then open the downloaded folder.

Alternatively, download the repository as a ZIP from GitHub and extract
it.

------------------------------------------------------------------------

## Step 2 --- Open the Project

Open the project folder in VS Code.

The structure should look similar to:

``` text
Assignment-2/
│
├── q1.html
├── style.css
├── q2.html
├── q2.css
└── README.md
```

------------------------------------------------------------------------

## Step 3 --- Run Question 1

Open:

``` text
q1.html
```

in a browser.

You should see three differently formatted paragraphs demonstrating:

-   Inline CSS
-   Internal CSS
-   External CSS

Make sure `style.css` is in the correct location because `q1.html`
contains:

``` html
<link rel="stylesheet" href="style.css">
```

------------------------------------------------------------------------

## Step 4 --- Run Question 2

Open:

``` text
q2.html
```

in a browser.

Make sure `q2.css` is in the same folder because the HTML contains:

``` html
<link rel="stylesheet" href="q2.css">
```

------------------------------------------------------------------------

# Testing the Theme Selector

Open `q2.html` and try:

``` text
Light
Dark
High Contrast
```

The Page Setup window should change according to the selected theme.

### Light

-   White background
-   Dark text
-   Light borders
-   Coloured action buttons

### Dark

-   Dark background
-   Light text
-   Dark borders
-   Different accent colours

### High Contrast

-   Black background
-   White text
-   White borders
-   Bright accent colours

The theme changes without JavaScript.

------------------------------------------------------------------------

# Testing Responsive Design

In Chrome:

1.  Open `q2.html`.
2.  Press `F12`.
3.  Click the **Toggle Device Toolbar** icon.
4.  Resize the viewport or select a mobile device.

Test different widths.

At approximately:

``` text
750px
```

the two main sections should stack vertically.

At:

``` text
500px
```

the footer and spacing are further adjusted for small screens.

------------------------------------------------------------------------

# Important Concepts Learned

## CSS Basics

-   Inline CSS
-   Internal CSS
-   External CSS
-   Classes
-   CSS selectors
-   CSS properties
-   Margins
-   Padding
-   Borders
-   Border radius

## Layout

-   Flexbox
-   `display: flex`
-   `flex-direction`
-   `flex: 1`
-   `gap`
-   `justify-content`
-   `align-items`
-   `flex-wrap`

## Form Elements

-   Radio buttons
-   `name`
-   `checked`
-   `label`
-   `for`
-   `select`
-   `option`
-   `input type="number"`
-   `input type="color"`

## Advanced CSS

-   CSS custom properties
-   `var()`
-   `:checked`
-   Sibling combinator `~`
-   Child combinator `>`
-   `transition`
-   Media queries
-   Responsive design

------------------------------------------------------------------------

# Final Takeaways

### 1. Three ways to apply CSS

``` text
Inline
    ↓
style="..."

Internal
    ↓
<style>...</style>

External
    ↓
style.css
```

### 2. Flexbox controls layout

``` css
display: flex;
```

allows child elements to be arranged efficiently.

Changing:

``` css
flex-direction: row;
```

to:

``` css
flex-direction: column;
```

allows the layout to adapt to smaller screens.

### 3. CSS variables make themes easier

Instead of changing every colour individually:

``` css
background-color: var(--bg);
color: var(--fg);
border-color: var(--border);
```

the theme only needs to change the variables.

### 4. `:checked` can be used without JavaScript

A radio button can become a CSS state:

``` css
#dark:checked
```

and that state can activate another CSS rule.

### 5. `~` works between siblings

``` css
#dark:checked ~ .page-setup
```

works because both elements are children of the same parent and
`.page-setup` comes after `#dark`.

It cannot be used to select a parent.

### 6. Media queries make the page responsive

``` css
@media (max-width: 750px) {
    ...
}
```

allows different CSS rules to be applied depending on screen width.

------------------------------------------------------------------------

# Final Result

The completed work demonstrates:

-   Different CSS application methods.
-   A styled Page Setup interface.
-   HTML form controls.
-   Flexbox-based layout.
-   Three selectable themes.
-   CSS-only theme switching.
-   CSS custom properties.
-   Smooth transitions.
-   Responsive behaviour on smaller screens.

No JavaScript is required for the CSS-only theme switching
implementation.
