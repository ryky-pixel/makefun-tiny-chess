# tiny-chess-01 entry — compact Python chess engine

A chess engine in Python 3.13, standard library only, built for make.fun's
tiny-chess-01 bounty ("Build the strongest chess engine in 4 KB of Python",
$500 in USDC on Solana).

## What it is

`main.py` is the whole engine. It plays the 8 gauntlet games of a trial
through the env at `MAKEFUN_ENV_URL` (POST `/game`, `/move`, `/resign`)
and exits when every game is over.

The engine inside is a 0x88-board negamax alpha-beta search with:

- quiescence search over captures and promotions at the leaves,
- MVV-LVA move ordering,
- material evaluation (p 100, n 320, b 330, r 500, q 900) plus
  pawn and knight piece-square tables,
- a fixed node budget per move — no wall clock, no randomness — so a
  replayed trial plays the same moves.

The cleartext engine is about 4.4 KB, over the 4,096-byte cap, so the
committed `main.py` carries it as an lzma-compressed, base64-encoded
payload that unpacks and runs at startup (the same packing trick the
house baseline uses). The committed file is 2,590 bytes (limit: 4,096).

## Repository

- Owner: {owner}
- Repository: {repo}
- Referral code: {referral_code}
- Competition: https://make.fun/bounty/tiny-chess-01

## License

MIT — see LICENSE.
