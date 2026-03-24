# test123

● Built. Active rules now:

  ┌─────────────────────────┬──────────┐
  │        Condition        │  Action  │
  ├─────────────────────────┼──────────┤
  │ Profit ≥ +80%           │ Sell ALL │
  ├─────────────────────────┼──────────┤
  │ Last 60s + profit ≥ 55% │ Sell ALL │
  ├─────────────────────────┼──────────┤
  │ Last 5s + any profit    │ Sell ALL │
  └─────────────────────────┴──────────┘

  ---
  More model ideas (ranked by how testable they are with your current data):

  High signal quality:

  1. Bid/ask imbalance at entry — if the Polymarket token's own order book is heavily stacked on one side (e.g. 10x more
   asks than bids for an Up token), skip. The market itself is telling you it won't go higher. You already fetch the
  book for pricing, just check the depth ratio.
  2. CVD trend direction, not just threshold — instead of a single 5-min CVD ratio, check if CVD is rising (last candle
  CVD > previous candle CVD). Flat CVD at 0.56 is weaker than CVD climbing from 0.52 → 0.56 → 0.59.
  3. BTC price distance from round numbers — BTC tends to stall/reverse at round thousands ($95k, $96k, etc). If price
  is within $200 of a round number and you'd be betting it continues through, skip or reduce size.
  4. Time-of-day filter — now that you have weeks of data, you can check: does your win rate drop after 10pm ET or
  before 9am? Some hours have thin Polymarket liquidity and your signals are noisier.

  Medium complexity:

  5. Spread-based size adjustment — you already skip on spread > MAX_SPREAD, but you could size down (bet $1 instead of
  $3) when spread is in the 0.02–0.03 range. Tight spread = confident market, wide spread = uncertain.
  6. Volume spike gate — if Binance 1-min volume just doubled vs the prior 3-min average, something is happening. Strong
   CVD + volume spike = size up. CVD without volume = normal bet.
  7. Chainlink vs Binance divergence — if CL price and Binance disagree by more than $50, the data feeds are lagging
  each other. Skip that window entirely, the PTB comparison becomes unreliable.