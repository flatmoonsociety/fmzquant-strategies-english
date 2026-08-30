
> Name

Trend tracking strategy based on Ichimoku-Momentum-Tracking-Strategy-Based-on-Ichimoku-Cloud
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11bbf4861b173c46134.png)
 [trans]

## Overview
This strategy combines moving averages, the Relative Strength Index (RSI), and the Ichimoku indicator with the goal of identifying trends in stock prices and trading within the context of the trends. The core idea is that when the short-term average crosses the medium- and long-term average and breaks above the cloud on the Ichimoku Balance Sheet, a buy signal is generated; when the short-term average crosses below the medium- and long-term average and breaks below the cloud, a sell signal is generated.
## Strategy Principle
This strategy uses four moving averages on the 13th, 21st, 89th and 233rd. The 13-day line represents the short-term trend, the 233-day line represents the long-term trend, and the 21-day line and the 89-day line are in the mid-term. When the short-term average crosses the medium- and long-term average, it means that the stock price trend changes from falling to rising, generating a buy signal. On the contrary, if the short-term average falls below the medium- and long-term average, it is a sell signal.
In addition, this strategy also incorporates the conversion line, base line and front line from the Ichimoku Balance Sheet indicator. The conversion line uses a 9-day moving average, the baseline uses a 26-day moving average, and the front line uses a medium- and short-term moving average. When the price crosses above the front line, it is a buy signal, and when it crosses below, it is a sell signal.
Finally, the strategy also uses the 12-day and 24-day lines in the RSI indicator. The 12-day line represents short-term overbought and oversold conditions, and the 24-day line represents mid-term overbought and oversold conditions. The strategy confirms trading signals by determining the intersection of the 12-day RSI line and the 24-day RSI line.
## Strategic Advantages
- Use moving averages to identify trend directions
- Ichimoku balance table determines the timing of entry and exit
- RSI indicator to avoid false breakouts
This strategy is very good at identifying the main trend direction of stock prices. Moving averages combined with Ichimoku Balance Sheet indicators make buy and sell signals more accurate. In addition, the introduction of the RSI indicator also avoids possible false breakthroughs. In general, this strategy combines the advantages of multiple indicators and can effectively lock in the main trends and profit from them.
## Risk Analysis
- Trend reversal risk
Traders need to pay close attention to market changes. Once there are signs that the price touches the average line, they must be vigilant and close their positions in a timely manner.
- Parameter optimization space
There is room for optimization in the period setting of the moving average and the parameters of the Ichimoku Balance Sheet, and traders can choose the optimal parameter combination according to different varieties.
- Transaction frequency is high
The transaction frequency of the strategy will be relatively high, and the handling fee issue needs to be fully considered. Parameters can be adjusted appropriately to reduce unnecessary transactions.
## Optimization direction
- Add stop loss and take profit strategy
The current strategy does not set stop-loss and take-profit logic, which will bring certain risks. You can consider adding such modules to your strategy later.
- Parameter optimization
For different trading varieties, the moving average cycle, Ichimoku balance table parameters, RSI cycle, etc. can be optimized to find the best combination. This can further improve the stability of the strategy.
- Combine more indicators
In addition to the indicators that have been used, you can also consider combining volatility, trading volume changes and other derivative indicators to form a more comprehensive basis for judgment.
## Summarize
This strategy combines moving averages, relative strength indicators and Ichimoku balance sheet indicators to effectively identify the main trends in security prices, and is a typical trend following strategy. The advantage of the strategy is that the indicator combination is comprehensive and the trend can be well grasped; however, the trading frequency is high and there is also a certain degree of retracement risk. By introducing stop-loss, take-profit, parameter optimization and other means, there is still room for improvement in the effectiveness of this strategy. Overall, this strategy is a stable and reliable trend strategy, suitable for investors who have a certain risk tolerance and want to continue to make profits.
||

## Overview

This strategy combines moving averages, relative strength index (RSI) and ichimoku cloud to identify price trends and make trades accordingly. The core idea is to generate buy signals when the short term moving average crosses above the medium term average and penetrates above the cloud, and to generate sell signals when the reverse happens.  

## Strategy Logic

The strategy employs four moving averages - 13, 21, 89 and 233 days. The 13 day MA represents short term trend while the 233 day line shows long term trend. The 21 and 89 day MAs are in between. When the short term MA crosses above the medium term ones, it indicates an upside breakout and generates buy signals. The opposite cross leads to sell signals.

In addition, the conversion line (9 day MA), base line (26 day MA) and leading span (average of conversion and base lines) of the Ichimoku cloud are used. Penetrating above the leading span gives buy signals while breaking below it shows sells.

