
> Name

Moving stop-loss buying and selling strategy based on RSI indicatorRSI-Indicator-Based-Moving-Stop-Loss-Buy-Sell-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/98590f2086e5b76617.png)
 [trans]
## Overview
This strategy realizes automated buying and selling by setting the buy signal line and sell signal line of the RSI indicator and combining it with the trailing stop loss. A buy signal is issued when the RSI indicator is below the buy signal line; a sell signal is issued when the RSI indicator is above the sell signal line. At the same time, a trailing stop is set to lock in profits and control risks.
## Strategy Principle
This strategy mainly determines the timing of buying and selling based on the overbought and oversold areas of the RSI indicator. When the RSI indicator is below 20, it is considered oversold, and when it is above 80, it is considered overbought. The strategy sets three RSI low buy lines, which are 20, 18, and 14 respectively. When the closing price of the day is higher than the previous day and the RSI indicator is lower than the corresponding buy line, a buy signal is issued. The strategy sets an RSI high sell line of 83, and sends a sell signal when the RSI indicator is above the sell line. In addition, the strategy also sets a trailing stop loss, which will stop the sale if the price is lower than 5% of the purchase price.
The entire strategy uses the overbought and oversold areas of the RSI indicator to determine the timing of buying and selling, and sets stop losses to lock in profits and control risks. It is a typical quantitative trading strategy based on technical indicators.
## Advantage Analysis
This strategy has the following advantages:
1. The classic and widely proven RSI indicator is used to determine buying and selling points, which can effectively capture overbought and oversold opportunities.
2. Set multiple buying lines to buy in batches at different levels of low prices to reduce buying costs.
3. A trailing stop is configured to control losses and lock in profits, which can effectively control risks.
4. The strategy logic is simple and clear, easy to understand and modify, and easy to verify on the real market.
5. RSI indicator parameters can be customized, and parameters can be adjusted for different varieties and markets.
## Risk Analysis
There are also some risks with this strategy:
1. A single indicator strategy is easy to produce false signals, and the signal sent by the RSI indicator may not be accurate.
2. There is no stop-profit strategy, and there is a risk of loss expansion.
3. There is a risk of collapse in the overbought and oversold range, especially in volatile markets.
4. In extreme market conditions, the price may directly fall below the stop loss line, making it impossible to stop the loss.
Corresponding solutions:
1. Make judgments based on multiple indicators to avoid false signals.
2. Add take-profit strategies such as zones or sar.
3. Adjust RSI parameters to narrow the range.
4. Dynamic stop loss or timely manual intervention.
## Optimization direction
This strategy can be optimized from the following directions:
1. Combine with other indicators to form an indicator combination to avoid false signals. Common combinations include: RSI + KDJ, RSI + MACD, etc.
2. Add take-profit strategies, such as trend following take-profit, timed take-profit, moving take-profit channel, etc.
3. Parameter optimization, adjusting RSI parameters for different varieties and cycles.
4. Strategy derivation, such as the head-turning strategy, batch entry strategy and other strategy combinations.
5. Appropriately narrow the trading range to avoid false signals of overbought and oversold.
## Summarize
The strategy as a whole is a typical quantitative trading strategy based on the RSI indicator by setting buy and sell signals. The strategy is simple to understand and easy to implement. However, there are shortcomings such as the unreliability of a single indicator signal and the greater risk of a no-take-profit strategy. We can further improve this strategy through parameter optimization, strategy combination, and adding take-profit strategies.
||

## Overview

This strategy sets the buy signal line and sell signal line based on the RSI indicator, combined with moving stop loss to achieve automated buying and selling. It sends a buy signal when the RSI indicator is lower than the buy signal line, and a sell signal when the RSI indicator is higher than the sell signal line. At the same time, it sets a moving stop loss to lock in profits and control risks.

## Strategy Principle 

This strategy is mainly based on the overbought and oversold zones of the RSI indicator to determine entry and exit timing. RSI below 20 is considered oversold, and above 80 is considered overbought. The strategy sets three RSI low buy signal lines at 20, 18, and 14. When the closing price is higher than the previous day and the RSI indicator is below the corresponding buy line, a buy signal is issued. The strategy sets an RSI high sell signal line at 83. When the RSI indicator is higher than this sell line, a sell signal is issued. In addition, the strategy also sets a moving stop loss. If the price falls below 5% of the buy price, it will stop loss sell.

