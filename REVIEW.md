# Boricua Flashcards Expert Review

## Executive summary

Boricua Flashcards has a strong foundation: it is fast, static, GitHub Pages-friendly, visually distinctive, and already aimed at a real learner's class notes. The current production `index.html` is the right product direction because it adds Daily, Study, Quiz, Visuals, and Progress, but it is too compressed and has a smaller learning dataset than `legacy-index.html`. The legacy app has the stronger vocabulary deck, examples, spaced-repetition progress, settings, notes, export/import, and Puerto Rico content. The best next release should merge those strengths into one primary app: keep the V2 learning loop and visual grammar, restore the richer deck and progress model, and improve accessibility, quiz filtering, weak-focus categories, and beginner-friendly grammar explanations.

The app should remain vanilla HTML/CSS/JS for now. A framework would add build and deployment overhead without solving the most important product issues. The next architectural move should be a light split into `data.js`, `storage.js`, `app.js`, and `styles.css`, but only after the current integrated app is stable.

## Senior software engineer findings

- Architecture: The live `index.html` is a minified one-file app, which is hard to review or safely extend. `legacy-index.html` is readable and more maintainable, but it lacks the newer Daily and Visuals tabs. A formatted single-file app is acceptable for this release; the next step should be a small module split.
- Data model: The legacy `DECK` model is stronger because each card has an id, category, Spanish, English, note, and example pair. The live V2 model is compact but too small and less durable. Grammar drills should be first-class cards or drill objects with focus tags.
- Progress: Legacy spaced-repetition boxes, due dates, XP, streak, settings, export, and import are worth preserving. V2's `boricuaV2` key needs a migration fallback so recent users do not lose XP.
- State management: Existing logic mixes rendering, scoring, data, and storage in one script. That is acceptable short-term but should be separated before adding typed answers, audio, note import, or generated drills.
- Bugs and brittleness: The live V2's due logic is only a seen-count threshold; legacy has a better SRS model. The live quiz selection lacks a full grammar/visuals section. Weak-focus tracking is too generic and should point to actionable learning categories.
- GitHub Pages readiness: The app works well as static files. `index.html`, `404.html`, `manifest.webmanifest`, icons, and `sw.js` should stay root-relative/simple. Service-worker cache versions must bump on every app-shell update.
- Offline/PWA: The service worker caches the core shell and icons. It should also cache `404.html` and the preserved reference/legacy pages when practical.
- Accessibility: Buttons are mostly usable, but legacy tabs and chips used `div` controls. Navigation should use real buttons, clear labels, visible focus states, and live feedback regions.
- Future support: Audio, typed answers, note import, spaced repetition, and generated drills are all feasible with the current local-only model if the deck/drill schema is clarified.

## Senior web UX/UI designer findings

- First impression: The Puerto Rico/Old San Juan theme is memorable and friendly. It supports the learner's motivation, especially with the flag logo and bright palette.
- Clarity: Daily/Study/Quiz/Visuals/Progress is a clearer product than a flashcard-only app. The header should describe the app as a daily Spanish practice tool, not just a card deck.
- Navigation: The five core tabs should be first-class. Notes and Settings can remain available as secondary tabs because this is still a personal study app.
- Mobile: Cards and controls are generally mobile-friendly, but tab rows need wrapping or grid behavior, and tap targets should stay at least 44px tall.
- Visual hierarchy: The app should lead with today's goal and a warmup prompt, then move to recall and grammar. Avoid oversized decorative panels that compete with learning content.
- Theme: Puerto Rico colors and Old San Juan accents work best as structural color, not as background noise. Panels need high opacity and strong text contrast.
- Visual grammar: Timeline metaphors are useful, but labels must say what they mean: present = now/habit, preterite = completed dot, imperfect = repeated/background line, future = later arrow.
- Feedback: Correct/incorrect states should show the answer and a short reason, not just color.
- Accessibility: Add `aria-live` feedback, visible focus outlines, semantic buttons, labels for selects, no color-only feedback, and reduced-motion handling.

## Ed tech product strategist findings

