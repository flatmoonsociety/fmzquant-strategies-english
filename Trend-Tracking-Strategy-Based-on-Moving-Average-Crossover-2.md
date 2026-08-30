
> Name

Trend-Tracking-Strategy-Based-on-Moving-Average-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13e1811ad82bbdcccfe.png)
[trans]
## Overview
This strategy calculates the EMA moving averages of different periods, determines their crossover situations, and combines the RSI indicator to determine the market trend to achieve trend following transactions. The core idea is: when the short-term EMA line crosses the longer-period EMA line from below, a buy signal is generated; when the short-term EMA crosses the longer-period EMA line from above, a sell signal is generated. The trading signal formed by such an EMA crossover tracks the market trend.
## Strategy Principle
This strategy mainly uses the speed characteristics of EMA to calculate 5 EMA lines of different periods, including 9-day line, 21-day line, 51-day line, 100-day line and 200-day line. Short-period EMA lines can respond to price changes faster, while longer-period EMA lines are relatively insensitive to noise and can reflect market trends. When the short-period EMA line crosses the longer-period EMA line from below, it means that the price has begun to rise, which is a buy signal; when the short-period EMA line crosses the longer-period EMA line from above, it means that the price has begun to fall, which is a sell signal. Therefore, the rising and falling trends of the market can be judged by the intersection of the EMA lines.
In addition, this strategy also introduces the RSI indicator to assist in judgment. Only when the RSI is greater than 65, a buy signal is issued; only when the RSI is less than 40, a sell signal is issued. This can filter out some false signals and prevent trades from being misled by huge price shocks.
## Strategic Advantages
The biggest advantage of this strategy is that it can effectively track market trends. Set multiple groups of EMA moving averages through the speed characteristics of EMA, judge their crossover situations, form buy and sell signals, and capture medium and long-term market trends. This trend following strategy has a higher winning rate and is suitable for long-term holdings.
In addition, this strategy also introduces the RSI indicator to assist in judgment, which can effectively filter noise and avoid being misled by short-term market fluctuations, thus improving the reliability of signals. The RSI parameter is set to 14, which can capture clearer overbought and oversold conditions.
In general, this strategy combines the trend tracking of moving averages and the overbought and oversold judgment of RSI. It can not only capture market trends, but also effectively filter out false signals. It is a highly reliable trend following strategy.
## Strategy Risk
The biggest risk with this strategy is that there will be a certain lag. The EMA itself has a certain lag in price changes, especially the longer period EMA, which means that there will be a certain delay in the generation of buy and sell signals. If there is a sharp reversal in price, a large floating loss will occur.
In addition, when the market is consolidating and oscillating, EMA crossover signals will appear frequently. At this time, setting the RSI parameter to 14 may filter out too many signals, resulting in missed trading opportunities.
To reduce these risks, the period parameters of the longer EMA can be appropriately shortened, and the overbought and oversold thresholds of the RSI can be appropriately relaxed to make the signal parameter settings more sensitive. Of course, there is also a higher risk of misleading. It is necessary to adjust parameters according to actual market conditions and find the best balance point.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimization of EMA cycle parameters. You can test more combinations of EMA period parameters to find the best parameter pair to make the signal more sensitive and reliable.
2. RSI parameter optimization. The RSI overbought and oversold zone range can be appropriately expanded to trigger signals more frequently, or the range can be narrowed to reduce the risk of misleading.
3. Add a stop loss mechanism. You can set a trailing stop loss or a pending order stop loss to lock in profits, which can effectively limit the risk of losses.
4. Combine with other indicators. Other indicators such as KDJ and MACD can be introduced to make the signal more reliable and improve the strategy effect.
5. Optimize warehouse management. The position size can be dynamically adjusted according to the degree of market volatility, and the position can be increased when the trend becomes clearer.
## Summarize
This strategy achieves effective capture and tracking of market trends by calculating multiple sets of EMA moving averages and judging their crossover situations, combined with the RSI indicator for auxiliary judgment. It combines the two major ideas of trend tracking and overbought and oversold judgment, which can capture medium and long-term market conditions while effectively filtering misleading signals. Through parameter optimization and strategy combination, a stable and efficient quantitative trading system can be formed. It represents a typical case of moving average strategy and indicator fusion strategy.
||

## Overview  

This strategy calculates EMA lines of different cycles to determine their crossover situation and uses the RSI indicator to judge the market trend, so as to implement trend tracking trading. The core idea is: generating buy signals when the short-term EMA line crosses over the longer-cycle EMA line from the bottom; generating sell signals when the short-term EMA crosses below the longer-cycle EMA line. By using such EMA crossover signals, the strategy tracks the market trend.

## Strategy Principle

