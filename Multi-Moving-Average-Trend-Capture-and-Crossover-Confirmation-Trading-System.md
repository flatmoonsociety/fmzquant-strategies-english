
> Name

Multi-Moving-Average-Trend-Capture-and-Crossover-Confirmation-Trading-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8bfbe35bb20e733db4b.png)
![IMG](https://www.fmz.com/upload/asset/2d8de425b6dafbb6f9fe6.png)


[trans]## Overview
The multiple moving average trend capture and cross-confirmation trading system is a quantitative trading strategy based on a multi-period exponential moving average (EMA) combination, which combines the relative strength index (RSI), the moving average trend difference (MACD) and the average true range (ATR) as auxiliary indicators. The core of this strategy is to determine the direction of the market trend by comparing the relationship between moving average positions in different time periods, and to open a position when the trend is clear and close the position when the trend weakens or reverses. The strategy is specially designed for a multi-period trend confirmation mechanism, which determines the strength and sustainability of the trend through the positional relationship between the short-term moving average and the medium- and long-term moving average, thereby improving the winning rate and stability of the transaction.
## Strategy Principle
The core principle of this strategy is to use multiple exponential moving averages (EMA) of different periods to determine market trends and capture trading opportunities. Five EMAs are used in the strategy: instantaneous moving average (14 periods), intermediate moving average (25 periods), short-term moving average (50 periods), medium-term moving average (100 periods) and long-term moving average (200 periods).
The main logic of the strategy is as follows:
1. **Trend Judgment Mechanism**:
   - Uptrend conditions: the instantaneous moving average is above the short-term, medium-term and long-term moving averages, and the short-term moving average is above the medium-term moving average
   - Downtrend conditions: the instantaneous moving average is below the short-term, medium-term and long-term moving average, and the short-term moving average is below the long-term moving average
2. **Entry signal**:
   - Long entry: when the uptrend conditions are met and no positions are currently held
   - Short entry: When the downtrend conditions are met and no positions are currently held, and the minimum ATR conditions are met (the market volatility is sufficient)
3. **Exit signal**:
   - Long position closing: when the instantaneous moving average falls below the short-term moving average
   - Short position closing: when the instantaneous moving average crosses the medium-term moving average
4. **Risk Control**:
   - Use the ATR indicator as a volatility filter and only take short trades when the volatility is sufficient (ATR is greater than its average)
   - Integrated RSI overbought and oversold levels as a potential additional filter (although defined in the code but not used in the current trading logic)
5. **Location Tracking**:
   - The strategy uses Boolean variables to track whether a position is currently open and the direction of the position (long or short)
## Strategic Advantages
1. **Multiple moving average confirmation**: Confirm the trend through multiple moving averages of different periods, reduce false breakthroughs and false signals, and improve signal quality.
2. **Accurate trend identification**: Compared with a single moving average system, a multiple moving average system can more accurately identify the turning point of the market trend, especially when the relative position of the instantaneous moving average and other moving averages changes.
3. **Flexible risk management**: Different entry and exit standards are adopted for long and short positions, which reflects the differentiated treatment of risks in different directions of the market, and additional volatility filtering is added for short transactions.
4. **Visual trading signals**: The strategy clearly displays the buying, selling, and closing points through graphical markers, which facilitates backtest analysis and real-time monitoring.
5. **Trend background visualization**: Use background color to distinguish upward trends and downward trends, visually display the market environment, and facilitate traders to quickly judge the current market status.
6. **Potential scalability**: The calculation of RSI and MACD indicators has been integrated. Although it is not currently used in trading logic, it provides a basis for future optimization of the strategy.
7. **Parameter Adjustability**: All key parameters can be adjusted through input control, including moving average period, RSI threshold, MACD parameters and ATR settings, to facilitate optimization according to different market environments and trading varieties.
## Strategy Risk
1. **Moving average lag**: All systems based on moving averages have a certain degree of lag, and large retracements may occur in volatile markets or rapid reversals. The solution is to adjust the moving average period or add additional concussive market filter conditions.
2. **Over-trading risk**: In a volatile market, the instantaneous moving average may frequently cross the short-term moving average, leading to over-trading. Invalid trades can be reduced by increasing the minimum holding time or adding additional filters.
3. **Different market adaptability issues**: The performance of the moving average strategy with fixed parameters varies greatly in different market environments and trading varieties. Parameter optimization should be performed for specific markets, or the use of adaptive parameters should be considered.
4. **Signal Conflict**: Although the RSI and MACD indicators are calculated in the code, they are not effectively integrated in the trading logic, which may lead to potential signal conflicts or missed optimization opportunities.
5. **Long Bias**: The current strategy uses different standards for longs and shorts. There is no volatility filter for longs, while shorts need to meet minimum ATR conditions, which may make the strategy more aggressive in rising markets and increase risk exposure.
6. **Fixed exit mechanism**: The strategy uses a fixed technical indicator crossover as the exit point. It lacks a stop-profit and stop-loss mechanism that is dynamically adjusted according to market conditions, and may not be able to effectively lock in profits or control risks.
7. **Parameter sensitivity**: The strategy relies on multiple moving average cycle parameters. Small changes in these parameters may lead to significant differences in trading results, increasing the risk of overfitting.
## Strategy optimization direction
1. **Integrating Calculated Indicators**: The strategy has calculated RSI and MACD indicators but is not fully utilizing them. RSI can be used to filter out extreme market conditions, and MACD can be used to confirm trend direction and improve signal quality. For example, you can require that the RSI is not in the overbought area when longs enter, and the RSI is not in the oversold area when shorts enter.
2. **Dynamic Stop Loss System**: Introduce a dynamic stop loss mechanism based on ATR, automatically adjust the stop loss distance according to market volatility, and improve risk management capabilities. This can be achieved by calculating the entry point plus or minus a certain multiple of the ATR value.
3. **Market status classification**: Increase the judgment mechanism of market status (trending market vs. volatile market), and adopt different trading strategies in different market conditions. For example, the strength of a market trend can be judged by the slope of a long-term moving average or the ADX indicator.
4. **Multiple time frame analysis**: Integrate trend information of higher time periods and only trade when the trend direction of higher time periods is consistent to increase the winning rate.
5. **Optimizing moving average parameters**: The current strategy uses a fixed moving average period (14, 25, 50, 100, 200). You can backtest different parameter combinations to find the optimal parameters that are more suitable for specific markets.
6. **Add trading volume confirmation**: Combine trading volume indicators to confirm trend strength, only trade in trends supported by trading volume, and reduce losses caused by false breakthroughs.
7. **Improve entry conditions**: Optimize the entry logic of long and short positions to make them more symmetrical, or make more detailed adjustments based on the characteristics of different market directions. For example, consider adding volatility filtering when entering long positions, or adjusting the stringency of trend confirmations.
8. **Add time filter**: Add trading time filter to avoid periods of greater market volatility or poor liquidity, such as important data releases or market opening and closing periods.
## Summarize
The multiple moving average trend capture and cross-confirmation trading system is a quantitative trading strategy based on technical analysis. It judges the market trend through a combination of multiple moving averages of different periods, opens a position when the trend is clear, and closes the position when the trend weakens. The core advantage of the strategy is to use multiple moving average crossovers to confirm trends, reduce false signals, and improve transaction quality.
This strategy performs better in markets with clear trends, but may face the risk of overtrading in volatile markets. By integrating the calculated RSI and MACD indicators, introducing a dynamic stop loss mechanism, optimizing the moving average parameter combination, and adding market status classification, the stability and adaptability of the strategy can be further improved.
For practical applications, it is recommended to conduct sufficient backtesting on different market environments and trading varieties, adjust parameters to adapt to specific market characteristics, and control single transaction risks in conjunction with fund management strategies. In addition, this strategy can be considered as part of an investment portfolio and used in conjunction with other complementary strategies to diversify trading risks and improve the stability of the overall investment portfolio. || ## Overview
The Multi-Moving Average Trend Capture and Crossover Confirmation Trading System is a quantitative trading strategy based on a combination of multiple exponential moving averages (EMAs) of different periods, complemented by auxiliary indicators including Relative Strength Index (RSI), Moving Average Convergence Divergence (MACD), and Average True Range (ATR). The core of this strategy lies in determining market trend direction by comparing the relative positions of moving averages across different timeframes, entering positions when trends are clearly established, and exiting when trends weaken or reverse. The strategy features a specially designed multi-period trend confirmation mechanism that assesses trend strength and sustainability through the relative positions of short-term averages against medium and long-term averages, thereby improving win rates and stability.

## Strategy Principles

The core principle of this strategy is to utilize multiple exponential moving averages (EMAs) of different periods to identify market trends and capture trading opportunities. The strategy employs five EMAs: instant average (14 periods), intermediate average (25 periods), short-term average (50 periods), medium-term average (100 periods), and long-term average (200 periods).

The main logic of the strategy is as follows:

1. **Trend Determination Mechanism**:
   - Uptrend conditions: Instant EMA above short-term, medium-term, and long-term EMAs, with short-term EMA above medium-term EMA
   - Downtrend conditions: Instant EMA below short-term, medium-term, and long-term EMAs, with short-term EMA below long-term EMA

2. **Entry Signals**:
   - Long entry: When uptrend conditions are met and no position is currently open
   - Short entry: When downtrend conditions are met, no position is currently open, and minimum ATR conditions are satisfied (sufficient market volatility)

3. **Exit Signals**:
   - Long exit: When the instant EMA crosses below the short-term EMA
   - Short exit: When the instant EMA crosses above the medium-term EMA

4. **Risk Control**:
   - Uses the ATR indicator as a volatility filter, only executing short trades when volatility is sufficient (ATR greater than its average)
   - Integrates RSI overbought and oversold levels as potential additional filters (though defined in the code but not currently utilized in the trading logic)

5. **Position Tracking**:
   - The strategy uses boolean variables to track whether a position is currently open and the direction of the position (long or short)

## Strategy Advantages

1. **Multiple Moving Average Confirmation**: By using multiple moving averages of different periods to jointly confirm trends, the strategy reduces false breakouts and erroneous signals, improving signal quality.

2. **Precise Trend Identification**: Compared to single moving average systems, multiple moving average systems can more accurately identify market trend turning points, especially when the relative position of the instant average changes in relation to other averages.

3. **Flexible Risk Management**: Different entry and exit criteria are applied to long and short positions, reflecting differentiated handling of risks in different market directions, with short trades requiring additional volatility filtering.

4. **Visualized Trading Signals**: The strategy clearly displays buy, sell, and exit points through graphical markers, facilitating backtesting analysis and real-time monitoring.

5. **Trend Background Visualization**: Using background colors to distinguish between uptrends and downtrends, providing an intuitive display of market conditions for traders to quickly assess the current market state.

6. **Potential for Expansion**: The strategy has already integrated RSI and MACD indicator calculations, which, although not currently used in the trading logic, provide a foundation for future optimization.

7. **Parameter Adjustability**: All key parameters can be controlled through inputs for adjustment, including moving average periods, RSI thresholds, MACD parameters, and ATR settings, making it convenient to optimize for different market environments and trading instruments.

## Strategy Risks

1. **Moving Average Lag**: All systems based on moving averages have inherent lag, which may result in significant drawdowns in oscillating markets or during rapid reversals. Solutions include adjusting moving average periods or adding additional filters for oscillating market conditions.

2. **Overtrading Risk**: In oscillating markets, the instant moving average may frequently cross the short-term moving average, leading to excessive trading. This can be mitigated by introducing minimum holding periods or additional filters to reduce ineffective trades.

3. **Market Adaptability Issues**: Moving average strategies with fixed parameters tend to perform differently across various market environments and trading instruments. Parameters should be optimized for specific markets, or adaptive parameters should be considered.

4. **Signal Conflicts**: Although RSI and MACD indicators are calculated in the code, they are not effectively integrated into the trading logic, potentially leading to signal conflicts or missed optimization opportunities.

5. **Long Bias**: The current strategy applies different standards to long and short positions, with long positions not requiring volatility filtering while short positions must meet minimum ATR conditions, which may make the strategy more aggressive in bullish markets, increasing risk exposure.

6. **Fixed Exit Mechanism**: The strategy uses fixed technical indicator crossovers as exit points, lacking dynamic stop-loss and take-profit mechanisms that adjust according to market conditions, which may fail to effectively lock in profits or control risks.

7. **Parameter Sensitivity**: The strategy relies on multiple moving average period parameters, and small changes in these parameters can lead to significant differences in trading results, increasing the risk of overfitting.

## Strategy Optimization Directions

1. **Integrate Calculated Indicators**: The strategy has already calculated RSI and MACD indicators but does not fully utilize them. RSI can be used to filter extreme market conditions, and MACD to confirm trend direction, improving signal quality. For example, requiring that RSI is not in overbought territory for long entries and not in oversold territory for short entries.

2. **Dynamic Stop-Loss System**: Introduce a dynamic stop-loss mechanism based on ATR, automatically adjusting stop-loss distances according to market volatility, enhancing risk management capabilities. This can be implemented by calculating entry points plus or minus a certain multiple of the ATR value.

3. **Market State Classification**: Add mechanisms to classify market states (trending vs. oscillating) and apply different trading strategies in different market states. For example, the slope of the long-term moving average or the ADX indicator can be used to assess trend strength.

4. **Multi-Timeframe Analysis**: Integrate trend information from higher timeframes, only trading when the trend direction aligns with higher timeframes, improving win rates.

5. **Optimize Moving Average Parameters**: The current strategy uses fixed moving average periods (14, 25, 50, 100, 200). Through backtesting different parameter combinations, optimal parameters for specific markets can be identified.

6. **Volume Confirmation**: Incorporate volume indicators to confirm trend strength, only trading in trends supported by volume, reducing losses from false breakouts.

7. **Improve Entry Conditions**: Optimize entry logic for both long and short positions to make them more symmetrical, or make more refined adjustments based on the characteristics of different market directions. For example, consider adding volatility filtering for long entries or adjusting the strictness of trend confirmation.

8. **Add Time Filters**: Incorporate trading time filters to avoid periods of high market volatility or poor liquidity, such as during important data releases or market opening/closing sessions.

## Summary

The Multi-Moving Average Trend Capture and Crossover Confirmation Trading System is a quantitative trading strategy based on technical analysis that uses a combination of multiple moving averages of different periods to identify market trends, entering positions when trends are clearly established and exiting when trends weaken. The core advantage of the strategy lies in using multiple moving average crossovers to confirm trends, reducing erroneous signals and improving trading quality.

This strategy performs well in markets with clear trends but may face risks of overtrading in oscillating markets. By integrating the already calculated RSI and MACD indicators, introducing dynamic stop-loss mechanisms, optimizing moving average parameter combinations, and adding market state classification, the stability and adaptability of the strategy can be further enhanced.

For practical application, it is recommended to first conduct thorough backtesting across different market environments and trading instruments, adjusting parameters to adapt to specific market characteristics, and combining with money management strategies to control single-trade risk. Additionally, consider using this strategy as part of an investment portfolio, combined with other complementary strategies to diversify trading risk and improve overall portfolio stability.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-23 00:00:00
end: 2025-03-02 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("etude9", shorttitle="etude 9", overlay=true)
//on tente de comlbiner avec le RSi un stratégie pas si mauvaise sur les longs 
// un d7 r rsi qui donne des indiciataions pas mal pour les short pour les long pas très concluant 
// === Paramètres d'entrée ===
// Source de prix
// et merde rendement sur long est plus efficace sans condition sur ATR !!
// par contre j'ai l'imression que le rsi ça va être bien pour les shorts 
// bon avec le RSi ça donne rien, et avec le macd, ç ce stade c'est foireux mmm 
pricetype = input(close, title="Source de prix pour les moyennes mobiles")

// Périodes des moyennes mobiles
instant = input(14, title="Période de la moyenne instantanée (10)")
interm = input(25, title="Perdiode intermediaire (25)")
shortperiod = input(50, title="Période de la moyenne mobile courte (20)")
mediumperiod = input(100, title="Période de la moyenne mobile moyenne (50)")
longperiod = input(200, title="Période de la moyenne mobile longue (100)")

// Paramètres du RSI
rsi_length = input.int(14, title="Période RSI")
rsi_overbought = input.int(78, title="Niveau de surachat (RSI)")
rsi_oversold = input.int(30, title="Niveau de survente (RSI)")

// Paramètres pour le MACD
fast_length = input.int(12, title="Longueur Rapide MACD")
slow_length = input.int(26, title="Longueur Lente MACD")
signal_length = input.int(9, title="Longueur du Signal MACD")

// Paramètres de l'ATR
atr_length = input.int(14, title="Période ATR")
atr_multiplier = input.float(1.5, title="Multiplicateur ATR pour le Stop-Loss")

// Calcul de l'ATR
atr = ta.atr(atr_length)

// === Calcul des moyennes mobiles (EMA uniquement) ===
instant_ma = ta.ema(pricetype, instant) // Moyenne mobile instantanée
short_ma = ta.ema(pricetype, shortperiod)  // Moyenne mobile courte (20)
medium_ma = ta.ema(pricetype, mediumperiod)  // Moyenne mobile moyenne (50)
long_ma = ta.ema(pricetype, longperiod)    // Moyenne mobile longue (100)
interm_ma = ta.ema(pricetype, interm)

// Calcul du RSI
rsi = ta.rsi(close, rsi_length)

// Calcul du MACD
[macd_line, signal_line, hist_line] = ta.macd(close, fast_length, slow_length, signal_length)

// Stocker les résultats de crossover et crossunder dans des variables globales
is_crossover = ta.crossover(macd_line, signal_line)
is_crossunder = ta.crossunder(macd_line, signal_line)

// Filtre ATR : on ne trade que si la volatilité est suffisante
min_atr = atr > ta.sma(atr, atr_length)  // ATR supérieur à sa moyenne

// === Conditions de tendance ===
trending_up = instant_ma > short_ma and instant_ma > medium_ma and instant_ma > long_ma and short_ma > medium_ma   // Tendance haussière
trending_down = instant_ma< short_ma and instant_ma<medium_ma and instant_ma<long_ma and short_ma<long_ma  // Tendance baissière
// Filtre RSI
rsi_filter_buy = rsi < rsi_overbought  // RSI n'est pas en surachat pour un achat
rsi_filter_sell = rsi > rsi_oversold  // RSI n'est pas en survente pour une vente

// === Gestion des positions ===
var bool in_position = false  // Variable pour suivre si une position est ouverte
var bool is_long = false      // Variable pour suivre si la position est longue ou courte

// === Signaux d'ouverture et de fermeture ===
bool buy_signal = false  // Signal d'ouverture d'une position longue
bool close_signal = false  // Signal de fermeture d'une position longue
bool sell_signal = false  // Signal d'ouverture d'une position courte
bool close_short_signal = false  // Signal de fermeture d'une position courte


// Ouvrir une position longue
if (trending_up and not in_position)
    strategy.entry("Long", strategy.long)
    in_position := true
    is_long := true
    buy_signal := true  // Signal d'ouverture
else
    buy_signal := false

// Fermer la position longue si instant_ma < medium_ma
if (in_position and is_long and instant_ma < short_ma)
    strategy.close("Long")
    in_position := false
    is_long := false
    close_signal := true  // Signal de fermeture
else
    close_signal := false

// Ouvrir une position courte
if (trending_down and not in_position and min_atr)
    strategy.entry("Short", strategy.short)
    in_position := true
    is_long := false
    sell_signal := true  // Signal d'ouverture
else
    sell_signal := false
// Fermer la position courte si instant_ma > medium_ma
if (in_position and not is_long and instant_ma > medium_ma)
    strategy.close("Short")
    in_position := false
    close_short_signal := true  // Signal de fermeture
else
    close_short_signal := false
// === Affichage des signaux sur le graphique ===
plotshape(series=buy_signal, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="Buy", size=size.small)
plotshape(series=sell_signal, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="Sell", size=size.small)
plotshape(series=close_signal, title="Close Long Signal", location=location.abovebar, color=color.orange, style=shape.labeldown, text="Close Long", size=size.small)
plotshape(series=close_short_signal, title="Close Short Signal", location=location.belowbar, color=color.blue, style=shape.labelup, text="Close Short", size=size.small)

// === Affichage des moyennes mobiles sur le graphique ===
plot(short_ma, color=color.blue, title="Moyenne mobile courte (20)", linewidth=2)
plot(medium_ma, color=color.orange, title="Moyenne mobile moyenne (50)", linewidth=2)
plot(long_ma, color=color.red, title="Moyenne mobile longue (100)", linewidth=2)
plot(instant_ma, color=color.rgb(43, 14, 111), title="Moyenne mobile instantanée (10)", linewidth=2)
plot(interm_ma, color=color.rgb(26, 192, 34), title="Moyenne mobile instantanée (10)", linewidth=2)

// Coloration de fond pour les tendances
bgcolor(color=trending_up ? color.new(color.green, 90) : trending_down ? color.new(color.red, 90) : na, title="Coloration de fond")
```

> Detail

https://www.fmz.com/strategy/484584

> Last Modified

2025-03-03 10:11:37
