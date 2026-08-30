
> Name

Trend following strategy EMA-Oscillator-Trend-Following-Strategy based on EMA indicator
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/9c4951cd877fb20ae4608d33c001c0084cc8399867ab5c5304f2daf26a51a0b8.png)
[trans]


## Overview
This strategy uses the EMA indicator to identify stock price trends, and combines the standard deviation to calculate buy and sell signals to implement a trend-tracking trading strategy. The main idea is to calculate the difference between the current price and the EMA and set the threshold to buy.
## Strategy Principle
The strategy first calculates the difference v between the close price and the EMA of length ema_length. Then calculate the standard deviation dev of the ema_length period of v. Then determine the buying direction coefficient k. A k of 1 indicates a bullish buy, and a k of -1 indicates a bearish buy. Then calculate the buy signal threshold dev_limit, which is k times dev times the limit factor. When v crosses dev_limit, a buy signal is generated. The exit signal is when v goes back through the 0 axis.
This strategy offers two modes:
1. Buy bearish, buy when v crosses the negative dev_limit, that is, follow the downward trend.
2. Buy bullish, buy when v crosses the positive dev_limit, that is, follow the upward trend.
In summary, this strategy dynamically calculates the standard deviation of the difference between price and EMA, and sets the buying threshold to track the trend. The factor parameter controls the sensitivity of the buy signal. ema_length controls the EMA period. The buy pattern controls the buying direction.
## Strategic advantage analysis
This strategy has the following advantages:
1. Use the EMA indicator to identify the price trend direction. The EMA indicator smoothes the price and is effective in identifying trends.
2. Calculate dynamic thresholds based on standard deviation, which is more adaptable to market changes than fixed thresholds.
3. Two buying modes can choose to track the upward trend or the downward trend.
4. The factor parameter provides room to adjust the buying sensitivity. The ema_length parameter can adjust the EMA cycle optimization parameters.
5. The strategy logic is clear and simple, easy to understand and modify.
6. Position management can be flexibly set up to implement active strategies for chasing ups and downs trends.
## Risk Analysis
This strategy also has the following risks:
1. The EMA indicator lags behind and may miss the turning point of the trend.
2. Relies on parameter optimization. If the parameters are not set properly, it may be too sensitive or slow.
3. The risks brought by chasing the trend, if the trend reverses, it may cause large losses.
4. Frequent long-short conversions lead to frequent transactions.
5. In sharp market fluctuations, signals are frequent and transaction costs increase.
To address these risks, you can consider adding stop-loss strategies to control risks, optimizing parameter combination tests to find the best parameters, adding filter conditions to avoid too frequent transactions, etc.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test the parameter effects of different EMA periods and find the optimal EMA period length.
2. Test different values ​​of factor to find the best threshold sensitivity.
3. Optimize the opening position management strategy, such as adding positions according to the trend.
4. Add other indicator filters to avoid erroneous transactions in volatile market conditions.
5. Add a stop-loss strategy to control single losses.
6. Optimize parameters for the two buying modes and find the best parameter combination.
7. Study trend reversal signals and set trend tracking off.
## Summarize
This strategy identifies the trend direction based on EMA and dynamically calculates the threshold to generate buy and sell signals to track the trend. The strategy logic is simple and clear, and position management can be flexibly configured to actively track trends. At the same time, the strategy also has certain risks, and it is necessary to optimize and test the parameter combination, and use the StopIteration loss strategy to control risks. This strategy can be used as a good case for combining application of learning indicators and optimizing parameter settings.
||

## Overview

This strategy uses the EMA indicator to identify price trends and combines standard deviation to calculate buy and sell signals for trend following trading. The main idea is to compute the difference between the close price and EMA, set a threshold to trigger orders.

## Strategy Logic

The strategy first calculates the difference v between close price and EMA of length ema_length. Then it calculates the standard deviation dev of v over ema_length periods. Next it determines the direction coefficient k, with k=1 for long and k=-1 for short. The buy signal threshold dev_limit is calculated by k * dev * factor limit. When v crosses over dev_limit, a buy signal is triggered. The exit signal is when v crosses 0. 

The strategy provides two modes:

1. Buy short, go long when v crosses below negative dev_limit, to follow a downtrend.

