# Antidepressant Jeopardy!

A browser-based Jeopardy game for teaching antidepressant pharmacology — receptor profiles, mechanisms, side effects, and special considerations. Built for psychiatry / internal medicine residents and med students.

**▶️ Play: https://USERNAME.github.io/antidepressant-jeopardy/**

(Replace `USERNAME` with your GitHub username after you enable Pages — see below.)

## Contents

Six categories × five clues = 30 questions, with two-team scoring built in.

| Category | Focus |
|---|---|
| SSRIs | Indications, dosing caps, pregnancy considerations |
| SNRIs | Metabolites, off-label and non-MDD indications |
| Atypical & Novel | Newer and mechanistically distinct agents |
| TCAs & MAOIs | Classic agents, dietary and interaction pitfalls |
| Receptor Profiles | Binding targets and what they predict |
| Side Effects & Safety | Adverse effects, monitoring, contraindications |

## How to run it

**No setup required.** Everything is in a single `index.html` — no build step, no dependencies, no internet connection needed once downloaded.

- **Locally:** download `index.html` and double-click it. It opens in any browser.
- **Hosted:** enable GitHub Pages (below) and share the link.

## Publishing with GitHub Pages

1. Create a new repository on GitHub named `antidepressant-jeopardy` and make it **Public**.
2. Upload `index.html` and `README.md` to the repo (drag and drop works — use **Add file → Upload files**).
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**. Set the branch to `main` and the folder to `/ (root)`. Click **Save**.
5. Wait 1–2 minutes, then reload the Pages settings screen. Your live URL will appear at the top.

The file must be named `index.html` for Pages to serve it at the root URL — it already is.

## Editing the questions

Open `index.html` in any text editor and find the `CATEGORIES` array near the bottom of the file. Each clue looks like this:

```js
{ value: 100, clue: "This SSRI is preferred in pregnancy...", answer: "What is sertraline?" }
```

Edit the text between the quotes. Keep the `value` numbers as they are so the board stays aligned, and remember answers are phrased as questions, Jeopardy-style.

To rename a category, change its `name` field.

## Notes

Educational use only. Content is intended for board review and teaching, not as clinical guidance — verify dosing and safety information against current prescribing references before applying it to patient care.