- Learning model: The app should be a daily retrieval loop, not a browseable glossary. Daily should sequence warmup, study, quiz, grammar, and sentence production.
- Retrieval practice: Study and Quiz both support retrieval. Quiz should include section selection and grammar drills, not just vocabulary translations.
- Spaced repetition: The legacy box model is a good start. The app should keep due dates, card boxes, seen counts, correct counts, and wrong counts locally.
- Interleaving: Mixing vocabulary, verbs, Puerto Rico words, class notes, and tense decisions will improve transfer. The learner also needs focused modes when a category is weak.
- Feedback: Feedback should explain why a tense or ser/ir choice is correct. For vocabulary, examples should show the word naturally.
- Transfer: Sentence production prompts are essential. The app should ask the learner to say or write sentences anchored in Puerto Rico contexts.
- XP and weak focus: XP is motivating only if it points toward meaningful work. Weak-focus categories should become recommendations like "practice preterite vs imperfect" or "review Puerto Rico vocabulary."
- Growth path: This can become a polished learning product if the content schema supports audio, typed responses, mastery, streaks, lesson packs, and imported notes.
- Local data to track: due date, box, seen, correct, wrong, last seen, quiz correct/answered, weak focus counts, daily tasks, daily XP, settings, and optional typed-answer attempts.

## Spanish language acquisition and Puerto Rican Spanish findings

- Accuracy: Most content is appropriate for beginner Spanish. The app should distinguish general Spanish from Puerto Rican usage using notes, not imply PR words are universal.
- Naturalness: Many examples are simple and useful. Some should be made more communicative: "Tengo pocos chavos" is better than isolated "chavos"; "¿A dónde fueron ustedes?" is clearer than only "¿A dónde fueron?"
- Puerto Rican vocabulary: `guagua`, `china`, `zafacón`, `guineo`, `habichuelas`, `nevera`, `mahones`, `chavos`, `janguear`, `pana`, `corillo`, `nítido`, `brutal`, and `bregar` should remain marked as Puerto Rico/Caribbean/casual where appropriate.
- Grammar explanations: Beginner grammar should focus on meaning first. Preterite is a completed event; imperfect is background, repeated, or ongoing past. Ser/ir preterite share forms but context decides meaning.
- Isolated words: The app should prioritize phrases and sentence chunks. Each non-verb should have 2-3 short examples, and verbs should show tense examples.
- Tense sequencing: Present, preterite, imperfect, and future are acceptable because the learner's class is already there. The app should avoid overloading with full conjugation charts before meaningful examples.
- Ser vs ir: The key distinction should be movement/destination vs identity/description/event. Examples must include destinations for ir and descriptions/events for ser.
- Pronunciation/listening: The next major content improvement should be audio or speech prompts, even if initially browser speech synthesis.
- Pronouns: Puerto Rican Spanish uses `ustedes` for plural "you"; `vosotros` can be omitted for this learner. The app should show `tú`, `usted`, and `ustedes` clearly.
- Speech patterns: Casual PR words like `janguear` and `chavos` should be labeled casual. Do not overdo slang at the expense of high-frequency core Spanish.

## Top 10 risks or gaps

1. The live app is minified and difficult to maintain.
2. The live app's deck is much smaller than the richer legacy deck.
3. Two localStorage schemas exist without a clear migration path.
4. Weak-focus tracking is too broad to guide learning.
5. Quiz filters do not fully cover grammar/visual drills.
6. Daily tasks can become XP checkboxes unless tied to actual practice.
7. Visual grammar tools need stronger explanations and feedback.
8. Accessibility is limited by non-button controls and sparse live feedback.
9. Offline cache can serve stale app shells if cache versions are not bumped.
10. The content model is not yet ready for audio, typed answers, or imported notes.

## Top 10 improvements ranked by impact and effort

1. High impact, medium effort: Use one primary integrated app that combines V2 Daily/Visuals with the richer legacy deck and SRS.
2. High impact, low effort: Add migration from `boricuaV2` to the richer progress state.
3. High impact, low effort: Add `Grammar / Visuals` and `Due now` quiz filters.
4. High impact, medium effort: Add actionable weak-focus categories.
5. High impact, medium effort: Restore verb tense examples and non-verb usage examples in Study and Quiz feedback.
6. Medium impact, low effort: Use semantic buttons and focus styles for tabs/chips.
7. Medium impact, low effort: Sync `404.html` and bump `sw.js`.
8. Medium impact, medium effort: Add Daily task completion and sentence prompt tracking.
9. Medium impact, medium effort: Add visual grammar trainers into the main app instead of a separate page only.
10. Medium impact, high effort: Split into modules after the integrated shell stabilizes.

## What should be done now

- Make `index.html` the strongest integrated app, not a redirect.
- Preserve `legacy-index.html`, `integrated-v2.html`, and `visuals.html`.
- Reuse the richer legacy vocabulary deck and examples.
- Keep the legacy SRS model and add fallback migration from V2 progress.
- Add Daily, Visuals, grammar drills, class phrase cards, quiz section filtering, and weak-focus recommendations.
- Improve accessibility with semantic controls, focus states, labels, and live feedback.
- Sync `404.html`, keep manifest registration, and bump the service-worker cache.

