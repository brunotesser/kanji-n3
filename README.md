<div align="center">

# 漢字アプリ N3

**Learn Japanese from N5 to N3 — radicals, kanji and vocabulary with spaced repetition**  
Aprenda japonês do N5 ao N3 — radicais, kanji e vocabulário com repetição espaçada  
部首・漢字・語彙をSRSで学ぶ — N5からN3まで

---

![iOS](https://img.shields.io/badge/iOS-16%2B-black?style=flat-square&logo=apple)
![Capacitor](https://img.shields.io/badge/Capacitor-v8-4A90E2?style=flat-square)
![Vanilla JS](https://img.shields.io/badge/Vanilla-JS-F7DF1E?style=flat-square&logo=javascript)
![Offline](https://img.shields.io/badge/100%25-Offline-00b894?style=flat-square)
![Vocab](https://img.shields.io/badge/2113%2B-vocab_entries-9b59b6?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-brightgreen?style=flat-square)

</div>

---

## What is this? · O que é? · これは何？

An **iOS app** to study Japanese the structured way — starting from radicals, building up to kanji, then mastering 2113+ vocabulary words from JLPT N3.

Inspired by WaniKani's unlock system. **100% offline, free, open source.**

> **PT-BR:** App iOS para estudar japonês do zero ao N3. Começa pelos radicais, sobe para kanji, chega no vocabulário. Sistema SRS próprio. Sem internet, sem assinatura, sem paywall.  
> **日本語:** 部首から始め、漢字を習得し、N3語彙2113語以上をマスターするiOSアプリ。独自SRS搭載・完全オフライン・無料・オープンソース。

---

## Learning path · Trilha · 学習パス

```
  部首 Radicals          漢字 Kanji            語彙 Vocabulary
 ──────────────    ──────────────────    ──────────────────────
  Learn the         Build from            Master words built
  building blocks   radical parts         from known kanji
  of every kanji    N5 → N4 → N3          2113+ N3 entries

  🔵 Radical        🔴 Kanji              🟣 Vocab
  unlocks ──────▶   unlocks ──────────▶   SRS levels up
```

Every kanji is composed of radicals. Every vocab word uses known kanji.  
**Master the parts first — the rest unlocks automatically.**

---

## Screens · Telas · 画面

### 🏠 Home Screen

```
╔══════════════════════════════╗
║  🔥 12  dias · days · 日     ║  ← streak bar
║              best: 21        ║
╠══════════════════════════════╣
║                              ║
║   ↺  Revisar · Review (8)   ║  ← gold hero button
║      8 reviews pending       ║    (Review / Learn / ✓ All good)
║                              ║
╠══════╦═══════╦═══════╦═══════╣
║  3   ║  0    ║  2    ║  6    ║
║ hoje ║radical║ kanji ║ vocab ║  ← lessons available
║ today║  🔵   ║  🔴   ║  🟣   ║
╠══════╩═══════╩═══════╩═══════╣
║  [RADICAIS]  [KANJI]  [VOCAB]║  ← browse tabs
║──────────────────────────────║
║  一  二  三  四  五  六  七  ║
║  八  九  十  口  日  月  木  ║
║  火  水  金  土  山  川  田  ║
╚══════════════════════════════╝
```

---

### 📖 Lesson · Lição · レッスン

Three steps per item — see, reveal, absorb:

```
  Step 1 · Etapa 1           Step 2 · Etapa 2          Step 3 · Etapa 3
 ╔═══════════════════╗      ╔═══════════════════╗      ╔═══════════════════╗
 ║                   ║      ║   fire · 火 · 불  ║      ║  火山 (かざん)    ║
 ║        火         ║ ───▶ ║   か · ひ · カ    ║ ───▶ ║  volcano · 火山   ║
 ║                   ║      ║                   ║      ║                   ║
 ║    [ Reveal ]     ║      ║  [ Continue ]     ║      ║  🧠 AI mnemonic   ║
 ╚═══════════════════╝      ╚═══════════════════╝      ╚═══════════════════╝
   Kanji shown first          Reading + meaning          Real sentences +
   何? What is this?          revealed                   AI-generated story
```

---

### 🔁 Review · Revisão · 復習

```
╔══════════════════════════════╗
║                              ║
║           火山               ║  ← word shown
║                              ║
║  What is the reading?        ║
║  Qual é a leitura?           ║
║  読み方は？                  ║
║                              ║
║  ╔════════════════════╗      ║
║  ║  かざん           ░║      ║  ← type answer
║  ╚════════════════════╝      ║
║                              ║
║  ✓ correct → SRS advances   ║
║  ✗ wrong  → back to start   ║
╚══════════════════════════════╝
```

---

### 📊 SRS Levels · Níveis · レベル

```
  New ──▶ [1] ──▶ [2] ──▶ [3] ──▶ [4] ──▶ [5] ──▶ Burned 🔥
           4h      8h      1d      2d      1w
                   Apprentice       Guru     Master  Enlightened
```

Correct answer → advance. Wrong answer → reset.  
The app schedules your next review automatically — you just show up.

> **PT:** Cada acerto avança. Cada erro reinicia. O app agenda a próxima revisão automaticamente.  
> **JP:** 正解で進み、不正解でリセット。次の復習は自動でスケジューリング。

---

## Database · Base de dados · データ

| Collection | Entries | Notes |
|---|---|---|
| `RADICAL_DB` | N5/N4/N3 | Visual mnemonics, readings, meanings |
| `KANJI_DB` | N5 → N3 | Linked to radicals + vocab |
| `VOCAB_DB` | **2113+** | Source: Nihongo no Mori N3 |
| `VOCAB_SENTENCES` | Per word | Furigana + PT-BR translation |

Categories in `VOCAB_DB`:
`名詞` `カタカナ語` `接続詞 (17)` `接尾語 (187)` `接頭語 (30)` `慣用表現 (28)` `敬語 (47)` `数え方 (39)` `動詞 (290)` `い形容詞` `な形容詞`

---

## Tech · Stack · 技術

```
iOS Wrapper     Capacitor v8.3.1
Frontend        HTML + CSS + Vanilla JS  (no framework — iOS WKWebView 3s timeout)
Storage         localStorage  (100% offline, zero backend)
AI Mnemonics    Anthropic API — claude-sonnet  (optional, BYO key)
Build tool      Xcode via npx cap sync ios
App ID          com.vini.kanjin3
```

**Why Vanilla JS?**  
iOS WKWebView enforces a 3-second script parse timeout. A single vanilla file is faster to parse than any React/Vue bundle on constrained memory devices.

---

## Run it · Como rodar · 動かし方

```bash
# Clone
git clone https://github.com/brunotesser/kanji-n3.git
cd kanji-n3

# Install
npm install

# Preview in browser
open www/index.html

# Run on iPhone
npx cap sync ios
npx cap open ios
# Xcode → Product → Run (⌘R) on physical device
```

**AI mnemonics** require an Anthropic API key. Add it as `'x-api-key': 'YOUR_KEY'` in the fetch headers inside `generateMnemonic()` in `www/index.html`. Without it, the app works fully — mnemonics just won't auto-generate.

---

## Contributing · Contribuindo · 貢献

PRs welcome, especially:

- 🈶 **More vocab** — N2/N1 entries
- 🧠 **Better mnemonics** — visual stories for kanji/radicals  
- 📱 **Android** — Capacitor supports it, needs testing
- 🌐 **English UI** — currently PT-BR first
- 🐛 **Bug reports** — open an issue

```bash
git checkout -b feat/your-contribution
# make changes → open PR
```

---

## License

MIT — free to use, modify, redistribute.

---

<div align="center">

Built in Tokyo · 東京 · Tóquio  
**[Bruno Tesser](https://brunotesser.jp)** · [@brunotesserjapao](https://www.youtube.com/@brunotesserjapao)

*"The best time to start studying kanji was yesterday. The second best time is now."*  
「漢字の勉強を始める最良のタイミングは昨日。次は今。」  
*"O melhor momento para começar a estudar kanji foi ontem. O segundo melhor é agora."*

</div>
