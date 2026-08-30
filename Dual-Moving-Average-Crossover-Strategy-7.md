
> Name

Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7e15eaf520bee1267f3eb1805c8232156994be9684624fc93f2a1b8b23a37b6e.png)

[trans]


## Overview
This strategy generates trading signals based on the difference between the moving averages of a pair of moving averages. It calculates two moving averages of fast period and slow period. When the fast line breaks through the slow line from below, a buy signal is generated; when the fast line breaks down from above and breaks through the slow line, a sell signal is generated.
## Principle analysis
The core logic of this strategy is to calculate two moving averages SMA (len1) and SMA (len2), and their difference dif. Among them, len1 represents the short-term moving average period, and len2 represents the long-term moving average period. The short-term moving average can respond to price changes more quickly, and the long-term moving average can better reflect the long-term trend.
When the short-term moving average crosses the long-term moving average from below, it means that the short-term price begins to rise above the long-term trend, and you can buy; when it crosses below the long-term moving average from above, it means that the short-term price begins to fall below the long-term trend, and you can sell.
In order to filter out misoperations, the strategy also introduces out3 as a trading signal line. out3 is the result of sma smoothing of the difference between the short-term moving average and the price median. A trading signal is generated only when out3 crosses dif.
Specifically, the long variable has a positive value when out3 crosses dif upward, which is used as a buy signal; the short variable has a negative value when out3 crosses dif downward, which is used as a sell signal. strategy.entry generates a buy order based on the long signal, and strategy.close generates a sell closing order based on the short signal.
## Advantage Analysis
This is a very simple and intuitive strategy for following trends. It uses the method of moving average crossover caused by the different periods of double moving averages to capture the trend conversion point, which can be more reliable than the single moving average system. And the introduction of filtering of trading signal lines can avoid false signals generated in volatile markets to a certain extent.
Compared with methods such as trailing stop loss, it adopts the trend following concept, which can maximize profits and will not be stopped when the trend is longer. At the same time, it will also control losses and close positions promptly when the trend reverses.
This strategy has fewer parameters and is easy to master and adjust. It is suitable as an introductory strategy for beginners to learn algorithmic trading.
## Risks and improvements
The biggest risk of this strategy is that the cycle parameters of the double moving average are improper, resulting in incorrect trading signals. If the short-term moving average period len1 is too long, you will miss the opportunity at the beginning of the trend; if it is too short, it will increase the probability of false signals. If the long-term moving average len2 is too long, position adjustments will be delayed; if it is too short, it will be easily disturbed by market fluctuations.
You can obtain the best combination by adjusting the parameters of len1 and len2, or you can try to introduce adaptive moving averages to dynamically adjust the period. In addition, false signals can be reduced by optimizing filter parameters.
Trend following strategies also need to pay attention to controlling the size of a single loss, and can set stop loss points or introduce position management for optimization.
## Summarize
The double moving average difference strategy is a very typical representative of trend following strategies. Its simple double moving average crossover system brings a stable signal source, and combined with the filter can effectively avoid being disturbed by market fluctuations. Better strategy performance can be obtained by optimizing the moving average cycle parameters. This strategy is very suitable to learn as an introductory strategy to algorithmic trading.
||


## Overview

This strategy generates trading signals based on the difference between two moving averages with different timeframes. It calculates a faster SMA and a slower SMA, and produces buy signals when the fast SMA crosses above the slow SMA from below, and sell signals when the fast SMA crosses below the slow SMA from above.

## How It Works 

The core logic of this strategy is to compute two moving averages, SMA(len1) and SMA(len2), and their difference dif. Here len1 represents the period of the faster MA and len2 the slower MA. The faster MA responds quicker to price changes while the slower MA reflects the long term trend better.

When the faster MA crosses above the slower MA from below, it indicates the short term price has started to rise above the long term trend, and thus a long entry can be taken. When the faster MA crosses below the slower MA from above, it signals the short term price has started to fall below the trend, and a short position can be entered.

To filter out false signals, the strategy also uses out3 as the trading signal line, which is the smoothed difference between the faster MA and price midpoint. Only when out3 crosses dif will trades be triggered. 

Specifically, the long variable holds positive values when out3 crosses above dif, giving buy signals. The short variable holds negative values when out3 crosses below dif, generating sell signals. strategy.entry entries long when long signal occurs, and strategy.close closes long when short signal emerges.

## Advantage Analysis

This is a very simple and intuitive strategy to follow trends. It uses the crossover of two MAs of different periods to identify trend reversal points, which can be more reliable than a single MA system. The filter of trading signal line also helps avoid false signals in choppy markets to some extent.

Compared to stop loss, it adopts a trend following mindset to maximize profits during longer trends without being stopped out. At the same time, it also controls losses by closing positions in time when trend reverses.

This strategy has few parameters and is easy to understand and tune, making it suitable as a beginner's algo trading strategy.

## Risks and Improvements

The biggest risk of this strategy is improperly chosen MA periods resulting in bad signals. If len1 is too long, early trend moves will be missed; if too short, whipsaws increase. If len2 is too long, position adjustments will be delayed; if too short, it may be disturbed by market noise.

The parameters can be optimized by trying different len1 and len2 values to find the best combination. Adaptive MAs can also be tested to dynamically change periods. The filter can also be improved to further reduce false signals.

Trend following strategies should also control loss on single trades, through stop loss or position sizing. 

## Conclusion

The dual MA crossover strategy is a quintessential trend following representative. Its simple dual MA crossover system provides steady signals, while the filter helps avoid noise. With optimized MA periods, it can achieve good performance. The strategy serves well as a beginner's algo trading strategy to learn.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Length1|
|v_input_2|100|Length2|
|v_input_3|true|Smoothing|
|v_input_4_ohlc4|0|Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-10 00:00:00
end: 2023-10-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//by afrazium
//@version=3
strategy(title="SMA Diff strat", shorttitle="SMAD STR", overlay=false, initial_capital=1, precision=8, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.1, calc_on_order_fills= false, calc_on_every_tick=false, pyramiding=0)
len1 = input(50, minval=1, title="Length1"), len2 = input(100, minval=1, title="Length2"), smo = input(1, minval=1, title="Smoothing")
src = input(ohlc4, title="Source")

mid = src
expr1 = sma(src, len1), expr2 = sma(src, len2)
dif = (expr1 - expr2), out1 = (mid - expr1), out2 = (mid - expr2), out3 = sma(out1, smo)

long = crossover(out3, dif) ? out3 : na, short = crossunder(out3, dif) ? out3 : na

plot(out3, color=black, linewidth=2), hline(0)
clr = out2 >= out1 ? lime : red, plot(dif, color=clr, linewidth=2)
plot(long, title = 'Crossover', color = green, style = circles, linewidth=4), plot(short, title = 'Crossunder', color = red, style = circles, linewidth=4)

strategy.entry("buy", strategy.long, when=crossover(out1, dif))
strategy.close("buy", when=crossunder(out1, dif))

//plot(out2, color=blue, linewidth=2)
//A = plot(mid/10, color=red, linewidth=1, transp=100), B = plot(mid/20, color=red, linewidth=1, transp=100)
//C = plot(-mid/10, color=green, linewidth=1, transp=100), D = plot(-mid/20, color=green, linewidth=1, transp=100)
//fill(A, B, color=red), fill(C, D, color=green)


```

> Detail

https://www.fmz.com/strategy/429464

> Last Modified

2023-10-17 13:54:05
