
> Name

Relative-Body-Index-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3f86a92cf7f83ac44d3c016a707833ab0d0cbc70ce458a72d5a93a47e0003cd3.png)

[trans]


## Overview
This strategy mainly uses the moving average crossover signal of the daily relative pen body ratio (RB) to determine the trend, and cooperates with stop loss and take profit for automatic trading. The "relative pen increase" in the strategy name refers to the moving average that calculates the relative pen increase of the daily line.
## Strategy Principle
The strategy is based on Vitelot's RBI indicator, which calculates the moving average of the Relative Pen Ratio (RB) of the daily candlestick. The calculation method of RB is:
In the formula, RB is equal to the ratio of the physical length of the sub-yang line to the length of the entire K line, taking a positive value; the RB of the negative line takes a negative value. The value range of RB is between -1 and 1.
The RBI indicator uses the moving average of RB to filter noise and capture the essential characteristics of the market. A buy signal is generated when the RBI indicator crosses above its signal line; a sell signal is generated when the RBI indicator crosses below its signal line.
In order to filter out false signals in the long uncertainty stage, when the RBI indicator crosses the signal line, this strategy will also determine whether the closing price is higher than the 13-period EMA. If it is higher, a real buy signal will be generated to execute the long strategy. Similarly, the short strategy will only be executed if the closing price is below the 13-period EMA.
The strategy also sets up stop-loss and take-profit mechanisms to control risks and lock in profits. After opening a position, the trail will track the set take-profit points and set a fixed stop-loss point.
## Advantage Analysis
- The RBI indicator filters out a lot of noise and can capture market trend characteristics to avoid being misled by false signals that shock the market.
- Combined with moving average filtering, it can effectively avoid false signals during long periods of uncertainty and reduce short losses.
- Stop-loss and take-profit settings help reduce the risk of loss for individual positions, while locking in profits and improving overall profitability.
- This strategy has fewer parameters, is easy to understand, and is suitable for automatic trading.
## Risk Analysis
- This strategy is based only on the RBI indicator, if the indicator itself produces false signals, the overall strategy will also fail.
- Improper setting of indicator parameters may also lead to a decrease in the quality of trading signals.
- Any technical indicator may fail under specific market conditions, and losses cannot be completely avoided.
- Setting a stop loss point that is too small may lead to too frequent stops; a stop loss point that is too large may increase a single loss.
- Insufficient drawdown control may lead to the risk of account liquidation.
## Optimization direction
- You can test different parameter combinations and optimize the parameters of the RBI indicator.
- Other auxiliary indicators can be added for filtering to improve signal quality.
- The parameters of stop loss and take profit can be optimized through machine learning training.
- You can add fund management strategies to control overall positions and risk exposure.
- You can try strategies with different holding times, such as overnight holding or short-term trading.
## Summarize
Overall, this strategy is a relatively simple and straightforward trend following strategy. It determines the trend direction by calculating the moving average crossover of the daily line relative to the pen body ratio, and at the same time adds moving average filtering and stop loss and take profit to control risks, which can effectively avoid false signals that shock the market. However, no technical indicator strategy can completely avoid risks. It is still necessary to pay attention to continuous improvement and optimization in parameter optimization, risk control, etc., in order to obtain long-term stable excess return. Overall, the strategy has clear logic, is easy to understand, is suitable for automatic trading, and is a very practical trend following strategy.

||

## Overview

This strategy mainly uses the moving average crossover signals of the relative body ratio (RB) of daily candlesticks to determine the trend, together with stop loss and take profit for automated trading. The "Relative Body Strength" in the strategy name refers to the moving average of the relative body strength of daily candlesticks.

## Strategy Logic  

The strategy is based on Vitelot's RBI indicator, which calculates the moving average of the relative body ratio (RB) of daily candlesticks. The RB is calculated as:

The formula calculates the ratio of the real body to the full length of the candlestick for bullish candles, taking positive values; and negative values for bearish candles. RB ranges from -1 to 1.

The RBI indicator uses the moving average of RB to filter out noise and capture the essence of market trends. A buy signal is generated when RBI crosses above its signal line, and a sell signal when crossing below.

To avoid false signals during uncertain bullish phases, the strategy also checks if the closing price is above the 13-period EMA before generating a true buy signal for long position. Similarly, only when the close is below the 13 EMA will the short position be executed.

The strategy also implements stop loss and take profit to control risks and lock in profits. After opening position, profit will be trailed based on the set points, with a fixed stop loss in points.

## Advantage Analysis

- RBI filters out significant noise and captures market trend characteristics, avoiding false signals from ranging markets.

- Using moving average filter avoids false signals effectively during uncertain bullish phases, reducing losses from shorts.

- Stop loss and take profit helps reduce loss risk on individual positions and lock in profits, improving overall profitability. 

- The strategy has few parameters and is easy to understand, suitable for automated trading.

## Risk Analysis

- The strategy relies solely on RBI, any wrong signals from the indicator could lead to failure.

- Poor parameter tuning of the indicator could also worsen the quality of trading signals.

- No technical indicators can completely avoid losses in certain market conditions.

- Stop loss set too tight may result in too frequent stop outs; too wide may lead to large losses on single positions.

- Insufficient drawdown control could lead to account wipeout risks.

