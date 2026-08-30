
> Name

Triple-Moving-Average-Crossover-and-Williams-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy combines three smooth moving averages, the relative strength index (RSI) and the William indicator to identify the trend direction of the stock price and look for entry opportunities when the trend reverses. When the three fast, medium and slow moving averages are aligned upward (downward), the RSI is higher (lower) than 50, and a downward (upper) William indicator signal appears, go long (short). The stop-loss point is set as a certain percentage of the entry price, and the stop-profit point is set after the entry price moves a certain percentage in a favorable direction.
## Strategy Principle
This strategy uses three smooth moving averages with different periods, including fast line, middle line and slow line. When the fast line crosses the middle line, it means that the stock price has entered an upward trend; when the fast line crosses below the middle line, it means that the stock price has entered a downward trend. After determining that the stock price is in an upward or downward trend, the strategy waits for the first trading opportunity to appear.
Specifically, after the stock price enters an upward trend, the strategy will wait for the following five conditions to be met at the same time before opening a long position:
1. The fast line, middle line and slow line are all upward;
2. RSI is higher than 50;
3. A downward William indicator pattern appears;
4. The stock price crosses the slow line;
5. There are currently no positions.
After the stock price enters a downward trend, the strategy will wait for the following five conditions to be met before opening a short position:
1. The fast line, middle line and slow line are all downward;
2. RSI is below 50;
3. The upward William indicator pattern appears;
4. The stock price crosses the slow line;
5. There are currently no positions.
After going long or short, the strategy will set stop loss points and take profit points to control risks. Specifically, the stop-loss point is a certain percentage of the entry price, and the take-profit point is the price after the entry price moves a certain percentage in a favorable direction.
## Strategic Advantages
1. Combining multiple indicators to confirm entry can effectively avoid false breakthroughs. The three moving averages determine the trend direction, the William indicator captures reversal signals, and the RSI filters the volatile market, jointly improving the accuracy of entry.
2. Setting stop-profit and stop-loss points can well control the risk-benefit ratio of each order, thereby ensuring that profitable transactions are greater than losing transactions.
3. The strategy logic is clear and easy to understand, and the parameter settings are reasonable, suitable for traders of different levels.
## Strategy Risk
1. In a volatile market, indicators may send out wrong signals, leading to unnecessary entry. You can filter out some volatile market conditions by optimizing the parameters of RSI.
2. A false breakthrough may occur when the fast line crosses the middle line and should be used in conjunction with other indicators. Consider adding a volume indicator.
3. If the stop loss point is too close to the entry price, the trade may be stopped and exited. The setting of the stop loss point needs to be adjusted to the appropriate position.
4. If the take-profit point is too far from the entry price, it may not be possible to exit at a profit, and the take-profit point also needs to be adjusted to a suitable position.
## Strategy optimization direction
1. You can test parameter combinations of different periods and optimize the parameters of the three moving averages and RSI.
2. You can add other indicators, such as trading volume indicators, to determine whether the trading volume is outstanding before a breakthrough.
3. The parameter settings of the strategy can be tested separately according to different varieties.
4. You can draw a profit curve based on the backtest results and test the settings of stop-loss and take-profit parameters.
5. You can try to conduct simulated trading and optimize parameter settings before enabling it.
## Summarize
The overall logic of this strategy is clear. Using a combination of indicators for entry and exit can effectively control risks. There is still a lot of room for parameter optimization of the strategy. By testing different parameter settings, the strategy can become a stable and profitable quantitative trading strategy. However, no strategy can completely avoid losses. Traders need to maintain trading discipline and stop profits when profits are made, and stop losses when losses occur.
||


## Overview

This strategy identifies the price trend direction by combining three smoothed moving averages, relative strength index (RSI) and Williams indicator, and seeks trading opportunities when the trend reverses. It goes long (short) when the fast, medium and slow moving averages align upward (downward), RSI is above (below) 50 and a down (up) Williams signal appears. The stop loss is set at a certain percentage of the entry price, and take profit at a certain percentage move in the favorable direction from the entry price.

## Strategy Logic

