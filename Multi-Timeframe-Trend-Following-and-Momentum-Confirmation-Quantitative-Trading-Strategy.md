
> Name

Multi-Timeframe-Trend-Following-and-Momentum-Confirmation-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/3f86bf45d02905cba92d42c14c242b2dc0d5b3fc2eba812519e3262911ad4c1d.png)
![IMG](assets/images/df284fbab7916e93de49f66366368cdffcffba3cdd1c7b84b5301d1f62c118f9.png)



[trans]

#### Overview
This is a comprehensive quantitative trading strategy that incorporates multi-time frame analysis and technical indicator confirmation. The core of this strategy is to evaluate the strength of the market trend through the crossing status of moving averages in different time periods (H1, H4 and daily lines), and to confirm trading signals by combining momentum indicators such as RSI and MACD. The system is equipped with a complete fund management mechanism, adopts dynamic stop loss and take profit based on ATR, and implements a compound exit strategy of partial profit and trailing take profit. This strategy is particularly suitable for the foreign exchange and precious metals markets, aiming to capture mid- to long-term trend trends while effectively controlling risks.
#### Strategy Principle
The core principle of this strategy is multi-dimensional market trend analysis and confirmation:
1. **Multiple Time Frame Trend Scoring System**:
   - Comprehensive trend score is calculated by comparing fast (50-period) and slow (200-period) moving averages on three time periods (H1, H4 and daily)
   - H1 time frame weighting ±1 point, H4 time frame weighting ±2 points, daily time frame weighting ±3 points
   - When the fast line is above the slow line, it gets positive points, otherwise it gets negative points, and the scores in the three time periods are accumulated to form the final score.
2. **Admission Conditions**:
   - Long entry: trend score ≥ 3, price above H1 fast moving average, RSI > 50, MACD line > signal line
   - Short entry: Trend score ≤ -3, price below H1 fast moving average, RSI < 50, MACD line < signal line
3. **Risk Management and Exit Strategy**:
   - Position calculation: Calculated based on the account balance and the set leverage (number of lots allocated per 1,000 US dollars), while limiting the risk of a single transaction to no more than 2% of the account
   - Stop loss setting: dynamically calculate stop loss distance based on 2 times ATR
   - Step-by-step profit taking: 50% of the positions are profit-taking at 1 times ATR, and the remaining 50% is set at a target level of 3 times ATR and adopts a trailing stop profit mechanism.
4. **Control Panel**:
   - Real-time display of moving average values and relationships for each time period
   - Shows current scores and trading signal recommendations (buy, sell or neutral)
#### Strategic Advantages
1. **Multi-dimensional trend confirmation**: By integrating trend information from three time periods, the strategy can more accurately identify strong trends and effectively filter out false signals and noise. Higher weights are assigned to longer time periods, which is in line with the principle of giving priority to long-term trends in technical analysis.
2. **Multiple verification of entry signals**: In addition to trend scoring, the strategy also requires price, RSI and MACD indicators to meet specific conditions at the same time before executing transactions. This multiple confirmation mechanism significantly improves signal quality.
3. **Intelligent Risk Management**:
   - Dynamic stop loss setting based on market volatility (ATR) to adapt to different market conditions
   - A step-by-step profit strategy balances the need to lock in gains and follow trends
   - The position size is automatically adjusted according to the account size to ensure the consistency of the capital ratio
