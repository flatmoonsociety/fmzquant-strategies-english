
> Name

High-Win-Rate-Trend-Mean-Reversion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6ba8b85a4894fe4f610e42db6fcc8059d7b30022da15e85897346e3474c524be.png)

[trans]
#### Overview
This is a quantitative trading strategy designed based on the mean reversion principle. It combines technical indicators such as Bollinger Bands, Relative Strength Index (RSI) and Average True Range (ATR) to trade by identifying overbought and oversold conditions in the market. The strategy adopts a low risk-reward ratio setting to increase the winning rate and controls risk through money management.
#### Strategy Principle
The strategy mainly implements transactions through the following aspects:
1. Use Bollinger Bands (20th day) as the basis for judging price fluctuation ranges
2. Determine the overbought and oversold status of the market through RSI (14th day)
3. Use ATR (14th) to dynamically set stop loss and profit targets
4. Enter long when the price breaks through the lower Bollinger Band and the RSI is below 30
5. Enter short when the price breaks through the upper Bollinger Band and the RSI is above 70
6. Set a risk-reward ratio of 0.75 to improve the strategy’s winning rate
7. Adopt 2% risk control based on account equity
#### Strategic Advantages
1. Combine multiple technical indicators to improve the reliability of trading signals
2. Capture overbought and oversold opportunities in the market through mean reversion characteristics
3. Use ATR to dynamically adjust the stop loss position to adapt to market fluctuations
4. Low risk-reward ratio settings improve strategy winning rate
5. Use percentage risk management to achieve effective allocation of funds
6. The strategy has clear logic and is easy to understand and execute.
7. Has good scalability and room for optimization
#### Strategy Risk
1. You may face frequent stop losses in a strong trending market
2. A low risk-reward ratio may result in relatively small single profits.
3. Bollinger Bands and RSI indicators may produce hysteresis
4. The stop loss position may not be ideal when the market fluctuates violently.
5. Transaction costs may affect the overall return of the strategy
Solution:
- Add trend filter
- Optimize entry timing
- Adjust indicator parameters
-Introduced more confirmation signals
#### Strategy optimization direction
1. Introduce trend judgment indicators to avoid contrarian trading
2. Optimize RSI and Bollinger Band parameters to improve signal accuracy
3. Dynamically adjust the risk-reward ratio according to different market conditions
4. Add trading volume indicators as auxiliary confirmation
5. Consider adding time filters to avoid trading during specific periods
6. Develop adaptive parameter mechanism to improve strategy adaptability
7. Improve the fund management system and optimize the size of positions
#### Summary
This strategy builds a robust trading system through the combination of the mean reversion principle and multiple technical indicators. The setting of low risk-reward ratio helps to increase the winning rate, while strict risk management ensures the safety of funds. Although there are some inherent risks, through continuous optimization and improvement, the strategy is expected to achieve better performance. This is a strategy suitable for steady traders, especially in volatile markets.
||

#### Overview
This is a quantitative trading strategy based on mean reversion principles, combining technical indicators such as Bollinger Bands, Relative Strength Index (RSI), and Average True Range (ATR) to identify market overbought and oversold conditions. The strategy employs a low risk-reward ratio to achieve high win rates and implements risk management through position sizing.

#### Strategy Principles
The strategy executes trades through the following aspects:
1. Uses Bollinger Bands (20-day) to determine price movement ranges
2. Employs RSI (14-day) to identify overbought and oversold conditions
3. Utilizes ATR (14-day) for dynamic stop-loss and take-profit levels
4. Enters long positions when price breaks below the lower band and RSI is below 30
5. Enters short positions when price breaks above the upper band and RSI is above 70
6. Sets a 0.75 risk-reward ratio to achieve higher win rates
7. Implements 2% risk per trade based on account equity

#### Strategy Advantages
1. Combines multiple technical indicators for reliable signals
2. Captures market opportunities through mean reversion characteristics
3. Uses ATR for dynamic stop-loss adjustment
4. Higher win rate through low risk-reward ratio setting
5. Effective capital allocation through percentage-based risk management
6. Clear and easy-to-understand strategy logic
7. Good scalability and optimization potential

