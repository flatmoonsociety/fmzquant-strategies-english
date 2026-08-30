
> Name

The-Quantitative-Trading-Strategy-Based-on-Dynamic-Moving-Average-Breakthrough-Entry
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1817bd16391af9a4dde.png)
[trans]
## Overview
The name of this strategy is "Quantitative trading strategy with dynamic moving average breakthrough for entry and fixed stop-profit and stop-loss for exit". The main idea of ​​this strategy is that during the trading period of every Monday, if the closing price is lower than the 115-period Hull dynamic moving average, then a long position operation will be carried out; in the subsequent trading period of every Wednesday, the position will be unconditionally closed and exited, and a fixed stop-profit and stop-loss point will be set.
## Strategy Principle
This strategy is mainly designed based on the indicator signals of Hull Moving Average and periodic trading rules.
First, during the trading session every Monday, determine whether the closing price is lower than the 115-period Hull moving average. If the conditions are met, perform a long position entry operation. Compared with ordinary moving averages, Hull moving averages can respond to price changes faster and are more sensitive to trend identification, so this indicator signal can improve the accuracy of entry timing.
Secondly, unconditionally close positions and exit during the trading session every Wednesday. Through this periodic operation method, we can avoid being affected by emergencies and reduce the probability of retracement. At the same time, a fixed ratio of take-profit and stop-loss points is set to control the risk and return of each transaction.
Finally, since the time span of each transaction position is shorter and the transaction frequency is higher, the position can be adjusted to a certain extent and the risk of a single transaction can be reduced.
## Advantage Analysis
This strategy has the following advantages:
1. Using the Hull Moving Average as an entry signal indicator can improve the accuracy of entry timing and capture trend opportunities.
2. Adopting a cyclical exit method can avoid risks caused by irrational behavior and reduce the probability of retracement.
3. Setting fixed take-profit and stop-loss points can well control the risk-return ratio of a single transaction.
4. Higher transaction frequency is helpful for position adjustment and reducing the risk of a single transaction.
5. The strategy rules are simple and clear, easy to understand and implement, and are suitable for the algorithmization of quantitative trading.

## Risk Analysis
There are also some risks in this strategy, mainly including:
1. The market may consolidate for a long time, resulting in a higher probability of being stuck after entering the market.
2. The setting of fixed take-profit and stop-loss points is not flexible enough, and it may happen that the stop-loss is taken too early or the take-profit is taken too late.
3. If there is a major and unexpected market event, the cyclical exit method may cause larger losses.
4. Frequent transactions will increase transaction costs and the impact of slippage.
5. Improper parameter settings (such as calculation period length, etc.) may affect strategy performance.

In order to reduce the above risks, the following optimization measures can be considered:
1. Judge the market pattern before entering the market and avoid entering the market during consolidation.
2. Set dynamic sliding take-profit and stop-loss or consider setting multiple fixed take-profit and stop-loss points in advance.
3. Suspend trading before and after major events to avoid periods of severe market fluctuations.
4. Appropriately reduce the frequency of transactions and reduce the impact of transaction costs and slippage.
5. Optimize parameter settings and conduct robustness tests to make the strategy more stable.
## Optimization direction
There is room for further optimization of this strategy, which mainly includes the following aspects:
1. Use methods such as machine learning to dynamically optimize the parameters of the moving average to make the indicator signal more accurate.
2. Try to combine multiple indicators to design more complex entry and exit rules.
3. Design adaptive stop-profit and stop-loss mechanisms based on different time periods and market environments.
4. Integrate risk management models to achieve better fund management.
5. Design a breakpoint restoration module to enable the strategy to successfully complete important events such as stock splits.
6. Add the real offer verification module to test the performance of the strategy in the real offer.

Through the integration and optimization of machine learning, indicator combinations, adaptive take-profit and stop-loss, risk management and other methods, this strategy can achieve stronger stability and profitability. At the same time, adding a real offer verification mechanism is an important means to further improve the strategy. These are the main directions in which this strategy can be optimized in the future.
## Summarize
This strategy is designed based on the idea of ​​Hull dynamic moving average indicator signal entry and fixed period exit. It has the advantages of accurate indicator signals and low retracement probability, and at the same time controls the take-profit and stop-loss of a single transaction. However, this strategy also has problems such as being trapped and unreasonable stop-profit and stop-loss settings. Future optimization directions include introducing machine learning and more complex multi-indicator combinations for entry, designing adaptive stop-profit and stop-loss mechanisms, and adding breakpoint reweighting and real offer verification modules. Through the comprehensive application of these measures, the stability and profitability of this strategy will be improved.
||

## Overview

The name of this strategy is "The Quantitative Trading Strategy Based on Dynamic Moving Average Breakthrough Entry and Fixed Profit-taking/Stop-loss Exit". The main idea of this strategy is to open long positions when the closing price is below the 115-period Hull Dynamic Moving Average on every Monday, and unconditionally close positions on every Wednesday afterwards, with fixed ratios of profit-target and stop-loss set simultaneously.

## Principles  

This strategy is mainly designed based on the indicator signals of Hull Moving Average and periodic trading rules.

