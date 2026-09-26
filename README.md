# tutor

An agent skill that teaches university courses for two goals at once: **the top grade on the exam**
and **understanding that outlasts it**. Works with Claude Code, Codex, and Antigravity; uses an
Obsidian vault as the textbook.

*[Türkçe açıklama aşağıda.](#türkçe)*

## What it does

- **Probe** — graded quizzes find exactly where your knowledge ends (a floor you get right, a ceiling
  you miss).
- **Plan** — the topic becomes a small dependency map: face-value truths at the top, your goal at the
  bottom. You approve it before teaching starts.
- **Teach** — node by node: why we need it → build it → connect it → check it. Socratic when you can
  reason your way there, narrated when you can't.
- **Exam mode** — reads the instructor's slides and past exams, triages topics by weight × weakness,
  writes new questions in the instructor's style, grades open answers like the instructor would.
- **Spaced review** — every topic leaves recall prompts with due dates; due reviews come first each
  session.
- **Everything lands in your vault** — one markdown file per topic, written live, with mermaid maps
  and LaTeX. Start in Claude Code, continue in Codex: the lesson file is the handoff.

## Install

The skill is the `skills/tutor/` folder. Put it where your agent looks for skills:

| Agent | Global | Per project (e.g. your vault) |
| --- | --- | --- |
| Claude Code | `~/.claude/skills/tutor/` | `.claude/skills/tutor/` |
| Codex | `~/.codex/skills/tutor/` | `.agents/skills/tutor/` |
| Antigravity | `~/.gemini/config/skills/tutor/` | `.agents/skills/tutor/` |

```bash
git clone https://github.com/zekierman/tutor
cp -r tutor/skills/tutor ~/.claude/skills/        # repeat for the others you use
```

Then open your agent inside your Obsidian vault and say *"let's study <topic> for <course>"*. On first
run it asks where your courses live and creates `learner.md` — your profile. Edit it: how you learn,
what you hate, your courses.

## Layout in your vault

```
Courses/
├── learner.md          # your profile
└── Data Structures/
    ├── _course.md      # exams, sources, topic map, exam intel, error log
    └── linked-lists.md # map, frontier, sessions, review table
```

Obsidian renders it: open the lesson file next to the terminal. The terminal is the classroom,
Obsidian is the textbook. Works on a tablet too if your vault syncs.

## Credits

Teaching principles (unconditional truths first; "how could I have discovered this?"; probe → plan →
teach) are adapted from [amosblomqvist/learn](https://github.com/amosblomqvist/learn), a pi
configuration. This is an independent rewrite for Claude Code / Codex / Antigravity with an exam
focus.

## License

MIT

---

## Türkçe

Üniversite dersleri için bir ajan skill'i. İki hedef: **sınavdan en yüksek not** ve **sınavdan sonra
da kalan gerçek kavrayış**. Claude Code, Codex ve Antigravity ile çalışır; ders kitabı olarak Obsidian
kasanı kullanır.

- **Yokla:** Puanlı sorularla bilginin tam nerede bittiğini bulur.
- **Planla:** Konuyu küçük bir bağımlılık haritasına çevirir; sen onaylamadan anlatmaya başlamaz.
- **Öğret:** Düğüm düğüm ilerler: neden gerekli → kur → bağla → kontrol et.
- **Sınav modu:** Hocanın slaytlarını ve çıkmış soruları okur, konuları ağırlık × zayıflık sırasına
  koyar, hocanın tarzında yeni sorular yazar, açık uçlu cevabını hoca gibi puanlar.
- **Aralıklı tekrar:** Her konu tarihli tekrar soruları bırakır; her oturum vadesi gelen tekrarla
  başlar.
- **Her şey kasana yazılır:** Konu başına bir markdown dosyası, canlı yazılır. Claude Code'da başlayıp
  Codex'te devam edebilirsin; devir ders dosyasıyla olur.

Kurulum için yukarıdaki tabloya bak. İlk çalıştırmada `learner.md` profilini oluşturur ve dersi
senin dilinde anlatır.
