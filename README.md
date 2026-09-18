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
| Depression Pharmacology Jeopardy | Jeopardy, 6 × 5 | Receptors, CYP interactions, TCAs, sexual side effects, cautions, alternative agents |
| Depression Treatment Jeopardy | Jeopardy, 5 × 5 | ECT/TMS/esketamine, treatment resistance, maintenance, DOD/VA guidelines, psychotherapies |
| NCD Jeopardy: Diagnosis & Management | Jeopardy, 5 × 5 · *coming soon* | Diagnostic criteria and domains, cognitive assessment tools, the dementia work-up, safety and driving, agitation and psychosis |
| NCD Jeopardy: Etiologies | Jeopardy, 6 × 5 · *coming soon* | Alzheimer's, Lewy body and Parkinson's, vascular, frontotemporal, infectious and prion, Huntington's/NPH/TBI |
| Development Through the Life Cycle | Jeopardy, 6 × 5 · *coming soon* | Infant milestones, toddler to preschool, Piaget/Freud/Erikson, attachment and play, puberty, aging and menopause |
| Sexuality, Gender & Dissociation | Jeopardy, 6 × 5 · *coming soon* | Sexual dysfunctions and their treatment, paraphilic and pedophilic disorders, gender dysphoria, dissociative disorders |
| Antipsychotic Jeopardy | Jeopardy, 7 × 5 | FGAs, SGAs and newer agents, clozapine, long-acting injectables, movement side effects, phases of care, name-the-drug receptor binding profiles (picture clues) |
| Antipsychotic Pharmacology | Connect Four, 5 × 5 or 7 × 6 | Receptor mechanisms, FGA potency, LAIs, CYP interactions, EPS management, clozapine monitoring (15 of the 25 questions also appear in Wizard's Escape) |
| Wizard's Escape | Speed round, 1–4 players | Any categories you pick — it reuses the Jeopardy questions |
| Receptor Lab: Antipsychotics | Click & drop, solo | 19 antipsychotics — which receptors each one binds, whether it antagonises / partially activates / activates / inverts them, and how tightly |

The four *coming soon* boards are finished and wizard-ready — every clue carries
its `short` label and two hand-written `decoys` — but each is parked with
`comingSoon: true`, so no card is clickable and none of their categories reach
Wizard's Escape yet. Deleting that one line on a game switches it fully on.

**Receptor Lab** is the odd one out — no clues, no teams, no buzzer, and its own
cauldron-lit palette instead of the navy and gold. You get an empty cell and a
drug name, and you click receptors out of the tray into the membrane: which ones
this drug actually binds, what it does at each (antagonist in red, partial
agonist in blue, agonist in green, inverse agonist in purple, or a reuptake block
for SERT/NET), and how tightly, sized in four bands. One click drops a receptor
in; dragging works too. Lock in and your cauldron is set beside the real one —
the true profile carries each receptor's Ki right under its label — with a
receptor-by-receptor table below.

A perfect round is 1000 points, split across the drug's *core* receptors: half
for knowing it binds at all, a quarter for the action, a quarter for the strength
band (half credit one band out). *Bonus* receptors are real but lower-yield —
they pay 40% of a core one and cost nothing if missed. Receptors the drug
genuinely does not touch cost you 40% of a core receptor if you place one, which
is the point: knowing risperidone has no muscarinic affinity, or that
pimavanserin has no dopamine affinity at all, is half the exercise. Anything
genuinely arguable is left unscored either way.

The four strength bands are the log-decade scheme from Siafis et al,
*Curr Neuropharmacol* 2018;16(8):1210-23 — very high (Ki < 1 nM), high (1–10),
moderate (10–100), low (100–1000), with Ki ≥ 1000 nM counted as no meaningful
binding. Every drug carries its own Ki citation on the answer screen, because
binding constants move with tissue, species and radioligand; the band is the
teaching point, not the decimal. Where the literature legitimately splits —
"5-HT2A antagonist" versus "inverse agonist" on a constitutively active receptor
— both answers score full marks.

Three modes. **Gauntlet** is the default: five random drugs back to back against
the clock, with five jars on the shelf that fill in as you go. **Survival** deals
drugs with no end — score above 800 and you brew on, hit 800 or less and the run
is over. **Free play** picks any single drug at your own pace, keeping a best
score per drug in `localStorage`. The second-messenger / G-protein layer is
deliberately not built yet, but every receptor already carries its transduction
pathway in `RL_TRANSDUCTION`, so that round can be added without re-deriving
anything.

Survival has a **shared board**, listed on the mode's menu and again under the
run summary: the ten longest runs anyone chose to post, from every device.
Posting is opt-in and happens only at the end of a run — you type the name you
want to appear under, and nothing leaves the browser until you press the button.
Runs are ranked by rounds survived first, since that is what the mode asks of
you; points banked (the surviving rounds only, not the one that ended it) break
ties between runs of the same length. It is a sibling of Wizard's Escape's board
but its own database node, `leaderboard/receptor`, because a run here is counted
in rounds rather than rooms and categories.

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

**Survival** is the third mode, and it changes the rules: three lives, and no
exit. There is no fixed castle — rooms keep coming, and the deck loops once you
have seen everything you selected. A wrong answer costs a life instead of costing
nothing, and so does letting the clock run out; the clock itself starts at 14
seconds and tightens by 0.4 seconds a room down to a floor of 6. The score is
filed under how many rooms you cleared.

Survival takes **up to four wizards at once**, and they all share one room. Open a
phone room before starting and everyone seated joins the same run: one question
across the top, one set of three pieces at full size, and a line of wizards along
the floor beneath them with their own lives and score. A wrong pick costs that
wizard a life and nobody else, and they can go again — the clock is the real
limit. The room ends once every wizard still standing has cleared it, or the clock
runs out and the stragglers pay for it. Lose your third life and your wizard
slumps and fades out of the line while the rest carry on. When the last one falls
the run ends on a standings table: deepest wins, and score settles a tie.

The alternative — four separate rooms side by side — would have shrunk the
question and twelve furniture labels into unreadability on any screen small
enough to sit round. One shared room keeps everything full size no matter how
many are playing.

Sharing a room does mean nothing on screen may point at the piece somebody
picked. A bolt flying to the right bookcase, or splinters bursting off it, would
hand the answer to everyone still reading — and a miss gives as much away, since
it rules a piece out. So in a coven the spell is a soft wash of colour over the
room, green or red, plus the caster's own staff swinging on their card. It is
deliberately dim: it fires while the others are still reading. Playing survival
alone, there is nobody to give anything away to, so the full bolt-and-splinters
spell lands as it always did.

Each wizard is drawn from a rotation of six looks — robe, hat shape, beard and
staff all change together — so four of them in one room are tellable apart at a
glance. Seat 1 is always the violet wizard, seat 2 the crimson one, and so on,
which means players keep the same wizard from run to run. A two-wizard race gets
two different ones, and the Jeopardy celebration's dancers are five different
wizards rather than one copied five times.

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

**Connect Four** is for two teams, red and yellow. On your turn pick a column; the
disc would land in the lowest open spot, and you have to answer a question to
keep it there. The other team gets to say a steal answer before the reveal, so
one reveal settles who (if anyone) takes the spot, and then play passes on. Four
in a row in any direction wins. The board is 5 × 5 by default, one spot per
question, with a 7 × 6 classic option; missed questions return under the pile,
so neither size ever runs out. The host can take back a wrong column before
revealing and undo any move, and team names and the win tally carry over from
game to game. Its questions sit in `GAMES` with `format: "connect-four"`, so the
Anki export works as it does for the boards. Questions too long to read in a
speed-round room (`wiz: false`, like full receptor mechanisms) stay out of
Wizard's Escape.

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

Write every new clue to three rules (they're spelled out in full in the
`GAME REGISTRY` comment above the array):

1. **Single ask.** One clue, one fact. A clue wanting two or three things at
   once can't become one multiple-choice option — trim it to the fact that
   matters and put the extra teaching detail in `answer`, which only the board
   shows.
2. **Three options, always.** Give every clue a `short` plus exactly two
   `decoys`, of the same *kind* as the answer. The sibling-answer fallback
   described above exists for older clues, not as the plan for new ones.
3. **Quick to read, not trivial.** `clue` is what a player reads mid-race in
   Wizard's Escape, so keep it to about one sentence, well under 30 words.

Strings go in as plain text, not HTML — the page renders them with
`textContent`, so an `&amp;` shows up on the board literally.

Games that aren't Jeopardy boards (like Wizard's Escape) go in the `EXTRAS`
array instead, and also need their own view markup and a branch in `route()`.

