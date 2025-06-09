# CSS Fundamentals - Comprehensive Study Notes

## Table of Contents

1. [Anatomy of a Style Rule](#anatomy-of-a-style-rule)
2. [Media Queries](#media-queries)
3. [Selectors](#selectors)
4. [Pseudo-classes](#pseudo-classes)
5. [Pseudo-elements](#pseudo-elements)
6. [Combinators](#combinators)
7. [Color](#color)
8. [Units](#units)
9. [Typography](#typography)
10. [Debugging in the Browser](#debugging-in-the-browser)

---

## Anatomy of a Style Rule

Understanding CSS terminology is crucial for effective communication and learning.

### Basic Structure

```css
.error-text {
  color: red;
}
```

### Key Terms:

- **Selector**: `.error-text` - targets which elements to style
- **Declaration Block**: Everything within the curly braces `{}`
- **Declaration**: `color: red;` - a property-value pair
- **Property**: `color` - what aspect to style
- **Value**: `red` - how to style it

### Important Notes:

- Each declaration ends with a semicolon (`;`)
- Multiple declarations can exist within one rule
- Proper terminology helps in debugging and communication

---

## Media Queries

Media queries allow CSS to adapt to different screen sizes and devices, enabling responsive design.

### Basic Syntax

```css
@media (condition) {
  /* CSS that runs if condition is met */
}
```

### Practical Examples

#### Small Screen Styles

```css
@media (max-width: 300px) {
  .small-only {
    color: red;
  }
}
```

#### Hiding/Showing Content Based on Screen Size

```css
.large-screens {
  display: none;
}

@media (min-width: 300px) {
  .large-screens {
    display: block;
  }
  .small-screens {
    display: none;
  }
}
```

### Key Concepts:

- **max-width**: Applies styles up to a certain width
- **min-width**: Applies styles from a certain width and above
- **display: none**: Completely removes element from rendering
- **Media Features**: Not CSS properties, but query-specific features

### Common Use Cases:

- Navigation (desktop links vs mobile hamburger)
- Layout adjustments
- Typography scaling
- Image optimization

### Important Notes:

- Media queries use media features, not CSS properties
- `font-size: 32px` is NOT a valid media query condition
- Responsive design is essential in modern web development

---

## Selectors

Selectors determine which HTML elements receive styling.

### Basic Selectors

#### Element Selector

```css
/* Targets all anchor tags */
a {
  color: red;
}
```

#### Class Selector

```css
/* Targets elements with class="navigation-link" */
.navigation-link {
  text-decoration: none;
}
```

#### ID Selector

```css
/* Targets element with id="header" */
#header {
  background-color: blue;
}
```

### Modern Development Note:

In modern JS ecosystems, tooling often generates selectors automatically, but understanding selector fundamentals remains important for debugging and optimization.

---

## Pseudo-classes

Pseudo-classes target elements based on their current state, providing dynamic styling without JavaScript.

### Common Pseudo-classes

#### :hover

```css
button:hover {
  color: blue;
}
```

- Triggers when user hovers over element
- Similar to onMouseEnter/onMouseLeave in JavaScript but with built-in state management

#### :focus

```css
button:focus {
  border: 2px solid royalblue;
  background: royalblue;
  color: white;
}
```

**Focus Navigation:**

- **Desktop**: Click or Tab/Shift+Tab to navigate
- **MacOS Safari**: Use Option+Tab (clicking doesn't focus buttons)
- **MacOS Firefox**: Tab skips links, navigates buttons/form fields only

#### :checked

```css
input:checked {
  width: 24px;
  height: 24px;
}
```

- Applies to checked checkboxes and radio buttons
- Useful for custom form styling

### Accessibility Considerations:

- Focus styles are crucial for keyboard navigation
- Never remove focus outlines without providing alternatives
- Focus styles help users with disabilities navigate your site
- Consider visiting [a11y.coffee](https://a11y.coffee) for deeper accessibility knowledge

### Key Benefits:

- No JavaScript required for state-based styling
- Built-in browser support
- Better performance than JS event listeners
- Semantic and accessible by default

---

## Pseudo-elements

Pseudo-elements target "sub-elements" within an element or create virtual elements.

### Syntax

```css
/* Double colon (modern) */
element::pseudo-element

/* Single colon (legacy, still supported) */
element:pseudo-element
```

### Common Pseudo-elements

#### ::placeholder

```css
input {
  font-size: 1rem;
}
input::placeholder {
  color: goldenrod;
}
```

#### ::before and ::after

```css
p::before {
  content: "→ ";
  color: deeppink;
}

p::after {
  content: " ←";
  color: deeppink;
}
```

**Equivalent HTML Structure:**

```html
<p>
  <span class="pseudo-before">→ </span>
  This paragraph has little arrows!
  <span class="pseudo-after"> ←</span>
</p>
```

### Decorative Example

```css
p::before {
  content: "";
  display: block;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background-color: peachpuff;
  margin: 8px;
}
```

### Best Practices:

- **Avoid text content**: Screen readers may vocalize ::before/::after content inconsistently
- **Use for decoration**: Empty content strings for visual elements are acceptable
- **Modern alternatives**: Component-based architectures provide better content bundling
- **Accessibility**: Decorative elements are generally safe when using empty content

### Important Notes:

- `content` property is required for ::before/::after
- These are essentially "secret spans"
- No performance difference from actual HTML elements
- Consider accessibility implications when adding content

---

## Combinators

Combinators allow you to combine selectors to target elements based on their relationship to other elements.

### Descendant Selector (Space)

```css
/* Targets all <a> tags inside <nav> tags */
nav a {
  color: red;
  font-weight: bold;
}
```

**HTML Example:**

```html
<nav>
  <a href="">Home</a>
  <!-- Styled -->
  <ul>
    <li><a href="">Shop</a></li>
    <!-- Also styled (nested) -->
  </ul>
</nav>
<p>
  <a href="">Article link</a>
  <!-- Not styled -->
</p>
```

### Child Selector (>)

```css
/* Only direct children, not deeper descendants */
.main-list > li {
  border: 2px dotted;
}
```

**HTML Example:**

```html
<ul class="main-list">
  <li>Salt</li>
  <!-- Styled (direct child) -->
  <li>Pepper</li>
  <!-- Styled (direct child) -->
  <li>
    Fruits & Veg:
    <ul>
      <li>Apple</li>
      <!-- NOT styled (grandchild) -->
      <li>Banana</li>
      <!-- NOT styled (grandchild) -->
    </ul>
  </li>
  <!-- Styled (direct child) -->
</ul>
```

### Key Differences:

- **Descendant (space)**: Targets ANY nested element, regardless of depth
- **Child (>)**: Targets ONLY direct children, one level down

### Family Tree Analogy:

- **Child**: One level down (parent → child)
- **Descendant**: Any level down (parent → child → grandchild → great-grandchild...)

---

## Color

Color is fundamental to web design and CSS provides multiple ways to define and work with colors.

### Color Properties

#### Text Color

```css
strong {
  color: red;
}
```

#### Background Color

```css
em {
  background-color: hsl(50deg 100% 50%);
}
```

### Color Formats

#### HSL (Recommended)

```css
.colorful-thing {
  color: hsl(200deg 100% 50%);
  border-bottom: 3px solid hsl(100deg 75% 50%);
}
```

**HSL Parameters:**

- **Hue**: 0° to 360° (color wheel position)
- **Saturation**: 0% to 100% (color intensity)
- **Lightness**: 0% to 100% (brightness)

#### Why HSL is Better:

- More intuitive than hex codes
- Easy to create color variations
- Better for programmatic color manipulation
- Easier to maintain consistent color schemes

### Transparency (Alpha Channel)

```css
.box {
  background-color: hsl(340deg 100% 50% / 1); /* Fully opaque */
  background-color: hsl(340deg 100% 50% / 0.75); /* 75% opacity */
  background-color: hsl(340deg 100% 50% / 0.5); /* 50% opacity */
  background-color: hsl(340deg 100% 50% / 0.25); /* 25% opacity */
}
```

### Modern Syntax Note:

The slash (`/`) separates color values from opacity values. This syntax is part of the 2016 CSS Color specification and works in all modern browsers (not IE).

**Legacy syntax for IE support:**

```css
background-color: hsla(340, 100%, 50%, 0.75);
```

### Color Best Practices:

- Use HSL for better maintainability
- Consider accessibility (contrast ratios)
- Test colors with colorblind users in mind
- Use alpha transparency for overlays and layering effects

---

## Units

CSS units determine the size and spacing of elements. Choosing the right unit is crucial for responsive and accessible design.

### Pixels (px)

```css
.box {
  width: 1000px;
  margin-top: 32px;
  padding: 8px;
  font-size: 16px;
}
```

- **Pros**: Predictable, corresponds to screen pixels
- **Cons**: Not responsive to user preferences
- **Use for**: Most layout properties (margin, padding, border)

### Em Units

```css
p {
  font-size: 18px;
  padding-bottom: 2em; /* 2 × 18px = 36px */
  border: 1px solid;
}
```

**Relative to current element's font size:**

```css
p {
  font-size: 24px;
}

span {
  font-size: 0.8em; /* 0.8 × 24px = 19.2px */
}
```

**Limitations:**

- Can be unpredictable in nested components
- Changes when parent font-size changes
- Can create confusing cascading effects

### Rem Units (Recommended)

```css
html {
  font-size: 16px; /* Don't actually set this! */
}

h1 {
  font-size: 2rem; /* 2 × 16px = 32px */
  margin: 0;
}

h2 {
  font-size: 1.25rem; /* 1.25 × 16px = 20px */
  margin-bottom: 1.5rem;
}

p {
  font-size: 1rem; /* 1 × 16px = 16px */
}
```

**Benefits:**

- Consistent across the entire app
- Respects user's font size preferences
- Predictable behavior
- Accessible by default

**Changing base size (proper way):**

```css
html {
  font-size: 1.2em; /* 20% larger rem values app-wide */
}
```

### Percentages

```css
.box {
  width: 250px;
  height: 250px;
  background-color: pink;
}

.child {
  width: 50%; /* 50% of parent's width = 125px */
  height: 75%; /* 75% of parent's height = 187.5px */
  background-color: black;
}
```

### Unit Selection Guidelines

#### Typography

- **Use rem**: Better accessibility, respects user preferences
- **Avoid px for font-size**: Blocks user's ability to resize text

#### Box Model (padding, border, margin)

- **Use px**: More intuitive, no clear accessibility advantage
- **Use rem**: When you want spacing to scale with text size

#### Width/Height

- **Use px**: For fixed-size elements
- **Use %**: For relative/responsive sizing
- **Use rem**: When size should scale with root font size

#### Colors

- **Use HSL**: Most intuitive and maintainable

### Accessibility Note:

Pixels don't completely block accessibility, but rem units provide better support for users who change their default font size in browser settings.

---

## Typography

Typography is the foundation of web design. Remove text from a webpage, and it becomes unusable.

### Font Families

#### Web Safe Fonts

```css
p {
  font-family: Arial;
  /* or */
  font-family: sans-serif; /* Let OS choose */
  font-family: serif;
  font-family: monospace;
}
```

#### Custom Fonts (Google Fonts)

**HTML (in `<head>`):**

```html
<link rel="preconnect" href="https://fonts.gstatic.com" />
<link
  href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap"
  rel="stylesheet"
/>
```

**CSS:**

```css
font-family: "Roboto", sans-serif;
```

#### Font Stacks

```css
font-family: "Roboto", Arial, sans-serif;
```

- Browser uses first available font
- Fallbacks ensure text renders while custom font loads
- Always end with generic family (serif, sans-serif, monospace)

### Font Styles

#### Font Weight

```css
/* Keywords */
font-weight: normal; /* 400 */
font-weight: bold; /* 700 */

/* Numeric values (100-900) */
font-weight: 300; /* Light */
font-weight: 400; /* Normal */
font-weight: 700; /* Bold */
font-weight: 900; /* Extra Bold */
```

#### Font Style

```css
font-style: normal;
font-style: italic;
font-style: oblique; /* Rarely used */
```

#### Text Decoration

```css
/* Remove underlines from links */
a {
  text-decoration: none;
}

/* Add underlines */
.important {
  text-decoration: underline;
}
```

**Important**: Underlines on the web typically indicate links. Use sparingly for non-link elements to avoid confusion.

### Text Alignment

```css
p.left {
  text-align: left; /* Default */
}
p.right {
  text-align: right;
}
p.center {
  text-align: center;
}
p.justify {
  text-align: justify; /* Stretch to fill width */
}
```

**Internationalization Note**: Be cautious with alignment in RTL (right-to-left) languages like Arabic or Hebrew.

### Text Transforms

```css
text-transform: uppercase; /* MAKE ALL CAPS */
text-transform: lowercase; /* make all lowercase */
text-transform: capitalize; /* Capitalize Each Word */
text-transform: none; /* Remove any transformation */
```

**Best Practice**: Use CSS transforms instead of editing HTML to preserve original casing for future changes.

### Spacing

#### Letter Spacing

```css
h3 {
  letter-spacing: 3px; /* Increase space between characters */
  letter-spacing: -1px; /* Decrease space between characters */
  letter-spacing: normal; /* Default spacing */
}
```

#### Line Height

```css
p {
  line-height: 1.5; /* Unitless - recommended */
  line-height: 1.2; /* Tighter spacing */
  line-height: 2; /* Double spacing */
}

/* Avoid fixed units */
p {
  line-height: 20px; /* Don't do this - doesn't scale */
}
```

**Accessibility Requirements:**

- **Minimum line-height**: 1.5 for accessibility
- **Default browser values**: Chrome 1.15, Firefox 1.2 (both too low)
- **Why unitless**: Scales proportionally when user increases font size

#### Complete Typography Example

```css
h3 {
  letter-spacing: 3px;
  line-height: 2;

  /* Additional styling */
  font-size: 1.25rem;
  color: hsl(0deg 0% 30%);
  text-transform: uppercase;
  font-weight: 100;
}
```

### Typography Best Practices:

1. **Use rem for font-size**: Better accessibility
2. **Set generous line-height**: Minimum 1.5 for accessibility
3. **Choose appropriate font stacks**: Always include fallbacks
4. **Use HSL for colors**: More maintainable
5. **Consider internationalization**: Test with different languages
6. **Preserve original casing**: Use text-transform instead of editing HTML

### JSX Gotcha:

When using React/JSX, some CSS properties might have different naming conventions due to JavaScript reserved words. Always check the documentation for JSX-specific syntax.

---

## Debugging in the Browser

Effective browser debugging is essential for CSS development. Modern browser developer tools provide powerful capabilities for inspecting and modifying styles.

### Opening Developer Tools

#### Keyboard Shortcuts:

- **Mac**: `Command` + `Option` + `I`
- **Windows/Linux**: `Control` + `Shift` + `I`
- **Alternative**: Right-click → "Inspect Element"

### Key Debugging Features

#### Elements Panel

- **View HTML structure**: See the DOM as browser interprets it
- **Live editing**: Modify HTML and CSS in real-time
- **Style inspection**: See all applied styles and their sources

#### Styles Panel

- **Computed styles**: Final calculated values
- **Cascade visualization**: See which styles are overridden
- **Box model**: Visual representation of padding, border, margin
- **Source mapping**: Trace styles back to original files

#### Console

- **Error messages**: CSS parsing errors and warnings
- **Style debugging**: Test selectors and properties
- **Performance insights**: Identify rendering bottlenecks

### Essential Debugging Techniques

#### Inspecting Specific Elements

1. Right-click on element → "Inspect"
2. Use element picker tool
3. Search by selector in Elements panel

#### Understanding the Cascade

- **Strikethrough styles**: Overridden by more specific rules
- **Inheritance**: See inherited vs. directly applied styles
- **Specificity**: Understand why certain styles take precedence

#### Live Editing

- **Double-click property values**: Edit in place
- **Add new properties**: Click in empty space in styles panel
- **Toggle properties**: Use checkboxes to enable/disable

#### Box Model Visualization

- **Hover over elements**: See box model overlay
- **Box model diagram**: In computed styles panel
- **Margin/padding inspection**: Click on box model values to edit

### Pro Tips:

1. **Use computed styles**: To see final calculated values
2. **Check for typos**: Misspelled properties show as crossed out
3. **Verify selectors**: Make sure your selectors actually target intended elements
4. **Test responsive design**: Use device toolbar for mobile testing
5. **Performance profiling**: Use Lighthouse for optimization suggestions

### Common Issues to Look For:

- **Selector specificity conflicts**: More specific selectors override general ones
- **Typos in property names**: Invalid properties are ignored
- **Unit mistakes**: Missing units or wrong unit types
- **Inheritance problems**: Understanding what inherits and what doesn't
- **Box model conflicts**: Margin collapse, overflow issues

### Workflow Recommendation:

1. **Inspect element** to understand current state
2. **Check applied styles** to see what's working
3. **Look for overrides** (strikethrough styles)
4. **Test changes live** in browser
5. **Copy working changes** back to your code
6. **Validate** that changes work across different browsers/devices

---

## Summary

This comprehensive guide covers the fundamental concepts of CSS that form the foundation for advanced styling techniques:

- **Style Rules**: Understanding selectors, properties, and values
- **Media Queries**: Creating responsive designs for different devices
- **Selectors & Combinators**: Targeting specific elements efficiently
- **Pseudo-classes & Pseudo-elements**: Adding interactivity and virtual elements
- **Color**: Using HSL for maintainable color schemes
- **Units**: Choosing between px, em, rem, and percentages appropriately
- **Typography**: Creating readable, accessible text styling
- **Debugging**: Using browser tools effectively for development

### Key Takeaways:

1. **Accessibility first**: Use rem for fonts, maintain good contrast, ensure adequate line-height
2. **Responsive design**: Use media queries and relative units
3. **Maintainability**: Prefer HSL colors and semantic selectors
4. **Performance**: Understand the cascade and specificity
5. **Modern practices**: Use CSS for styling states rather than JavaScript when possible

### Next Steps:

- Practice with real projects
- Explore CSS Grid and Flexbox
- Learn about CSS animations and transitions
- Study advanced selectors and functions
- Implement design systems and methodologies
