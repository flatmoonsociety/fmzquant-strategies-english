
> Name

Trend following strategy based on RSI RSI-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4cc54d1af22a44cd0a644c2866a77bc303750b28bad4c2183e5bf9c7d07173bb.png)
[trans]


## Overview
This strategy is designed based on the Relative Strength Index (RSI) indicator. It uses the RSI indicator to determine overbought and oversold conditions and achieve trend tracking. Go long when the RSI is below the oversold line, go short when the RSI is above the overbought line, and make profits by tracking the main trend of the market.
## Strategy Principle
This strategy uses the RSI indicator to determine whether the market is overbought or oversold. The RSI indicator is calculated based on the rise and fall within a certain time period. When the RSI is below 30, it is considered oversold, and when the RSI is above 70, it is considered overbought.
Specifically, this strategy first defines the RSI calculation parameters length=14, the overbought line overBought=70, and the oversold line overSold=30. Then calculate the RSI value vrsi based on the close price. Determine whether vrsi is above the overbought line or below the oversold line. If a golden cross occurs, go long. If a death cross occurs, go short. After going long or short, set the stop loss point to etoroStopTicks ticks, and close the position after the stop loss is triggered within the window period.
In this way, this strategy can capture the main trend of the market, buy at the oversold point, sell at the overbought point, and achieve trend tracking.
## Strategic Advantages
- Use the RSI indicator to determine overbought and oversold conditions, which is helpful for capturing market trends.
- The backtest window setting is flexible and different time ranges can be selected for testing.
- The stop loss point is set reasonably to control the loss of a single transaction
## Strategy Risk
- RSI has a crotch pulling phenomenon and may produce false signals
- The stop loss point is static and cannot dynamically track market fluctuations.
- Unable to determine the trend reversal point and may open a position in the opposite direction
Risk resolution:
- Combine with other indicators to filter RSI signals to avoid wrong opening of positions
- Dynamically adjust stop loss points and track market fluctuations in real time
- Add trend judgment indicators to avoid opening reverse positions
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimize RSI parameters and find the optimal parameter combination
You can test different RSI calculation period lengths, different overbought and oversold thresholds, and find optimal parameters to reduce false signals.
2. Add trend judgment indicators to avoid counter-trend trading
Indicators such as moving averages and MACD can be added to determine the trend direction to avoid generating false signals at trend reversal points.
3. Dynamic stop loss
Dynamic stop loss points can be set based on indicators such as ATR to make the stop loss closer to market fluctuations.
4. Optimize entry rules
Other conditions can be added based on the RSI signal, such as breaking through a certain price level, amplifying trading volume, etc. as entry signals to improve entry accuracy.
## Summarize
This strategy uses the RSI indicator to determine overbought and oversold conditions and capture trends. Compared with the traditional trailing stop loss strategy, it has the advantage of using indicators to judge market timing. However, the RSI indicator has a pull-back phenomenon and cannot determine the trend reversal point. This is the direction in which this strategy needs to be optimized. Through parameter optimization, increasing trend judgment, dynamic stop loss and other means, the stability and profitability of the strategy can be further improved.
||


## Overview

This strategy is designed based on the Relative Strength Index (RSI) indicator to identify overbought and oversold situations and follow the trend. It goes long when RSI is below the oversold line and goes short when RSI is above the overbought line, aiming to profit by following the main trend of the market.

## Strategy Logic

This strategy uses the RSI indicator to identify overbought and oversold conditions in the market. RSI is calculated based on the price changes over a certain period of time. An RSI below 30 is considered oversold while an RSI above 70 is considered overbought. 

Specifically, this strategy first defines the RSI parameters length=14, overbought=70, oversold=30. It then calculates the RSI value vrsi based on the close price. When vrsi crosses above the overbought line or below the oversold line, it triggers a long or short trade accordingly. After entering the trade, a stop loss of etoroStopTicks ticks is set. The positions will be closed when stop loss is triggered within the trading window.

In this way, the strategy is able to follow the major trend of the market - going long at oversold situations and going short at overbought situations.

## Advantages

- Utilize RSI to identify overbought/oversold market conditions for catching the trend
- Flexible backtesting window for testing different time periods
- Reasonable stop loss setting for controlling single trade loss

## Risks

- RSI divergence may generate false signals
- Static stop loss fails to adapt to market fluctuation
- Hard to identify trend reversal, may lead to reverse trades

Solutions:

- Add filter indicators to avoid wrong entries based on false RSI signal
- Dynamic stop loss to track market movement in real time
- Add trend judging tools to prevent reverse trades

## Improvement

The strategy can be optimized in the following aspects:

1. Optimize RSI parameters for best performance

Test different RSI periods and overbought/oversold levels to find optimum parameters and reduce false signals.

2. Add trend judging tools to avoid counter trend trades 

Add MA, MACD to judge trend direction and avoid wrong signals at turning points.

3. Dynamic stop loss

Use ATR to set adaptive stop loss for better tracking market fluctuation. 

4. Improve entry rules

Add other conditions like breakout, volume increase to RSI signal to improve entry accuracy.

## Conclusion

The strategy catches the trend by identifying overbought and oversold situations using RSI. Compared to traditional tracking stop strategies, it has the advantage of timing the market with indicators. However, problems like RSI divergence and inability to detect trend reversal need to be addressed. Further improvements on parameter optimization, trend judging, dynamic stop loss can enhance the stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|From Month|
|v_input_2|true|From Day|
|v_input_3|2018|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|14|length|
|v_input_8|30|overSold|
|v_input_9|70|overBought|
|v_input_10|120|etoroStopTicks|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-01 00:00:00
end: 2023-10-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy("RSI Etoro Strategy", overlay=true, max_bars_back=2000)
// To use:
// Capital = capital * leverage
// Slippage Ticks: 3, 5 ? (Mainly for spread)
// etoroStopTicks: Set it accordingly to the stock (to corresponds to etoro default of 50 % for exemple...)

// === INPUT BACKTEST RANGE ===
FromMonth = input(defval = 12, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2018, title = "From Year", minval = 1995)
ToMonth   = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 1995)


// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => time >= start and time <= finish ? true : false // create function "within window of time"

length = input( 14 )
overSold = input( 30 )
overBought = input( 70 )
etoroStopTicks = input( 120 )
// 120 because it is approximatively the number of ticks for default SL of 50% at x5 leverage for copper (no fee)...
price = close

vrsi = rsi(price, length)

if (not na(vrsi))
    if (crossover(vrsi, overSold))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE", when = window())
    if (crossunder(vrsi, overBought))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE", when = window())
strategy.exit("exit SE", "RsiSE", loss=etoroStopTicks, when = window())
strategy.exit("exit LE", "RsiLE", loss=etoroStopTicks, when = window())

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/431411

> Last Modified

2023-11-07 16:33:43
