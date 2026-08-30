
> Name

Long-Only-Triple-EMA-Golden-Cross-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is based on three EMA moving averages of different periods to judge trading signals, and uses three EMA moving averages of 8 periods, 50 periods and 200 periods to judge golden crosses and dead crosses, so as to take advantage of different EMA moving averages and achieve better trading results.
## Strategy Principle
This strategy calculates three EMA moving averages of 8 periods, 50 periods and 200 periods, and sets the Bollinger Bands channel to judge breakthroughs. The specific logic is:
1. Calculate three moving averages: 8-period EMA, 50-period EMA and 200-period EMA.
2. When the 8-period EMA crosses above the 50-period EMA and forms a golden cross, go long; when the 50-period EMA crosses below the 8-period EMA and forms a dead cross, close the position.
3. You can choose to perform long operations only when the price is higher than the 200-period EMA to avoid misoperations in volatile market conditions.
4. Set an optional take-profit EMA and close the position when the price falls below the moving average.
The bottom is determined through the calculation of fast period EMA, the medium period EMA ensures the trend, and the slow period EMA filters shocks. The three complement each other, and the trading frequency is taken into consideration while judging the pattern transformation.
## Strategic Advantages
1. The three EMA moving averages can reasonably judge the trend and give full play to the advantages of EMA in different periods. The 8-period EMA determines short-term bottom rebound opportunities, the 50-period EMA determines the mid-term trend direction, and the 200-period EMA filters shocks to ensure the general trend.
2. You can choose to go long only when the price is higher than the 200-period EMA to avoid false signals caused by volatile market conditions.
3. Optional take profit EMA moving average to set a reasonable take profit position.
4. Visual settings such as belt color, EMA line display, etc. improve the adjustability of the strategy.
5. Contains the judgment logic of golden cross and dead cross, which is concise and easy to understand.
## Risks and Solutions
1. The EMA moving average has hysteresis and may miss the best opportunity to establish a position. You can shorten the EMA period appropriately, or combine it with other indicators such as MACD to judge the timing.
2. In a volatile market, the EMA moving average may produce false signals. You can use long-period EMA to filter out shocks, or add other filtering conditions.
3. The take-profit position is fixed and cannot be adjusted according to market fluctuations. You can change it to dynamic take profit, and determine the take profit position based on indicators such as ATR.
4. Failure to consider stop loss exiting criteria, there is a risk of loss. You can set a trailing stop or a fixed pip stop to control risk.
## Strategy optimization
1. The EMA period can be optimized to find the best parameter combination.
2. Indicators such as MACD can be added to determine the timing of long and short positions.
3. Add dynamic take-profit conditions and adjust the take-profit position according to the degree of market fluctuations.
4. Add stop loss logic and set a moving stop loss or a fixed point value stop loss.
5. Optimize entry conditions, such as adding filters such as volume and energy indicators.
## Summarize
This strategy is based on the stable filtering of EMA to determine the trend direction, and combines the advantages of EMA of different periods to capture trading opportunities. Optimizing the stop-profit and stop-loss strategy and adding more indicators for judgment can improve the strategy's winning rate. Overall, this strategy is relatively simple and practical, and is suitable for trend following transactions based on EMA moving average judgment.
||


## Overview

This strategy generates trading signals based on the golden cross and death cross of three EMA lines with different periods to take advantage of each EMA's strengths and achieve better trading performance.

## Strategy Logic

The strategy calculates three EMA lines with periods of 8, 50 and 200, and generates signals when the faster EMA crosses above or below the slower EMA. The logic is:

1. Calculate the 8-period, 50-period and 200-period EMA lines.

2. Go long when the 8-period EMA crosses above the 50-period EMA (golden cross), close position when the 50-period EMA crosses below the 8-period EMA (death cross).

3. Optionally only go long when the price is above the 200-period EMA to avoid whipsaws. 

4. An optional profit-taking EMA line can be set to close positions when the price crosses below it.

The fast EMA identifies bottoms, the medium EMA determines trend, and the slow EMA filters out noise. Together they identify trend changes while maintaining decent trading frequency.

## Advantages

