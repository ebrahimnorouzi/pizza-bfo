# Pizza BFO Ontology

A pizza ontology aligned to BFO 2020 - the BFO that NFDIcore 3.0.5 builds on - and made from BFO and NFDIcore design patterns. It holds no individuals: its instance data is a separate knowledge graph built from ROBOT templates.

This site is published from the `docs/` folder of this repository by
GitHub Actions, every time `main` changes.

## Getting the ontology

| What | Where |
|---|---|
| Browse | `https://ebrahimnorouzi.github.io/pizza-bfo/pizzabfo.owl` |
| Edit file | `src/ontology/pizzabfo-edit.owl` |
| Released file | `pizzabfo.owl` |
| Documentation | [The ontology's documentation page](ontology/index-en.html) |

Edit the **edit file**, never the released one: the released file is produced
by the build and is overwritten by it.

## Turning this site on

GitHub does not publish Pages until it is asked. Once, in the repository's
**Settings > Pages**, set the source to **Deploy from a branch** and choose
the `gh-pages` branch - the workflow creates that branch the first time it
runs. The site then appears at `https://<owner>.github.io/<repository>/`.
