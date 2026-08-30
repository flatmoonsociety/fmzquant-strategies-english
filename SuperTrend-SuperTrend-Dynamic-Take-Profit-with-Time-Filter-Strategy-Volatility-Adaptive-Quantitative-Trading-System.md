
> Name

SuperTrend Dynamic Take-Profit-with-Time-Filter-Strategy-Volatility-Adaptive-Quantitative-Trading-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d7cb05ccd8d0f2958d10.png)
![IMG](https://www.fmz.com/upload/asset/2d90365a04c8c62cbe4e8.png)


[trans]

#### Overview
SuperTrend dynamic take-profit and time filter strategy is a quantitative trading system based on volatility adaptiveness. The core relies on the SuperTrend indicator as a dynamic tracking stop-loss tool. The strategy captures market trends by identifying moments when price breaks above the SuperTrend indicator line and incorporates multiple filtering mechanisms, including a Moscow Time (MSK) filter, price level filtering, and a fixed percentage take-profit function. The system is designed in a multi-functional mode, which can be used to trade long or short positions alone, or to achieve two-way trading. The strategy intuitively displays the trading direction through color changes on the chart: the green area indicates an upward trend (long), and the red area indicates a downward trend (short), which greatly improves the strategy visualization experience and the convenience of operational decision-making.
#### Strategy Principle
The core operation of this strategy is based on the following key mechanisms:
1. **SuperTrend indicator calculation**: The strategy uses the ATR indicator (default period 23) and multiplier factor (default 1.8) to calculate the SuperTrend line. This line automatically adjusts its position according to market volatility to form dynamic support and resistance.
2. **Trading signal generation**:
   - Long entry signal: triggered when the closing price breaks above the SuperTrend line upward (dir value changes from positive to negative) and meets the time and price filter conditions.
   - Short entry signal: triggered when the closing price falls below the SuperTrend line downward (dir value changes from negative to positive) and the filter conditions are met.
3. **Trading mode selection**: The strategy provides three trading modes:
   - Long Only: Only long transactions are executed and positions are closed when short signals are received.
   - Short Only: Only short trades are executed, and positions are closed when long signals are received.
   - Both: Allows the execution of long and short two-way transactions.
4. **Multiple filtration system**:
   - Moscow time filter (MSK, UTC+3): allows users to set a specific trading period and only execute transactions during that period.
   - Price level filtering: You can set a price threshold, and only execute long positions when the price is higher than the threshold, and execute short positions when the price is lower than the threshold.
5. **Dynamic take-profit mechanism**: The strategy implements a fixed percentage take-profit (default 1.5%) based on the entry price. Once the price reaches the take-profit level, the strategy automatically closes the position and locks in profits. Take profit levels can be displayed visually on the chart, and users can turn this visualization feature on or off as needed.
#### Strategic Advantages
Digging deeper into this code, I concluded the following significant advantages:
1. **Volatility Adaptability**: The SuperTrend indicator is based on ATR calculation, which can automatically adjust the tracking distance according to market fluctuations, increase the protection distance in high-volatility markets, and track prices more closely in low-volatility markets, improving the strategy's adaptability to different market environments.
2. **Multiple Risk Control**: The strategy integrates three layers of risk management: time filtering, price filtering and take-profit settings. This multi-dimensional risk control mechanism significantly improves transaction security.
3. **Flexible trading direction**: You can choose only long, only short or two-way trading, allowing the strategy to adapt to different market preferences and trading restrictions.
4. **Time Intelligent Optimization**: The unique Moscow time filter allows trading during specific time periods, helping to avoid market inefficiency periods and capture efficient trading windows in a targeted manner, especially suitable for traders who need to consider international trading periods.
5. **Visualization advantages**: Through background color changes, SuperTrend line colors and take-profit level marks, it provides an intuitive visual trading reference and reduces the complexity of analysis.
6. **Commission optimization design**: The strategy has built-in commission consideration (0.06%), making the backtest results closer to the real trading environment.
7. **Closing price execution mechanism**: The strategy uses the closing price to execute orders (process_orders_on_close=true), which reduces the impact of slippage and improves the reliability of backtesting.
#### Strategy Risk
Although this strategy is well designed, there are still potential risks:
1. **Trend reversal delay**: The SuperTrend indicator is essentially a lagging indicator. When the market reverses sharply, it may generate a delayed signal, resulting in untimely entry or exit and increasing the risk of retracement. The solution is to adjust the ATR period and multiplier factor to balance sensitivity and stability.
2. **Limitations of fixed take profit**: Using a fixed percentage take profit may lock in profits prematurely and miss out on more gains in a strong trend. It is recommended to dynamically adjust the take-profit percentage based on market volatility or optimize the take-profit strategy in combination with other technical indicators.
3. **Parameter sensitivity**: Strategy performance is highly dependent on parameter settings (ATR period, multiplier factor, take-profit percentage, etc.). Improper parameters may lead to over-trading or missed signals. The optimal parameter combination should be found through historical data backtesting.
4. **Over-restrictive filters**: Too strict time and price filters may lead to missed effective trading opportunities. It is recommended to adjust the filtering conditions based on actual trading varieties and market characteristics.
5. **Market Condition Dependence**: This strategy performs well in markets with obvious trends, but may frequently generate false signals in volatile markets. Consider adding a market status identification mechanism and enabling strategies only in trending markets.
6. **Lack of stop loss mechanism**: Although SuperTrend can be used as a dynamic stop loss reference, the stop loss conditions are not clearly set in the code, and you may face large losses under extreme market conditions. It is recommended to add a hard stop loss mechanism.
#### Strategy optimization direction
Based on code analysis, I recommend the following optimization directions:
1. **Dynamic parameter adaptation**: You can write a function to automatically adjust SuperTrend’s ATR cycle and multiplier factor according to market conditions (volatility, trading volume, etc.) to improve strategy adaptability. The advantage of this is that it can automatically find the optimal parameter combination in different market stages.
2. **Multi-time period confirmation**: Introducing a multi-time period confirmation mechanism, transactions will only be executed when the larger time period and the current time period SuperTrend direction are consistent, reducing false signals. This can significantly improve signal quality.
3. **Intelligent take-profit system**: Change the fixed percentage take-profit to dynamic take-profit or segmented take-profit based on ATR (some positions are profit-taking at a lower target, and some positions seek greater profits), optimizing the fund management strategy.
4. **Market status identification**: Add trend strength indicators (such as ADX) or volatility indicators to only execute transactions when the market meets specific conditions to avoid trading in an inefficient market environment.
5. **Risk Management Enhancement**: Add risk limits for each transaction and account risk management logic to ensure that single and overall risks are within control.
6. **Multi-indicator fusion**: Combined with other technical indicators (such as MACD, RSI or Bollinger Bands) as auxiliary confirmation, transactions will be executed only when multiple indicators resonate, improving signal reliability.
7. **Transaction volume adaptation logic**: Dynamically adjust the transaction size according to market liquidity and volatility, reduce positions when fluctuations are large, and increase positions during stable trends.
8. **Backtesting cycle expansion**: Conduct extensive backtesting under different market cycles and conditions to ensure that the strategy is stable in various market environments.
#### Summary
SuperTrend dynamic take-profit and time filter strategy is a comprehensive quantitative trading system that combines technical analysis and risk management. It captures trends through the SuperTrend indicator and utilizes multiple filtering mechanisms to improve signal quality. The main advantage of the strategy lies in its volatility adaptability and multi-layer risk control, while potential risks mainly come from indicator lag and parameter sensitivity.
The strategy can further improve its adaptability and profitability by implementing recommended optimization measures such as dynamic parameter adjustments, multi-timeframe confirmations and smart take-profit systems. The most important thing is that traders should understand the design principles and limitations of this strategy, combine their own risk preferences and market knowledge, and make personalized adjustments to the parameters to achieve the best trading results.
Overall, this is a trading strategy with a clear structure and strict logic. It has high practical value and customization potential, and is suitable for quantitative investors with certain trading experience. ||
#### Overview
The SuperTrend Dynamic Take-Profit with Time Filter Strategy is a volatility-adaptive quantitative trading system that relies on the SuperTrend indicator as a dynamic trailing stop tool. This strategy captures market trends by identifying moments when price breaks through the SuperTrend indicator line, combined with multiple filtering mechanisms including Moscow time (MSK) filter, price level filtering, and fixed percentage take-profit functionality. The system is designed as a multi-functional mode that can trade long positions only, short positions only, or enable bidirectional trading. The strategy visually displays trading direction on the chart through color changes: green areas indicate uptrends (long), while red areas indicate downtrends (short), greatly enhancing strategy visualization and operational decision-making convenience.

#### Strategy Principles
The core operation of this strategy is based on the following key mechanisms:

1. **SuperTrend Indicator Calculation**: The strategy uses the ATR indicator (default period 23) and a multiplier factor (default 1.8) to calculate the SuperTrend line, which automatically adjusts its position according to market volatility, forming dynamic support and resistance.

2. **Trade Signal Generation**:
   - Long entry signal: Triggered when the closing price breaks above the SuperTrend line (dir value changes from positive to negative) and meets time and price filtering conditions.
   - Short entry signal: Triggered when the closing price falls below the SuperTrend line (dir value changes from negative to positive) and meets filtering conditions.

3. **Trade Mode Selection**: The strategy offers three trading modes:
   - Long Only: Only executes long trades, closes positions on short signals.
   - Short Only: Only executes short trades, closes positions on long signals.
   - Both: Allows bidirectional trading.

4. **Multiple Filtering Systems**:
   - Moscow time filter (MSK, UTC+3): Allows users to set specific trading sessions, executing trades only within those periods.
   - Price level filtering: Sets a price threshold, executing long positions only when price is above the threshold and short positions when below.

5. **Dynamic Take-Profit Mechanism**: The strategy implements a fixed percentage take-profit (default 1.5%) based on entry price. Once price reaches the take-profit level, the strategy automatically closes positions to lock in profits. Take-profit levels can be visually displayed on the chart, and users can enable or disable this visualization as needed.

#### Strategy Advantages
After deep analysis of this code, I've identified the following significant advantages:

1. **Volatility Adaptability**: The SuperTrend indicator is based on ATR calculation, allowing it to automatically adjust tracking distance according to market volatility conditions. It increases protection distance in high-volatility markets and tracks price more closely in low-volatility markets, improving the strategy's adaptability to different market environments.

2. **Multiple Risk Controls**: The strategy integrates three layers of risk management: time filtering, price filtering, and take-profit settings. This multi-dimensional risk control mechanism significantly enhances trading safety.

3. **Flexible Trading Direction**: Options for long-only, short-only, or bidirectional trading allow the strategy to adapt to different market preferences and trading restrictions.

4. **Time-Intelligent Optimization**: The unique Moscow time filter allows trading during specific time periods, helping to avoid inefficient market sessions and specifically capturing efficient trading windows, particularly suitable for traders who need to consider international trading sessions.

5. **Visualization Advantages**: Through background color changes, SuperTrend line colors, and take-profit level markers, the strategy provides intuitive visual trading references, reducing analytical complexity.

6. **Commission-Optimized Design**: The strategy incorporates commission considerations (0.06%), making backtesting results closer to real trading environments.

7. **Close Price Execution Mechanism**: The strategy uses close price order execution (process_orders_on_close=true), reducing slippage impact and improving backtesting reliability.

#### Strategy Risks
Despite its excellent design, the strategy still has the following potential risks:

1. **Trend Reversal Delay**: The SuperTrend indicator is inherently a lagging indicator and may produce delayed signals during sharp market reversals, leading to untimely entries or exits and increased drawdown risk. The solution is to adjust ATR periods and multiplier factors to balance sensitivity and stability.

2. **Fixed Take-Profit Limitations**: Using a fixed percentage take-profit may lock in profits too early, missing out on additional gains during strong trends. It's recommended to dynamically adjust take-profit percentages based on market volatility or optimize take-profit strategies by combining other technical indicators.

3. **Parameter Sensitivity**: Strategy performance is highly dependent on parameter settings (ATR period, multiplier factor, take-profit percentage, etc.). Inappropriate parameters may lead to overtrading or missed signals. Optimal parameter combinations should be sought through historical data backtesting.

4. **Over-Restrictive Filters**: Overly strict time and price filtering may cause missed valid trading opportunities. Filter conditions should be adjusted according to the actual trading instrument and market characteristics.

5. **Market Condition Dependency**: This strategy performs excellently in markets with clear trends but may frequently produce false signals in oscillating markets. Consider adding market state recognition mechanisms to enable the strategy only in trending markets.

6. **Lack of Stop-Loss Mechanism**: Although SuperTrend can serve as a dynamic stop-loss reference, the code does not explicitly set stop-loss conditions, potentially facing significant losses in extreme market conditions. Adding a hard stop-loss mechanism is recommended.

#### Strategy Optimization Directions
Based on code analysis, I recommend the following optimization directions:

1. **Dynamic Parameter Adaptation**: Functions can be written to automatically adjust SuperTrend's ATR period and multiplier factor based on market states (such as volatility, volume, etc.), improving the strategy's adaptability. The advantage of this approach is that parameters can be automatically optimized as market conditions change, without manual intervention.

2. **Multi-Timeframe Confirmation**: By introducing SuperTrend direction confirmation from higher timeframes, low-quality signals can be effectively filtered. For example, executing trades on the 1-hour chart only when the SuperTrend direction on both daily and 4-hour charts align can significantly reduce losses from false breakouts.

3. **Intelligent Take-Profit System**: The current fixed percentage take-profit can be improved to a multi-tiered take-profit strategy, such as dividing positions into two parts with the first part taking profit at a smaller target (e.g., 0.8%) and the second part at a higher level (e.g., 2.5%), or dynamically setting take-profit levels based on ATR values to better adapt to current market volatility.

4. **Market State Recognition**: Integrate ADX (Average Directional Index) to measure trend strength, activating the strategy only when ADX is above a specific threshold (e.g., 25) to avoid frequent trading in oscillating markets. A volatility filter could also be added to pause trading during periods of abnormally high volatility.

5. **Enhanced Risk Management**: Add maximum loss limits for each trade and implement money management rules (such as the Kelly criterion or fixed proportion risk) to ensure that single trade risk does not exceed a specific percentage (e.g., 2%) of the total account.

6. **Multi-Indicator Fusion**: Combine SuperTrend with other technical indicators (such as moving average crossovers, RSI overbought/oversold zones, or MACD histogram) to establish multiple confirmation systems and improve signal quality. For example, execute long trades only when RSI shows oversold conditions and SuperTrend gives a buy signal.

7. **Trading Volume Adaptation Logic**: Dynamically adjust trading size based on market volatility and liquidity, for example, reducing position size when ATR values are large and increasing positions when ATR values are small and trends are clear, optimizing capital utilization efficiency.

8. **Extended Backtesting Period**: Conduct comprehensive backtesting across different market environments (bull markets, bear markets, ranging markets) and different time periods to ensure long-term stability and adaptability of the strategy. It's particularly important to test strategy performance under extreme market conditions.

#### Summary
The SuperTrend Dynamic Take-Profit with Time Filter Strategy is a comprehensive trading system that integrates trend following, time filtering, and take-profit management. Its core advantage lies in the volatility-adaptive SuperTrend indicator calculation and multi-level trading filtering mechanisms, enabling it to maintain relatively stable performance in changing market environments.

The strategy's main innovation point is combining the Moscow time filter with traditional SuperTrend trading logic, making it particularly suitable for traders considering the impact of international trading sessions. Meanwhile, the built-in fixed percentage take-profit function provides a simple yet effective profit protection mechanism, preventing profit giveback due to market reversals.

However, the strategy also faces challenges such as indicator lag and parameter sensitivity. By implementing the suggested optimization measures, such as dynamic parameter adjustment, multiple indicator confirmation, and enhanced risk management, the strategy's robustness and profitability can be significantly improved. Particularly through market state recognition mechanisms, the strategy can become more "intelligent," executing trades only under suitable market conditions.

For practical application, traders need to fine-tune strategy parameters according to the characteristics of specific trading instruments and personal risk preferences. Through continuous monitoring and regular optimization, this strategy can become an effective component of medium to long-term quantitative trading systems, contributing stable returns to investment portfolios.

In conclusion, this is a well-designed, clearly structured quantitative trading strategy with high practical value and expansion potential. With reasonable parameter settings and necessary risk controls, it can function effectively in various market environments, providing traders with reliable trading signals and profit protection mechanisms.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-26 00:00:00
end: 2024-07-11 00:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("Supertrend Fixed TP Unified with Time Filter (MSK)", overlay=true,
     default_qty_value=0.01,
     commission_type=strategy.commission.percent,
     commission_value=0.06,
     pyramiding=0,
     process_orders_on_close=true)

// Настройки индикатора
atrPeriod = input(23, "ATR Length")
factor = input.float(1.8, "Factor", step=0.1, minval=0.1)
tradeMode = input.string("Both", "Trade Mode", options=["Long Only", "Short Only", "Both"])

// Общий параметр тейк-профита
takeProfitPercent = input.float(1.5, "Take Profit (%)", minval=0.01)
showTP = input.bool(true, "▲▼ Показывать ТП") // Добавлен переключатель

// Фильтр цены
price_param = input.float(10000.0, "Цена фильтра", step=1.0)
use_price_filter = input.bool(false, "Использовать фильтр цены")

// Фильтр по времени (Московское время)
useTimeFilter = input.bool(true, "▲▼ Использовать фильтр по времени") // Переключатель фильтра времени
timeFrom = input.int(0, "Время С (часы MSK)", minval=0, maxval=23, step=1)
timeTo = input.int(23, "Время ДО (часы MSK)", minval=0, maxval=23, step=1)

// Функция проверки времени (с учетом Московского времени UTC+3)
isTimeInRange() =>
    if not useTimeFilter
        true // Фильтр отключен
    else
        // Переводим время сервера (UTC) в Московское время (UTC+3)
        mskHour = (hour(time) + 3) % 24 // Добавляем 3 часа для MSK
        if timeFrom <= timeTo
            mskHour >= timeFrom and mskHour < timeTo // До timeTo (не включая timeTo)
        else
            mskHour >= timeFrom or mskHour < timeTo // До timeTo (не включая timeTo)

// Расчет Supertrend
[supertrend, dir] = ta.supertrend(factor, atrPeriod)

// Визуализация Supertrend
plot(supertrend, "Supertrend", 
     color = dir < 0 ? color.green : color.red,
     linewidth = 2,
     style = plot.style_linebr)

bgcolor(dir < 0 ? color.new(color.green, 90) : color.new(color.red, 90))

// Сигналы входа с фильтром по времени
longEntry = (dir < 0 and dir[1] > 0) and (use_price_filter ? close > price_param : true) and isTimeInRange()
shortEntry = (dir > 0 and dir[1] < 0) and (use_price_filter ? close < price_param : true) and isTimeInRange()

// Логика стратегии
if tradeMode == "Both"
    if longEntry
        strategy.close("Short", comment="Close Short")
        strategy.entry("Long", strategy.long)
    if shortEntry
        strategy.close("Long", comment="Close Long")
        strategy.entry("Short", strategy.short)
else if tradeMode == "Long Only"
    if longEntry
        strategy.entry("Long", strategy.long)
    if shortEntry
        strategy.close("Long", comment="Close Long")
else if tradeMode == "Short Only"
    if shortEntry
        strategy.entry("Short", strategy.short)
    if longEntry
        strategy.close("Short", comment="Close Short")

// Управление тейк-профитом
var color tpColor = na
var float tpLevel = na
var label tpLabel = na

// Сброс при закрытии позиции
if strategy.position_size == 0 and strategy.position_size[1] != 0
    tpLevel := na
    tpColor := na
    label.delete(tpLabel)
    tpLabel := na

// Обновление ТП при открытии позиции
if strategy.position_size > 0
    entryPrice = strategy.opentrades.entry_price(0)
    tpLevel := entryPrice * (1 + takeProfitPercent/100)
    tpColor := color.green
    // Закрытие лонга по TP на закрытии бара
    if close >= tpLevel
        strategy.close("Long", comment="TP Long")
    // Обновление метки
    if showTP
        label.delete(tpLabel)
        tpLabel := label.new(
             bar_index, tpLevel, 
             text = str.tostring(tpLevel, "#.##"), 
             color = color.green, 
             textcolor = color.white,
             style = label.style_label_down,
             yloc = yloc.price)
    
if strategy.position_size < 0
    entryPrice = strategy.opentrades.entry_price(0)
    tpLevel := entryPrice * (1 - takeProfitPercent/100)
    tpColor := color.red
    // Закрытие шорта по TP на закрытии бара
    if close <= tpLevel
        strategy.close("Short", comment="TP Short")
    // Обновление метки
    if showTP
        label.delete(tpLabel)
        tpLabel := label.new(
             bar_index, tpLevel, 
             text = str.tostring(tpLevel, "#.##"), 
             color = color.red, 
             textcolor = color.white,
             style = label.style_label_up,
             yloc = yloc.price)

// Визуализация ТП
plot(showTP ? tpLevel : na, "Take Profit", 
     color = tpColor,
     linewidth = 1,
     style = plot.style_circles)

// Обновление позиции метки
if showTP and not na(tpLevel)
    label.set_xy(tpLabel, bar_index, tpLevel)
```

> Detail

https://www.fmz.com/strategy/488263

> Last Modified

2025-03-26 13:12:56