#### Strategy Risks
1. May face frequent stop-losses in strong trend markets
2. Lower potential profits per trade due to low risk-reward ratio
3. Potential lag in Bollinger Bands and RSI indicators
4. Stop-loss positions may be suboptimal during high volatility
5. Trading costs may impact overall returns
Solutions:
- Add trend filters
- Optimize entry timing
- Adjust indicator parameters
- Introduce additional confirmation signals

#### Optimization Directions
1. Incorporate trend indicators to avoid counter-trend trades
2. Optimize RSI and Bollinger Bands parameters for better accuracy
3. Implement dynamic risk-reward ratios based on market conditions
4. Add volume indicators for signal confirmation
5. Include time filters to avoid specific trading periods
6. Develop adaptive parameter mechanisms
7. Enhance position sizing and risk management system

#### Conclusion
The strategy builds a robust trading system through mean reversion principles and multiple technical indicators. The low risk-reward ratio setting helps achieve higher win rates, while strict risk management ensures capital preservation. Despite inherent risks, continuous optimization and refinement could lead to improved performance. This strategy is suitable for conservative traders, particularly in markets with high volatility.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-11-11 00:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("High Win Rate Mean Reversion Strategy for Gold", overlay=true)

// Input Parameters
bbLength = input.int(20, title="Bollinger Bands Length")
bbMult = input.float(2, title="Bollinger Bands Multiplier")
rsiLength = input.int(14, title="RSI Length")
rsiOverbought = input.int(70, title="RSI Overbought Level")
rsiOversold = input.int(30, title="RSI Oversold Level")
atrLength = input.int(14, title="ATR Length")
rrRatio = input.float(0.75, title="Risk/Reward Ratio", step=0.05)  // Lower RRR to achieve a high win rate
riskPerTrade = input.float(2.0, title="Risk per Trade (%)", step=0.1) / 100  // 2% risk per trade

// Bollinger Bands Calculation
basis = ta.sma(close, bbLength)
dev = bbMult * ta.stdev(close, bbLength)
upperBand = basis + dev
lowerBand = basis - dev

// RSI Calculation
rsi = ta.rsi(close, rsiLength)

// ATR Calculation for Stop Loss
atr = ta.atr(atrLength)

// Entry Conditions: Mean Reversion
longCondition = close < lowerBand and rsi < rsiOversold
shortCondition = close > upperBand and rsi > rsiOverbought

// Stop Loss and Take Profit based on ATR
longStopLoss = close - atr * 1.0  // 1x ATR stop loss for long trades
shortStopLoss = close + atr * 1.0  // 1x ATR stop loss for short trades

longTakeProfit = close + (close - longStopLoss) * rrRatio  // 0.75x ATR take profit
shortTakeProfit = close - (shortStopLoss - close) * rrRatio  // 0.75x ATR take profit

// Calculate position size based on risk
equity = strategy.equity
riskAmount = equity * riskPerTrade
qtyLong = riskAmount / (close - longStopLoss)
qtyShort = riskAmount / (shortStopLoss - close)

// Long Trade
if (longCondition)
    strategy.entry("Long", strategy.long, qty=qtyLong)
    strategy.exit("Take Profit/Stop Loss", from_entry="Long", limit=longTakeProfit, stop=longStopLoss)

// Short Trade
if (shortCondition)
    strategy.entry("Short", strategy.short, qty=qtyShort)
    strategy.exit("Take Profit/Stop Loss", from_entry="Short", limit=shortTakeProfit, stop=shortStopLoss)

// Plot Bollinger Bands
plot(upperBand, color=color.red, linewidth=2, title="Upper Bollinger Band")
plot(lowerBand, color=color.green, linewidth=2, title="Lower Bollinger Band")
plot(basis, color=color.gray, linewidth=2, title="Bollinger Basis")

// Plot RSI for visual confirmation
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.green)
plot(rsi, color=color.purple, title="RSI")

```

> Detail

https://www.fmz.com/strategy/471689

> Last Modified

2024-11-12 14:45:46
