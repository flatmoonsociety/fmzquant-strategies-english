
> Name

Multi-Indicator Fusion-Mean-Reversion-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12696c94368f5088d68.png)

[trans]
#### Overview
This strategy is a quantitative trading strategy that combines mean reversion and trend tracking. It mainly uses the three technical indicators of MA, MACD and ATR to achieve the generation of trading signals and risk control. The core idea of ​​the strategy is to use the cross signal of the MACD indicator to capture market reversal opportunities when the price deviates from the moving average, and at the same time use ATR dynamic stop loss to control risks.
#### Strategy Principle
The strategy uses a triple verification mechanism:
1. Use the moving average (MA) to determine the degree of price deviation. You can choose SMA or EMA.
2. Determine the timing of trend reversal through the golden cross and dead cross of the MACD indicator.
3. Use the ATR indicator to dynamically set stop loss positions
Specifically, when the price is lower than the moving average and MACD is a golden cross, a long position is opened; when the price is above the moving average and the MACD is a dead cross, a short position is opened. At the same time, the stop loss position is automatically set according to the volatility of ATR.
#### Strategic Advantages
1. High signal reliability: verified by multiple indicators to reduce false signal interference
2. Improve risk control: use ATR dynamic stop loss to avoid major retracement
3. Flexible and adjustable parameters: parameters can be adjusted according to different market characteristics
4. The strategy logic is clear: the entry and exit conditions are clear and easy to understand and execute.
5. Strong adaptability: can be applied to different time periods and market environments
#### Strategy Risk
1. A volatile market may result in frequent transactions, increasing costs.
2. Response to trend turning points may be delayed
3. Parameter optimization has the risk of overfitting
4. Stop loss may have larger slippage when the market fluctuates violently.
5. Using multiple indicators at the same time may reduce strategy efficiency.
#### Strategy optimization direction
1. Introduce trading volume indicators to improve signal reliability
2. Add trend strength filter to avoid weak market conditions
3. Optimize the stop loss mechanism and consider trailing stop
4. Add volatility filtering to adjust positions during periods of high volatility
5. Develop adaptive parameter mechanism to improve strategy stability
#### Summary
This strategy achieves a relatively robust trading system through a combination of mean reversion and trend following. The verification mechanism of multiple indicators improves the reliability of trading signals, while the ATR dynamic stop loss controls risks well. Although there is some room for optimization, overall it is a strategic framework with clear logic and strong practicality.
|| 

#### Overview
This strategy combines mean reversion and trend following approaches, utilizing MA, MACD, and ATR technical indicators for generating trading signals and risk control. The core concept is to capture market reversals when price deviates from moving averages, confirmed by MACD crossover signals, while implementing ATR-based dynamic stop-loss for risk management.

#### Strategy Principles
The strategy employs a triple verification mechanism:
1. Using Moving Average (MA) to assess price deviation, with options for SMA or EMA
2. Utilizing MACD crossovers to identify trend reversal timing
3. Implementing ATR indicator for dynamic stop-loss placement
Specifically, long positions are initiated when price is below MA with MACD golden cross, while short positions are triggered when price is above MA with MACD death cross. Stop-loss levels are automatically set based on ATR volatility.

#### Strategy Advantages
1. High signal reliability: Multiple indicator verification reduces false signals
2. Comprehensive risk control: ATR dynamic stop-loss prevents significant drawdowns
3. Flexible parameters: Adjustable based on different market characteristics
4. Clear strategy logic: Explicit entry and exit conditions
5. Strong adaptability: Applicable to various timeframes and market conditions

#### Strategy Risks
1. Frequent trading in choppy markets may increase costs
2. Possible lag in trend reversal detection
3. Parameter optimization risks overfitting
4. Potential slippage during high volatility periods
5. Multiple indicators may reduce strategy efficiency

#### Optimization Directions
1. Incorporate volume indicators for enhanced signal reliability
2. Add trend strength filters to avoid weak market conditions
3. Optimize stop-loss mechanism, consider trailing stops
4. Include volatility filters to adjust positions during high volatility periods
5. Develop adaptive parameter mechanisms for improved stability

#### Summary
This strategy achieves a relatively robust trading system by combining mean reversion and trend following approaches. The multiple indicator verification mechanism enhances trading signal reliability, while ATR dynamic stop-loss effectively controls risk. Despite some room for optimization, it represents a logically sound and practical strategy framework.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-01 00:00:00
end: 2024-10-31 23:59:59
period: 3h
basePeriod: 3h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Mean Reversion Strategy with ATR, MACD and MA", overlay=true)

// === Настройки для индикаторов ===
// Параметры скользящей средней (MA)
maLength = input.int(30, title="Период скользящей средней (MA)")
maType = input.string("EMA", title="Тип скользящей средней", options=["SMA", "EMA"])

// Параметры ATR
atrLength = input.int(10, title="Период ATR")
atrMultiplier = input.float(10, title="ATR множитель для стоп-лосса")

// Параметры MACD
macdFastLength = input.int(8, title="Период быстрой EMA для MACD")
macdSlowLength = input.int(26, title="Период медленной EMA для MACD")
macdSignalLength = input.int(5, title="Период сигнальной линии MACD")

// === Рассчёт индикаторов ===
// Скользящая средняя
ma = if maType == "SMA"
    ta.sma(close, maLength)
else
    ta.ema(close, maLength)

// ATR (Средний истинный диапазон)
atr = ta.atr(atrLength)

// MACD
[macdLine, signalLine, _] = ta.macd(close, macdFastLength, macdSlowLength, macdSignalLength)

// Условия для входа на покупку и продажу
longCondition = ta.crossover(macdLine, signalLine) and close < ma
shortCondition = ta.crossunder(macdLine, signalLine) and close > ma

// === Управление позициями ===
if (longCondition)
    strategy.entry("Buy", strategy.long)
    // Стоп-лосс на основе ATR
    stopLossLevel = close - atr * atrMultiplier
    strategy.exit("Take Profit/Stop Loss", "Buy", stop=stopLossLevel)

if (shortCondition)
    strategy.entry("Sell", strategy.short)
    // Стоп-лосс на основе ATR
    stopLossLevel = close + atr * atrMultiplier
    strategy.exit("Take Profit/Stop Loss", "Sell", stop=stopLossLevel)

// Визуализация
plot(ma, title="MA", color=color.blue, linewidth=2)
plot(macdLine, title="MACD Line", color=color.green)
plot(signalLine, title="Signal Line", color=color.red)
hline(0, "Zero Line", color=color.gray)


```

> Detail

https://www.fmz.com/strategy/471687

> Last Modified

2024-11-12 14:30:35
