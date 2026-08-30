
> Name

Adaptive-Trend-Following-with-Dynamic-Risk-Control-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13b8e75ecdf100dd585.png)

[trans]
#### Overview
This strategy is a short-term trading system that combines multiple technical indicators. It is mainly based on the Parabolic Steering Index (PSAR) as the core signal. It also combines moving averages and momentum indicators for transaction filtering, and adopts a risk management method that combines dynamic stop loss and fixed take profit. The strategy design fully takes into account market trends and volatility, and is suitable for short-term trading in volatile market environments.
#### Strategy Principle
The strategy uses the PSAR indicator as the main trend judgment tool, and generates trading signals when the price breaks through PSAR. In order to improve the reliability of the signal, the following filter conditions are added:
1. The 50-period exponential moving average (EMA50) serves as a trend filter to ensure that the trading direction is consistent with the mid-term trend
2. The Relative Strength Index (RSI) is used to filter out volatile markets. Long positions require RSI>40, and short positions require RSI<60.
3. Use ATR (average true range) to dynamically calculate stop loss positions to provide more flexible risk control
4. Adopt a fixed profit-taking target of 0.7% to ensure that profits are pocketed in a timely manner.
5. Set up a position checking mechanism to avoid repeated opening of positions
#### Strategic Advantages
1. Complete signal system: combines trend tracking and momentum indicators to provide more reliable trading signals
2. Flexible risk control: dynamic stop loss can be adaptively adjusted according to market volatility
3. Prevent false breakthroughs: Multiple filtering conditions can effectively reduce the impact of false signals
4. Clear profit targets: fixed take-profit ratio helps control position holding time and improve capital utilization efficiency
5. Transaction logic is clear: each component has clear responsibilities to facilitate subsequent optimization and adjustment.
#### Strategy Risk
1. Excessive filtering risk: Multiple conditions may lead to missing some high-quality trading opportunities
2. Fixed take profit limit: 0.7% fixed take profit may exit a strong trend prematurely
3. Parameter sensitivity: The parameter settings of PSAR, EMA, RSI and other indicators have a greater impact on strategy performance.
4. Dependence on market environment: may perform poorly in low-volatility or violently volatile markets
5. Impact of slippage: Frequent transactions may lead to higher transaction costs
#### Strategy optimization direction
1. Dynamic take-profit mechanism: the take-profit ratio can be adjusted according to market volatility
2. Position management optimization: Introducing a dynamic position management system based on volatility
3. Market environment identification: Add a market environment judgment module to adjust strategy parameters under different market conditions.
4. Indicator parameter optimization: introduce an adaptive parameter adjustment mechanism to improve strategy adaptability
5. Transaction cost control: optimize the frequency of opening and closing positions and reduce transaction costs
#### Summary
This strategy builds a complete trading system by combining multiple technical indicators, and has good considerations in trend judgment, risk control and transaction execution. The core advantage of the strategy lies in its flexible risk control mechanism and complete signal system, but at the same time, attention must be paid to parameter optimization and market adaptability. Through continuous optimization and improvement, this strategy is expected to maintain stable performance in different market environments. ||
#### Overview
This strategy is a short-term trading system that combines multiple technical indicators, primarily based on the Parabolic SAR (PSAR) as the core signal generator, while incorporating moving averages and momentum indicators for trade filtering, along with a combination of dynamic stop-loss and fixed take-profit risk management methods. The strategy is designed to consider market trends and volatility, making it suitable for short-term trading in volatile market conditions.

#### Strategy Principles
The strategy uses the PSAR indicator as its primary trend determination tool, generating trading signals when price crosses the PSAR. To enhance signal reliability, the following filters are added:
1. 50-period Exponential Moving Average (EMA50) as a trend filter to ensure trade direction aligns with medium-term trends
2. Relative Strength Index (RSI) to filter out ranging markets, requiring RSI>40 for long positions and RSI<60 for short positions
3. Average True Range (ATR) for dynamic stop-loss calculation, providing more flexible risk control
4. Fixed 0.7% take-profit target to secure gains promptly
5. Position check mechanism to avoid duplicate entries

