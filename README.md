# ⛪ Pilgrim's Path II — The Road to Constance

A pixel-art study game for the **Church History I final exam**, covering Lessons 7–12: Augustine to the proto-reformers, **397–1415 A.D.**

Sequel to [Pilgrim's Path](https://beneisenberg.github.io/pilgrims-path/) (the mid-term game, 35–451 A.D.), which remains online.

**Everything is in one `index.html`** — no build step, no dependencies, no server. Open the file and play; it works offline once loaded.

---

## The game

### 📖 Story: The Road to Constance
The main mode. It is 1415, and you carry the monastery's *Chronicle of a Thousand Years* from Augustine's besieged Hippo to the Council of Constance. Six chapters, one per lesson, each built from narration, mastery gates, wayside inns, optional review detours, and boss battles — accompanied by Balaam, a sarcastic pack mule who declines to explain his lifespan.

The eight bosses are drawn from the course material: the Donatist Divider, Pelagius the Self-Made, the Eight Whispers (Evagrius' evil thoughts), the Rift Wraith of 1054, the King's Shadow (Becket's murderers), Simon the Simoniac, the Pyre of Constance — and THE EXAMINER, who unrolls a scroll a thousand years long.

Chapter **gates** won't open until you've actually mastered that chapter's dates and figures, so the story can't be rushed past the studying.

### 🔥 Daily Pilgrimage
A short spaced-repetition session targeting exactly what your memory is about to lose, with a streak counter.

### Free Play
- **Timeline Trek** — match events to years across all 20 official dates
- **Order the Ages** — sort shuffled events chronologically, then watch the pilgrim walk your answer down the road
- **Disputation Hall** — the lesson review questions, drillable by lesson (7–12) or all at once
- **Saints & Scholars** — "who am I?" with 25 figures; each has seven clues, five dealt at random per encounter, so no single detail can be memorized in place of the rest. Wrong answers are drawn from contemporaries.

### 📚 The Cloister
- **Study Chapel** — full reference: the 20 dates with mnemonics, every figure's dossier, the reform movements, East-vs-West distinctives, atonement theories side by side, and the Cloister Joke Book (memory aids, allegedly)
- **THE FINAL** — a 30-question mock exam, unlocked by completing the story
- **Wardrobe** — earned outfits and accessories

---

## The 20 dates

| | | | |
|---|---|---|---|
| 397 Confessions | 426 City of God | 432 Patrick to Ireland | **529 Council of Orange** |
| **529 Benedict's Rule** | 622 Birth of Islam | 718 Boniface to the Germans | 800 Charlemagne crowned |
| 860 Cyril & Methodius | 988 Christianity to Russia | 1054 East–West Schism | 1093 Anselm to Canterbury |
| 1099 First Crusade | 1150 Paris & Oxford | 1175 Waldensians | 1208 Francis renounces wealth |
| 1215 Fourth Lateran | 1272 Summa Theologica | 1378 Great Schism | 1415 Hus burned |

The game deliberately drills the two classic traps: **529 holds two events**, and **1054 (East–West) is not 1378 (Great Schism)**.

---

## Wardrobe unlocks

Chapter outfits are earned by completing story chapters. The rest:

| Item | How to earn it |
|---|---|
| 🧢 Ball Cap | Reach 500 XP |
| 👱 Beach-Blonde Wig | Score 2,000+ in Saints & Scholars |
| 🎩 Top Hat | Reach Bishop rank (2,800 XP) |
| 🎓 John Calvin's Cap | Finish the story — reach Constance |
| 🤵 Tuxedo | Earn an A on THE FINAL |
| 🩱 Pink Polka-Dot Swimsuit | Flee a boss battle |
| 🗡️ Sting | Defeat three different bosses |
| 💍 The One Ring | Defeat the Examiner |

Accessories like the Pilgrim's Staff, Chronicle Scroll and Gilded Cross arrive through the ten achievements.

---

## Deploying to GitHub Pages

1. Create a new repository (e.g. `pilgrims-path-2`).
2. Upload `index.html`, `README.md`, and `.nojekyll` to the repository root.
3. **Settings → Pages →** deploy from the `main` branch, `/ (root)` folder.
4. The game goes live at `https://<username>.github.io/pilgrims-path-2/` within a minute or two.

`.nojekyll` tells GitHub Pages to serve the file as-is rather than running it through Jekyll.

---

## Notes

**File size.** `index.html` is ~6 MB because both music tracks are base64-embedded inside it. That's well within GitHub's limits (the warning threshold is 50 MB), and it keeps the game a single portable file. First load pulls the whole thing; after that it's cached.

**Music.** Two loops: one for the road, one for boss battles, which swaps back automatically when the fight ends. Browsers block audio autoplay until the user interacts with the page, so the music starts on the first tap or keypress where autoplay is refused. There's a 🎵 toggle in the HUD.

To swap the tracks, replace the base64 payloads in the `MUSIC` constant near the top of the `<script>`:

```bash
base64 -w0 new-map.mp3      # paste after "data:audio/mpeg;base64," for MUSIC.map
base64 -w0 new-battle.mp3   # same for MUSIC.battle
```

96 kbps mono keeps the file small. Empty payloads are handled gracefully — the game simply runs with sound effects only.

**Saves.** Progress is stored in the browser under the key `pilgrim-save-2`, separate from the v1 game, and saves automatically after every scene, answer, and unlock. Clearing site data resets progress.

**Before publishing:** confirm the music tracks' license permits public redistribution, since they're embedded in a publicly served file.

---

## For future maintainers (human or AI)

The engine is data-driven: essentially all course content lives in constant arrays near the top of the script — `DATES`, `PEOPLE`, `BOSSES`, `RQ`, `STUDY_SECTIONS`, `CHAPTERS`, `STORY_SCRIPT`, plus `HATS` / `ROBES` / `ACCESSORIES` / `ACHIEVEMENTS`. Swapping the course content is mostly a matter of rewriting those arrays.

Invariants worth knowing before editing:

- **Spaced-repetition IDs are positional.** Boss questions are keyed `b<bossIndex>:<questionIndex>` and review questions `r<index>`, so *append* rather than reorder or delete, or existing saves will map progress onto the wrong items.
- `CH_BG`, `CH_SCENES`, `CHAPTERS` and `STORY_SCRIPT` must all have the same length (one entry per chapter).
- Every question needs exactly three wrong answers.
- **Answer options must not give themselves away**: no ALL-CAPS emphasis inside options, and the correct answer must not be conspicuously longer than the decoys. Elaborate the wrong answers to match rather than trimming the right one into uselessness.
- Timeline spacing is driven by `TL_PPY` (pixels per year); a wider date range needs a smaller value.

The v1 repository contains an `UPDATING.md` handoff guide with the full schema reference; the notes above supersede it wherever the two differ.

---

*Made with 🕯️ and spaced repetition. Luck is for the unprepared.*
