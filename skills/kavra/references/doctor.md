# Check mode ("kavra kontrol", "is my study setup healthy?")

Read-only. Report first; fix only what the learner approves. Get today's date from the system.

Run each check and mark it 🟢 / 🟡 / 🔴:

| # | Check | 🟢 | 🔴 |
| --- | --- | --- | --- |
| 1 | `learner.md` exists and has `language` and `courses_root` | both set | missing file or fields |
| 2 | Every course folder has `_course.md` | all | a folder without it |
| 3 | Review queue tables parse: dates are `YYYY-MM-DD`, `Step` is 0–4 or done, columns intact | all rows valid | a malformed row (name it) |
| 4 | Overdue reviews (`Next` < today) | 0 | any — report count per course and the oldest date |
| 5 | Exams: dates present and not all in the past | next exam known | no dates, or every exam passed (course may be finished) |
| 6 | Topic map ↔ files: every linked topic file exists, every topic file is on the map | in sync | orphan files or dead links (list them) |
| 7 | No duplicate sections: each role (map, frontier, review queue…) appears once per file | clean | same role twice (e.g. an English and a Turkish heading) |
| 8 | Frontmatter is flat `key: value` only | flat | nested lists/objects |
| 9 | Topics marked `solid`/`exam-ready` have evidence (a produce task and a transfer check in the lesson file) | yes | status without evidence |

Output one table (check, status, finding), then one fix line per 🔴, then a one-sentence verdict.
For overdue reviews, the fix is not "delete them" — offer a short mixed review round now.
