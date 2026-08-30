
> Name

Adaptive-Mean-Reversion-Trading-Strategy-Based-on-Chande-Momentum-Oscillator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ef5fef3349f30ba268.png)

[trans]
#### Overview
The mean reversion trading strategy based on the Chande Momentum Oscillator (CMO) is a technical analysis strategy that identifies overbought and oversold areas by calculating the momentum of price changes over a certain period of time. This strategy mainly monitors the momentum changes of asset prices and trades when prices deviate to extremes to capture opportunities for prices to return to the mean. The strategy uses the 9-day cycle CMO indicator as the core signal, opening a long position when the CMO is lower than -50, and closing the position when the CMO is higher than 50 or the position is held for more than 5 days.
#### Strategy Principle
The core of the strategy is the calculation and application of CMO indicators. CMO measures momentum by calculating the ratio of the difference to the sum of the rises and falls over a certain period. The specific calculation formula is:
CMO = 100 × (sum up - sum down)/(sum up + sum down)
Unlike traditional RSI, CMO uses both up and down data in the numerator, providing a more symmetrical measure of momentum. The strategy considers the market to be oversold when CMO is below -50 and expects the price to rebound, so it opens a long position. When the CMO rises above 50 or the position is opened for more than 5 days, the strategy closes the position to take profit or stop loss.
#### Strategic Advantages
1. Clear signals - CMO provides clear overbought and oversold judgment standards, and the trading signals are clear and there will be no ambiguity.
2. Improved risk control - By setting the maximum holding time, the risk of long-term hold-up is avoided.
3. Strong adaptability - the strategy can adjust parameters according to different market conditions and has good adaptability
4. Solid theoretical foundation - based on mature mean regression theory, with reliable academic support
5. Simple calculation - the indicator calculation method is simple and intuitive, easy to understand and implement
#### Strategy Risk
1. Trending market risk - In strong trending markets, mean reversion strategies may frequently lose money
2. Parameter sensitivity - the choice of CMO cycle and threshold has a greater impact on strategy performance
3. False signal risk - False signals may be generated during periods of severe market volatility
4. Time risk - fixed closing time may miss better profit opportunities
5. Slippage risk – you may face greater slippage in less liquid markets
#### Strategy optimization direction
1. Introducing trend filtering - you can add long-term trend indicators and only open positions when the trend is going
2. Dynamic parameter optimization - dynamically adjust CMO cycles and thresholds based on market volatility
3. Improve the stop loss mechanism - add dynamic stop loss to protect existing profits
4. Optimize holding time - the maximum holding time can be dynamically adjusted based on volatility
5. Increase volume confirmation - improve signal reliability by combining volume indicators
#### Summary
This strategy captures overbought and oversold opportunities in the market through the CMO indicator, and combines it with a fixed time stop loss to build a robust mean reversion trading system. The strategy logic is clear, the risk control is reasonable, and it has good practical value. By further optimizing parameters and adding auxiliary indicators, the stability and profitability of the strategy can be further improved. ||
#### Overview
The Mean-Reversion Trading Strategy based on the Chande Momentum Oscillator (CMO) is a technical analysis strategy that identifies overbought and oversold zones by calculating price momentum over a specific period. The strategy monitors momentum changes in asset prices and trades when prices show extreme deviations, aiming to capture mean-reversion opportunities. It uses a 9-day CMO indicator as the core signal, entering long positions when CMO falls below -50 and exiting when CMO rises above 50 or the holding period exceeds 5 days.

#### Strategy Principle
The core of the strategy lies in the calculation and application of the CMO indicator. CMO measures momentum by computing the ratio of the difference between gains and losses to their sum over a specified period. The formula is:
CMO = 100 × (Sum of Gains - Sum of Losses)/(Sum of Gains + Sum of Losses)

Unlike traditional RSI, CMO uses both up and down movements in the numerator, providing a more symmetrical momentum measurement. The strategy enters long positions when CMO falls below -50, indicating oversold conditions and expecting price recovery. Positions are closed when CMO rises above 50 or after holding for 5 days.

#### Strategy Advantages
1. Clear Signals - CMO provides definitive overbought and oversold criteria, generating unambiguous trading signals
2. Robust Risk Control - Maximum holding period prevents long-term position trapping
3. High Adaptability - Parameters can be adjusted for different market conditions
4. Solid Theoretical Foundation - Based on well-established mean-reversion theory with academic support
5. Simple Calculation - Indicator methodology is straightforward and easy to understand

#### Strategy Risks
1. Trend Market Risk - Mean-reversion strategies may suffer frequent losses in strong trending markets
2. Parameter Sensitivity - Strategy performance heavily depends on CMO period and threshold selection
3. False Signal Risk - Volatile markets may generate false signals
4. Time Risk - Fixed exit timing might miss better profit opportunities
5. Slippage Risk - May face significant slippage in low liquidity markets

#### Optimization Directions
1. Trend Filtering - Add long-term trend indicators to trade only with the trend
2. Dynamic Parameter Optimization - Adjust CMO period and thresholds based on market volatility
3. Enhanced Stop-Loss - Implement dynamic stop-loss to protect profits
4. Holding Period Optimization - Dynamically adjust maximum holding time based on volatility
5. Volume Confirmation - Incorporate volume indicators to improve signal reliability

#### Summary
The strategy captures market overbought and oversold opportunities through the CMO indicator, combining fixed-time stop-loss to build a robust mean-reversion trading system. It features clear logic and reasonable risk control with practical value. The strategy's stability and profitability can be further enhanced through parameter optimization and additional auxiliary indicators.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-09 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Chande Momentum Oscillator Strategy", overlay=false)

// Input for the CMO period
cmoPeriod = input.int(9, minval=1, title="CMO Period")

// Calculate price changes
priceChange = ta.change(close)

// Separate positive and negative changes
up = priceChange > 0 ? priceChange : 0
down = priceChange < 0 ? -priceChange : 0

// Calculate the sum of ups and downs using a rolling window
sumUp = ta.sma(up, cmoPeriod) * cmoPeriod
sumDown = ta.sma(down, cmoPeriod) * cmoPeriod

// Calculate the Chande Momentum Oscillator (CMO)
cmo = 100 * (sumUp - sumDown) / (sumUp + sumDown)

// Define the entry and exit conditions
buyCondition = cmo < -50
sellCondition1 = cmo > 50
sellCondition2 = ta.barssince(buyCondition) >= 5

// Track if we are in a long position
var bool inTrade = false

if (buyCondition and not inTrade)
    strategy.entry("Long", strategy.long)
    inTrade := true

if (sellCondition1 or sellCondition2)
    strategy.close("Long")
    inTrade := false

// Plot the Chande Momentum Oscillator
plot(cmo, title="Chande Momentum Oscillator", color=color.blue)
hline(-50, "Buy Threshold", color=color.green)
hline(50, "Sell Threshold", color=color.red)

```

> Detail

https://www.fmz.com/strategy/474705

> Last Modified

2024-12-11 17:17:50
