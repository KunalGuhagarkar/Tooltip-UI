# Tooltip UI

A navigation tooltip built with **only HTML and CSS**, no JavaScript. When you hover over a navigation item, a pointer arrow glides to that item beneath a tooltip box.

## Overview

This project is based on the [Tooltip UI project on roadmap.sh](https://roadmap.sh/projects/tooltip-ui).

This project practises CSS positioning, hover effects, and smooth transitions to create dynamic UI behaviour without scripting. The tooltip sits above the navigation bar, and a triangular pointer animates to whichever item is hovered (Home, Projects, or Blog).

## Features

- Pure HTML and CSS, with zero JavaScript
- Pointer arrow slides horizontally to the hovered nav item
- Fade-in and slide animation using `opacity` and `transform` transitions
- Clean, minimal black-and-white design
- Flexbox layout for easy centring and alignment

## Project Structure

```
.
├── index.html   # Markup: tooltip box, pointer arrow (SVG), nav items
├── style.css    # Layout, styling, hover effects, and transitions
└── README.md
```

## Getting Started

1. Clone or download this repository.
2. Make sure `index.html` and `style.css` are in the same folder.
3. Open `index.html` in your browser.

No build step or dependencies are required.

## How It Works

### Structure

The page is a vertical flex column with three parts:

1. **Tooltip box** (`.tooltip-container`): a black rounded box with the tooltip text.
2. **Pointer arrow** (`<svg>`): a small triangle that points down at the nav.
3. **Navigation bar** (`.nav-container`): the items *Home*, *Projects*, and *Blog*, separated by dots.

### The core trick: `:has()` with the sibling combinator

The arrow comes right before `.nav-container` in the HTML. This lets CSS detect which nav item is hovered by selecting the arrow based on its sibling's state:

```css
svg:has(+ .nav-container > p:nth-of-type(1):hover) {
    opacity: 1;
    transform: translateX(-100px) translateY(-5px);
}
```

Read it as: *"Select the `svg` that is immediately followed by `.nav-container` which contains a first `<p>` currently being hovered."*

| Hovered item | `nth-of-type` | Arrow offset         |
| ------------ | ------------- | -------------------- |
| Home         | 1             | `translateX(-100px)` |
| Projects     | 3             | `translateX(0)`      |
| Blog         | 5             | `translateX(100px)`  |

The dots (`.`) at positions 2 and 4 are also `<p>` elements, which is why the nav items use odd `nth-of-type` values.

### Animation

By default the arrow is hidden (`opacity: 0`) and nudged slightly upward. On hover, it fades in and moves to the correct position, with `transition` properties making the movement smooth.

## Browser Support

This project relies on the CSS `:has()` selector, which is supported in all modern browsers (Chrome/Edge 105+, Safari 15.4+, Firefox 121+). Older browsers will not show the arrow animation.

## Possible Improvements

- Hide the tooltip box until hover, so it also fades or slides in
- Show a different tooltip message for each nav item
- Add alternative animations: scale-in, slide-up, or bounce
- Make the arrow position responsive using percentages instead of fixed pixel offsets
- Add `cursor: pointer` and focus styles (`:focus-visible`) for keyboard accessibility
- Convert nav items to `<a>` elements inside a `<nav>` for better semantics

## What I Learned

- Positioning elements relative to one another with Flexbox and `transform`
- Creating smooth hover transitions with CSS only
- Using the `:has()` selector to style an element based on a sibling's state
- Building interactive UI without JavaScript

## Author

**Kunal Guhagarkar**