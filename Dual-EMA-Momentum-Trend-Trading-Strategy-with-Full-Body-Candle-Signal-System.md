
> Name

Dual-EMA-Momentum-Trend-Trading-Strategy-with-Full-Body-Candle-Signal-System
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/0733578ed40b3b409242298fcc8d8276147407186e5842997bbfe89a1fbcc934.png)

[trans]
#### Overview
This strategy is a trend following system that combines technical analysis and price action. The core of the strategy is to use the 9-period and 15-period exponential moving averages (EMA) as trend direction indicators, and combine it with the full-body candle chart (Marubozu) as a momentum confirmation signal to form a complete trading decision-making system. By analyzing the intersection of moving averages and price trends, the strategy can capture the main trend changes in the market and trade at the right time.
#### Strategy Principle
The strategy uses a double filtering mechanism to confirm trading signals. First, use the 9-period and 15-period EMAs to determine the market trend direction. Second, by identifying full-body candlestick patterns as momentum confirmation signals. When a full body long candle appears and the closing price is above the two EMAs, the system generates a buy signal; when a full body short candle appears and the closing price is below the two EMAs, the system generates a sell signal. The criterion for a full body candle is that the body part accounts for at least 75% of the entire candle, which indicates that the market has shown a strong one-way movement during this period.
#### Strategic Advantages
1. High signal reliability: By combining the two-dimensional confirmation of moving average and full body candle, the reliability of trading signals is significantly improved.
2. Accurate trend grasp: The double moving average system can effectively identify market trends and avoid frequent trading in sideways markets.
3. Clear execution standards: The entry and exit conditions of the strategy are clear, making it easy to implement quantitatively
4. Improved risk control: The system’s built-in reverse signal closing mechanism effectively controls position risks.
5. Simple and intuitive operation: The strategy logic is simple, easy to understand and execute, and is suitable for all types of traders.
#### Strategy Risk
1. Lagging risk: The moving average indicator itself has lag, which may lead to a slight delay in entry timing.
2. Risk of false breakthrough: The market may have a false breakthrough, resulting in false signals
3. Sideways market risk: Frequent false signals may occur during market fluctuations
4. Instantaneous gap risk: A large gap may cause stop loss to become invalid.
5. Parameter optimization risk: There may be differences in optimal parameters under different market environments
#### Optimization direction
1. Introduce volatility filter: ATR indicator can be added to filter trading signals in low volatility environment
2. Optimize the moving average period: the moving average period parameters can be adjusted according to different market characteristics
3. Increase trend strength confirmation: trend strength indicators such as ADX can be introduced as auxiliary judgments
4. Improve the stop loss mechanism: you can add a trailing stop loss function to better protect profits
5. Add market environment filtering: introduce a market status judgment mechanism to automatically reduce the trading frequency in sideways markets
#### Summary
This strategy builds a robust trend-following trading system by combining a moving average system and full-body candle signals. The strategy design fully considers the two dimensions of trend confirmation and momentum confirmation, and has good reliability and practicality. Through reasonable optimization and risk control measures, strategies can maintain stable performance in different market environments. Overall, this is a trading strategy system with rigorous logic and strong practicality.
||

#### Overview
This strategy is a trend following system that combines technical analysis and price action. The core of the strategy utilizes 9-period and 15-period Exponential Moving Averages (EMA) as trend direction indicators, while incorporating full body candles (Marubozu) as momentum confirmation signals to form a complete trading decision system. Through analysis of moving average crossovers and price action, the strategy can capture major market trend changes and execute trades at appropriate times.

#### Strategy Principles
The strategy employs a dual filtering mechanism to confirm trading signals. First, it uses 9-period and 15-period EMAs to determine market trend direction. Second, it identifies full body candle patterns as momentum confirmation signals. A buy signal is generated when a full body bullish candle closes above both EMAs, while a sell signal is triggered when a full body bearish candle closes below both EMAs. A full body candle is defined as having its body occupy at least 75% of the total candle length, indicating strong unidirectional market movement during that period.

#### Strategy Advantages
1. High Signal Reliability: Combining EMAs and full body candles significantly improves trading signal reliability
2. Accurate Trend Capture: The dual EMA system effectively identifies market trends, avoiding frequent trading in ranging markets
3. Clear Execution Standards: Strategy entry and exit conditions are well-defined, facilitating quantitative implementation
4. Comprehensive Risk Control: Built-in reverse signal closing mechanism effectively controls position risk
5. Simple and Intuitive Operation: Strategy logic is simple to understand and execute, suitable for various types of traders

#### Strategy Risks
1. Lag Risk: Moving averages inherently have lag, potentially causing delayed entry timing
2. False Breakout Risk: Markets may exhibit false breakouts leading to incorrect signals
3. Range-bound Market Risk: Frequent false signals may occur during market consolidation periods
4. Gap Risk: Large price gaps may render stop losses ineffective
5. Parameter Optimization Risk: Optimal parameters may vary across different market environments

#### Optimization Directions
1. Introduce Volatility Filter: Add ATR indicator to filter trading signals in low volatility environments
2. Optimize Moving Average Periods: Adjust EMA periods according to different market characteristics
3. Add Trend Strength Confirmation: Incorporate ADX or similar trend strength indicators as auxiliary judgment tools
4. Improve Stop Loss Mechanism: Add trailing stop loss functionality for better profit protection
5. Add Market Environment Filter: Introduce market state judgment mechanism to automatically reduce trading frequency in ranging markets

#### Summary
This strategy builds a robust trend following trading system by combining moving average systems with full body candle signals. The strategy design fully considers both trend confirmation and momentum confirmation dimensions, offering good reliability and practicality. Through appropriate optimization and risk control measures, the strategy can maintain stable performance across different market environments. Overall, this is a logically rigorous and highly practical trading strategy system.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-25 00:00:00
end: 2024-11-24 00:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("9 & 15 EMA with Full Body Candle Strategy", overlay=true)

// Input parameters for EMAs
ema9Length = input.int(9, title="9-period EMA")
ema15Length = input.int(15, title="15-period EMA")

// Calculate the 9-period and 15-period EMAs
ema9 = ta.ema(close, ema9Length)
ema15 = ta.ema(close, ema15Length)

// Define full body (marubozu) candle conditions
fullBodyBullishCandle = (close > open) and (close - open >= (high - low) * 0.75)
fullBodyBearishCandle = (close < open) and (open - close >= (high - low) * 0.75)

// Buy condition: Full body candle closes above both EMAs
buySignal = fullBodyBullishCandle and close > ema9 and close > ema15

// Sell condition: Full body candle closes below both EMAs
sellSignal = fullBodyBearishCandle and close < ema9 and close < ema15

// Plot the EMAs on the chart
plot(ema9, color=color.blue, linewidth=2, title="9-period EMA")
plot(ema15, color=color.orange, linewidth=2, title="15-period EMA")

// Plot buy and sell signals
plotshape(series=buySignal, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY", size=size.small)
plotshape(series=sellSignal, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL", size=size.small)

// Execute buy and sell strategy
if (buySignal)
    strategy.entry("Buy", strategy.long)

if (sellSignal)
    strategy.entry("Sell", strategy.short)

// Close buy position on sell signal
if (sellSignal)
    strategy.close("Buy")

// Close sell position on buy signal
if (buySignal)
    strategy.close("Sell")

```

> Detail

https://www.fmz.com/strategy/472974

> Last Modified

2024-11-25 17:30:46
