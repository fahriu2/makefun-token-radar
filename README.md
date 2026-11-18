# makefun-token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/fahriu2/makefun-token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/fahriu2/makefun-token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar ranks 198 pre-token DeFi protocols by the implied value of a future token launch, computed from each protocol's TVL, seven-day growth, chain breadth and age with no token — with a concrete farm plan for every row. Built for make.fun's token-radar-01 bounty; the dashboard is static, offline and deterministic.

## How it scores (radar-2)

Every rankable pre-token protocol gets one implied value from the snapshot's own figures, the same function for every row:

- `base = TVL x 0.22`
- `growth = 7-day change clamped to -50%..+150%, weighted 0.6`
- `breadth = 1 + 0.04 per chain, up to 6 chains`
- `maturity = 0.5 + 0.5 x min(age in days, 1095) / 1095`
- `implied = max(1, round(base x growthMul x breadth x maturity))`

Why each term is there: TVL is the size of the business a token would price; seven-day growth is its momentum, clamped so one hot week cannot double a value and one bad week cannot halve it; chain breadth is distribution, a protocol live on more chains reaches more farmers; age is how long the protocol has run with no token, so a launch would price years of built-up use, not a month of it.

A protocol counts as pre-token when its record carries no token at all: no market cap, no CoinGecko id, no symbol. Protocols whose token already trades are kept apart in the Live view (30 rows by market cap), where the price is a fact, not a model. An unknown listing date counts as one year, the middle of the range. The board keeps the 40 watchlist slugs plus every other pre-token protocol below the floor that is not a wrapped, staked or bridged product of a token that already trades, not a versioned pool and not an exchange. Each board row carries a concrete farm plan, regenerated on the page from the row's own fields.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input snapshot.json
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=2y9ns93n&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
