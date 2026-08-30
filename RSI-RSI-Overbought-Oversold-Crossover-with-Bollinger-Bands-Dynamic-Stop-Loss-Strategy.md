
> Name

RSI-Overbought-Oversold-Crossover-with-Bollinger-Bands-Dynamic-Stop-Loss-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8d3625e10e29a5bdfbb.png)
![IMG](https://www.fmz.com/upload/asset/2d83d0e0a238bef7def79.png)




[trans]
#### Overview
This strategy is a trading system that combines the overbought and oversold signals of the RSI indicator with the Bollinger Bands boundary. It manages trading risks by setting dynamic stop loss levels and take profit levels based on the risk-benefit ratio. The core of the strategy is to generate trading signals when the RSI indicator crosses overbought and oversold levels, and combine the price's position in the Bollinger Bands to improve the accuracy of trading.
#### Strategy Principle
The strategy is mainly based on the following core principles:
1. Use the 14-period RSI indicator to measure overbought and oversold conditions in the market
2. When RSI crosses the 30 (oversold) level from bottom to top, a long signal is triggered
3. When RSI crosses the 70 (overbought) level from top to bottom, a short signal is triggered
4. Set a long stop loss based on the lowest price in the past 10 periods
5. Set short stop loss based on the highest price in the past 10 periods
6. Use a risk-to-benefit ratio of 2:1 to dynamically calculate the take-profit level
7. Confirm the validity of trading signals based on the Bollinger Bands position
#### Strategic Advantages
1. Dynamic risk management: The strategy can adapt to changes in market volatility by dynamically setting stop loss and take profit levels.
2. Clear risk-benefit ratio: a fixed risk-benefit ratio setting of 2:1 is conducive to long-term stable profitability.
3. Multiple signal confirmation: combine RSI and Bollinger Bands two technical indicators to improve the reliability of trading signals
4. Automated execution: The strategy is completely automated, eliminating human emotional interference
5. Flexible parameter settings: RSI parameters and risk management parameters can be adjusted according to different market characteristics
#### Strategy Risk
1. Risk of false breakthrough: RSI cross signal may have false breakthrough, leading to wrong transactions
2. Shock market risk: In a range-bound market, stop loss may be triggered frequently
3. Risk of setting stop loss: setting stop loss at the highest and lowest price in a fixed period may not be suitable for all market environments.
4. Money management risk: A fixed risk-to-benefit ratio may be too aggressive under certain market conditions
5. Slippage risk: During periods of severe volatility, the actual transaction price may deviate significantly from the signal price.
#### Strategy optimization direction
1. Introduce trend filter: you can add trend indicators such as moving averages to trade in the trend direction
2. Optimize stop loss settings: consider using ATR to dynamically adjust stop loss distance
3. Increase trading volume confirmation: add trading volume indicators to verify the validity of the signal
4. Market environment classification: dynamically adjust the risk-return ratio according to different market environments
5. Add time filtering: avoid trading during periods of lower volatility
6. Optimize parameter adaptation: introduce an adaptive mechanism to dynamically adjust RSI parameters
#### Summary
This strategy builds a complete trading system by combining the RSI overbought and oversold signals with the Bollinger Bands border positions. The core advantage of the strategy lies in dynamic risk management and clear risk-return ratio settings, but you still need to pay attention to the risks caused by false breakthroughs and changes in the market environment. There is room for further improvement of the strategy by introducing trend filtering and optimizing stop loss settings.
|| 

#### Overview
This strategy combines RSI overbought/oversold signals with Bollinger Bands boundaries to create a trading system that manages risk through dynamic stop-loss levels and reward-to-risk ratio-based take-profit levels. The core mechanism triggers trading signals when RSI crosses overbought/oversold levels, enhanced by price position within Bollinger Bands.

#### Strategy Principles
The strategy operates on several key principles:
1. Uses 14-period RSI to measure market overbought/oversold conditions
2. Generates long signals when RSI crosses above 30 (oversold)
3. Generates short signals when RSI crosses below 70 (overbought)
4. Sets long stop-loss based on 10-period low
5. Sets short stop-loss based on 10-period high
6. Calculates take-profit levels using 2:1 reward-to-risk ratio
7. Confirms trade signals using Bollinger Bands position

#### Strategy Advantages
1. Dynamic Risk Management: Strategy adapts to market volatility through dynamic stop-loss and take-profit levels
2. Clear Risk-Reward Ratio: Fixed 2:1 ratio promotes consistent long-term profitability
3. Multiple Signal Confirmation: Combines RSI and Bollinger Bands for improved signal reliability
4. Automated Execution: Eliminates emotional bias through complete automation
5. Flexible Parameters: Adjustable RSI and risk management parameters for different market characteristics

#### Strategy Risks
1. False Breakout Risk: RSI crossover signals may generate false breakouts
2. Ranging Market Risk: Frequent stop-losses may occur in sideways markets
3. Stop-Loss Setting Risk: Fixed-period high/low stops may not suit all market conditions
4. Money Management Risk: Fixed risk-reward ratio may be too aggressive in certain markets
5. Slippage Risk: Significant price deviation may occur during high volatility periods

#### Optimization Directions
1. Trend Filter Integration: Add moving averages for trend-aligned trading
2. Stop-Loss Optimization: Consider ATR for dynamic stop-loss adjustment
3. Volume Confirmation: Include volume indicators for signal validation
4. Market Environment Classification: Adjust risk-reward ratio based on market conditions
5. Time Filtering: Avoid trading during low volatility periods
6. Parameter Adaptation: Implement adaptive mechanisms for RSI parameters

#### Summary
The strategy creates a comprehensive trading system by combining RSI overbought/oversold signals with Bollinger Bands boundaries. Its core strengths lie in dynamic risk management and clear risk-reward ratio settings, though attention must be paid to false breakout risks and changing market conditions. Further improvements can be achieved through trend filtering, stop-loss optimization, and other suggested enhancements.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-23 00:00:00
end: 2025-02-19 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © humblehustle

//@version=5
strategy("RSI Oversold Crossover Strategy", overlay=true)

// === INPUT PARAMETERS ===
rsi_length = input(14, title="RSI Length")
rsi_overbought = input(70, title="RSI Overbought Level")
rsi_oversold = input(30, title="RSI Oversold Level")

// === RSI CALCULATION ===
rsi = ta.rsi(close, rsi_length)

// === ENTRY CONDITIONS ===
long_condition = ta.crossover(rsi, rsi_oversold)  // RSI crosses above 30
short_condition = ta.crossunder(rsi, rsi_overbought)  // RSI crosses below 70

// === STOP LOSS & TARGET CALCULATION ===
longStop = ta.lowest(low, 10)  // Recent swing low for longs
shortStop = ta.highest(high, 10)  // Recent swing high for shorts
longTarget = close + (close - longStop) * 2  // 2:1 Risk-Reward
shortTarget = close - (shortStop - close) * 2  // 2:1 Risk-Reward

// === EXECUTE TRADES ===
if long_condition
    strategy.entry("Long", strategy.long)
    strategy.exit("ExitLong", from_entry="Long", stop=longStop, limit=longTarget)

if short_condition
    strategy.entry("Short", strategy.short)
    strategy.exit("ExitShort", from_entry="Short", stop=shortStop, limit=shortTarget)

// === ALERTS ===
alertcondition(long_condition, title="Long Signal", message="BUY: RSI Crossed Above 30 (Oversold)")
alertcondition(short_condition, title="Short Signal", message="SELL: RSI Crossed Below 70 (Overbought)")

// === PLOTTING INDICATORS & SIGNALS ===
hline(rsi_overbought, "RSI Overbought", color=color.red)
hline(rsi_oversold, "RSI Oversold", color=color.green)
plot(rsi, title="RSI", color=color.blue, linewidth=2)

plotshape(series=long_condition, location=location.belowbar, color=color.green, style=shape.labelup, title="BUY Signal", size=size.large)
plotshape(series=short_condition, location=location.abovebar, color=color.red, style=shape.labeldown, title="SELL Signal", size=size.large)

```

> Detail

https://www.fmz.com/strategy/483096

> Last Modified

2025-02-21 13:29:30
