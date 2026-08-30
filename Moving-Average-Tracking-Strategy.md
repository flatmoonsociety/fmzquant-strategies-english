
> Name

Moving-Average-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/e81b8ed286efa50b119abf5d45839b384e6e60da8778053d087373fbc70a98c4.png)

[trans]

## Overview
The Moving Average Following Strategy is a trend following strategy based on a simple moving average. This strategy uses a simple moving average with a length of 200 days to determine the direction of the price trend. When the price crosses above the moving average, it goes long, and when the price crosses below the moving average, it goes short, thereby tracking the trend.
## Strategy Principle
This strategy is mainly based on the following principles:
1. Use the slowMA, a simple moving average with a length of 200 days, to determine the price trend direction.
2. When the closing price close crosses the slowMA, it is considered that the market has begun to rise, so go long.
3. When the closing price closes below the slowMA, it is believed that the market has begun to fall, so go short.
4. Record the last long and short time through the last_long and last_short variables.
5. Use the crossover function to determine the intersection of last_long and last_short to generate a trading signal.
6. During the backtest period, go long when the long signal long_signal is received, and go short when the short_signal signal is received.
This strategy mainly judges the direction of the trend through the moving average, and performs reverse operations in time when the moving average turns to achieve profit by tracking the trend.
## Advantage Analysis
This strategy has the following advantages:
1. The strategic ideas are simple and clear, easy to understand and implement.
2. Using long-period moving averages can effectively filter noise and lock in the main trend.
3. By performing reverse operations in time, you can capture larger price fluctuations at the turning point of the trend.
4. Only one indicator, the moving average, is needed, eliminating the complexity of combining multiple indicators.
5. The entry and exit rules are clear and do not require excessive human intervention.
## Risk Analysis
There are also some risks with this strategy:
1. Long-term moving averages are not sensitive to short-term adjustments and may miss short-term opportunities.
2. The ability to identify the top and bottom of large cycle trends is weak and reversal losses are prone to occur.
3. There is no stop loss mechanism, which may lead to larger retracements.
4. The parameters are fixed, and the ability to adapt to different varieties and market environments is weak.
5. Strategy testing based only on historical data may lead to the risk of overfitting.
In view of risks, optimization and improvement can be made from the following aspects:
1. Combine short-period moving averages and take into account long-term and short-period trends. 
2. Increase the volume and price combination conditions to avoid false breakthroughs.
3. Add trend indicator filtering to improve the ability to identify trend turning points.
4. Add a dynamic stop loss mechanism to control single losses.
5. Use parameter optimization methods to improve the adaptability of parameters.
6. Conduct replication tests in different market environments to check the robustness of the strategy.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the period parameters of the moving average and find the optimal parameter combination. Parameter optimization methods such as Walk Forward Analysis can be used.
2. Add short-term moving averages to form a multi-moving average strategy while tracking long and short cycle trends.
3. Combine with trend indicators, such as MACD, etc., to improve the ability to identify trend turning points.
4. Add stop-loss mechanisms, such as trailing stop-loss, pending order stop-loss, etc., to control single losses.
5. Conduct replication testing to test strategies in different varieties and time periods to improve robustness.
6. Use machine learning and other methods to realize parameter adaptation and strategy optimization of the strategy.
## Summarize
The moving average tracking strategy is a simple and practical trend tracking strategy with clear ideas, easy to implement, and can capture trend opportunities. However, this strategy also has some problems, such as insensitivity to short-term adjustments and weak risk control capabilities. We can optimize from many aspects to make the strategy more robust, parameters more optimized, and risk control more complete. Generally speaking, the moving average tracking strategy has good application value and is an important strategic idea for quantitative trading.
||


## Overview

The moving average tracking strategy is a trend-following strategy based on simple moving average. It uses a 200-day simple moving average to determine the price trend direction. When the price crosses above the moving average, it goes long. When the price crosses below the moving average, it goes short. This strategy tracks the trend to profit.