2. Buy long, go long when v crosses above positive dev_limit, to follow an uptrend.

In summary, the strategy dynamically calculates the standard deviation of the difference between price and EMA to set the threshold and follows trends. The factor controls the sensitivity of buy signals. ema_length determines the EMA period. The buy mode controls the order direction.

## Advantage Analysis 

The advantages of this strategy include:

1. EMA identifies trend direction well by smoothing prices.

2. Dynamic threshold based on standard deviation adapts better than fixed thresholds. 

3. Two buy modes allow following uptrend or downtrend.

4. The factor provides flexibility in tuning buy sensitivity. ema_length allows EMA period optimization.

5. The logic is simple and easy to understand and modify.

6. Position sizing can be configured flexibly for aggressive trend following.

## Risk Analysis

The risks of the strategy:

1. EMA has lag and may miss trend turning points. 

2. It relies on parameter optimization. Improper settings lead to insufficient sensitivity or oversensitivity.

3. Trend following risks larger losses when trend reverses.  

4. Frequent long/short switches increase trading frequency.

5. Frequent signals in ranging markets increase costs.

To address the risks, consider adding stop loss, optimizing parameters, adding filters to avoid overtrading, etc.

## Optimization Directions

The strategy can be optimized by:

1. Testing different EMA periods to find the optimal length.

2. Testing different factor values to find the best sensitivity.

3. Optimizing position sizing strategies, e.g. pyramiding. 

4. Adding filters to avoid wrong trades in choppy markets.

5. Incorporating stop loss to control single trade loss.

6. Optimizing parameters separately for the two buy modes.

7. Researching trend reversal signals to stop trend following.

## Conclusion

The strategy identifies trends with EMA and generates dynamic threshold orders to follow trends. The logic is simple and clear. Position sizing can be aggressive for trend chasing. It has risks that need to be addressed through parameter optimization and stop loss. It serves as a good example to learn indicator combination and parameter tuning.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|Period|
|v_input_float_1|1.7|Factor|
|v_input_string_1|0|Model: Buy on enter to OverSell|Buy on enter to OverBuy|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-06 00:00:00
end: 2023-11-05 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Azzrael

// Based on EMA and EMA Oscilator https://www.tradingview.com/script/qM9wm0PW-EMA-Oscilator-Azzrael/

// (EMA - close) + Std Dev + Factor = detecting oversell/overbuy
// Long only!
// Pyramiding - sometimes, depends on ...
// There 2 enter strategies in one script 
// 1 - Classic, buy on entering to OverSell zone (more profitable ~> 70%)
// 2 - Crazy, buy on entering to OverBuy zone (catching trend and pyramiding, more net profit)
// Exit - crossing zero of (EMA - close)

//@version=5
strategy("STR:EMA Oscilator [Azzrael]", overlay=false, 
 margin_long=100, 
 margin_short=100, 
 currency=currency.USD,
 default_qty_type=strategy.percent_of_equity,
 default_qty_value=30,
 pyramiding=3)

entry_name="Buy"

ema_length = input.int(200, "Period", minval=2, step=10)
limit = input.float(1.7, "Factor", minval=1, step=0.1, maxval=10)
dno = input.string(defval="Buy on enter to OverSell", title="Model", options=["Buy on enter to OverSell", "Buy on enter to OverBuy"]) == "Buy on enter to OverSell"

v = close - ta.ema(close, ema_length)
dev = ta.stdev(v, ema_length)
k = dno ? -1 : 1
dev_limit = k*dev*limit

cond_long = dno ? ta.crossunder(v, dev_limit) : ta.crossover(v, dev_limit)
cond_close = ta.cross(v, 0) 

// dev visualization
sig_col = (dno and v <= dev_limit) or (not dno and v >= dev_limit) ? color.green : color.new(color.blue, 80)
plot(dev_limit, color=color.green)
plot(k*dev, color=color.new(color.blue, 60))
plot(v, color=sig_col )
hline(0)

// Make love not war
strategy.entry(entry_name, strategy.long, when=cond_long)
strategy.close(entry_name, when=cond_close)

```

> Detail

https://www.fmz.com/strategy/431217

> Last Modified

2023-11-06 09:53:27
