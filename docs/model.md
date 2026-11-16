# Data model

Each chapter directory (`data/<book>/<NN>/`, with book matthew, mark, luke, john or acts) holds two files with one JSON object per line: `nodes.jsonl` and `edges.jsonl`. `tools/build.py` enforces everything below.

## Node types

Every node has `id`, `type` and `label`. An id is `<type>:<lowercase-slug>`, made of the characters a–z, 0–9 and `-`.

| Type | Extra required fields | Optional fields | Id examples |
|---|---|---|---|
| passage | `ref` ("Matt 2:1", "Mark 15:1", "Luke 2:1", "John 19:13", "Acts 18:12") | `text` (WEB, at most one verse); `variants`: a list of `{reading, attested_by: [manuscript ids], note}` | `passage:mt-02-01`, `passage:mk-15-01`, `passage:lk-02-01`, `passage:jn-19-13`, `passage:ac-18-12` |
| claim | `ref`, `statement`, `kind` (person, place, office, event, object, custom or time) | | `claim:mt-02-01-herod-king-of-judea` |
| person | | `aka`, `dates`, `wikidata` | `person:herod-the-great` |
| place | | `lat`, `lon`, `pleiades`, `wikidata`, `modern_name` | `place:bethlehem` |
| site | | `lat`, `lon`, `excavators`, `periods`, `wikidata` | `site:herodium` |
| artifact | `kind` (inscription, coin, structure, burial, manuscript, papyrus, tool, vessel, artwork or other), `date` | `found` (year, by whom), `held_at`, `catalogue`, `wikidata` | `artifact:pilate-stone` |
| text | `author`, `work`, `locator` | `date`, `language`, `biblical` (true for any book of the Bible) | `text:josephus-antiquities-18-116-119` |
| observation | `kind` (astronomical, geological, biological, chemical or other), `date` | `method` | `observation:lunar-eclipse-4-bce-03-13` |
| source | `url`, `title`, `accessed` (YYYY-MM-DD, read from the clock with `date +%F` on the day of the fetch; never estimated, never later than today), `excerpt` (verbatim, at most 300 characters) | `publisher`, `authors`, `year` | `source:wikipedia-herodium` |

Write claims small: one checkable fact each. For example, Matt 2:1 yields "Jesus was born in Bethlehem of Judea" (event), "Herod was king when Jesus was born" (office) and "Magi came from the east to Jerusalem" (event).

## Edge types

An edge has the form `{"from": id, "type": t, "to": id, ...}`.

| Type | From → to | Extra fields |
|---|---|---|
| asserts | passage → claim | |
| mentions | claim → person or place | |
| attests | artifact, text, site or observation → claim, person or place | `grade` (A, B, C or D) and `note` (exactly what the evidence shows) |
| complicates | artifact, text, site or observation → claim, person or place | `note` (exactly what is in tension) |
| found_at | artifact → site | |
| identified_as | site → place | `note` if the identification is debated |
| preserves | artifact (a manuscript) → passage | |
| documented_by | any evidence or anchor → source | |
| related_to | any → any | `note` |
| parallels | passage → passage | optional `note`. The same event told in another Gospel; see `docs/parallels.md` |

Use an `observation` for scientific data such as a computed eclipse, a sediment-core earthquake date or a DNA result. Every artifact, text, site and observation needs at least one `documented_by` source.

Another book of the Bible is a cross-reference, not independent evidence. Mark its text node `"biblical": true` and link it with `related_to`; the build rejects `attests` or `complicates` from it.

## Reusing nodes across chapters

Herod, Jerusalem, Galilee and the Temple appear in many chapters. Before you create a person, place, site, artifact or text, search the existing ids, for example `grep -h '"id"' data/*/*/nodes.jsonl`, or `build/graph.json` after a build. Reuse an id when it exists. You may repeat the node line in your chapter so your chapter is self-contained, but the label and fields must match exactly; the build reports any difference as a merge conflict.

## Sources

Prefer sources that are stable and fetchable:
- Wikipedia, plus its REST summary at `https://en.wikipedia.org/api/rest_v1/page/summary/<Title>`
- museum collection pages: the Israel Museum, the British Museum, the Louvre
- Wikisource for Josephus (Whiston translation) and other public-domain texts
- Pleiades for places
- Wikidata
- publisher abstract pages for peer-reviewed papers

Copy the excerpt verbatim from the fetched page. It must state the fact the edge relies on.
