
> Name

Hawk-Eye-Short-term-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Overview
The Eagle Eye short-term trading strategy is a short-term trading strategy that combines a variety of technical indicators. This strategy uses indicators such as moving average, MACD, RSI, stoch and vwma to construct trading signals and conduct short-term operations within a 1-hour time period.
## Strategy Principle
The strategy first calculates the fast moving average (21 periods) and the slow moving average (55 periods). When the fast line crosses the slow line and MACD turns from negative to positive, a buy signal is generated. When the fast line crosses the slow line and MACD turns from positive to negative, a sell signal is generated. In addition, the strategy also incorporates the RSI indicator to filter signals. A buy signal is generated only when the RSI is low and upward. A sell signal is generated when the RSI is high and downward. Finally, this strategy also introduces the position of the vwma indicator to compare the fast and slow moving averages to further confirm the trend.
Specifically, a buy signal is generated when MACD turns from negative to positive, the small moving average crosses the large moving average and the 50-period VWMA is lower than the 200-period VWMA. A sell signal is generated when MACD turns from positive to negative, the small moving average crosses below the large moving average and the 50-period VWMA is higher than the 200-period VWMA. Buy when the fast line of the Stoch indicator is higher than the slow line. Sell ​​when the fast line of the Stoch indicator is below the slow line.
## Advantage Analysis
The biggest advantage of this strategy is that multiple indicators combine to filter signals, which can effectively reduce the probability of wrong transactions. MACD determines the trend direction, VWMA determines the main trend position, Stoch filters out overbought and oversold areas, and RSI avoids overshooting areas. The combined use of multiple indicators makes trading signals more reliable. This multi-indicator combination strategy not only ensures the quality of trading signals, but also controls the problem of excessive trading.
In addition, short-term operations in a 1-hour period can seize short-term opportunities in the market and achieve higher profits. Compared with long-term trading, short-term trading has a higher winning rate.
## Risk Analysis
The biggest risk with this strategy is that the multi-indicator combination may be too complex. Improper setting of indicator parameters may lead to poor strategy performance. In order to ensure the effect, a large amount of backtesting is required to optimize the indicator parameters.
In addition, short-term trading has a higher trading frequency. Too frequent transactions not only increase transaction costs, but also increase operational risks. If you cannot continue to mark the market, you may not be able to enter and exit in time.
Finally, multi-index combination increases the risk of strategy curve fitting. The optimization process may cause over-optimization problems, resulting in poor real-time results.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize indicator parameters and find the best parameter combination.
2. Add stop-loss strategies to reduce single losses.
3. Optimize entry conditions and improve the accuracy of trend judgment.
4. Combined with position management, optimize the efficiency of fund use.
5. Test the effects of different types of contracts.
6. Add machine learning algorithms and use historical data for training to reduce the risk of over-fitting.
## Summarize
The Eagle Eye short-term trading strategy combines multiple indicators to construct trading signals and performs short-term operations in a 1-hour period. The advantage of this strategy is that the indicator combination is reliable and the winning rate is high. However, there are also risks such as difficulty in parameter optimization and high transaction frequency. Overall, this strategy has a very large room for optimization, and if the parameters are adjusted properly, the effect will be excellent. Through continuous optimization and testing, this strategy can become a very practical short-term trading strategy.

||

## Overview

The Hawk Eye short-term trading strategy is a short-term trading strategy that combines multiple technical indicators. The strategy uses indicators like moving averages, MACD, RSI, Stoch, and VWMA to construct trading signals and make short-term trades within a 1-hour timeframe.

## Strategy Logic

The strategy first calculates the fast moving average (21 periods) and slow moving average (55 periods). When the fast MA crosses above the slow MA, and MACD turns from negative to positive, a buy signal is generated. When the fast MA crosses below the slow MA, and MACD turns from positive to negative, a sell signal is generated. In addition, the strategy also incorporates the RSI indicator to filter signals. Buy signals are only generated when RSI is low and turning up. Sell signals are only generated when RSI is high and turning down. Finally, the strategy also utilizes VWMA to compare the positions of the fast and slow moving averages to further confirm the trend. 

