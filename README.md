# tiny-chess-01 entry

Single-file Python engine (4,094 bytes, stdlib only), packed with lzma +
base85 + a 2-line unpacker. Talks to the env exactly like the starter
(POST /game, POST /move, loop until done).

Search: iterative-deepening negamax alpha-beta, bound-type transposition
table (EXACT/LOWER/UPPER + depth, Zobrist), null-move pruning (depth >= 4,
depth-3), late-move reductions (depth >= 3, moves after the first 3, no
re-search), killer moves (one per ply), MVV-LVA capture ordering,
quiescence (captures/promotions/check evasions), PVS-style root re-search
on tied scores, fixed 150,000-node budget per move (no clock).
Eval: material (100/320/330/500/900) + piece-square tables matching the
house engine (pawn/knight/bishop + opening king table), incremental.

Tests: perft passed on all standard positions (startpos d4 197,281;
Kiwipete d4 4,085,603; pos4 d3 9,467; pos5 d3 62,379); deterministic
(same position twice = same move). Local practice trials (6 games each):
trial-0 2.5/6, Elo 1,191, max move 5.3s, avg 4.0s, total ~1,100s;
trial-1 2.5/6, Elo 1,191, max move 6.0s, avg 4.2s. Above the 1,154
practice floor, below the ~1,365 sunfish baseline. v1 was 2.0/6, ~1,099.
