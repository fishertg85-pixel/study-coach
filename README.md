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
- Add material: add new segments from pasted or uploaded material, or revise one segment, with undo, segment removal and an update history.
- Exam practice: board-style questions written fresh from a lesson each time (K-type, scenario questions that do not name the answer, single best answer), with shuffled answer order, rationales and the source passage.
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

- **Courses**: lessons are grouped into courses (the lesson's course field). A course screen lists its lessons in order (move up/down, move to another course, rename), shows course-level study data, and offers course-wide exam practice drawn from every lesson (attempts are saved in a per-course record).
- **Add material and reorganize a course**: on a course screen, paste or upload new material. Claude plans the fewest topic-coherent lessons (new content folded in, overlaps merged, untouched segments kept verbatim), you review the plan, then it writes only the new or rewritten segments. Previous lessons are moved to a "(previous)" course.
