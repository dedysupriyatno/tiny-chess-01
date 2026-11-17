# tiny-chess-01 entry

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/dedysupriyatno/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/dedysupriyatno/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

Built for the [make.fun bounty "Build the strongest chess engine in 4 KB of Python"](https://make.fun/bounty/tiny-chess-01).

Single-file Python engine (4,027 bytes, stdlib only), packed with
`makefun compress` from the readable `source.py` (11,171 bytes) in
this folder. Talks to the env exactly like the starter (POST /game,
POST /move, loop until done).

Search: iterative-deepening negamax alpha-beta, bound-type
transposition table (EXACT/LOWER/UPPER + depth, Zobrist keys with a
fixed seed), null-move pruning (depth >= 4, non-pawn material >= 900,
not in check), late-move reductions (depth >= 3, moves after the
first 3, non-capture non-promotion, no re-search), killer moves and
MVV-LVA capture ordering, quiescence over captures, promotions and
check evasions, PVS-style re-search at the root only. Fixed
100,000-node budget per move (no clock). Eval: material
(100/320/330/500/900) + piece-square tables + bishop-pair bonus,
kept incrementally in make/unmake, with tracked king squares.

Tests: perft passes on all standard positions (startpos d4 197,281;
Kiwipete d4 4,085,603; pos4 d3 9,467; pos5 d3 62,379) when all four
promotion pieces are counted; this engine generates queen and
knight promotions only, as specified. Determinism verified (same
position twice = same move).

Local practice trial-0: 3/6, Elo 1,279 — above the 1,154 practice
floor. Wins by checkmate vs depth-2, depth-3 and depth-4; losses by
checkmate vs nodes-100k, nodes-250k and nodes-500k. Moves: 628,
max 5,340 ms, avg 1,780 ms, no timeouts.
