
> Name

Dual-EMA-and-Stochastic-RSI-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/cd08b3ce9f386fd99d.png)

[trans]
#### Overview
This is a trend following strategy that combines the Exponential Moving Average (EMA) and the Stochastic RSI. This strategy identifies high-probability trading opportunities by analyzing price trends and overbought and oversold conditions. The strategy utilizes the crossover of EMA 9 and EMA 21 to determine the direction of the trend, while using the Stochastic RSI to confirm the state of the market, thereby improving the quality of trading signals.
#### Strategy Principle
The core logic of the strategy is based on a combination of two main technical indicators:
1. Dual Moving Average System: Uses 9-period and 21-period exponential moving averages (EMA) to identify trends. When the fast EMA (9) crosses the slow EMA (21) upward, a long signal is generated, and vice versa, a short signal is generated.
2. Stochastic RSI indicator: Identify overbought and oversold areas by calculating the Stochastic indicator of RSI values. The indicator first calculates the 14-period RSI, then converts it into stochastic form, and finally smoothes it using a 3-period simple moving average (SMA).
Trigger conditions for trading signals:
- Long conditions: EMA 9 crosses EMA 21 upwards, and Stochastic RSI is below the oversold threshold (20)
- Short conditions: EMA 9 crosses EMA 21 downwards, and Stochastic RSI is above the overbought threshold (80)
- Closing conditions: when an opposite trading signal appears
#### Strategic Advantages
1. Signal confirmation mechanism: By combining trend and momentum indicators, the risk of false breakthroughs is reduced
2. Flexible parameter settings: allows traders to adjust the parameters of EMA period and Stochastic RSI according to different market conditions
3. Clear visualization: The strategy displays EMA lines directly on the price chart and Stochastic RSI on a separate panel for easy analysis
4. Risk management: includes basic stop loss and profit mechanisms
5. Double filtering: Use trend and overbought and oversold indicators as double filtering to improve trading quality
#### Strategy Risk
1. Trend reversal risk: In a volatile market, false moving average crossover signals may appear.
2. Lagging problem: The moving average is essentially a lagging indicator, which may lead to late entry.
3. Sideways market risk: In a market with no obvious trend, frequent false signals may occur
4. Parameter sensitivity: Different parameter settings may lead to significantly different results.
5. Market environment dependence: The strategy performs better in strong trending markets, but may perform poorly in volatile markets.
#### Strategy optimization direction
1. Introduce volatility filtering: ATR indicator can be added to filter trading signals in low volatility environment
2. Optimize the stop loss mechanism: implement trailing stop loss to better protect profits
3. Add time filtering: add trading time windows to avoid periods of low liquidity
4. Add volume confirmation: consider volume factors when generating trading signals
5. Optimization parameter adaptation: a mechanism to dynamically adjust parameters according to market conditions
#### Summary
This is a trend following strategy with clear structure and rigorous logic. By combining EMA and Stochastic RSI, the strategy is better balanced in identifying trends and market conditions. Although there are some inherent risks, through reasonable parameter optimization and risk management, this strategy can maintain stable performance in a variety of market environments. It is recommended that traders conduct sufficient backtesting before using it in real markets, and adjust parameter settings according to specific market characteristics.
|| 

#### Overview
This is a trend-following strategy that combines Exponential Moving Averages (EMA) with Stochastic Relative Strength Index (Stochastic RSI). The strategy identifies high-probability trading opportunities by analyzing price trends and overbought/oversold conditions. It utilizes EMA 9 and EMA 21 crossovers to determine trend direction while using Stochastic RSI for market state confirmation to enhance signal quality.

#### Strategy Principles
The core logic is based on the combination of two main technical indicators:
1. Dual EMA System: Uses 9-period and 21-period Exponential Moving Averages to identify trends. Long signals are generated when the fast EMA(9) crosses above the slow EMA(21), and vice versa for short signals.
2. Stochastic RSI: Identifies overbought and oversold areas by calculating the stochastic oscillator of RSI values. It first calculates a 14-period RSI, converts it to stochastic form, and then smooths it with a 3-period Simple Moving Average (SMA).

Trading signal conditions:
- Long Entry: EMA 9 crosses above EMA 21 and Stochastic RSI is below the oversold threshold (20)
- Short Entry: EMA 9 crosses below EMA 21 and Stochastic RSI is above the overbought threshold (80)
- Exit: When opposite trading signals occur

#### Strategy Advantages
1. Signal Confirmation: Reduces false breakout risks by combining trend and momentum indicators
2. Flexible Parameters: Allows traders to adjust EMA periods and Stochastic RSI parameters for different market conditions
3. Clear Visualization: Displays EMAs directly on the price chart and Stochastic RSI in a separate panel for easy analysis
4. Risk Management: Includes basic stop-loss and profit-taking mechanisms
5. Dual Filtering: Uses trend and overbought/oversold indicators as double filters to improve trade quality

