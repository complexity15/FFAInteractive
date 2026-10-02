# FFA Interactive Sermon Notes — Project Instructions

## What this project is
Building weekly interactive sermon pages for Faith Fellowship Aurora (ffaurora.org), hosted on Cloudflare and embedded in Squarespace via iframe. Each sermon is a single self-contained `index.html` file (+ slide images if not using Imgur URLs).

## Standard deck structure
- **Introduction** slide first (thumbLabel: "Introduction", no number)
- Numbered slides after that (1, 2, 3...) — numbering is calculated dynamically from array position, never hardcoded
- Thumbnail strip breaks into two rows after slide "8" for cleaner layout
- Mobile-responsive: controls stack vertically under 480px width

## Two build modes, per sermon
**With YouTube video available:**
- Each slide has `startSeconds` / `endSeconds` marking its portion of the sermon recording
- Button reads "▶ Hear this slide" (or custom `voiceLabel`, e.g. "Listen to Introduction")
- Tapping opens a small draggable, closable popup that auto-plays just that clip and auto-stops at endSeconds
- YouTube video ID goes in `YOUTUBE_VIDEO_ID`

**Without video (e.g. recording was missed):**
- No timestamps — button instead reads "📝 Read Sermon Notes"
- Tapping opens the same draggable popup, but showing bullet-point notes pulled from the pastor's sermon notes doc, matched to that slide
- To match notes to slides: since PPT slides are usually flat images with no extractable text, actually view each slide image and cross-reference against the notes/lesson docx files to find the right section

**Going forward:** both can coexist — a slide can have video AND notes when both source materials are available. Not mutually exclusive.

## Sermon notes writing rules
- Use only verbatim excerpts from the pastor's sermon-notes document. Do not add paraphrases, interpretations, summaries, or assistant-written wording.
- Match each excerpt to the specific slide it explains.
- Curate the notes: keep the key highlights and the context needed to understand that slide, without copying every line from the manuscript.
- Remove conversational filler, audience prompts, and structural labels that do not help explain the slide (for example, “So, are you ready?”, “If you are, say…”, or “Main Idea:”).
- Keep the notes substantial enough to explain the slide, but concise and easy to read in the popup.

## Verse tags
- Small pill-shaped "Verse" tags placed over specific spots on a slide image
- Tapping shows a tile with the ESV reference + text
- Position via `top`/`left` percentages in a `markers` array on the slide — these are guesses since I can't see the actual image myself; always ask the user to confirm placement once live and adjust based on screenshots
- Tile auto-flips above/below the marker depending on available space so it never gets clipped by the stage edges

## Image hosting
- Preferred: bundle slide images as files alongside `index.html` in the same Cloudflare deploy folder, referenced by relative filename (e.g. `slide-02.jpg`) — no Imgur needed
- Imgur URLs still work if the user already has them hosted there

## Deployment
- Host: Cloudflare (Workers & Pages → Create → "Upload your static files")
- File must be named `index.html` to serve at the root URL without a path suffix
- Embed in Squarespace via a Code Block iframe:
  `<iframe src="[URL]" width="100%" height="900" style="border:none;" allow="autoplay; encrypted-media"></iframe>`
- The `allow="autoplay; encrypted-media"` attribute is required for the video popup to autoplay when nested in Squarespace's iframe

## Known limitations to keep in mind
- I cannot watch/listen to the YouTube video myself — timestamps must come from the user
- I cannot fetch content from Imgur album links (`/a/...`) — only direct `i.imgur.com/....ext` links work, and even those I can't preview myself
- Past weeks' files aren't retained on my end between sessions — if editing an older sermon, ask the user to re-upload that week's current `index.html` rather than trying to reconstruct it from memory
