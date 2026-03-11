# Pokémon Evolution Stage Classifier

Predicts a Pokémon's evolution stage from its base stats, using a classifier trained on Gens 1–3 and tested against Gen 4 as a generalization benchmark.

---

## What it does

- Pulls base stats and species metadata from the [PokéAPI](https://pokeapi.co/) for all Gen 1–4 Pokémon
- Labels each Pokémon as one of four classes:
  - **Stage 1** — Base form (e.g. Bulbasaur, Pikachu)
  - **Stage 2** — First evolution (e.g. Ivysaur, Raichu)
  - **Stage 3** — Second evolution (e.g. Venusaur, Charizard)
  - **Legendary** — Legendary or Mythical (e.g. Mewtwo, Dialga)
- Trains and compares Logistic Regression, Random Forest, and Gradient Boosting classifiers on Gen 1–3
- Evaluates the best model on a held-out Gen 4 set it has never seen

---

## Notebook walkthrough

| Section | Description |
|---|---|
| 1. Install & Import | Library setup |
| 2. Fetch Data | API calls to pull stats + evolution chains for Gen 1–4 |
| 3. EDA | Stage distributions, stat histograms, Gen 1–3 vs Gen 4 comparison, correlation heatmap |
| 4. Feature Engineering | Train/test split (80/20 on Gen 1–3); Gen 4 held out entirely |
| 5. Train & Compare | 5-fold cross-validation across three models |
| 6. Best Model Evaluation | Classification report + confusion matrix on Gen 1–3 holdout |
| 7. Gen 4 Generalization | How well the model transfers to unseen Pokémon |
| 8. Predict Any Pokémon | `predict_evolution_stage("lucario")` — works by name or Pokédex ID |
| 9. Summary | Accuracy table and key findings |

---

## Features used

`hp`, `attack`, `defense`, `special_attack`, `special_defense`, `speed`, `total`, `base_experience`, `weight`, `height`

---

## Notes

- `class_weight='balanced'` is set on all classifiers to handle the small Legendary class
- Evolution stages are capped at 3 for non-legendaries (branched evolutions like Eevee collapse to stage 1)
- The Gen 4 test set is never touched during training or model selection