4. **Visual decision support**: The control panel intuitively displays the trend status and comprehensive score of each time period, helping traders to quickly judge market conditions and enhance decision-making confidence.
5. **Strong adaptability**: The strategy can be applied to a variety of trading varieties, especially in foreign exchange pairs and precious metals with obvious trends, which perform better.
#### Strategy Risk
1. **Trend Reversal Risk**: Although the strategy improves accuracy through multi-time frame analysis, it may still face a large retracement in the event of a strong market reversal. It is recommended to temporarily reduce positions or suspend trading before the release of important economic data or events.
2. **Excessive trading risk**: When the market is in range oscillation, the trend score may frequently fluctuate near the critical value, resulting in repeated entry and exit. The solution is to add an additional choppy market filter such as ATR% or a volatility indicator.
3. **Parameter sensitivity**: Strategy performance is more sensitive to SMA cycle (50/200) and ATR multiple settings. It is recommended to use comprehensive historical backtesting to optimize parameters and regularly evaluate whether parameters are still suitable for the current market environment.
4. **Money Management Limitations**: The current fixed ratio risk model may not be flexible enough under extreme market conditions. Consider introducing a volatility-adjusted position size calculation method to automatically reduce positions during periods of high volatility.
5. **Execution Delay Risk**: In a fast market, the multiple confirmations that the strategy relies on may lead to delayed entry timing and missing the best price. To mitigate this risk, consider adding early entry signals based on price action.
#### Strategy optimization direction
1. **Improve trend identification mechanism**:
   - Replace the simple moving average (SMA) with the exponential moving average (EMA) or Hull moving average to improve the response speed of trend identification
   - Introduce trend strength indicators (such as ADX) as additional filters to ensure only entering in clear trends
   - Consider adding distance assessment between price and moving averages to avoid entering into overextended markets
2. **Enhanced signal confirmation system**:
   - Add trading volume analysis to ensure that the trading direction is consistent with the trading volume trend
   - Integrate price action pattern recognition (such as breakthroughs, backtests, high and low patterns) as auxiliary confirmation
   - Introduce seasonality and market sentiment indicators to improve signal quality
3. **Optimize exit mechanism**:
   - Realize dynamic take-profit adjustment based on market conditions, giving greater profit margins in strong trends
   - Add moving average crossovers or trend score changes as early exit signals for some positions
   - Develop time stop loss based on fluctuation cycles to avoid long-term unprofitable transactions
4. **Enhance Risk Management**:
   - Achieve correlation-sensitive risk allocation and avoid excessive risk concentration in highly correlated markets
   - Add daily, weekly and monthly maximum drawdown limits, which will automatically reduce positions or suspend trading when triggered
   - Develop a dynamic leverage adjustment system based on market volatility
5. **Improve system adaptability**:
   - Develop parameter adaptive mechanism to automatically adjust key parameters according to different market stages
   -Introducing machine learning algorithms to optimize the distribution of trend score weights
   - Added news event filter to suspend trading before and after the release of important economic data
#### Summary
The multi-time frame trend tracking and momentum confirmation quantitative trading strategy is a comprehensive and systematic trading solution that generates high-quality trading signals by integrating trend information and technical indicator confirmations across multiple time periods. Its greatest advantage lies in its multi-level trend identification and signal confirmation mechanism, which effectively improves signal quality; at the same time, dynamic risk management and step-by-step profit strategies based on market volatility provide a solid guarantee for capital security.
The main risks to the strategy are potential drawdowns and parameter sensitivity during trend reversals. Through the recommended optimization directions, such as improving the trend identification mechanism, enhancing the signal confirmation system, optimizing the exit mechanism, enhancing risk management and improving system adaptability, this strategy can further enhance stability and profitability in various market environments.
For traders who want to capture mid- to long-term trend opportunities in the foreign exchange and precious metals markets, this is a strategic framework with sound theory and strong practicality. After sufficient backtesting and appropriate parameter optimization, it can be used as a core component of systematic trading or an independent trading system. ||
#### Overview
This is a comprehensive quantitative trading strategy that integrates multi-timeframe analysis with technical indicator confirmation. The core of the strategy lies in evaluating market trend strength through moving average crossovers across different time periods (H1, H4, and daily), combined with momentum indicators such as RSI and MACD for trade signal confirmation. The system is equipped with a sophisticated money management mechanism, employing dynamic ATR-based stop-loss and take-profit levels, and implementing a compound exit strategy with partial profit-taking and trailing stops. This strategy is particularly suitable for forex and precious metals markets, designed to capture medium to long-term trending movements while effectively controlling risk.

#### Strategy Principles
The core principle of this strategy is multi-dimensional market trend analysis and confirmation:

