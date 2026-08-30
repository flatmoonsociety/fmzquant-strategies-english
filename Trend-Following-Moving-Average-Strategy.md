
> Name

Trend-Following-Moving-Average-Strategy Based on Trend-Following-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/31c7f8af8662e14b8f44696810369b65ca21090340c9269fe4d248db422c08ba.png)
[trans]
### Overview
This strategy calculates the channel moving average, establishes a long or short position when the price breaks through the channel moving average, and tracks the stock price trend. It is a trend following strategy.
### Strategy Principles
This strategy first calculates the average of the 20-day high as the upper track of the channel, the average of the 20-day low as the lower track of the channel, and calculates the center line of the channel. The center line of the channel represents the average recent price trend. When the price crosses above the midline of the channel, a long position is established; when the price crosses below the midline of the channel, a short position is established. Track the price trend until the price falls back to the opposite direction of the channel range, then close the position.
### Advantage Analysis
- Use channels to track price trends and avoid funds being locked in sideways markets;
- Determine the buying and selling points through the upper and lower rails of the channel, and the entry is easy to control;
- The channel range filters out some noise and increases the probability of profit;
- Configurable channel parameters to adjust the sensitivity of the strategy;
### Risk Analysis
- After a significant breakthrough of the channel center line, there may be a pullback to test the center line, and you will be trapped at this time;
- Volatile stocks are not suitable for this strategy and are prone to high-frequency trading arbitrage;
- Improper parameter settings may also affect the strategy effect;
### Optimization direction
- Optimize channel cycle parameters and test the impact of different parameters on strategy effects;
- Add stop-profit and stop-loss strategies to control single losses and all losses;
- Combine with other indicators as auxiliary judgment to avoid false signals;
-Build positions in stages to reduce the probability of being trapped by breaking through the midline of the callback test;
### Summarize
Overall, this strategy is relatively simple and direct. It uses basic price channels to determine the stock price trend and is a trend following strategy. The advantage is that it is easy to operate, makes full use of the investment opportunities brought by price trends, and avoids funds being locked up. The disadvantage is that improper parameter settings may affect the effect, and there is a certain risk of callback testing. Through reasonable optimization, the stability of the strategy can be improved and the performance of the real offer can be enhanced.
||

### Overview

This strategy calculates the channel moving average lines and establishes long or short positions when the price breaks through the channel lines to follow the trend of the stock price. It belongs to the trend following strategy.  

### Strategy Principle   

The strategy first calculates the 20-day high average as the upper rail of the channel, the 20-day low average as the lower rail of the channel, and calculates the midline of the channel. The midline of the channel represents the recent average price trend. When the price breaks through the midline of the channel upwards, a long position is established. When the price breaks through the midline of the channel downwards, a short position is established. Follow the price trend until the price falls back to the opposite side of the channel range, close the position.

### Advantage Analysis

- Use the channel to track price trends, avoid funds being locked in ranging markets; 
- Channel rails help determine entry and exit points, making it easy to control entries;
- The channel range filters out some noise and increases profit probability;  
- The channel parameters can be adjusted to tune the sensitivity of the strategy;

### Risk Analysis  

- Significant midline breakouts may be followed by pullback tests of the midline, resulting in being trapped;
- Oscillating stocks are not suitable for this strategy and may lead to high frequency trading;   
- Improper parameter settings may also affect strategy performance;  

### Optimization Directions

- Optimize channel cycle parameters to test impacts of different parameters;
- Add profit taking and stop loss strategies to control single and total losses;
- Combine other indicators as auxiliary judgements to avoid wrong signals; 
- Take positions in batches to reduce the probability of being trapped during pullback tests;   

### Summary   

In general, this strategy is relatively simple and straightforward. It judges stock price trends through basic price channels and belongs to the trend following type. The advantages are easy operation, full use of investment opportunities brought by price trends, and avoiding fund lock-ups. The disadvantages are that improper parameter settings may affect performance and there are certain risks of pullback tests. Through reasonable optimization, the stability of the strategy can be improved and real trading performance can be enhanced.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2000|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2019|Backtest Start Year|
|v_input_5|3|testEndMonth|
|v_input_6|31|Backtest Start Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//future strategy
//strategy(title = "stub", default_qty_type = strategy.fixed, default_qty_value = 1,  overlay = true, commission_type=strategy.commission.cash_per_contract,commission_value=2)
//stock strategy
strategy(title = "dc", default_qty_type = strategy.percent_of_equity, default_qty_value = 20,  overlay = true, commission_type=strategy.commission.cash_per_contract,commission_value=.005)
//forex strategy
//strategy(title = "stub", default_qty_type = strategy.percent_of_equity, default_qty_value = 20,  overlay = true)
//crypto strategy
//strategy(title = "stub", default_qty_type = strategy.percent_of_equity, default_qty_value = 20,  overlay = true, commission_type=strategy.commission.percent,commission_value=.25,default_qty_value=20)


testStartYear = input(2000, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testEndYear = input(2019, "Backtest Start Year")
testEndMonth = input(3)
testEndDay = input(31, "Backtest Start Day")
testPeriodEnd = timestamp(testStartYear,testStartMonth,testStartDay,0,0)


testPeriod() =>
    true
    //time >= testPeriodStart  ? true : false

dcPeriod = 20

dcUpper = highest(close, dcPeriod)[1]
dcLower = lowest(close, dcPeriod)[1]
dcAverage = (dcUpper + dcLower) / 2

plot(dcLower, style=line, linewidth=3, color=red, offset=1)
plot(dcUpper, style=line, linewidth=3, color=aqua, offset=1)

plot(dcAverage, color=black, style=line, linewidth=3, title="Mid-Line Average")

strategy.entry("simpleBuy", strategy.long, when=close > dcAverage)
strategy.close("simpleBuy",when=close < dcLower)
    
strategy.entry("simpleSell", strategy.short,when=close < dcAverage)
strategy.close("simpleSell",when=close > dcAverage)
    


```

> Detail

https://www.fmz.com/strategy/443123

> Last Modified

2024-02-29 14:00:35
