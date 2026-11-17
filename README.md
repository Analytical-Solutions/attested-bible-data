# The Attested Bible: data

A verse-level evidence graph. Each historical claim in the text is linked to the archaeological finds, inscriptions, coins, manuscripts and ancient writings that bear on it. Each link carries a strength grade, a note saying exactly what the evidence shows, and a receipt: a short verbatim quote from a source that was fetched and re-checked.

The graph records evidence in tension with the text, and searches that found nothing, as plainly as confirmations.

**Version 0.1.1 (2026-11-16).** This release covers Matthew, Mark, Luke, John and Acts.

| | Count |
|---|---|
| Verses (passages) | 4,786 |
| Claims | 1,740 |
| Evidence items (artifacts, texts, sites, observations) | 840 |
| Persons and places | 382 |
| Sources, each with a verified excerpt | 1,498 |
| Graded links: A / B / C / D | 225 / 425 / 701 / 157 |
| Evidence in tension (`complicates`) | 77 |
| Manuscript links (`preserves`) | 13,748 |
| Parallel accounts (`parallels`) | 1,526 |
| Nodes / edges | 9,246 / 24,540 |

## Grades

Each `attests` edge carries a grade:

| Grade | Meaning | Example |
|---|---|---|
| A | **Direct.** The evidence names the same person, place, office or event. | An inscription naming Pontius Pilate as prefect of Judea |
| B | **Specific.** It confirms the specific setting at the right place and time. | A first-century synagogue excavated at Magdala |
| C | **Contextual.** It shows the custom, object or condition existed then and there. | Basalt millstones in first-century Galilee |
| D | **Contested.** Its identification, date or authenticity is disputed; the note says by whom. | An ossuary inscription whose authenticity is debated |

**Further rules:**
- A grade covers the whole claim.
- Evidence in tension is recorded as a `complicates` edge.
- A manuscript of the text only `preserves` its passages and never attests their claims.

The binding rules, with the decisions taken while applying them, are in [`docs/calibration.md`](docs/calibration.md).

## What is here

| Path | Contents |
|---|---|
| `graph.json` | The whole graph merged into one file: `nodes` (each with its `origin` chapter) and `edges` |
| `data/<book>/<NN>/nodes.jsonl`, `edges.jsonl` | The same graph, one chapter per directory, one JSON object per line |
| `data/<book>/<NN>/matrix.csv` | The chapter's search matrix. Every person, place and claim is crossed with every evidence category and marked `found`, `none-found` (with what was searched) or `n/a` |
| `data/<book>/<NN>/source-check.json` | The result of re-fetching every source in the chapter and confirming its excerpt is on the page |
| `data/scenes/<book>/<NN>.json` | Where each scene takes place: verse ranges with a setting, the words that place it, and whether it is stated or inferred |
| `geo/coordinates.csv` | Coordinates for places and sites, each with its source (Wikidata or Pleiades) and precision |
| `docs/model.md` | Node and edge types, required fields and id conventions |
| `docs/calibration.md` | The grading rules |
| `SUMMARY.md` | The strongest evidence, coverage by chapter, and the claims with no evidence yet |
| `METHODS.md` | How the data was made, and its limitations |

**Node types:**
- passage
- claim
- person, place
- site, artifact, text, observation
- source

**Edge types:**
- `asserts`: a passage makes a claim
- `mentions`
- `attests`: graded A–D
- `complicates`
- `found_at`, `identified_as`
- `preserves`: a manuscript carries a passage
- `documented_by`: evidence to its sources
- `related_to`
- `parallels`: the same event told in another book

Ids look like `claim:ac-18-12-gallio-proconsul` and `passage:mt-27-02`.

## Licence

The data is licensed under [CC BY 4.0](LICENSE). You may share and adapt it for any purpose, including commercially, as long as you give credit.

Each source node quotes a short excerpt, at most 300 characters, from a third-party page as a citation. Those excerpts keep their original licences; see [`NOTICE.md`](NOTICE.md).

## How to cite

Use the metadata in [`CITATION.cff`](CITATION.cff); GitHub's "Cite this repository" button reads it. For example:

> Analytical Solutions. *The Attested Bible: a verse-level evidence graph* (data), version 0.1.1, 2026-11-16. https://github.com/Analytical-Solutions/attested-bible-data

To cite a single claim or piece of evidence, give its id and the version.

## Corrections

The grades are judgements made under written rules, and they can be wrong. To challenge a grade or propose evidence, open an issue. Name the claim or node id and link a source that states the fact. Evidence against a claim is as welcome as evidence for it.
