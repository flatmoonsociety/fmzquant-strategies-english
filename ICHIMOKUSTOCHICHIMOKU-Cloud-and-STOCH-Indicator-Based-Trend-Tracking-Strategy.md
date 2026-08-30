
> Name

Trend tracking strategy based on ICHIMOKU pattern and STOCH indicatorICHIMOKU-Cloud-and-STOCH-Indicator-Based-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3d425018bc9330299cae1ca8fdc5bc6f8eb8435be1d72705e4cdc380d1f736d3.png)
[trans]

## Overview
This strategy is based on the ICHIMOKU cloud shape indicator and the STOCH random indicator to realize the judgment and tracking of trends. The strategy is called "Cloud Stoch Trend Following Strategy".
## Strategy Principle
This strategy mainly uses the ICHIMOKU cloud chart and STOCH indicator to determine the current trend direction, as well as overshoot, overbought and oversold conditions.
When the Conversion Line crosses the Base Line and the Stoch indicator rebounds from the oversold area, it is considered that the market is bullish, and the strategy adopts a bullish direction; when the Conversion Line crosses the Base Line and the Stoch indicator falls back from the overbought area, the market is considered to be bearish, and the strategy adopts a bearish direction.
In the code, the Conversion Line is defined as the average of the highest and lowest prices of nearly N1 K lines; the Base Line is defined as the average of the highest and lowest prices of nearly N2 K lines. A bullish signal is generated when the conversion line crosses the base line.
In the Stoch indicator, the overbought line and oversold line thresholds are defined, as well as the smoothing parameters K and D. Stoch generates a bullish signal when it rebounds from oversold territory and a bearish signal when it retreats from overbought territory.
Combining the two indicators, this strategy realizes the judgment of the trend direction.
## Advantage Analysis
This strategy combines graphical form indicators and overbought and oversold indicators to effectively determine the direction of the trend.
Compared with using the trend judgment indicator alone, this strategy comprehensively considers the trend and overshoot situation, and can more accurately judge the entry opportunity.
The ICHIMOKU cloud chart can identify medium and long-term trends, while the Stoch indicator can detect short-term overbought and oversold conditions. The two complement each other to form a systematic judgment.
## Risk Analysis
This strategy mainly involves the following risks:
1. When a sudden black swan event occurs, there is a systemic risk of indicator failure.
2. There is a certain lag, and there is a risk of missing part of the market or opening a position in the opposite direction.
3. There is a certain degree of subjectivity in the comprehensive judgment of multiple factors, and improper parameter settings may lead to the risk of errors.
4. When transactions are frequent, transaction costs will have a certain impact on profits.
Corresponding optimization measures:
1. Make judgments based on news events to avoid blind trading when major policy events occur.
2. Appropriately shorten the cycle parameters to reduce the probability of lagging judgment.
3. Conduct backtesting to optimize parameters and improve the scientific nature of parameter settings.
4. Appropriately increase the stop-profit and stop-loss range and reduce the frequency of transactions.
## Optimization direction
This strategy can be optimized mainly from the following aspects:
1. Optimize the cycle parameters of ICHIMOKU conversion lines and baselines to make them more in line with the characteristics of different markets.
2. Optimize the K and D smoothing parameters of the Stoch indicator, as well as the overbought and oversold threshold parameters.
3. Add other indicator judgments to form a multi-factor model and improve the systematicness of the strategy.
4. Optimize the stop-profit and stop-loss points to reduce the frequency of transactions while ensuring profits.
5. Add a module for judging emergencies to avoid failure when major events occur.
## Summarize
This strategy is based on the ICHIMOKU cloud chart and Stoch indicator to achieve comprehensive judgment on the trend direction and overbought and oversold conditions, and can effectively track the trend market. Due to the consideration of graphic forms and quantitative indicators, the strategy is more systematic. In the future, this strategy can be further optimized by optimizing parameters, adding other indicators, and emergency event judgment modules.
||


## Overview

This strategy is based on the ICHIMOKU cloud chart pattern indicator and the STOCH random indicator to determine and track trends. The strategy name is "ICHIMOKU Cloud Stoch Trend Tracking Strategy".

## Strategy Principle 

The strategy mainly judges the current trend direction and overbought/oversold situations through the ICHIMOKU cloud chart and the STOCH indicator.

When the Conversion Line crosses above the Base Line and the Stoch indicator bounces back from the oversold area, it is considered a bullish trend and the strategy takes a bullish direction. When the Conversion Line crosses below the Base Line and the Stoch indicator falls back from the overbought area, it is considered a bearish trend and the strategy takes a bearish direction.

In the code, the Conversion Line is defined as the average of the highest and lowest prices of the last N1 bars; The Base Line is defined as the average of the highest and lowest prices of the last N2 bars. A bullish signal is generated when the conversion line crosses above the base line.  

The Stoch indicator defines overbought and oversold threshold lines, as well as smoothing parameters K and D. A bullish signal is generated when the Stoch bounces back from the oversold area, and a bearish signal is generated when it falls back from the overbought area.

