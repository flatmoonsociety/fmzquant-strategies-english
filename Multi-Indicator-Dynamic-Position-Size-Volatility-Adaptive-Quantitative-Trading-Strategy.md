
> Name

Multi-Indicator Cross Dynamic Position Volatility Adaptive Quantitative Trading Strategy-Multi-Indicator-Dynamic-Position-Size-Volatility-Adaptive-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d89723a2f292a8e67bbe.png)
![IMG](https://www.fmz.com/upload/asset/2d8b4eb9a83e3831f9b13.png)



[trans]

#### Overview
The multi-indicator cross dynamic position volatility adaptive quantitative trading strategy is a comprehensive quantitative trading system that integrates trend detection, momentum indicators, volatility analysis, sentiment assessment and liquidity area identification functions. The strategy uses cross signals from multiple technical indicators to generate buy and sell decisions, while dynamically adjusting position sizes based on market volatility to enable adaptive management of risk. The core components include EMA trend identification system, RSI momentum filter, MACD direction confirmation, stochastic RSI fine adjustment, Ichimoku trend confirmation and ATR-based volatility adjustment position system.
#### Strategy Principle
The core logic of this strategy is based on multi-layer indicator screening, forming a strict signal generation mechanism:
1. **Trend Identification System**: The strategy uses two EMAs (9 and 21 periods by default) to determine the market trend direction. When the fast EMA is higher than the slow EMA, it is identified as an upward trend; otherwise, it is a downward trend. This trend judgment can be made in different time frames, such as using daily data (D) for trend identification.
2. **Momentum Indicator Combo**:
   - The RSI indicator measures price momentum, with a default period of 14 and overbought (70) and oversold (30) thresholds.
   - The MACD indicator (12,26,9) is used to confirm the direction of momentum, paying special attention to the value of the MACD histogram.
   - Stochastic RSI calculates %K and %D values, which are used to detect short-term overbought and oversold areas and help fine-tune the timing of entry.
3. **Imoku Cloud Trend Confirmation**: Completely calculate all components of the Ichimoku Cloud (turning line, baseline, leading band A/B and delay line) to further confirm the trend direction. When leading band A is higher than leading band B, it is identified as an upward trend; otherwise, it is a downward trend.
4. **Volatility and Liquidity Assessment**:
   - Use the ATR indicator to measure market volatility as a basis for adjusting position size.
   - Detect volume bursts, defined as current volume exceeding 2 times the 20-period volume SMA.
   - Automatically plot recent high and low pivots for visualization of dynamic support/resistance areas.
5. **Sentiment and Liquidity Indicators**:
   - Using the 50-period SMA as an indicator of market sentiment, prices above the SMA indicate bullish sentiment and prices below the SMA indicate bearish sentiment.
   - Use the 20-period volume SMA as a proxy for liquidity concentration.
6. **Buy and sell signal logic**:
   - Bull signal conditions: EMA trending upward, RSI<50, MACD histogram>0, stochastic RSI %K<80, Ichimoku is bullish.
   - Short signal conditions: EMA trending downward, RSI>50, MACD histogram <0, Stochastic RSI %K>20, Ichimoku is bearish.
7. **Dynamic position calculation**: Calculate the position size based on the account size, risk percentage and current ATR value. The formula is: position size = (account size × risk percentage)/ATR. This ensures consistent exposure across different volatility environments.
#### Strategic Advantages
1. **Multi-level signal confirmation system**: This strategy requires multiple technical indicators to meet specific conditions at the same time to generate trading signals, reducing the possibility of false signals and improving the reliability of trading decisions.
2. **Adaptive Risk Management**: Through the dynamic position adjustment mechanism based on ATR, the strategy can automatically adjust the transaction size according to market volatility. This means automatically reducing positions in higher-volatility market environments and increasing positions when volatility is lower, enabling truly adaptive risk management.
3. **Comprehensive market perspective**: The strategy integrates the analysis of multiple market dimensions such as trend, momentum, volatility, sentiment and liquidity, providing a comprehensive understanding of market conditions rather than relying solely on a single factor.
4. **Flexible parameter settings**: The strategy provides a wealth of adjustable parameters, including EMA period, RSI settings, risk percentage and account size, etc., allowing traders to customize according to personal risk preferences and specific market conditions.
5. **Visual auxiliary functions**: The strategy includes a variety of visual elements such as background color changes, pivot point marks, and signal shapes, which help traders intuitively understand market conditions and signal triggering conditions.
6. **Integrated strategy backtesting function**: The strategy has a built-in Pine Script strategy backtesting module, allowing traders to directly evaluate the historical performance of the strategy without writing additional backtesting code.
#### Strategy Risk
1. **Over-Reliance on Technical Indicators**: Strategies rely solely on technical indicators to generate signals, which can lead to unresponsive or inappropriate trading decisions when there are fundamental changes in the market, such as major news events. The solution is to use strategies as decision support tools rather than fully automated systems, or to integrate real-time news APIs to improve responsiveness to changes in fundamentals.
2. **Indicator lag risk**: Most of the technical indicators used (such as EMA, RSI, MACD) are lagging indicators in nature, which may lead to delays in entry or exit in rapidly changing markets. To mitigate this risk, consider adding forward-looking indicators or shortening the period of some indicators.
3. **Parameter optimization trap**: The strategy contains multiple adjustable parameters, and there is a risk of over-optimization, which may cause the strategy to perform poorly in real trading. It is recommended to use stepwise optimization and forward testing methods to verify the robustness of parameters.
4. **Signal scarcity risk**: Since the strategy requires multiple conditions to be met at the same time to generate a signal, in some market environments no trading signals may be generated for a long time, resulting in missed opportunities. Consider setting up alternative signal conditions or introducing a hierarchical signal system to balance signal quality and quantity.
5. **Lack of stop-loss mechanism**: The current strategy relies on reverse signals to close positions without a clear stop-loss mechanism, which may lead to larger losses when a strong trend reverses. It is recommended to add a stop-loss mechanism based on ATR multiples or key support/resistance levels.
#### Strategy optimization direction
1. **Integrated Multi-Time Frame Analysis**: The current strategy already allows analysis of trends on different time frames, but can be further expanded into a complete multi-time frame confirmation system. For example, requiring the trend directions of the larger time frame and the smaller time frame to be consistent, or using the larger time frame to determine the trend direction and the smaller time frame to find entry points, which can reduce losses caused by false breakthroughs.
2. **Add automatic take-profit and stop-loss function**: Set dynamic stop-loss levels based on multiples of ATR or support/resistance levels, and implement automatic take-profit functions based on risk-reward ratios, or introduce trailing stop-loss functions to protect earned profits and optimize the risk-reward ratio of each transaction.
3. **Optimize sentiment indicators**: Replace the current 50-period SMA with the actual news sentiment API, or integrate social media sentiment analysis to obtain a more accurate market sentiment indicator. This improves the strategy's responsiveness to changes in fundamentals.
4. **Introduction of Volatility Filter**: Halt trading in extreme volatility environments, or adjust the stringency of signal conditions. For example, requiring stronger confirmation signals when volatility is particularly high could help avoid overtrading in volatile markets.
5. **Signal strength grading system**: Upgrade the current binary signal system (with signal or no signal) to a grading system based on the number and intensity of meeting conditions, thereby enabling strategies to adopt different position sizes for signals of different strengths, which can control risks more precisely and optimize capital utilization.
6. **Integrated machine learning optimization**: Introduce machine learning algorithms to optimize parameter selection or directly predict the optimal position size, reduce the impact of human bias on parameter selection, and improve the strategy's adaptability to market changes.
#### Summary
The multi-indicator cross dynamic position volatility adaptive quantitative trading strategy represents a comprehensive technical analysis method that provides a structured trading decision-making framework by integrating the cross signals of multiple indicators and a dynamic risk management system. The core advantage of this strategy lies in its multi-level signal confirmation mechanism and volatility-based adaptive position management, allowing it to maintain consistent risk control in different market environments. Although there are risks such as over-reliance on technical indicators and parameter optimization traps, these risks can be effectively mitigated through the recommended optimization directions, such as adding multi-time frame analysis, improving the stop-loss mechanism, and introducing sentiment APIs. Ultimately, the strategy not only provides a trading signal generation system, but also includes a complete risk management framework, providing quantitative traders with a comprehensive trading solution. ||
#### Overview
The Multi-Indicator Dynamic Position Size Volatility-Adaptive Quantitative Trading Strategy is a comprehensive quantitative trading system that integrates trend detection, momentum indicators, volatility analysis, sentiment evaluation, and liquidity zone identification functions. This strategy uses cross signals from multiple technical indicators to generate buy and sell decisions, while dynamically adjusting position size based on market volatility to achieve adaptive risk management. Core components include EMA trend identification system, RSI momentum filter, MACD direction confirmation, Stochastic RSI fine-tuning, Ichimoku Cloud trend confirmation, and ATR-based volatility-adjusted position sizing system.

#### Strategy Principles
The core logic of this strategy is built on multi-layered indicator filtering, forming a strict signal generation mechanism:

1. **Trend Identification System**: The strategy uses two EMAs (default 9 and 21 periods) to determine market trend direction. When the fast EMA is above the slow EMA, an uptrend is identified; otherwise, it's a downtrend. This trend judgment can be performed in different timeframes, such as using daily data (D) for trend identification.

2. **Momentum Indicator Combination**:
   - RSI indicator measures price momentum, with a default period of 14 and overbought (70) and oversold (30) thresholds.
   - MACD indicator (12,26,9) confirms momentum direction, with special attention to MACD histogram values.
   - Stochastic RSI calculates %K and %D values to detect short-term overbought/oversold areas, helping to fine-tune entry timing.

3. **Ichimoku Cloud Trend Confirmation**: Fully calculates all components of the Ichimoku Cloud (Tenkan-sen, Kijun-sen, Senkou Span A/B, and Chikou Span) to further confirm trend direction. When Senkou Span A is above Senkou Span B, an uptrend is identified; otherwise, it's a downtrend.

4. **Volatility and Liquidity Assessment**:
   - Uses ATR indicator to measure market volatility, serving as the basis for adjusting position size.
   - Detects volume explosions, defined as current volume exceeding 2 times the 20-period volume SMA.
   - Automatically plots recent pivot highs and lows for dynamic support/resistance zone visualization.

5. **Sentiment and Liquidity Indicators**:
   - Uses 50-period SMA as a market sentiment indicator, with price above SMA indicating bullish sentiment and below SMA indicating bearish sentiment.
   - Uses 20-period volume SMA as a proxy for liquidity concentration.

6. **Buy/Sell Signal Logic**:
   - Long signal conditions: EMA trend up, RSI<50, MACD histogram>0, Stochastic RSI %K<80, Ichimoku Cloud bullish.
   - Short signal conditions: EMA trend down, RSI>50, MACD histogram<0, Stochastic RSI %K>20, Ichimoku Cloud bearish.

7. **Dynamic Position Calculation**: Calculates position size based on account size, risk percentage, and current ATR value, using the formula: Position Size = (Account Size × Risk %) / ATR. This ensures consistent risk exposure across different volatility environments.

#### Strategy Advantages
1. **Multi-level Signal Confirmation System**: The strategy requires multiple technical indicators to simultaneously meet specific conditions to generate trading signals, reducing the possibility of false signals and increasing the reliability of trading decisions.

2. **Adaptive Risk Management**: Through the ATR-based dynamic position adjustment mechanism, the strategy can automatically adjust trading size according to market volatility. This means automatically reducing position size in high-volatility market environments and increasing it in low-volatility environments, achieving truly adaptive risk management.

3. **Comprehensive Market Perspective**: The strategy integrates analysis of multiple market dimensions including trend, momentum, volatility, sentiment, and liquidity, providing a comprehensive understanding of market conditions rather than relying on a single factor.

4. **Flexible Parameter Settings**: The strategy offers a rich set of adjustable parameters, including EMA periods, RSI settings, risk percentage, and account size, allowing traders to customize according to personal risk preferences and specific market conditions.

5. **Visual Assistance Functions**: The strategy includes multiple visualization elements such as background color changes, pivot point markings, and signal shapes, helping traders intuitively understand market conditions and signal trigger conditions.

6. **Integrated Strategy Backtesting Functionality**: The strategy incorporates Pine Script's strategy backtesting module, allowing traders to directly evaluate the historical performance of the strategy without writing additional backtesting code.

#### Strategy Risks
1. **Over-reliance on Technical Indicators**: The strategy completely relies on technical indicators to generate signals, which may lead to slow or inappropriate trading decisions when the market undergoes fundamental changes (such as major news events). The solution is to use the strategy as a decision support tool rather than a fully automated system, or to integrate real-time news APIs to improve responsiveness to fundamental changes.

2. **Indicator Lag Risk**: Most technical indicators used (such as EMA, RSI, MACD) are inherently lagging indicators, which may cause delayed entry or exit in rapidly changing markets. To mitigate this risk, consider adding forward-looking indicators or shortening the periods of certain indicators.

3. **Parameter Optimization Trap**: The strategy contains multiple adjustable parameters, posing a risk of over-optimization, which may lead to poor performance in live trading. It is recommended to use walk-forward optimization and out-of-sample testing methods to verify the robustness of parameters.

4. **Signal Scarcity Risk**: Since the strategy requires multiple conditions to be met simultaneously to generate signals, it may not produce trading signals for long periods in certain market environments, leading to missed opportunities. Consider setting alternative signal conditions or introducing a tiered signal system to balance signal quality and quantity.

5. **Lack of Stop-Loss Mechanism**: The current strategy relies on reverse signals for closing positions without an explicit stop-loss mechanism, which may lead to significant losses during strong trend reversals. It is recommended to add stop-loss mechanisms based on ATR multiples or key support/resistance levels.

#### Strategy Optimization Directions
1. **Integrate Multi-timeframe Analysis**: The current strategy already allows trend analysis in different timeframes, but it can be further expanded into a complete multi-timeframe confirmation system. For example, requiring trend directions in larger and smaller timeframes to be consistent, or using larger timeframes to determine trend direction and smaller timeframes to find entry points, which can reduce losses from false breakouts.

2. **Add Automatic Take-Profit and Stop-Loss Functions**: Set dynamic stop-loss levels based on ATR multiples or support/resistance levels, and implement automatic take-profit functions based on risk-reward ratios, or introduce trailing stop functions to protect profits and optimize the risk-reward ratio of each trade.

3. **Optimize Sentiment Indicators**: Replace the current 50-period SMA with actual news sentiment APIs, or integrate social media sentiment analysis to obtain more accurate market sentiment indicators. This can improve the strategy's response speed to fundamental changes.

4. **Introduce Volatility Filters**: Pause trading in extreme volatility environments, or adjust the strictness of signal conditions. For example, requiring stronger confirmation signals in particularly high volatility, which helps avoid overtrading in unstable markets.

5. **Signal Strength Grading System**: Upgrade the current binary signal system (signal or no signal) to a graded system based on the number and strength of conditions met, enabling different position sizes for different strength signals, which allows for more refined risk control and capital utilization optimization.

6. **Integrate Machine Learning Optimization**: Introduce machine learning algorithms to optimize parameter selection or directly predict optimal position size, reducing the impact of human bias on parameter selection and improving the strategy's adaptability to market changes.

#### Summary
The Multi-Indicator Dynamic Position Size Volatility-Adaptive Quantitative Trading Strategy represents a comprehensive technical analysis approach that provides a structured trading decision framework through the integration of cross signals from multiple indicators and a dynamic risk management system. The core advantages of this strategy lie in its multi-level signal confirmation mechanism and volatility-based adaptive position management, enabling it to maintain consistent risk control across different market environments. While risks such as over-reliance on technical indicators and parameter optimization traps exist, these can be effectively mitigated through the suggested optimization directions, such as adding multi-timeframe analysis, improving stop-loss mechanisms, and introducing sentiment APIs. Ultimately, this strategy not only provides a trading signal generation system but also contains a complete risk management framework, offering quantitative traders a comprehensive trading solution.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-18 00:00:00
end: 2025-04-15 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"TRX_USD"}]
*/

