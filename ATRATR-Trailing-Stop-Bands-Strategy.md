
> Name

Adaptive trailing stop loss strategy based on ATR indicator ATR-Trailing-Stop-Bands-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13597c3de6e3f62e876.png)

[trans]

## Overview
The core idea of ​​this strategy is to use the average true range (ATR) indicator to set an adaptive trailing stop loss line, so that profitable positions can be protected to the greatest extent while avoiding premature stop loss. The ATR indicator can dynamically capture the degree of market volatility, adjust the stop loss distance according to market fluctuations, and minimize the probability of the stop loss being triggered while ensuring the stop loss. This strategy also adds Bollinger Bands to visualize the upper and lower limits of the stop loss line, and you can choose whether to add shadow line protection to resist the impact of a volatile market.
## Strategy Principle
This strategy uses the N-period average of the ATR indicator multiplied by a multiple as the basic stop loss distance. The larger the ATR value, the greater the market volatility, and the wider the stop loss distance is set; the smaller the ATR value, the narrower the stop loss distance is set. This allows the stop loss distance to be dynamically adjusted based on market volatility.
Specifically, the strategy uses the following core logic:
1. Calculate the ATR value of ATR period (nATRPeriod).
2. Get the basic stop loss distance nLoss based on the ATR value multiplied by the multiple (nATRMultip).
3. Update the stop loss line xATRTrailingStop based on the current high, low and previous period's stop loss line.
4. If the current low point triggers the stop loss line of the previous period, the stop loss line moves to nLoss below the low point.
5. If the current high point triggers the stop loss line of the previous period, the stop loss line moves downward to nLoss distance above the high point.
6. If the stop loss is not triggered, the stop loss line will be adjusted based on the distance between the closing price and the stop loss line.
7. Add optional shadow line protection distance to further optimize the stop loss line.
8. Draw a Bollinger Bands track to visualize the upper and lower limits of the stop loss line.
9. Determine the position direction based on the color of the stop loss line.
This strategy flexibly uses the ATR indicator to allow the stop loss line to be adaptively adjusted according to market fluctuations, which can not only ensure that the stop loss distance is reasonable, but also try to avoid unnecessary position losses caused by overly aggressive stop losses.
## Advantage Analysis
This strategy has the following advantages:
1. Use the ATR indicator to dynamically adjust the stop loss distance and adapt to different market conditions.
2. The multiple parameters can be customized to realize flexible adjustment of the stop loss distance.
3. Add the Bollinger Bands track to form the visual upper and lower limits of the stop loss line.
4. Optional shadow line protection function to avoid whipsaw that may shock the market.
5. Can be used as a trailing stop to maximize the retracement of profitable positions.
6. The strategy idea is clear and easy to understand, and the parameters are few and easy to optimize.
7. Can be used in a variety of varieties and cycles, with a wide range of applications.
## Risk Analysis
There are also some risks that need to be noted in this strategy:
1. The ATR indicator lags in responding to market emergencies, which may cause the stop loss distance to be too large.
2. Setting the multiple too large will also lead to the stop loss distance being too wide, increasing the risk of loss.
3. The shadow line protection function will make the stop loss line too loose when the shock increases.
4. Entry rules are not considered and cannot be used as an Entries/Exits strategy.
5. It is necessary to repeatedly test and optimize parameters to adapt to different varieties and cycles.
6. Breaking through the stop loss may lead to an expansion of losses and requires effective fund management.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test different ATR cycle parameters and optimize the stop loss distance.
2. Adjust the multiple parameter to find a balance between stop loss distance and stop loss probability.
3. Optimize the shadow line protection cycle parameters to prevent whipsaw.
4. Try adding entry conditions on top of stop loss to make it an Entries/Exits strategy.
5. Add trend judgment indicators and adjust the stop loss distance according to the trend.
6. Combined with the wave theory, adjust the stop loss distance according to the wave position.
7. Add position control to limit single losses.
## Summarize
This strategy uses the adaptive characteristics of the ATR indicator to design a stop-loss mechanism that can be dynamically adjusted. While ensuring stop loss, we also try to reduce unnecessary stop loss triggers as much as possible. The strategic ideas are simple and clear, and can be flexibly optimized according to your own needs. It is more effective when used as a trailing stop loss tool, which can protect position profits to the maximum extent. With parameter optimization and risk control in place, this strategy can become an effective stop-loss tool in quantitative trading.
||


