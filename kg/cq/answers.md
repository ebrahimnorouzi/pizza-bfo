# Questions about the knowledge graph, answered

Each query in this folder run against `pizzabfo-kg.ttl` together with the ontology it imports and the reasoner's conclusions about each individual, with OntoBoard > ROBOT > SPARQL...

## CQ5: Who baked each pizza, in which oven, and over which period?

`cq5_who_baked_each_pizza.rq` - 3 row(s)

| pizza | baker | oven | from | to |
|---|---|---|---|---|
| order 1, a margherita | Luigi Rossi | wood-fired oven at Da Luigi | 2026-11-01T18:00:00 | 2026-11-01T18:02:00 |
| order 2, a diavola | Luigi Rossi | wood-fired oven at Da Luigi | 2026-11-01T18:05:00 | 2026-11-01T18:08:00 |
| order 3, a quattro formaggi | Maria Esposito | oven at Napoli Centrale | 2026-11-01T19:30:00 | 2026-11-01T19:33:00 |

## CQ7: Which pizzas did each pizzeria bake on 2026-11-01, and in which city?

`cq7_pizzas_per_pizzeria_on_a_day.rq` - 3 row(s)

| pizzeria | city | pizza | started |
|---|---|---|---|
| Pizzeria Da Luigi | Karlsruhe | order 1, a margherita | 2026-11-01T18:00:00 |
| Pizzeria Da Luigi | Karlsruhe | order 2, a diavola | 2026-11-01T18:05:00 |
| Pizzeria Napoli Centrale | Naples | order 3, a quattro formaggi | 2026-11-01T19:30:00 |

## Which of the pizzas baked are spicy, and who baked them? (the reasoner's conclusion)

`cq8_spicy_pizzas_baked.rq` - 1 row(s)

| pizza | baker |
|---|---|
| order 2, a diavola | Luigi Rossi |
