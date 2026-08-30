
> Name

Momentum-Moving-Average-Crossover-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c7e84888afc38d2385ed6143024b154c2ee5cca22c4c8eaa80cddb107490e129.png)

[trans]

### Overview
This strategy combines moving average crossovers and momentum indicators to achieve effective tracking of trends and timely reversal. The strategy first uses the fast moving average and the slow moving average to form golden cross long and dead cross short signals. Then combined with the momentum indicator of certain parameters, when the golden cross is long, if the momentum indicator on the fast moving average rises again, it will be regarded as the trend continues and the long position will be maintained; when the momentum indicator drops, it will be regarded as the trend reversal and the position will be closed. When shorting the dead cross, the same principle is also used to track the trend reversal. At the same time, the strategy also introduces the ADX indicator to filter out erroneous signals in non-trend conditions.
### Strategy Principles
The core logic of this strategy is based on trend signals formed by moving average crossovers and momentum indicators to determine trend reversals. The code logic of the key parts is as follows:
1. Calculate the fast moving average price1 and the slow moving average price2. Among them, price1 is a 5-period HMA and price2 is a 7-period HMA.
2. When price1 crosses price2 above, a long signal is generated, and when price1 crosses below price2, a short signal is generated. This is a common usage based on moving averages.
3. After the long signal is triggered, if the momentum indicator roc1 of the fast moving average price1 rises again, it is deemed that the trend continues and the long state is maintained.
4. When the momentum indicator roc1 drops, it is considered that the trend is reversed and the position is closed. The processing logic for short signals is the same.
5. The ADX threshold is introduced to filter out erroneous signals in non-trend conditions. Actual long and short signals will only be generated when ADX is higher than the threshold.
### Advantage Analysis
Compared with the simple moving average strategy, the biggest advantage of this strategy is the introduction of momentum indicators to determine trend reversals, which can track trends and reversals in a more timely and accurate manner. The specific advantages are as follows:
1. The moving average itself lags in responding to price changes, while the momentum indicator can capture reversal signals faster, which is beneficial to timely stop loss or reverse opening of positions.
2. Reversal signals based on momentum indicators are more reliable and can reduce unnecessary repeated opening and closing of positions in trend trading.
3. The application of ADX indicator avoids false signals in non-trending markets, allowing the strategy to focus more on the trend stage, thereby increasing the probability of profit.
4. The strategy logic is clear and simple, easy to understand and track, and is suitable for beginners to learn algorithmic trading.
5. There is a large space for optimization of indicator parameters, and optimization for different markets can be achieved by adjusting the moving average period, momentum parameters, etc.
### Risk Analysis
The main risks of this strategy come from the following aspects:
1. The moving average itself lags in response to price changes, which may cause signals to lag and miss the best entry opportunity.
2. False breakthroughs cause unnecessary opening or closing of positions, and it is necessary to further optimize indicator parameters or introduce additional filtering conditions.
3. Trend reversal judgment relies on momentum indicators. When the market changes drastically, the effect of momentum indicators may be compromised.
4. The ADX index cannot perfectly judge trends and consolidations. Setting the threshold too high or too low will cause problems.
5. The strategy does not consider transaction costs. When using it in practice, you need to pay attention to setting stop loss points to control risks.
### Optimization direction
This strategy can be further optimized from the following aspects:
1. Try other types of moving averages, or adjust the moving average parameters to optimize the smoothing effect of the indicator.
2. Optimize the length parameter of the momentum indicator so that it can capture price reversal more sensitively.
3. Try to set up price filters when the momentum indicator reverses to avoid being misled by small short-term fluctuations.
4. Further enhance the use of ADX, such as using different parameters for different ADX levels, etc.
5. Introduce auxiliary conditions such as trading volume indicators to improve signal quality and filter out false breakthroughs.
6. Add a stop-loss mechanism to control single losses. Evaluate the real market fee level and set reasonable stop-profit and stop-loss levels.
### Summarize
This strategy integrates the advantages of moving average indicators and momentum indicators to achieve trend tracking and reversal capture. Compared with pure trend following, this strategy can respond more flexibly to different stages of the market and avoid losses caused by highs and lows while maintaining trend trading. Through parameter optimization and the introduction of auxiliary conditions, there is room for further improvement of the strategy effect. Overall, the strategy has clear logic, is simple and reliable, and is very suitable for beginners to learn and use algorithmic trading.
|| 


### Overview

This strategy combines moving average crossovers and momentum indicators to effectively track and reverse trends. It first uses fast and slow moving averages to generate golden cross long signals and death cross short signals. Then with momentum indicators of certain parameters, if the momentum on the fast MA turns up again after golden cross, the trend is considered continuing and long position will be kept. When momentum turns down, it's considered as trend reversal and existing position will be closed. The same logic applies to death cross short signals when tracking trend reversals. ADX filter is also used to avoid wrong signals when not in trending state.

### Strategy Logic

The core logic of this strategy is based on trend signals from MA crossovers and trend reversal signals from momentum indicators. The key parts are:

1. Calculate fast MA price1 (5-period HMA) and slow MA price2 (7-period HMA).

2. Golden cross with price1 crossing above price2 generates long signal. Death cross with price1 crossing below price2 generates short signal. This is the common usage of MAs.

3. After long signal, if price1's momentum roc1 turns up again, the trend is considered continuing and long position will be kept.

4. When momentum roc1 turns down, it's considered as trend reversal and existing position will be closed. Same logic applies to short signals.

5. Introduce ADX threshold to avoid wrong signals when not in trending state. Signals are generated only when ADX is above threshold.

### Advantage Analysis

