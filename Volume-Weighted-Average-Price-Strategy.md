
> Name

Volume-Weighted-Average-Price-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/a2a1500b674f49658afdecd3d97a2063d6afb64f42412c1bc0f512f336a030e8.png)

[trans]

## Overview
The Value at Average Price (VWAP) strategy is a strategy that tracks the average price of a stock over a specific period of time. This strategy uses VWAP as a benchmark and opens a long or short position when the price is above or below VWAP. It also sets stop loss and take profit conditions to manage the trade.
## Strategy Principle
The strategy first calculates the sum of the products of typical prices (average of high, low and closing prices) and volume, as well as the sum of volume. Then divide the sum of products by the sum of trading volumes to calculate the VWAP value. When the price goes above VWAP, go long; when the price goes below VWAP, go short.
The stop-profit condition for a long position is that the price rises by 3% from the entry price; the stop-loss condition is that the price drops by 1% from the entry price. Similar conditions apply to short positions.
## Advantage Analysis
The main advantages of the VWAP strategy are:
1. Use VWAP, a recognized important statistical indicator, as the benchmark for trading signals to make the strategy more effective;
2. Use vwap signals and stop-profit and stop-loss at the same time to make profits in the trend and reduce losses;
3. The strategy logic is simple and clear, easy to understand and implement.
## Risk Analysis
There are also some risks with this strategy:
1. VWAP cannot predict future prices, so VWAP signals may lag;
2. Stop loss conditions are set too loosely, which may increase losses;
3. The longer the backtesting time is and the more trading signals there are, the actual effect may be different.
These risks can be reduced by adjusting parameters, optimizing stop loss algorithms, etc.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize VWAP parameters and find the best calculation cycle;
2. You can test other trailing stop loss algorithms, such as trailing stop loss, exponential trailing stop loss, etc.;
3. Can be combined with other indicators as filters to avoid VWAP signal errors; such as energy indicators, Bollinger Bands indicators, etc.
## Summarize
In general, the average price trading volume value strategy takes advantage of the predictive power of vwap, an important indicator, and sets stop-profit and stop-loss conditions to obtain long-term positive returns. However, it is still necessary to further optimize and combine other strategies to reduce the risks caused by market fluctuations and increase the profit margin of the strategy.

|| 

## Overview

The Volume Weighted Average Price (VWAP) strategy is a strategy that tracks the average price of a stock over a specified time. The strategy uses VWAP as a benchmark and takes long or short positions when the price crosses above or below VWAP. It also sets stop loss and take profit conditions to manage trades.  

## Strategy Logic

The strategy first calculates the typical price (average of high, low and close prices) multiplied by volume, and the sum of volume. Then VWAP is calculated by dividing the sum of typical price-volume product by the sum of volume. When price crosses over VWAP, go long. When price crosses below, go short.  

The profit taking condition for long positions is to close when price rises 3% above the entry price. The stop loss condition is when price drops 1% below entry price. Similar conditions apply for short positions.

## Advantage Analysis

The main advantages of the VWAP strategy are:

1. Uses the well-recognized VWAP statistic as benchmark for trade signals, making the strategy more effective.  

2. Utilizes both vwap signals and stop loss/profit taking, able to profit from trends and limit losses.

3. Simple and clear logic, easy to understand and implement.

## Risk Analysis

There are also some risks with this strategy:  

1. VWAP cannot predict future prices, so signals may lag.

2. Stop loss may be too wide, increasing potential loss.  

3. Longer backtests means more signals, actual performance may differ.

These risks may be reduced through parameter tuning, optimizing stop loss algorithms etc.

## Optimization Directions 

Some ways to optimize the strategy include:

1. Optimize VWAP parameters to find best calculation period.  

2. Test other tracking stop algorithms e.g. moving average stop, parabolic SAR.

3. Combine other indicators to filter VWAP signals, e.g. volume, Bollinger Bands.


## Conclusion

In summary, the VWAP strategy utilizes the predictive power of this important statistic, with stop loss/profit taking to achieve long-term positive expectancy. But further optimizations and combination with other strategies are needed to reduce market fluctuation risks for larger profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-28 00:00:00
end: 2023-12-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("VWAP Strategy by Royce Mars", overlay=true)

cumulativePeriod = input(14, "Period")

var float cumulativeTypicalPriceVolume = 0.0
var float cumulativeVolume = 0.0

typicalPrice = (high + low + close) / 3
typicalPriceVolume = typicalPrice * volume
cumulativeTypicalPriceVolume := cumulativeTypicalPriceVolume + typicalPriceVolume
cumulativeVolume := cumulativeVolume + volume
vwapValue = cumulativeTypicalPriceVolume / cumulativeVolume

// Buy condition: Price crosses over VWAP
buyCondition = crossover(close, vwapValue)

// Short condition: Price crosses below VWAP
shortCondition = crossunder(close, vwapValue)

// Profit-taking condition for long positions: Sell long position when profit reaches 3%
profitTakingLongCondition = close / strategy.position_avg_price >= 1.03

// Profit-taking condition for short positions: Cover short position when profit reaches 3%
profitTakingShortCondition = close / strategy.position_avg_price <= 0.97

// Stop loss condition for long positions: Sell long position when loss reaches 1%
stopLossLongCondition = close / strategy.position_avg_price <= 0.99

// Stop loss condition for short positions: Cover short position when loss reaches 1%
stopLossShortCondition = close / strategy.position_avg_price >= 1.01

// Strategy Execution
strategy.entry("Buy", strategy.long, when=buyCondition)
strategy.close("Buy", when=shortCondition or profitTakingLongCondition or stopLossLongCondition)

strategy.entry("Short", strategy.short, when=shortCondition)
strategy.close("Short", when=buyCondition or profitTakingShortCondition or stopLossShortCondition)

// Plot VWAP on the chart
plot(vwapValue, color=color.blue, title="VWAP")

```

> Detail

https://www.fmz.com/strategy/437032

> Last Modified

2023-12-29 16:31:33