## Overview

The core idea of this strategy is to use the Average True Range (ATR) indicator to set an adaptive trailing stop loss line to maximize the protection of profitable positions while avoiding premature stop loss. The ATR indicator can dynamically capture the volatility of the market and adjust the stop loss distance based on market volatility, ensuring effective stop loss while minimizing the probability of stop loss being triggered. This strategy also incorporates Bollinger Bands for visualizing the upper and lower limits of the stop loss line, with the option of adding wick protection to counter the whipsaw effect in ranging markets.

## Strategy Logic

This strategy uses the N period average of ATR indicator multiplied by a factor as the base stop loss distance. The larger the ATR value, the larger the market volatility, so the wider the stop loss distance is set. The smaller the ATR value, the narrower the stop loss distance is set. This allows dynamic adjustment of stop loss distance based on market volatility.

Specifically, the strategy uses the following core logic:

1. Calculate the ATR value of the ATR period (nATRPeriod). 

2. Obtain the base stop loss distance nLoss by multiplying the ATR value by a factor (nATRMultip).

3. Update the stop loss line xATRTrailingStop based on current high, low and stop loss line of previous period.

4. If current low triggers previous period's stop loss line, the stop loss line moves up to below the low by nLoss distance.

5. If current high triggers previous period's stop loss line, the stop loss line moves down to above the high by nLoss distance.

6. If stop loss is not triggered, adjust the stop loss line based on the distance of close price to it. 

7. Add optional wick protection distance for further optimization of stop loss line.

8. Plot Bollinger Bands to visualize upper and lower limit of stop loss line.

9. Determine position direction based on color of stop loss line.

The strategy flexibly uses ATR indicator to enable the stop loss line to adjust adaptively based on market volatility, ensuring reasonable stop loss distance while avoiding excessive stop loss that causes unnecessary loss of positions.

## Advantages

The advantages of this strategy:

1. Use ATR indicator to adjust stop loss distance dynamically adapting to different market conditions.

2. Customizable multiplier allows flexible adjustment of stop loss distance. 

3. Addition of Bollinger Bands provides visualization of upper and lower limits of stop loss line.

4. Optional wick protection avoids whipsaw in ranging markets.

5. Can be used as trailing stop loss to maximize drawdown of profitable positions.

6. Strategy logic is clear and easy to understand with few optimizable parameters. 

7. Applicable to multiple products and timeframes.

## Risks 

Some risks of this strategy to note:

1. ATR indicator reacts slowly to market shocks, leading to large stop loss distance.

2. Excessive multiplier setting also enlarges stop loss distance, increasing loss risk.

3. Wick protection can make stop loss line too loose when whipsaw increases.

4. Entry rules not considered, cannot be used as Entries/Exits strategy.

5. Extensive testing and optimization of parameters needed for different products and timeframes.

6. Stop loss breakout may enlarge losses, requiring effective capital management.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Test different ATR periods to optimize stop loss distance.

2. Adjust multiplier to balance between stop loss distance and probability.

3. Optimize wick protection period to prevent whipsaw. 

4. Try adding entry conditions on top of stop loss to make it Entries/Exits strategy.

5. Add trend indicator to adjust stop loss distance based on trend.

6. Adjust stop loss based on Elliott Waves theory.

7. Add position sizing to limit single loss amount.

## Summary

