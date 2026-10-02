# Handoff Notes (read this first in a new chat)

Live site: https://complexity15.github.io/FFAInteractive/ (GitHub Pages, branch `main`, root).
Repo: https://github.com/complexity15/FFAInteractive
Working copy on the PC: `C:\Users\paulo\Documents\Interactive Sermon\FFAInteractive`

## Ground rules (decided with the owner)
- Work ONLY in this repo folder. Do not change the older folders in `Interactive Sermon\` (September 13/20/27, "... mobile test", etc.); they are kept as personal originals.
- The three current sermons in `sermons/` were copied from the "mobile test" folders and have all features.
- Background details of the sermon page format: see `project-instructions.md` and `slide-config-reference.md` in this folder.
- Not a git-global-configured machine: identity is set per repo (user `complexity15`). Pushing needs the owner to approve a browser login if prompted.
- Commit trailer: `Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>`.

## Repo layout
- `index.html` - app home (church logo, intro, series name, list of sermons). Add each new sermon card here (newest first).
- `manifest.webmanifest`, `sw.js`, `assets/icons/` - installable web app (PWA). Name: "FFA Interactive". Theme/background `#1E1B16`.
- `sermons/YYYY-MM-DD/index.html` + `slides/` (images) + `resources/` (notes, lesson guides, transcript).
- `templates/`, `docs/`, `assets/`, `archive/` (older versions and experiments).

## Features in each sermon page (keep when making a new one)
Slide viewer, numbered slide groups, Listen (YouTube clips per slide, follows slide changes, also in Theater mode), Sermon notes popup, Your thoughts, Discussion Guide, dark/light toggle, guided tours (portrait/landscape/Theater), tour overlay tint `rgba(20,17,13,.38)`, Theater mode on desktop (fullscreen hides the Theater toggle), landscape slide-number panel fills available space.
Best starting point for a new sermon: copy the latest sermon page (`sermons/2026-09-27/index.html`, or 2026-09-20 if audio is used) and update the slides, notes, title, date and video ID.

## Decisions
- No in-app "Sermons" back button (removed on request). Android back gesture is the way back. iPhone has no back button; offer one if asked.
- Home page: no feature tiles. Series name "Growing Together, Reaching Together" in sage green `#8FA37A` below "Choose a sermon".
- Sermon pages are embedded elsewhere by iframe (height 800), so avoid anything that changes embedded behavior.
- Service worker: pages load network-first with `cache: 'no-cache'`; bump `CACHE` version in `sw.js` (currently `ffa-interactive-v8`) whenever shipping changes.
- Android install must be done from Chrome (Brave only makes a shortcut). iPhone install is Safari -> Share -> Add to Home Screen (untested; owner has no iPhone).
- September 13 and 27 have an empty `YOUTUBE_VIDEO_ID`; only September 20 has Listen clips.

## Weekly workflow: adding a new sermon
Owner provides: slide images (numbered, in a folder), sermon notes (.docx), FG lesson / discussion guide, title + series + date, YouTube link and transcript (.srt) if available, any special slides.
Steps:
1. Create `sermons/YYYY-MM-DD/` with `slides/` and `resources/`; copy the latest sermon `index.html` as the base.
2. Update title, date, slides array (`background: "slides/<file>"`), notes matched slide by slide (verbatim excerpts, see `project-instructions.md`), verse markers, and the video ID/timestamps if a recording exists.
3. Add the sermon card to the root `index.html` (newest first) and bump the `sw.js` cache version; add the new folder path to the `SHELL` list only if offline pre-caching is wanted.
4. Test in a browser (slides, notes, portrait/landscape, Theater mode, no horizontal overflow).
5. Commit and push to `main`; check the live URL after about a minute.

## Ideas discussed, not built
Reusable template for other churches (single settings file), custom domain, iPhone back button, Play Store/App Store listing, admin form for adding sermons.
