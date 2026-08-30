
> Name

Triple-EMA-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is modified based on SoftKill21's Amazing scalper for majors with risk management strategy, using a triple exponential moving average instead of the original simple moving average to reduce lag. This strategy is suitable for the 1-minute period of major currency pairs, using trend following methods to conduct buying and selling operations based on the golden crosses and dead crosses of fast EMA, standard EMA and slow EMA. At the same time, position size is determined based on London and New York trading hours and risk management principles.
## Strategy Principle
This strategy uses three exponential moving averages with different periods: 25-period fast EMA, 50-period standard EMA, and 100-period slow EMA. When the fast EMA crosses the standard EMA and the slow EMA, a buy signal is generated; when the fast EMA crosses the standard EMA and the slow EMA, a sell signal is generated. To reduce lag, the EMA is calculated using a quadratic exponential smoothing technique. The strategy also determines whether entry conditions are met based on the opening times of London and New York sessions. Additionally, the strategy uses a fixed percentage of account equity to determine the position size for each order to control risk.
Specifically, the strategy first calculates three EMA lines, and then determines whether the fast EMA forms a golden cross or a dead cross with the standard EMA and slow EMA. If the conditions that match the opening time of the London or New York session are met at the same time, a buy or sell signal is generated. When determining the position size, the strategy first calculates a fixed percentage of the account equity as the risk exposure, and then converts it into the number of contracts and standard lots, thereby dynamically adjusting the position of each order.
## Advantage Analysis
This strategy has the following advantages:
1. Using triple EMA can effectively smooth price data and identify trend directions. The fast EMA is sensitive to price changes, the standard EMA tracks stably, and the slow EMA filters out noise. Used together, the three can filter out false breakthroughs and determine the trend direction.
2. Apply quadratic exponential smoothing technology to calculate EMA to reduce hysteresis and make the signal more sensitive.
3. Combine with the main trading hours to avoid misleading signals during non-main trading hours.
4. Adopt risk management principles and adjust positions based on account equity. Avoid the impact of a single large loss on your account.
5. The strategy logic is simple and clear, easy to understand and implement, and suitable for novices to learn.
6. It can be optimized and adjusted for different currency pairs and time periods, and has a wide range of applications.
## Risk Analysis
There are also some possible risks with this strategy:
1. EMA cannot effectively filter short-term false breakthroughs caused by emergencies, and may produce false signals. It is recommended to combine analysis and filtering with other indicators.
2. Fixed percentage positions cannot dynamically adjust to market fluctuations, and there is a problem of too large or too small positions. You can consider introducing indicators such as volatility to dynamically adjust positions.
3. Only considering the two main trading periods, you may miss trading opportunities in other periods. You can test the effects of different time periods.
4. Without a stop-loss mechanism, unilateral losses cannot be effectively controlled. You can set a trailing stop or a time stop.
5. The EMA crossover has a certain lag, and the best entry opportunity may be missed. Consider lowering the EMA period or combining it with other leading indicators.
6. Effectiveness may be affected by transaction costs. It is recommended to adjust the stop loss and take profit positions appropriately.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test different EMA cycle parameters and find the optimal parameter combination. Technologies such as adaptive EMA can be introduced to dynamically optimize the EMA cycle.
2. Add other filtering indicators, such as RSI, Bollinger Bands, etc., to improve the quality of signals.
3. Introduce a dynamic position management mechanism to adjust positions according to market volatility and profitability.
4. Add trailing stop loss and time stop loss to limit losses. Adjust the stop loss point appropriately.
5. Test different trading sessions to find the best trading time. Periods can be filtered by combining indicators such as volatility.
6. Optimize the take-profit and stop-loss levels to balance the profit size and winning rate. Introduce smart stops such as parabolic stop losses.
7. Try to modify and improve the EMA calculation method, such as linear weighted EMA, etc., to reduce the lag.
8. Combine with automatic machine learning methods to find optimal parameters.
9. Model transaction costs and adjust the system to maximize net profit.
Through the above optimization, the profitability of the system can be improved, drawdowns can be controlled, and the scope of application can be expanded, thereby obtaining a more powerful and stable trading strategy.
## Summarize
The overall idea of ​​this strategy is clear. It uses triple EMA to identify trends, operates in conjunction with the main trading periods, and uses account ratios to determine positions. It is a typical trend following strategy. There is a large space for strategy optimization. Through parameter optimization, mechanism improvement, technology introduction and other means, the applicability of the strategy can be further expanded in more markets and the robustness of the strategy can be improved. As a newbie learning to mortise and tenon, this strategy is a great place to start. Through learning and improvement, you can improve your understanding of quantitative trading systems. If handled properly, this strategy can be transformed into a mature and reliable quantitative strategy.
|| 

