# Cryptogram

A browser-based substitution-cipher puzzle game. Each famous quote is encrypted with a random letter-substitution key, and your job is to crack it.

**▶ Play:** https://daeunmint.github.io/cryptogram/

<!-- Add a screenshot: upload screenshot.png to the repo and uncomment the line below -->
<!-- ![Cryptogram screenshot](screenshot.png) -->

## How to play

- Every letter in the quote is replaced by a different letter (no letter maps to itself).
- Tap a cell and type your guess, using the on-screen keyboard or a physical keyboard.
- Cells that share the same code letter are highlighted, but you fill in each one yourself.
- Wrong letters turn red right away.
- One or two letters are revealed at the start. Use **Hint** to reveal the selected cell.

| Key | Action |
|---|---|
| `A`–`Z` | Enter a letter |
| `Backspace` | Erase (moves back if the cell is empty) |
| `←` `→` | Move between cells |

## Features

- **Daily puzzle:** the same puzzle for everyone each day, generated from a date-seeded random key
- **Difficulty levels:** Easy / Normal / Hard (quote length and number of starting letters)
- **Scoring:** points from difficulty, speed, hints and misses
- **Badges:** 12 achievements such as *Flawless*, *Codebreaker* and *Week Warrior*
- **Letter counts:** frequency panel for each code letter
- Instant wrong-letter feedback and miss counter
- Completed letters are marked on the keyboard
- Google sign-in sync across browsers and devices, plus a manual save code
- Saved progress and personal records (best score and time per level, daily streak, recent solves)
- Mobile-friendly layout with light and dark themes

## Tech

- A single `index.html` file: HTML, CSS and vanilla JavaScript, no framework or build step
- Progress and records are stored in the browser with `localStorage`, and synced across devices with Firebase (Google sign-in + Firestore) when signed in
- Hosted on GitHub Pages

### Core logic

- **Derangement key:** shuffle `A–Z` with Fisher–Yates and reshuffle until no letter maps to itself.
- **Per-cell state:** guesses are stored by cell index, not by code letter, so matching letters are highlighted without being auto-filled.
- **Daily seed:** the date string is hashed into a seeded PRNG, so the quote, key and starting letters are identical for a given day.
- **Score:** `base + speed bonus − hint penalty − miss penalty`, with a higher base for harder levels.
- **Persistence:** game state is serialized to JSON on every move (debounced) and restored on load.

## Development notes

I prototyped this game with Claude (AI-assisted "vibe coding") and shaped it through repeated playtesting. Design decisions I made along the way:

1. **Starting letters:** revealed 1–2 letters at the start so a puzzle is approachable without hints.
2. **Instant feedback:** replaced a manual *Check* button with immediate red highlighting of wrong letters.
3. **Saved records:** added progress saving and personal stats so it feels like a real game.
4. **Longer quotes:** switched to longer quotes for more letter-frequency clues and a better challenge.
5. **Per-cell input:** changed from auto-filling every matching letter to highlighting them only, so the player does the solving.
6. **Miss counter and keyboard marks:** show how many wrong letters were entered and which letters are fully solved.
7. **Game systems:** added difficulty levels, a daily puzzle, letter-frequency help, scoring and badges.

## Roadmap

- [ ] PWA support (install to home screen, offline play)
- [x] Difficulty levels
- [x] Letter-frequency helper panel
- [x] Daily puzzle, scoring and badges
- [ ] Korean (Hangul) version with jamo-level substitution
- [ ] Android build with Capacitor

## Run locally

Download `index.html` and open it in any modern browser.
