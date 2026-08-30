
> Name

Welles-Wilders-Trend-Balance-Point-System
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This is the original trend equilibrium point system created by Welles Wilder in 1978, and its trading rules can be found in his book "New Concept Technical Analysis System". This system uses momentum indicators to identify trends and sets stop-loss and take-profit in specific ways, forming a more robust trend tracking system.
### Strategy Principles
The main components and trading rules of the strategy are as follows:
1. Momentum indicator: Calculate the changes in the closing price of N periods and determine the price trend.
2. Long conditions: The momentum value of the current cycle and the past two cycles continues to rise.
3. Short selling conditions: The momentum value of the current period and the past two periods continues to decline.
4. Stop loss point: the average price of the previous day ± the fluctuation range of the previous day.
5. Take-profit point: 2 times the average price of the previous day - the lowest price (long) or 2 times the average price - the highest price (short).
6. Exit at the stop loss or take profit price after entering the market.
This strategy is simple and direct, using momentum to determine the direction of the trend, and using specific stop-loss and take-profit methods to control risks, forming a relatively robust trend tracking system.
### Advantage Analysis
Compared with other trend following strategies, this strategy has the following main advantages:
1. The momentum indicator is simple to calculate and easy to implement.
2. Multi-cycle combination judgment can filter noise.
3. The stop-loss and stop-profit method is relatively stable.
4. The size of a single loss can be limited.
5. The drawdown is controllable and the profit realization is clear.
6. It is not difficult to implement and can be operated flexibly.
7. Adjustable parameters, suitable for different markets.
8. The strategic idea is intuitive and simple.
9. Generally speaking, stability and risk control capabilities are strong.
### Risk Analysis
However, this strategy also has the following risks:
1. The momentum indicator lags and may miss key turning points.
2. The effect depends on the degree of parameter optimization.
3. The transaction volume is not taken into account, so there is a risk of being trapped.
4. The stop-loss and take-profit settings are arbitrary and may fail in anticipation.
5. The backtest cycle is short and long-term robustness needs to be verified.
6. Fixed position operation and cannot be dynamically adjusted.
7. The optimization space is limited and there is uncertainty in excess returns.
8. Pay attention to the return retracement ratio to prevent overfitting.
### Optimization direction
In view of the above analysis, this strategy can be optimized from the following dimensions:
1. Try different ways of calculating momentum.
2. Add transaction volume verification.
3. Optimize stop loss and take profit parameters.
4. Introduce machine learning to generate dynamic signals.
5. Evaluate the robustness of multiple varieties and multiple cycles.
6. Build a dynamic position management model.
7. Set the maximum retracement tolerance.
8. Optimize fund management strategies.
9. Continuous backtest verification to prevent over-optimization.
### Summarize
Overall, this strategy is a relatively simple and straightforward trend following system. However, any strategy needs to be continuously optimized and verified to maintain adaptability to the market. Through systematic work, the effectiveness and stability of the strategy can be improved.
||


### Overview

This is the original Trend Balance Point System created by Welles Wilder in 1978, with rules found in his book New Concepts in Technical Trading Systems. It identifies trend with momentum and sets stops/targets in a structured way to form a robust trend following system.

### Strategy Logic

The key components and rules are:

1. Momentum indicator: Calculates price change over N periods to determine trend.

2. Long condition: Momentum rising over current and previous two periods. 

3. Short condition: Momentum falling over current and previous two periods.

4. Stop loss: Previous day's average price ± previous day's range.

5. Take profit: 2 * previous day's average price - previous day low (long) or high (short).

6. Exits with stop or target after entry.

The strategy directly uses momentum for trend identification and a structured stop/target approach to control risk and form a robust trend following system.

### Advantages

Compared to other trend following strategies, the main advantages are:

1. Simple momentum calculation, easy to implement.

2. Multi-period combo filters noise. 

3. Structured stop/target is robust.

4. Limits loss per trade.

5. Drawdown controllable, profit taking clear.

6. Easy to operate flexibly.

7. Adjustable parameters for different markets. 

8. Intuitive and simple logic.

9. Overall good stability and risk control.

### Risks

However, the risks are:

1. Momentum lag may miss key turns.

2. Performance relies on parameter tuning.

3. No volume filter, risk of being trapped.

4. Stop/target settings are rigid, may fail in practice. 

5. Limited backtest period, need to verify long-term robustness. 

6. Fixed size lacks dynamic adjustment.

7. Limited optimization space, uncertain alpha. 

8. Need to monitor reward/risk ratios and curve fitting.

### Enhancements

In light of the analysis, enhancements may involve:

1. Testing different momentum calculations. 

2. Adding volume confirmation.

3. Optimizing stop/target parameters.

4. Introducing machine learning for dynamic signals.

5. Evaluating robustness across products and timeframes.

6. Constructing dynamic position sizing models. 

7. Setting maximum tolerable drawdown limit.

8. Optimizing risk management strategies.

9. Continual backtesting to prevent overfitting.

### Conclusion

In summary, this is a relatively simple and direct trend following system. But continual optimizations and robustness testing are key for any strategy to stay adaptive. Through systematic efforts, strategy performance and stability can be enhanced.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|Momentum Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-15 00:00:00
end: 2023-09-22 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © 2020 X-Trader.net

//@version=3
strategy("Trend Balance Point System by Welles Wilder", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, initial_capital = 10000)

MomPer = input(2, "Momentum Period")

isLong = strategy.position_size > 0
isShort = strategy.position_size < 0

longTrigger = mom(close, MomPer)[1] > mom(close, MomPer)[2] and mom(close, MomPer)[1] > mom(close, MomPer)[3]
shortTrigger = mom(close, MomPer)[1] < mom(close, MomPer)[2] and mom(close, MomPer)[1] < mom(close, MomPer)[3]

longEntry = (not isLong) and longTrigger 
shortEntry = (not isShort) and shortTrigger

longStop = valuewhen(longEntry, ((high[1]+low[1]+close[1])/3 - (high[1]-low[1])), 0)
longTP = valuewhen(longEntry, (2*(high[1]+low[1]+close[1])/3 - low[1]), 0)
shortStop = valuewhen(shortEntry, ((high[1]+low[1]+close[1])/3 + (high[1]-low[1])), 0)
shortTP = valuewhen(shortEntry, (2*(high[1]+low[1]+close[1])/3 - high[1]), 0)

strategy.entry(id = "Long", long = true, when = longEntry)
strategy.exit("Exit Long", "Long", profit = longTP, loss = longStop, when = isLong) 

strategy.entry(id = "Short", long = false, when = shortEntry)
strategy.exit("Exit Short", "Short", profit = shortTP, loss = shortStop, when = isShort) 


```

> Detail

https://www.fmz.com/strategy/427674

> Last Modified

2023-09-23 15:30:58
