
> Name

Dual-Moving-Average-Tracking-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a63c08a89ffd505442.png)
[trans]

## Overview
This strategy calculates two moving averages with different parameters and generates a buy signal when the fast line crosses the slow line. At the same time, the average true fluctuation range is used to calculate the trailing stop price, and a sell signal is generated when the price falls below the stop price. This strategy can effectively track market trends and stop losses promptly after profits are made.
## Strategy Principle
1. Fast Moving Average (EMA): The parameter is the 12-day exponential moving average, which can quickly respond to price changes.
2. Slow Moving Average (SMA): The parameter is the 45-day simple moving average, which represents the mid- to long-term trend.  
3. When the fast moving average crosses the slow moving average, a buy signal is generated.
4. Calculate the 15-day average true range (ATR) as the stop loss benchmark.
5. Set the trailing stop loss range (such as 6 times ATR) based on the ATR value, and update the stop loss price in real time.
6. When the price is lower than the stop loss price, a sell signal is generated.
This strategy combines the advantages of trend tracking and stop loss management. It can not only track the medium and long-term direction, but also control single losses through stop loss.
## Advantage Analysis
1. The moving average combination can effectively identify trends and increase the reliability of signals.
2. Dynamic tracking stop loss can stop losses in time to avoid damaging financial strength.
3. Combine with ATR stop loss to make the stop loss price reasonable to prevent being too sensitive.
4. The strategy ideas are clear and easy to understand, and the parameters can be adjusted flexibly.
## Risk Analysis
1. The moving average lags behind and short-term opportunities may be missed.
2. Stop loss that is too loose will worsen profitability.
3. An overly sensitive stop loss will increase the frequency of transactions and the burden of handling fees.
4. Changes in stock volatility may affect the stability of ATR parameters.
You can appropriately optimize the moving average parameters, or adjust the ATR multiple to balance the stop loss range. You can also combine other indicators as filter conditions to improve entry timing.
## Optimization direction
1. Test more parameter combinations to choose the best moving average.
2. Adjust the multiple parameters of ATR stop loss according to the characteristics of different stocks.
3. Add filter conditions such as volume and price indicators to avoid unnecessary transactions.
4. Accumulate more historical data for testing to verify parameter stability.
## Summary
This strategy successfully integrates moving average trend tracking and ATR dynamic stop loss, and can adapt to different stock characteristics through parameter optimization. This strategy forms clear buy boundaries and stop loss boundaries, making the trading logic simple and clear. Generally speaking, this double moving average tracking stop loss strategy is stable, simple, and easy to optimize, and is suitable as a basic strategy for stock trading.
||

## Overview 
This strategy generates buy signals when the fast moving average crosses over the slow moving average. At the same time, it calculates the trailing stop loss price based on Average True Range to set sell signals. This strategy can effectively track market trends and cut losses in a timely manner when profit-taking.

## Principles
1. Fast Moving Average (EMA): 12-day Exponential Moving Average that responds quickly to price changes. 
2. Slow Moving Average (SMA): 45-day Simple Moving Average that depicts medium to long term trends.
3. Buy signals are generated when the fast MA crosses over the slow MA.  
4. The 15-day Average True Range (ATR) is calculated as the benchmark for stop loss.
5. Set the trailing stop loss amplitude based on ATR (e.g. 6 x ATR) and update stop price in real time.
6. Sell signals are generated when price drops below the stop loss price.  

This strategy combines the advantages of trend following and stop loss management. It can track medium to long term trends and control single trade loss through stop loss.

## Advantage Analysis
1. MA combos effectively identify trends and increase signal reliability. 
2. Dynamic trailing stop loss timely stops loss to avoid fund damages.
3. ATR-based stop loss makes stop price reasonable and prevents oversensitivity. 
4. The strategy logic is simple and parameters are flexible.

## Risk Analysis
1. MAs have lags that may miss short-term chances.  
2. Excessive loose stop loss undermines profitability.
3. Excessive tight stop loss increases trade frequency and commission fees.
4. Changing volatility may influence ATR parameter stability.  

Parameters can be optimized to balance stop loss amplitude. Other indicators can also be combined to improve entry timing.  

## Optimization Directions
1. Test more parameter combinations to find the optimal MAs.  
2. Adjust ATR multiplier according to specific stock characteristics. 
3. Add filtering conditions like volume indicators to avoid unnecessary trades.  
4. Accumulate more historical data to test parameter stability.  

## Conclusion
This strategy successfully combines MA’s trend following ability and ATR’s dynamic trailing stop loss. Parameters can be optimized to adapt to different stocks. It forms clear buy and sell boundaries, making logic simple and clear. In conclusion, this dual MA tracking stop loss strategy features stability, simplicity and ease of optimization. It works well as a fundamental strategy for stock trading.

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
|v_input_8|12|Exponential MA|
|v_input_9|45|Simple MA|
|v_input_10|12|Stop EMA|
|v_input_11|6|Trailing Stop #ATR|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-05 00:00:00
end: 2024-02-04 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
//created by XPloRR 24-02-2018

strategy("XPloRR MA-Buy ATR-MA-Trailing-Stop Strategy",overlay=true, initial_capital=1000,default_qty_type=strategy.percent_of_equity,default_qty_value=100)

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

emaPeriod = input(12, "Exponential MA")
smaPeriod = input(45, "Simple MA")
stopPeriod = input(12, "Stop EMA")
delta = input(6, "Trailing Stop #ATR")

testPeriod() => true

emaval=ema(close,emaPeriod)
smaval=sma(close,smaPeriod)
stopval=ema(close,stopPeriod)
atr=sma((high-low),15)

plot(emaval, color=blue,linewidth=1)
plot(smaval, color=orange,linewidth=1)
plot(stopval, color=lime,linewidth=1)

long=crossover(emaval,smaval) 
short=crossunder(emaval,smaval)

//buy-sell signal
stop=0
inlong=0
if testPeriod()
    if (long and (not inlong[1]))
        strategy.entry("buy",strategy.long)
        inlong:=1
        stop:=emaval-delta*atr
    else
        stop:=iff((nz(emaval)>(nz(stop[1])+delta*atr))and(inlong[1]),emaval-delta*atr,nz(stop[1]))
        inlong:=nz(inlong[1])
        if ((stopval<stop) and (inlong[1]))
            strategy.close("buy")
            inlong:=0
            stop:=0
else
    inlong:=0
    stop:=0
plot(stop,color=green,linewidth=1)

```

> Detail

https://www.fmz.com/strategy/441073

> Last Modified

2024-02-05 13:45:51