The strategy uses three moving averages with different periods, including fast, medium and slow MAs. When the fast MA crosses over the medium MA, it signals an upward price trend. When the fast MA crosses below the medium MA, it signals a downward price trend. After identifying the uptrend or downtrend, the strategy waits for the first trading opportunity. 

Specifically, after the price enters an uptrend, the strategy waits until the following five conditions are met before going long:

1. The fast, medium and slow MAs are all pointing up;

2. RSI is above 50;

3. A downside Williams pattern appears;  

4. The price crosses over the slow MA;

5. There is no current position.

After the price enters a downtrend, the strategy waits until the following five conditions are met before going short:

1. The fast, medium and slow MAs are all pointing down;

2. RSI is below 50;

3. An upside Williams pattern appears;

4. The price crosses below the slow MA; 

5. There is no current position.

After going long or short, the strategy sets a stop loss at a certain percentage below the entry price, and a take profit target at a certain percentage above the entry price.

## Advantages

1. Combining multiple indicators to confirm entries can effectively avoid false breakouts. The triple MAs identify the trend direction, Williams catches reversal signals, and RSI filters out range-bound price action, jointly improving the accuracy of entries.

2. Setting stop loss and take profit can well control the risk/reward of each trade, ensuring winning trades exceed losing trades. 

3. The strategy logic is clear and easy to understand. The parameters are reasonably set. It suits traders at different levels.

## Risks

1. Indicators may generate incorrect signals during range-bound markets, causing unnecessary entries. Optimizing RSI parameters can filter out some whipsaws.

2. The fast and medium MA crossover may have false breakouts. Using other indicators in combination, e.g. volume, is recommended.

3. If the stop loss is too close to the entry price, it may get stopped out prematurely. The stop loss should be adjusted to a proper position.

4. If the take profit is too far from the entry price, it may not get hit. The take profit also needs proper adjustment.

## Optimization Directions

1. Test different parameter combinations for the three MAs and RSI.

2. Add other indicators, like volume, to check if volume surges on breakouts. 

3. Test parameters respectively based on different products. 

4. Draw profit curves based on backtest results to optimize stop loss and take profit.

5. Try paper trading before enabling it to optimize parameters.

## Conclusion

The strategy has clear logic overall, entering and exiting positions with a combination of indicators, which effectively controls risk. There is large room for parameter optimization. By testing different parameter settings, this strategy can become a steady profitable quantitative trading strategy. However, no strategy can completely avoid losses. Traders need to follow trading disciplines - taking profits when winning and cutting losses when losing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|0.1|Stop Loss %|
|v_input_float_2|0.4|Target Profit %|
|v_input_int_1|21|(?Smooth Moving Average)Fast Length|
|v_input_int_2|50|Mid Length|
|v_input_int_3|200|Slow Length|
|v_input_int_4|14|(?RSI)length|
|v_input_int_5|2|(?Fractals)Periods|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-28 00:00:00
end: 2023-09-27 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//This script is a combination of 3 smoothed moving averages, and RSI. When moving averages are aligned upward (downward) and RSI is above (below) 50 and a down (up) William fractal appears, it enters long (short) position. Exiting from long and short entries are defined by StopLoss and TargetProfit.

//@version=5

strategy(title="3SmmaCrossUp + Fractal + RSI", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, currency=currency.USD, commission_type=strategy.commission.percent, commission_value=0.03)

///////////////////////////////////////////////////////////////////////////////////////////////////////////////// inputs

// Global
src = input(close, title="Source")
stopLoss = input.float(defval = 0.1, title = "Stop Loss %", minval = 0, maxval=100, step = 0.1)
targetProfit = input.float(defval = 0.4, title = "Target Profit %", minval = 0, maxval=100, step = 0.1)

// Smooth Moving Average
fastSmmaLen = input.int(21, minval=1, title="Fast Length", group = "Smooth Moving Average")
midSmmaLen = input.int(50, minval=1, title="Mid Length",group = "Smooth Moving Average")
slowSmmaLen = input.int(200, minval=1, title="Slow Length",group = "Smooth Moving Average")

// RSI
rsiLen = input.int(defval=14, title="length", minval=1, maxval=1000, step=1, group="RSI")

