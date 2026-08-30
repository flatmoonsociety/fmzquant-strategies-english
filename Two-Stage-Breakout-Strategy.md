
> Name

Two-Stage-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b61de209aea886e071.png)
[trans]


## Overview
This strategy makes trading decisions based on the rise and fall of the 5-minute opening price, and uses two-level span breakthroughs to set different trigger conditions, aiming to capture larger price changes in a volatile trend.
## Strategy Principle
The strategy calculates the percentage increase or decrease of the current 5-minute K-line based on the opening price of the 5-minute K-line at 2 o'clock every day. When the increase or decrease exceeds the set first-level span, a corresponding buying or selling decision is made. Set stop loss and take profit levels at the same time to exit the position.
If the stop loss is triggered, when the increase or decrease continues to expand and exceeds the trigger condition of the second span, the previous order will be cancelled, a new buy or sell order will be placed using the second span, and the stop loss and take profit will continue to be tracked.
Through the setting of the two-level span, some noise can be filtered out in the volatile market, and transactions can only be carried out when the price changes significantly. At the same time, the activation of the second level span can reduce the situation where the stop loss is triggered too frequently.
## Strategic Advantages
- Use two levels of span to set different trigger conditions, which can effectively filter the noise in the volatile market and only trade when there are larger changes.
- The activation of the second span can effectively prevent the stop loss from being triggered too frequently
- Calculate the current rise and fall based on the opening price, and you can make profits by taking advantage of the trend after the opening of the new trading day
- The strategy logic is simple and clear, easy to understand and implement
## Risks and Countermeasures
- In sharply volatile market conditions, positions may be opened frequently and then stopped and exited, resulting in increased transaction costs.
- If the second level span is set too large, better trading opportunities may be missed.
- Setting the span too small may increase the number of unnecessary transactions
Countermeasures:
- Optimize span parameters and find the best balance point
- Increase the daily transaction limit to avoid too frequent transactions
- Combined with trend judgment, use more aggressive parameters when the trend is obvious
## Optimization direction
- Optimize the values of the two-order span and find the best parameter combination
- Study the difference in parameters between different varieties and different time periods
- Combined with trend indicators, use more aggressive parameters when the trend is obvious
- Increase the daily trading limit to avoid excessive trading
- Optimize take-profit and stop-loss points to achieve a better risk-reward ratio
## Summarize
This strategy uses two-level span breakthroughs to capture price jumps and effectively filter noise in volatile markets. The strategy concept is simple and clear, and better results can be obtained through parameter optimization. The next step can be to consider combining it with trend judgment indicators to give full play to strategic advantages in trending markets. Generally speaking, the strategic ideas are novel, the breakthrough principle is effectively used, and good results can be achieved after optimization and adjustment.
||

## Overview

This strategy makes trading decisions based on the percentage change from the 5-minute opening price at 2:00 AM each day, using a two-stage breakout to set different trigger conditions, aiming to capture significant price movements in ranging markets.

## Strategy Logic

The strategy calculates the percentage change of the current 5-minute candle based on its open price compared to the opening price of the 5-minute candle at 2:00 AM everyday. When the percentage change exceeds the first-stage breakout threshold, corresponding buy or sell decisions are made. Stop loss and take profit levels are also set to close positions.  

If the stop loss is triggered, when the percentage change continues to expand and exceeds the second-stage trigger condition, previous orders will be cancelled and new buy or sell orders using the second-stage threshold will be placed, with stop loss and take profit continuing to be tracked.

The two-stage breakout setup filters out some noise during ranging markets, only making trades on more significant price movements. Activating the second stage can reduce situations where the stop loss is triggered too frequently. 

## Advantages

- The two-stage breakout with different trigger conditions effectively filters out noise in ranging markets, only trading on larger price swings
- Activating the second stage avoids stop loss being triggered too frequently 
- Calculating percentage change from the opening price utilizes new trends after market open each day
- Simple and clear strategy logic, easy to understand and implement

## Risks and Mitigations

- High volatility may trigger frequent opening and closing of positions, increasing trading costs
- Setting the second stage too high may miss good trading opportunities 
- Setting the stages too low may trigger unnecessary extra trades

Mitigations:

- Optimize parameters to find the best balance
- Limit max number of trades per day to avoid over-trading
- Use more aggressive parameters during obvious trends

## Enhancement Opportunities

- Optimize values for the two breakout stages to find best combination
- Research optimal parameters for different products and time periods
- Incorporate trend indicator to use more aggressive settings during strong trends 
- Limit daily max trades to prevent over-trading
- Optimize stop loss and take profit points for better risk-reward

## Summary

This strategy captures price spikes using a two-stage breakout in ranging markets, filtering out noise effectively. The concept is simple and clear, and can achieve good results through parameter optimization. Next step is to combine with trend indicators to maximize performance during trending markets. Overall this is a novel strategy that makes good use of breakout principles, and can achieve solid results after tuning.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|Stop Loss Pips|
|v_input_int_2|400|Take Profit Pips|
|v_input_float_1|0.25|Percentage Change Trigger (%)|
|v_input_float_2|0.35|Additional Trigger Percentage (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-01 00:00:00
end: 2023-10-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Auto Entry Bot", overlay=true)

// Define input for the stop loss and take profit levels
stopLossPips = input.int(200, title="Stop Loss Pips", minval=1)
takeProfitPips = input.int(400, title="Take Profit Pips", minval=1)

// Calculate the percentage change from the 5-minute opening candle at 2:00 AM
var float openPrice = na
if (hour == 2 and minute == 0)
    openPrice := open
percentageChange = (close - openPrice) / openPrice * 100

// Track the cumulative percentage change
var float cumulativeChange = 0

// Define input for the percentage change trigger
triggerPercentage1 = input.float(0.25, title="Percentage Change Trigger (%)", minval=0.01, step=0.01)
triggerPercentage2 = input.float(0.35, title="Additional Trigger Percentage (%)", minval=0.01, step=0.01)

// Check for price change trigger
if (percentageChange >= triggerPercentage1)
    // Sell signal
    strategy.entry("Sell", strategy.short)
    strategy.exit("ExitSell", loss=stopLossPips, profit=takeProfitPips)
    cumulativeChange := 0  // Reset cumulative change after a trade

if (percentageChange <= -triggerPercentage1)
    // Buy signal
    strategy.entry("Buy", strategy.long)
    strategy.exit("ExitBuy", loss=stopLossPips, profit=takeProfitPips)
    cumulativeChange := 0  // Reset cumulative change after a trade

// If the price keeps hitting stop loss, activate the second trigger
if (strategy.position_size < 0 and percentageChange <= -triggerPercentage2)
    strategy.cancel("Sell")  // Cancel previous sell order
    strategy.entry("Sell2", strategy.short)
    strategy.exit("ExitSell2", loss=stopLossPips, profit=takeProfitPips)
    cumulativeChange := 0  // Reset cumulative change after a trade

if (strategy.position_size > 0 and percentageChange >= triggerPercentage2)
    strategy.cancel("Buy")  // Cancel previous buy order
    strategy.entry("Buy2", strategy.long)
    strategy.exit("ExitBuy2", loss=stopLossPips, profit=takeProfitPips)
    cumulativeChange := 0  // Reset cumulative change after a trade

```

> Detail

https://www.fmz.com/strategy/430872

> Last Modified

2023-11-02 15:58:29
