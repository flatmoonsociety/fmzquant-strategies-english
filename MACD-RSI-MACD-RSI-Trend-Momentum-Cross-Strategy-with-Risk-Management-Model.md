
> Name

MACD-RSI Trend Momentum Cross Strategy with Risk Management Model-MACD-RSI-Trend-Momentum-Cross-Strategy-with-Risk-Management-Model
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/127c9a06a2cad94a436.png)

[trans]
#### Overview
This strategy is a trend following trading system that combines MACD (Moving Average Convergence Divergence) and RSI (Relative Strength Index). The strategy operates on a 5-minute timeframe and generates trading signals by analyzing MACD crossovers with the signal line and RSI overbought and oversold levels. Percent-based stop-loss and profit-taking mechanisms are also integrated for risk management.
#### Strategy Principle
The strategy is mainly based on the following core logic:
1. Capture price trends using the MACD indicator set with 12-26-9 parameters
2. Use the 14-period RSI indicator to identify overbought and oversold conditions.
3. When the MACD line crosses the signal line and the RSI is below 45, a long signal is triggered
4. When the MACD line crosses the signal line and the RSI is higher than 55, a closing signal is triggered
5. Set a 1.2% stop loss to control risks and a 2.4% stop profit to lock in profits.
6. Use 10-period EMA as a trend filter to improve signal quality
#### Strategic Advantages
1. Advantages of indicator combination: combined with MACD trend tracking characteristics and RSI fluctuation characteristics, it can more accurately capture market turning points
2. Perfect risk control: adopt a fixed proportion of stop loss and stop profit, and strictly control the risk of a single transaction
3. Signal confirmation mechanism: Both MACD and RSI conditions must be met before opening a position to reduce false signals
4. Strong adaptability: can adapt to different market environments through parameter adjustment
5. Clear execution logic: clear trading rules and easy to automate
#### Strategy Risk
1. Volatile market risk: In a volatile market, frequent transactions may result in losses.
2. Slippage risk: Frequent transactions in the 5-minute cycle may lead to greater slippage
3. Risk of false breakthrough: MACD cross signal may have a false breakthrough
4. Parameter sensitivity: indicator parameter settings have a greater impact on strategy performance
5. Market environment dependence: Strategies perform better in markets with clear trends
#### Strategy optimization direction
1. Add trading volume filtering: consider trading volume factors when generating signals to improve signal reliability
2. Dynamic stop loss setting: adaptively adjust the stop loss ratio according to market volatility
3. Introduce trend strength filtering: add trend strength indicators such as ADX to optimize trading opportunities
4. Improve position management: realize dynamic position control based on volatility
5. Optimization parameter adaptation: develop dynamic parameter optimization mechanism to improve strategy adaptability
#### Summary
This strategy combines the advantages of MACD and RSI to build a trading system with both trend following and momentum characteristics. The perfect risk control mechanism and clear transaction logic make it highly practical. Through the suggested optimization directions, there is room for further improvement of the strategy. When applying in real market, it is recommended to conduct sufficient backtest verification first and adjust the parameters appropriately according to the specific market characteristics. ||
#### Overview
This strategy is a trend-following trading system that combines MACD (Moving Average Convergence Divergence) and RSI (Relative Strength Index). Operating on a 5-minute timeframe, it generates trading signals by analyzing MACD crossovers and RSI overbought/oversold levels. The strategy incorporates percentage-based stop-loss and take-profit mechanisms for risk management.

#### Strategy Principles
The strategy is based on the following core logic:
1. Uses MACD indicator with 12-26-9 parameters to capture price trends
2. Employs 14-period RSI to identify overbought/oversold conditions
3. Generates long signals when MACD line crosses above signal line and RSI is below 45
4. Triggers exit signals when MACD line crosses below signal line and RSI is above 55
5. Sets 1.2% stop-loss for risk control and 2.4% take-profit to secure gains
6. Uses 10-period EMA as trend filter to improve signal quality

#### Strategy Advantages
1. Indicator Combination: Merges MACD's trend-following characteristics with RSI's oscillation properties for more accurate market turning points
2. Comprehensive Risk Control: Uses fixed-ratio stop-loss and take-profit to strictly control single trade risk
3. Signal Confirmation: Requires both MACD and RSI conditions for entry, reducing false signals
4. High Adaptability: Can be adjusted through parameters to suit different market conditions
5. Clear Execution Logic: Trading rules are explicit and easy to automate

#### Strategy Risks
1. Choppy Market Risk: May generate frequent trades leading to losses in ranging markets
2. Slippage Risk: Frequent trading on 5-minute timeframe may face significant slippage
3. False Breakout Risk: MACD crossover signals may produce false breakouts
4. Parameter Sensitivity: Strategy performance heavily depends on indicator parameter settings
5. Market Environment Dependency: Strategy performs better in clear trending markets

#### Strategy Optimization Directions
1. Add Volume Filters: Consider volume factors in signal generation to improve reliability
2. Dynamic Stop-Loss: Implement adaptive stop-loss based on market volatility
3. Introduce Trend Strength Filter: Add ADX or similar indicators to optimize trading timing
4. Improve Position Management: Implement volatility-based dynamic position sizing
5. Optimize Parameter Adaptation: Develop dynamic parameter optimization mechanism

#### Summary
This strategy builds a trading system combining trend-following and momentum characteristics through MACD and RSI integration. Its comprehensive risk control mechanisms and clear trading logic provide good practicality. Through suggested optimization directions, the strategy has room for further improvement. Before live trading, it's recommended to conduct thorough backtesting and adjust parameters according to specific market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-11 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
//@version=5
strategy("MACD + RSI Basit Strateji", overlay=true, initial_capital=1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// İndikatör parametreleri
fastLength = input(12, "MACD Fast Length")
slowLength = input(26, "MACD Slow Length")
signalLength = input(9, "MACD Signal Length")
rsiLength = input(14, "RSI Period")
rsiOversold = input(45, "RSI Oversold Level")
rsiOverbought = input(55, "RSI Overbought Level")

// Stop Loss ve Take Profit ekledim
stopLoss = input(1.2, "Stop Loss (%)")
takeProfit = input(2.4, "Take Profit (%)")

// MACD hesaplama
[macdLine, signalLine, histLine] = ta.macd(close, fastLength, slowLength, signalLength)

// RSI hesaplama
rsiValue = ta.rsi(close, rsiLength)

// EMA trend filtresi
emaValue = ta.ema(close, 10)

// Alım sinyali koşulları - sadece MACD ve RSI kullanalım
longCondition = macdLine > signalLine and rsiValue < rsiOversold

// Satım sinyali koşulları
shortCondition = macdLine < signalLine and rsiValue > rsiOverbought

// Pozisyon yönetimi - Stop Loss ve Take Profit ekledim
if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("TP/SL", "Long", 
                 profit = close * takeProfit / 100,
                 loss = close * stopLoss / 100)

if (shortCondition)
    strategy.close("Long")

// Grafik göstergeleri
plotshape(longCondition, title="Alım", 
         style=shape.triangleup, 
         location=location.belowbar, 
         color=color.green, 
         size=size.large, 
         text="AL")

plotshape(shortCondition, title="Satım", 
         style=shape.triangledown, 
         location=location.abovebar, 
         color=color.red, 
         size=size.large, 
         text="SAT")

// İndikatörleri göster
plot(rsiValue, "RSI", color=color.purple)
hline(rsiOversold, "Oversold", color=color.gray)
hline(rsiOverbought, "Overbought", color=color.gray)
```

> Detail

https://www.fmz.com/strategy/474960

> Last Modified

2024-12-13 10:35:00
