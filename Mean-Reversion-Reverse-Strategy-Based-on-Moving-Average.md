
> Name

Mean-Reversion-Reverse-Strategy-Based-on-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/75a72467e56fbf6aa26974cc2ccea813819940eb3d260c1247e6ca2b5462a1ac.png)

[trans]

This strategy is named "Mean Reversion Reverse Strategy Based on Moving Average". Its main idea is to buy after falling below the key moving average and stop profit after reaching the preset target profit.
The main principle of this strategy is to use the reversal of short-term moving averages to capture rebound opportunities in consolidation markets. Specifically, when the price falls below the long-term moving average (such as the 20-day moving average, the 50-day moving average, etc.), it shows strong signs of oversold. Due to the mean reversion characteristics of market fluctuations, the price will often rebound to a certain extent. At this time, if the shorter-period moving average (such as the 10-day moving average) shows an upward reversal signal, then it is a better time to buy. Corresponding to this strategy, it is to buy when the closing price is lower than the 20-day line and higher than the 50-day line, and use short-term reversal to capture its rebound.
The specific buying logic of this strategy is: buy 1 lot after the price falls below the 20-day line, add 1 lot after falling below the 50-day line, continue to add 1 lot after falling below the 100-day line, add up to 1 lot after falling below the 200-day line, and go long 4 lots. Close the position after reaching the preset take profit target. Time and stop loss conditions are also set.
### Advantage Analysis
1. Using the reversal characteristics of moving averages can effectively identify short-term rebound opportunities.
2. Open positions in batches to reduce the risk of a single point
3. Set profit-taking conditions to lock in profits
4. Use the opening price and previous lows to filter to avoid false breakthroughs
### Risk Analysis
1. When holding for a long time, you may face reversal risk. If the market continues to fall, losses will expand further
2. The moving average signal may be falsely positive, resulting in losses.
3. The set profit-taking target may not be reached, and the profit-taking cannot be achieved in whole or in part.
### Optimization direction
1. Can test the rate of return and stability under different parameter settings.
2. You can consider combining other indicators such as MACD, KD, etc. to decide to buy.
3. You can choose the moving average period suitable for your trading style according to the characteristics of different varieties.
4. Machine learning algorithms can be introduced to dynamically optimize parameters
### Summarize
Overall, this strategy is a relatively classic and common moving average trading strategy. It correctly uses the smoothing characteristics of moving averages and combines multiple moving averages to identify short-term buying opportunities. Control risks by opening positions in batches and taking profits promptly. However, its response to market emergencies such as major policy news may be relatively passive, which is a direction that can continue to be optimized. Overall, after making appropriate improvements in parameter optimization and risk control, this strategy can achieve stable excess returns.
||

The strategy is named "Mean Reversion Reverse Strategy Based on Moving Average". The main idea is to buy when price breaks through key moving averages and take profit when reaching preset targets.  

The main principle of this strategy is to capture rebound opportunities in range-bound markets by using the reversion of short-term moving averages. Specifically, when prices break through longer cycle moving averages (such as 20-day and 50-day MAs) and show signs of strong overselling, prices tend to rebound to some extent due to the mean reversion characteristic of market fluctuations. At this time, if shorter cycle moving averages (such as 10-day MA) show upward reversal signal, it would be a good timing to buy. In this strategy, it will buy when the close price is below 20-day MA while above 50-day MA, in order to capture its rebound with short-term MA reversal.

The specific entry logic is: Buy 1 lot when price breaks through 20-day MA, add 1 lot when breaking through 50-day MA, continue to add 1 lot when breaking through 100-day MA, and add up to 1 lot when breaking through 200-day MA, for a maximum of 4 lots. Take profit after reaching the preset targets. It also sets time and stop loss conditions.

### Advantage Analysis 

1. Effectively identify short-term rebound opportunities by using the reversal characteristics of moving averages  
2. Reduce risks of single point by pyramiding orders
3. Lock in profits by setting take profit targets
4. Avoid false breakouts by using open price and previous low price filters

### Risk Analysis