1. The triple EMAs effectively determine trends and capitalize on individual strengths. The 8-period EMA catches short bottoms, 50-period EMA determines mid-term trend, and 200-period EMA filters out noise.

2. Only going long above 200-period EMA avoids whipsaws.

3. Customizable profit-taking EMA sets reasonable profit targets. 

4. Visual customizations like bar colors and EMA plotting improve flexibility.

5. Simple golden/death cross logic is easy to understand.

## Risks and Mitigations

1. EMA lags may cause missed entry timing. Shorten EMA periods or combine with indicators like MACD.

2. Whipsaws may generate bad signals. Use longer EMAs to filter, or add conditions.

3. Fixed profit target is not adaptive. Use dynamic exits based on ATR etc.

4. No stops means unlimited risk. Add trailing or fixed-value stops.

## Enhancement Opportunities

1. Optimize EMA periods for best parameters.

2. Add indicators like MACD for timing.

3. Implement dynamic profit-taking based on volatility.

4. Add stop-loss logic, trailing or fixed value.

5. Improve entry conditions, e.g. volume filters.

## Conclusion

This strategy capitalizes on EMA's trend filtering to identify high-probability moves. Optimizing exits, adding indicators and filters can improve performance. Overall it is simple and practical for EMA-based trend following.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Enable Bar Color?|
|v_input_2|true|Show 8 EMA|
|v_input_3|true|Show 50 EMA|
|v_input_4|true|Show 200 EMA|
|v_input_5|false|Show profit level EMA|
|v_input_6|false|Long only above EMA200|
|v_input_7|8|v_input_7|
|v_input_8|50|v_input_8|
|v_input_9|200|v_input_9|
|v_input_10|50|v_input_10|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-18 00:00:00
end: 2023-09-20 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Long only EMA CROSS 8/50/200 Backtest", shorttitle="Golden Cross Tri EMA", overlay=true)

// EMA 8/50/200 Cross TEST



// Input
switch1=input(true, title="Enable Bar Color?")
switch2=input(true, title="Show 8 EMA")
switch3=input(true, title="Show 50 EMA")
switch4=input(true, title="Show 200 EMA")
switch5=input(false, title="Show profit level EMA")
bool_Long_EMA200=input(false, title="Long only above EMA200")
movingaverage_8 = ema(close, input(8))
movingaverage_50 = ema(close, input(50))
movingaverage_market_signal = ema(close, input(200))
movingaverage_profitlvl = ema(close, input(50))


// Calculation
bullish_cross = if bool_Long_EMA200 == true
    crossover(movingaverage_8, movingaverage_50) and movingaverage_8 > movingaverage_market_signal
else 
    bullish_cross = crossover(movingaverage_8, movingaverage_50)
bearish_cross = crossunder(close, movingaverage_profitlvl)

// Strategy
if bullish_cross
    strategy.entry("long", strategy.long)

strategy.close("long", when = bearish_cross )

// Colors
bartrendcolor = close > movingaverage_8 and close > movingaverage_50 and change(movingaverage_50) > 0 ? green : close < movingaverage_8 and close < movingaverage_50 and change(movingaverage_50) < 0 ? red : blue
barcolor(switch1?bartrendcolor:na)

// Output
plot(switch2?movingaverage_8:na,color = change(movingaverage_8) > 0 ? green : red,linewidth=2, title="EMA8")
plot(switch3?movingaverage_50:na,color = change(movingaverage_50) > 0 ? green : red,linewidth=2,title="EMA50")
plot(switch4?movingaverage_market_signal:na,color = change(movingaverage_market_signal) > 0 ? green : red,linewidth=3,title="EMA200")
plot(switch5?movingaverage_profitlvl:na,color = change(movingaverage_profitlvl) > 0 ? green : red,linewidth=3, title="EMA Profit LVL")

//
alertcondition(bullish_cross, title='Golden Cross (bullish)', message='Bullish')
alertcondition(bearish_cross, title='Death Cross (bearish)', message='Bearish')
```

> Detail

https://www.fmz.com/strategy/427895

> Last Modified

2023-09-26 16:23:53