## Optimization Directions

- Different parameter combinations can be tested to optimize the RBI parameters.

- Additional indicators could be added for signal filtering and quality improvements.

- Machine learning can be used to train and optimize the stop loss and take profit parameters.

- Risk management strategies can be added to control overall position sizing and risk exposure.

- Different holding periods like overnight holdings or short term scalping could be explored.

## Conclusion

Overall this is a relatively simple and straightforward trend following strategy. It uses RBI crossover to determine trend direction, with additional filters and stop loss/take profit to control risks, effectively avoiding false signals from ranging markets. But no technical indicators can completely avoid risks. Continuous improvements such as parameter optimization, risk management are still needed for long term stable excess returns. The logic is clear and easy to understand, suitable for automated trading. It is a very practical trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|MA1 Period|
|v_input_2|5|Signal Period|
|v_input_3|0.2|Exclusion level|
|v_input_4|false|Calculate the binary version|
|v_input_5|false|Treshold Long|
|v_input_6|false|Treshold Short|
|v_input_7|300|SL Activation|
|v_input_8|true|SL Trigger|
|v_input_9|120|TP Activation|
|v_input_10|true|TP Trigger|
|v_input_11|true|From Month|
|v_input_12|true|From Day|
|v_input_13|2019|From Year|
|v_input_14|6|To Month|
|v_input_15|19|To Day|
|v_input_16|2020|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-11 00:00:00
end: 2023-10-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("RBI Backtest /w TSSL", shorttitle="RBI Strategy", overlay=false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, initial_capital = 10000, slippage = 5)
// RBI:
//  The EMA of the relative body (RB) of Japanese candles is evaluated.
//  The RB of a candle (my definition) is simply the ratio of the body with respect to its full length
//  and taken positive for bull candles and negative for bear candles:
//      e.g. a bull "marubozo" has RB=1 a bear "marubozo" has RB=-1;
//      a "doji" has RB=0.
//  This simple indicator grasps the essence of the market by filtering out a great deal of noise.
//
//  A flag can be selected to calculate its very basic binary version, where a bull candle counts as a one
//  and a bear candle counts as a minus one.
//
//  Enter (or exit) the market when the signal line crosses the base line.
//  When the market is choppy we have a kind of alternating bear and bull candles so that
//  RBI is FLAT and usually close to zero. 
//  Therefore avoid entering the market when RBI is FLAT and INSIDE the Exclusion level.
//  The exclusion level is to be set by hand: go back in history and check when market was choppy; a good
//  way to set it is to frame the oscillations of RBI whe price was choppy.
//
//  RBI is more effective when an EMA of price is used as filtering. I found EMA(13) to be
//  a decent filter: go long when base crosses signal upwards AND closing price is above EMA(13);
//  same concept for going short.
//
//  As any other indicator, use it with responsibility: THERE CAN'T BE A SINGLE MAGIC INDICATOR winning
//  all trades.
//
//  Above all, have fun.
//
// Vitelot/Yanez/Vts March 31, 2019

par1 = input(5, title="MA1 Period")
par2 = input(5, title="Signal Period")
exclusion = input(0.2, title="Exclusion level")

useBin = input(false, title="Calculate the binary version")

treshold_long = input(0, title="Treshold Long")
treshold_short = input(0, title="Treshold Short")

fixedSL = input(title="SL Activation", defval=300)
trailSL = input(title="SL Trigger", defval=1)
fixedTP = input(title="TP Activation", defval=120)
trailTP = input(title="TP Trigger", defval=1)

FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2019, title = "From Year", minval = 2017)
ToMonth   = input(defval = 6, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 19, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 2020, title = "To Year", minval = 2017)
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
startTimeOk()  => true // create function "within window of time" if statement true

ynSimple(t) =>
    s = (close>open)? 1: -1
    ema(sum(s,t),t)

ynRel(t) =>
    s = (close-open)/(high-low)
    ema(sum(s,t),t)

yn = useBin? ynSimple(par1): ynRel(par1) 
sig = ema(yn,par2)


plot(yn, color=aqua, title="RBI", linewidth=3, transp=0)
plot(sig, color=orange, title="Signal", linewidth=2, transp=0)

hline(0, color=white, title="Zero level", editable=false)
hline(exclusion, color=yellow, title="Exclusion level +", editable=true, linestyle=line)
hline( 0-exclusion, color=yellow, title="Exclusion level -", editable=true, linestyle=line)

long = crossover(yn,sig) and yn < treshold_long
short = crossover(sig,yn)  and yn > treshold_short

// === STRATEGY - LONG POSITION EXECUTION ===
strategy.entry("Long", strategy.long, when= long and startTimeOk())
strategy.exit("Exit", qty_percent = 100, loss=fixedSL, trail_offset=trailTP, trail_points=fixedTP) 
strategy.exit("Exit", when= short)
// === STRATEGY - SHORT POSITION EXECUTION ===
strategy.entry("Short", strategy.short, when= short and startTimeOk())
strategy.exit("Exit", qty_percent = 100, loss=fixedSL, trail_offset=trailTP, trail_points=fixedTP)
strategy.exit("Exit", when= long)

```

> Detail

https://www.fmz.com/strategy/429564

> Last Modified

2023-10-18 11:16:53