## Overview

This strategy is modified from SoftKill21's Amazing scalper for majors with risk management by using triple exponential moving averages instead of simple moving averages to reduce lag. It is suitable for major currency pairs at 1-minute timeframe, adopting trend following approach based on golden cross and death cross of fast EMA, standard EMA and slow EMA. It also incorporates London and New York sessions and risk management principles to determine position sizing.

## Strategy Logic

The strategy uses three EMAs with different periods: 25-period fast EMA, 50-period standard EMA and 100-period slow EMA. When fast EMA crosses over standard EMA and slow EMA, it generates buy signal. When fast EMA crosses below standard EMA and slow EMA, it generates sell signal. To reduce lag, EMAs are calculated using double exponential smoothing technique. The strategy also checks if open market times of London or New York sessions match the entry conditions. In addition, position sizing of each order is determined dynamically by using a fixed percentage of account equity to control risk.

Specifically, the strategy first calculates the three EMA lines, then checks if fast EMA forms golden cross or death cross with standard EMA and slow EMA. If the condition also matches London or New York open market times, buy or sell signals are generated. When determining position size, the strategy calculates fixed percentage of account equity as risk exposure, then converts it to contract size and round lots to adjust position dynamically for each order.

## Advantage Analysis 

The strategy has the following advantages:

1. The triple EMAs can effectively smooth price data and identify trend direction. Fast EMA is sensitive to price changes, standard EMA steadily tracks, and slow EMA filters noise. Used together, they can filter false breakouts and determine trend direction.

2. The use of double exponential smoothing reduces lag and makes signals more sensitive. 

3. Incorporating major trading sessions avoids misleading signals during off-peak hours.

4. The risk management approach adjusts position size based on account equity, avoiding excessive loss on single trades.

5. The logic is simple and clear, easy to understand and implement, suitable for beginners.

6. The strategy can be optimized and adjusted for different currency pairs and timeframes, with wide applicability.

## Risk Analysis

The strategy also has some potential risks:

1. EMAs cannot effectively filter short-term false breakouts caused by sudden events, which may generate wrong signals. Other indicators may be added to filter and analyze.

2. Fixed percentage position sizing cannot dynamically adjust to market volatility, leading to over- or under-sized positions. Dynamic position sizing based on volatility can be considered.

3. Only two major sessions are considered, which may miss trading opportunities in other sessions. Effects of different sessions can be tested.

4. Lack of stop loss mechanism results in inability to effectively control one-sided loss. Moving or time-based stop loss can be implemented.

5. EMA crossovers have some lag and may miss best entry timing. Reducing EMA periods or incorporating leading indicators can help.

6. Performance may be affected by transaction costs. Stop loss and take profit levels should be adjusted accordingly.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Test different EMA period parameters to find optimal combinations. Adaptive EMAs can be introduced to dynamically optimize periods.

2. Add other filtering indicators like RSI, Bollinger Bands to improve signal quality.

3. Introduce dynamic position sizing based on market volatility and profitability. 

4. Add moving or time stop loss to limit losses. Fine tune stop loss levels.

5. Test different trading sessions to find the optimal times. Volatility measures can help screening.

6. Optimize take profit and stop loss levels to balance profit size and win rate. Introduce intelligent stops like parabolic SAR.

7. Try modifying EMA calculation like linear weighted EMA to reduce lag.

8. Employ machine learning to find optimal parameters.

9. Model transaction costs and adjust system for maximum net profit.