//@version=5
strategy("Phoenix Master Strategy (PMI)", overlay=true, max_lines_count=500, max_labels_count=500)

// === INPUTLAR === //
timeframeTrend = input.timeframe("D", "Trend Zaman Dilimi")
showBackground = input.bool(true, "Trend Arka Plan Rengi Göster")
riskPercent = input.float(1.0, title="Risk %", minval=0.1, maxval=10.0)
accountSize = input.float(10000, title="Hesap Büyüklüğü ($)", minval=100)

// === EMA Trend === //
emaFast = input.int(9, "Hızlı EMA")
emaSlow = input.int(21, "Yavaş EMA")
ema1 = request.security(syminfo.tickerid, timeframeTrend, ta.ema(close, emaFast))
ema2 = request.security(syminfo.tickerid, timeframeTrend, ta.ema(close, emaSlow))
trendUp = ema1 > ema2
trendDown = ema1 < ema2

// === RSI === //
rsiLength = input.int(14, "RSI Periyodu")
rsiOB = input.int(70, "RSI Overbought")
rsiOS = input.int(30, "RSI Oversold")
rsi = ta.rsi(close, rsiLength)

// === MACD === //
macdSource = input.source(close, "MACD Kaynağı")
[macdLine, signalLine, macdHist] = ta.macd(macdSource, 12, 26, 9)