To park a game without losing it, add `comingSoon: true` to its entry. Its card
greys out and stops being a link, a direct `#hash` to it lands on the hub
instead, and its categories drop out of Wizard's Escape — while all of its clues
stay in the file. Deleting that one line brings it straight back.

Everything below the arrays is the shared engine code, so a fix there applies to
every game at once. Don't split styling or a game out into a separate file — the site
is deliberately one file, and a sibling file would look editable while having no
effect on the page.

## Phone buzzers

Under every board there's **Open buzzer room**. It shows a 4-letter code and a
join link; players open the site on their phones, enter the code and a name, and
get one big buzzer. Opening a clue arms every phone, the first press wins, and
the clue card lists who buzzed in order with the gap behind the leader. Revealing
the answer or closing the clue locks them again.

A **host console** runs alongside it: the room panel shows a second link
(`#host-<code>`) that opens a phone-sized view of whichever clue is live —
with the answer — while the room still sees only the question. The answer never
travels over the network: the room stores just the clue's coordinates, and the
console looks the text up in its own copy of the page.

**Wizard's Escape uses the same rooms.** "Play from phones" on its setup screen
opens one; players join at the same kind of link and get three big numbered
buttons. The answers stay on the big screen and never travel over the network —
a phone only ever says "seat 2 chose the third one" — which keeps everyone
looking up at the shared game. It works for all three modes: a solo run, a
two-wizard race with both rooms on the screen, and survival for up to four.
Whoever is not on a phone keeps the keyboard; with every seat taken the screen
stops accepting answers of its own.