Furthermore, 12 and 24 day RSIs are applied. The 12 day RSI represents short term overbought/oversold levels while the 24 day line shows medium term situations. Crossovers between the two can help confirm trading signals.  

## Advantages

- Identify trend direction with MAs  
- Ichimoku cloud for entry and exit timing   
- Avoid false breakouts using RSI

This strategy excels at capturing the prevailing trend of security prices. Entry and exit based on MAs and ichimoku improves precision. Moreover, RSI crossover helps avoid false signals. In summary, this combines strengths of multiple indicators to effectively trade along the trend.  

## Risks 

- Trend reversal risk  
Traders should watch out for prices touching moving averages and get ready to close positions. 

- Parameter optimization  
There are rooms to improve MA periods, Ichimoku parameters etc. Traders can experiment to find the optimal set for different products.

- High trading frequency  
The strategy may trade quite frequently, thus commission costs need to be considered. Fine tuning parameters can help reduce unnecessary trades.


## Improvements

- Add stop loss/profit target  
Introducing such risk management mechanisms would reduce drawdowns.

- Parameter tuning  
Optimize MA periods, Ichimoku inputs, RSI days etc for better stability across different products.

- Incorporate more indicators  
Other derived indicators around volatility and volume could provide additional insight.

## Conclusion
This is a typical trend following strategy harnessing strengths of MAs, RSI and Ichimoku cloud. It reliably locks onto prevailing trends. Through refinements like stop loss, parameter optimization etc, performance can be further improved. Overall this is a stable, profitable momentum strategy suitable for investors with adequate risk appetite seeking persistent gains.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Tenkan Sen Periods|
|v_input_2|26|Kijun Sen Periods|
|v_input_3|52|Senkou Span B Periods|
|v_input_4|26|Displacement|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-11 00:00:00
end: 2024-01-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy("EMA + Ichimoku Kinko Hyo Strategy", shorttitle="EMI", overlay=true, default_qty_type=strategy.percent_of_equity, max_bars_back=1000, default_qty_value=100, calc_on_order_fills= true, calc_on_every_tick=true, pyramiding=0)

TenkanSenPeriods = input(9, minval=1, title="Tenkan Sen Periods")
KijunSenPeriods = input(26, minval=1, title="Kijun Sen Periods")
SenkouSpanBPeriods = input(52, minval=1, title="Senkou Span B Periods")
displacement = input(26, minval=1, title="Displacement")
donchian(len) => avg(lowest(len), highest(len))
TenkanSen = donchian(TenkanSenPeriods)
KijunSen = donchian(KijunSenPeriods)
SenkouSpanA = avg(TenkanSen, KijunSen)
SenkouSpanB = donchian(SenkouSpanBPeriods)
SenkouSpanH = max(SenkouSpanA[displacement - 1], SenkouSpanB[displacement - 1])
SenkouSpanL = min(SenkouSpanA[displacement - 1], SenkouSpanB[displacement - 1])
ChikouSpan = close[displacement-1]

Sema = ema(close, 13)
Mema = ema(close, 21)
Lema = ema(close, 89)
XLema = ema(close, 233)

plot(Sema, color=blue, title="13 EMA", linewidth = 2)
plot(Mema, color=fuchsia, title="21 EMA", linewidth = 1)
plot(Lema, color=orange, title="89 EMA", linewidth = 2)
plot(XLema, color=teal, title="233 EMA", linewidth = 2)
plot(KijunSen, color=maroon, title="Kijun Sen", linewidth = 3)
plot(close, offset = -displacement, color=lime, title="Chikou Span", linewidth = 2)
sa=plot (SenkouSpanA, offset = displacement, color=green,  title="Senkou Span A", linewidth = 1)
sb=plot (SenkouSpanB, offset = displacement, color=red,  title="Senkou Span B", linewidth = 3)
fill(sa, sb, color = SenkouSpanA > SenkouSpanB ? green : red)

longCondition = (rsi(close, 12)>rsi(close, 24)) and close>ChikouSpan and Sema>KijunSen
strategy.entry("Long",strategy.long,when = longCondition)

strategy.close("Long", when = (rsi(close, 12)<rsi(close, 24) and (close<KijunSen and close<ChikouSpan)))

shortCondition = (rsi(close, 12)<rsi(close, 24)) and close<ChikouSpan and Sema<KijunSen
strategy.entry("Short",strategy.short, when = shortCondition)

strategy.close("Short", when = (rsi(close, 12)>rsi(close, 24) and (close>KijunSen and close>ChikouSpan)))
```

> Detail

https://www.fmz.com/strategy/439206

> Last Modified

2024-01-18 12:32:46