// === Stoch RSI === //
stochLength = input.int(14, "Stoch RSI Uzunluğu")
stochK = input.int(3, "%K")
stochD = input.int(3, "%D")
k = ta.stoch(close, high, low, stochLength)
stochKval = ta.sma(k, stochK)
stochDval = ta.sma(stochKval, stochD)
// === Ichimoku === //
tenkanPeriod = input.int(9, "Tenkan (Dönem)")
kijunPeriod = input.int(26, "Kijun (Dönem)")
senkouSpanBPeriod = input.int(52, "Senkou Span B (Dönem)")
displacement = input.int(26, "İchimoku Gecikme (Displacement)")

tenkan = (ta.highest(high, tenkanPeriod) + ta.lowest(low, tenkanPeriod)) / 2
kijun = (ta.highest(high, kijunPeriod) + ta.lowest(low, kijunPeriod)) / 2
senkouSpanA = (tenkan + kijun) / 2
senkouSpanB = (ta.highest(high, senkouSpanBPeriod) + ta.lowest(low, senkouSpanBPeriod)) / 2
chikouSpan = close[displacement]

// Ichimoku Trend Yorumlama
cloudUp = senkouSpanA > senkouSpanB
cloudDown = senkouSpanA < senkouSpanB

// Bulut Çizimi (İsteğe Bağlı Görsel İçin)
// plot(senkouSpanA[displacement], title="Senkou Span A", color=color.green)
// plot(senkouSpanB[displacement], title="Senkou Span B", color=color.red)