Specifically, when MACD turns from negative to positive, the fast MA crosses above the slow MA, and 50-period VWMA is below 200-period VWMA, a buy signal is generated. When MACD turns from positive to negative, the fast MA crosses below the slow MA, and 50-period VWMA is above 200-period VWMA, a sell signal is generated. The strategy buys when the fast Stoch is above the slow Stoch, and sells when the fast Stoch is below the slow Stoch.

## Advantage Analysis 

The biggest advantage of this strategy is the combination of multiple indicators to filter signals, which can effectively reduce the probability of wrong trades. MACD determines trend direction, VWMA judges major trend location, Stoch filters overbought/oversold zones, and RSI avoids overshoot areas. The combination of multiple indicators makes trading signals more reliable. The use of multiple indicators ensures signal quality while controlling excessive trading.

In addition, short-term trading within the 1-hour timeframe can capture short-term opportunities in the market and achieve higher profits. Compared to long-term trading, short-term trading has a higher win rate.

## Risk Analysis

The biggest risk of this strategy is that the combination of multiple indicators may be too complex. Improper parameter settings can lead to poor strategy performance. Extensive backtesting and optimization is needed to ensure good results.

In addition, short-term trading has higher trading frequency. Excessively frequent trading not only increases transaction costs but also increases operational risks. Failure to monitor the market continuously may result in missed entries and exits. 

Finally, the combination of multiple indicators increases the risk of curve fitting. The optimization process may lead to overfitting issues and poor performance in live trading.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize indicator parameters to find the best parameter combination.

2. Add stop loss strategies to reduce single trade loss. 

3. Optimize entry conditions to improve accuracy in judging trends.

4. Incorporate position sizing to optimize capital usage efficiency.

5. Test the effectiveness across different products and contracts.

6. Add machine learning algorithms that utilize historical data for training and reduce overfitting risks.

## Summary 

The Hawk Eye short-term trading strategy combines multiple indicators to construct trading signals and makes short-term trades within the 1-hour timeframe. The advantages of this strategy are reliable indicator combinations and high win rate. But there are also risks like difficulty in parameter optimization and high trading frequency. Overall, this strategy has great optimization potential. With proper parameter tuning, the performance can be very impressive. Through continuous optimization and testing, this strategy can become a very practical tool for short-term trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|fastLength|
|v_input_2|55|slowlength|
|v_input_3|8|MACDLength|
|v_input_4|5|smoothK|
|v_input_5|5|smoothD|
|v_input_6|8|lengthRSI|
|v_input_7|21|lengthStoch|
|v_input_8_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-15 00:00:00
end: 2023-09-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Hawk 1H Strategy", overlay=true)

fastLength = input(21)
slowlength = input(55)
MACDLength = input(8)
smallEMA = ema(close, fastLength)
largeEMA = ema(close, slowlength)
MACD = smallEMA - largeEMA
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD

smoothK = input(5, minval=1)
smoothD = input(5, minval=1)
lengthRSI = input(8, minval=1)
lengthStoch = input(21, minval=1)
src = input(close, title="RSI Source")
vFast = stoch(close, high, low, 8)
vSlow = sma(vFast, 5)
rsi1 = rsi(src, lengthRSI)
k = sma(stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK)
d = sma(k, smoothD)

fiftyVWMA = vwma(close, 55)
twohunVWMA = vwma(close,144)


if (MACD > MACD[1]) and (MACD[1] > MACD[2]) and (fiftyVWMA < twohunVWMA)
    if (vFast > vSlow) and (k < 30) //and (vSlow < 40)
        strategy.entry("MacdLE", strategy.long, comment='Buy')
        
if (MACD < MACD[1]) and (MACD[1] < MACD[2]) and (fiftyVWMA > twohunVWMA)
    if (vFast < vSlow) and (k > 70)//and (vSlow > 60)//and (rsi1 > 60)
        strategy.entry("MacdSE", strategy.short, comment='Sell')


    



//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/427574

> Last Modified

2023-09-22 12:09:01
