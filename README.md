# SOLVD nonogram solver

Solver for [SOLVD](https://solvd.art) nonogram mint challenges — including
112×112 tier-6 boards. A fast C core does the solving; Python runners drive it
in parallel and verify every answer against the clues before submitting.

## Components

- **`nonobp.c`** — the core solver in C: line propagation plus guessing with
  backtracking and restarts.
  Build: `gcc -O3 -march=native -o nonobp nonobp.c`
- **`psolve.py`** — runs several `nonobp` copies in parallel with different
  settings, takes the first answer, checks it against every clue, and writes
  the answer as hex. Handles any number of boards of any size.
  Usage: `python3 psolve.py challenge.json answer.json`
  (set `BIN` at the top of the file to your `nonobp` path)
- **`main.py` + `common.py`** — the 1-minute loop: log in to SOLVD, fetch a
  challenge, solve it, submit, then mint through the `baw` CLI (Binance
  Agentic Wallet). Paths in these files are from my machine (`/workspace/solvd/...`)
  — change them to match yours.

## Benchmarks

- One 112×112 tier-6 board: ~5–8 s
- Four 56×56 boards: ~1.4 s
