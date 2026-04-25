# Changelog

## Next release

- Fixed overlapping text in the Visuals timeline by moving tense explanations into stable captions.
- Changed Progress category bars to update gradually from SRS box progress instead of only after cards are mastered.
- Polished the Puerto Rican flag logo so the white star is centered in the blue triangle.
- Reworked the Visuals timeline cards with clearer past, now, future, completed-action, ongoing-past, and future-arrow graphics.
- Added a regular verb tense endings chart for present, preterite, imperfect, and future inside the Visuals section.
- Added `REVIEW.md` with an expert review across engineering, UX, ed tech, and Puerto Rican Spanish teaching lenses.
- Rebuilt `index.html` as the primary integrated language-learning app with Daily, Study, Quiz, Visuals, Progress, Notes, and Settings.
- Preserved the richer legacy vocabulary deck, Puerto Rico pack, class-note cards, verb tense examples, non-verb usage examples, spaced repetition, settings, export, and import behavior.
- Added grammar/visual drill cards for preterite vs imperfect and preterite ser vs ir.
- Added quiz section support for `Grammar / Visuals` and `Due now`.
- Added weak-focus tracking for actionable categories such as verb conjugation, preterite, imperfect, preterite vs imperfect, ser vs ir, Puerto Rico vocabulary, class notes, and vocabulary.
- Added migration fallback from the recent `localStorage.boricuaV2` state into the richer `boricua_flashcards_v2` progress model.
- Synced `404.html` with the primary app shell.
- Bumped the service-worker cache to `boricua-flashcards-v9` and cached the main shell plus preserved reference pages.