// Fractals
n = input.int(title="Periods", defval=2, minval=2, group = "Fractals")

///////////////////////////////////////////////////////////////////////////////////////////////////////////////// initialization

var waitingFirstTradeInUpwardTrend = false
var waitingFirstTradeInDownwardTrend = false

///////////////////////////////////////////////////////////////////////////////////////////////////////////////// functions

smma(ma, src, len) => 
    smma = 0.0
    smma := na(smma[1]) ? ma : (smma[1] * (len - 1) + src) / len
    smma
    
fractals(n, highs, lows) =>
    // UpFractal
    bool upflagDownFrontier = true
    bool upflagUpFrontier0 = true
    bool upflagUpFrontier1 = true
    bool upflagUpFrontier2 = true
    bool upflagUpFrontier3 = true
    bool upflagUpFrontier4 = true
    for i = 1 to n
        upflagDownFrontier := upflagDownFrontier and (highs[n-i] < highs[n])
        upflagUpFrontier0 := upflagUpFrontier0 and (highs[n+i] < highs[n])
        upflagUpFrontier1 := upflagUpFrontier1 and (highs[n+1] <= highs[n] and highs[n+i + 1] < highs[n])
        upflagUpFrontier2 := upflagUpFrontier2 and (highs[n+1] <= highs[n] and highs[n+2] <= highs[n] and highs[n+i + 2] < highs[n])
        upflagUpFrontier3 := upflagUpFrontier3 and (highs[n+1] <= highs[n] and highs[n+2] <= highs[n] and highs[n+3] <= highs[n] and highs[n+i + 3] < highs[n])
        upflagUpFrontier4 := upflagUpFrontier4 and (highs[n+1] <= highs[n] and highs[n+2] <= highs[n] and highs[n+3] <= highs[n] and highs[n+4] <= highs[n] and highs[n+i + 4] < highs[n])
    flagUpFrontier = upflagUpFrontier0 or upflagUpFrontier1 or upflagUpFrontier2 or upflagUpFrontier3 or upflagUpFrontier4
    
    upFractal = (upflagDownFrontier and flagUpFrontier)
    
    // downFractal
    bool downflagDownFrontier = true
    bool downflagUpFrontier0 = true
    bool downflagUpFrontier1 = true
    bool downflagUpFrontier2 = true
    bool downflagUpFrontier3 = true
    bool downflagUpFrontier4 = true
    
    for i = 1 to n
        downflagDownFrontier := downflagDownFrontier and (lows[n-i] > lows[n])
        downflagUpFrontier0 := downflagUpFrontier0 and (lows[n+i] > lows[n])
        downflagUpFrontier1 := downflagUpFrontier1 and (lows[n+1] >= lows[n] and lows[n+i + 1] > lows[n])
        downflagUpFrontier2 := downflagUpFrontier2 and (lows[n+1] >= lows[n] and lows[n+2] >= lows[n] and lows[n+i + 2] > lows[n])
        downflagUpFrontier3 := downflagUpFrontier3 and (lows[n+1] >= lows[n] and lows[n+2] >= lows[n] and lows[n+3] >= lows[n] and lows[n+i + 3] > lows[n])
        downflagUpFrontier4 := downflagUpFrontier4 and (lows[n+1] >= lows[n] and lows[n+2] >= lows[n] and lows[n+3] >= lows[n] and lows[n+4] >= lows[n] and lows[n+i + 4] > lows[n])
    flagDownFrontier = downflagUpFrontier0 or downflagUpFrontier1 or downflagUpFrontier2 or downflagUpFrontier3 or downflagUpFrontier4
    
    downFractal = (downflagDownFrontier and flagDownFrontier)
    [upFractal, downFractal]

///////////////////////////////////////////////////////////////////////////////////////////////////////////////// calcs

[upFractal, downFractal] = fractals(n, high, low)


rsiIsHigh = ta.rsi(src, rsiLen) >= 50 


slowMa = ta.sma(src, slowSmmaLen)
midMa = ta.sma(src, midSmmaLen)
fastMa = ta.sma(src, fastSmmaLen)

