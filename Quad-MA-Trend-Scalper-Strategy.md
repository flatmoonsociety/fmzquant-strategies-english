
> Name

Quad-MA-Trend-Scalper-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/16cac84b8ef925cafd2cf52701f8606b6b0384f35fe12b6fb0bbfb78c54f8f05.png)

[trans]

## Overview
The Quad MA Trend Scalper is a trend following strategy that uses four moving averages of different periods to generate buy and sell signals. It is suitable for smaller time frames such as 10 minutes to 30 minutes for market beating operations.
## Strategy Principle
This strategy uses two sets of moving averages simultaneously. The first group is the fast moving average, including the MA1 of length1 period and the MA2 of length2 period. Their crossover generates buy and sell signals. The second group is the long-term moving average, including MA3 with a period of longlength1 and MA4 with a period of longlength2, which are used to determine the long-term trend direction.
Only when the fast moving average MA1 and MA2 have a golden cross, a long position will be opened. At this time, it is also necessary to determine whether the long-term moving average MA3 is above MA4. If so, it means that it is currently in a long-term upward trend, and the long signal is effective at this time.
After looking for opportunities in the long position, when the fast moving average MA1 crosses MA3, it means the short-term trend is reversed, and the position is closed at this time and the loss is stopped.
The logic of short signal generation is opposite to that of long signal symmetric, so we won’t go into details here.
Through such a design, the strategy can effectively track the trend direction and avoid being trapped in volatile market conditions. At the same time, using long-term and short-term cooperation, you can open positions at high-probability profit opportunities and set stop losses to control risks.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Use multiple sets of moving averages for judgment to make trading signals more reliable. Avoid being caught in volatile market conditions.
2. Use the long-term idea of ​​​​judging the general trend and short-term entry, which can effectively track the trend direction.
3. Set a short-term stop-loss closing point to quickly stop losses and control single losses.
4. Suitable for high-leverage transactions with higher yields.
## Risk Analysis
There are also some risks with this strategy:
1. The divergence between long and short lines may cause wrong transactions. At this time, you need to identify the signal in advance and stop the loss in time.
2. The moving average strategy is sensitive to parameter tuning. If the parameters are improperly selected, it may lead to excessive trading frequency or signal lag. Multiple tests are needed to find the best parameter combination.
3. When trading with high leverage, you must control the capital utilization rate to avoid the risk of liquidation.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Add volatility indicators, evaluate market volatility, open positions during periods of low volatility, and avoid instantaneous points of high volatility.
2. Increase the trading volume indicator and open a position at the high volume breakthrough point. Avoid false breakthroughs caused by shrinking trading volume.
3. Optimize the moving average parameters and find the best parameter combination. Cooperate with step optimization to find the global optimal parameters.
4. Observe signal characteristics on multiple time frames, design multi-time frame trading rules, and use larger time frames to confirm signals.
## Summarize
The four-moving average trend quick gap strategy is a typical trend-following strategy. It uses two sets of moving averages of different periods to make judgments, open positions in the direction of the general trend, and then use short moving averages to quickly stop profits and losses. The strategy is clear, EASY controls risks, and is suitable for high-frequency trading. There is a certain probability of false signal risk, which needs to be improved through parameter optimization and rule optimization to maximize profit opportunities.
||

## Overview  

The Quad MA Trend Scalper strategy is a trend following strategy that uses 4 moving averages of different periods to generate buy and sell signals. It works best on smaller timeframes from 10mins to 30mins for scalping to beat the market.  

## Strategy Logic  

The strategy uses two groups of moving averages. The first group consists of the fast moving averages - Length1 period MA1 and Length2 period MA2, the crossover between which generates trading signals. The second group consists of the long moving averages - Longlength1 period MA3 and Longlength2 period MA4, which determines the long term trend direction.

Long positions are opened only when the fast MAs (MA1 and MA2) have a golden crossover AND the long MAs (MA3 and MA4) suggest an upward trend (MA3 above MA4).  

The long position will be closed when the fast MA1 crosses below the slow MA3, which suggests a short term trend reversal.

