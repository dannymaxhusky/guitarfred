# GuitarFred Product Design Audit

Date: 2026-06-14
Scope: local product at `http://127.0.0.1:8765/` and `http://127.0.0.1:8765/learn/`.
Destination requested: Figma. The Figma plugin installed, but the expected write tools were not exposed in this session, so the evidence package is saved locally for direct placement in Figma.

## Captured Steps

1. Main tool, desktop default state
   Health: strong. The fretboard, chord result, interval wheel, and voicing shelf feel polished and visually coherent.
   Screenshot: `01-main-tool-desktop.png`

2. Main tool, desktop advanced section opened
   Health: mixed. The control responds, but the first viewport still mostly shows the fold header, so the feature value is not immediately visible.
   Screenshot: `02-main-tool-advanced-desktop.png`

3. Main tool, mobile default state
   Health: good. The coach layout is clearer and more focused than desktop, but lower content runs long and needs stronger section navigation.
   Screenshot: `03-main-tool-mobile.png`

4. Learning flow, desktop stage 1
   Health: useful but dense. The staged learning model is solid, but the first screen asks the user to process many chord cards and long instructions at once.
   Screenshot: `04-learning-stage1-desktop.png`

5. Learning flow, import new song
   Health: needs restructuring. The example format dominates the viewport and pushes the actual input and submit action below the fold.
   Screenshot: `05-learning-import-desktop.png`

6. Learning flow, mobile stage 1
   Health: usable but busy. The 2-column stage nav and chord cards fit, but the page becomes a long checklist without a sticky next action.
   Screenshot: `06-learning-stage1-mobile.png`

## Strengths

- The main fretboard tool has a distinctive, high-quality dark visual language. It feels like a serious music tool rather than a generic web app.
- The default Am7 state gives the user something meaningful to inspect immediately.
- The tool explains intervals in plain language, which is a strong differentiator for learning.
- The learning page has a complete progression model: chord recognition, switching, rhythm, sections, full song, and importing a new song.
- Mobile layouts are not broken; both surfaces reflow intentionally.

## UX Risks

1. Product surfaces feel disconnected.
   The learning page has a visible link back to the fretboard tool, but the main fretboard tool has no visible path into the learning flow. Users can discover "tool from course" but not "course from tool."

2. Visual language is split.
   The fretboard tool uses a dark "Midnight Studio" style, while the learning flow uses a warm paper style. Both are valid, but together they feel like separate products.

3. The advanced section hides value.
   Opening "进阶视角 · CAGED / 根音 / 练习" does not reveal enough content in the first viewport. It should either scroll into the opened panel, show a preview summary, or expose the first advanced panel immediately.

4. Stage 1 learning is high density.
   Ten chord cards, chord diagrams, tips, sound buttons, and completion buttons all compete at once. The task is clear, but the screen reads more like a reference sheet than a coached lesson.

5. Locked stages do not explain themselves.
   Locked stage buttons are visible and clickable-looking, but they silently do nothing. Users need an explicit locked state and a short unlock reason.

6. Import flow starts with documentation instead of action.
   The new-song page leads with a large example block. The textarea and import button should be visible sooner, with the example collapsible or placed beside the input on desktop.

7. Completion actions are repetitive and small.
   "我学会了" is repeated on each chord card. On desktop and mobile these controls are functional but easy to miss compared with the large visual chord cards.

## Accessibility Risks

- The fretboard uses many empty buttons for fret cells. In the captured state, 72 visible button controls have no accessible text.
- Several fretboard touch targets are under 44px tall, especially on mobile lower frets and string labels.
- Locked learning stages are not real disabled controls and do not expose `aria-disabled`.
- The learning progress bar has no `role="progressbar"` or aria value metadata.
- Status changes such as chord recognition, stage completion, and audio playback are visual/audio only from the screenshot evidence; they need live-region or text-state verification.
- Screenshot review cannot prove full keyboard support, screen-reader order, audio behavior, or WCAG compliance.

## Recommendations

1. Add a shared product-level header.
   Use a simple switch between "指板工具" and "歌曲陪练" on both surfaces. Add a primary CTA on the fretboard screen such as "用这个和弦开始练歌" or "去学一首歌."

2. Unify design tokens across both surfaces.
   Keep the dark fretboard as the premium product identity, then bring the learning flow closer through shared typography, buttons, radius, and accent colors. It does not need to become fully dark, but it should feel like the same product.

3. Improve first-run guidance on the fretboard.
   Keep the seeded Am7, but add a compact next-step strip: "点任意品位识别和弦", "展开 CAGED", "进入歌曲陪练." This gives users a path without adding a landing page.

4. Make advanced mode reveal immediate value.
   When opened, scroll the panel into view or show a one-line preview of CAGED, root anchors, and quiz. Make the opened state visibly different beyond border highlight.

5. Redesign stage 1 as a coached checklist.
   Group chords by difficulty or song section, show progress like "0/10 chords learned," and provide one persistent next action. Keep individual chord cards, but reduce repeated explanatory text inside every card.

6. Fix locked states.
   Use disabled semantics, `aria-disabled`, and a visible reason such as "先完成第1关解锁." A click on a locked stage should show the next required action.

7. Restructure import.
   Put the textarea and import button above the example. Make the example collapsible or side-by-side on desktop. Add a parsed preview before committing a new song.

8. Add accessibility labels and state semantics.
   Give fret buttons labels like "6弦 3品，按下选择 E", label string toggles, add `aria-live` for chord result changes, and expose the learning progress as a real progressbar.

## Evidence Limits

- This audit used local screenshots and DOM inspection only.
- I did not run a full keyboard-only pass, screen reader pass, contrast calculation, or real user test.
- Audio behavior was not judged beyond visible controls and code evidence.
