# CompProof: Airbnb photo-analysis agent (capstone)

A one-file prototype that compares my Airbnb listing's photos against anonymized competing listings and proposes evidence-backed, reviewable changes (for example, which photo should lead).

Built for the Product Faculty AI capstone.

## How it works
Plan → retrieve → generate → self-check:
1. **Plan:** checks the request is in scope and the data is complete.
2. **Retrieve:** picks competitors with higher occupancy than mine, plus matching expert notes.
3. **Generate:** proposes a change, citing named competitors (Claude via the course `PFAI` helper, or a labelled sample mode).
4. **Self-check:** fixed rules plus an AI re-check mark each card verified or flagged.

Each card carries a rubric-based confidence rating (share of supporting competitors × expert-note fit). I approve, request revision or reject each one, and decisions go to a downloadable run log.

## Live demo
https://capstone.productfaculty.com/joshkehoe

## Run it
Open `index.html` in a browser. It starts in **sample mode** with made-up demo data (illustrations in `assets/`). To use the real AI, paste your own Claude API key in the page. Keys are never stored in this repo.

## Contents
- `index.html`: the whole prototype
- `capstone.json`, `assets/`: course upload files and demo illustrations
- `docs/PRD.md`: product requirements

All data here is made up. My real listing and competitor data is not included.
