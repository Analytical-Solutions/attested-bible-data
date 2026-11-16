# How this data was made

## The text and its claims

The base text is the World English Bible, which is in the public domain, fetched from bible-api.com. Each chapter is split into small claims that can be checked one at a time. A claim is about a person, place, office, event, object, custom or time, and it is tied to its verse by an `asserts` edge.

When another book tells the same event, its passage asserts the existing claim instead of a new one, and the two passages are joined by a `parallels` edge. When the accounts differ, the difference is recorded as `related_to`, with a note saying what differs.

## The search

Every anchor in a chapter (its persons, places and claims) is crossed with every evidence category. There are eleven categories:
- inscription
- coin
- structure or site
- burial or ossuary
- manuscript
- documentary papyrus
- Jewish literature (Josephus, Philo, the Dead Sea Scrolls, rabbinic texts)
- Greco-Roman literature
- material culture
- geography or nature
- astronomy or calendar

Early Christian writings that know the Gospels are treated as reception, and graded D at most.

Each cell of this search matrix ends as one of:
- `found`, with the evidence ids
- `none-found`, with a note saying what was searched
- `n/a`

A gap in the evidence is therefore a recorded result, not a silence.

## Evidence and receipts

Every piece of evidence cites at least one source page that was actually fetched. Each source records its address, the date it was read, and a verbatim excerpt of at most 300 characters stating the fact. An automated check re-fetches every page and confirms the excerpt is on it; its results are in each chapter's `source-check.json`.

Sources are mostly open online editions and reference pages:
- Josephus in Whiston's translation
- Perseus and Wikisource editions of Greek and Latin authors
- Sefaria for the Mishnah and Talmud
- museum and excavation pages
- Wikipedia, for modern summaries of finds

Modern scholarship is cited as a source, never treated as ancient evidence.

## Grading

Grades follow the written rules in [`docs/calibration.md`](docs/calibration.md). In short:
- A grade must cover the whole claim. When evidence names an office or a building, the office claim may be A, and an event set there is at most B.
- A source that confirms a claim but contradicts part of it is B, with a `complicates` edge.
- Rabbinic texts carry the caveat that they were redacted around 200 CE and later.
- Miracles and appearances are written as claims, searched honestly, and recorded as none-found.
- A copy of the text (a manuscript) only `preserves` its passages.

When a grade was changed in review, the reason is appended to the edge's note.

## Who did the research

This is **AI-assisted research**, and you should weigh it that way.
- **Research.** The chapters were researched by AI research agents (open-weight GLM-5.3 models, run locally) working under written briefs and the grading rules.
- **Lead review.** Every returned chapter was reviewed by a lead AI reviewer (Anthropic's Claude). It checked the strong grades, regraded by the written rules, recorded its reasons, and accepted the chapter.
- **Range audits.** Separate AI reviewers then audited each range of chapters. They re-verified sources, checked every A and B grade against its excerpt, merged duplicates and checked parallels.
- **Consolidation.** Two consolidation passes applied the rules consistently across all five books.
- **Human oversight.** The project owner directed the work. The grades have **not yet been reviewed by a subject-matter expert**. Corrections are welcome.

## Limitations

- **"None-found"** means nothing was found in the sources searched. It does not mean nothing exists.
- **Online editions.** Many sources are online editions and reference pages rather than primary publications. The excerpt shows exactly what each page says.
- **Grades are judgements.** Two careful readers could grade some links differently; the rules and notes make each judgement inspectable.
- **Dates.** Evidence dates are written as the sources give them, sometimes as periods or ranges.
- **Coordinates.** Some coordinates are candidates or regions; each row states its precision.
- **Scenes.** Scene settings marked `inferred` follow from an earlier scene, not from words in the verse.
- **Manuscripts.** The manuscript links cover chosen witnesses (the major codices and early papyri where a source lists their contents). They are not a full critical apparatus.
