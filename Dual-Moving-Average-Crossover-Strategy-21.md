
> Name

Based on the dual-moving average breakthrough strategy Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/7a5025622e3b3d9002.png)
[trans]
### Overview
This strategy visualizes areas of price movement by calculating and plotting a 20-period simple moving average (SMA) and a 21-period exponential moving average (EMA), and filling in color between them. A buy signal is generated when the price crosses above the 20-period SMA; a sell signal is generated when the price crosses below the 21-period EMA. This strategy has both trailing stop loss and take profit functions.
### Strategy Principles
The core idea of ​​the double moving average breakout strategy is to use the crossover between the fast moving average and the slow moving average as a buy and sell signal. The 20-period SMA is relatively more sensitive and can respond quickly to price changes; the 21-period EMA's response is slightly lagging but smoother. When the short-term and long-term trend directions are consistent, that is, when the two average lines cross upward or downward, it is judged that the trend has entered a strong stage, and the buying or selling decision made at this time has a greater winning rate.
Specifically, when the closing price crosses above the 20-period EMA, it means that the short-term and long-term are both upward trends, so go long; when the closing price crosses below the 21-period EMA, it means that both the short-term and long-term are downtrends, so go short. The closing signal is opposite to the entry signal. If the price falls below the 20-period SMA, long positions will be closed, and if the price breaks above the 21-period EMA, short positions will be closed.
This strategy also uses fill technology to fill in color between the two moving averages to form a visual indicator to assist in judging market trends.
### Strategic Advantages
The double moving average breakout strategy has the following advantages:
1. The principle is simple, easy to understand and implement;
2. It is more accurate to judge the market trend through the intersection of double lines;
3. Visual indicators intuitively display price fluctuation areas;
4. It has the function of tracking stop loss and stop profit, which can lock in profits and reduce risks;
5. It has strong scalability and can be optimized in various ways based on this strategy.
### Strategy Risk
There are also some risks with this strategy:
1. Wrong signals are easily generated in volatile market conditions;
2. Improper stop-loss and stop-profit settings may result in losses or reduced profits;
3. Improper parameter settings (such as cycle length) will affect the strategy effect;
4. Mechanized trading can easily lead to a series of losses.
In response to the above risks, the following measures can be taken to deal with them:
1. Add filtering conditions to avoid entering the market during the shock period;
2. Optimize stop-loss and take-profit parameters to balance risk and return;
3. Test the robustness of parameters and select indicator parameters suitable for the market;
4. Manually intervene in abnormal situations to avoid continuous losses.
### Strategy optimization
This strategy can be optimized from the following aspects:
1. Add other technical indicator filters, such as trading volume, volatility and other indicators, to avoid false breakthroughs;
2. Dynamically optimize moving average parameters based on machine learning methods;
3. Combine sentiment indicators, news, etc. to improve decision-making effects;
4. Add an adaptive stop loss mechanism to adjust the stop loss range according to market changes.
### Summarize
This strategy uses the intersection of fast and slow double moving averages to judge market trend changes and make buying and selling decisions accordingly. This strategy has the advantages of being simple, intuitive, and easy to implement, but it also has certain risks. Through parameter optimization, adding filter conditions, manual intervention, etc., risks can be reduced and strategy effects improved. This strategy has a large space for expansion and is worthy of in-depth research and application.
||

### Overview  

This strategy calculates and plots the 20-period simple moving average (SMA) and 21-period exponential moving average (EMA), fills the color between them to visualize the price fluctuation zone. It generates buy signals when the price crosses above the 20-period SMA and sell signals when the price crosses below the 21-period EMA. The strategy also has trailing stop loss and take profit functions.  

### Strategy Logic

The core idea of the dual moving average crossover strategy is to use the crossovers between fast and slow moving averages as trading signals. The 20-period SMA responds faster to price changes while the 21-period EMA is slightly lagging but smoother. When the short-term and long-term trends are consistent, i.e. the two moving averages crossover up or down, it indicates the trend is strengthening and the trading decisions made will likely be more profitable.  

