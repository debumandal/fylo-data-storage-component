# Frontend Mentor - Fylo data storage component solution

This is a solution to the [Fylo data storage component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/fylo-data-storage-component-1dZPRbV5n). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [Challenges Faced & How I Solved Them](#challenges-faced--how-i-solved-them)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the site depending on their device's screen size

### Screenshot

![Fylo Data Storage Component Preview](./preview.jpg)

### Links

- Solution URL: [Solution URL]()

- Live Site URL: [Live site URL]()

## My process

### Built with

- Semantic HTML5

- CSS Custom Properties

- Flexbox

- Mobile-first workflow

- CSS pseudo-elements

- CSS border triangle technique

- ARIA attributes for accessibility

---

### Challenges Faced & How I Solved Them

During the development of this component, I ran into several distinct CSS layout and styling hurdles:

#### 1. Space Distribution Between `0 GB` and `1000 GB`

- **Problem:** I wrapped both values in `<span>` tags inside `<p class="range">` and added `display: flex; justify-content: space-between;`, but the two labels refused to separate and stayed clustered together in the center.
- **Root Cause:** The parent card had `align-items: center`, which caused child elements without explicit widths to shrink-wrap tightly around their inner content. Because the paragraph container had no available space left over, `justify-content: space-between` had nothing to distribute.
- **Solution:** I gave `width: 100%` to both the `.data-range` wrapper and the `.range` paragraph while harmonizing their `max-width` with the parent progress bar. This allowed the container to stretch across the card, giving Flexbox the room needed to push each span to opposite ends.

#### 2. Desktop Background Image & Horizon Split

- **Problem:** The desktop mockup required the top half of the screen to show a dark blue background color, while the bottom half featured the wavy graphic spanning full width. Initially, using multiple position coordinates and `background-size: 50% 100%` distorted and squished the artwork.
- **Solution:** I anchored the desktop background image cleanly using `background-position: bottom;` and sized it with `background-size: 100% 50%;` alongside `background-repeat: no-repeat;`. Because the graphic has a transparent top area, pinning it to the bottom allowed the deep `background-color: var(--clr-neutral-blue-950)` on `body` to show through on the top half, perfectly producing the two-tone horizon divide.

#### 3. Creating the "185 GB Left" Speech Bubble Triangle Pointer

- **Problem:** Creating the speech-bubble pointer under the floating badge using a rotated square (`transform: rotate(45deg)`) resulted in an awkward diamond notch sticking out from the side instead of a clean, right-angled triangle pointing straight down. Additionally, my pseudo-element initially failed to show up at all.
- **Solution:**
  1. I learned that pseudo-elements (`::before` / `::after`) require `content: ""` and `position: absolute` to render.
  2. To get a sharp, right-angled wedge flush with the right edge, I switched to the classic **CSS Border Technique**: setting `width: 0`, `height: 0`, a solid `border-top`, a transparent `border-left`, and no background color. This produced the exact speech bubble tail from the design.

#### 4. Card Baseline Alignment & Viewport Centering

- **Problem:** On desktop, setting `min-height: 56.2rem` on `.container` and `align-items: end` caused the entire component to be pulled toward the very bottom of the screen instead of floating gracefully in the center.
- **Solution:** I moved vertical viewport centering to the `body` (`min-height: 100dvh; display: flex; justify-content: center; align-items: center;`) and set `.container` to `align-items: flex-end;` with a fixed `min-height: 17rem`, so both cards share the same bottom edge while the whole module stays centered on the page.

---

### What I learned

This project provided deep practical practice with responsive layout transitions, accessibility best practices, and CSS visual tricks:

```html
<!-- Semantic & Accessible Buttons -->
<button type="button" aria-label="Upload document" class="btn doc-type">
  <img src="./images/icon-document.svg" alt="" />
</button>
```

```css
/* Precise CSS Border Triangle for Speech Bubble Pointer */
.data-remaining::after {
  content: "";
  position: absolute;
  width: 0;
  height: 0;
  border-top: 1.5rem solid var(--clr-neutral-blue-200);
  border-left: 1.5rem solid transparent;
  right: 0;
  bottom: -1.45rem;
}

/* Horizontal Centering with Transform */
.data-remaining {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
```

Key takeaways:

- **ARIA vs Alt Attributes:** When using icon-only buttons, providing an explicit `aria-label` on the `<button>` and leaving `alt=""` on the decorative `<img>` prevents screen readers from redundantly announcing both the button and image names.

- **Flexbox Shrink-Wrapping:** Remember that flex children shrink-wrap by default when their cross-axis alignment is centered; explicit widths (`width: 100%`) are often necessary for `justify-content: space-between` to take effect.

- **Pseudo-Elements Requirements:** A pseudo-element must always define `content: ""` to exist in the DOM.

### Continued development

In future projects, I plan to continue refining:

- Fluid typography and spacing using CSS `clamp()`.

- Complex multi-layered CSS background combinations.

- Building custom accessible components without relying on external libraries.

### Useful resources

- [MDN Web Docs - ARIA: button role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/button_role) - Essential for understanding keyboard accessibility and labeling icon buttons.

- [CSS-Tricks: The Shapes of CSS](https://css-tricks.com/the-shapes-of-css/) - A helpful refresher on how transparent borders create pure CSS geometric shapes and triangles.

## Author

- Frontend Mentor - [@Debumandal]()

- GitHub - [@Debumandal]()
