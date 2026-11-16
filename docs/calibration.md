# Grading calibration (binding)

These are the architect's decisions from Matthew 1–28 and reviewers 1–4. Every runner and reviewer applies them. When a rule and a brief disagree, the rule wins; record the conflict in `notes.md`.

## Grades

- **A:** the evidence names the same person, office, place or event. A person is A when an independent source names them (Tacitus on Christus; the Caiaphas ossuary). A place is A when a source names it.
- **B:** the evidence confirms the specific setting: the same institution or practice, in the same place and period. A pre-Christian manuscript carrying the exact passage a Gospel quotes is also B, as the Great Isaiah Scroll is for Isaiah quotations.
- **C:** context. It shows a custom or condition in the period and region. Crowd sizes, general institutions, finds from a later period and parallels from elsewhere in the empire are C, not B.
- **D:**
  - the identification, date or authenticity is disputed
  - an unprovenanced (antiquities-market or looted) find, unless a cited source reports scientific authentication
  - a reception text reporting a tradition

  Name the dispute in the note.

## Scope rules

- **A grade covers the whole claim.** If the evidence supports only part, split the claim or grade the weaker part. A source that confirms the governor does not attest that someone was handed over to him: the Pilate stone is A for Pilate's office and B for "they delivered him to Pilate".
- **A site or a custom never attests a person**, unless the site is that person's own documented building. Link a person's hometown to the person with `related_to`.
- **Predictions and parables:** evidence attests that the event happened, or that the custom existed. It never attests that something was predicted or that a parable was told; say so in the note. Word claims neutrally: never "fulfilled".
- **Miracles and appearances:** write them as claims and search honestly. Record none-found. Never grade setting evidence as if it attested the miracle.
- **Copies of the text:** a manuscript of the book only `preserves` the passages it carries. It never attests a claim, and the build rejects that.
- **Other books of the Bible** (including the deuterocanon, and other Gospels when they are cross-referenced as texts) are `"biblical": true` and `related_to` only. Differences between Gospels are recorded with `related_to`, never `complicates`; see `docs/parallels.md`.
- **Early Christian writings that know the Gospels** are reception. This covers the Didache, Ignatius, Papias, Justin, Irenaeus, Origen and Eusebius on Gospel events, and pilgrim traditions about sites. Link them with `related_to`, or grade D at most. A reception text may be C only when it reports something independent of the Gospel text in its own day, such as a counter-story circulating; name the dependence in the note.
- **Mishnah and Talmud** were redacted around 200 CE and later. Every edge from them says that they may not describe the practice of the 30s CE exactly.
- **Modern scholarship** is a `source`, never a `text`. Scientific data (an eclipse computation, a sediment core, DNA, a plant's range, an isotope study) is an `observation`.
- **Record tension with `complicates`.** Never raise a grade to make a claim look stronger. A reviewer may change a grade in either direction only when a rule above requires it, and must append the reason to the note.
- **A fetched page beats memory and the brief.** If a page does not state what a lead says, do not enter the lead, and record the discrepancy in `notes.md`.

## Architect rulings (2026-11-15, applied by the consolidation pass)

- **Titles and offices.**
  - When evidence names an office, title, building or person, and the claim adds an event, split the claim.
  - The office claim gets the A, and the event claim gets B (confirms the setting). The model is claim:ac-04-01-captain-of-the-temple.
- **Partial contradiction.**
  - A source that confirms a claim but contradicts part of it (a number, a place) is B plus `complicates`, never A. An example is Josephus's Egyptian against Acts 21:38.
  - A different source in tension does not lower an A that fully covers the claim. Examples are Suetonius against Dio on Claudius's expulsion, and Josephus against Tacitus on Drusilla.
- **Mishnah laws on the same practice.**
  - A Mishnah law naming the same act or custom is B for the custom claim, and C for an event claim set in it. It always carries the c. 200 CE caveat.
  - Examples are carrying a mat or kneading on the Sabbath, the Nazirite haircut and the Passover lamb.
- **Coins.**
  - When the coin is the claim (the widow's two lepta, the temple-tax shekel), it is B.
  - When a coin is named inside a saying or parable (the lost drachma, the sparrows' assarion), it is C. The same saying in two Gospels gets the same edge.
- **`parallels`** means the same event told in another book. Two passages in one book are `related_to`, with a note.
- **Values a fetch can supply** (a Wikidata id, an access date) are never written from memory.