1. **Multi-Timeframe Trend Scoring System**:
   - Calculates a comprehensive trend score by comparing fast (50-period) and slow (200-period) moving averages across three timeframes (H1, H4, and daily)
   - H1 timeframe is weighted ±1 point, H4 timeframe ±2 points, and daily timeframe ±3 points
   - Positive scores are assigned when the fast MA is above the slow MA, negative when below, with the final score being the sum across all timeframes

2. **Entry Conditions**:
   - Long Entry: Trend score ≥3, price above H1 fast moving average, RSI>50, MACD line>signal line
   - Short Entry: Trend score ≤-3, price below H1 fast moving average, RSI<50, MACD line<signal line

3. **Risk Management and Exit Strategy**:
   - Position sizing: Based on account balance and set leverage (lots per $1000), while limiting single trade risk to no more than 2% of the account
   - Stop-loss: Dynamically calculated at 2x ATR distance
   - Stepped profit-taking: 50% position closed at 1x ATR profit, remaining 50% with 3x ATR target and trailing stop mechanism

4. **Control Panel**:
   - Real-time display of moving average values and relationships across timeframes
   - Visualization of current score and trade signal recommendations (buy, sell, or neutral)

#### Strategy Advantages
1. **Multi-dimensional Trend Confirmation**: By integrating trend information from three timeframes, the strategy can more accurately identify strong trends, effectively filtering out false signals and noise. Higher weights are assigned to longer timeframes, aligning with the principle of long-term trend priority in technical analysis.

2. **Multiple Entry Signal Validation**: Besides trend scoring, the strategy requires specific conditions for price, RSI, and MACD indicators to be met simultaneously, significantly improving signal quality through this multi-confirmation mechanism.

3. **Intelligent Risk Management**:
   - Dynamic stop-loss based on market volatility (ATR), adapting to different market conditions
   - Stepped profit-taking strategy balances securing gains and following trends
   - Position size automatically adjusts based on account size, ensuring consistent capital allocation

4. **Visual Decision Support**: The control panel intuitively displays trend status across timeframes and the composite score, helping traders quickly assess market conditions and enhancing decision confidence.

5. **High Adaptability**: The strategy can be applied to various trading instruments, performing particularly well in forex pairs and precious metals with distinct trends.

#### Strategy Risks
1. **Trend Reversal Risk**: Despite enhanced accuracy through multi-timeframe analysis, the strategy may still face significant drawdowns during strong market reversals. Consider temporarily reducing position size or pausing trading before major economic data releases or events.

2. **Overtrading Risk**: When markets are range-bound, the trend score may frequently fluctuate around threshold values, causing repeated entries and exits. A solution is to add an additional range-market filter, such as ATR percentage or volatility indicators.

3. **Parameter Sensitivity**: Strategy performance is sensitive to SMA periods (50/200) and ATR multiplier settings. Comprehensive historical backtesting is recommended to optimize parameters, with periodic evaluation of whether they remain suitable for current market conditions.

4. **Money Management Limitations**: The current fixed proportion risk model may not be flexible enough in extreme market conditions. Consider introducing volatility-adjusted position sizing to automatically reduce positions during highly volatile periods.

5. **Execution Delay Risk**: In fast markets, the multiple confirmations required by the strategy may lead to delayed entries, missing optimal prices. To mitigate this risk, consider adding early entry signals based on price action.

#### Strategy Optimization Directions
1. **Improved Trend Identification Mechanism**:
   - Replace Simple Moving Averages (SMA) with Exponential Moving Averages (EMA) or Hull Moving Averages for faster trend identification
   - Introduce trend strength indicators (such as ADX) as additional filters to ensure entries only in clear trends
   - Consider adding distance evaluation between price and moving averages to avoid entries in overextended markets

2. **Enhanced Signal Confirmation System**:
   - Add volume analysis to ensure trade direction aligns with volume trends
   - Integrate price action pattern recognition (breakouts, retests, high-low formations) as auxiliary confirmation
   - Incorporate seasonality and market sentiment indicators to improve signal quality

