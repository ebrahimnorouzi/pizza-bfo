# Requirements (eXtreme Design scoping)

Written before modelling. Each iteration takes one or two stories, finds the design pattern
that answers them, and ends in a release.

## Principles

- **Aligned to BFO 2020**, the version of the Basic Formal Ontology that NFDIcore 3.0.5 uses
  (its `entity`, `material entity`, `quality`, `role`, `process`, `one-dimensional temporal
  region` and the 2020 relations such as `has continuant part`).
- **Patterns, not invention**: the BFO and NFDIcore patterns bundled with OntoBoard.
- **No individuals in the ontology.** It says what pizzas, toppings, bakers and bakings *are*.
  Which pizzas a pizzeria actually sells and bakes is instance data: a separate knowledge graph,
  filled from ROBOT templates (`kg/`), that imports the ontology.

## User stories

| | Story |
|---|---|
| S1 | As a menu planner, I want to describe a pizza by its base and toppings, so that menus can be compared. |
| S2 | As a guest, I want to know which pizzas are spicy, so that I can avoid or choose them. |
| S3 | As a pizzeria, I want to record who baked a pizza, in which oven and when, so that orders can be traced. |
| S4 | As a data steward, I want the pizzeria's menu and bakings recorded as data, not in the ontology, so that the ontology stays reusable. |

## Competency questions

| | Question | Story | Iteration |
|---|---|---|---|
| CQ1 | What parts does a pizza have - its base and its toppings? | S1 | 1 |
| CQ2 | Which toppings does each named pizza have? | S1 | 1 |
| CQ3 | Which pizzas are cheesy, and which have meat? | S1 | 1 |
| CQ4 | Which toppings are hot, and so which pizzas are spicy? | S2 | 2 |
| CQ5 | Who baked a given pizza, in which oven, and over which period? | S3 | 3 |
| CQ6 | Which role does a baker realize in a baking? | S3 | 3 |
| CQ7 | Which pizzas did a pizzeria bake on a given day? (answered by the knowledge graph) | S4 | KG |

## Contextual statements

- A pizza is an `object` (BFO); its base is a `fiat object part` of it and its toppings are
  `material entity` parts - related with BFO 2020's `has continuant part`.
- Spiciness is a `quality` that `inheres in` a topping; a topping is its `bearer`.
- Baking a pizza is a `process` that `realizes` a baker `role`, `occurs in` an oven and
  `occupies` a one-dimensional temporal region; the role is the `role of` an agent.

## Reasoning requirements

- A pizza with a cheese topping is a `cheesy pizza`; with a meat topping, a `meaty pizza`.
- A topping that bears a hot spiciness is a `spicy topping`, and a pizza that has one is a
  `spicy pizza` - found by the reasoner, never asserted.
- The ontology must stay in OWL 2 EL, so ELK classifies it.
