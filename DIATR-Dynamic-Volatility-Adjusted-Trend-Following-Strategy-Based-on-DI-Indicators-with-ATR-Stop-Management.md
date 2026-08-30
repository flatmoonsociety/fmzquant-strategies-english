
> Name

Dynamic-Volatility-Adjusted-Trend-Following-Strategy-Based-on-DI-Indicators-with-ATR-Stop-Management
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/147db016b817dfdd444.png)

[trans]
#### Overview
This strategy is a trend following system that combines the Trend Index (DMI) and the Average True Range (ATR). The core of the strategy is to identify the direction and intensity of the market trend through DI+ and DI- indicators, and use ATR to dynamically adjust the stop-profit and stop-loss positions. By introducing trend filtered moving averages as auxiliary confirmations, the reliability of trading signals is further improved. The strategy design fully takes into account market volatility and has good adaptability.
#### Strategy Principle
Strategy operation is based on the following core mechanisms:
1. Use the DI+ and DI- indicators to measure trend direction and strength. When DI+ is higher than DI- and the difference exceeds the threshold, it indicates that the upward trend is established; otherwise, the downward trend is confirmed.
2. Introduce the trend filtered moving average (SMA) as a trend confirmation tool. The signal is triggered only when the price and moving average position confirm each other. 
3. Use the ATR indicator to dynamically calculate stop loss and take profit positions to ensure that risk management can adapt to different market environments.
4. Strictly follow time limits when executing transactions to avoid too frequent transactions.
#### Strategic Advantages
1. Strong dynamic adjustment ability - ATR enables adaptation to market fluctuations.
2. Improved risk control - a dynamic stop-loss and stop-profit mechanism based on volatility is set up. 
3. High signal reliability - Reduce false signals through cross-validation of multiple indicators.
4. Flexible and adjustable parameters - strategy parameters can be optimized according to different market characteristics.
5. The execution logic is clear - the entry and exit conditions are clear, making it easy to operate.
#### Strategy Risk
1. Risk of volatile market - Continuous stop losses may occur during range-bound market fluctuations.
Suggestion: Add oscillator filtering or adjust parameter thresholds.
2. Risk of slippage - you may face larger slippage during times of severe volatility.
Suggestion: Appropriately relax the stop loss position and reserve room for slippage.
3. False breakout risk - misjudgments may occur at trend turning points.
Suggestion: Combine with trading volume and other indicators to confirm the signal.
4. Parameter sensitivity - the performance of different parameter combinations varies greatly.
Suggestion: Find parameter intervals with strong stability through backtesting.
#### Strategy optimization direction
1. Signal optimization - ADX indicator can be introduced to evaluate the strength of the trend, or a trading volume confirmation mechanism can be added.
2. Position management - Position size can be dynamically adjusted based on trend strength to achieve more sophisticated risk control.
3. Time structure - multi-time period analysis can be considered to enhance signal reliability.
4. Market adaptability - an adaptive parameter adjustment mechanism can be developed according to the characteristics of different varieties.
#### Summary
This strategy achieves dynamic tracking of trends and risk control by combining trend indicators and volatility indicators. The strategic design focuses on practicality and operability, and has strong market adaptability. There is room for further improvement of the strategy through parameter optimization and signal improvement. It is recommended that investors need to fully test the actual application and make targeted adjustments according to specific market characteristics.
|| 

#### Overview
This strategy is a trend following system that combines the Directional Movement Index (DMI) with Average True Range (ATR). The core mechanism uses DI+ and DI- indicators to identify market trend direction and strength, while utilizing ATR for dynamic stop-loss and take-profit adjustments. The introduction of a trend filtering moving average further enhances signal reliability. The strategy design considers market volatility and demonstrates good adaptability.

#### Strategy Principle
The strategy operates based on the following core mechanisms:
1. Uses DI+ and DI- indicators to measure trend direction and strength. When DI+ exceeds DI- by the threshold value, an uptrend is confirmed; vice versa for downtrends.
2. Incorporates a trend filtering moving average (SMA) as a trend confirmation tool. Signals are only triggered when price and moving average positions mutually confirm.
3. Utilizes ATR indicator to dynamically calculate stop-loss and take-profit levels, ensuring risk management adapts to different market conditions.
4. Strictly follows time restrictions in trade execution to avoid excessive trading frequency.

#### Strategy Advantages
1. Strong Dynamic Adjustment - Achieves market volatility adaptation through ATR.
2. Comprehensive Risk Control - Implements volatility-based dynamic stop-loss and take-profit mechanisms.
3. High Signal Reliability - Reduces false signals through multiple indicator cross-validation.
4. Flexible Parameters - Strategy parameters can be optimized for different market characteristics.
5. Clear Execution Logic - Precise entry and exit conditions facilitate real-world implementation.

