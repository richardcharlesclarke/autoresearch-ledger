# Autoresearch Ledger

Shared experiment ledger for Apple Silicon `autoresearch-mlx` runs on comparable hardware.

## Purpose

This repo is the machine-readable source of truth for:

- completed experiments
- the current best known recipe
- the exact parameter changes that led to each result

It is meant to be shared across multiple agents so they can avoid repeating work and branch from the latest good recipe.

## Files

- `experiments.jsonl`
  Append-only log. One JSON object per experiment.
- `best-known.json`
  The current best kept recipe and the experiment that established it.

## Minimal protocol

1. Pull latest changes before choosing a new experiment.
2. Read `best-known.json` and the most recent lines of `experiments.jsonl`.
3. Choose the next experiment relative to the best current kept recipe.
4. Run the experiment.
5. Append one new JSON line to `experiments.jsonl`.
6. If the experiment wins, update `best-known.json`.
7. Commit and push.

## Notes

- Keep the ledger compact and structured.
- Record exact parameter changes rather than vague summaries.
- Completed experiments only should go into `experiments.jsonl`.
- In-progress experiments can be tracked elsewhere locally, but they should only be written here once they complete or crash.
