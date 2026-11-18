# Tiny Chess — a 4 KB chess engine

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Jeytm/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Jeytm/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An entry for [tiny-chess-01](https://make.fun/bounty/tiny-chess-01): the
strongest chess engine I could fit in 4 KB of Python.

## How it plays

- 0x88 board, negamax search with alpha-beta pruning
- Iterative deepening to a fixed node budget (100,000 nodes a move early
  in a game, stepping down as games go long) — no clock reads anywhere,
  so a replayed game plays the same moves
- Transposition table, killer moves, and MVV-LVA move ordering
- Null-move pruning (depth reduction 2, skipped in check and without
  non-pawn material)
- Quiescence search over captures, promotions, and check evasions
- Incremental material plus piece-square evaluation, a bishop-pair
  bonus, and middlegame/endgame king tables picked by total material

`main.py` is the whole engine. It speaks HTTP to the game environment
(`POST /game`, `POST /move`, `POST /resign`) and nothing else: no model
calls, no other files, no randomness. The packed file is produced from
a readable source with `makefun compress`; the packed bytes are what is
graded, and they measure 3,988 bytes — under the 4,096 cap.

## License

MIT — see LICENSE.