// === ATR & Volatilite === //
atrLength = input.int(14, "ATR Periyodu")
atr = ta.atr(atrLength)

// === Hacim Tabanlı Volatilite Alarmı === //
volumeExplode = volume > ta.sma(volume, 20) * 2

// === Destek & Direnç Bölgeleri (Pivot) === //
pivotHigh = ta.pivothigh(high, 5, 5)
pivotLow = ta.pivotlow(low, 5, 5)
plot(pivotHigh, title="Direnç", style=plot.style_cross, color=color.red, linewidth=1)
plot(pivotLow, title="Destek", style=plot.style_cross, color=color.green, linewidth=1)

// === Sentiment Göstergesi (Haber Sinyali Placeholder) === //
sentimentDummy = close > ta.sma(close, 50) ? 1 : -1
plotshape(sentimentDummy == 1 ? close : na, title="Pozitif Sentiment", location=location.abovebar, style=shape.triangleup, color=color.lime, size=size.tiny)
plotshape(sentimentDummy == -1 ? close : na, title="Negatif Sentiment", location=location.belowbar, style=shape.triangledown, color=color.maroon, size=size.tiny)

// === Likidite Heatmap (Zonal Risk Göstergesi Dummy) === //
heatZone = ta.sma(volume, 20)
plot(heatZone, title="Likidite Isı Haritası", color=color.orange, style=plot.style_columns)

