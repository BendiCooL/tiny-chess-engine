# tiny-chess-engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/BendiCooL/tiny-chess-engine/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/BendiCooL/tiny-chess-engine/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine that fits in 4 KB of Python: negamax search with a transposition table, quiescence and tapered piece-square evaluation, driven by a fixed node budget so every move is deterministic. It plays the make.fun house gauntlet through the trial env.

## Inside

- PVS alpha-beta with iterative deepening and a transposition table
- Quiescence over captures and promotions, with check evasions
- Null-move pruning, late-move reductions, check extensions, killer-move ordering, repetition = draw in search
- Evaluation: material + piece-square tables with a king midgame/endgame taper, bishop pair, incremental Zobrist keys
- Fixed node budget per move (62k, tapered down late in the game), so play is fully deterministic

The readable source (`engine_src.py`, kept beside the repo, not committed) is packed into the 4,084-byte `main.py` with the kit's own `makefun compress`. Local practice trials against the house gauntlet (depth-2 through nodes-500k) are run before submitting; this build scored 10.5/18 across the three practice instances (per-instance Elo estimates 1364 / 1654 / 1099 against the Sunfish baseline's 1364 / 1451 / 1279). A fuller-featured development build scored 12.5/18 in practice but did not fit in 4 KB once packed.

## Run it

```sh
MAKEFUN_ENV_URL=http://store:8080 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=wg2zeety&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
