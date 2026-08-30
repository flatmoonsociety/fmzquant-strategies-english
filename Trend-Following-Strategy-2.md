
> Name

Based on trend following strategy Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1468aa7244f7540d194.png)
[trans]

## Overview
This strategy is based on the principle of trend following, using the Parabolic SAR indicator to determine the direction of the market trend, and combining it with the barcolor indicator to visually display the bull and bear status of the price. It goes long when the trend is upward and short when the trend is downward to capture the profits brought by the market trend.
## Strategy Principle
This strategy mainly uses the Parabolic SAR indicator to determine the direction of the market trend. Parabolic SAR, also known as the parabolic steering indicator, consists of two parameters, Step represents the moving step of the SAR point, and Max represents the maximum step of the SAR point. When the market is trending, the SAR point will follow the price and move upward or downward as the trend continues. When the trend reverses, the SAR point will cross the price and appear on the other side of the price. Therefore, by comparing the high and low relationship between the SAR point and the K line, the current trend direction can be judged.
Specifically, when the SAR point is below the lowest price of the K line, it means that it is currently in an upward trend, and the strategy will go long at this time; when the SAR point crosses the highest point of the K line, it means that the trend has reversed, and the strategy will close the long order; on the contrary, when the SAR point is above the highest price of the K line, it means that it is currently in a downward trend, and the strategy will go short at this time; when the SAR point crosses the lowest point of the K line, it means that the trend has reversed, and the strategy will close the short order.
In order to judge the current trend situation more intuitively, this strategy also uses the barcolor indicator to color the K line. When the closing price is higher than the SAR point, the K-line is displayed in green, representing an upward trend; when the closing price is lower than the SAR point, the K-line is displayed in red, representing a downward trend.
## Strategic advantage analysis
The biggest advantage of this strategy is that it can accurately capture market trends and follow the trends for trading, avoiding being disturbed by frequent market noise. The specific advantages are as follows:
1. Use Parabolic SAR indicator to determine the trend. The design of SAR points is very subtle and can quickly and accurately capture trend reversal.
2. The barcolor indicator is used to visually display the current bull and bear status, making it clear at a glance.
3. Trading signals come from the trend itself rather than other factors, and will not be misled by short-term price fluctuations.
4. Use trend tracking stop loss, stop loss in time without being too sensitive, and prevent being trapped.
5. Keeping the trading direction consistent and not doing reverse operations will help avoid unnecessary transactions.
6. The trading rules are simple and clear, easy to understand and implement, and suitable for novices to learn.
## Strategy risk analysis
The biggest risks of this strategy are:
1. Unable to determine the specific entry and exit timings, it is easy to miss opportunities in the early and late stages of the trend.
2. If you stop trading and hold a position during the consolidation market, you will not be able to make a profit or stop the loss, and there is a risk of being trapped.
3. There is no way to limit the profit and loss ratio of a single transaction, and a single loss may be too large.
4. Only do unilateral transactions, and can only capture one of the long market and short market.
5. Failure to consider large-scale trend judgments, and there is a risk of hedging against the general trend.
6.  parametric optimal solution is found.

In order to solve the above risks, optimization can be carried out from the following aspects:
1. Combine with other indicators to determine the specific timing of entry and exit.
2. Add trend revealing indicators to avoid opening positions during consolidation.
3. Set risk management rules to limit single losses.
4. Optimize the switching logic of long and short positions to capture more trading opportunities.
5. Add multi-time frame analysis to determine the direction of large-level trends.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the settings of Parabolic SAR parameters to better adapt to different varieties and cycles.
2. Use indicators such as moving averages to filter entry opportunities.
3. Add a breakout entry strategy and enter the market promptly after the trend starts.
4. Optimize the stop loss strategy to avoid the stop loss being too sensitive or too slow.
5. Add a stop-profit strategy and take the initiative to stop profits after the profit reaches a certain level.
6. Optimize the fund management strategy and improve the risk-adjusted return of the strategy.
7. Multi-time frame optimization to ensure that the large-level trend is consistent with the trading direction.
8. Introduce machine learning and other technologies to dynamically optimize parameters.
## Summarize
This strategy determines the trend direction through the Parabolic SAR indicator and follows the trend to trade immediately after it starts. The advantage of the strategy is that the trading signals come from the trend itself and are not easily disturbed by market noise. However, there are also problems such as being unable to limit the risk of a single transaction and missing the opportunity to enter. Future optimization directions include setting up take-profit and stop-loss strategies, optimizing parameter settings, adding filters, etc., so that the strategy can achieve better performance in backtesting and real trading.
||
## Overview

This strategy is based on the principle of trend following. It uses the Parabolic SAR indicator to determine the market trend direction and combines the barcolor indicator to visualize the bull/bear state of prices. It goes long when the trend goes up and goes short when the trend goes down, aiming to capture profits from market trends.

## Strategy Logic