Through the above optimizations, the system's profitability can be improved, drawdowns controlled, applicability expanded, to obtain a more powerful and robust trading strategy.

## Summary

The overall logic of this strategy is clear, using triple EMAs to identify trends, combining with major sessions for execution, and adopting position sizing based on account percentage. It belongs to a typical trend following system. There is large room for optimization via parameter tuning, mechanism improvements, technology introduction etc. to further expand its applicability across more markets and improve robustness. As a learning 웽e for beginners, it provides a good starting point. With practice and enhancements, it can transform into a mature and reliable quantitative strategy.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|Length|
|v_input_2|50|Length|
|v_input_3|100|Length|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|50|TP|
|v_input_6|100|SL|
|v_input_7|true|Trade london session?|
|v_input_8|true|Trade new york session?|
|v_input_9|true|Risk % of equity |


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-19 00:00:00
end: 2023-09-26 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// original author SoftKill21
//@version=4
//@capam 

strategy(title="Triple EMA Scalper low lag strat", shorttitle="3EMA scalper", overlay=true)
strategy.initial_capital = 50000
len1 = input(25, minval=1, title="Length")
len2 = input(50, minval=1, title="Length")
len3 = input(100, minval=1, title="Length")

src = input(close, title="Source")
tmp1 = ema(src, len1)
tmp2 = ema(src, len2)
tmp3 = ema(src, len3)
fastemaOut = 2*tmp1 - ema(tmp1, len1)
standardemaOut = 2*tmp2 - ema(tmp2, len2)
slowemaOut = 2*tmp3 - ema(tmp3, len3)
//fastemaOut = sma(src, len1)
//standardemaOut = sma(src, len2)
//slowemaOut = sma(src, len3)

plot(fastemaOut, color=color.black, title="First EMA")
plot(standardemaOut, color=color.yellow, title="Second EMA")
plot(slowemaOut, color=color.blue, title="Third EMA")


timeinrange(res, sess) => time(res, sess) != 0


londopen = timeinrange(timeframe.period, "0300-1100") 
nyopen = timeinrange(timeframe.period, "0800-1600") 

longCondition = crossover(fastemaOut,standardemaOut) and crossover(fastemaOut,slowemaOut) and londopen //or nyopen)
shortCondition = crossunder(fastemaOut,standardemaOut) and crossunder(fastemaOut,slowemaOut) and londopen// or nyopen)

longCondition2 = crossover(fastemaOut,standardemaOut) and crossover(fastemaOut,slowemaOut) and nyopen
shortCondition2 = crossunder(fastemaOut,standardemaOut) and crossunder(fastemaOut,slowemaOut) and nyopen
tp = input(50,title="TP")
sl = input(100, title="SL")

tradeLondon =  input(title="Trade london session?", type=input.bool, defval=true)
tradeNewyork = input(title="Trade new york session?", type=input.bool, defval=true)

//MONEY MANAGEMENT--------------------------------------------------------------
balance = strategy.netprofit + strategy.initial_capital //current balance
floating = strategy.openprofit          //floating profit/loss
risk = input(1,type=input.float,title="Risk % of equity ")/100           //risk % per trade
temp01 = balance * risk     //Risk in USD
temp02 = temp01/sl        //Risk in lots
temp03 = temp02*100000      //Convert to contracts
size = temp03 - temp03%1000 //Normalize to 1000s (Trade size)
if(size < 1000)
    size := 1000        

if(tradeLondon==true)
    strategy.entry("long",1,when=longCondition)
    strategy.exit("tp/sl","long",profit=tp,loss=sl)
    
    strategy.entry("short",0,when=shortCondition)
    strategy.exit("tp/sl","short",profit=tp,loss=sl)

if(tradeNewyork==true)
    strategy.entry("long",1,when=longCondition2)
    strategy.exit("tp/sl","long",profit=tp,loss=sl)
    
    strategy.entry("short",0,when=shortCondition2)
    strategy.exit("tp/sl","short",profit=tp,loss=sl)

// strategy.risk.max_intraday_filled_orders(2) 
```

> Detail

https://www.fmz.com/strategy/428000

> Last Modified

2023-09-27 17:19:26