3. **Optimized Exit Mechanism**:
   - Implement dynamic take-profit adjustments based on market state, allowing for larger profit targets in strong trends
   - Add moving average crossovers or trend score changes as early exit signals for partial positions
   - Develop time-based stops based on volatility cycles to avoid trades that remain unprofitable for extended periods

4. **Enhanced Risk Management**:
   - Implement correlation-sensitive risk allocation to avoid excessive risk concentration in highly correlated markets
   - Add daily, weekly, and monthly maximum drawdown limits that automatically reduce position size or pause trading when triggered
   - Develop a dynamic leverage adjustment system based on market volatility

5. **Improved System Adaptability**:
   - Develop parameter self-adaptation mechanisms that automatically adjust key parameters based on different market phases
   - Introduce machine learning algorithms to optimize trend score weight distribution
   - Add news event filters to pause trading before and after important economic data releases

#### Summary
The Multi-Timeframe Trend Following and Momentum Confirmation Quantitative Trading Strategy is a comprehensive, systematic trading solution that generates high-quality trading signals by integrating trend information from multiple timeframes and technical indicator confirmations. Its greatest strength lies in the multi-layered trend identification and signal confirmation mechanisms, effectively improving signal quality; meanwhile, the dynamic risk management based on market volatility and stepped profit-taking strategy provide solid protection for capital safety.

The main risks of the strategy include potential drawdowns during trend reversal periods and parameter sensitivity. Through the suggested optimization directions, such as improving the trend identification mechanism, enhancing the signal confirmation system, optimizing the exit mechanism, strengthening risk management, and increasing system adaptability, this strategy can further improve its stability and profitability across various market environments.

For traders looking to capture medium to long-term trend opportunities in forex and precious metals markets, this is a theoretically sound and highly practical strategy framework. After thorough backtesting and appropriate parameter optimization, it can be used as a core component of systematic trading or as a standalone trading system.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-20 00:00:00
end: 2025-02-27 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("JolurocePro v2.0", overlay=true, margin_long=100, margin_short=100, pyramiding=1)

// 1. Configuración Principal
capitalMaximo      = input(20000, "Capital Maximo (USD)")
lotajeBase         = input.float(0.1, "Lotes por 1000 USD", minval=0.01)
paresPermitidos    = input.string("XAUUSD,EURUSD,GBPUSD,GBPNZD,EURCAD,USDCAD,USDJPY", "Pares Permitidos")

// 2. Indicadores Multitemporales
[mediaRapidaH1, mediaLentaH1] = request.security(syminfo.tickerid, "60", [ta.sma(close, 50), ta.sma(close, 200)])
[mediaRapidaH4, mediaLentaH4] = request.security(syminfo.tickerid, "240", [ta.sma(close, 50), ta.sma(close, 200)])
[mediaRapidaD, mediaLentaD]   = request.security(syminfo.tickerid, "D", [ta.sma(close, 50), ta.sma(close, 200)])

// 3. Calculo del Score
currentScore = (mediaRapidaH1 > mediaLentaH1 ? 1 : -1) + (mediaRapidaH4 > mediaLentaH4 ? 2 : -2) + (mediaRapidaD > mediaLentaD ? 3 : -3)

