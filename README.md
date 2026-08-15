# Board Study Games

A small collection of browser-based review games for psychiatry / internal
medicine residents and med students. The landing page lists every game; picking
one opens its board.

**▶️ Play: https://amangerian.github.io/MPboardstudy/**

## Games

| Game | Format | Covers |
|---|---|---|
| Antidepressant Jeopardy! | Jeopardy, 6 × 5 | SSRIs, SNRIs, atypicals, TCAs & MAOIs, receptor profiles, side effects & safety |
| Depression Jeopardy! | Jeopardy, 5 × 5 + Final | MDD criteria, specifiers, sleep architecture & course, TCAs & MAOIs, newer treatments |
| ABPN Neuro Jeopardy | Jeopardy, 6 × 5 | Epilepsy, stroke localisation, headache, neuropathy, cognitive impairment, CNS infection |
| ABPN Neuro: Double Jeopardy | Jeopardy, 4 × 5 + Final | Movement disorders, neuroimaging, functional neuroanatomy, psychiatric genetics |
| Wizard's Escape | Speed round, 1–2 players | Any categories you pick — it reuses the Jeopardy questions |

**Wizard's Escape** is a haunted-castle escape: each room's exit is blocked by
three identical pieces of furniture, each labelled with a candidate answer, and
the question is written across the top of the room. Pick the right one and the
wizard's spell shatters it and opens the door; a wrong pick fizzles, costs no
points, and you try again. Answer faster for a stronger spell and more points.
Escape the last room and you watch the wizard walk out of the castle into the
night. Two-player mode splits the screen — both wizards get the same question,
but only the first to answer correctly gets through that room, and the first one
out of the castle wins (the loser is left behind in a lit castle window). Keys
are `1 2 3` solo, `A S D` and `J K L` for two players.

A two-wizard race needs more questions than a solo run — only one wizard clears
a room per question — so with a small category selection the castle shrinks to a
size the question pool can actually finish.

**Scores are saved on the device that played them.** Enter your initials before
starting (they're remembered for next time and label the panes during a race)
and each finished run is kept in the browser's local storage with its score,
rooms cleared, and the categories that run covered — so you can see what you've
actually studied, not just what you scored. "Best escapes" on the setup screen
lists the top runs, and **Clear scores** wipes them. Nothing leaves the device:
scores are per-browser, so a different computer, browser, or a private window
starts empty, and clearing site data erases them.

It has no questions of its own: it draws them from the Jeopardy games above, so
adding a Jeopardy game puts its categories in the wizard's picker automatically.
Clues whose question is a picture (`image`) are shown on the board but kept out
of the wizard game for now. Two other optional fields control how a clue plays
there — `short`, a compact label for when the real answer is a paragraph, and
`decoys`, the two wrong options. Decoys otherwise default to other answers from the same category, which
only works where a category is a homogeneous list; where it mixes question types
(a duration, a symptom list, a drug name) the options must be written by hand or
the right answer is the only one that even fits the question.

## One file

The entire site — landing page, styling, game engine and every question — is
`index.html`. Nothing else is needed to run or publish it.

- **Hosted:** upload that one file to the repo; GitHub Pages serves it.
- **Locally:** download it and double-click. No build step, no dependencies, no
  internet connection.

Each game has its own shareable link via the URL hash, e.g.
`…/MPboardstudy/#antidepressant-jeopardy` opens straight to that board.

## Adding a game

Claude does this via the `add-game` skill — hand it a Jeopardy PowerPoint, an
HTML game, or a list of clues and it adds the game and validates the result.

By hand: open `index.html`, find the `GAMES` array (it sits between the
`GAME REGISTRY` comment markers near the bottom) and append an object:

```js
{
  id: "antipsychotic-jeopardy",
  title: "Antipsychotic Jeopardy!",
  kind: "Jeopardy",
  blurb: "One or two sentences, shown on the card.",
  tags: ["Psychopharm", "5 categories", "25 clues"],
  subtitle: "Shown under the title while playing",
  categories: [
    {
      name: "TYPICALS",
      clues: [
        { value: 100, clue: "Clue text.", answer: "What is ...?" }
      ]
    }
  ]
}
```

`id` must be unique and kebab-case — it's the URL hash. Keep strings
double-quoted, and let `value` ascend down each column. Categories may have
different numbers of clues; short columns show as blank tiles.

Games that aren't Jeopardy boards (like Wizard's Escape) go in the `EXTRAS`
array instead, and also need their own view markup and a branch in `route()`.

Everything below the arrays is the shared engine code, so a fix there applies to
every game at once. Don't split styling or a game out into a separate file — the site
is deliberately one file, and a sibling file would look editable while having no
effect on the page.

## Editing questions

Edit the text between the quotes in the relevant game's `categories`. Answers
are phrased as questions, Jeopardy-style. To rename a category, change its
`name`; to rename a game, change its `title`.

## Publishing with GitHub Pages

Already set up for this repo. To update it: **Add file → Upload files** in the
`MPboardstudy` repo, drop in `index.html`, commit. Live in 1–2 minutes — hard
refresh if the browser serves a cached copy.

To repeat this elsewhere:

1. Create a **Public** repository and upload `index.html` to its root.
2. Go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**, set the branch to `main`
   and the folder to `/ (root)`, and click **Save**.
4. Wait 1–2 minutes. The live URL is `https://<username>.github.io/<repo-name>/`.

Two things that commonly go wrong: the file must be named `index.html` and sit
at the repo root, and the URL path is the **repository** name — not the name of
the project inside it.

## Playing

Click a tile to show the clue, then **Reveal Answer** (or press Space). A tile is
only used up once its answer has been revealed, so opening one by mistake and
pressing Esc leaves it on the board. Each clue scores once; the pick highlights
and **Undo** reverses it. Team names are editable, and teams can be added or
removed mid-game. Stepping back to the hub and returning keeps a game in
progress — scores and used tiles survive until the page is reloaded.

## Notes

Educational use only. Content is intended for board review and teaching, not as
clinical guidance — verify dosing and safety information against current
prescribing references before applying it to patient care.