Compared to simple MA strategies, the biggest advantage of this strategy is the introduction of momentum indicators to determine trend reversals more promptly and accurately. Specific advantages:

1. MAs themselves lag price changes, while momentum indicators can quickly capture reversal signals for timely stop loss or reverse trading.

2. Reversal signals based on momentum are more reliable, avoiding unnecessary open/close orders during trend trading.

3. ADX avoids wrong signals in non-trending markets, keeping the strategy more focused on trends with higher winning odds.

4. The logic is simple and easy to understand, suitable for algo trading beginners. 

5. Large optimization space by adjusting MA periods, momentum parameters etc. for different markets.

### Risk Analysis

The main risks of this strategy come from:

1. The lagging nature of MAs, which may cause delayed signals, missing best entry points.

2. False breakouts causing unnecessary entries or exits. Needs further optimization of parameters or additional filters.

3. Trend reversal detection relies on momentum, which may falter during huge market swings.

4. ADX is imperfect in detecting trends and consolidations. Improper threshold settings can cause issues.

5. No consideration of trading costs. Proper stop loss should be set when applied in real trading.

### Optimization Directions

The strategy can be further optimized in the following aspects:

1. Try other types of MAs or adjust MA parameters for better smoothing effects.

2. Optimize momentum indicator length for higher sensitivity to catch price reversals. 

3. Set price filters when momentum reverses to avoid being misled by short-term fluctuations.

4. Enhance ADX usage by using different parameters at different ADX levels.

5. Introduce volume indicators etc. to improve signal quality and filter false breakouts. 

6. Add stop loss mechanisms to control single trade loss. Evaluate realistic trading costs to set proper profit targets and stop loss.

### Summary

This strategy combines the advantages of MA and momentum indicators to track trends and capture reversals. Compared to pure trend following strategies, it can be more flexible in dealing with different market stages, avoiding losses from trend climax while keeping trend trading. Further improvements can be made through parameter optimization and introducing auxiliary conditions. Overall speaking, the strategy has clear and simple logic, very suitable for algo trading beginners to learn and apply.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_open|0|Source: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|5|1st MA Length|
|v_input_3|0|1st MA Type: HMA|EMA|SMA|
|v_input_4|7|2nd MA Length|
|v_input_5|0|2nd MA Type: HMA|EMA|SMA|
|v_input_6|14|ADX Smoothing|
|v_input_7|14|DI Length|
|v_input_8|20|ADX threshold|
|v_input_9|true|Lookback 1|
|v_input_10|2|Minimum slope magnitude * 100|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//study(title="MA Crossover Strategy", overlay = true)
strategy("MA Crossover Strategy with MA Turning Point Exits", overlay=true)
src = input(open, title="Source")

price = request.security(syminfo.tickerid, timeframe.period, src)
ma1 = input(5, title="1st MA Length")
type1 = input("HMA", "1st MA Type", options=["SMA", "EMA", "HMA"])

ma2 = input(7, title="2nd MA Length")
type2 = input("HMA", "2nd MA Type", options=["SMA", "EMA", "HMA"])

adxlen = input(14, title="ADX Smoothing")
dilen = input(14, title="DI Length")
adxthreshold = input(20, title="ADX threshold")

dirmov(len) =>
	up = change(high)
	down = -change(low)
	plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
	minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(plusDM, len) / truerange)
	minus = fixnan(100 * rma(minusDM, len) / truerange)
	[plus, minus]
adx(dilen, adxlen) =>
	[plus, minus] = dirmov(dilen)
	sum = plus + minus
	adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
	
sig = adx(dilen, adxlen)

//study("Average Directional Index", shorttitle="ADX", format=format.price, precision=2, resolution="")

//plot(sig, color=color.red, title="ADX")

f_hma(_src, _length)=>
    _return = wma((2*wma(_src, _length/2))-wma(_src, _length), round(sqrt(_length)))
price1 = if (type1 == "SMA")
    sma(price, ma1)
else
    if (type1 == "EMA")
        ema(price, ma1)
    else
        f_hma(price, ma1)
    
price2 = if (type2 == "SMA")
    sma(price, ma2)
else
    if (type2 == "EMA")
        ema(price, ma2)
    else
        f_hma(price, ma2)

//plot(series=price, style=line,  title="Price", color=black, linewidth=1, transp=0)
plot(series=price1, style=line,  title="1st MA", color=blue, linewidth=2, transp=0)
plot(series=price2, style=line, title="2nd MA", color=green, linewidth=2, transp=0)


//longCondition = price1> price2
longCondition = price1> price2 and sig > adxthreshold
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = price1 < price2 and sig > adxthreshold
if (shortCondition)
    strategy.entry("Short", strategy.short)

lookback1 = input(1, "Lookback 1")
roc1 = roc(price1, lookback1)

ma1up = false
ma1down = false
ma2up = false
ma2down = false

ma1up := nz(ma1up[1])
ma1down := nz(ma1down[1])
ma2up := nz(ma2up[1])
ma2down := nz(ma2down[1])

trendStrength1 = input(2, title="Minimum slope magnitude * 100", type=float) * 0.01

if crossover(roc1, trendStrength1)
    ma1up := true
    ma1down := false
    
if crossunder(roc1, -trendStrength1) 
    ma1up := false
    ma1down := true

shortexitCondition = ma1up and ma1down[1] and sig > adxthreshold
if (shortexitCondition)
    strategy.close("Short")

longexitCondition = ma1down and ma1up[1] and sig > adxthreshold
if (longexitCondition)
    strategy.close("Long")
    
    


```

> Detail

https://www.fmz.com/strategy/430023

> Last Modified

2023-10-24 12:31:44