The strategy mainly uses the Parabolic SAR indicator to judge the market trend direction. Parabolic SAR, also known as the parabolic stop and reverse indicator, consists of two parameters: Step, which represents the step of SAR point movement, and Max, which represents the max step allowed for SAR points. When the market is in a trend, SAR points will stick close to prices and move up or down continuously along with the trend. When the trend reverses, SAR points will cross prices and appear on the other side. Therefore, by comparing SAR points with high/low prices, the current trend direction can be determined. 

Specifically, when SAR points are below the lowest price, it indicates an uptrend, and the strategy will go long. When SAR points cross above the highest price, it signifies a trend reversal, and the strategy will close long positions. Conversely, when SAR points are above the highest price, it signals a downtrend, and the strategy will go short. When SAR points cross below the lowest price, it represents a reversal, and the strategy will close short positions.

To visually determine the current trend condition more intuitively, the strategy also uses the barcolor indicator to color the bars. Green bars represent an uptrend when the close is higher than SAR points, while red bars signify a downtrend when the close is lower.

## Advantage Analysis

The biggest advantage of this strategy is that it can accurately capture market trends and follow the trends to trade, avoiding interference from frequent market noises. The specific advantages are:

1. Using Parabolic SAR to determine trends, the design of SAR points is ingenious and can quickly and precisely capture trend reversals.

2. Adopting the barcolor indicator to visually display the current bull/bear state in an intuitive manner.

3. Trade signals come from the trend itself instead of other factors, avoiding being misguided by short-term price fluctuations.

4. Employing trend tracking stops loss, timely stopping out without being too sensitive, preventing being caught in traps.

5. Maintaining consistent trade direction, avoiding unnecessary reverse trades, being beneficial for simplicity. 

6. The trading rules are simple and clear, easy to understand and implement, suitable for beginners to learn.

## Risk Analysis

The biggest risks of this strategy are:

1. Unable to determine specific entry and exit points, likely to miss early and late trend opportunities.

2. Stop trading and hold positions during consolidation, unable to profit or stop loss, with the risk of being caught.

3. Unable to limit the risk/reward ratio of each trade, single trade loss could be too big. 

4. Only doing unilateral trades, only able to capture either uptrends or downtrends. 

5. Not considering the analysis of greater trend, carries the risk of trading against the major trend.

To address these risks, optimizations can be made in the following aspects:

1. Combine other indicators to determine specific entry and exit points.

2. Add trend discovering indicators to avoid opening positions during consolidation.

3. Set risk management rules to limit per trade loss. 

4. Optimize the long/short switching logic to capture more trading opportunities.

5. Add multi-timeframe analysis to determine the major trend direction.

## Optimization Directions

This strategy can be further optimized in the following aspects:

1. Optimize the Parabolic SAR parameters to better suit different products and timeframes.

2. Add filters like moving averages to filter entry points. 

3. Incorporate breakout strategies to get in a trend early after trend starts.

4. Optimize stop loss strategies to avoid being too sensitive or too insensitive.

5. Add profit taking strategies to actively take profit when reaching a certain level.

6. Enhance money management strategies to improve risk-adjusted returns.

7. Multi-timeframe optimizations to ensure major trend alignment with trade direction.

8. Introduce machine learning etc. to dynamically optimize parameters.

## Summary

This strategy determines the trend direction with the Parabolic SAR indicator and follows the trend immediately after it starts. The advantage is trade signals come from the trend itself, less susceptible to market noises. But it also has weaknesses like unable to limit per trade risks and missing entry points. Future optimizations include setting stop loss/take profit, parameter tuning, adding filters etc. to improve strategy performance in backtests and live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Trend Code|
|v_input_2|true|From Day|
|v_input_3|true|From Month|
|v_input_4|2019|From Year|
|v_input_5|true|To Day|
|v_input_6|true|To Month|
|v_input_7|2020|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-06 00:00:00
end: 2023-11-05 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Trend Trader Strategy (Trend Code)", shorttitle="Trend Trader Strategy (Trend Code)", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

//Inputs
TrendCode = input(5, title = "Trend Code")

////////////////////////////////////////////////////////////////////////////////
// BACKTESTING RANGE
 
// From Date Inputs
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2019, title = "From Year", minval = 1970)
 
// To Date Inputs
toDay = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2020, title = "To Year", minval = 1970)
 
// Calculate start/end date and time condition
startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true
 
////////////////////////////////////////////////////////////////////////////////

//Parabolic SAR
psar = sar(0.02, 0.02, TrendCode * 0.005)


//Plot PSAR
plot(psar, title="PSAR", color = color.teal , trackprice=true)

//Barcolor
barcolor(close > psar ? color.green : color.red, title = "Bar Color")

if (psar >= high and time_cond)
    strategy.entry("long", strategy.long, stop=psar, comment="long")
else
    strategy.cancel("long")

if (psar <= low and time_cond)
    strategy.entry("short", strategy.short, stop=psar, comment="short")
else
    strategy.cancel("short")
        
if (not time_cond)
    strategy.close_all()





 

```

> Detail

https://www.fmz.com/strategy/431219

> Last Modified

2023-11-06 10:09:02