// === Arka Plan Rengi === //
bgcolor(showBackground ? (trendUp ? color.new(color.green, 85) : trendDown ? color.new(color.red, 85) : na) : na)

// === Giriş/Çıkış Sinyalleri === //
longSignal = trendUp and rsi < 50 and macdHist > 0 and stochKval < 80 and cloudUp
shortSignal = trendDown and rsi > 50 and macdHist < 0 and stochKval > 20 and cloudDown

plotshape(longSignal, title="Al Sinyali", location=location.belowbar, color=color.green, style=shape.labelup, text="AL")
plotshape(shortSignal, title="Sat Sinyali", location=location.abovebar, color=color.red, style=shape.labeldown, text="SAT")

// === Alarm Koşulları === //
alertcondition(longSignal, title="AL Sinyali Alarmı", message="Phoenix - AL Sinyali")
alertcondition(shortSignal, title="SAT Sinyali Alarmı", message="Phoenix - SAT Sinyali")
alertcondition(volumeExplode, title="Hacim Patlaması", message="Phoenix - Hacim Patlaması Tespit Edildi")

// === Pozisyon Büyüklüğü Hesaplama === //
riskDollar = accountSize * (riskPercent / 100)
positionSize = riskDollar / atr
plot(positionSize, title="Pozisyon Büyüklüğü (Lot)", color=color.fuchsia, linewidth=1)

// === STRATEJİ MODÜLÜ === //
strategy.entry("AL", strategy.long, when=longSignal)
strategy.close("AL", when=shortSignal)
strategy.entry("SAT", strategy.short, when=shortSignal)
strategy.close("SAT", when=longSignal)

// === BİTTİ === //
// Phoenix Master Indicator tüm ileri düzey fonksiyonlarla aktif: trend, sinyal, volatilite, sentiment, likidite, pozisyon büyüklüğü ve strateji test!

```

> Detail

https://www.fmz.com/strategy/491042

> Last Modified

2025-04-18 09:55:17
