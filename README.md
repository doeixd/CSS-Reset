# CSS Reset

My opinionated CSS reset for new projects. 
<br />

```css
@layer reset {
  *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; vertical-align:baseline; min-width:0; scroll-behavior:smooth; animation-composition:accumulate; }
  :where(:not(:is(svg *, p, h1, h2, h3, h4, h5, h6))) { transition:ease-out 100ms; transition-property:color, background, margin, padding, width, grid-column, grid-row, height, grid-template-columns, grid-template-rows, opacity, border, border-radius; }
  :where(html) { text-size-adjust:none; -webkit-text-size-adjust:none; -moz-text-size-adjust:none; --bodyFontSize:clamp(13.5px, 2.4vw, 16px); --bodyFontColor:#323232; tab-size:4; font-family:'Work Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif; color:var(--bodyFontColor); line-height:1.5; -webkit-font-smoothing:antialiased; font-size:var(--bodyFontSize); font-synthesis:none; text-rendering:optimizeLegibility; }
  :where(html:focus-within) { scroll-behavior:smooth; }
  :where(:not(:defined)) { display:block; }
  :where(:is(body, html)) { width:100%; height:100%; }
  :where(:is(img, picture, video, canvas, svg)) { display:block; max-width:100%; vertical-align:middle; }
  :where(:is(input, button, textarea, select):not([disabled])) { font:inherit; cursor:pointer; }
  :where(*:not(:is(main, body, .prose, .app, .root, #root, article, form)) > :is(h1, h2, h3, h4, h5, h6)), :where(p) { font-size:inherit; font-weight:inherit; overflow-wrap:break-word; text-overflow:ellipsis; background-color:inherit; }
  :where(:is(h1, h2, h3, h4, h5, h6)) { text-wrap:balance; letter-spacing:0.2px; scroll-padding-block:1lh; }
  :where(p) { text-wrap:pretty; }
  :where(textarea) { form-sizing:content; min-height:2lh; max-height:10lh; }
  :where(button) { box-sizing:content-box; text-box-trim:both; text-box-edge:cap alphabetic; }
  :where(:is(#root, #__next, div#app)) { isolation:isolate; }
  :where(table) { text-indent:0; border-color:inherit; border-collapse:collapse; border-spacing:0; }
  :where(*:not(p) ~ :is(ul, ol) > li), .list-style-none { list-style:none; }
  :where([src='']) { visibility:hidden; }
  *::backdrop { all:unset; position:fixed; inset:0; opacity:0.7; }
  :where(dialog) { max-width:100dvw; max-height:100dvh; }
  :where(:not(:is(html, audio, textarea, body, main, table, button, checkbox, input, td, tr, th, tbody, table, tfoot, video, form, details, select, summary, fieldset, hr, *::before, *::after, frame, iframe, datalist, object))) { border-style:solid; border-width:0; border-color:currentColor; }
  :where(:is(a:empty, ul:empty, dl:empty, div:empty, section:empty, article:empty, p:empty, h1:empty, h2:empty, h3:empty, h4:empty, h5:empty, h6:empty)) { display:none; }
  :where(.display-none) { display:none; }
  :where([hidden], .visually-hidden) { clip:rect(0 0 0 0); clip-path:inset(50%); height:1px; overflow:hidden; position:absolute; white-space:nowrap; width:1px; content-visibility:hidden; }
  :where(:target) { scroll-margin-block:5ex; }
  :where(summary) { cursor:pointer; display:list-item; }
  :where(iframe) { border:0; }
  :where(svg:not([width])) { height:auto; }
  :where(svg) { fill:currentColor; }
  :where(select), :where(select::picker(select)) { appearance: base-select }
  :where(:is(textarea, select, input)) {field-sizing: content; }
  @media (prefers-reduced-motion: reduce) { *, *::before, *::after { animation-duration:0.01ms !important; animation-iteration-count:1 !important; transition-duration:0.01ms !important; transition:none; animation-name:none; } }
  @view-transition { navigation:auto; }
}
```

<br />
<br />


## With comments