slowSmma = smma(slowMa ,src, slowSmmaLen)
midSmma = smma(midMa, src, midSmmaLen)
fastSmma = smma(fastMa, src, fastSmmaLen)

isFastSmmaUpward = ta.rising(fastSmma, 1)
isMidSmmaUpward = ta.rising(midSmma, 1)
isSlowSmmaUpward = ta.rising(slowSmma, 1)

isFastSmmaDownward = ta.falling(fastSmma, 1)
isMidSmmaDownward = ta.falling(midSmma, 1)
isSlowSmmaDownward = ta.falling(slowSmma, 1)

slowMovingAveragesAreUpward = isMidSmmaUpward and isSlowSmmaUpward
slowMovingAveragesAreDownward = isMidSmmaDownward and isSlowSmmaDownward

justEnteredUpwardTrend = ta.crossover(fastSmma, midSmma) ? true : false
justEnteredDownwardTrend = ta.crossunder(fastSmma, midSmma) ? true : false

waitingFirstTradeInUpwardTrend := justEnteredUpwardTrend == true ? true : (isFastSmmaDownward or isMidSmmaDownward or isSlowSmmaDownward ? false : waitingFirstTradeInUpwardTrend)
waitingFirstTradeInDownwardTrend := justEnteredDownwardTrend == true ? true : (isFastSmmaUpward or isMidSmmaUpward or isSlowSmmaUpward ? false : waitingFirstTradeInDownwardTrend)

priceCrossedOverSlowMa = ta.crossover(close, slowSmma)
priceCrossedUnderSlowMa = ta.crossunder(close, slowSmma)

enterLongCondition = barstate.isconfirmed and low > fastSmma and rsiIsHigh and (downFractal or priceCrossedOverSlowMa) and waitingFirstTradeInUpwardTrend and strategy.position_size == 0

enterShortCondition = barstate.isconfirmed and high < fastSmma and (not rsiIsHigh) and (upFractal or priceCrossedUnderSlowMa) and waitingFirstTradeInDownwardTrend and strategy.position_size == 0

///////////////////////////////////////////////////////////////////////////////////////////////////////////////// strategy

if(enterLongCondition)
    strategy.entry(id="L", direction=strategy.long)
    waitingFirstTradeInUpwardTrend := false

if(enterShortCondition)
    strategy.entry(id="S", direction=strategy.short)
    waitingFirstTradeInDownwardTrend := false
    
if(strategy.position_size > 0)
    strategy.exit(id="EL", stop=strategy.position_avg_price * (1 - stopLoss/100), limit=strategy.position_avg_price * (1+targetProfit/100)) 
if(strategy.position_size < 0)
    strategy.exit(id="ES", stop=strategy.position_avg_price * (1 + stopLoss/100), limit=strategy.position_avg_price * (1-targetProfit/100)) 

///////////////////////////////////////////////////////////////////////////////////////////////////////////////// plots

plot(series = slowSmma, title="Slow SMMA", linewidth=3)
plot(series = midSmma, title="Mid SMMA", linewidth=2)
plot(series = fastSmma, title="Fast SMMA", linewidth=1)
plotchar(series=rsiIsHigh, title='rsiIsHigh', char='')
plotchar(series=justEnteredUpwardTrend, title='justEnteredUpwardTrend', char='')
plotchar(series=justEnteredDownwardTrend, title='justEnteredDownwardTrend', char='')
plotchar(series=waitingFirstTradeInUpwardTrend, title='waitingFirstTradeInUpwardTrend', char='')
plotchar(series=waitingFirstTradeInDownwardTrend, title='waitingFirstTradeInDownwardTrend', char='')
plotchar(series=enterLongCondition, title='enterLongCondition' , char='')
plotchar(series=enterShortCondition, title='enterShortCondition' , char='')
plotshape(series=upFractal, title='upFractal', style=shape.triangleup, location=location.abovebar, color=#009688, size = size.tiny)
plotshape(series=downFractal, title='downFractal', style=shape.triangledown, location=location.belowbar, color=color.red, size = size.tiny)












```

> Detail

https://www.fmz.com/strategy/428052

> Last Modified

2023-09-28 10:58:16