This strategy utilizes the adaptive characteristic of ATR indicator to design a dynamic stop loss mechanism. While ensuring stop loss, it also minimizes unnecessary stop loss triggers. The strategy logic is simple and clear, allowing flexible optimization based on needs. It works best as trailing stop loss to maximize protection of profits. With proper parameter optimization and risk control, this strategy can be an effective stop loss tool in quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|nATRPeriod|
|v_input_2|4|nATRMultip|
|v_input_3|30|#Periods of Wick Protection|
|v_input_4|false|Max [1] or Avg Wick Protection [0]|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-12 00:00:00
end: 2023-10-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v2.0 13/10/2014
// Average True Range Trailing Stops Strategy, by Sylvain Vervoort 
// The related article is copyrighted material from Stocks & Commodities Jun 2009 
// Modified by River to add Bands, and change color of Trailing Stop and add Wick Protection. Now turned into a Strategy for Backtesting Purposes.
// After backtesting, it seems clear that it functions well as a Trailing Stop, but not as an Entry/Exit strategy.
////////////////////////////////////////////////////////////
strategy(title="ATR Trailing Stop Bands Strategy[R] ", overlay = true)
nATRPeriod = input(5)
nATRMultip = input(4)
length = input(30, "#Periods of Wick Protection", minval=2)
bType = input(0, "Max [1] or Avg Wick Protection [0]", minval=0, maxval=1)
avgupperwick = sma(close[1] <= open[1] ? high[1] - open[1] : high[1] - close[1], length)
maxupperwick = highest(close[1] <= open[1] ? high[1] - open[1] : high[1] - close[1], length)
avglowerwick = sma(close[1] > open[1] ? open[1] - low[1] : close[1] - low[1], length)
maxlowerwick = highest(close[1] > open[1] ? open[1] - low[1] : close[1] - low[1], length)
upperwick = bType == 0 ? avgupperwick : maxupperwick
lowerwick = bType == 0 ? avglowerwick : maxlowerwick
xATR = atr(nATRPeriod)
nLoss = nATRMultip * xATR 
upperband = iff(high < nz(upperband[1], 0) and high[1] < nz(upperband[1], 0), min(nz(upperband[1]), high + nLoss + upperwick), high + nLoss + upperwick)
lowerband = iff(low > nz(lowerband[1], 0) and low[1] > nz(lowerband[1], 0), max(nz(lowerband[1]), low - nLoss - lowerwick), low - nLoss - lowerwick) 
xATRTrailingStop = iff(low > nz(xATRTrailingStop[1], 0) and low[1] > nz(xATRTrailingStop[1], 0), max(nz(xATRTrailingStop[1]), low - nLoss - lowerwick),
 iff(high < nz(xATRTrailingStop[1], 0) and high[1] < nz(xATRTrailingStop[1], 0), min(nz(xATRTrailingStop[1]), high + nLoss + upperwick), 
//                        iff(low <= nz(xATRTrailingStop[1], 0) and close[1] > nz(xATRTrailingStop[1], 0), high + nLoss + upperwick, iff(high >= nz(xATRTrailingStop[1], 0) and close[1] < nz(xATRTrailingStop[1], 0), low - nLoss - lowerwick,0))))
 iff(low <= nz(xATRTrailingStop[1], 0) and close[1] > nz(xATRTrailingStop[1], 0), upperband[1], iff(high >= nz(xATRTrailingStop[1], 0) and close[1] < nz(xATRTrailingStop[1], 0), lowerband[1],0))))

pos =	iff(close[1] > nz(xATRTrailingStop[1], 0) and low <= nz(xATRTrailingStop[1], 0), 1,
 iff(close[1] < nz(xATRTrailingStop[1], 0) and high >= nz(xATRTrailingStop[1], 0), -1, nz(pos[1], 0))) 
color = pos == 1 ? red: pos == -1 ? green : blue 
plot(upperband, color=red, title="ATR Upper")
plot(xATRTrailingStop, color=color, title="ATR Trailing Stop", linewidth=2)
plot(lowerband, color=green, title="ATR Lower")

longCondition = (color == green and color[1] == red)
if (longCondition)
    strategy.entry("Long", strategy.long)
longExitCondition = (color == red and color[1] == green)
if (longExitCondition)
    strategy.close("Long")

shortCondition = (color == red and color[1] == green)
if (shortCondition)
    strategy.entry("Short", strategy.short)
shortexitCondition = (color == green and color[1] == red)
if (shortexitCondition)
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/429651

> Last Modified

2023-10-19 12:42:26
