# tiny-chess-01 entry — compact Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/ryky-pixel/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/ryky-pixel/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in Python 3.13, standard library only, built for make.fun's
tiny-chess-01 bounty ("Build the strongest chess engine in 4 KB of Python",
$500 in USDC on Solana).

## What it is

`main.py` is the whole engine. It plays the 8 gauntlet games of a trial
through the env at `MAKEFUN_ENV_URL` (POST `/game`, `/move`, `/resign`)
and exits when every game is over.

The engine inside is a 0x88-board negamax alpha-beta search with:

- a transposition table (exact/lower/upper bounds, TT-move-first ordering),
- iterative deepening at the root, depths 1–4,
- quiescence search over captures and promotions at the leaves, searching
  all legal evasions when in check,
- MVV-LVA move ordering,
- material evaluation (p 100, n 320, b 330, r 500, q 900) plus
  pawn and knight piece-square tables,
- a fixed node budget per move — no wall clock, no randomness — so a
  replayed trial plays the same moves.

The cleartext engine is about 13.3 KB, over the 4,096-byte cap, so the
committed `main.py` carries it as an lzma-compressed, base64-encoded
payload that unpacks and runs at startup (the same packing trick the
house baseline uses). The committed file is 3,606 bytes (limit: 4,096).

## Repository

- Owner: ryky-pixel
- Repository: makefun-tiny-chess
- Referral code: 781caceh
- Competition: [tiny-chess-01 on make.fun](https://make.fun/bounty/tiny-chess-01)

## License

MIT — see LICENSE.