Specifically, when the closing price crosses above the 20-period SMA, it indicates that both short-term and long-term are in uptrends, so go long. When the closing price crosses below the 21-period EMA, it indicates that both short-term and long-term are in downtrends, so go short. The exit signals are opposite of the entry signals. For example, when price drops below the 20-period SMA, close long positions. When price crosses back above the 21-period EMA, close short positions.

The fill technique is also used to fill color between the two moving averages to form a visual indicator to aid in judging market trends.  

### Advantages

The dual moving average crossover strategy has the following advantages:

1. Simple logic and easy to understand and implement;  
2. Crossovers of the two moving averages reliably indicate changes in trend direction;
3. Visual indicator intuitively displays price fluctuation levels;
4. Trailing stop loss and take profit locks in profits and reduces risks; 
5. High extensibility for various optimizations based on this strategy.

### Risks

There are also some risks with this strategy:  

1. Prone to whipsaws and generating false signals during range-bound periods;
2. Improper stop loss and take profit settings may lead to losses or reduced profits;
3. Inadequate parameter tuning (e.g. period lengths) may adversely affect strategy performance;  
4. Automated trading may trigger consecutive losses.

The following measures can be adopted to address the above risks:

1. Add filters to avoid entering during choppy periods;
2. Optimize stop loss and take profit parameters to balance risk-return;
3. Test parameter robustness and select appropriate parameters for the market;
4. Manually intervene during exceptional circumstances to prevent enlarged losses.
   
### Enhancement Opportunities 

The strategy can be improved in the following aspects:

1. Add other technical indicator filters, such as volume and volatility, to avoid false breakouts;  
2. Dynamically optimize moving average parameters based on machine learning;
3. Incorporate sentiment and news analytics to improve decisions;  
4. Build in adaptive stop loss mechanism to adjust stop loss scale based on market conditions.

### Summary

This strategy identifies trend changes using crossovers between fast and slow moving averages, and makes corresponding long and short decisions. It has advantages like simplicity, intuitiveness and ease of implementation, but also bears some risks. The risks can be reduced and performance improved via parameter optimization, adding filters, manual oversight etc. The strategy has great extensibility and is worth in-depth research and application.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-27 00:00:00
end: 2024-02-26 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("BMSB Breakout Strategy", shorttitle="BMSB Breakout", overlay=true)

source = close
smaLength = 20
emaLength = 21

sma = ta.sma(source, smaLength)
ema = ta.ema(source, emaLength)

outSma = request.security(syminfo.tickerid, timeframe.period, sma)
outEma = request.security(syminfo.tickerid, timeframe.period, ema)

smaPlot = plot(outSma, color=color.new(color.red, 0), title='20w SMA')
emaPlot = plot(outEma, color=color.new(color.green, 0), title='21w EMA')

fill(smaPlot, emaPlot, color=color.new(color.orange, 75), fillgaps=true)

// Definir condiciones para la estrategia de compra y venta
buyCondition = ta.crossover(close, outSma)
sellCondition = ta.crossunder(close, outEma)

// Entrada larga (compra) y salida corta
strategy.entry("Long", strategy.long, when=buyCondition and not na(sellCondition))
strategy.close("Short", when=buyCondition)

// Entrada corta (venta) y salida larga
strategy.entry("Short", strategy.short, when=sellCondition and not na(buyCondition))
strategy.close("Long", when=sellCondition)

// Puedes ajustar la configuración de la estrategia y los valores predeterminados según tus preferencias

plotshape(series=buyCondition, location=location.belowbar, color=color.green, style=shape.triangleup, title="Buy Signal")
plotshape(series=sellCondition, location=location.abovebar, color=color.red, style=shape.triangledown, title="Sell Signal")

```

> Detail

https://www.fmz.com/strategy/442921

> Last Modified

2024-02-27 13:51:51
