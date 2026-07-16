# HTML, CSS & Tailwind — Interview Notes
---

## HTML

### Structure & Semantics

- HTML stands for HyperText Markup Language, and it's the standard markup language we use to structure content on the web — things like headings, paragraphs, images, links, forms, and tables.

- HTML5 is the modern version of HTML — it introduced semantic tags like `header`, `nav`, `main`, `section`, `article`, and `footer`, plus native support for audio, video, canvas, and better form controls.

- Semantic elements are tags that clearly describe their meaning, and we use them because they improve readability for developers, and help screen readers and search engines understand the page structure better — so they're good for accessibility and SEO both.

- `section` is used for a thematic grouping of related content, while `article` is for a self-contained piece of content that could stand on its own, like a blog post or a news item.

- `div` is a block-level container and `span` is an inline container — both are non-semantic, so I mainly use them just for grouping or styling elements when no semantic tag fits.

- `strong` gives semantic importance to text — like saying this is genuinely important — while `b` is purely visual bold styling with no meaning attached.

- The doctype declaration at the top of the file tells the browser which HTML version we're using, so it renders the page in standards mode instead of quirks mode.

- Self-closing tags are elements that don't wrap any content, so they don't need a closing tag — things like `img`, `br`, `hr`, and `input`.

- `ol` is an ordered list, `ul` is an unordered list, and `dl` is a description list used for term-definition pairs.

### Attributes & Identity

- `id` should be unique on a page and is used to target one specific element, while `class` can be reused across multiple elements — so I use `id` for unique hooks and `class` for shared styling or grouping.

- `data-*` attributes let me attach custom data directly onto an HTML element, and then I can read that data easily in JavaScript through `element.dataset`.

- The `alt` attribute on an image gives alternative text — it helps screen readers describe the image, and it also shows as fallback text if the image fails to load.

- The `meta` tag holds metadata about the document, like character encoding or SEO description, and the viewport meta tag specifically controls how the page scales on mobile devices so it renders responsively.

### Storage & Embedding

- `localStorage` persists data until it's manually cleared, `sessionStorage` only lasts for the current browser session, and cookies are smaller, can have an expiry, and get sent to the server with every request — so I pick based on how long the data needs to live and whether the server needs it.

- An `iframe` lets me embed another HTML page or external content inside the current page.

### Performance / Loading

- The `preload` attribute tells the browser to fetch a resource early, which helps performance for things we know we'll need soon.

- With script tags, `async` loads the script in parallel and runs it as soon as it's ready, without waiting for HTML parsing to finish, while `defer` also loads in parallel but waits until the HTML is fully parsed before executing, and runs scripts in order.

---

## CSS

### Box Model

- Every element in CSS is rendered using the box model, which is content, then padding, then border, then margin, going from inside out.

- With `content-box`, which is the default, the width and height I set only apply to the content itself, but with `border-box`, the width and height include the padding and border too — which is usually easier to reason about, so I often set `border-box` globally.

- Margin creates space outside the border, between this element and its neighbors, while padding creates space inside the border, between the content and the border itself.

### Display & Positioning

- The `display` property controls how an element behaves in the layout — `block` takes the full width and starts on a new line, `inline` only takes the space it needs and doesn't respect width or height, `inline-block` stays in line but does respect width and height, and then there's `flex`, `grid`, and `none`.

- `visibility: hidden` hides the element but still keeps its space reserved in the layout, whereas `display: none` removes it from the layout completely, so nothing else shifts.

- `position` controls how an element is positioned — `static` is the default flow, `relative` offsets it from its own normal position, `absolute` positions it relative to the nearest positioned ancestor, `fixed` positions it relative to the viewport so it stays put on scroll, and `sticky` behaves like relative until a scroll threshold, then sticks like fixed.

- `z-index` controls the stacking order of positioned elements — higher values sit above lower ones within the same stacking context.

- `overflow` controls what happens when content is too big for its container — `visible` lets it spill out, `hidden` clips it, `scroll` always shows scrollbars, and `auto` shows them only when needed.

### Layout Systems

