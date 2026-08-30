
> Name

15-minute breakout multi-period synergy strategy based on risk-return ratio optimization model 15-Minute-Breakout-Multi-Timeframe-Synergy-Strategy-with-Risk-Reward-Optimization-Model
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8b099d5076a19efe161.png)
![IMG](https://www.fmz.com/upload/asset/2d8c27f772acdfaa0588d.png)
 

[trans]

## Overview
This strategy is a quantitative trading system based on time period breakthroughs, using the synergistic relationship between the 15-minute and 2-minute time periods to determine trading signals. It determines the entry timing by observing whether the closing price of the 2-minute K-line breaks through the high or low of the previous complete 15-minute K-line. At the same time, it sets up a precise risk control mechanism to ensure that the risk and return ratio is 1:3, that is, each risk unit may obtain 3 times the profit. The strategy essentially captures the continuation of momentum after a short-term price breakthrough. The average winning rate is about 30%, but due to a good risk-return ratio design, it can still achieve overall positive expected returns.
## Strategy Principle
The core principle of this strategy is to identify price breakout signals through multi-period analysis. The specific implementation process is as follows:
1. First, the strategy uses the `request.security` function to obtain the highest price, lowest price and time information of the 15-minute period.
2. When a new 15-minute K-line is detected (by comparing the time of the current and previous 15-minute periods), the strategy will save the high and low points of the previous completed 15-minute K-line as the breakthrough reference point.
3. For long conditions, the strategy determines whether the closing price of the current 2-minute K-line breaks through the high point of the previous complete 15-minute K-line. When the conditions are met, the entry price is the closing price of the 2-minute K-line, the stop loss is set at the low point of the previous 15-minute K-line, and the profit target is set to the entry price plus 3 times the risk value (risk value = entry price - stop loss price).
4. For short selling conditions, the strategy determines whether the closing price of the current 2-minute K-line breaks through the low of the previous complete 15-minute K-line. When the conditions are met, the entry price is the closing price of the 2-minute K-line, the stop loss is set at the high point of the previous 15-minute K-line, and the profit target is set to the entry price minus 3 times the risk value (risk value = stop loss price - entry price).
This design utilizes the concept of breakout trading while combining the advantages of multi-period analysis, using a larger time period (15 minutes) to determine important price levels, and a smaller time period (2 minutes) to optimize entry timing, reduce slippage and improve execution accuracy.
## Strategic Advantages
1. **Clear Risk Management**: The strategy is designed with a precise risk-to-benefit ratio (1:3) to ensure that the potential gain of each transaction is 3 times the potential loss, which enables positive expected returns even if the winning rate is only about 30%.
2. **Multi-period synergy**: By combining the two time periods of 15 minutes and 2 minutes, the strategy can not only capture important price levels in the larger time period, but also use the smaller time period to optimize entry points and improve trading accuracy.
3. **Automated Execution**: The strategy is completely automated, using clear entry and exit conditions, reducing emotional interference and subjective judgment.
4. **Fund Management Integration**: The strategy uses the account equity percentage method to manage positions (default_qty_value=10), ensuring that the risk increases or decreases in proportion to the account size.
5. **Strong adaptability**: The code structure is simple and clear, easy to expand and modify, and can be applied to different markets and products.
## Strategy Risk
1. **Low Win Rate Risk**: The average win rate of the strategy is about 30%, which means that most trades will result in small losses. For some traders, consecutive losing trades can lead to psychological stress and premature abandonment of the strategy.
2. **False breakout signals**: Prices may not continue to move in the expected direction after a breakthrough, resulting in frequent stop loss triggers. Especially in sideways or highly volatile markets, false breakthroughs are more common.
3. **Slippage Risk**: When the market moves rapidly, the actual execution price may be different from the strategic plan price, affecting the accurate realization of the risk-return ratio.
4. **Over-trading risk**: Since the strategy is based on short-term execution of transactions (2 minutes), it may lead to over-trading and increase transaction costs.
5. **Market environment dependence**: This strategy performs better in markets with obvious trends, but may not be effective in range-bound markets.
Solution:
- Add additional filters such as trend indicators or volatility indicators to reduce false signals.
- Consider setting a maximum daily trading limit to avoid over-trading.
- Adjust risk parameters or pause the strategy during periods of low or high volatility.
- Regularly backtest and optimize strategy parameters to ensure adaptation to the current market environment.
## Strategy optimization direction
1. **Add trend filter**: Before executing breakout trades, introducing trend confirmation indicators (such as moving averages, MACD, etc.) and only entering the market when consistent with the general trend can significantly improve the strategy winning rate.
2. **Dynamic Risk-Return Ratio**: The current strategy uses a fixed risk-return ratio of 1:3, which can be dynamically adjusted according to market volatility, such as adopting a more conservative target in a market with high volatility.
3. **Time filter**: Add time filter conditions to avoid trading during the market opening, closing, or periods of particularly low volatility.
4. **Partial profit-taking mechanism**: Realize the segmented profit function, close some positions when the price reaches a certain target, and allow the remaining positions to continue to track the trend and improve overall profitability.
5. **Adaptive parameters**: Change fixed parameters (such as 15-minute period) to dynamic parameters that are automatically adjusted based on market conditions, so that the strategy can better adapt to different market environments.
6. **Volume Confirmation**: Add volume analysis to ensure that price breakthroughs are accompanied by sufficient trading volume, which usually improves the reliability of breakthrough signals.
These optimization directions are mainly aimed at improving the winning rate and stability of the strategy, while maintaining its core advantages - clear risk management and multi-cycle synergy characteristics. By introducing more market factors into consideration, false signals can be reduced and the probability of success for each transaction can be increased.
## Summarize
"15-minute breakthrough multi-period collaborative strategy based on risk-benefit ratio optimization model" is a quantitative trading system with clear structure and rigorous logic. It captures momentum opportunities after breakthroughs by combining price information in different time periods. Although the strategy's winning rate is not high (about 30%), positive expected returns are achieved through a carefully designed risk-benefit ratio mechanism of 1:3.
The core advantage of the strategy lies in its strict risk control, clear entry and exit rules and multi-period collaborative analysis methods. The main risks come from false breakout signals and the psychological pressure caused by low winning rates. Future optimization directions should focus on improving signal quality, reducing false breakout trades, and consider adding trend filtering and dynamic parameter adjustment functions.
For quantitative traders pursuing short- to medium-term trading opportunities, this is a basic strategy framework worth considering that can be further customized and optimized based on personal risk preferences and trading goals. ||
## Overview

This strategy is a quantitative trading system based on timeframe breakout, utilizing the synergistic relationship between 15-minute and 2-minute timeframes to determine trading signals. It identifies entry opportunities by observing whether the 2-minute candle's closing price breaks through the high or low of the previous completed 15-minute candle, while implementing a precise risk control mechanism that ensures a risk-to-reward ratio of 1:3, meaning each unit of risk can potentially yield 3 units of profit. The strategy essentially captures momentum continuation after short-term price breakouts, with an average win rate of approximately 30%, but can still achieve an overall positive expected return due to its well-designed risk-reward ratio.

## Strategy Principles

The core principle of this strategy is to identify price breakout signals through multi-timeframe analysis. The specific implementation process is as follows:

1. First, the strategy uses the `request.security` function to obtain the highest price, lowest price, and time information for the 15-minute timeframe.

2. When a new 15-minute candle is detected (by comparing the current and previous 15-minute period times), the strategy saves the high and low points of the previous completed 15-minute candle as breakout reference points.

3. For long conditions, the strategy determines whether the current 2-minute candle's closing price breaks through the high of the last complete 15-minute candle. When this condition is met, the entry price is the 2-minute candle's closing price, the stop loss is set at the low of the previous 15-minute candle, and the profit target is set at the entry price plus 3 times the risk value (risk value = entry price - stop loss price).

4. For short conditions, the strategy determines whether the current 2-minute candle's closing price breaks through the low of the last complete 15-minute candle. When this condition is met, the entry price is the 2-minute candle's closing price, the stop loss is set at the high of the previous 15-minute candle, and the profit target is set at the entry price minus 3 times the risk value (risk value = stop loss price - entry price).

This design leverages the concept of breakout trading while combining the advantages of multi-timeframe analysis, using a larger timeframe (15 minutes) to determine important price levels and a smaller timeframe (2 minutes) to optimize entry timing, reduce slippage, and improve execution precision.

## Strategy Advantages

1. **Clear Risk Management**: The strategy features a precise risk-reward ratio (1:3), ensuring that the potential return for each trade is three times the potential loss, which allows for positive expected returns even with a win rate of only around 30%.

2. **Multi-Timeframe Synergy**: By combining 15-minute and 2-minute timeframes, the strategy can both capture important price levels from the larger timeframe and optimize entry points using the smaller timeframe, improving trading precision.

3. **Automated Execution**: The strategy is fully automated with clear entry and exit conditions, reducing emotional interference and subjective judgment.

4. **Integrated Capital Management**: The strategy adopts a percentage of equity approach for position sizing (default_qty_value=10), ensuring that risk scales proportionally with account size.

5. **High Adaptability**: The code structure is concise and clear, making it easy to extend and modify for application across different markets and products.

## Strategy Risks

1. **Low Win Rate Risk**: The strategy has an average win rate of approximately 30%, meaning most trades will result in small losses. For some traders, consecutive losing trades may cause psychological pressure and premature abandonment of the strategy.

2. **False Breakout Signals**: After a price breakout, the price may not continue to move in the expected direction, leading to frequent stop-loss triggers. This is especially common in ranging markets or highly volatile conditions.

3. **Slippage Risk**: During rapid market movements, the actual execution price may differ from the planned price, affecting the precise implementation of the risk-reward ratio.

4. **Overtrading Risk**: Since the strategy executes trades based on a short timeframe (2 minutes), it may lead to overtrading and increased transaction costs.

5. **Market Environment Dependency**: This strategy performs better in trending markets and may underperform in range-bound, oscillating markets.

Solutions:
- Add additional filtering conditions, such as trend indicators or volatility indicators, to reduce false signals.
- Consider setting daily maximum trade limits to avoid overtrading.
- Adjust risk parameters or pause the strategy during periods of low or high volatility.
- Regularly backtest and optimize strategy parameters to ensure adaptation to the current market environment.

## Strategy Optimization Directions

1. **Add Trend Filters**: Introduce trend confirmation indicators (such as moving averages, MACD, etc.) before executing breakout trades, only entering when aligned with the larger trend, which can significantly improve the strategy's win rate.

2. **Dynamic Risk-Reward Ratio**: The strategy currently uses a fixed 1:3 risk-reward ratio, but could be enhanced by dynamically adjusting this ratio based on market volatility, such as adopting more conservative targets in highly volatile markets.

3. **Time Filtering**: Add time-based filtering conditions to avoid trading during market open, close, or particularly low volatility periods.

4. **Partial Profit-Taking Mechanism**: Implement a staged profit-taking functionality that closes part of the position when certain price targets are reached, allowing the remaining position to continue tracking the trend, improving overall profitability.

5. **Adaptive Parameters**: Transform fixed parameters (such as the 15-minute period) into dynamic parameters that automatically adjust based on market conditions, enabling the strategy to better adapt to different market environments.

6. **Volume Confirmation**: Incorporate volume analysis to ensure price breakouts are accompanied by sufficient trading volume, which typically enhances the reliability of breakout signals.

These optimization directions primarily aim to improve the strategy's win rate and stability while maintaining its core advantages—clear risk management and multi-timeframe synergy. By introducing consideration of more market factors, false signals can be reduced, increasing the probability of success for each trade.

## Summary

The "15-Minute Breakout Multi-Timeframe Synergy Strategy with Risk-Reward Optimization Model" is a clearly structured, logically rigorous quantitative trading system that captures momentum opportunities after breakouts by combining price information from different timeframes. Despite the strategy's relatively low win rate (approximately 30%), it achieves positive expected returns through a carefully designed 1:3 risk-reward ratio mechanism.

The strategy's core strengths lie in its strict risk control, clear entry and exit rules, and multi-timeframe synergistic analysis method. The main risks come from false breakout signals and the psychological pressure associated with a low win rate. Future optimization should focus on improving signal quality, reducing false breakout trades, and considering the addition of trend filtering and dynamic parameter adjustment capabilities.

For quantitative traders seeking medium to short-term trading opportunities, this represents a worthwhile basic strategy framework that can be further customized and optimized according to individual risk preferences and trading objectives.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-03-23 00:00:00
end: 2025-03-24 21:00:00
period: 15m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("15-min Breakout via 2-min Candle (R:R=1:3)", 
     overlay=true,
     initial_capital=100000,
     default_qty_type=strategy.percent_of_equity,
     default_qty_value=10)

//-----------------------------------------------------
// 1) Retrieve 15-min high/low & time via request.security
//-----------------------------------------------------
fifteenHigh = request.security(syminfo.tickerid, "15", high)
fifteenLow  = request.security(syminfo.tickerid, "15", low)
time15      = request.security(syminfo.tickerid, "15", time)

//-----------------------------------------------------
// 2) Store the most recent closed 15-min bar's high/low
//-----------------------------------------------------
// We use a var variable (stored over time) and update it 
// whenever a NEW 15-min bar is detected.
var float last15High = na
var float last15Low  = na

// A new 15-min bar (in the "15" series) is indicated when time15 changes.
bool new15bar = time15 != time15[1]

// Update high/low when a new 15-min bar starts
if new15bar
    // [1] = previous closed 15-min bar value
    last15High := fifteenHigh[1]
    last15Low  := fifteenLow[1]

//-----------------------------------------------------
// 3) Long position: 2-min close > most recent closed 15-min high
//-----------------------------------------------------
bool longCondition = not na(last15High) and close > last15High
if longCondition
    // Entry is 2-min close
    float stopPrice  = last15Low
    float risk       = close - stopPrice
    float takeProfit = close + 3 * risk
    
    strategy.entry("Long Breakout", strategy.long)
    strategy.exit("Long Exit (SL/TP)", "Long Breakout", stop=stopPrice, limit=takeProfit)

//-----------------------------------------------------
// 4) Short position: 2-min close < most recent closed 15-min low
//-----------------------------------------------------
bool shortCondition = not na(last15Low) and close < last15Low
if shortCondition
    float stopPrice  = last15High
    float risk       = stopPrice - close
    float takeProfit = close - 3 * risk
    
    strategy.entry("Short Breakout", strategy.short)
    strategy.exit("Short Exit (SL/TP)", "Short Breakout", stop=stopPrice, limit=takeProfit)

```

> Detail

https://www.fmz.com/strategy/488850

> Last Modified

2025-03-31 17:32:58
