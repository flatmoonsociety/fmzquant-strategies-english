
> Name

Dual-TEMA-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
The double TEMA cross trading strategy is a relatively common strategy for tracking price trends. This strategy uses the triple exponential moving average TEMA with two different parameters. When the fast line crosses the slow line from below, it generates a long signal, and when the fast line crosses the slow line from above, it closes the position. This strategy can effectively track price trends and obtain better returns when the trend is clear.
### Strategy Principles
This strategy uses TEMA (Triple Exponential Moving Average) as the main technical indicator. The calculation formula of TEMA is:
TEMA = (3*EMA1) - (3*EMA2) + EMA3

Among them, EMA1, EMA2 and EMA3 are exponential moving averages EMA of length N respectively. TEMA can respond to price changes more quickly by calculating EMA three times.
The strategy uses the shorter TEMA as the fast line and the longer TEMA as the slow line. When the fast line crosses the slow line, the price starts to rise, and a long signal is generated; when the fast line crosses the slow line, the price starts to fall, and the position is closed.
The key to this strategy is parameter setting and conditional judgment. The fast line sets a shorter period, such as 20 days, to capture price changes faster; the slow line sets a longer period, such as 60 days, to filter out false breakthroughs. When the price shows an obvious upward or downward trend, the fast line can quickly cross above or below the slow line to generate a trading signal.
### Advantage Analysis
This strategy has the following advantages:
1. Using the TEMA indicator can respond to price changes more quickly and capture trend reversals.
2. The double TEMA structure can filter out false breakthroughs and enter high-probability trend trading.
3. The adjustable parameter setting is flexible, and the parameters can be adjusted according to the market to adapt to different market conditions.
4. The strategy logic is simple and clear, easy to understand and implement, and the capital utilization rate is high.
5. Better returns can be obtained in trending markets, and the effect is better in markets with clear trends.
### Risk Analysis
This strategy also has the following risks:
1. Frequent trading losses are likely to occur during consolidation.
2. If the parameters are set improperly, too many false signals may be generated.
3. Unable to effectively respond to short-term market changes caused by emergencies.
4. There is a certain time lag and short-term opportunities may be missed.
5. Opening a position with the trend in a sharply volatile market is risky.
6. Parameters need to be adjusted in a timely manner to adapt to market changes, and certain parameter optimization experience is required.
Corresponding risk management measures:
1. Optimize parameter settings to avoid being too sensitive.
2. Combine with other indicators to filter entry signals.
3. Use exit stop loss to ensure single loss control.
4. Reduce the position size and control the risk of a single transaction.
5. Add parameter optimization judgment and manual intervention mechanism.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the parameters of fast and slow lines to better adapt to different varieties and market environments. A dynamic parameter optimization mechanism can be introduced.
2. Add other indicators in combination, such as MACD, Bollinger Bands, etc., to improve the effectiveness of signals.
3. Add stop loss strategies, such as trailing stop, time stop, ATR stop, etc., to control losses.
4. Combine with the VIX index to avoid opening positions in times of panic.
5. Introduce volume and energy indicators, and then consider opening a position when the large amount can be significantly amplified.
6. Optimize fund management strategies, such as fixed quota transactions, position management, etc.
7. Combine with machine learning to automatically optimize parameters.
### Summarize
The Double TEMA Cross Strategy is a strategy that uses trend index indicators for trend tracking. It is helpful to capture price trends and trade under clear trends. But you also need to pay attention to risk control to avoid losses caused by improper use. Through further optimization testing, the strategy Parameters settings can be made more scientific and reasonable, and better returns can be obtained in trending markets.
||


### Overview

The dual TEMA crossover trading strategy is a common trend-following strategy using two TEMA (Triple Exponential Moving Average) lines with different parameters. It generates long signals when the faster TEMA crosses above the slower TEMA, and closes positions when the faster TEMA crosses below the slower TEMA. This strategy can effectively track price trends and gain profits when the trend is clear.

### Strategy Logic

The strategy utilizes the TEMA (Triple Exponential Moving Average) as the main technical indicator. The TEMA is calculated as:

TEMA = (3*EMA1) - (3*EMA2) + EMA3

Where EMA1, EMA2 and EMA3 are EMAs of period N. By calculating EMAs three times, TEMA can respond faster to price changes.

The strategy uses a shorter-period TEMA as the fast line, and a longer-period TEMA as the slow line. When the fast line crosses above the slow line, indicating an upside price move, it generates long signals. When the fast line crosses below the slow line, indicating a downside price move, it closes positions. 

