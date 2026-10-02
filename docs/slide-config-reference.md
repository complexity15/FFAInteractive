# Slide Config Schema Reference

Each sermon's `index.html` has a `const slides = [...]` array. Each slide object supports:

```js
{
  // --- Image (required) ---
  background: "slide-02.jpg",   // relative filename OR full i.imgur.com URL

  // --- Optional text overlay (rarely used — most slides are flat images) ---
  heading: "",
  bullets: [],

  // --- Video mode fields (omit both if using notes mode instead) ---
  startSeconds: 2183,
  endSeconds: 2254,
  voiceLabel: "Listen to Introduction",  // optional override of default "Hear this slide"

  // --- Notes mode field (omit if using video mode instead) ---
  notes: [
    "First bullet point summarizing what the pastor said on this slide",
    "Second bullet point"
  ],

  // --- Verse tags (optional, either mode) ---
  markers: [
    { verseKey: "luke15-1", top: "26%", left: "50%" }
  ],

  // --- Thumbnail label override (used only for the Introduction slide) ---
  thumbLabel: "Introduction"
}
```

Matching `verses` lookup object (top-level, alongside `slides`):
```js
const verses = {
  "luke15-1": {
    ref: "Luke 15:1",
    text: "Now the tax collectors and sinners were all drawing near to hear him."
  }
};
```

## Notes on fields
- `markers` `top`/`left` are percentages relative to the full slide image — position is always a best guess since the image isn't visible directly; confirm and adjust after the user sees it live.
- Removing a slide from the array auto-renumbers everything after it — thumbnail numbers are computed from array position (`numberedCount`), never hardcoded.
- The row-break in the thumbnail strip happens automatically after the 8th numbered slide.
- `YOUTUBE_VIDEO_ID` is a separate top-level constant, only relevant in video mode.
