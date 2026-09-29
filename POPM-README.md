# SAFe® POPM — Quiz

A Kahoot-style quiz app for SAFe **Product Owner / Product Manager** training. Two ways to play:

- **🎬 Live game** — you host on a big screen, everyone scans one QR code and answers the **same questions in sync**. After each question the room sees the correct-answer stats and a live podium, then you advance everyone together.
- **📝 Self-paced practice** — six independent single-lesson quizzes people can take on their own, any time.

---

## Files

| File | What it is |
|------|------------|
| `popm-index.html` | The hub / landing page — links to everything |
| `popm-host.html` | **Live game host** (the screen you present from) |
| `popm-play.html` | **Player pad** — what participants open on their phones |
| `popm-lesson-1-exploring-product-roles-and-responsibilities.html` | Self-paced quiz — Lesson 1 |
| `popm-lesson-2-preparing-for-pi-planning.html` | Self-paced quiz — Lesson 2 |
| `popm-lesson-3-leading-pi-planning.html` | Self-paced quiz — Lesson 3 |
| `popm-lesson-4-executing-iterations.html` | Self-paced quiz — Lesson 4 |
| `popm-lesson-5-executing-the-pi.html` | Self-paced quiz — Lesson 5 |
| `popm-lesson-6-get-certified.html` | Self-paced quiz — Lesson 6 |

> Keep all files in the **same folder** (repo root). The pages link to each other with relative paths.

Each lesson has a larger question bank than it uses, so every round draws a **random** subset — quizzes don't repeat the same questions each time.

### The 6 lessons

1. 🧭 Exploring Product Roles and Responsibilities
2. 📅 Preparing for PI Planning
3. 🗣️ Leading PI Planning
4. ⚙️ Executing Iterations
5. 🏁 Executing the PI
6. 🎓 Get Certified

---

## Hosting on GitHub Pages (free)

1. Put these files in a **public** repository (they can live in the same repo as your Scrum Master game).
2. **Add file → Upload files** → drag in all the `popm-*.html` files (plus this README). Keep them in the **root**, then **Commit changes**.
3. **Settings → Pages → Source:** *Deploy from a branch* → Branch **main**, folder **/ (root)** → **Save**.
4. Wait ~1–2 minutes. Your site goes live at:
   ```
   https://YOUR-USERNAME.github.io/YOUR-REPO/
   ```

**Your links**

- Hub: `.../popm-index.html`
- Host a live game: `.../popm-host.html`
- Players join: `.../popm-play.html` (the QR code handles this automatically)
- A single lesson: `.../popm-lesson-1-exploring-product-roles-and-responsibilities.html`

To update later: edit a file on GitHub (pencil icon → commit) or re-upload it. Pages redeploys within ~1–2 minutes.

---

## Firebase (already configured)

The live game uses **Firebase Realtime Database** so every player writes to their own path and simultaneous answers never collide. **Your Firebase config is already pasted into `popm-host.html` and `popm-play.html`** — the same project as your Scrum Master game.

Because each game generates its own unique PIN, the POPM and Scrum Master games can share one Firebase project **without ever colliding**. You can even run both at the same time.

**Database rules** (Firebase console → Realtime Database → Rules) should allow read/write for a classroom session:
```json
{
  "rules": {
    "games": { ".read": true, ".write": true }
  }
}
```

**Notes on test-mode rules:** open rules are fine for classroom sessions with non-sensitive data, but they typically **expire after ~30 days** — just re-open them (or re-apply the rule above) when they lapse. Don't store anything sensitive.

**If the live game won't connect once hosted:** in the Firebase console check **Authentication → Settings → Authorized domains** and make sure `YOUR-USERNAME.github.io` is listed, and confirm the `databaseURL` in the config matches your database.

---

## Running a live session

1. Open **`popm-host.html`** on the machine connected to the projector.
2. Pick a lesson → **Create game**. A fresh **PIN + QR code** is generated (new every launch), and the question set is locked in — **identical for everyone**.
3. Ask the room to scan the QR (or go to `popm-play.html` and type the PIN), enter a name — you'll see them join live.
4. Click **Start**. For each question:
   - The big screen shows the question, four colored answers, and a countdown.
   - Phones show the same answers as tappable buttons.
   - When the timer ends (or everyone's answered), the reveal shows **% correct**, a breakdown of each option, and the **live leaderboard**.
5. Click **Next** to advance everyone. After the last question, the **🥇🥈🥉 podium** shows the winners.

The game auto-cleans itself from the database when you close the host tab.

---

## Running self-paced practice

Just share a lesson link (e.g. `.../popm-lesson-3-leading-pi-planning.html`). Each start page has a QR code so people can open it on their phones. These can optionally use a shared leaderboard — see the config comment inside each lesson file.

---

## Customizing questions

- **Live game:** questions are embedded in `popm-host.html` (the `LESSONS` object near the bottom of the script).
- **Self-paced:** each `popm-lesson-*.html` keeps its own bank in its file (the `LESSON` object).

Edit the text, answers, or the `correct` index there. The correct answer is identified by index, and answer options are shuffled automatically at play time.

---

*Built for SAFe® Product Owner / Product Manager training. SAFe is a registered trademark of Scaled Agile, Inc.*