#### Strategy Risks
1. Oscillation Market Risk - May result in consecutive stops in range-bound markets.
Suggestion: Add oscillation indicators for filtering or adjust parameter thresholds.

2. Slippage Risk - May face significant slippage during high volatility periods.
Suggestion: Appropriately widen stop-loss positions to accommodate slippage.

3. False Breakout Risk - Potential misjudgments at trend turning points.
Suggestion: Incorporate volume indicators for signal confirmation.

4. Parameter Sensitivity - Performance varies significantly with different parameter combinations.
Suggestion: Find stable parameter ranges through backtesting.

#### Strategy Optimization Directions
1. Signal Optimization - Consider introducing ADX indicator for trend strength evaluation or adding volume confirmation mechanisms.

2. Position Management - Implement dynamic position sizing based on trend strength for more refined risk control.

3. Time Structure - Consider multi-timeframe analysis to enhance signal reliability.

4. Market Adaptability - Develop adaptive parameter adjustment mechanisms based on different instrument characteristics.

#### Summary
This strategy achieves dynamic trend following and risk control by combining directional and volatility indicators. The strategy design emphasizes practicality and operability, demonstrating strong market adaptability. Through parameter optimization and signal improvements, there is room for further enhancement. Investors are advised to thoroughly test and make specific adjustments based on market characteristics before implementation.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-04 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("使用 DI+ 和 DI- 的策略 (最終完整修正且含圖表止損止盈線)", overlay=true)

// 輸入參數
diLength = input.int(title="DI 長度", defval=14)
adxSmoothing = input.int(title="ADX Smoothing", defval=14)
trendFilterLength = input.int(title="趨勢過濾均線長度", defval=20)
strengthThreshold = input.int(title="趨勢強度門檻值", defval=20)
atrLength = input.int(title="ATR 長度", defval=14)
atrMultiplierStop = input.float(title="ATR 停損倍數", defval=1.5)
atrMultiplierTakeProfit = input.float(title="ATR 止盈倍數", defval=2.5)

// 計算 DI+ 和 DI-
[diPlus, diMinus, _] = ta.dmi(diLength, adxSmoothing)

// 計算趨勢過濾均線
trendFilterMA = ta.sma(close, trendFilterLength)

// 判斷趨勢方向和強度
strongUpTrend = diPlus > diMinus + strengthThreshold and close > trendFilterMA
strongDownTrend = diMinus > diPlus + strengthThreshold and close < trendFilterMA

// 計算 ATR
atr = ta.atr(atrLength)

// 追蹤止損止盈價格 (使用 var 宣告，只在進場時更新)
var float longStopPrice = na
var float longTakeProfitPrice = na
var float shortStopPrice = na
var float shortTakeProfitPrice = na

// 進場邏輯
longCondition = strongUpTrend
shortCondition = strongDownTrend

if (longCondition)
    strategy.entry("多單", strategy.long)
    longStopPrice := close - atr * atrMultiplierStop // 進場時計算並更新止損價
    longTakeProfitPrice := close + atr * atrMultiplierTakeProfit // 進場時計算並更新止盈價

if (shortCondition)
    strategy.entry("空單", strategy.short)
    shortStopPrice := close + atr * atrMultiplierStop // 進場時計算並更新止損價
    shortTakeProfitPrice := close - atr * atrMultiplierTakeProfit // 進場時計算並更新止盈價


// 出場邏輯 (使用 time 限制和 ATR)
inLongPosition = strategy.position_size > 0
inShortPosition = strategy.position_size < 0

lastEntryTime = strategy.opentrades.entry_bar_index(strategy.opentrades - 1)

if (inLongPosition and time > lastEntryTime)
    strategy.exit("多單出場", "多單", stop=longStopPrice, limit=longTakeProfitPrice)

if (inShortPosition and time > lastEntryTime)
    strategy.exit("空單出場", "空單", stop=shortStopPrice, limit=shortTakeProfitPrice)

// 繪製 DI+、DI- 和趨勢過濾均線
plot(diPlus, color=color.green, title="DI+")
plot(diMinus, color=color.red, title="DI-")
plot(trendFilterMA, color=color.blue, title="趨勢過濾均線")

// 繪製止損止盈線 (使用 plot 函數繪製)
plot(strategy.position_size > 0 ? longStopPrice : na, color=color.red, style=plot.style_linebr, linewidth=2, title="多單停損")
plot(strategy.position_size > 0 ? longTakeProfitPrice : na, color=color.green, style=plot.style_linebr, linewidth=2, title="多單止盈")
plot(strategy.position_size < 0 ? shortStopPrice : na, color=color.red, style=plot.style_linebr, linewidth=2, title="空單停損")
plot(strategy.position_size < 0 ? shortTakeProfitPrice : na, color=color.green, style=plot.style_linebr, linewidth=2, title="空單止盈")
```

> Detail

https://www.fmz.com/strategy/477595

> Last Modified

2025-01-06 16:18:01
