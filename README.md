# The Federation Loom

An interactive, scored game that teaches federated ontologies: multiple ontologies will
always exist — and that's healthy — but RDF links (SKOS/OWL) let them behave like one
living, richer graph.

Play in two acts across five real US-focused vocabularies — CEDS and CTDL (the focus
standards, underlined in gold on the graph) plus O*NET, schema.org, and EduCOR:

- **Prologue.** A brief read on why multiple ontologies exist (and always will), and how to play.
- **Act I — The Weave.** Judge which term in another vocabulary each term joins to;
  the loom weaves each connection as a visible RDF link on the graph.
- **Act II — The Harvest.** Run federated queries that only work across the links you wove.

### Which link for which thing

The game is deliberate about this, because published crosswalks often aren't. SKOS
mapping properties (`skos:exactMatch`, `broadMatch`, `relatedMatch`) are defined to hold
between instances of `skos:Concept` — code-list and taxonomy entries such as a CIP
program code or an O*NET skill. Ontology **classes and properties** take OWL/RDFS
instead (`owl:equivalentClass`, `rdfs:subClassOf`, `owl:equivalentProperty`). So
`ceds:Credential → ceterms:Credential` is an `rdfs:subClassOf` axiom, not a
`skos:closeMatch`.

The game is also explicit that **alignment is not verification**. A schema link makes a
question askable across two systems; it says nothing about whether a particular learner's
diploma is genuine. That takes an issuer-signed credential or an instance published in
the registry by the issuer.

### Relationship to EDUcore

EDUcore runs the same federation on a Neo4j property graph rather than an RDF
triplestore — its `MAPS_TO` and `STRUCTURALLY_MAPS_TO` relationships carry what the SKOS
matches and the OWL/RDFS axioms carry here. Different storage, same principle: concepts
align to concepts, structure aligns to structure. The game says this on the score screen.

The first play is a quick game (3 joins, 2 queries); the expanded loom (6 joins, 3 queries)
unlocks from the score screen. Every visit and every replay deals a fresh random hand — which
joins and queries appear, their order, and the order of the answer buttons — so a room full of
players won't all see the same quiz. No login, no persistence — score lives only in the tab.

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

Any static host works — there is no build toolchain, just the one HTML file.

**Render.** `render.yaml` in the repo root is a ready-to-use blueprint. In Render:
New → Blueprint → pick this repo → Apply. It creates a static site that copies
`index.html` into `dist/` and publishes that, with PR previews on. To set it up by hand
instead: New → Static Site, build command `mkdir -p dist && cp index.html dist/`,
publish directory `dist`.

**GitHub Pages.** Push to GitHub, then Settings → Pages → deploy from the `main`
branch root.

## Grounded in

[CEDS](https://ceds.ed.gov/) · [CTDL](https://credreg.net/) ·
[O*NET](https://www.onetonline.org/) · [schema.org](https://schema.org/) ·
[EduCOR](https://arxiv.org/abs/2107.05522) · [SKOS](https://www.w3.org/TR/skos-reference/) ·
[OWL](https://www.w3.org/TR/owl2-overview/).
The CIP→SOC program-to-occupation crosswalk in the game is real, published by NCES.