```css
/* Everything is in the reset layer so it can be easily overwritten. */
@layer reset {
  /* Applies to everything */
  *, *::before, *::after { 
    /* Controversial, but I like having a clean slate of margin / padding. */
    margin:0; 
    padding: 0; 
    /* Resets to what I believe most people already assume is the case. */
    box-sizing: border-box; 
    vertical-align: baseline;
    min-width: 0;
    scroll-behavior: smooth;
  }

/* I prefer having some sort of transition */
  :where(:not(:is(svg *, p, h1, h2, h3, h4, h5, h6)) {
    transition: ease-out 100ms;
    transition-property: color, background, margin, padding, width, grid-column, grid-row, height, grid-template-     columns, grid-template-rows, opacity, border, border-radius
  }

  /* Everything is defined with :where so they have zero specificity and can easily be overwritten. */
  
  :where(html) { 
    /* Fixes safari zoom issue */
    text-size-adjust: none; 
    -webkit-text-size-adjust: none; 
    -moz-text-size-adjust: none; 

    /* My preferred text settings. */
    --bodyFontSize: clamp(13.5px, 2.4vw, 16px);
    --bodyFontColor: light-dark(#fafafa, #323232);
    tab-size: 4; 
    font-family: 'Work Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif ; 
    color: var(--bodyFontColor);
    line-height: 1.5; 
    -webkit-font-smoothing: antialiased; 
    font-size: var(--bodyFontSize);
    font-synthesis: none;
    text-rendering: optimizeLegibility;
    overscroll-behavior: none
  }

  /* Smooth scrolling when focusing within the page */
  :where(html:focus-within) {
   scroll-behavior: smooth;
  }

  /* Makes webcomponents / unknown elements display as you'd expect */
  :where(:not(:defined)) { 
      display: block; 
  }

  /* What most would already expect the size of the width / height to be. */
  :where(:is(body, html)) { 
    width: 100%; 
    height: 100%; 
  }

  /* Fixes common media element issues */
  :where(:is(img, picture, video, canvas, svg)) { 
    display: block; 
    max-width: 100%; 
    vertical-align: middle; 
  }

  /* Makes the font / cursor of inputs what you'd probably expect. */
  :where(:is(input, button, textarea, select):not([disabled])) { 
    font: inherit; 
    cursor: pointer; 
  }

  /* Headings / text outside of the normal places should look like normal text  */
  :where(*:not(:is(main, body, .prose, .app, .root, #root)) > :is(h1, h2, h3, h4, h5, h6)), :where(p) { 
    font-size: inherit; 
    font-weight: inherit; 
    overflow-wrap: break-word;
    text-overflow: ellipsis;
    background-color: inherit;
  }

  /* Normal headings should look like / act headings */
  :where(:is(h1, h2, h3, h4, h5, h6)) { 
    text-wrap: balance; 
    letter-spacing: 0.2px; 
    scroll-padding-block: 1lh; 
  }

  /* Make text pretty */
  :where(p) { 
    text-wrap: pretty
  }

  /* Auto-grow text areas. */
  :where(textarea) { 
    form-sizing: content; 
    min-height: 2lh; 
    max-height: 10lh; 
  }

  /* Shrink text areas to content */
  :where(:is(textarea, select, input)) {
    field-sizing: content;
  }

  /* Allow button borders to escape their containers. I think this is what most people want. Also, trim additional space in buttons */
  :where(button) { 
    box-sizing: content-box;
    text-box-trim: both;
    text-box-edge: cap alphabetic;
  }

  /* SPA containers should be isolated. Maybe will help with css performance? Doubt it tho. */
  :where(:is(#root, #__next, div#app)) { 
    isolation: isolate; 
  }

  /* Tables as you probably want them. */
  :where(table) { 
    text-indent: 0; 
    border-color: inherit; 
    border-collapse: collapse; 
    border-spacing: 0; 
  }

  /* Lists that arnt next to text should not have bullet points. */
  :where(*:not(p) ~ :is(ul, ol) > li), .list-style-none { 
    list-style: none; 
  }

  /* Hide blank images  */
  :where([src='']) { 
    visibility: hidden; 
  }

  /* Fixes unexpected popover backdrop issues */
  *::backdrop { 
    all:unset;
    position: fixed;
    inset: 0;
    opacity: 0.7;
  }

  :where(modal::dialog) { 
    max-width: 100dvw; 
    max-height:100dvh; 
  }

  /* Makes so if just a border color / width is defined, then it'll still work as expected */
  :where(:not(:is(html, audio, textarea, body, main, table, button, checkbox, input, td, tr, th, tbody, table, tfoot, video, form, details, select, summary, fieldset, hr, *::before, *::after, frame, iframe, datalist, object))) { 
    border-style: solid; 
    border-width: 0; 
  }

  /* Hides empty elements */
  :where(:is(a:empty, ul:empty, dl:empty, div:empty, section:empty, article:empty, p:empty, h1:empty, h2:empty, h3:empty, h4:empty, h5:empty, h6:empty)) { 
    display: none; 
  }

  /* Everyone will probably need this at some point */
  :where(.display-none) { 
    display: none; 
  }

  :where([hidden], .visually-hidden) {
    clip: rect(0 0 0 0); 
    clip-path: inset(50%);
    height: 1px;
    overflow: hidden;
    position: absolute;
    white-space: nowrap; 
    width: 1px;
    content-visibility: hidden;
  }

  /* Makes Url heading targets display in view. */
  :where(:target) { 
    scroll-margin-block: 5ex; 
  }

  /* Simple prefers reduced motion compliance */
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { 
      animation-duration: 0.01ms !important; 
      animation-iteration-count: 1 !important; 
      transition-duration: 0.01ms !important; 
      transition: none; 
      animation-name: none; 
    } 
  }

  /* Turns on view transitions */
  @view-transition { 
    navigation: auto; 
  }

  /* Consistent styling for the summary element */ 
  :where(summary) { 
   cursor: pointer; 
   display: list-item; 
  } 
  
  /* Remove the default border from iframes */ 
  :where(iframe) { 
   border: 0; 
  }

  /* Ensure SVGs inherit color and don't have a default size */
  :where(svg:not([width])) {
    height: auto;
  }

  :where(svg) {
    fill: currentColor;
  }

  /* Makes select element styleable */
  :where(select), :where(select::picker(select)) {
    appearance: base-select
  }
}
```