### Getting people into a room

Every room panel shows a **QR code** beside the code, and the join link is set
large enough to read across a desk. **Show join screen** fills the whole screen
with a big QR, the code at projector size and the link underneath — click
anywhere or press Escape to dismiss it. It updates live, so the host can leave
it up and watch names appear as people join.

The QR is generated in the page itself (byte mode, error correction level M),
because a QR library would mean loading something from a CDN and the site has to
stay one file.

One nicety: opening `index.html` straight off the disk, or serving it on
localhost, produces an address no phone can reach — so in that case the QR and
the join link point at the published site instead. The room lives in the shared
database, so a phone joining through the published copy lands in the same room.

**Buzzers on / off** switches the whole thing off mid-game — the board then plays
exactly as it did before, scoring by team buttons as usual. With no room open,
nothing about the game changes at all.

Rooms are held in a Firebase Realtime Database (project `mp-board-study`), talked
to over its REST API and server-sent events so the page needs no library and
stays one file. A room holds only names, timestamps and which clue is live, and
**Close room** deletes it. The database URL is the `DB` constant in the buzzer
section of `index.html`.

### The database rules have to be published

None of this works until the Realtime Database's rules allow it, and a database
with unpublished rules refuses every write. `firebase-rules.json` in this folder
is what to paste — **Realtime Database → Rules** in the Firebase console, then
**Publish**. It is for the console only; it is not part of the site and does not
belong in the repo. The same applies after the file changes: the Receptor Lab's
`leaderboard/receptor` node was added to it later than the rest, so a database
still running the older rules refuses to show or accept those runs, and the
board says it is not published yet.

If they are missing you now find out immediately: opening a room says the
database refused the write instead of showing a code for a room that was never
created, and phones say the rules still need publishing instead of "no room".

## Anki export

Every board has a **Download Anki deck (.apkg)** button under it. The file is a
real Anki package — a zip around a SQLite collection — built in the browser
with no library, so the page stays one self-contained file. Open it and Anki
imports the deck directly; no import dialog, no field mapping.

Each clue becomes one Basic note (clue on the front, the full answer on the
back), filed in a deck named `Board Study Games::<game>` and tagged
`board-study-games` plus `bsg::<game>::<category>`, so you can study one
category on its own. Picture clues carry their image in as a real media file.

Note ids, deck ids and note guids are derived from the content rather than the
clock, so re-exporting after editing a clue and importing again **updates** the
existing notes instead of creating a second copy.

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

Click a tile to show the clue, then **Reveal Answer** (or press Space). A clock
starts the moment a tile is opened but stays hidden for the first 30 seconds, so
a team gets half a minute to think before it appears in the corner and counts up.
It freezes when the answer is revealed, leaving the elapsed time on screen while
you award points, and resets for the next clue.

When the last tile on a board is used up, the winning team is announced over
falling streamers with a line of dancing wizards along the bottom, for about
eight seconds — click anywhere or press Esc to dismiss it early. Ties and draws
are named properly, and resetting the board arms it again. A tile is
only used up once its answer has been revealed, so opening one by mistake and
pressing Esc leaves it on the board. Each clue scores once; the pick highlights
and **Undo** steps back through them. Several teams can be scored on one clue —
each can go down once, one after another, the way it happens when two teams buzz
and miss — but a correct answer closes the clue. Team names are editable, and teams can be added or
removed mid-game. Stepping back to the hub and returning keeps a game in
progress — scores and used tiles survive until the page is reloaded.

## Notes

Educational use only. Content is intended for board review and teaching, not as
clinical guidance — verify dosing and safety information against current
prescribing references before applying it to patient care.
