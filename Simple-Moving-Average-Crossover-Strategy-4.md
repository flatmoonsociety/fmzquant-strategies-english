
> Name

Moving Average Golden Cross Strategy Simple-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is based on trading the golden cross pattern of three moving averages. Go long when the fast moving average crosses the medium speed line and the medium speed line crosses the slow speed line; go short when the fast moving average crosses below the medium speed line and the medium speed line crosses below the slow speed line.
### Strategy Principles
1. Set three moving averages with different periods: fast line, medium speed line, and slow speed line
2. When the fast line crosses the medium speed line and the medium speed line crosses the slow speed line, go long
3. When the fast line crosses the medium speed line and the medium speed line crosses the slow speed line, go short
4. Entry delay can be set to filter out false breakthroughs
5. Close the position when the reverse signal is triggered
Specifically, this strategy uses the crossover between three moving averages of different periods to trade. The fast line represents the current short-term trend, the medium-speed line represents the mid-term trend, and the slow-speed line represents the long-term trend. When the short, medium and long moving averages cross upward in sequence, it means that the trend has started and you are going long; when they cross downward, it means the trend is reversing and you are going short. Entry delays can also be set to filter out short-term false breakthroughs.
### Advantage Analysis
1. Use three moving averages to determine changes in trend direction and improve accuracy.
2. Delayed entry can filter out false breakthroughs and avoid being trapped.
3. The transaction logic is simple and intuitive, easy to understand and implement
4. The moving average parameters can be flexibly adjusted and suitable for different periods.
5. Trade with the trend and avoid the risks of trading against the trend
### Risk Analysis
1. Under a large cycle, a longer holding time is required, and there is a risk of loss expansion.
2. There is a certain lag in the intersection of the three lines, and the best entry point may be missed.
3. The moving average parameters need to be optimized, otherwise the signal may be inaccurate
4. Long-term positions need to consider overnight risks
Risks can be managed by adjusting the holding time, optimizing moving average parameters, and introducing stop-loss strategies.
### Optimization direction
1. Test different moving average period parameters to find the optimal parameters
2. Evaluate the pros and cons of different entry delays to screen signals
3. Introduce stop-loss strategy and adjust stop-loss position according to actual market conditions
4. Study the parameter preferences of different varieties and establish a parameter optimization system
5. Test adding re-entry and position addition rules to optimize positions
### Summarize
This strategy is based on the intersection of three moving averages to determine the trend direction to hold positions. The advantage is that the trading signal is simple and clear and highly configurable; the disadvantage is that it is easy to lag and requires parameter optimization. The effect can be improved through parameter tuning, stop-loss strategies, etc., and the retracement risk can be controlled. This strategy helps traders master the application of moving averages and the trading ideas of multiple moving average crossovers.
|| 

### Overview

This strategy trades based on golden cross and dead cross of 3 simple moving averages. It goes long when the fast SMA crosses above mid SMA and mid SMA crosses above slow SMA; It goes short when the reverse crossover happens. 

### Strategy Logic

1. Set 3 SMAs with different periods: fast, mid, slow
2. Go long when fast SMA crosses above mid SMA and mid above slow SMA
3. Go short when fast SMA crosses below mid SMA and mid below slow SMA
4. Can set entry delay to avoid false breakouts 
5. Exit when reverse crossover signal triggers

Specifically, it utilizes the crossovers between 3 SMAs of different periods to trade. The fast SMA represents short term trend, mid SMA represents medium term trend, and slow SMA represents long term trend. When the three SMAs crossover upward in sequence, it signals an uptrend to go long. When downward crossover happens, it signals a downtrend to go short. Entry delay can also be set to avoid short term false breakouts.

### Advantage Analysis

1. Using 3 SMAs improves directional accuracy  
2. Delayed entry avoids false breakouts and being trapped
3. Simple and intuitive logic, easy to understand
4. Flexible SMA parameter tuning for different cycles  
5. Trend following avoids counter-trend risks

### Risk Analysis

1. Long holding in long cycle risks loss expansion
2. SMA crossover has some lag, may miss best entry points 
3. Requires SMA parameter optimization, otherwise signals may be inaccurate
4. Long holding introduces overnight risks

Risks can be managed through position sizing, SMA optimization, stop loss strategies etc.

### Optimization Directions

1. Test different SMA periods to find optimal parameters
2. Evaluate entry delay to filter out signals
3. Introduce stop loss adaptable to actual price action
4. Study parameter preference across different products
5. Test adding re-entry and pyramiding rules to optimize holding

### Summary

This strategy holds positions based on 3 SMA crossovers to determine trend direction. Pros are simple clear signals and configurability; Cons are lagging signals and parameter dependency. Performance can be improved and risks controlled through parameter optimization, stop loss etc. It helps traders master using SMA and crossover strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|SMA Top|
|v_input_2|50|SMA Mid|
|v_input_3|200|SMA Low|
|v_input_4|5|Long: After trigger, how many bars to wait?|
|v_input_5|5|Short: After trigger, how many bars to wait?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © DaynTrading

//@version=4
// strategy(
//      title="Simple Moving Average Cross",
//      overlay=true,
//      initial_capital=5000,
//      default_qty_type=strategy.percent_of_equity,
//      default_qty_value=2,
//      commission_type=strategy.commission.percent,
//      commission_value=0.075,
//      pyramiding=0
//      )

sma_top_input = input(title="SMA Top", type=input.integer, defval=20)
sma_mid_input = input(title="SMA Mid", type=input.integer, defval=50)
sma_low_input = input(title="SMA Low", type=input.integer, defval=200)

bars_long = input(title="Long: After trigger, how many bars to wait?", type=input.integer, defval=5)
bars_short = input(title="Short: After trigger, how many bars to wait?", type=input.integer, defval=5)

sma_top = sma(close, sma_top_input)
sma_mid = sma(close, sma_mid_input)
sma_low = sma(close, sma_low_input)

long = sma_top > sma_mid and sma_mid > sma_low
short = sma_top < sma_mid and sma_mid < sma_low

long_condition = long and long[bars_long] and not long[bars_long + 1]
short_condition = short and short[bars_short] and not short[bars_short + 1]

close_long = sma_top < sma_mid and sma_mid < sma_low and not long[bars_long + 1]
close_short = sma_top > sma_mid and sma_mid > sma_low and not short[bars_short + 1]

plot(sma_top, title="SMA Top", color=#95f252, linewidth=2)
plot(sma_mid, title="SMA Mid", color=#FF1493, linewidth=2)
plot(sma_low, title="SMA Low", color=#6a0dad, linewidth=2)

strategy.entry("LongPosition", strategy.long, when = long_condition)
strategy.entry("ShortPosition", strategy.short, when = short_condition)
    
strategy.close("LongPosition", when = close_short)
strategy.close("ShortPosition", when = close_long)
```

> Detail

https://www.fmz.com/strategy/427445

> Last Modified

2023-09-21 10:47:24
