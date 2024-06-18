# CSS Reset

My opinionated CSS reset for new projects. 
<br />

```css
@layer reset {
  *, *::before, *::after { transition: all ease-in-out 100ms; margin:0; padding: 0; box-sizing: border-box; vertical-align: baseline; min-width: 0; scroll-behavior: smooth }
  :root { --bodyFontSize: clamp(13.5px, calc(1.2vw * 2), 16px) }
  :where(html) { text-size-adjust: none; -webkit-text-size-adjust: none; -moz-text-size-adjust: none; tab-size: 4; font-family: 'Work Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif ; color: #333; }
  :where(:not(:defined)) { display: block; }
  :where(:is(body, html)) { width: 100%; height: 100%; }
  :where(body) { line-height: 1.5; -webkit-font-smoothing: antialiased; font-size: var(--bodyFontSize); }
  :where(:is(img, picture, video, canvas, svg)) { display: block; max-width: 100%; vertical-align: middle; }
  :where(:is(input, button, textarea, select)) { font: inherit; cursor: pointer; }
  :where(*:not(main, body, .prose, .app, .root, #root) > :is(h1, h2, h3, h4, h5, h6)), :where(p) { font-size: inherit; font-weight: inherit; overflow-wrap: break-word; scroll-padding-block: 1lh; }
  :where(:is(h1, h2, h3, h4, h5, h6)) { text-wrap: balance; letter-spacing: 0.2px; }
  :where(p) { text-wrap: pretty; } 
  :where(:is(#root, #__next, div#app)) { isolation: isolate; }
  :where(table) { text-indent: 0; border-color: inherit; border-collapse: collapse; border-spacing: 0; }
  :where(*:not(p) ~ :is(ul, ol) > li), .list-style-none { list-style: none; }
  :where([src='']) { visibility: hidden; }
  *::backdrop{ all:unset; }
  :where(modal::dialog) { max-width: 100dvw; max-height:100dvh; }
  :where(:not(:is(html, audio, textarea, body, main, table, button, checkbox, input, td, tr, th, tbody, table, tfoot, video, form, details, select, summary, fieldset, hr, *::before, *::after, frame, iframe, datalist, object))) { border-style: solid; border-width: 0; }
  :where(:is(a:empty, ul:empty, dl:empty, div:empty, section:empty, article:empty, p:empty, h1:empty, h2:empty, h3:empty, h4:empty, h5:empty, h6:empty)) { display: none; }
  :where(.hidden) { display: none; }
  :target { scroll-margin-block: 5ex; }
  @media (prefers-reduced-motion: reduce) { *, *::before, *::after { animation-duration: 0.01ms !important; animation-iteration-count: 1 !important; transition-duration: 0.01ms !important; transition: none; animation-name: none; } }
  @view-transition { navigation: auto; }
  :where(textarea) { textarea { form-sizing: content; min-height: 2lh; max-height: 10lh; }
  :where(button) { box-sizing: content-box };
}
```
