 2. Betfair Exchange — Tennis In-Play Bot

  Betfair is the largest betting exchange in the world (~$60B/year volume). Critically, it's a peer-to-peer exchange — no bookmaker, just a 5% commission on net winnings.

  Why tennis is the best market algorithmically:

  - Point-by-point probability is fully quantifiable via Markov chains
  - Inputs: server hold %, first serve %, break probability — all historically documented
  - Given the current score + server, you can compute exact win probability
  - Betfair odds often lag this by 2–5 seconds in-play — that's your edge

  What the bot does:
  1. Connect to Betfair Streaming API (WebSocket, free)
  2. Subscribe to live match odds
  3. Run a Monte Carlo / Markov model of match state → true probability
  4. When market_implied_probability diverges from model_probability by >2%, bet
  5. Target: 1–3% ROI per bet, ~10–20 bets per match

  Technical fit: betfairlightweight Python library, streaming API is almost identical to the WebSocket feeds you already use. Your Rust bot could handle the latency-sensitive parts.

  Real edge available: Yes, because the market is set by humans reacting to points, not algorithmic models. For the first 10–15 minutes of a match, markets are often stale.

 I love this idea, but the downside in slovenia i dont have access to Betfair exchange, is there anything similar? :) 
 

