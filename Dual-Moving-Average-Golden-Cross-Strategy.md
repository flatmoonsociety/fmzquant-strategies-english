
> Name

Dual-Moving-Average-Golden-Cross-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/43f0a20be222166b8b843f6997c4b3214f0e031503178c55dcd0b3ed2a00c24c.png)
 [trans]

## Overview
The double moving average golden cross strategy is a quantitative trading strategy based on moving averages. This strategy determines market trends and buying and selling opportunities by calculating moving averages of different periods. When the short-term moving average crosses the long-term moving average, a golden cross is generated, which is a buy signal; when the short-term moving average crosses below the long-term moving average, a death cross is generated, which is a sell signal.
## Strategy Principle
The core logic of the Double Moving Average Golden Cross strategy is based on the smoothing properties of moving averages. Moving averages can effectively filter out market noise and indicate the general trend direction. The short-term moving average is more sensitive to price changes and can capture price fluctuation information in the recent period; while the long-term moving average responds slowly to recent price changes and can reflect the long-term market trend. When the short-term moving average crosses the long-term moving average, it means that the market is forming a new upward trend; when the short-term moving average crosses below the long-term moving average, it means that the rising trend may end and you need to consider leaving the market.
Another key point of the dual moving average strategy is the RSI indicator. RSI can effectively determine whether the market is overbought or oversold. Combined with RSI, you can avoid false trades near market turning points. This strategy will only generate buy and sell signals if the RSI indicator meets the conditions.
Specifically, the trading decision logic of this strategy is as follows:
1. Calculate 20-period, 50-period and 100-period moving averages
2. Determine whether the 20-period moving average crosses the 50-period and 100-period moving averages. If so, it may enter a trend upward stage.
3. Also check whether the RSI indicator is less than 50, indicating that it has not entered the overbought area.
4. When the above three conditions are met at the same time, a buy signal is generated
5. Determine whether the 20-period moving average falls below the 50-period and 100-period moving averages. If so, it may enter a trend downward stage.
6. Also check whether the RSI indicator exceeds 48.5, indicating that it has not entered the oversold area.
7. When the above three conditions are met at the same time, a sell signal is generated
Through the combination of multiple parameters, this strategy can effectively filter out false signals and improve the accuracy of trading decisions.
## Strategic Advantages
The double moving average golden cross strategy has the following advantages:
1. The strategy is simple and clear, easy to understand and implement
2. Parameter optimization is flexible and the period of the moving average can be adjusted to adapt to different markets.
3. The combined use of moving averages and RSI indicators can effectively filter noise and evaluate the actual market trend.
4. Backtest data shows that this strategy has stable returns and small retracements.
5. Strategy parameters can be further optimized by integrating advanced technologies such as machine learning
## Strategy Risk
The double moving average golden cross strategy also has the following risks:
1. When the market fluctuates violently, the moving average lags behind and may miss the best buying and selling point.
2. The strategy relies on parameter optimization. If the parameters are set improperly, it will greatly affect the strategy returns.
3. During long-term operation, the market structure may change, and the moving average and RSI parameters need to be adjusted.
4. Mechanized trading strategies tend to concentrate positions and are more risky when the market turns.
To reduce risks, you can optimize from the following aspects:
1. Combine with volatility indicators and other indicators to evaluate the frequency and amplitude of market fluctuations, and dynamically adjust the moving average cycle
2. Add a machine learning model to dynamically optimize parameters
3. Set stop-loss and stop-profit conditions to avoid excessive losses in a single transaction
4. Adopt a position management system to adjust the position size according to market conditions and reduce the risk of concentrated positions.
## Strategy optimization direction
There is room for further optimization of the double moving average golden cross strategy:
1. Add other indicators to filter signals, such as trading volume, Bollinger Bands, etc., to improve the stability of the strategy
2. Use machine learning to dynamically optimize parameters to make the strategy more intelligent.
3. Design an adaptive moving average cycle setting plan and adjust parameters according to changes in market structure
4. Combined with the advanced risk management system, dynamically adjust positions and reduce strategic risks
5. Construct algorithmic trading portfolios and integrate multiple trading strategies to improve stability
## Summarize
The double moving average golden cross strategy is a very classic rule-based quantitative trading strategy. It is simple and easy to implement, has flexible parameter optimization, and excellent income performance. It is a good choice for beginners to get started with quantitative trading. However, this strategy also has certain limitations. Through further research and optimization, it can move towards higher intelligence and stability, and truly achieve sustained profitability.
||

## Overview

The Dual Moving Average Golden Cross strategy is a quantitative trading strategy based on moving averages. By calculating moving averages of different periods, it judges market trends and trading opportunities. When the short-term moving average crosses above the long-term moving average, a golden cross is formed as a buy signal. When the short-term moving average crosses below the long-term moving average, a death cross is formed as a sell signal.

## Strategy Logic  

The core logic of the Dual Moving Average Golden Cross strategy lies in the smoothing characteristics of moving averages. Moving averages can effectively filter market noise and indicate general trend directions. The short-term moving average is more sensitive to price changes, capturing price fluctuation information over the recent period. The long-term moving average responds more slowly to recent price changes, reflecting the long-term trend of the market. When the short-term moving average crosses above the long-term moving average, it indicates the market is forming a new uptrend. When the short-term moving average crosses below the long-term moving average, it suggests the uptrend may be ending and one should consider exiting positions.

