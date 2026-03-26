# poly_bot

● Now I have the full picture. Here's the deep analysis:

  ---
  Why the Bot Isn't Profitable: Root Cause Analysis

  Problem #1: The Price Filter Is Blocking ~80% of All Bets (Critical)

  This is the #1 operational issue. Out of 537 blocked bet attempts:
  - 468 were too expensive (price > 0.70) — the market was already pricing the outcome at 0.83 on average
  - 69 were the wrong side (price < 0.52)

  Why? By T+3:00 (when the bot bets), the 5-minute window is 60% over. Polymarket participants also watch BTC price — they've already priced in the direction. The market moves from ~0.50 at T+0 to 0.83 average by T+3. Your 0.52–0.70 fair range is correct for early betting but is
  virtually never achievable by T+3.

  You're arriving to the party 3 minutes late. Only 5 actual bets landed in the last 8 hours (out of 439 windows).


Ok how could we fix that? do you think it would be more profitable if fixed?
  ---
  Problem #2: The Coinbase Order Book Feed Is Frozen (Critical Bug)

  Look at every single OB breakdown in the logs:
  CB=Up(0.992)   ← every single window, never changes
  CB=Up(0.992)
  CB=Up(0.992)

  Coinbase is frozen at 0.992 — it's stuck and always voting "Up." This means:
  - OB can never truly be neutral; CB always injects a bullish vote
  - OB=Down requires all 3 other sources (BN, KR, BP) to unanimously vote Down
  - OB=Up fires trivially — just 1 more source agrees with the frozen CB

  Result: OB=Up fires 104 times, OB=Down only 20 times (5:1 ratio). OB accuracy:
  - OB=Up: 46.8% accuracy — below a coin flip
  - OB=Down: 38.9% accuracy — way below random

  The OrderBook signal is actively hurting you. It's not a signal, it's noise + a broken data feed. When CVD and OB disagree (50 windows), CVD was right 60% of the time, OB was right only 40%.

ok remove coinbase then, or fix it if you can - but test it !
  ---
  Problem #3: Signal Quality Reality Check

  ┌───────────┬──────────┬──────────────┬───────────────────────────────┐
  │  Signal   │ Accuracy │   Fires On   │            Verdict            │
  ├───────────┼──────────┼──────────────┼───────────────────────────────┤
  │ CVD       │ ~60–65%  │ ~89 windows  │ ✅ Real signal, works         │
  ├───────────┼──────────┼──────────────┼───────────────────────────────┤
  │ Momentum  │ ~72%     │ ~36 windows  │ ✅ Real signal, works         │
  ├───────────┼──────────┼──────────────┼───────────────────────────────┤
  │ OrderBook │ ~45%     │ ~112 windows │ ❌ Broken — worse than random │
  └───────────┴──────────┴──────────────┴───────────────────────────────┘

  CVD is your real alpha. It measures taker-buy vs taker-sell pressure from 1-min Binance klines. It genuinely predicts the 5-minute BTC direction. The threshold of 0.6 is reasonable.

  Momentum is decent but fires rarely (strong moves are uncommon). The $30 threshold is appropriate.

  OrderBook is broken at two levels: (a) the data feed is frozen, (b) order books in crypto are notoriously unreliable for short-term direction due to spoofing and iceberg orders. Even if you fix CB, the concept is questionable for 5-min windows.

  ---
  Problem #4: The mom_veto Is Net Negative

  When CVD and Momentum disagree, the bot skips. Looking at all 21 mom_veto windows: CVD was right ~5 times (missed good bets) vs the veto was right ~6 times (avoided bad bets). It's roughly break-even but causes you to miss good CVD signals.

  ok what do you suggest here?

  ---
  Is the Core Concept Correct?

  Yes, partially. Using Binance order flow data (CVD) to predict Polymarket BTC binary outcomes is conceptually sound and demonstrably works at 60-65% accuracy. But:

  1. You're betting too late — By T+3:00, the market has already priced in your signal. You need to bet at T+1:00–T+2:00 when the market is still near 50/50.
  2. OB is destroying signal quality — It has a frozen data feed AND is a bad signal concept for this timeframe.
  3. CVD + early entry = the actual edge. The early peek at T+2:00 already exists in the code — it just requires 4/5 OB sources to agree (impossible since CB is frozen).

  ---
  What To Fix

  Immediate (bugs):
  1. Fix the Coinbase order book feed — it's returning 0.992 for every single window

  Strategic:
  2. Shift betting earlier to T+1:30–T+2:00 — the Polymarket price is still near 50/50 then
  3. Decouple from OB — remove OB as a required confirmation signal; make CVD alone sufficient at high confidence ratios (e.g. ratio < 0.35 or > 0.65)
  4. Re-evaluate the price filter — for T+2 betting, 0.52–0.70 might be achievable. For T+3, it's almost never achievable

  The SNIPE at T+4:45 went 2/2 wins in dry mode — late momentum IS real but the price is always blocked by then too.

✻ Cogitated for 8m 3s