Firstly, during the trading session on every Monday, long positions will be opened if the closing price is below the 115-period Hull Moving Average. Compared to common moving averages, Hull Moving Average responds faster to price changes and identifies trends more sensitively. Therefore, the indicator signals can improve the accuracy of market entry.

Secondly, positions will be closed unconditionally during the trading sessions on every Wednesday. This periodic operation approach can avoid being impacted by contingent events and reduce the probability of drawdowns. Meanwhile, fixed ratios of stop-loss and profit-target are set to control the risk and reward of every trade.

Finally, as each trade holding period is relatively short with higher trading frequency, it can adjust positions to some extent and decrease single trade risk.

## Advantage Analysis 

This strategy has the following advantages:

1. Using Hull Moving Average as the entry signal indicator improves the accuracy of timing market entry and captures trend opportunities.

2. The periodic exit method can avoid risks from irrational behaviors and reduce drawdown probability. 

3. The fixed profit-target and stop-loss points can control risk-reward ratio of each trade effectively.

4. High trading frequency is beneficial to adjust positions and decrease single trade risk.

5. The trading rules are simple and easy to understand and implement, which is suitable for algorithmic quantitative trading.

## Risk Analysis

This strategy also has some risks:  

1. Prolonged consolidation in the market may lead to higher probability of being trapped after entry.

2. The fixed profit-target and stop-loss points lack flexibility and may exit position too early or too late.  

3. Periodic exit may lead to huge losses if contingent events happen.

4. Frequent trading increases cost and slippage influence. 

5. Improper parameter settings (like period numbers) may affect strategy performance.

Some optimization measures can be considered to reduce the above risks:

1. Judge market condition before entry to avoid entering consolidation phases.

2. Set dynamic or multiple fixed ratios for profit-taking and stop-loss. 

3. Suspend trading around significant events to avoid extreme volatility.  

4. Lower trading frequency appropriately to reduce cost and slippage.

5. Optimize parameter settings and do robustness test to make the strategy more stable.

## Optimization Directions

This strategy can be further optimized in the following aspects:

1. Use machine learning models to optimize parameters of moving average dynamically for more accurate signals.  

2. Try combining multiple indicators to design more complex entry and exit rules.

3. Design adaptive profit-taking and stop-loss mechanisms according to different periods and market environments. 

4. Incorporate risk management models for better capital management. 

5. Design rights adjustment module to handle events like stock splits smoothly.  

6. Add real trading verification module to test strategy's performance in live markets.

By organically combining machine learning, indicator portfolio, adaptive profit-taking/stop-loss, risk management and other methods, this strategy can achieve stronger stability and profitability. Meanwhile, adding real trading verification mechanisms is also important for further perfecting the strategy. These are the main optimization directions for this strategy.


## Conclusion

This strategy is designed based on the ideas of Hull Dynamic Moving Average indicator signal entry and fixed cycle exit. It has advantages like accurate signals and low drawdown probability, while controlling single trade's profit-taking and stop-loss. But problems like being trapped and improper profit-taking/stop-loss settings also exist. Future optimization directions include introducing machine learning and more complex multi-indicator combinations for entry, designing adaptive profit-taking/stop-loss mechanisms, adding rights adjustment and real trading verification modules, etc. By comprehensively adopting these measures, the stability and profitability of this strategy will be enhanced.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|0.8|StopLoss %|
|v_input_float_2|1.5|Take Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-18 00:00:00
end: 2024-02-17 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © gnatskiller

//@version=5
strategy("Strategia HMA + LUN/MER", overlay=true)

// Inputs: stoploss %, takeProfit %
stopLossPercentage = input.float(defval=0.8, title='StopLoss %', minval=0.1, step=0.2) / 100
takeProfit = input.float(defval=1.5, title='Take Profit %', minval=0.3, step=0.2) / 100

// Calculate HMA 115
hma115 = ta.hma(close, 115)

// Exit and Entry Conditions - Check current day, session time, and price below HMA 115
isLong = dayofweek == dayofweek.monday  and not na(time(timeframe.period, "1000-1101")) and close < hma115
isExit = dayofweek == dayofweek.wednesday and not na(time(timeframe.period, "1000-1101"))

// Calculate Stoploss and Take Profit values
SL = strategy.position_avg_price * (1 - stopLossPercentage)
TP = strategy.position_avg_price * (1 + takeProfit)

// Strategy Enter, and exit when conditions are met
if isLong
    strategy.entry("Enter Long", strategy.long)
if strategy.position_size > 0 
    if isExit
        strategy.close("Enter Long", comment="Exit")
        strategy.exit("Exit", "Exit", stop=SL, limit=TP)

// Plot Stoploss and TakeProfit lines
plot(strategy.position_size > 0 ? SL : na, style=plot.style_linebr, color=color.red, linewidth=2, title="StopLoss")
plot(strategy.position_size > 0 ? TP : na, style=plot.style_linebr, color=color.green, linewidth=2, title="TakeProfit")

// Plot HMA 115
plot(hma115, color=color.blue, title="HMA 115")

```

> Detail

https://www.fmz.com/strategy/441955

> Last Modified

2024-02-18 09:53:48
