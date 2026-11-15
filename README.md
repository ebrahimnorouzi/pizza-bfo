# Pizza BFO Ontology

A pizza ontology aligned to **BFO 2020** - the version of the Basic Formal Ontology that
NFDIcore 3.0.5 builds on - and made from the **BFO and NFDIcore design patterns** that come with
[OntoBoard](https://ebrahimnorouzi.github.io/ontoboard/). It is a test bed for OntoBoard: every
step below is one OntoBoard menu action, every iteration ends in a release with a semantic
version, and every release is a git tag.

| | |
|---|---|
| Ontology IRI | `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo.owl` |
| Latest release | [`pizzabfo.owl`](pizzabfo.owl), [`pizzabfo.ttl`](pizzabfo.ttl); each version under [`releases/`](releases/) |
| Version IRIs | `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo/<version>` |
| Terms | numbered from the project's ID range: `PIZZABFO_0001000` and up |
| Licence | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| Built with | OntoBoard 1.132.0 in Protégé - nothing else installed |

## The rule this project keeps

**The ontology has no individuals.** It says what pizzas, toppings, bakers and bakings *are*.
Which pizzas a pizzeria sells, who baked them and when is instance data: a separate knowledge
graph in [`kg/`](kg/), made from ROBOT templates, that imports the ontology (from v1.1.0). The
release script checks it: a release with an individual in it is refused.

## What it imports

*OntoBoard → Imported terms...* lists these with every term each one brings, by label.

| Import | From | How |
|---|---|---|
| `bfo` | BFO 2020, `http://purl.obolibrary.org/obo/bfo/2020/bfo.owl` | 16 terms chosen with *Find terms in another ontology...*; BOT module |
| `bfo_specific_dependence_and_inherence` | pattern library | quality, bearer of, inheres in |
| `bfo_process_site_and_history` | pattern library | occurs in |
| `nfdi-process-role-realization` | pattern library (NFDIcore) | has participant, realizes, occupies temporal region |
| `nfdi-role-borne-by-agent` | pattern library (NFDIcore) | role of, agent |
| `nfdi-temporal-region` | pattern library (NFDIcore) | one-dimensional temporal region, first and last instant |
| `nfdi-organization-identified-located` | pattern library (NFDIcore) | organization, located in, city |

Several of the patterns bring the same terms - *bearer of*, *agent*, IAO's *information content
entity* - and two of them word that last one differently. *Imported terms...* shows both in its
*Also in* column. The build's quality report is about this project's own terms only
(`robot_report` in `src/ontology/pizzabfo-odk.yaml`), as ODK's is; those differences belong to the
ontologies the terms come from.

## The steps

Compare your work with a tag at any point: `git diff v0.2.0 v0.3.0 -- src/ontology/pizzabfo-edit.owl`.

### v0.1.0 - the project and its requirements

1. *OntoBoard → Project → New ODK project...*: ID `pizzabfo`, title `Pizza BFO Ontology`, base IRI
   `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo.owl`, CC BY 4.0.
2. The XD scoping - stories, competency questions, contextual statements, reasoning
   requirements: [`docs/xd/requirements.md`](docs/xd/requirements.md).
3. *Project → Build...* → `test` passes on the empty project. *Project → Release...* → `0.1.0`.

### v0.2.0 - what a pizza is made of (CQ1-CQ3)

1. *OntoBoard → Find terms in another ontology...*: load
   `http://purl.obolibrary.org/obo/bfo/2020/bfo.owl` (it is in the list of suggestions), search and
   tick: object, fiat object part, object aggregate, material entity, quality, role,
   disposition, process, site, one-dimensional temporal region, has continuant part, continuant
   part of, bearer of, inheres in, occurs in, realizes. *Import 16 terms...* → *Add them*.
2. Model, with each new term numbered from your ID range (*New class* on the board, or the class
   tab): `pizza` (an object) with `has base` and `has topping` under BFO 2020's `has continuant
   part`; bases, toppings, five named pizzas, and the defined `cheesy pizza` and `meaty pizza`.
3. The tests in [`src/sparql/`](src/sparql/) for CQ1-CQ3; *Build...* → `test`; *Release...* →
   `0.2.0`. The reasoner finds every named pizza cheesy, and diavola and hawaiian meaty
   ([`docs/cq/answers.md`](docs/cq/answers.md)).

### v0.3.0 - how hot a topping is (CQ4)

1. *ROBOT → Pattern library...*: **Specific Dependence And Inherence** (BFO) → *Import terms...*.
2. `spiciness` is a quality, with `mild spiciness` and `hot spiciness` disjoint under it. A topping
   is the `bearer of` its spiciness; `spicy topping` and `spicy pizza` are defined.
3. The reasoner finds chili pepper and spicy salami spicy toppings, and diavola a spicy pizza.
   *Release...* → `0.3.0`.

### v0.4.0 - who bakes a pizza, where and when (CQ5, CQ6)

1. *Pattern library...*: NFDIcore's **process**, **role**, **temporal** and **organization**
   patterns, and BFO's **Process Site And History**.
2. `pizza baking` is a process that has a pizza as participant, realizes a `pizza baker role`
   (the role of an agent), occurs in a `pizza oven` and occupies a one-dimensional temporal
   region. A `pizzeria` is an organization located in a city.
3. *Project → Update project files...* brings the Makefile up to date with the scoped report.
   *Release...* → `0.4.0`.

### v1.0.0 - the first stable release

This README, and the release. Nothing in the ontology changed from 0.4.0.

### v1.1.0 - the knowledge graph, from templates

The instance data, kept apart from the ontology: [`kg/`](kg/).

| | |
|---|---|
| Graph | [`kg/pizzabfo-kg.ttl`](kg/pizzabfo-kg.ttl), IRI `https://ebrahimnorouzi.github.io/pizza-bfo/kg.owl` |
| Version IRI | `https://ebrahimnorouzi.github.io/pizza-bfo/kg/1.1.0`; kept as [`kg/releases/1.1.0/`](kg/releases/1.1.0/) |
| Imports | the ontology release it was made for, by its version IRI `.../pizzabfo/1.0.0` - [`kg/catalog-v001.xml`](kg/catalog-v001.xml) maps it to `releases/1.0.0/pizzabfo.owl` |
| Made from | nine ROBOT templates in [`kg/templates/`](kg/templates/): cities, pizzerias, bakers, their roles, ovens, instants, intervals, pizzas, bakings |

1. In a spreadsheet, nine sheets - each a ROBOT template: your headings, then a row saying what
   each column is (`ID`, `TYPE`, `AL rdfs:label@en`, `I RO:0000057` and so on). A sheet names
   what another sheet makes by its label: a baking names its pizza as `order 1, a margherita`.
   Only the first row of each sheet has an ID; the rest are left blank.
2. Open `kg/pizzabfo-kg.ttl` in Protégé (*File → Open*); its catalog finds the ontology on disk.
3. *OntoBoard → Knowledge graph → Sheet editor*: it opens `kg/templates/` by itself. For each
   sheet's tab, *Generate IRIs...* → *Continue the numbering in these sheets* → *OK*: each sheet
   continues its own numbering, `kg:PB_0000002` after `kg:PB_0000001`. *Save*.
4. *Knowledge graph → Check sheets...* on `kg/templates/`: nothing to report.
5. *Knowledge graph → Template...* → *Add the axioms to this ontology*, for each sheet in order -
   cities first, bakings last, so every name a sheet uses already exists. 105 axioms, 25
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

*OntoBoard → Project → Build...* → `test`: the reasoner, the quality report, every query in
`src/sparql/` (each returns what breaks a rule, so an empty answer passes) and the OWL 2 DL
profile check - all inside Protégé.
