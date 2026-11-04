# Study Coach

A single-file web app that builds study lessons from a topic or uploaded documents and teaches them aloud, with quizzes between segments, a final assessment, visual aids, a study guide and a PowerPoint export. It also keeps a lesson library and records study time, reviews and quiz attempts.

## Features
- Build a lesson from a topic, pasted notes, or uploaded PDF, Word, PowerPoint, text or Markdown files.
- Contents page: start any segment in any order.
- Spoken narration (browser text-to-speech) shown as bullets, with hands-free or tap-to-answer quizzes.
- Evidence rating on each segment (High, Moderate, Low, Insufficient).
- Library with categories, search and sort, synced per user.
- Study data: time per lesson and segment, sessions and reviews, quiz attempts, delayed retention check, CSV export.
- Optional natural voice: Kokoro-82M (Apache-2.0) via kokoro-js, run in the browser; British and American female voices. Falls back to the device voice if the model cannot load.
- Downloads: PowerPoint, study guide (.md, .html), lesson file (.json).

## Runtime
`index.html` is built to run as a Claude Artifact. These features use Claude artifact runtime capabilities and do not work when the file is opened elsewhere (for example GitHub Pages):
- `sample`: lesson generation
- `db` and `user`: the synced library
- `downloads`: saving files

Declared capabilities: `{"sample":{},"downloads":true,"db":{},"user":{}}`

Outside Claude, only audio, quizzes and the study guide for lessons already in the page work, and lessons are kept in the browser's localStorage.

## Notes
- Lessons and study data live in the user's Claude account, not in this repo. Back them up with each lesson's .json download and the study-data .csv download.
- Browser voices vary by device. Pick a British or other natural voice under Audio settings.
- Lesson text is written by Claude. Check clinical, legal and exam-critical details against primary sources.
