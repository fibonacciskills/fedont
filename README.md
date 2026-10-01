# The Federation Loom

An interactive, scored game that teaches federated ontologies: multiple ontologies will
always exist — and that's healthy — but RDF links (SKOS/OWL) let them behave like one
living, richer graph.

<<<<<<< Updated upstream
Play in two acts across five real US-focused vocabularies — CEDS and CTDL (the focus
standards, underlined in gold on the graph) plus O*NET, schema.org, and EDUcore:
=======
Play in two acts across four real US-focused vocabularies — CEDS and CTDL (the focus
standards, underlined in gold on the graph) plus schema.org and EduCOR:
>>>>>>> Stashed changes

- **Prologue.** A brief read on why multiple ontologies exist (and always will), and how to play.
- **Act I — The Weave.** Judge which term in another vocabulary each term joins to;
  the loom weaves each connection as a visible RDF link on the graph.
- **Act II — The Harvest.** Run federated queries that only work across the links you wove.

### Which link for which thing

The game is deliberate about this, because published crosswalks often aren't. SKOS
mapping properties (`skos:exactMatch`, `broadMatch`, `relatedMatch`) are defined to hold
between instances of `skos:Concept` — code-list and taxonomy entries such as a CIP
program code or a published competency. Ontology **classes and properties** take OWL/RDFS
instead (`owl:equivalentClass`, `rdfs:subClassOf`, `owl:equivalentProperty`). So
`ceds:CredentialDefinition → ceterms:Credential` is an `owl:equivalentClass` axiom, not a
`skos:exactMatch`. (CEDS v14 has no class named Credential; Credential Definition is its
counterpart, defined in CTDL's own words.)

The game is also explicit that **alignment is not verification**. A schema link makes a
question askable across two systems; it says nothing about whether a particular learner's
diploma is genuine. That takes an issuer-signed credential or an instance published in
the registry by the issuer.

### EDUcore on the graph

EDUcore, the education standards knowledge graph, is the fifth vocabulary. Its nodes in
the game are real forged nodes from that graph: the O*NET-SOC occupation 15-1252, the
CIP program 11.0701 (one `CLASSIFICATION_CROSSWALK` edge apart, per the NCES crosswalk),
CTDL-ASN's `ceasn:Competency`, and CEDS's Learning Resource class (C200228). EDUcore runs
the same federation on a Neo4j property graph rather than an RDF triplestore: each
standard's elements resolve to CEDS hub tuples by authored `EXACT_MATCH` or inferred
`CLOSE_MATCH` edges, `SUBCLASS_OF` carries structure, and `CLASSIFICATION_CROSSWALK`
carries CIP→SOC. Different storage, same principle: concepts align to concepts, structure
aligns to structure. The game says this on the score screen.

The facts behind every join and query were checked against the live EDUcore graph via
its MCP server (standards inventory, class definitions, crosswalk edges).

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
<<<<<<< Updated upstream
[O*NET](https://www.onetonline.org/) · [schema.org](https://schema.org/) ·
EDUcore · [SKOS](https://www.w3.org/TR/skos-reference/) ·
=======
[schema.org](https://schema.org/) ·
[EduCOR](https://arxiv.org/abs/2107.05522) · [SKOS](https://www.w3.org/TR/skos-reference/) ·
>>>>>>> Stashed changes
[OWL](https://www.w3.org/TR/owl2-overview/).
CIP program codes are real, published by NCES, and used as a controlled vocabulary by
both CEDS and CTDL — which is what the `skos:exactMatch` round in the game turns on.