By combining the two indicators, the strategy determines the trend direction.

## Advantage Analysis

The strategy combines chart pattern indicators and overbought/oversold indicators to effectively determine the trend direction.

Compared to using a single trend judgment indicator, this strategy comprehensively considers both trend and overrun situations, and can more accurately determine entry timing.

The ICHIMOKU cloud chart can identify medium and long term trends, while the Stoch indicator can discover short-term overbought/oversold situations. The two complement each other to form systematic judgments.

## Risk Analysis

The main risks of this strategy are:

1. The risk of indicator failure in case of black swan events. 

2. There is some lag, which may miss part of the trend or reverse opening positions.

3. The combined multiple factors judgment has some subjectivity, and improper parameter settings may cause mistakes.

4. High trading frequency may impact profits due to transaction costs.

Corresponding optimization measures:

1. Combine news events to avoid blind trading during major policy events.

2. Appropriately shorten cycle parameters to reduce lag probability.

3. Optimize parameters through backtesting to improve scientific settings.

4. Appropriately increase take profit and stop loss ranges to reduce trading frequency.

## Optimization Directions

The main optimization directions for this strategy are:

1. Optimize the cycle parameters of the ICHIMOKU conversion line and base line to better fit different market characteristics.

2. Optimize the K, D smoothing parameters and overbought/oversold threshold values of the Stoch indicator. 

3. Increase other indicators to form a multifactor model and improve system reliability.

4. Optimize take profit and stop loss points to reduce trading frequency while ensuring profitability.

5. Add a module to judge emergencies and avoid failure during major events.

## Summary

This strategy combines ICHIMOKU cloud charts and Stoch indicators to make comprehensive judgments on trend direction and overbought/oversold situations, which can effectively track trending markets. By considering chart patterns and quantitative indicators, the strategy is more systematic. Future optimizations may include adjusting parameters, adding other indicators, adding emergency judgment modules, etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|length|
|v_input_1|5|smoothK|
|v_input_2|3|smoothD|
|v_input_3|25|OverBought|
|v_input_4|65|OverSold|
|v_input_5|1800|Profit|
|v_input_6|1200|Stop|
|v_input_int_2|9|Conversion Line Length|
|v_input_int_3|26|Base Line Length|
|v_input_int_4|52|Leading Span B Length|
|v_input_int_5|true|Lagging Span|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-15 00:00:00
end: 2023-11-14 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("ICHI + STOCH V1", overlay=true)
length = input.int(20, minval=1)
smoothK = input(5)
smoothD = input(3)
OverBought = input(25)
OverSold = input(65)
Profit = input(1800)
Stop = input(1200)
k = ta.sma(ta.stoch(close, high, low, length), smoothK)
d = ta.sma(k, smoothD)
co = ta.crossover(k,d)
cu = ta.crossunder(k,d)
conversionPeriods = input.int(9, minval=1, title="Conversion Line Length")
basePeriods = input.int(26, minval=1, title="Base Line Length")
laggingSpan2Periods = input.int(52, minval=1, title="Leading Span B Length")
displacement = input.int(1, minval=1, title="Lagging Span")
conversionLine = math.avg(ta.lowest(conversionPeriods), ta.highest(conversionPeriods))
baseLine = math.avg(ta.lowest(basePeriods), ta.highest(basePeriods))
leadLine1 = math.avg(conversionLine, baseLine)
leadLine2 = math.avg(ta.lowest(laggingSpan2Periods), ta.highest(laggingSpan2Periods))
TREND = ta.ema(math.avg(leadLine1,leadLine2),displacement)
//plot(conversionLine, color=#2962FF, title="Conversion Line")
//plot(baseLine, color=#B71C1C, title="Base Line")
//plot(close, offset = -displacement + 1, color=#43A047, title="Lagging Span")
plot(TREND, color=#2962FF, title="TREND")
p1 = plot(leadLine1,style=plot.style_line, offset = displacement - 1, color=#A5D6A7,
	 title="Leading Span A")

p2 = plot(leadLine2,style=plot.style_line, offset = displacement - 1, color=#EF9A9A,
	 title="Leading Span B")
fill(p1, p2, color = leadLine1 > leadLine2 ? color.rgb(67, 160, 71, 90) : color.rgb(244, 67, 54, 90))
close_price = ta.sma(close,1)
pc = plot(close_price,style=plot.style_line, color=#2a0ab9,
	 title="Price Close")
if (not na(k) and not na(d))
	if (co and k < OverSold)and(close_price > TREND)
		strategy.entry("BUY order", strategy.long, comment="BUY order")
		strategy.exit("exitBUY", "BUY order", profit = Profit, loss = Stop)
	if (cu and k > OverBought)and(close_price < TREND)
		strategy.entry("SELL order", strategy.short, comment="SELL order")
		strategy.exit("exitSELL", "SELL order", profit = Profit, loss = Stop)
//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)
```

> Detail

https://www.fmz.com/strategy/432182

> Last Modified

2023-11-15 11:19:29