This strategy mainly utilizes the fast and slow properties of EMA and calculates 5 EMA lines of different cycles, including 9-day, 21-day, 51-day, 100-day and 200-day line. The short-cycle EMA line can respond to price changes faster, while longer-cycle EMA lines are relatively insensitive to noise and can reflect market trend.

When the short-cycle EMA line crosses over the longer-cycle EMA line from the bottom, it indicates the price starts rising and triggers the buy signal. When the short-cycle EMA crosses below the longer-cycle EMA, it indicates the price starts declining and triggers the sell signal. Therefore, by judging the crossover situations of EMA lines, we can determine the uptrend or downtrend of the market.

In addition, this strategy also introduces the RSI indicator for auxiliary judgement. Buy signals will only be triggered when RSI is greater than 65, and sell signals only when RSI is less than 40. This helps filter out some wrong signals and avoid being misguided by huge price swings.

## Advantages  

The biggest advantage of this strategy is that it can effectively track the market trend. By utilizing the fast and slow properties of EMA to set up multiple groups of EMA lines and judging their crossover situations, it can capture the mid-long term trend of the market. This kind of trend tracking strategy has a relatively high winning rate and suits long-term holding.

In addition, this strategy also introduces the RSI indicator for assistance judgement, which can effectively filter out noise and avoid being misguided by short-term market fluctuations, thus improving the reliability of trading signals. The RSI parameter is set to 14 so that it can capture relatively significant overbought/oversold situations.

In conclusion, this strategy combines the strengths of moving average trend tracking and RSI overbought/oversold judgement. It can not only capture market trends but also filter out wrong signals effectively, making itself a trend tracking strategy with relatively high reliability.

## Risks

The biggest risk of this strategy is there will be some lag. EMA itself has some lagging attribute when responding to price changes, especially longer-cycle EMA. This means the generation of buy and sell signals will be delayed. In case of sharp price reversion, huge floating loss may occur.  

Also, when the market is fluctuating within range, crossover signals between EMA lines will occur frequently. The RSI parameter of 14 may filter out too many signals, leading to missing trading opportunities.

To reduce the risks above, we may shorten the period of longer-cycle EMA appropriately and loosen the overbought/oversold threshold of RSI to make the signal more sensitive. Of course this exposes to higher false signal risks. Adjustments on parameters need to be made based on real market situations to find the optimal balance point.

## Optimization Directions

This strategy can be optimized from the following aspects:

1. Optimize EMA period parameters. Trying more combinations of EMA periods to find the best signal sensitivity and reliability. 

2. Optimize RSI parameters. Properly enlarge the overbought/oversold range to trigger signals more frequently or narrow it down to reduce false signals.

3. Add stop loss mechanisms such as moving stop loss or pending orders to lock in profit and reduce loss risk.

4. Incorporate other indicators like KDJ, MACD to improve signal reliability.

5. Optimize position management dynamically based on market volatility.

## Conclusion

This strategy calculates multiple groups of EMA lines to determine crossover situations combined with RSI indicator to effectively capture and track market trends. By integrating the ideas of trend tracking and overbought/oversold judgement, it can capture mid-long term trends with effective false signal filtering. After parameter optimization and strategy integration, it can form a steady and efficient quantitative trading system, representing a typical case of moving average strategies and indicator fusion strategies.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-06 00:00:00
end: 2024-02-05 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Ravikant_sharma

//@version=5

strategy('new', overlay=true)

start = timestamp(1990, 1, 1, 0, 0)
end = timestamp(2023, 12, 12, 23, 59)
ema0 = ta.ema(close, 9)
ema1 = ta.ema(close, 21)
ema2 = ta.ema(close, 51)
ema3 = ta.ema(close, 100)
ema4 = ta.ema(close, 200)

rsi2=ta.rsi(ta.sma(close,14),14)
plot(ema0, '9', color.new(color.green, 0))
plot(ema1, '21', color.new(color.black, 0))
plot(ema2, '51', color.new(color.red, 0))
plot(ema3, '200', color.new(color.blue, 0))   

//plot(ema4, '100', color.new(color.gray, 0)) 


//LongEntry = (  ta.crossover(ema0,ema3)  or  ta.crossover(ema0,ema2) or  ta.crossunder(ema2,ema3) ) // ta.crossover(ema0,ema1) //
LongEntry=false
if ta.crossover(ema0,ema1) 
    if rsi2>65
        LongEntry:=true
if ta.crossover(ema1,ema2)
    if rsi2>65
        LongEntry:=true
        
LongExit =  ta.crossunder(ema0,ema2) or close >(strategy.position_avg_price*1.25) or rsi2 <40 or close < (strategy.position_avg_price*0.98)



if true
    if(LongEntry and rsi2>60)
        strategy.entry('Long', strategy.long, 1)
    if(LongExit)
        strategy.close('Long') 


```

> Detail

https://www.fmz.com/strategy/441152

> Last Modified

2024-02-06 11:37:23
