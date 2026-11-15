# Pizza BFO Ontology

A pizza ontology aligned to **BFO 2020** - the version of the Basic Formal Ontology that
NFDIcore 3.0.5 builds on - and made from the **BFO and NFDIcore design patterns** that come with
[OntoBoard](https://ebrahimnorouzi.github.io/ontoboard/). It is a test bed for OntoBoard: every
step below is one OntoBoard menu action, every iteration ends in a release with a semantic
version, and every release is a git tag.

| | |
|---|---|
| Ontology IRI | `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo.owl` |
| Latest release | [`pizzabfo.owl`](pizzabfo.owl) and [`pizzabfo-full.owl`](pizzabfo-full.owl); each version under [`releases/`](releases/) |
| Version IRIs | `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo/<version>` |
| Documentation | [The ontology's documentation page](https://ebrahimnorouzi.github.io/pizza-bfo/ontology/index-en.html), written by *OntoBoard > Build and release > Documentation...* (Widoco); the [project site](https://ebrahimnorouzi.github.io/pizza-bfo/) |
| Terms | numbered from the project's ID range: `PIZZABFO_0001000` and up |
| Licence | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| Built with | OntoBoard 1.153.0 in Protégé: an ODK project, its targets run by OntoBoard itself - nothing else installed, no Docker |

## Made again with OntoBoard 1.153.0

This repository was first built with OntoBoard 1.132.0, in the project layout of its own that
OntoBoard used up to 1.135. On 2026-11-15 every release was made again with OntoBoard 1.153.0:
the project of each tag carried over by *OntoBoard > Project > Update project files...* into the
layout the [Ontology Development Kit](https://github.com/INCATools/ontology-development-kit) (ODK)
v1.6.1 writes, committed, and released by *OntoBoard > Build and release > Release...*, which
runs ODK's own `prepare_release` - inside Protégé, by OntoBoard itself. Each release holds the
ontology it always held, under the version IRI it was published with.

One thing was taken out on the way: OntoBoard 1.135 wrote `owl:versionInfo "0.1.0"` into the edit
file, and ODK's release writes the release's own, so the old one is gone from the first commit on.

## The rule this project keeps

**The ontology has no individuals.** It says what pizzas, toppings, bakers and bakings *are*.
Which pizzas a pizzeria sells, who baked them and when is instance data: a separate knowledge
graph in [`kg/`](kg/), made from ROBOT templates, that imports the ontology (from v1.1.0). ODK's
build does not check this; it is a rule kept by hand.

## What it imports

*OntoBoard > Reuse > Imported terms...* lists these with every term each one brings, by label.
They are declared in ODK's configuration, `src/ontology/pizzabfo-odk.yaml`.

| Import | From | How |
|---|---|---|
| `bfo` | BFO 2020, `http://purl.obolibrary.org/obo/bfo/2020/bfo.owl` | 16 terms chosen with *Find terms in another ontology...*; a BOT module ODK rebuilds from that address |
| `bfo_specific_dependence_and_inherence` | pattern library | quality, bearer of, inheres in |
| `bfo_process_site_and_history` | pattern library | occurs in |
| `nfdi-process-role-realization` | pattern library (NFDIcore) | has participant, realizes, occupies temporal region |
| `nfdi-role-borne-by-agent` | pattern library (NFDIcore) | role of, agent |
| `nfdi-temporal-region` | pattern library (NFDIcore) | one-dimensional temporal region, first and last instant |
| `nfdi-organization-identified-located` | pattern library (NFDIcore) | organization, located in, city |

The patterns are modules of the project's own (`module_type: custom`): ODK's refresh leaves them
as they are, and importing the pattern again changes them. Several bring the same terms -
*bearer of*, *agent*, IAO's *information content entity* - and two of them word that last one
differently; *Imported terms...* shows both in its *Also in* column. The quality report is about
this project's own terms only, as ODK's is.

## What you need

1. [Protégé Desktop](https://protege.stanford.edu/) 5.5.0 or 5.6.x.
2. OntoBoard **1.153.0**: put `ontoboard-1.153.0.jar` in Protégé's `plugins` folder (remove any
   other `ontoboard-*.jar` first) and restart Protégé.
3. *OntoBoard > Run self-test*: the line `Build and release > Build (nothing installed) | ok` means
   that ODK's targets run inside Protégé.

## The steps

Every release is two commits - the iteration's work, then the release, tagged. Compare your work
with a tag at any point: `git diff v0.2.0 v0.3.0 -- src/ontology/pizzabfo-edit.owl`.

### v0.1.0 - the project and its requirements

1. *OntoBoard > Project > New ODK project...*: ID `pizzabfo`, title `Pizza BFO Ontology`, base IRI
   `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo.owl`, CC BY 4.0. It writes the project
   ODK itself writes, and makes it a git repository.
2. The XD scoping - stories, competency questions, contextual statements, reasoning
   requirements: [`docs/xd/requirements.md`](docs/xd/requirements.md).
3. *OntoBoard > Build and release > Build...* → `test` passes on the empty project.
4. *OntoBoard > Share > Git...* → *Commit everything, with a message*. *OntoBoard > Build and
   release > Release...*: version `0.1.0`, version IRI `<ontbase>/<version>`, *Commit and tag*.

### v0.2.0 - what a pizza is made of (CQ1-CQ3)

1. *OntoBoard > Reuse > Find terms in another ontology...*: load
   `http://purl.obolibrary.org/obo/bfo/2020/bfo.owl` (it is in the list of suggestions), search and
   tick: object, fiat object part, object aggregate, material entity, quality, role,
   disposition, process, site, one-dimensional temporal region, has continuant part, continuant
   part of, bearer of, inheres in, occurs in, realizes. *Import 16 terms...* → *Add them*.
2. Model, with each new term numbered from your ID range (*New class* on the board, or the class
   tab; the first one asks which of ODK's two ranges is yours): `pizza` (an object) with
   `has base` and `has topping` under BFO 2020's `has continuant part`; bases, toppings, five
   named pizzas, and the defined `cheesy pizza` and `meaty pizza`.
3. The tests in [`src/sparql/`](src/sparql/) for CQ1-CQ3; *Build...* → `test`; commit;
   *Release...* → `0.2.0`. The reasoner finds every named pizza cheesy, and diavola and hawaiian
   meaty ([`docs/cq/answers.md`](docs/cq/answers.md)).

### v0.3.0 - how hot a topping is (CQ4)

1. *OntoBoard > Reuse > Pattern library...*: **Specific Dependence And Inherence** (BFO) →
   *Import terms...* → *Add them*.
2. `spiciness` is a quality, with `mild spiciness` and `hot spiciness` disjoint under it. A topping
   is the `bearer of` its spiciness; `spicy topping` and `spicy pizza` are defined.
3. The reasoner finds chili pepper and spicy salami spicy toppings, and diavola a spicy pizza.
   Commit; *Release...* → `0.3.0`.

### v0.4.0 - who bakes a pizza, where and when (CQ5, CQ6)

1. *Pattern library...*: NFDIcore's **process**, **role**, **temporal** and **organization**
   patterns, and BFO's **Process Site And History**.
2. `pizza baking` is a process that has a pizza as participant, realizes a `pizza baker role`
   (the role of an agent), occurs in a `pizza oven` and occupies a one-dimensional temporal
   region. A `pizzeria` is an organization located in a city.
3. Commit; *Release...* → `0.4.0`.

### v1.0.0 - the first stable release

The README and the release. Nothing in the ontology changed from 0.4.0.

### v1.1.0 - the knowledge graph, from templates

The instance data, kept apart from the ontology: [`kg/`](kg/).

| | |
|---|---|
| Graph | [`kg/pizzabfo-kg.ttl`](kg/pizzabfo-kg.ttl), IRI `https://ebrahimnorouzi.github.io/pizza-bfo/kg.owl` |
| Version IRI | `https://ebrahimnorouzi.github.io/pizza-bfo/kg/1.1.0`; kept as [`kg/releases/1.1.0/`](kg/releases/1.1.0/) |
| Imports | the ontology release it was made for, by its version IRI `.../pizzabfo/1.0.0` - [`kg/catalog-v001.xml`](kg/catalog-v001.xml) maps it to `releases/1.0.0/pizzabfo.owl` |
| Made from | nine ROBOT templates in [`kg/templates/`](kg/templates/): cities, pizzerias, bakers, their roles, ovens, instants, intervals, pizzas, bakings |

The graph is as OntoBoard 1.132.0 made it: it is not part of ODK's release, and the rebuild did
not make it again.

1. In a spreadsheet, nine sheets - each a ROBOT template: your headings, then a row saying what
   each column is (`ID`, `TYPE`, `AL rdfs:label@en`, `I RO:0000057` and so on). A sheet names
   what another sheet makes by its label: a baking names its pizza as `order 1, a margherita`.
   Only the first row of each sheet has an ID; the rest are left blank.
2. Open `kg/pizzabfo-kg.ttl` in Protégé (*File → Open*); its catalog finds the ontology on disk.
3. *OntoBoard > Spreadsheets > Sheet editor*: it opens `kg/templates/` by itself. For each sheet's
   tab, *Generate IRIs...* → *Continue the numbering in these sheets* → *OK*: each sheet continues
   its own numbering, `kg:PB_0000002` after `kg:PB_0000001`. *Save*.
4. *OntoBoard > Spreadsheets > Check sheets...* on `kg/templates/`: nothing to report.
5. *OntoBoard > Spreadsheets > Template...* → *Add the axioms to this ontology*, for each sheet in
   order - cities first, bakings last, so every name a sheet uses already exists. 105 axioms, 25
   individuals. *File → Save*.
6. *Reasoner → HermiT*: consistent; `order 2, a diavola` is a spicy pizza, a cheesy pizza and a
   meaty pizza - from the ontology's definitions, never asserted.
7. The questions in [`kg/cq/`](kg/cq/), answered in [`kg/cq/answers.md`](kg/cq/answers.md): who
   baked each pizza, in which oven and when; which pizzas each pizzeria baked on a day; which of
   them were spicy.

**Dates.** ROBOT does not give a value the datatype of its property's range, so a date typed as
`2026-11-01T18:00:00` becomes text. Write `2026-11-01T18:00:00^^xsd:dateTime`, as
`kg/templates/06_instants.tsv` does; *Template...* warns about a value written the other way when
the property declares a datatype.

## Checking it

*OntoBoard > Build and release > Build...* → `test`: ODK's own `test` - the reasoner, ODK's
checks, the quality report, the OWL profile - and every question in `src/sparql/` asked of the
ontology with its imports (each returns what breaks a rule, so an empty answer passes); all inside
Protégé.

Every push runs the same `test` on GitHub, in ODK's own container (`.github/workflows/qc.yml`);
on your machine, with Docker, `cd src/ontology && sh run.sh make test`.

## Versioning

Each release - ODK's `prepare_release` - stamps `owl:versionIRI <ontbase>/<version>` and
`owl:versionInfo`, and is kept under `releases/<version>/`, from the second release on with
`CHANGES.md`, what changed term by term. *OntoBoard > Build and release > History...* walks
through them in Protégé.

## Licence

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). BFO 2020, NFDIcore and the patterns keep
their own IRIs and licences.