## Strategy Logic

The strategy is based on the following principles:

1. Use a 200-day simple moving average (slowMA) to determine the price trend.  
2. When the closing price (close) crosses above slowMA, it signals an upward trend, so go long.
3. When the closing price (close) crosses below slowMA, it signals a downward trend, so go short.
4. Use last_long and last_short variables to record the last long and short entry time.  
5. Use crossover function to detect the crossover between last_long and last_short to generate trade signals.
6. In the backtest period, go long when receiving the long signal (long_signal), and go short when receiving the short signal (short_signal).

The strategy tracks the trend by moving average direction and makes reverse trades when the MA crossover happens, to profit from the trend. 

## Advantage Analysis 

The strategy has the following advantages:

1. The strategy logic is simple and easy to understand and implement.
2. The long-period moving average filters out noise and locks in the major trend. 
3. Timely reverse trades can capture significant price swings around trend reversals.
4. It only uses one indicator, avoiding the complexity of multiple indicators.
5. Clear entry and exit rules without much human intervention.

## Risk Analysis

There are also some risks:

1. Long-period MA is not sensitive to short-term corrections, missing short-term opportunities.
2. Weak ability in identifying major trend reversal, with reversal losses.
3. No stop loss mechanism, leading to large drawdowns.  
4. Fixed parameters have weak adaptability across different products and market environments.
5. Backtest overfitting risk as the strategy is only tested on historical data.

The risks can be addressed through the following optimizations:

1. Add short-period MA to also capture short-term trends.
2. Add volume filters to avoid false breakout signals. 
3. Add trend-following indicators to improve trend reversal identification.
4. Add dynamic stop loss to control single trade loss.
5. Use parameter optimization methods to improve adaptability.  
6. Robustness test across different market environments.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Optimize the MA period parameter using methods like Walk Forward Analysis to find the optimal parameters.

2. Add a short-period MA to track both long and short-term trends.

3. Incorporate trend indicators like MACD to improve trend reversal identification. 

4. Add stop loss mechanisms like trailing stop loss to control single trade loss.

5. Robustness test on different products and time periods.

6. Use machine learning for parameter adaptive optimization.

## Conclusion

The moving average tracking strategy is a simple and practical trend-following strategy. It has a clear logic and is easy to implement for capturing trends. But it also has some weaknesses like being insensitive to short-term corrections and weak risk control. We can optimize the strategy from multiple aspects to make it more robust, better parameterized and with stronger risk management. Overall, the moving average tracking strategy has good application value and is an important trend trading concept in quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2012|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2019|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|31|Backtest Stop Day|
|v_input_7|200|v_input_7|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-19 00:00:00
end: 2023-10-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("MA X 200 BF", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.0)

/////////////// Time Frame ///////////////
testStartYear = input(2012, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2019, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() => true

///////////// MA 200 /////////////
slowMA = sma(close, input(200))

/////////////// Strategy ///////////////
long = close > slowMA
short = close < slowMA

last_long = 0.0
last_short = 0.0
last_long := long ? time : nz(last_long[1])
last_short := short ? time : nz(last_short[1])

long_signal = crossover(last_long, last_short)
short_signal = crossover(last_short, last_long)

/////////////// Execution /////////////// 
if testPeriod()
    strategy.entry("Long Entry",  strategy.long, when=long_signal)
    strategy.entry("Short Entry", strategy.short, when=short_signal)
    strategy.exit("Long Ex", "Long Entry")
    strategy.exit("Short Ex", "Short Entry")

/////////////// Plotting /////////////// 
plot(slowMA, color = long ? color.lime : color.red, linewidth=2)
bgcolor(strategy.position_size > 0 ? color.lime : strategy.position_size < 0 ? color.red : color.white, transp=80)
bgcolor(long_signal ? color.lime : short_signal ? color.red : na, transp=30)
```

> Detail

https://www.fmz.com/strategy/429782

> Last Modified

2023-10-20 17:03:32
