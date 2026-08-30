
> Name

Dual-EMA-Stochastic-Oscillator-System-A-Quantitative-Trading-Model-Combining-Trend-Following-and-Momentum
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/793cea9f9600e91a15.png)

[trans]
#### Overview
This strategy is a quantitative trading system that combines a double exponential moving average (EMA) and a stochastic oscillator. Use the 20-period and 50-period EMA to determine the market trend, use the stochastic oscillator to find trading opportunities in overbought and oversold areas, and achieve the perfect combination of trend and momentum. The strategy employs strict risk management measures, including fixed stop loss and profit target settings.
#### Strategy Principle
The core logic of the strategy is divided into three parts: trend judgment, entry timing and risk control. Trend judgment mainly relies on the relative positions of the fast EMA (20 periods) and the slow EMA (50 periods). When the fast line is above the slow line, it is judged to be an upward trend, and vice versa. Entry signals are confirmed by the cross of the stochastic oscillator, looking for high-probability trading opportunities in overbought and oversold areas. Risk control adopts the setting of fixed percentage stop loss and 2 times take profit ratio to ensure that each transaction has a clear risk-return ratio.
#### Strategic Advantages
1. Combine trend tracking and momentum indicators to obtain stable profits in trending markets
2. Adopt scientific fund management methods and control the loss of each transaction through a fixed risk ratio.
3. Indicator parameters can be flexibly adjusted according to different market characteristics.
4. The strategy has clear logic and is easy to understand and execute.
5. Suitable for trading in multiple time periods
#### Strategy Risk
1. Frequent false signals may occur in volatile markets
2. The choice of EMA parameters will affect strategy performance
3. The overbought and oversold settings of the stochastic oscillator need to be adjusted for specific markets.
4. Stops may be too wide in fast-moving markets
5. The impact of transaction costs on strategy returns needs to be considered
#### Strategy optimization direction
1. Add trading volume indicator as auxiliary confirmation
2. Introduce ATR indicator to dynamically adjust stop loss position
3. Adaptively adjust indicator parameters according to market volatility
4. Add trend strength filter to reduce false signals
5. Develop adaptive profit target calculation methods
#### Summary
This strategy builds a complete trading system by combining trend and momentum indicators. The core advantage of the strategy lies in its clear logical framework and strict risk control, but in actual application, parameter optimization still needs to be carried out based on specific market conditions. Through continuous improvement and optimization, the strategy is expected to maintain stable performance in various market environments.
|| 

#### Overview
This strategy is a quantitative trading system that combines dual Exponential Moving Averages (EMA) with the Stochastic Oscillator. It utilizes 20-period and 50-period EMAs to determine market trends while using the Stochastic Oscillator to identify trading opportunities in overbought and oversold zones, achieving a perfect blend of trend and momentum. The strategy implements strict risk management measures, including fixed stop-loss and profit targets.

#### Strategy Principles
The core logic consists of three components: trend identification, entry timing, and risk control. Trend identification primarily relies on the relative position of fast EMA (20-period) and slow EMA (50-period), where an uptrend is confirmed when the fast line is above the slow line, and vice versa. Entry signals are confirmed by Stochastic Oscillator crossovers, seeking high-probability trades in overbought and oversold zones. Risk control employs fixed percentage stop-losses and 2:1 profit targets, ensuring clear risk-reward ratios for each trade.

#### Strategy Advantages
1. Combines trend following and momentum indicators for consistent profits in trending markets
2. Implements scientific money management through fixed risk percentages
3. Indicator parameters can be flexibly adjusted for different markets
4. Clear and easy-to-understand strategy logic
5. Applicable across multiple timeframes

#### Strategy Risks
1. May generate frequent false signals in ranging markets
2. EMA parameter selection significantly impacts strategy performance
3. Stochastic overbought/oversold levels need market-specific adjustment
4. Stop-loss levels may be too wide in volatile markets
5. Trading costs need to be considered for strategy profitability

#### Optimization Directions
1. Add volume indicators for additional confirmation
2. Incorporate ATR for dynamic stop-loss adjustment
3. Develop adaptive parameter adjustment based on market volatility
4. Implement trend strength filters to reduce false signals
5. Develop adaptive profit target calculation methods

#### Summary
This strategy establishes a complete trading system by combining trend and momentum indicators. Its core strengths lie in its clear logical framework and strict risk control, though practical application requires parameter optimization based on specific market conditions. Through continuous improvement and optimization, the strategy has the potential to maintain stable performance across various market environments.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-06 00:00:00
end: 2025-01-04 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("EMA + Stochastic Strategy", overlay=true)

// Inputs for EMA
emaShortLength = input.int(20, title="Short EMA Length")
emaLongLength = input.int(50, title="Long EMA Length")

// Inputs for Stochastic
stochK = input.int(14, title="Stochastic %K Length")
stochD = input.int(3, title="Stochastic %D Smoothing")
stochOverbought = input.int(85, title="Stochastic Overbought Level")
stochOversold = input.int(15, title="Stochastic Oversold Level")

// Inputs for Risk Management
riskRewardRatio = input.float(2.0, title="Risk-Reward Ratio")
stopLossPercent = input.float(1.0, title="Stop Loss (%)")

// EMA Calculation
emaShort = ta.ema(close, emaShortLength)
emaLong = ta.ema(close, emaLongLength)

// Stochastic Calculation
k = ta.stoch(high, low, close, stochK)
d = ta.sma(k, stochD)

// Trend Condition
isUptrend = emaShort > emaLong
isDowntrend = emaShort < emaLong

// Stochastic Signals
stochBuyCrossover = ta.crossover(k, d)
stochBuySignal = k < stochOversold and stochBuyCrossover
stochSellCrossunder = ta.crossunder(k, d)
stochSellSignal = k > stochOverbought and stochSellCrossunder

// Entry Signals
buySignal = isUptrend and stochBuySignal
sellSignal = isDowntrend and stochSellSignal

// Strategy Execution
if buySignal
    strategy.entry("Buy", strategy.long)
    stopLoss = close * (1 - stopLossPercent / 100)
    takeProfit = close * (1 + stopLossPercent * riskRewardRatio / 100)
    strategy.exit("Take Profit/Stop Loss", from_entry="Buy", stop=stopLoss, limit=takeProfit)

if sellSignal
    strategy.entry("Sell", strategy.short)
    stopLoss = close * (1 + stopLossPercent / 100)
    takeProfit = close * (1 - stopLossPercent * riskRewardRatio / 100)
    strategy.exit("Take Profit/Stop Loss", from_entry="Sell", stop=stopLoss, limit=takeProfit)

// Plotting
plot(emaShort, color=color.blue, title="Short EMA")
plot(emaLong, color=color.red, title="Long EMA")
```

> Detail

https://www.fmz.com/strategy/477533

> Last Modified

2025-01-06 11:48:55
