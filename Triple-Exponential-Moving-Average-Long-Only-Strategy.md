
> Name

Triple-Exponential-Moving-Average-Long-Only-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/956037267034eed70d.png)
[trans]


## Overview
The Triple Exponential Moving Average Long Only Strategy is a long-term strategy based on the Triple Exponential Moving Average as a trading signal. This strategy calculates three EMAs of different periods and overlays them into TEMA indicators to filter out short-term market noise and identify the medium and long-term trend direction. Go long when the price goes above TEMA, close the position when it goes below TEMA. This strategy is suitable for investors interested in mid- to long-term trend trading.
## Strategy Principle
This strategy identifies mid- to long-term trends through the TEMA technical indicator. The TEMA indicator is a trend indicator obtained by triple smoothing the EMA exponential moving average. The EMA indicator itself plays a certain filtering role on the price. By calculating three EMA exponential moving averages of different periods and performing superposition conversion, TEMA can further filter out short-term noise and highlight the trend of larger periods.
Specifically, this strategy first calculates the EMA indicator ema1 of the fastEmaPeriod period, then calculates ema2 of the same period based on ema1, and finally calculates ema3 based on ema2. The final TEMA indicator is calculated according to the formula: TEMA = 3 * (ema1 - ema2) + ema3. When the price goes above TEMA, go long; when the price goes below TEMA, close the position.
Through multiple exponential smoothing, the TEMA indicator can effectively identify the twists and turns of medium and long-term trend directions and filter out the interference of short-term noise on transactions, so it is very suitable as a long-term trading strategy for shorts.
## Strategic advantage analysis
- Using the TEMA indicator can effectively identify medium and long-term trends, filter out short-term noise interference, and avoid being trapped.
- Only long positions, not short positions, can avoid the unlimited loss risk caused by short positions.
- Using percentage position management, the position size can be flexibly adjusted according to account funds to control risks.
- The time window setting allows backtesting to specify a historical time period and optimize strategy parameters.
## Strategy risk analysis
- When holding long-term positions, rapid U-turns may result in large losses when encountering a major black swan event.
- When the TEMA indicator fails at the trend turning point, you may miss the opportunity to stop loss in time.
- Percentage positions cannot limit the size of a single loss, and stop loss is required to control risks.
- There is a risk of over-fitting in backtesting, and parameter optimization may not be suitable for future markets.
## Strategy optimization direction
- Optimize parameters combined with volatility indicators to improve the robustness of parameters.
- Add stop loss strategy to control single loss.
- Optimize position management and reduce positions during retracements.
- Added Tendency indicator across time periods to improve the accuracy of trend judgment.
- Test different holding period parameters and find the optimal holding period.
## Summarize
To sum up, this triple exponential moving average long-term strategy identifies the trend direction by calculating the TEMA indicator, adopts long-term positions to avoid being disturbed by short-term noise, only goes long and does not short-sell to avoid unlimited loss risks, and can effectively capture the medium and long-term trends for long-term positions. However, this strategy also has certain risks and requires appropriate optimization to improve robustness. Overall, this strategy is suitable for investors who have a certain risk tolerance and are inclined to trend trading.
||


## Overview

The Triple Exponential Moving Average Long Only Strategy is a long-term trend following strategy based on the Triple Exponential Moving Average (TEMA) indicator. It uses TEMA to filter out short-term market noise and identify mid-to-long-term trend directions. The strategy goes long when price crosses above TEMA and exits when price falls below TEMA. It is suitable for investors interested in mid-to-long term trend trading.

## Strategy Logic

The strategy identifies mid-to-long term trends using the TEMA indicator. TEMA is a smoothed trend indicator derived from triple exponential smoothing of the standard EMA. EMA itself has some noise filtering effect. TEMA further reduces short-term noise by smoothing three EMAs of different periods. 

Specifically, the strategy first calculates the EMA (ema1) of period fastEmaPeriod, then calculates another EMA (ema2) of ema1 using the same period, and finally calculates ema3 based on ema2. The final TEMA is calculated as: TEMA = 3 * (ema1 - ema2) + ema3. The strategy goes long when price crosses above TEMA and exits when price falls below TEMA.

Through multiple exponential smoothing, TEMA can effectively identify mid-to-long term trend directions despite zigzags and reversals, filtering out short-term noise. Thus it is well-suited for long-term trend following strategies.

## Advantage Analysis

- TEMA effectively identifies mid-to-long term trends and filters out short-term noise, avoiding whipsaws.

- Only long positions avoid unlimited downside risks of shorting. 

- Percentage position sizing flexibly sizes positions based on account size for risk control.

- Time window backtesting optimizes parameters on specific historical periods.

## Risk Analysis

- Severe black swan events may cause sharp reversals during long holding periods, leading to large losses.

- TEMA may fail to signal trend changes for timely stop loss. 

- Percentage sizing does not limit per trade loss size, requiring stops.

- Backtesting risks overfitting, optimized parameters may not fit future markets.

## Improvement Directions

- Add volatility metrics to robustify parameters.

- Implement stop loss to control single trade loss size.

- Optimize position sizing to lower size during drawdowns. 

- Add cross-timeframe Tendency indicators to improve trend accuracy.

- Test different holding period parameters for optimum.

## Conclusion

In summary, the Triple EMA Long Only Strategy identifies trend directions via the TEMA indicator, holds long-term positions to avoid short-term noise, stays only long to avoid unlimited downside, and effectively catches mid-to-long term trends. However, risks exist requiring optimizations to improve robustness. Overall it suits investors with some risk tolerance favoring trend trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|7|Fast TEMA Period|
|v_input_2|true|From Month|
|v_input_3|4|From Day|
|v_input_4|2010|From Year|
|v_input_5|true|To Month|
|v_input_6|true|To Day|
|v_input_7|9999|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-08 00:00:00
end: 2023-11-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("TEMA_System_long_only", overlay=true)

//Collect inputs parameters

fastEmaPeriod = input(7, minval=1, title="Fast TEMA Period")

// === INPUT BACKTEST RANGE ===
FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 4, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2010, title = "From Year", minval = 2000)
ToMonth   = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 2000)

// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => true // create function "within window of time"

fastEma = ema(close, fastEmaPeriod)

//convert EMA into TEMA

ema1 = ema(close, fastEmaPeriod)
ema2 = ema(ema1, fastEmaPeriod)
ema3 = ema(ema2, fastEmaPeriod)

fastTEMA = 3 * (ema1 - ema2) + ema3


buy  = close > fastTEMA
sell = close < fastTEMA

plot(fastTEMA, title = 'TEMA', linewidth=3, color=white)

if window()
    strategy.entry("long",strategy.long, when = buy)
    strategy.close("long", when = sell )
```

> Detail

https://www.fmz.com/strategy/432179

> Last Modified

2023-11-15 10:54:39