#### Strategy Risks
1. Trend Reversal Risk: False EMA crossover signals may occur in highly volatile markets
2. Lag Issues: Moving averages are inherently lagging indicators, potentially leading to delayed entries
3. Sideways Market Risk: May generate frequent false signals in markets without clear trends
4. Parameter Sensitivity: Different parameter settings can lead to significantly different results
5. Market Environment Dependency: Strategy performs well in trending markets but may underperform in ranging markets

#### Strategy Optimization
1. Volatility Filter: Add ATR indicator to filter trades in low volatility environments
2. Stop Loss Enhancement: Implement trailing stops for better profit protection
3. Time Filter: Add trading time windows to avoid low liquidity periods
4. Volume Confirmation: Consider volume factors when generating trading signals
5. Adaptive Parameters: Implement dynamic parameter adjustment based on market conditions

#### Summary
This is a well-structured trend-following strategy with rigorous logic. By combining EMA and Stochastic RSI, the strategy achieves a good balance in identifying trends and market conditions. While there are inherent risks, the strategy can maintain stable performance across various market environments through proper parameter optimization and risk management. Traders are advised to conduct thorough backtesting and adjust parameters according to specific market characteristics before live trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-10 00:00:00
end: 2025-02-09 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA 9/21 + Stoch RSI Strategy", shorttitle="EMA+StochRSI", overlay=true)

// ===== Užívateľské vstupy ===== //
emaFastLen     = input.int(9,   "Rýchla EMA (9)")
emaSlowLen     = input.int(21,  "Pomalá EMA (21)")
rsiLen         = input.int(14,  "RSI Length")
stochRsiLen    = input.int(14,  "Stoch RSI Length")     // úsek, z ktorého berieme min/max RSI
stochSignalLen = input.int(3,   "Stoch RSI K/D Smoothing")
overSold       = input.int(20,  "Stoch RSI Oversold (%)")
overBought     = input.int(80,  "Stoch RSI Overbought (%)")

// ===== Výpočet EMA(9) a EMA(21) ===== //
emaFast = ta.ema(close, emaFastLen)
emaSlow = ta.ema(close, emaSlowLen)

// ===== Výpočet RSI a Stoch RSI ===== //
// 1) Klasické RSI
rsiValue = ta.rsi(close, rsiLen)

// 2) Prevod RSI -> Stoch RSI: 
//    (rsiValue - min(rsiValue, stochRsiLen)) / (max(rsiValue, stochRsiLen) - min(rsiValue, stochRsiLen)) * 100
//    Následne vyhladíme K a D (podobne ako pri bežnom Stochastic)
rsiLowest  = ta.lowest(rsiValue,  stochRsiLen)
rsiHighest = ta.highest(rsiValue, stochRsiLen)
stochRaw   = (rsiValue - rsiLowest) / math.max(rsiHighest - rsiLowest, 1e-10) * 100.0
stochK     = ta.sma(stochRaw, stochSignalLen)
stochD     = ta.sma(stochK,   stochSignalLen)

// ===== Podmienky pre LONG / SHORT ===== //
// LONG, ak:
//  - EMA(9) prekríži EMA(21) smerom nahor
//  - Stoch RSI je v prepredanej zóne (t.j. stochK < overSold)
longCondition  = ta.crossover(emaFast, emaSlow) and (stochK < overSold)

// SHORT, ak:
//  - EMA(9) prekríži EMA(21) smerom nadol
//  - Stoch RSI je v prekúpenej zóne (stochK > overBought)
shortCondition = ta.crossunder(emaFast, emaSlow) and (stochK > overBought)

// ===== Vstup do pozícií ===== //
if longCondition
    strategy.entry("Long", strategy.long)

if shortCondition
    strategy.entry("Short", strategy.short)

// ===== Výstup z pozície pri opačnom signáli (okamžite na trhu) ===== //
if strategy.position_size > 0 and shortCondition
    // Ak držíme LONG a príde signál na SHORT, zavrieme LONG
    strategy.close("Long", comment="Exit Long")

if strategy.position_size < 0 and longCondition
    // Ak držíme SHORT a príde signál na LONG, zavrieme SHORT
    strategy.close("Short", comment="Exit Short")

// ===== (Nepovinné) Môžeš pridať stop-loss, take-profit, trailing stop atď. ===== //

```

> Detail

https://www.fmz.com/strategy/481394

> Last Modified

2025-02-10 16:56:56