The keys of this strategy lie in parameter tuning and condition logics. The fast line with a shorter period like 20-day can quickly capture price dynamics, while the slow line with a longer period like 60-day can filter out false breakouts. When a significant price uptrend or downtrend emerges, the fast line can cross above or below the slow line swiftly to produce trading signals.

### Advantage Analysis

The advantages of this strategy include:

1. TEMA can respond faster to price changes and capture trend reversals.

2. The dual TEMA structure helps filter false breakouts and enter high-probability trend trades.

3. Flexible adjustable parameters to adapt to different market conditions.

4. Simple and clear logic, easy to understand and implement, high capital utilization.

5. Good profits can be gained in trending markets, especially strong-trending ones.

### Risk Analysis

The risks of this strategy include:

1. Prone to frequent trading losses in range-bound markets.

2. May generate excessive false signals if parameters are not tuned properly. 

3. Unable to respond effectively to sudden events and short-term price moves.

4. Lagging signals may miss short-term opportunities. 

5. High risks of opening positions against strong swings.

6. Requires experience in parameter optimization to adapt to changing markets.

Risk management measures:

1. Optimize parameters to avoid oversensitivity.

2. Add other indicators to filter entry signals.

3. Use stop losses to limit single trade loss.

4. Reduce position sizing to control risk.

5. Add parameter optimization rules and manual intervention mechanisms.

### Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize fast and slow line parameters for different products and market conditions. Introduce dynamic parameter optimization mechanisms.

2. Incorporate other indicators like MACD, Bollinger Bands to improve signal validity. 

3. Add stop loss strategies like trailing stop, time stop, ATR stop to control losses.

4. Avoid opening positions when VIX is high.

5. Add volume indicators, only consider entering on obvious volume expansion.

6. Optimize money management like fixed fractional position sizing, drawdown control.

7. Use machine learning to automatically optimize parameters.

### Summary

The dual TEMA crossover strategy is an overall trend-following strategy using trend technical indicators. It helps capture price trends and trade along the trends. But risks should be managed properly to avoid losses from improper use. Further optimizations and tests can lead to more scientific parameter tuning and better performance in trending markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2020|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|20|Fast Length|
|v_input_8|60|Slow Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-10-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © nickrober

//@version=4
strategy(title="TEMA Cross Backtest", shorttitle="TEMA_X_BT", overlay=true, commission_type=strategy.commission.percent, commission_value=0, initial_capital = 1000,  default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// Backtest inputs
FromMonth = input(defval=1, title="From Month", minval=1, maxval=12)
FromDay = input(defval=1, title="From Day", minval=1, maxval=31)
FromYear = input(defval=2020, title="From Year", minval=2010)
ToMonth = input(defval=1, title="To Month", minval=1, maxval=12)
ToDay = input(defval=1, title="To Day", minval=1, maxval=31)
ToYear = input(defval=9999, title="To Year", minval=2017)

// Define backtest timewindow
start = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish = timestamp(ToYear, ToMonth, ToDay, 23, 59)  // backtest finish window
window() =>  true

//TEMA Section
xLength = input(20, minval=1, title="Fast Length")
xPrice = close
xEMA1 = ema(xPrice, xLength)
xEMA2 = ema(xEMA1, xLength)
xEMA3 = ema(xEMA2, xLength)
xnRes = (3 * xEMA1) - (3 * xEMA2) + xEMA3
xnResP = plot(xnRes, color=color.green, linewidth=2, title="TEMA1")

yLength = input(60, minval=1, title="Slow Length")
yPrice = close
yEMA1 = ema(yPrice, yLength)
yEMA2 = ema(yEMA1, yLength)
yEMA3 = ema(yEMA2, yLength)
ynRes = (3 * yEMA1) - (3 * yEMA2) + yEMA3
ynResP = plot(ynRes, color=color.red, linewidth=2, title="TEMA2")

fill(xnResP, ynResP, color=xnRes > ynRes ? color.green : color.red, transp=75, editable=true)

// Buy and Sell Triggers
LongEntryAlert = xnRes > ynRes
LongCloseAlert = xnRes < ynRes
ShortEntryAlert = xnRes < ynRes
ShortCloseAlert = xnRes > ynRes

// Entry & Exit signals
strategy.entry("Long", strategy.long, when = xnRes > ynRes and window()) 
strategy.close("Long", when = xnRes < ynRes)
//strategy.entry("Short", strategy.short, when = xnRes < ynRes and window())
//strategy.close("Short", when = xnRes > ynRes)
```

> Detail

https://www.fmz.com/strategy/429085

> Last Modified

2023-10-12 17:34:19
