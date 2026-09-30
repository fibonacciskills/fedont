# The Federation Loom

An interactive, scored game that teaches federated ontologies: multiple ontologies will
always exist — and that's healthy — but RDF links (SKOS/OWL) let them behave like one
living, richer graph.

Play in two acts across five real US-focused vocabularies — CEDS and CTDL (the focus
standards, underlined in gold on the graph) plus O*NET, schema.org, and EduCOR:

- **Prologue.** A brief read on why multiple ontologies exist (and always will), and how to play.
- **Act I — The Weave.** Judge which concept in another vocabulary each concept joins to;
  the loom weaves each connection as a visible RDF link (`skos:exactMatch` / `closeMatch` /
  `broadMatch`) on the graph.
- **Act II — The Harvest.** Run federated queries that only work across the links you wove.

The first play is a quick game (3 joins, 2 queries); the expanded loom (6 joins, 3 queries)
unlocks from the score screen. No login, no persistence — score lives only in the tab.

## Run it

The whole site is one self-contained file. Either open `index.html` directly in a
browser, or serve the folder:

```sh
python3 -m http.server 8080
# → http://localhost:8080
```

The only external dependency is Google Fonts; the game degrades gracefully to system
fonts offline.

## Deploy

Any static host works (GitHub Pages, Netlify, etc.). For GitHub Pages: push to GitHub,
then Settings → Pages → deploy from the `main` branch root.

## Grounded in

[CEDS](https://ceds.ed.gov/) · [CTDL](https://credreg.net/) ·
[O*NET](https://www.onetonline.org/) · [schema.org](https://schema.org/) ·
[EduCOR](https://arxiv.org/abs/2107.05522) · [SKOS](https://www.w3.org/TR/skos-reference/).
The CIP→SOC program-to-occupation crosswalk in the game is real, published by NCES.