// 4. Panel de Control
var table panel = table.new(position.top_right, 4, 6, bgcolor=color.new(#2C3E50, 90))

if barstate.islast
    // Encabezado
    table.cell(panel, 0, 0, " JolurocePro ", width=4, text_color=color.white, text_size=size.large)
    
    // Temporalidad H1
    table.cell(panel, 0, 1, "H1", text_color=color.white)
    table.cell(panel, 1, 1, str.tostring(math.round(mediaRapidaH1, 4)), text_color=mediaRapidaH1 > mediaLentaH1 ? #2ECC71 : #E74C3C)
    table.cell(panel, 2, 1, str.tostring(math.round(mediaLentaH1, 4)), text_color=mediaRapidaH1 > mediaLentaH1 ? #2ECC71 : #E74C3C)
    table.cell(panel, 3, 1, mediaRapidaH1 > mediaLentaH1 ? "▲" : "▼", text_color=mediaRapidaH1 > mediaLentaH1 ? #2ECC71 : #E74C3C)
    
    // Temporalidad H4
    table.cell(panel, 0, 2, "H4", text_color=color.white)
    table.cell(panel, 1, 2, str.tostring(math.round(mediaRapidaH4, 4)), text_color=mediaRapidaH4 > mediaLentaH4 ? #2ECC71 : #E74C3C)
    table.cell(panel, 2, 2, str.tostring(math.round(mediaLentaH4, 4)), text_color=mediaRapidaH4 > mediaLentaH4 ? #2ECC71 : #E74C3C)
    table.cell(panel, 3, 2, mediaRapidaH4 > mediaLentaH4 ? "▲" : "▼", text_color=mediaRapidaH4 > mediaLentaH4 ? #2ECC71 : #E74C3C)
    
    // Temporalidad Diaria
    table.cell(panel, 0, 3, "Diario", text_color=color.white)
    table.cell(panel, 1, 3, str.tostring(math.round(mediaRapidaD, 4)), text_color=mediaRapidaD > mediaLentaD ? #2ECC71 : #E74C3C)
    table.cell(panel, 2, 3, str.tostring(math.round(mediaLentaD, 4)), text_color=mediaRapidaD > mediaLentaD ? #2ECC71 : #E74C3C)
    table.cell(panel, 3, 3, mediaRapidaD > mediaLentaD ? "▲" : "▼", text_color=mediaRapidaD > mediaLentaD ? #2ECC71 : #E74C3C)
    
    // Recomendacion
    table.cell(panel, 0, 4, "Score Actual:", text_color=color.white)
    table.cell(panel, 1, 4, str.tostring(currentScore), text_color=currentScore >= 3 ? #2ECC71 : currentScore <= -3 ? #E74C3C : #F1C40F, width=3)
    table.cell(panel, 0, 5, "Senal:", text_color=color.white)
    table.cell(panel, 1, 5, currentScore >= 3 ? "COMPRA" : currentScore <= -3 ? "VENTA" : "NEUTRO", text_color=currentScore >= 3 ? #2ECC71 : currentScore <= -3 ? #E74C3C : #F1C40F, width=3)

// 5. Indicadores Tecnicos
atrValor = ta.atr(14)
rsi = ta.rsi(close, 14)
macdLine = ta.ema(close, 12) - ta.ema(close, 26)
macdSignal = ta.ema(macdLine, 9)

// 6. Condiciones de Entrada
condicionLong = currentScore >= 3 and close > mediaRapidaH1 and rsi > 50 and macdLine > macdSignal
condicionShort = currentScore <= -3 and close < mediaRapidaH1 and rsi < 50 and macdLine < macdSignal

// 7. Gestion de Riesgo
posicionSize = math.min((strategy.equity / 1000) * lotajeBase, strategy.equity * 0.02)
slLong = close - (atrValor * 2)
tp1Long = close + (atrValor * 1)
tp2Long = close + (atrValor * 3)

slShort = close + (atrValor * 2)
tp1Short = close - (atrValor * 1)
tp2Short = close - (atrValor * 3)

// 8. Ejecucion de Ordenes
if condicionLong
    strategy.entry("Long", strategy.long, qty=posicionSize)
    strategy.exit("TP1", "Long", stop=slLong, limit=tp1Long, qty_percent=50)
    strategy.exit("TP2", "Long", limit=tp2Long, trail_points=atrValor*10)

if condicionShort
    strategy.entry("Short", strategy.short, qty=posicionSize)
    strategy.exit("TP1", "Short", stop=slShort, limit=tp1Short, qty_percent=50)
    strategy.exit("TP2", "Short", limit=tp2Short, trail_points=atrValor*10)

// 9. Senales Visuales
plotshape(condicionLong, "Compra", shape.triangleup, location.belowbar, color=#2ECC71, size=size.small)
plotshape(condicionShort, "Venta", shape.triangledown, location.abovebar, color=#E74C3C, size=size.small)
```

> Detail

https://www.fmz.com/strategy/484095

> Last Modified

2025-02-28 09:53:59