The whole strategy judges the timing of buying and selling through the overbought and oversold zones of the RSI indicator, and sets a stop loss to lock in profits and control risks. It is a typical quantitative trading strategy based on technical indicators.

## Advantage Analysis

The advantages of this strategy include:

1. Use the classic and widely verified RSI indicator to determine trading points and effectively capture overbought and oversold opportunities.

2. Setting multiple buy lines allows split buying at different low prices, reducing the cost of buying.  

3. Configuring a moving stop loss to control losses and lock in profits can effectively manage risks.

4. The strategy logic is simple and clear, easy to understand and modify, and easy to verify in live trading.

5. RSI indicator parameters can be customized and adjusted for different products and markets.

## Risk Analysis

There are also some risks to this strategy:

1. Relying on a single indicator, it is prone to false signals and the RSI indicator signals may not be accurate.  

2. There is no profit taking strategy, risks of letting losses expand.

3. There are risks of the overbought and oversold zone breakdowns, especially in range-bound markets.  

4. In extreme market conditions, prices may break through the stop loss line directly and fail to stop loss.

The solutions are:

1. Use multiple indicators combined to avoid false signals.  

2. Add profit taking strategies like zones or sar.

3. Adjust RSI parameters to narrow the overbought/oversold zones.  

4. Use dynamic stop loss or manual intervention when necessary.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Combine other indicators to form an indicator portfolio to avoid false signals, such as RSI + KDJ, RSI + MACD.

2. Add profit taking strategies like trailing stop loss, time-based exit, moving exit channel. 

3. Parameter optimization, adjust RSI parameters based on different products and timeframes.  

4. Strategy derivatives such as reversal strategies, scaling in strategies.

5. Narrow the buy/sell zones appropriately to avoid false signals.

## Conclusion

In summary, this is a typical quantitative trading strategy based on RSI indicator by setting buy/sell signals. The strategy is simple and easy to implement, but relies on a single indicator with high risks of no profit taking. We can further improve it through parameter tuning, strategy combo, adding profit taking mechanisms etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|RSI Period|
|v_input_2|83|RSI Sell Level|
|v_input_3|5|Stop Percentage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-17 00:00:00
end: 2024-01-16 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("RSI Buy/Sell Strategy", overlay=false)

// Input for RSI period
rsiPeriod = input(12, title="RSI Period")

// Input for RSI levels
rsiBuyLevel1 = 20
rsiBuyLevel2 = 18
rsiBuyLevel3 = 14
rsiSellLevel = input(83, title="RSI Sell Level")

// Input for stop loss percentage
stopLossPercent = input(5, title="Stop Percentage")

// Calculate RSI
rsiValue = ta.rsi(close, rsiPeriod)

// Buy Conditions: RSI below buy levels
buyCondition1 = close[1] > close and rsiValue <= rsiBuyLevel1
buyCondition2 = close[1] > close and rsiValue <= rsiBuyLevel2
buyCondition3 = close[1] > close and rsiValue <= rsiBuyLevel3

// Sell Conditions: RSI above sell level or stop loss
sellCondition = (rsiValue > rsiSellLevel )//or ( close[1] < close * (1 - stopLossPercent / 100))

// Calculate position size based on 10% of current equity
positionSize = strategy.equity * 0.8 / close

// Plot RSI on the chart
plot(rsiValue, title="RSI", color=color.blue)

// Plot horizontal lines for buy and sell levels
hline(rsiBuyLevel1, "Buy Level 1", color=color.green)
hline(rsiBuyLevel2, "Buy Level 2", color=color.green)
hline(rsiBuyLevel3, "Buy Level 3", color=color.green)
hline(rsiSellLevel, "Sell Level", color=color.red)

// Execute Buy and Sell orders with stop loss
strategy.entry("Buy1", strategy.long, when = buyCondition1, qty = positionSize,stop=close * stopLossPercent / 100)
strategy.entry("Buy2", strategy.long, when = buyCondition2, qty = positionSize,stop=close * stopLossPercent / 100)
strategy.entry("Buy3", strategy.long, when = buyCondition3, qty = positionSize,stop=close * stopLossPercent / 100)

strategy.close("Buy1", when = sellCondition)
strategy.close("Buy2", when = sellCondition)
strategy.close("Buy3", when = sellCondition)

```

> Detail

https://www.fmz.com/strategy/439063

> Last Modified

2024-01-17 13:54:43