The logic for shorts is symmetric and omitted here.  

This design allows the strategy to effectively track the trend direction and avoid being whipsawed in range-bound markets. Also, the combination of long and short term MAs helps identify high-probability profit opportunities to enter trades, with stop loss in place to control risks.

## Advantage Analysis   

The main advantages of this strategy are:

1. Using multiple MAs improves signal reliability and avoids whipsaws. 

2. The long-term to short-term timeframe analysis facilitates effective trend following.  

3. The short-term stop loss helps limit single trade loss.

4. Suitable for high leverage trading with good profitability.

## Risk Analysis

There are also some risks:

1. Divergence between long and short MAs may cause bad trades. These need to be identified in advance for early exit.

2. The strategy is sensitive to parameter tuning. Improper parameters may lead to over-trading or signal delays. Multiple optimization is required to find the optimum.

3. With high leverage, capital usage needs to controlled to avoid margin calls.

## Optimization Directions

Some ways to optimize the strategy:

1. Add volatility indicators to assess volatility level for improved timing.

2. Add volume indicators to trade breakouts with authentic high volume. 

3. Optimize MA lengths through iterative testing to find global optimum. 

4. Examine signals across timeframes for improved signal confirmation.

## Conclusion

The Quad MA Trend Scalper is a typical trend following strategy. It uses two groups of MAs to determine trend direction and enter positions along the major trend. Profits are captured quickly using the fast MAs. The logic is simple and risk is easy to control, making it suitable for high frequency trading. There can be some false signals which need to be improved through parameter and logic optimization to maximize profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Exponential MA|
|v_input_2|true|Long Exponential MA|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|13|MA Fast|
|v_input_5|21|MA Slow|
|v_input_6|54|Long MA 1|
|v_input_7|84|Long MA 2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-21 00:00:00
end: 2023-12-10 10:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="Quad MA Trend Scalper Backtest", shorttitle="QMA BACKTEST", overlay=true, pyramiding = 100)

//
//INPUTS
//

price = close
exponential = input(false, title="Exponential MA")
longexponential = input(true, title="Long Exponential MA")
src = input(close, title="Source")

length1 = input(13, title="MA Fast")
length2 = input(21, title="MA Slow")

longlength1 = input(54, title="Long MA 1")
longlength2 = input(84, title="Long MA 2")

//
//MAs
//

ma1 = exponential ? ema(src, length1) : sma(src, length1)
ma2 = exponential ? ema(src, length2) : sma(src, length2)
ma3 = longexponential ? ema(src, longlength1) : sma(src, longlength1)
ma4 = longexponential ? ema(src, longlength2) : sma(src, longlength1)

plot(ma1, color = black, linewidth = 2)
plot(ma2, color = red, linewidth = 2)
plot(ma3, color = blue, linewidth = 2)
plot(ma4, color = green, linewidth = 5)

long1 = crossover(ma1, ma2) and ma3 > ma4
long2 = crossover(ma1, ma2) and ma3 < ma4
short1 = crossunder(ma1, ma2) and ma3 < ma4
short2 = crossunder(ma1, ma2) and ma3 > ma4

//plotshape(long1, style=shape.triangleup, location=location.belowbar, color=green, size=size.tiny)
//plotshape(long2, style=shape.triangleup, location=location.belowbar, color=red, size=size.tiny)
//plotshape(short1, style=shape.triangledown, location=location.abovebar, color=green, size=size.tiny)
//plotshape(short2, style=shape.triangledown, location=location.abovebar, color=red, size=size.tiny)

//
//STRATEGY
//

//LONG
if (crossover(ma1, ma2) and ma1>ma4)
    strategy.entry("Long", strategy.long, comment="Long")
    
strategy.close("Long", when = crossunder(ma1, ma3))

//SHORT

if (crossunder(ma1, ma2) and ma1<ma4)
    strategy.entry("Short", strategy.short, comment="Short")

strategy.close("Short", when = crossover(ma1, ma3))


```

> Detail

https://www.fmz.com/strategy/436243

> Last Modified

2023-12-22 14:25:04
