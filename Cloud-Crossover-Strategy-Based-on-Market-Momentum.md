
> Name

Cloud-Crossover-Strategy-Based-on-Market-Momentum based on real market fluctuations
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The main idea of ​​this strategy is to use the cloud chart's delayed crossing line technology to determine the true trend of the market and achieve low-risk transactions. Go long when the delayed crossing line crosses the base line, and go short when it crosses below.
## Strategy Principle
This strategy determines market trends by calculating indicators such as conversion lines, baselines, and delayed crossing lines.
The conversion line is the mid-price line of the past 9 days, reflecting the average price of the past 9 days. The baseline is the mid-price line over the past 26 days, reflecting the longer-term average price. The delayed crossing line is the closing price after the price is delayed for 26 days.
When the short-term average price conversion line crosses the long-term average price baseline, it means that the short-term price breaks through the long-term price, which is a bull signal. When the delayed crossing line also crosses the baseline, the bullish trend is verified and the buy signal is stronger.
When the short-term average price conversion line crosses the long-term average price baseline, it means that the short-term price falls below the long-term price, which is a short signal. When the delayed crossing line also crosses below the baseline, the bear trend is verified and the sell signal is stronger.
By calculating these indicators and observing their intersections, you can determine the direction of future trends. When the delay crosses the baseline, go long, and when it crosses below, go short. You can use the cloud chart to determine the true market trend, filter out some false breakthroughs, and perform reverse operations.
## Strategic Advantages
1. The delayed crossing line has a denoising effect and can filter out many false breakthroughs.
2. Combine short-term and long-term moving averages to achieve long-short switching.
3. The timing of entry is precise and the retracement is small.
4. Easy to master, suitable for beginners.
5. Can be widely used in different varieties and cycles.
## Strategy Risk
1. Delayed crossing lines lag behind price changes and may miss some opportunities.
2. False signals will be generated when long and short period indicators diverge.
3. It is easy to get trapped in volatile market conditions.
4. Improper parameter optimization will affect the effect.
It is necessary to optimize the parameter combination and cooperate with stop loss to control risks. Consider adding other indicators to filter signals.
## Optimization direction
1. Optimize moving average parameters such as conversion lines and baselines to improve strategy stability.
2. Increase tolerance settings to avoid frequent transactions.
3. Filter based on volatility, trading volume and other indicators to ensure that transactions follow the trend.
4. Adjust the position size according to the characteristics of the product and the trader's risk preference.
5. Make trend judgments in large cycles, and make specific entries in small cycles.
## Summarize
This strategy uses Cloud Chart's delayed crossing line technology to determine the true market trend and achieve low-risk transactions. The strategies are simple to understand and easy to master. However, there are also certain risks that require targeted optimization. The strategy effect can be further improved through parameter adjustment, stop loss avoidance, signal filtering and other means. Overall, this strategy provides an effective trading tool for beginners.
|| 

## Overview

The core idea of this strategy is to determine the real trend of the market using the delayed crossover line of the Ichimoku Cloud for low-risk trading. Go long when the delayed crossover line crosses above the baseline, and go short when it crosses below.

## Strategy Logic

This strategy calculates conversion line, baseline, delayed crossover line and other indicators to determine market trend. 

The conversion line is the mid-price of the past 9 days, reflecting the recent 9-day average price. The baseline is the mid-price of the past 26 days, reflecting the longer term average price. The delayed crossover line is the closing price delayed by 26 days.

When the short-term average price conversion line crosses above the long-term average price baseline, it indicates the short-term price breaks through the long-term price, which is a bullish signal. When the delayed crossover line also crosses above the baseline, it validates the bullish trend and this long signal is stronger.

When the short-term average price conversion line crosses below the long-term average price baseline, it indicates the short-term price falls through the long-term price, which is a bearish signal. When the delayed crossover line also crosses below the baseline, it validates the bearish trend and this short signal is stronger. 

By calculating these indicators and observing their crossover, we can determine the future trend direction. Go long when the delayed crossover line crosses above the baseline, and go short when it crosses below. This uses the Ichimoku Cloud to determine the real market momentum and filter out some false breakouts for reverse operations.

## Advantages of the Strategy

1. The delayed crossover line filters out many false breakouts.

2. Combining short-term and long-term moving averages enables switching between long and short.

3. Precise entry timing with small drawdowns. 

4. Easy to understand, suitable for beginners.

5. Can be widely applied across different products and timeframes.

## Risks of the Strategy

1. The delayed crossover line lags price changes and may miss some opportunities.

2. Divergence between long and short cycles may generate false signals. 

3. Prone to being trapped in range-bound markets.

4. Improper parameter optimization affects performance.

Risk management by stop loss and parameter optimization is needed. Other indicators may be added to filter signals.

## Optimization Directions 

1. Optimize moving average parameters like conversion and baseline to improve stability.

2. Introduce tolerance to avoid excessive trading.

3. Add volatility, volume and other filters to ensure trading with the trend.

4. Adjust position sizing based on product character and risk preference.

5. Use higher timeframe for trend analysis and lower timeframe for entries.

## Conclusion

This strategy uses the delayed crossover line of the Ichimoku Cloud to determine market momentum for low-risk trading. The strategy is simple and easy to understand. But it also has some risks, requiring custom optimization. Further improvements can be made through parameter tuning, risk management, signal filtering etc. Overall, it provides an effective trading tool for beginners.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Conversion Line Periods|
|v_input_2|26|Base Line Periods|
|v_input_3|52|Lagging Span 2 Periods|
|v_input_4|26|Displacement|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-25 00:00:00
end: 2023-09-24 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="Chikou Crossover", shorttitle="Chikou", overlay=true)

conversionPeriods = input(9, minval=1, title="Conversion Line Periods"),
basePeriods = input(26, minval=1, title="Base Line Periods")
laggingSpan2Periods = input(52, minval=1, title="Lagging Span 2 Periods"),
displacement = input(26, minval=1, title="Displacement")

donchian(len) => avg(lowest(len), highest(len))

conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)

plot(conversionLine, color=#0496ff, title="Conversion Line")
plot(baseLine, color=#991515, title="Base Line")
plot(close, offset = -displacement, color=#459915, title="Lagging Span")

p1 = plot(leadLine1, offset = displacement, color=green,
 title="Lead 1")
p2 = plot(leadLine2, offset = displacement, color=red, 
 title="Lead 2")
fill(p1, p2, color = leadLine1 > leadLine2 ? green : red)

if (crossover(baseLine, close[26]))
    strategy.entry("ChikouLE", strategy.long, comment="ChikouLE")

if (crossunder(baseLine, close[26]))
    strategy.entry("ChikouSE", strategy.short, comment="ChikouSE")

// plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)

```

> Detail

https://www.fmz.com/strategy/427806

> Last Modified

2023-09-25 17:28:29
