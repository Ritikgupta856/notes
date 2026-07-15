# HTML CSS & Tailwind — Interview Preparation Guide

## Table of Contents

1. [HTML Interview Questions](#html-interview-questions)
2. [1. What is HTML?](#1-what-is-html)
3. [2. Why is HTML important?](#2-why-is-html-important)
4. [3. What is the difference between HTML and HTML5?](#3-what-is-the-difference-between-html-and-html5)
5. [4. What are semantic elements in HTML?](#4-what-are-semantic-elements-in-html)
6. [5. Why should we use semantic HTML?](#5-why-should-we-use-semantic-html)
7. [6. What is the difference between block and inline elements?](#6-what-is-the-difference-between-block-and-inline-elements)
8. [7. What is the difference between div and span?](#7-what-is-the-difference-between-div-and-span)
9. [8. What is the purpose of the alt attribute in images?](#8-what-is-the-purpose-of-the-alt-attribute-in-images)
10. [9. What is the difference between id and class?](#9-what-is-the-difference-between-id-and-class)
11. [10. What are data-* attributes?](#10-what-are-data-attributes)
12. [11. What is the purpose of the meta tag?](#11-what-is-the-purpose-of-the-meta-tag)
13. [12. Why is the viewport meta tag used?](#12-why-is-the-viewport-meta-tag-used)
14. [13. What is the difference between strong and b tags?](#13-what-is-the-difference-between-strong-and-b-tags)
15. [14. What is the difference between em and i tags?](#14-what-is-the-difference-between-em-and-i-tags)
16. [15. What is the purpose of the doctype declaration?](#15-what-is-the-purpose-of-the-doctype-declaration)
17. [16. What are self-closing tags?](#16-what-are-self-closing-tags)
18. [17. What is the difference between section and article?](#17-what-is-the-difference-between-section-and-article)
19. [18. What is the difference between header, head, and heading?](#18-what-is-the-difference-between-header-head-and-heading)
20. [19. What is the difference between ol, ul, and dl?](#19-what-is-the-difference-between-ol-ul-and-dl)
21. [20. What is accessibility in HTML?](#20-what-is-accessibility-in-html)
22. [21. How do labels improve form accessibility?](#21-how-do-labels-improve-form-accessibility)
23. [22. What is the difference between button and input type="button"?](#22-what-is-the-difference-between-button-and-input-typebutton)
24. [23. What are the different input types in HTML5?](#23-what-are-the-different-input-types-in-html5)
25. [24. What is the difference between localStorage, sessionStorage, and cookies?](#24-what-is-the-difference-between-localstorage-sessionstorage-and-cookies)
26. [25. What is iframe?](#25-what-is-iframe)
27. [26. What are the new features of HTML5?](#26-what-are-the-new-features-of-html5)
28. [27. What is the purpose of the preload attribute?](#27-what-is-the-purpose-of-the-preload-attribute)
29. [28. What is the difference between async and defer in script tags?](#28-what-is-the-difference-between-async-and-defer-in-script-tags)
30. [29. How do you improve SEO with HTML?](#29-how-do-you-improve-seo-with-html)
31. [30. What is CSS?](#30-what-is-css)
32. [31. Why is CSS called cascading?](#31-why-is-css-called-cascading)
33. [32. What is specificity in CSS?](#32-what-is-specificity-in-css)
34. [33. Inline vs internal vs external CSS?](#33-inline-vs-internal-vs-external-css)
35. [34. What is the box model?](#34-what-is-the-box-model)
36. [35. What is the difference between content-box and border-box?](#35-what-is-the-difference-between-content-box-and-border-box)
37. [36. What is the difference between margin and padding?](#36-what-is-the-difference-between-margin-and-padding)
38. [37. What is margin collapsing?](#37-what-is-margin-collapsing)
39. [38. What is display property?](#38-what-is-display-property)
40. [39. Difference between block, inline, and inline-block?](#39-difference-between-block-inline-and-inline-block)
41. [40. What is position property in CSS?](#40-what-is-position-property-in-css)
42. [41. Difference between relative, absolute, fixed, and sticky?](#41-difference-between-relative-absolute-fixed-and-sticky)
43. [42. What is z-index?](#42-what-is-z-index)
44. [43. What is overflow property?](#43-what-is-overflow-property)
45. [44. What is opacity?](#44-what-is-opacity)
46. [45. What is the difference between visibility hidden and display none?](#45-what-is-the-difference-between-visibility-hidden-and-display-none)
47. [46. What is Flexbox?](#46-what-is-flexbox)
48. [47. What is CSS Grid?](#47-what-is-css-grid)
49. [48. Flexbox vs Grid?](#48-flexbox-vs-grid)
50. [49. What is justify-content?](#49-what-is-justify-content)
51. [50. What is align-items?](#50-what-is-align-items)
52. [51. What is align-self?](#51-what-is-align-self)
53. [52. What is gap in CSS?](#52-what-is-gap-in-css)
54. [53. What are pseudo-classes?](#53-what-are-pseudo-classes)
55. [54. What are pseudo-elements?](#54-what-are-pseudo-elements)
56. [55. What is the difference between pseudo-class and pseudo-element?](#55-what-is-the-difference-between-pseudo-class-and-pseudo-element)
57. [56. What is responsive design?](#56-what-is-responsive-design)
58. [57. What are media queries?](#57-what-are-media-queries)
59. [58. Mobile-first vs desktop-first?](#58-mobile-first-vs-desktop-first)
60. [59. What are CSS units?](#59-what-are-css-units)
61. [60. em vs rem?](#60-em-vs-rem)
62. [61. px vs % vs vw/vh?](#61-px-vs-vs-vwvh)
63. [62. What is transition in CSS?](#62-what-is-transition-in-css)
64. [63. What is transform?](#63-what-is-transform)
65. [64. What is animation in CSS?](#64-what-is-animation-in-css)
66. [65. What is keyframes?](#65-what-is-keyframes)
67. [66. What is the difference between transition and animation?](#66-what-is-the-difference-between-transition-and-animation)
68. [67. What is inherit, initial, unset, and revert?](#67-what-is-inherit-initial-unset-and-revert)
69. [68. What is CSS variable?](#68-what-is-css-variable)
70. [69. Why use CSS variables?](#69-why-use-css-variables)
71. [70. What is BEM?](#70-what-is-bem)
72. [71. What is the difference between absolute and relative units?](#71-what-is-the-difference-between-absolute-and-relative-units)
73. [72. How do you center a div?](#72-how-do-you-center-a-div)
74. [73. What is min-width, max-width, min-height, max-height?](#73-what-is-min-width-max-width-min-height-max-height)
75. [74. What is object-fit?](#74-what-is-object-fit)
76. [75. What is background-size cover vs contain?](#75-what-is-background-size-cover-vs-contain)
77. [76. What are combinators in CSS?](#76-what-are-combinators-in-css)
78. [77. What is !important?](#77-what-is-important)
79. [78. How do you optimize CSS performance?](#78-how-do-you-optimize-css-performance)
80. [79. What is Tailwind CSS?](#79-what-is-tailwind-css)
81. [80. Why use Tailwind CSS?](#80-why-use-tailwind-css)
82. [81. What does utility-first mean?](#81-what-does-utility-first-mean)
83. [82. Tailwind vs traditional CSS?](#82-tailwind-vs-traditional-css)
84. [83. What are the advantages of Tailwind?](#83-what-are-the-advantages-of-tailwind)
85. [84. What are the disadvantages of Tailwind?](#84-what-are-the-disadvantages-of-tailwind)
86. [85. How does Tailwind work internally?](#85-how-does-tailwind-work-internally)
87. [86. What is Tailwind config file?](#86-what-is-tailwind-config-file)
88. [87. How do responsive classes work in Tailwind?](#87-how-do-responsive-classes-work-in-tailwind)
89. [88. How do hover, focus, and active states work in Tailwind?](#88-how-do-hover-focus-and-active-states-work-in-tailwind)
90. [89. How do dark mode classes work in Tailwind?](#89-how-do-dark-mode-classes-work-in-tailwind)
91. [90. What is the difference between container and mx-auto?](#90-what-is-the-difference-between-container-and-mx-auto)
92. [91. How do spacing utilities work in Tailwind?](#91-how-do-spacing-utilities-work-in-tailwind)
93. [92. How do color utilities work in Tailwind?](#92-how-do-color-utilities-work-in-tailwind)
94. [93. What is arbitrary value in Tailwind?](#93-what-is-arbitrary-value-in-tailwind)
95. [94. What is @apply in Tailwind?](#94-what-is-apply-in-tailwind)
96. [95. What are Tailwind plugins?](#95-what-are-tailwind-plugins)
97. [96. How do you customize Tailwind theme?](#96-how-do-you-customize-tailwind-theme)
98. [97. Tailwind with React — any benefit?](#97-tailwind-with-react-any-benefit)
99. [98. How do you manage long class names in Tailwind?](#98-how-do-you-manage-long-class-names-in-tailwind)
100. [99. What is clsx or classnames used for with Tailwind?](#99-what-is-clsx-or-classnames-used-for-with-tailwind)
101. [100. What is Tailwind Preflight?](#100-what-is-tailwind-preflight)
102. [101. How is Tailwind different from CSS Modules?](#101-how-is-tailwind-different-from-css-modules)
103. [102. How do you create responsive layouts in Tailwind?](#102-how-do-you-create-responsive-layouts-in-tailwind)
104. [103. How do flex and grid work in Tailwind?](#103-how-do-flex-and-grid-work-in-tailwind)
105. [104. What is the difference between hidden and invisible in Tailwind?](#104-what-is-the-difference-between-hidden-and-invisible-in-tailwind)
106. [105. How do transitions and animations work in Tailwind?](#105-how-do-transitions-and-animations-work-in-tailwind)
107. [106. What is the difference between space-x and gap?](#106-what-is-the-difference-between-space-x-and-gap)
108. [107. How do you make Tailwind code maintainable?](#107-how-do-you-make-tailwind-code-maintainable)
109. [div vs span](#div-vs-span)
110. [id vs class](#id-vs-class)
111. [HTML vs HTML5](#html-vs-html5)
112. [block vs inline vs inline-block](#block-vs-inline-vs-inline-block)
113. [margin vs padding](#margin-vs-padding)
114. [relative vs absolute vs fixed vs sticky](#relative-vs-absolute-vs-fixed-vs-sticky)
115. [Flexbox vs Grid](#flexbox-vs-grid)
116. [em vs rem](#em-vs-rem)
117. [visibility hidden vs display none](#visibility-hidden-vs-display-none)
118. [pseudo-class vs pseudo-element](#pseudo-class-vs-pseudo-element)
119. [Bootstrap vs Tailwind](#bootstrap-vs-tailwind)
120. [gap vs space-x](#gap-vs-space-x)
121. [CSS vs Tailwind](#css-vs-tailwind)
122. [inline CSS vs external CSS](#inline-css-vs-external-css)
123. [How does the browser render HTML and CSS?](#how-does-the-browser-render-html-and-css)
124. [What is reflow vs repaint?](#what-is-reflow-vs-repaint)
125. [How do you optimize frontend CSS performance?](#how-do-you-optimize-frontend-css-performance)
126. [Why is Tailwind popular in modern frontend development?](#why-is-tailwind-popular-in-modern-frontend-development)
127. [How would you decide between CSS, SCSS, Tailwind, and CSS-in-JS?](#how-would-you-decide-between-css-scss-tailwind-and-css-in-js)

## HTML Interview Questions

## 1. What is HTML?
**Answer:** HTML stands for HyperText Markup Language. It is the standard markup language used to structure content on the web, such as headings, paragraphs, images, links, forms, and tables.

## 2. Why is HTML important?
**Answer:** HTML is important because it provides the structure of a web page. Without HTML, the browser would not know how to organize or display content meaningfully.

## 3. What is the difference between HTML and HTML5?
**Answer:** HTML5 is the modern version of HTML. It introduced semantic tags like `header`, `section`, and `article`, along with built-in support for audio, video, canvas, and better form controls.

## 4. What are semantic elements in HTML?
**Answer:** Semantic elements are tags that clearly describe their meaning, like `header`, `nav`, `main`, `section`, `article`, and `footer`. They improve readability, accessibility, and SEO.

## 5. Why should we use semantic HTML?
**Answer:** We use semantic HTML because it makes the structure more meaningful for developers, browsers, screen readers, and search engines. It improves accessibility and maintainability.

## 6. What is the difference between block and inline elements?
**Answer:** Block elements take the full available width and start on a new line, like `div` and `p`. Inline elements only take the width they need and stay in the same line, like `span` and `a`.

## 7. What is the difference between div and span?
**Answer:** `div` is a block-level container, while `span` is an inline container. Both are non-semantic and mainly used for grouping and styling.

## 8. What is the purpose of the alt attribute in images?
**Answer:** The `alt` attribute provides alternative text for an image. It improves accessibility for screen readers and also helps when the image fails to load.

## 9. What is the difference between id and class?
**Answer:** `id` should be unique for a page and is used to identify a single element. `class` can be reused across multiple elements and is mainly used for styling and grouping.

## 10. What are data-* attributes?
**Answer:** `data-*` attributes are custom attributes used to store extra information directly on HTML elements. They are commonly accessed in JavaScript.

## 11. What is the purpose of the meta tag?
**Answer:** The `meta` tag provides metadata about the document, such as character encoding, viewport settings, description, and SEO-related information.

## 12. Why is the viewport meta tag used?
**Answer:** The viewport meta tag is used to make the page responsive on mobile devices by controlling layout scaling and width behavior.

## 13. What is the difference between strong and b tags?
**Answer:** `strong` gives semantic importance, while `b` is mainly for visual bold styling without implying importance.

## 14. What is the difference between em and i tags?
**Answer:** `em` adds semantic emphasis, while `i` is mostly for visual italic styling without semantic emphasis.

## 15. What is the purpose of the doctype declaration?
**Answer:** The doctype tells the browser which version of HTML is being used and helps the browser render the page in standards mode.

## 16. What are self-closing tags?
**Answer:** These are elements that do not require a closing tag because they do not wrap content, like `img`, `br`, `hr`, and `input`.

## 17. What is the difference between section and article?
**Answer:** `section` is a thematic grouping of content, while `article` is a self-contained piece of content that can stand independently, like a blog post or news item.

## 18. What is the difference between header, head, and heading?
**Answer:** `head` contains metadata and is not shown on the page, `header` is a semantic section of visible page content, and headings are tags like `h1` to `h6` used for titles.

## 19. What is the difference between ol, ul, and dl?
**Answer:** `ol` is an ordered list, `ul` is an unordered list, and `dl` is a description list used for term-definition pairs.

## 20. What is accessibility in HTML?
**Answer:** Accessibility means building HTML in a way that all users, including those using assistive technologies, can understand and interact with the content.

## 21. How do labels improve form accessibility?
**Answer:** Labels connect text with form inputs so users and screen readers know exactly what each field is for. Clicking the label also focuses the input.

## 22. What is the difference between button and input type="button"?
**Answer:** Both create clickable buttons, but `button` is more flexible because it can contain HTML content inside it, while `input type="button"` cannot.

## 23. What are the different input types in HTML5?
**Answer:** HTML5 introduced types like `email`, `number`, `date`, `range`, `url`, `tel`, `search`, `color`, and more for better validation and user experience.

## 24. What is the difference between localStorage, sessionStorage, and cookies?
**Answer:** `localStorage` persists until cleared, `sessionStorage` lasts for the browser session, and cookies are smaller, can expire, and are sent to the server with requests.

## 25. What is iframe?
**Answer:** An `iframe` is used to embed another HTML page or external content inside the current page.

## 26. What are the new features of HTML5?
**Answer:** HTML5 introduced semantic elements, audio, video, canvas, SVG support, improved forms, local storage, and better multimedia handling without plugins.

## 27. What is the purpose of the preload attribute?
**Answer:** The `preload` attribute tells the browser whether media or resources should be loaded early for better performance or UX.

## 28. What is the difference between async and defer in script tags?
**Answer:** `async` loads the script in parallel and executes it as soon as it is ready, while `defer` also loads in parallel but executes only after the HTML is fully parsed.

## 29. How do you improve SEO with HTML?
**Answer:** I improve SEO by using semantic tags, proper heading structure, descriptive meta tags, alt text for images, clean URLs, and accessible content structure.

---

# CSS Interview Questions

## 30. What is CSS?
**Answer:** CSS stands for Cascading Style Sheets. It is used to control the presentation, layout, colors, spacing, and visual styling of HTML elements.

## 31. Why is CSS called cascading?
**Answer:** It is called cascading because multiple style rules can apply to the same element, and CSS decides which rule wins based on priority, specificity, and source order.

## 32. What is specificity in CSS?
**Answer:** Specificity is the rule system CSS uses to determine which selector is more specific and therefore should be applied when multiple rules target the same element.

## 33. Inline vs internal vs external CSS?
**Answer:** Inline CSS is written directly on an element, internal CSS is inside a `style` tag in the page, and external CSS is written in a separate stylesheet file. External CSS is preferred for maintainability.

## 34. What is the box model?
**Answer:** The box model describes how every element is rendered as content, padding, border, and margin.

## 35. What is the difference between content-box and border-box?
**Answer:** In `content-box`, width and height apply only to the content. In `border-box`, width and height include padding and border, which is usually easier to manage.

## 36. What is the difference between margin and padding?
**Answer:** Margin creates space outside the border, while padding creates space inside the border between the content and border.

## 37. What is margin collapsing?
**Answer:** Margin collapsing happens when vertical margins of adjacent block elements combine into a single margin instead of adding together.

## 38. What is display property?
**Answer:** The `display` property controls how an element behaves in the layout, such as `block`, `inline`, `inline-block`, `flex`, `grid`, or `none`.

## 39. Difference between block, inline, and inline-block?
**Answer:** `block` takes full width and starts on a new line, `inline` stays in line and does not respect width and height fully, and `inline-block` stays inline but does respect width and height.

## 40. What is position property in CSS?
**Answer:** The `position` property controls how an element is positioned, with values like `static`, `relative`, `absolute`, `fixed`, and `sticky`.

## 41. Difference between relative, absolute, fixed, and sticky?
**Answer:** `relative` positions an element relative to itself, `absolute` positions it relative to the nearest positioned ancestor, `fixed` positions it relative to the viewport, and `sticky` behaves like relative until a scroll threshold is reached.

## 42. What is z-index?
**Answer:** `z-index` controls the stacking order of positioned elements. Higher values appear above lower ones within the same stacking context.

## 43. What is overflow property?
**Answer:** The `overflow` property controls what happens when content exceeds its container, such as `visible`, `hidden`, `scroll`, or `auto`.

## 44. What is opacity?
**Answer:** `opacity` controls the transparency of an element, where `1` is fully visible and `0` is fully transparent.

## 45. What is the difference between visibility hidden and display none?
**Answer:** `visibility: hidden` hides the element but keeps its layout space, while `display: none` removes it from the layout completely.

## 46. What is Flexbox?
**Answer:** Flexbox is a one-dimensional layout system used to align and distribute items efficiently in a row or column.

## 47. What is CSS Grid?
**Answer:** CSS Grid is a two-dimensional layout system used for rows and columns, making it ideal for complex page layouts.

## 48. Flexbox vs Grid?
**Answer:** Flexbox is best for one-dimensional layouts, while Grid is better for two-dimensional layouts where both rows and columns matter.

## 49. What is justify-content?
**Answer:** `justify-content` aligns flex or grid items along the main axis.

## 50. What is align-items?
**Answer:** `align-items` aligns items along the cross axis in flexbox or grid.

## 51. What is align-self?
**Answer:** `align-self` allows one specific item to override the container's `align-items` setting.

## 52. What is gap in CSS?
**Answer:** `gap` defines spacing between flex or grid items without needing margins on the children.

## 53. What are pseudo-classes?
**Answer:** Pseudo-classes target elements based on state or position, like `:hover`, `:focus`, `:first-child`, and `:nth-child()`.

## 54. What are pseudo-elements?
**Answer:** Pseudo-elements target parts of an element, such as `::before`, `::after`, `::placeholder`, and `::selection`.

## 55. What is the difference between pseudo-class and pseudo-element?
**Answer:** A pseudo-class targets the state of an existing element, while a pseudo-element targets a virtual part of an element.

## 56. What is responsive design?
**Answer:** Responsive design means building layouts that adapt well across different screen sizes and devices.

## 57. What are media queries?
**Answer:** Media queries let us apply CSS conditionally based on factors like screen width, height, orientation, or resolution.

## 58. Mobile-first vs desktop-first?
**Answer:** Mobile-first means starting with styles for smaller screens and scaling up, while desktop-first starts with large-screen styles and scales down. Mobile-first is generally preferred.

## 59. What are CSS units?
**Answer:** Common CSS units include `px`, `%`, `em`, `rem`, `vw`, `vh`, and `fr`. The right choice depends on layout, scalability, and responsiveness.

## 60. em vs rem?
**Answer:** `em` is relative to the parent element's font size, while `rem` is relative to the root element's font size.

## 61. px vs % vs vw/vh?
**Answer:** `px` is fixed, `%` is relative to the parent, and `vw` and `vh` are relative to the viewport width and height.

## 62. What is transition in CSS?
**Answer:** A transition lets CSS property changes happen smoothly over a duration instead of changing instantly.

## 63. What is transform?
**Answer:** `transform` is used to visually modify an element with operations like translate, scale, rotate, and skew.

## 64. What is animation in CSS?
**Answer:** CSS animation allows more advanced movement or style changes over time using keyframes.

## 65. What is keyframes?
**Answer:** `@keyframes` defines the intermediate steps of an animation.

## 66. What is the difference between transition and animation?
**Answer:** Transition is triggered by a property change and usually handles simple effects, while animation can run automatically and support multiple stages with keyframes.

## 67. What is inherit, initial, unset, and revert?
**Answer:** `inherit` takes the parent's value, `initial` resets to the default spec value, `unset` acts as inherit or initial depending on the property, and `revert` rolls back to the previous cascade origin.

## 68. What is CSS variable?
**Answer:** CSS variables, also called custom properties, are reusable values defined with `--name` and accessed using `var()`.

## 69. Why use CSS variables?
**Answer:** They improve consistency, theming, maintainability, and make it easier to update repeated values like colors and spacing.

## 70. What is BEM?
**Answer:** BEM stands for Block, Element, Modifier. It is a naming convention that makes CSS more structured and maintainable.

## 71. What is the difference between absolute and relative units?
**Answer:** Absolute units like `px` stay fixed, while relative units like `%`, `em`, `rem`, `vw`, and `vh` adapt based on another value.

## 72. How do you center a div?
**Answer:** The best approach depends on context, but I usually use Flexbox with `display: flex`, `justify-content: center`, and `align-items: center`.

## 73. What is min-width, max-width, min-height, max-height?
**Answer:** These properties set the minimum or maximum allowed dimensions of an element and are useful in responsive layouts.

## 74. What is object-fit?
**Answer:** `object-fit` controls how replaced content like images or videos fits inside its container, using values like `cover`, `contain`, or `fill`.

## 75. What is background-size cover vs contain?
**Answer:** `cover` fills the container completely and may crop the image, while `contain` ensures the full image is visible but may leave empty space.

## 76. What are combinators in CSS?
**Answer:** Combinators define relationships between selectors, such as descendant, child, adjacent sibling, and general sibling.

## 77. What is !important?
**Answer:** `!important` forces a declaration to override normal specificity rules, but it should be avoided unless absolutely necessary.

## 78. How do you optimize CSS performance?
**Answer:** I optimize CSS by keeping selectors simple, removing unused styles, minimizing heavy layout changes, using efficient architecture, and reducing unnecessary repaints and reflows.

---

# Tailwind CSS Interview Questions

## 79. What is Tailwind CSS?
**Answer:** Tailwind CSS is a utility-first CSS framework that lets us build designs directly in markup using small reusable utility classes.

## 80. Why use Tailwind CSS?
**Answer:** Tailwind speeds up development, keeps styling consistent, reduces context switching between HTML and CSS files, and encourages reusable design systems.

## 81. What does utility-first mean?
**Answer:** Utility-first means styling is done using small single-purpose classes like `p-4`, `text-center`, or `bg-blue-500` instead of writing custom CSS for everything.

## 82. Tailwind vs traditional CSS?
**Answer:** Traditional CSS usually involves writing custom selectors and stylesheets, while Tailwind uses utility classes directly in the markup for faster and more consistent styling.

## 83. What are the advantages of Tailwind?
**Answer:** The main advantages are faster UI development, consistency, easier responsive styling, good design token control, and less need for naming custom classes.

## 84. What are the disadvantages of Tailwind?
**Answer:** The main drawbacks are that class lists can become long, the markup can look crowded, and teams unfamiliar with utility-first styling may need time to adapt.

## 85. How does Tailwind work internally?
**Answer:** Tailwind generates utility classes based on its configuration. In modern setups, it scans project files and includes only the classes actually used, which keeps the final CSS small.

## 86. What is Tailwind config file?
**Answer:** The Tailwind config file is where we customize theme values like colors, spacing, breakpoints, fonts, and plugins.

## 87. How do responsive classes work in Tailwind?
**Answer:** Responsive classes use prefixes like `sm:`, `md:`, `lg:`, and `xl:` to apply utilities at specific breakpoints.

## 88. How do hover, focus, and active states work in Tailwind?
**Answer:** Tailwind uses state variants like `hover:`, `focus:`, `active:`, and `disabled:` to apply styles conditionally based on interaction state.

## 89. How do dark mode classes work in Tailwind?
**Answer:** Tailwind supports dark mode using the `dark:` variant, and it can be triggered by media preference or a class-based strategy depending on configuration.

## 90. What is the difference between container and mx-auto?
**Answer:** `container` sets a responsive max-width at each breakpoint, while `mx-auto` centers an element horizontally by applying auto margins.

## 91. How do spacing utilities work in Tailwind?
**Answer:** Spacing utilities like `p-4`, `m-2`, `gap-6`, and `space-y-4` map to predefined spacing values in the theme.

## 92. How do color utilities work in Tailwind?
**Answer:** Tailwind provides color classes like `bg-blue-500`, `text-red-600`, and `border-gray-300`, all based on the configured design system.

## 93. What is arbitrary value in Tailwind?
**Answer:** Arbitrary values let us use custom values directly inside square brackets, like `w-[250px]` or `bg-[#1e1e1e]`, when the default scale is not enough.

## 94. What is @apply in Tailwind?
**Answer:** `@apply` lets us combine Tailwind utility classes inside a custom CSS rule. I use it sparingly when repeated utility groups need abstraction.

## 95. What are Tailwind plugins?
**Answer:** Plugins extend Tailwind by adding new utilities, components, variants, or theme behavior.

## 96. How do you customize Tailwind theme?
**Answer:** I customize the theme in `tailwind.config.js` by extending colors, spacing, fonts, shadows, breakpoints, and other design tokens.

## 97. Tailwind with React — any benefit?
**Answer:** Yes, Tailwind works especially well with React because component-based architecture and utility-first styling fit naturally together.

## 98. How do you manage long class names in Tailwind?
**Answer:** I manage long class names by grouping logically, extracting reusable components, using helper functions like `clsx`, and avoiding unnecessary utility duplication.

## 99. What is clsx or classnames used for with Tailwind?
**Answer:** They are helper libraries used to conditionally combine classes in a clean and readable way.

## 100. What is Tailwind Preflight?
**Answer:** Preflight is Tailwind's base style reset built on top of modern CSS normalization to give more consistent default styling across browsers.

## 101. How is Tailwind different from CSS Modules?
**Answer:** CSS Modules scope custom CSS locally, while Tailwind focuses on using predefined utility classes directly in markup. They solve different styling problems.

## 102. How do you create responsive layouts in Tailwind?
**Answer:** I use utility classes with breakpoint prefixes like `grid-cols-1 md:grid-cols-2 lg:grid-cols-4` or `flex-col md:flex-row`.

## 103. How do flex and grid work in Tailwind?
**Answer:** Tailwind provides utility classes that map directly to CSS properties, such as `flex`, `justify-between`, `items-center`, `grid`, `grid-cols-3`, and `gap-4`.

## 104. What is the difference between hidden and invisible in Tailwind?
**Answer:** `hidden` applies `display: none`, removing the element from layout, while `invisible` applies `visibility: hidden`, keeping the layout space.

## 105. How do transitions and animations work in Tailwind?
**Answer:** Tailwind provides utilities like `transition`, `duration-300`, `ease-in-out`, `animate-spin`, and more for quick motion styling.

## 106. What is the difference between space-x and gap?
**Answer:** `gap` works with flex and grid layouts for spacing between items, while `space-x` and `space-y` add margin-based spacing between direct children.

## 107. How do you make Tailwind code maintainable?
**Answer:** I keep it maintainable by using consistent design tokens, reusable components, helper functions for conditional classes, and avoiding overuse of arbitrary values.

---

# Rapid-Fire Interview Questions

## div vs span
**Answer:** `div` is block-level, `span` is inline.

## id vs class
**Answer:** `id` is unique, `class` is reusable.

## HTML vs HTML5
**Answer:** HTML5 is the modern version with semantic tags, multimedia, and better form support.

## block vs inline vs inline-block
**Answer:** Block takes full width, inline stays in line, inline-block stays inline but supports width and height.

## margin vs padding
**Answer:** Margin is outside the border, padding is inside the border.

## relative vs absolute vs fixed vs sticky
**Answer:** Relative offsets itself, absolute positions against nearest positioned ancestor, fixed sticks to viewport, sticky sticks on scroll threshold.

## Flexbox vs Grid
**Answer:** Flexbox is one-dimensional, Grid is two-dimensional.

## em vs rem
**Answer:** `em` depends on parent, `rem` depends on root.

## visibility hidden vs display none
**Answer:** Hidden keeps layout space, none removes the element from layout.

## pseudo-class vs pseudo-element
**Answer:** Pseudo-class targets state, pseudo-element targets a part of an element.

## Bootstrap vs Tailwind
**Answer:** Bootstrap is component-based and opinionated, Tailwind is utility-first and highly customizable.

## gap vs space-x
**Answer:** `gap` is layout-native spacing, `space-x` adds child margins between siblings.

## CSS vs Tailwind
**Answer:** CSS is custom styling from scratch, Tailwind is utility-first styling with predefined classes.

## inline CSS vs external CSS
**Answer:** Inline is quick but hard to maintain, external CSS is scalable and preferred.

---

# Senior-Level Questions

## How does the browser render HTML and CSS?
**Answer:** The browser parses HTML into the DOM, parses CSS into the CSSOM, combines them into the render tree, calculates layout, and then paints pixels to the screen. Any major DOM or CSS change can trigger reflow or repaint depending on the change.

## What is reflow vs repaint?
**Answer:** Reflow happens when layout needs to be recalculated, such as width or position changes. Repaint happens when visual appearance changes without affecting layout, such as color changes.

## How do you optimize frontend CSS performance?
**Answer:** I reduce unused CSS, keep selectors simple, avoid layout thrashing, prefer transforms over layout-heavy animations, minimize reflows, and load critical CSS efficiently.

## Why is Tailwind popular in modern frontend development?
**Answer:** Tailwind is popular because it improves speed, consistency, and developer productivity while fitting well with component-based frameworks like React and Next.js.

## How would you decide between CSS, SCSS, Tailwind, and CSS-in-JS?
**Answer:** I choose based on team preference, project size, design system maturity, runtime constraints, and maintainability. Tailwind is great for speed and consistency, SCSS is great for custom stylesheet control, and CSS-in-JS can be useful when styles depend heavily on component logic.