1. May face reversal risks in long holding periods. Losses would expand if market continues to fall.
2. MA signals may give false signals, leading to losses
3. May fail to fully or partially take profits if profit target is not reached

### Optimization Directions

1. Test profitability and stability under different parameter settings
2. Consider combining other indicators like MACD, KD to decide entries
3. Choose suitable MA periods based on characteristics of different products  
4. Introduce machine learning algorithms to dynamically optimize parameters

### Summary

In general, this is a classic and universal MA trading strategy. It correctly utilizes the smoothing feature of MAs, combined with multiple MAs to identify short-term buying opportunities. It controls risks by pyramiding orders and timely profit taking. But its response to market events like significant policy news may be more passive. This is something that can be further optimized. Overall, with appropriate improvements in parameter optimization and risk control, this strategy can obtain steady excess returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|5|Quantity 1|
|v_input_int_2|10|Quantity 2|
|v_input_int_3|15|Quantity 3|
|v_input_int_4|20|Quantity 4|
|v_input_1|true|Profit Percentage|
|v_input_int_5|2|Pyramiding|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-13 00:00:00
end: 2023-12-20 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA_zorba1", shorttitle="zorba_ema", overlay=true)

// Input parameters
qt1 = input.int(5, title="Quantity 1", minval=1)
qt2 = input.int(10, title="Quantity 2", minval=1)
qt3 = input.int(15, title="Quantity 3", minval=1)
qt4 = input.int(20, title="Quantity 4", minval=1)
ema10 = ta.ema(close, 10)
ema20 = ta.ema(close, 20)
ema50 = ta.ema(close, 50)
ema100 = ta.ema(close, 100)
ema200 = ta.ema(close, 200)

// Date range filter
start_date = timestamp(year=2021, month=1, day=1)
end_date = timestamp(year=2024, month=10, day=27)
in_date_range = true

// Profit condition
profit_percentage = input(1, title="Profit Percentage")  // Adjust this value as needed

// Pyramiding setting
pyramiding = input.int(2, title="Pyramiding", minval=1, maxval=10)

// Buy conditions
buy_condition_1 = in_date_range and close < ema20 and close > ema50 and close < open and close < low[1]
buy_condition_2 = in_date_range and close < ema50 and close > ema100 and close < open and close < low[1]
buy_condition_3 = in_date_range and close < ema100 and close > ema200 and close < open and close < low[1]
buy_condition_4 = in_date_range and close < ema200 and close < open and close < low[1]

// Exit conditions
profit_condition = strategy.position_avg_price * (1 + profit_percentage / 100) <= close
exit_condition_1 = in_date_range and (close > ema10 and ema10 > ema20 and ema10 > ema50 and ema10 > ema100 and ema10 > ema200 and close < open) and profit_condition and close < low[1] and close < low[2]
exit_condition_2 = in_date_range and (close < ema10 and close[1] > ema10 and close < close[1] and ema10 > ema20 and ema10 > ema50 and ema10 > ema100 and ema10 > ema200 and close < open) and profit_condition and close < low[1] and close < low[2]

// Exit condition for when today's close is less than the previous day's low
//exit_condition_3 = close < low[1]

// Strategy logic
strategy.entry("Buy1", strategy.long, qty=qt1 * pyramiding, when=buy_condition_1)
strategy.entry("Buy2", strategy.long, qty=qt2 * pyramiding, when=buy_condition_2)
strategy.entry("Buy3", strategy.long, qty=qt3 * pyramiding, when=buy_condition_3)
strategy.entry("Buy4", strategy.long, qty=qt4 * pyramiding, when=buy_condition_4)

strategy.close("Buy1", when=exit_condition_1 or exit_condition_2)
strategy.close("Buy2", when=exit_condition_1 or exit_condition_2)
strategy.close("Buy3", when=exit_condition_1 or exit_condition_2)
strategy.close("Buy4", when=exit_condition_1 or exit_condition_2)
```

> Detail

https://www.fmz.com/strategy/436137

> Last Modified

2023-12-21 15:45:23
