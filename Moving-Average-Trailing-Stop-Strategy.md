
> Name

Moving-Average-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy generates buy signals through the intersection of the fast EMA buying moving average and the slow SMA selling moving average, and uses ATR to dynamically track the stop loss to achieve risk control, aiming to surpass the buy and hold strategy with a small number of transactions.
## Strategy Principle
1. Calculate the fast EMA buying moving average and the slow SMA buying moving average. When the fast line crosses the slow line and reaches a certain buying strength, a buying signal is generated.
2. Calculate the fast EMA selling moving average and the slow SMA selling moving average. When the fast line crosses the slow line, a selling signal is generated.
3. Use the N-day average of the ATR indicator multiplied by the multiple as a dynamic trailing stop to achieve risk control.
4. Start the strategy during backtesting and perform buy and sell executions.
5. Optimize different parameter combinations for each stock and find the best parameters.
This strategy combines the advantages of moving average indicators to judge trends and cross signals and ATR dynamic tracking stop loss, and adapts to the characteristics of each variety through parameter optimization. The goal is to obtain excess returns beyond buying and holding through a small number of precise transactions.
## Advantage Analysis
1. The intersection of fast EMA and slow SMA generates trading signals, which can identify trends.
2. ATR stop loss adjusts the stop loss position according to market fluctuations to effectively control risks.
3. Optimizing parameters for each stock can improve profitability.
4. Simple transaction logic and rules, easy to implement and verify.
5. The backtest function is complete and can verify the strategy effect.
6. Pursue stable excess returns beyond buying and holding.
## Risk Analysis
1. The optimized parameters may not be suitable for the future and may need to be re-optimized regularly.
2. EMA and SMA crossover may produce false signals or signal lags.
3. The ATR stop loss may be too aggressive, and the stop loss range can be appropriately relaxed.
4. If the trading frequency is too low, you may miss better trading opportunities.
5. The impact of transaction costs needs to be considered.
## Optimization direction
1. Continue to test different parameter combinations to find the optimal parameters.
2. Try to introduce other indicators for signal filtering.
3. Optimize the cycle parameters of ATR and balance the sensitivity of stop loss levels.
4. Evaluate the effect of appropriately widening the stop loss range.
5. Consider combining machine learning and other methods to automatically optimize parameters.
6. Study the effects of increasing the frequency of opening positions.
## Summarize
This moving average tracking stop loss strategy combines the advantages of moving average crossover signals and ATR stop loss control risk, and adapts to the characteristics of each stock through parameter optimization. It is a simple and practical overbought and hold strategy idea. Although the optimized parameters do not guarantee future results, the overall trading logic of this strategy is clear and highly operable. It is worthy of further improvement and verification and has very inspiring significance.
|| 

## Overview 

This strategy generates buy signals when fast EMA buy line crosses over slow SMA buy line, and uses ATR dynamic trailing stop for risk control. It aims to outperform buy and hold strategy with limited trades.

## Strategy Logic

1. Calculate fast EMA and slow SMA buy lines, generate buy signal when fast line crosses over slow line with certain buy strength.

2. Calculate fast EMA and slow SMA sell lines, generate sell signal when fast line crosses below slow line.

3. Use N day ATR average multiplied by coefficient as dynamic trailing stop for risk control.

4. Start strategy in backtest period for buy and sell execution.

5. Optimize parameters for each stock to find best values.

The strategy combines the advantages of MA crossing for signals and ATR trailing stop for risk control. Parameter optimization adapts to each product's characteristics, aiming for excess returns over buy and hold with precise trades.

## Advantage Analysis

1. Fast EMA and slow SMA crossovers identify trends and generate signals.

2. ATR stop adjusts based on market volatility, effectively controlling risks.

3. Optimizing for each stock improves profitability. 

4. Simple logic and rules, easy to implement and verify.

5. Complete backtest functionality to validate strategy.

6. Seeks steady outperformance over buy and hold.

## Risk Analysis

1. Optimized parameters may not work for future, periodic re-optimization may be needed.

2. EMA and SMA crosses may generate incorrect or lagging signals. 

3. ATR stop may be too aggressive, can loosen stop loss range.

