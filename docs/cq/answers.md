# Competency questions, answered

Each query in this folder run against the released `pizzabfo.owl` (reasoned with ELK), with OntoBoard > ROBOT > SPARQL... Regenerated on every release.

## CQ1: What parts does a pizza have - its base and its toppings?

`cq1_parts_of_a_pizza.rq` - 2 row(s)

| part_relation | kind_of_part |
|---|---|
| has base | pizza base |
| has topping | pizza topping |

## CQ2: Which toppings does each named pizza have?

`cq2_toppings_of_each_pizza.rq` - 16 row(s)

| pizza | topping |
|---|---|
| diavola | mozzarella topping |
| diavola | spicy salami topping |
| diavola | tomato topping |
| funghi | mozzarella topping |
| funghi | mushroom topping |
| funghi | tomato topping |
| hawaiian | ham topping |
| hawaiian | mozzarella topping |
| hawaiian | pineapple topping |
| hawaiian | tomato topping |
| margherita | mozzarella topping |
| margherita | tomato topping |
| quattro formaggi | gorgonzola topping |
| quattro formaggi | mozzarella topping |
| quattro formaggi | parmesan topping |
| quattro formaggi | tomato topping |

## CQ3: Which pizzas are cheesy, and which have meat? (inferred by the reasoner)

`cq3_cheesy_and_meaty_pizzas.rq` - 7 row(s)

| pizza | kind |
|---|---|
| diavola | cheesy pizza |
| funghi | cheesy pizza |
| hawaiian | cheesy pizza |
| margherita | cheesy pizza |
| quattro formaggi | cheesy pizza |
| diavola | meaty pizza |
| hawaiian | meaty pizza |

## CQ4: Which toppings are hot, and so which pizzas are spicy? (inferred by the reasoner)

`cq4_spicy_toppings_and_pizzas.rq` - 3 row(s)

| kind | member |
|---|---|
| spicy pizza | diavola |
| spicy topping | chili pepper topping |
| spicy topping | spicy salami topping |