## What should be deferred

- Full module split into separate JS/CSS files.
- Audio recording or speech recognition.
- AI-generated drills or automatic note OCR/import.
- Account sync or cloud storage.
- Full typed-answer grading.
- Full CEFR curriculum sequencing.
- Teacher/admin authoring tools.

## Proposed app architecture

For the next release, a formatted single-file `index.html` is acceptable because GitHub Pages deployment stays simple and there is no build step. The file should be structured clearly:

- CSS variables and layout styles.
- Semantic HTML sections for Daily, Study, Quiz, Visuals, Progress, Notes, and Settings.
- Data constants: deck, tense examples, usage examples, grammar drills.
- Storage helpers: load, migrate, save, export/import.
- Learning helpers: filters, due logic, SRS marking, weak-focus tracking.
- Rendering helpers for each tab.
- Event binding at the bottom.

Future split:

- `index.html`: app shell.
- `styles.css`: visual system.
- `data.js`: cards, examples, drills.
- `storage.js`: migration, SRS, localStorage.
- `visuals.js`: grammar trainers.
- `app.js`: render and event coordination.

## Proposed learning model

- Daily loop: warmup sentence, study cards, quick quiz, visual grammar, and production prompt.
- Study: bidirectional recall with examples after reveal.
- Quiz: multiple-choice recall by section, including grammar/visual drills.
- Visuals: meaning-first tense timelines, conjugation builder, preterite/imperfect, ser/ir, and class phrases.
- Progress: SRS boxes, due cards, mastery meters, weak-focus recommendations, badges, and local export/import.
- Feedback: every miss increments card progress and weak-focus categories.

## Proposed UX flow

1. Open on Daily.
2. Complete a warmup prompt aloud.
3. Study a few due cards.
4. Take a focused quiz.
5. Use Visuals for the weakest grammar category.
6. Check Progress for recommendations.
7. Use Notes and Settings when needed, not as the primary flow.

## Puerto Rican Spanish content strategy

- Keep high-frequency general Spanish as the base.
- Keep Puerto Rican vocabulary in its own marked pack.
- Use Puerto Rico contexts in examples: San Juan, Viejo San Juan, Santurce, la playa, la guagua, arroz con habichuelas.
- Mark casual words clearly.
- Teach `ustedes` as the normal plural "you" form for the learner.
- Favor useful chunks: `¿Cómo fue tu día?`, `¿A dónde fueron ustedes?`, `No tengo chavos`, `Voy en guagua`.

## Accessibility checklist

- Use real buttons for tabs, chips, and choices.
- Add visible focus outlines.
- Label all selects.
- Keep touch targets at least 44px tall.
- Do not rely on color alone for correct/incorrect feedback.
- Use `aria-live` for feedback and score messages.
- Keep text contrast strong over themed backgrounds.
- Support keyboard tabbing through all controls.
- Respect reduced-motion preferences.
- Keep mobile line lengths and scrolling comfortable.

## Suggested GitHub issues or backlog items

1. Split app into `data.js`, `storage.js`, `app.js`, and `styles.css`.
2. Add typed-answer mode with forgiving accent/case handling.
3. Add browser speech synthesis for pronunciation examples.
4. Add audio/listening prompts for Puerto Rican Spanish.
5. Add note import workflow for class vocabulary.
6. Add a proper lesson pack model.
7. Add a "practice weak focus" mode.
8. Add review history charts.
9. Add editable custom cards stored locally.
10. Add automated smoke tests for the static app.

## Acceptance criteria for the next release

- `index.html` loads the integrated app directly with no redirect dependency.
- `legacy-index.html`, `integrated-v2.html`, and `visuals.html` remain available.
- The app shows Daily, Study, Quiz, Visuals, Progress, Notes, and Settings.
- Daily warmup and tasks render and save completion.
- Study shows the richer deck and reveals examples.
- Verb cards show present, preterite, imperfect, and future examples where available.
- Quiz section selector includes All, Verbs, Common words, Puerto Rico, Class notes, Grammar / Visuals, and Due now.
- Visuals include timeline cards, conjugation builder, preterite vs imperfect trainer, ser vs ir trainer, and class phrase cards.
- Progress updates after correct and incorrect answers.
- Weak-focus recommendations show actionable categories.
- `localStorage` loads existing `boricua_flashcards_v2` progress and can migrate basic `boricuaV2` progress.
- `manifest.webmanifest` and `sw.js` remain valid.
- `404.html` matches the app shell.
- Local browser test shows no console errors.