4. Low trade frequency may miss good opportunities. 

5. Need to consider impact of trading costs.

## Optimization Directions

1. Continue testing different parameter combinations for optimum values.

2. Try introducing other indicators for signal filtering.

3. Optimize ATR period to balance stop loss sensitivity.

4. Evaluate effect of relaxing stop loss range.

5. Consider machine learning for automated parameter optimization. 

6. Study effect of increasing trade frequency.

## Summary
This moving average trailing stop strategy combines the strengths of MA crossovers for signals and ATR stops for risk control. Parameter optimization adapts it to each stock's characteristics. Although optimized parameters have no guarantee, the overall logic is simple and practical for outperforming buy and hold. Further improvements and verification are worthwhile, as the strategy has good inspirational value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2005|Start Year|
|v_input_2|true|Start Month|
|v_input_3|true|Start Day|
|v_input_4|2050|Stop Year|
|v_input_5|12|Stop Month|
|v_input_6|31|Stop Day|
|v_input_7|true|Background|
|v_input_8|12|Fast EMA Buy|
|v_input_9|54|Slow SMA Buy|
|v_input_10|52|Minimum Buy Strength|
|v_input_11|18|Fast EMA Sell|
|v_input_12|55|Slow SMA Sell|
|v_input_13|100|Minimum Sell Strength|
|v_input_14|8|Trailing Stop (#ATR)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
//created by XPloRR 04-03-2018

strategy("XPloRR MA-Trailing-Stop Strategy",overlay=true, initial_capital=1000,default_qty_type=strategy.percent_of_equity,default_qty_value=100)

testStartYear = input(2005, "Start Year")
testStartMonth = input(1, "Start Month")
testStartDay = input(1, "Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testStopYear = input(2050, "Stop Year")
testStopMonth = input(12, "Stop Month")
testStopDay = input(31, "Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)

testPeriodBackground = input(title="Background", type=bool, defval=true)
testPeriodBackgroundColor = testPeriodBackground and (time >= testPeriodStart) and (time <= testPeriodStop) ? #00FF00 : na
bgcolor(testPeriodBackgroundColor, transp=97)

ema1Period = input(12, "Fast EMA Buy")
sma1Period = input(54, "Slow SMA Buy")
strength1 = input(52, "Minimum Buy Strength")

ema2Period = input(18, "Fast EMA Sell")
sma2Period = input(55, "Slow SMA Sell")
strength2 = input(100, "Minimum Sell Strength")

delta = input(8, "Trailing Stop (#ATR)")

testPeriod() => true

ema1val=ema(close,ema1Period)
sma1val=sma(close,sma1Period)
ema1strength=10000*(ema1val-ema1val[1])/ema1val[1]

ema2val=ema(close,ema2Period)
sma2val=sma(close,sma2Period)
ema2strength=10000*(ema2val-ema2val[1])/ema2val[1]

plot(ema1val,color=blue,linewidth=1)
plot(sma1val,color=orange,linewidth=1)
plot(ema2val,color=navy,linewidth=1)
plot(sma2val,color=red,linewidth=1)

long=crossover(ema1val,sma1val) and (ema1strength > strength1) 
short=crossunder(ema2val,sma2val) and (ema2strength < -strength2)

stopval=ema(close,6)
atr=sma((high-low),15)

inlong=0
buy=0
stop=0
if testPeriod()
    if (inlong[1])
        inlong:=inlong[1]
        buy:=close
        stop:=iff((stopval>(stop[1]+delta*atr)),stopval-delta*atr,stop[1])
    if (long) and (not inlong[1])
        strategy.entry("buy",strategy.long)
        inlong:=close
        buy:=close
        stop:=stopval-delta*atr
plot(buy,color=iff(close<inlong,red,lime),style=columns,transp=90,linewidth=1)
plot(stop,color=iff((short or (stopval<stop)) and (close<inlong),red,lime),style=columns,transp=60,linewidth=1)
if testPeriod()
    if (short or (stopval<stop)) and (inlong[1])
        strategy.close("buy")
        inlong:=0
        stop:=0
        buy:=0


```

> Detail

https://www.fmz.com/strategy/427305

> Last Modified

2023-09-19 21:33:48