#### Strategy Advantages
1. Comprehensive signal system: Combines trend following and momentum indicators for more reliable trading signals
2. Flexible risk control: Dynamic stop-loss adapts to market volatility
3. False breakout prevention: Multiple filtering conditions effectively reduce the impact of false signals
4. Clear profit targets: Fixed take-profit ratio helps control holding time and improve capital efficiency
5. Clear trading logic: Well-defined component responsibilities facilitate subsequent optimization and adjustment

#### Strategy Risks
1. Over-filtering risk: Multiple conditions may cause missed trading opportunities
2. Fixed take-profit limitations: 0.7% fixed take-profit may exit strong trends too early
3. Parameter sensitivity: PSAR, EMA, RSI parameter settings significantly impact strategy performance
4. Market environment dependence: May underperform in low volatility or highly volatile markets
5. Slippage impact: Frequent trading may lead to higher transaction costs

#### Strategy Optimization Directions
1. Dynamic take-profit mechanism: Adjust profit targets based on market volatility
2. Position management optimization: Introduce volatility-based dynamic position sizing system
3. Market environment recognition: Add market state identification module to adjust strategy parameters accordingly
4. Indicator parameter optimization: Implement adaptive parameter adjustment mechanism
5. Transaction cost control: Optimize entry/exit frequency to reduce trading costs

#### Summary
The strategy builds a complete trading system by combining multiple technical indicators, with solid considerations in trend identification, risk control, and trade execution. Its core strengths lie in its flexible risk control mechanism and comprehensive signal system, while attention needs to be paid to parameter optimization and market adaptability. Through continuous optimization and improvement, the strategy has the potential to maintain stable performance across different market conditions.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-20 00:00:00
end: 2025-02-17 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("妮可百分百", overlay=true)

// ? 設定 Parabolic SAR 參數
start = input.float(0.02, "起始 AF")
increment = input.float(0.02, "加速因子")
maximum = input.float(0.2, "最大 AF")

// ? 計算 Parabolic SAR
SAR = ta.sar(start, increment, maximum)

// ? ATR 計算（用於動態止損）
atrLength = input.int(14, "ATR 計算週期")
atrMultiplier = input.float(1.3, "ATR 係數")  // 2倍 ATR 作為止損範圍
ATR = ta.atr(atrLength)

// ? 固定 0.5% 止盈計算
takeProfitPercent = 0.007  // 0.7% 固定止盈
takeProfitLong = close * (1 + takeProfitPercent)  // 多單止盈
takeProfitShort = close * (1 - takeProfitPercent) // 空單止盈

// ? **50 EMA 過濾**
ema50 = ta.ema(close, 50)

// ? **RSI 過濾（防止震盪進場）**
rsiLength = input.int(14, "RSI 週期")
rsi = ta.rsi(close, rsiLength)
longFilter = rsi > 40  // 只在 RSI > 31 時做多
shortFilter = rsi < 60 // 只在 RSI < 69 時做空

// ? **檢查是否已經有持倉**
isFlat = strategy.position_size == 0  // **無持倉時，才能開新單**

// ? **多頭進場條件**
longCondition = ta.crossover(close, SAR) and close > ema50 and longFilter and isFlat  

// ? **空頭進場條件**
shortCondition = ta.crossunder(close, SAR) and close < ema50 and shortFilter and isFlat  

// ? **進場策略**
if (longCondition)
    strategy.entry("B", strategy.long, comment="B")

if (shortCondition)
    strategy.entry("S", strategy.short, comment="S")

// ? **止盈 & 止損**
stopLossLong = close - (ATR * atrMultiplier)  // 多單 ATR 止損
stopLossShort = close + (ATR * atrMultiplier) // 空單 ATR 止損

strategy.exit("Exit Long", from_entry="B", stop=stopLossLong, limit=takeProfitLong, comment="TP Long")
strategy.exit("Exit Short", from_entry="S", stop=stopLossShort, limit=takeProfitShort, comment="TP Short")

// ? **標記進出場點**
plotshape(series=longCondition, location=location.belowbar, style=shape.triangleup, size=size.small, title="B")
plotshape(series=shortCondition, location=location.abovebar, style=shape.triangledown, size=size.small, title="S")

// ? **繪製 50 EMA**
plot(ema50, color=color.blue, title="50 EMA")

```

> Detail

https://www.fmz.com/strategy/482600

> Last Modified

2025-02-19 11:26:56