- Flexbox is a one-dimensional layout system, so it's great for aligning and distributing items in a single row or column.
	- `flex-grow` – Defines how much an item should grow relative to others.
	- `flex-shrink` – Defines how much an item should shrink when space is limited.
	- `flex-basis` – Sets the initial size of a flex item before growing or shrinking.
	- `flex: 1` – Shorthand for `flex-grow: 1`, `flex-shrink: 1`, and `flex-basis: 0`, allowing items to share available space equally.

- CSS Grid is two-dimensional, so it handles rows and columns at the same time, which makes it better suited for full page or more complex layouts.

- `justify-content` aligns items along the main axis, and `align-items` aligns them along the cross axis.

- `gap` adds spacing directly between flex or grid items using the layout system itself, while `space-x` and `space-y` add margin-based spacing between direct children — I generally prefer `gap` when I can, since it's more predictable.

### Selectors

- A pseudo-class targets a real element based on its state or position, like `:hover`, `:focus`, `:first-child`, or `:nth-child()`.

- A pseudo-element targets a virtual part of an element that doesn't exist in the actual markup, like `::before`, `::after`, `::placeholder`, or `::selection`.

### Visual & Motion

- `opacity` controls how transparent an element is, from `0`, fully invisible, to `1`, fully visible — but the element is still there taking up space and can still be interactive.

- `transform` visually manipulates an element using things like translate, scale, rotate, or skew, without affecting the normal document flow.

- A `transition` smooths out a property change that happens due to some trigger, like a hover, while an `animation`, combined with `@keyframes`, can run automatically and go through multiple stages without needing a trigger.

- `object-fit` controls how an image or video fits inside its container — `cover` fills the whole container and may crop the content, while `contain` shows the entire image but might leave empty space. `background-size` follows the same cover-versus-contain logic for background images.

### Units

- `px` is a fixed unit, `%` is relative to the parent, `em` is relative to the parent's font size and compounds as you nest, `rem` is relative to the root font size so it's more predictable, `vw` and `vh` are relative to the viewport, and `fr` is used in Grid to represent a fraction of the available space.

### Cascade & Misc

- CSS is called cascading because when multiple rules target the same element, specificity and source order decide which one actually wins — inline styles beat IDs, which beat classes, which beat plain element selectors.

- Inline CSS is written directly on the element, internal CSS sits inside a `style` tag in the page, and external CSS lives in a separate file — I go with external for anything beyond a quick one-off, since it's easier to maintain and gets cached by the browser.

- `!important` forces a rule to override normal specificity, but I try to avoid it since it makes the cascade harder to reason about — I'll only reach for it when overriding something like third-party CSS I can't otherwise touch.

---

## Tailwind CSS

### Core Concept

- Tailwind CSS is a utility-first CSS framework, so instead of writing custom CSS rules, I style elements directly in the markup using small, reusable utility classes like `p-4`, `text-center`, or `bg-blue-500`.

- I like using Tailwind because it speeds up development, keeps styling consistent across the team, removes the constant context-switching between HTML and CSS files, and since it's all utility classes, there's no dead CSS left behind when I delete a component.

- `@apply` lets me pull a group of utility classes into one custom CSS class, which I'll use when the same combination of utilities keeps repeating and it's cleaner to name it once.

### Responsive & State Variants

- Responsive classes use breakpoint prefixes like `sm:`, `md:`, `lg:`, and `xl:`, and Tailwind is mobile-first, so each prefix applies from that breakpoint upward.

- State variants like `hover:`, `focus:`, `active:`, and `disabled:` let me apply styles conditionally based on the element's interaction state, right in the class name.

### Layout Utilities

- `container` sets a responsive max-width for the element at each breakpoint, while `mx-auto` just centers an element horizontally using automatic left and right margins — I usually use them together.

- `gap-*` adds spacing directly in flex or grid layouts, while `space-x-*` and `space-y-*` add margin between direct children instead — I lean on `gap` when the layout supports it since it's cleaner.

- `hidden` maps to `display: none`, while `invisible` maps to `visibility: hidden` — so the same distinction as plain CSS applies here too.

- `transition` enables smooth animation when a property changes, such as on hover or focus.

- `duration-*` controls how long the transition takes. For example, `duration-300` means the transition lasts **300 milliseconds**.
