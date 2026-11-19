<!--
  Recurring corner badge. Slidev auto-discovers `global-top.vue` at the project
  root and renders it once, above every slide.

  TODO: drop your badge image at public/images/badge.png (or change `src`).
  Until the file exists, it renders as a broken image on every slide.

  To hide it on any slide, set `hideBadge: true` in that slide's frontmatter.
-->
<template>
  <CornerBadge src="/images/badge.png" />
</template>

<style>
/* Hide the slide title in every footer. The theme has no option for this: its
   Footer prints the slide's `title` frontmatter (or "World Wide Technology").
   `visibility: hidden` keeps the element's flex space so the page number stays
   pinned right. Unscoped on purpose so it reaches the theme layouts' markup.
   To bring the footer title back, delete this block. */
.wwt-footer__title {
  visibility: hidden;
}

/* Hide the top-left WWT logo that each content layout draws, and keep the
   footer's bottom-left one. To bring the top-left logo back on a single slide,
   add this to that slide's frontmatter:

     class: show-top-logo

   Pure CSS on purpose: it works the same in dev, presenting and export.
   The footer's logo carries the same `wwt-monogram-mark` class as the layouts'
   logos, so it is re-shown explicitly (and the per-slide rule matches it too,
   which is harmless: it is already shown).
   !important throughout because the theme's own rule has the same specificity
   as the hide rule and load order isn't guaranteed. */
.wwt-monogram-mark {
  display: none !important;
}
.wwt-footer__monogram,
.show-top-logo .wwt-monogram-mark {
  display: block !important;
}

/* Click-reveal option. With `htmlAttrs: data-click-reveal: "off"` in the deck's
   headmatter, content that a layout (stats, process, timeline, boxes with
   `reveal`) or a `v-click` would hide until clicked is always shown. Clicks
   still advance, so the [click] cues in the speaker notes step through as
   usual; set each slide's `clicks:` to its number of cues.
   To bring click reveal back deck-wide, remove that headmatter line. To bring
   it back on a single slide, add this to that slide's frontmatter:

     class: reveal-on-click

   !important because the framework hides these with its own rule. */
html[data-click-reveal="off"] .slidev-layout:not(.reveal-on-click) .slidev-vclick-hidden {
  opacity: 1 !important;
  pointer-events: auto !important;
}
</style>
