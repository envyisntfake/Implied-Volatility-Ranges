# IV Bands Day Types: Identification & Playbook

Framework for trading 1‑Day Implied Volatility Bands (±1σ/±2σ/±3σ) derived from VIX/VXN.

## Core Formula (Daily Bands)
**Bands_k = C ± k · ( C · IV / √252 )** with k ∈ {1,2,3}.  
**C**: prior close/settle of the underlying (SPX/ES or NDX/NQ, be consistent).  
**IV**: prior day close of the relevant implied volatility index as decimal (VIX for S&P, VXN for NAS).  
Round final levels to the instrument’s tick (ES/NQ = 0.25).

# What each band “means” (under a normal-returns model):

 - ±1σ band: ~68% of days are expected to finish inside this range.
 - ±2σ band: ~95% of days should finish inside.
 - ±3σ band: ~99.7% containment.

These are finish-the-day probabilities, not guarantees, and real markets have fat tails.

## Day Types Overview
| # | Name | Quick Definition | Primary Edge |
|---|------|------------------|--------------|
| 1 | Opening Fade (fail back inside ±1σ) | Open or early push outside ±1σ then close back inside | Mean reversion to C/VWAP |
| 2 | Trend Break & Hold at ±1σ | Break and hold above +1σ (or below −1σ) with successful retest | Continuation to ±2σ/±3σ |
| 3 | 1σ Pullback in Trend | Impulse beyond ±1σ, orderly pullback to ±1σ, continuation | Buy/sell the dip at ±1σ |
| 4 | 2σ Exhaustion Fade | First touch of ±2σ with momentum/volume divergence | Reversion to ±1σ then VWAP |
| 5 | Gap Logic | Open outside band; either gap-and-go or gap-fill toward C | Follow/fade based on early confirmation |
| 6 | Opening Range (OR) Filter | Break/hold of OR aligned with ±1σ location | Filter for higher-probability breakouts |

---

## 1. Opening Fade (Fail Back Inside ±1σ)
### Identification
- Open/early drive outside +1σ/−1σ.
- Within 15–30m, a 3–5m candle closes back inside the band.
- Delta/volume stall; wick rejection; RSI rolls from >70 or <30.

### Trade Plan
- Enter in reversion direction (short from failed +1σ, long from failed −1σ).
- Stop: 0.35–0.50σ beyond the failed band extreme.
- Targets: VWAP or C, then opposite 0.5σ; trail on VWAP/20-EMA.

### Invalidation
- Full 5–10m close back outside the band after entry.
- New catalyst or strong breadth against the fade.

---

## 2. Trend Break & Hold at ±1σ
### Identification
- Clean break through +1σ (or −1σ) with expanding volume/breadth.
- Retest holds as support/resistance (band flip).
- VWAP and 20-EMA aligned with move; HH/HL or LL/LH print.

### Trade Plan
- Enter on retest/hold with confirmation candle.
- Stop: 0.25–0.35σ outside the band or below retest swing.
- Targets: ±2σ; runner to ±3σ; trail with 20-EMA or 0.5σ pullback.

### Invalidation
- Loss of ±1σ on a closing basis with volume (failed flip).
- Internals diverge persistently against the move.

---

## 3. 1σ Pullback in Trend (Continuation)
### Identification
- Impulse beyond ±1σ sets direction.
- Orderly pullback to ±1σ; pullback volume/delta lighter than impulse.
- Reversal signal at band and continuation of structure.

### Trade Plan
- Enter at ±1σ with reversal print in trend direction.
- Stop: 0.25–0.35σ past the band.
- Targets: impulse extreme → ±2σ; scale then trail.

### Invalidation
- Deep close back inside prior range with VWAP loss.
- Second rejection at band without follow-through.

### Notes
- Use anchored VWAP from session open or morning pivot for confluence.

---

## 4. 2σ Exhaustion Fade
### Identification
- First touch of ±2σ in session.
- Momentum divergences (price extreme without confirmation by RSI/MACD/delta).
- Large wick or failure to close beyond ±2σ.

### Trade Plan
- Enter fade on first 5m close back inside ±2σ.
- Stop: 0.35–0.50σ beyond ±2σ extreme.
- Targets: ±1σ then VWAP; scale at ±1σ, trail remainder.

### Invalidation
- Strong continuation closes beyond ±2σ with rising volume.
- Fresh catalyst extends the move.

---

## 5. Gap Logic with Bands
### Identification
- Open outside ±1σ (gap > 0.5σ).
- Gap-and-go: holds outside band first 15–30m; Gap-fill: fails back inside quickly.
- Check ON delta, early breadth, and news calendar.

### Trade Plan
- Gap-and-go: trade with gap direction on pullback to band; target ±2σ.
- Gap-fill: fade back inside toward C/VWAP; partials at VWAP then 0.5σ.
- Stops: 0.30–0.45σ depending on liquidity/open volatility.

### Invalidation
- Behavior flips against plan (e.g., rebreak/hold outside when attempting fill).
- Outlier opening auction imbalance.

---

## 6. Opening Range (OR) Filter with ±1σ
### Identification
- Define OR (first 15–30m).
- OR high above +1σ or OR low below −1σ increases continuation odds.
- Retest of OR boundary aligns with ±1σ.

### Trade Plan
- Enter only if OR break aligns with band and holds on retest.
- Stop: beyond OR boundary or 0.35σ (whichever is tighter).
- Targets: ±2σ then trail; or measured move of OR range.

### Invalidation
- Failure to hold OR on close.
- Rotation back through VWAP with momentum against position.

---

## Risk Management & Execution
- Vol-scaled sizing: Contracts = Risk$ / (Stop (σ) × σ₁(price) × tick_value).
- Default stops: 0.25–0.35σ for trend retests; 0.35–0.50σ for fades.
- Scale at objective levels (±1σ, VWAP, ±2σ); trail survivors (20-EMA or structure).
- News filter: Avoid initiating positions right before tier-1 releases (CPI, FOMC, NFP).

## What to Track
- Win rate, average R, payoff ratio, expectancy.
- σ-location at entry/exit; % of session outside ±1σ; ±2σ breaches.
- Context: catalyst vs no-catalyst; trend vs balanced; opening gap size.
- Slippage vs stop distance; partial timing; VWAP alignment impact.

## Implementation Notes
- Be consistent with underlying (ES vs SPX, NQ vs NDX).
- Recompute bands daily after vol index close; round to tick.
- Use a consistent intraday timeframe (e.g., 5m) for signals; use 1–3m only for timing.
- Backtest each setup separately; avoid rule creep when combining.