Another key point of the dual moving average strategy is the RSI indicator. RSI can effectively determine whether the market is in overbought or oversold status. By incorporating RSI, it avoids generating wrong trading signals around market turning points. This strategy will only generate buy and sell signals when RSI meets the criteria.

Specifically, the trading logic is as follows:

1. Calculate the 20-, 50-, and 100-period moving averages  
2. Check if the 20-period moving average crosses above the 50- and 100-period moving averages, indicating a potential uptrend
3. Also check if RSI is below 50, suggesting not in overbought status
4. If all 3 criteria are met, generate a buy signal
5. Check if the 20-period moving average crosses below the 50- and 100-period moving averages, indicating a potential downtrend
6. Also check if RSI exceeds 48.5, suggesting not in oversold status
7. If all 3 criteria are met, generate a sell signal

By combining multiple parameters, this strategy can effectively filter false signals and improve accuracy of trading decisions.  

## Advantages

The Dual Moving Average Golden Cross strategy has the following advantages:

1. The strategy logic is simple and clear, easy to understand and implement
2. The parameters are flexible for optimization by adjusting moving average periods to fit different markets
3. The combination of moving averages and RSI can effectively filter noise and evaluate real market trends  
4. Backtests show this strategy offers steady returns and smaller drawdowns
5. The strategy can be further optimized with machine learning and other advanced techniques

## Risks

The risks associated with this strategy include:

1. Moving averages may lag during violent market swings, missing best entry and exit points
2. Strategy performance depends heavily on parameter optimization 
3. Market regime changes over long term may necessitate adjustment of parameters
4. Mechanical trading systems can result in concentrated positions and higher risk around turning points

To mitigate risks, optimizations can be made in the following aspects:  

1. Incorporate volatility metrics to dynamically adjust moving average periods based on market fluctuation frequency and magnitude
2. Add machine learning models to dynamically optimize parameters
3. Set stop loss limits to contain downside on individual trades 
4. Adopt position sizing schemes to reduce risks associated with concentrated positions 

## Enhancement Opportunities

There is room for further enhancement for the Dual Moving Average Golden Cross strategy:

1. Incorporate additional filters like volume, Bollinger Bands to improve stability
2. Apply machine learning techniques to auto-tune parameters and increase adaptiveness 
3. Design adaptive schemes for adjusting moving average periods based on evolving market landscapes
4. Incorporate advanced risk management systems to dynamically size positions to match risk appetite
5. Construct algos ensemble systems with multiple models to improve robustness

## Conclusion

The Dual Moving Average Golden Cross strategy is a classic rule-based quantitative trading strategy. It’s easy to implement with flexible parameter tuning and good backtested results. It serves as a great starting point for novice quants. However, it has some intrinsic limitations. With further research and optimization, it can be enhanced into more intelligent and stable systems for sustained profitability.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-09 00:00:00
end: 2024-01-16 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Based on Larry Connors RSI-2 Strategy - Lower RSI
strategy(title="EA_3Minute_MagnetStrat", shorttitle="EA_3Minute_MagnetStrat", overlay=false)
src = close, 
//RSI CODE
up = rma(max(change(src), 0), 30)
down = rma(-min(change(src), 0), 30)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
//Criteria for Moving Avg rules
ma20= vwma(close,20)
ma50 = vwma(close,50)
ma100= vwma(close,100)

//Rule for RSI Color
//col = ma30 > ma50 > ma200 and rsi <=53?lime: ma50 < ma200  and rsi >= 60?red : silver
long1 = ma20 > ma50 and ma50 > ma100 and rsi < 50 
short1 = ma20 < ma50 and ma50 < ma100 and rsi > 48.5 
//plot(rsi, title="RSI", style=line, linewidth=1,color=col)
//plot(100, title="Upper Line 100",style=line, linewidth=3, color=aqua)
//plot(0, title="Lower Line 0",style=line, linewidth=3, color=aqua)

//band1 = plot(60, title="Upper Line 60",style=line, linewidth=1, color=aqua)
//band0 = plot(44, title="Lower Line 40",style=line, linewidth=1, color=aqua)
//fill(band1, band0, color=silver, transp=90)
//strategy.entry ("buy", strategy.long, when=long)
//strategy.entry ("sell", strategy.short, when=short)
//plot(long,"long",color=green,linewidth=1)
//plot(short,"short",color=red,linewidth=1)
//
long = long1[1] == 0 and long1 == 1
short = short1[1] == 0 and short1 == 1
longclose = long[3] == 1
shortclose = short[3] == 1

//Alert

strategy.entry("short", strategy.short,qty = 1, when=short)
strategy.entry("long", strategy.long,qty=1, when=long)
plot(long,"long",color=green,linewidth=1)
plot(short,"short",color=red,linewidth=1)
strategy.close("long",when=longclose)
strategy.close("short",when=shortclose)

//strategy.exit(id="long",qty = 100000,when=longclose)
//strategy.exit(id="short",qty = 100000,when=shortclose)
plot(longclose,"close",color=blue,linewidth=1)
plot(shortclose,"close",color=orange,linewidth=1)
//strategy.exit(id="Stop", profit = 20, loss = 100)
```

> Detail

https://www.fmz.com/strategy/439103

> Last Modified

2024-01-17 17:38:36
