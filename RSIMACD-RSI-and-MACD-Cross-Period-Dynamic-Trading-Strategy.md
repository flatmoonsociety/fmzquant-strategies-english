
> Name

RSI and MACD Cross Multi-Period Dynamic Trading Strategy-RSI-and-MACD-Cross-Period-Dynamic-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d7f12d7f38314fd3770e.png)
![IMG](https://www.fmz.com/upload/asset/2d963babd911bcbe070f3.png)




[trans]
#### Overview
The RSI and MACD cross multi-period dynamic trading strategy is a quantitative trading system that combines the relative strength index (RSI) and the moving average convergence divergence indicator (MACD), and is specially designed for the 15-minute K-line cycle. This strategy monitors the market for overbought and oversold conditions (RSI) and the price momentum trend (MACD), triggering trading signals when both indicators meet specific conditions simultaneously. Specifically, when the RSI value is below 30 (oversold) and the MACD fast line crosses the signal line, the system generates a buy signal; when the RSI value is above 70 (overbought) and the MACD fast line crosses below the signal line, the system generates a sell signal. Each transaction is configured with a percentage-based take-profit (5%) and stop-loss (2%) mechanism, effectively controlling the risk-reward ratio at a good level of 2.5:1.
#### Strategy Principle
The core of this strategy is to logically combine the signals of two classic technical indicators to improve the reliability of trading decisions:
1. **RSI indicator application**: Use the default 14-period RSI to identify overbought and oversold conditions in the market. Conventional wisdom holds that RSI below 30 is oversold (possible rebound), and above 70 is overbought (possible pullback). The code uses `ta.rsi(close, rsiLength)` to calculate the RSI value.
2. **MACD indicator application**: adopt the standard parameter settings of fast line period 12, slow line period 26, and signal line smoothing factor 9. MACD is calculated through the `ta.macd(close, macdFast, macdSlow, macdSignal)` function to obtain the MACD line and signal line. Key trading signals come from the intersection of the MACD line and the signal line, captured by the `ta.crossover` and `ta.crossunder` ​​functions.
3. **Combined signal logic**:
   - Conditions for opening a long position: RSI < 30 (oversold) AND MACD fast line crosses the signal line
   - Short position opening conditions: RSI > 70 (overbought) AND MACD fast line crosses the signal line
4. **Fund Management**: The strategy uses the percentage of account funds for position management (`default_qty_type=strategy.percent_of_equity, default_qty_value=100`), and 100% of the total funds are invested in each transaction.
5. **Risk Control**: The take-profit level (±5% of the entry price) and the stop-loss level (±2% of the entry price) are automatically set for each transaction, which is implemented through the `strategy.exit` function.
#### Strategic Advantages
1. **Indicator Collaborative Confirmation**: Combining the two indicators RSI and MACD, double confirmation is required to issue a trading signal, effectively reducing the occurrence of false breakthroughs and false signals, and improving the quality of transactions.
2. **Balanced entry and exit mechanism**: Entry is based on the objective judgment of technical indicators, and exit is based on preset take-profit and stop-loss levels, forming a complete closed-loop transaction and reducing interference from subjective factors.
3. **Good risk-reward ratio**: The take-profit ratio (5%) is 2.5 times the stop-loss ratio (2%), which is in line with the risk management principles of professional trading. As long as the winning rate exceeds 30%, long-term profits can be achieved.
4. **Adapt to market rhythm**: The 15-minute period is suitable for day traders. It can capture short-term fluctuations without over-trading, balancing trading frequency and signal quality.
5. **Visual feedback**: The strategy provides traders with an intuitive visual reference by drawing RSI indicator lines and overbought and oversold horizontal lines to facilitate real-time monitoring of market status.
#### Strategy Risk
1. **Concussive market risk**: In a sideways volatile market, RSI may frequently hover in the overbought and oversold areas, and MACD may also produce multiple crossovers, leading to excessive trading and continuous losses. The solution is to add additional trend filters such as moving averages or the ADX indicator.
2. **Parameter Sensitivity**: Strategy performance is more sensitive to the parameter settings of RSI and MACD. The traditional default parameters are currently used, which may not be suitable for all market environments. It is recommended to optimize parameters according to specific trading varieties and market characteristics.
3. **Fixed take-profit and stop-loss limits**: Using a fixed percentage of take-profit and stop-loss may not be able to adapt to the fluctuation characteristics of different markets. High-volatility markets may result in stops being taken too frequently, while low-volatility markets may make it difficult to hit take-profit targets.
4. **Lack of trading time control**: The current strategy does not set trading time filtering, which may generate adverse signals during periods of poor liquidity or abnormal fluctuations.
5. **No backhand mechanism**: The long and short signals in the strategy are triggered independently, and the lack of an effective backhand trading mechanism may lead to greater losses for reverse positions in strong trending markets.
#### Strategy optimization direction
1. **Dynamic parameter adjustment**: You can consider dynamically adjusting the overbought and oversold thresholds of RSI and MACD parameters based on market volatility (such as the ATR indicator) to adapt to different market environments. The implementation method is as follows:   
```
   atrValue = ta.atr(14)
   dynamicRsiOversold = 30 - (atrValue / close * 100)
   dynamicRsiOverbought = 70 + (atrValue / close * 100)
   
```

2. **Add trend filter**: Introduce additional trend confirmation indicators, such as adding the ADX indicator, and only execute transactions when ADX>25 (indicating that the market has an obvious trend) to avoid frequent transactions in volatile markets:   
```
   adxValue = ta.adx(14)
   adxFilter = adxValue > 25
   longCondition = (rsi < rsiOversold) and macdCrossUp and adxFilter
   
```

3. **Optimize fund management**: Instead of fixing 100% fund ratio, position management based on volatility can be adopted. The greater the volatility, the smaller the position:   
```
   positionSize = 100 / (ta.atr(14) / close * 100)
   
```

4. **Introduction of time filtering**: Add trading time window control to avoid market opening, closing and low liquidity periods:   
```
   timeFilter = (time >= timestamp("00:30:00")) and (time <= timestamp("23:00:00"))
   
```

5. **Improved stop-profit and stop-loss mechanism**: Adopt take-profit and stop-loss based on technical level, such as using previous high and low points, support and resistance levels or ATR multiples as dynamic stop-loss points instead of fixed percentages:   
```
   atrValue = ta.atr(14)
   dynamicStopLoss = atrValue * 1.5
   
```

#### Summarize
The RSI and MACD cross multi-period dynamic trading strategy is a quantitative trading system with a clear structure and clear logic. It provides relatively reliable trading signals by integrating the advantages of the overbought and oversold indicator (RSI) and the momentum trend indicator (MACD). This strategy is particularly suitable for short-term trading with a 15-minute period. Its core advantage lies in the dual-indicator confirmation mechanism and clear capital risk management rules.
Although the strategy design is reasonable, there are still challenges of parameter sensitivity and market adaptability. By introducing optimization measures such as dynamic parameter adjustment, trend filters, optimized fund management, time filtering, and improved stop-profit and stop-loss mechanisms, the robustness and adaptability of the strategy can be further improved.
Any quantitative strategy needs to undergo comprehensive historical backtesting and forward verification, while being personalized and adjusted based on specific market conditions and trader risk preferences. This strategy provides a good quantitative trading framework, on which traders can carry out secondary development and optimization to build a more complete trading system. ||
#### Overview

The RSI and MACD Cross-Period Dynamic Trading Strategy is a quantitative trading system that combines the Relative Strength Index (RSI) and Moving Average Convergence Divergence (MACD) indicators, specifically designed for 15-minute chart intervals. This strategy monitors market overbought/oversold conditions (RSI) and price momentum trends (MACD), triggering trading signals when both indicators simultaneously meet specific criteria. Specifically, when the RSI value falls below 30 (oversold) and the MACD fast line crosses above the signal line, the system generates a buy signal; when the RSI value rises above 70 (overbought) and the MACD fast line crosses below the signal line, the system generates a sell signal. Each trade is configured with percentage-based take profit (5%) and stop loss (2%) mechanisms, effectively maintaining a favorable risk-reward ratio of 2.5:1.

#### Strategy Principles

The core of this strategy lies in combining signals from two classic technical indicators to enhance the reliability of trading decisions:

1. **RSI Application**: Uses the default 14-period RSI to identify market overbought and oversold conditions. The traditional view considers RSI below 30 as oversold (potential bounce) and above 70 as overbought (potential reversal). The code calculates RSI values using `ta.rsi(close, rsiLength)`.

2. **MACD Application**: Employs standard parameters with a fast period of 12, slow period of 26, and signal smoothing factor of 9. MACD is calculated through the `ta.macd(close, macdFast, macdSlow, macdSignal)` function, yielding the MACD line and signal line. Key trading signals derive from crossovers between the MACD line and signal line, captured by the `ta.crossover` and `ta.crossunder` functions.

3. **Combined Signal Logic**:
   - Long entry condition: RSI < 30 (oversold) AND MACD fast line crosses above the signal line
   - Short entry condition: RSI > 70 (overbought) AND MACD fast line crosses below the signal line

4. **Capital Management**: The strategy employs account equity percentage for position sizing (`default_qty_type=strategy.percent_of_equity, default_qty_value=100`), investing 100% of total funds in each trade.

5. **Risk Control**: Each trade automatically sets take-profit levels (±5% of entry price) and stop-loss levels (±2% of entry price), implemented through the `strategy.exit` function.

#### Strategy Advantages

1. **Indicator Confirmation Synergy**: By combining RSI and MACD indicators, the strategy requires dual confirmation to issue trading signals, effectively reducing false breakouts and misleading signals, thus improving trade quality.

2. **Balanced Entry and Exit Mechanism**: Entries are based on objective technical indicator assessments, while exits rely on preset take-profit and stop-loss levels, forming a complete trading loop and reducing subjective interference.

3. **Favorable Risk-Reward Ratio**: The take-profit percentage (5%) is 2.5 times the stop-loss percentage (2%), aligning with professional trading risk management principles—requiring only a win rate above 30% to achieve long-term profitability.

4. **Market Rhythm Adaptation**: The 15-minute timeframe suits intraday traders, capturing short-term fluctuations without overtrading, balancing trading frequency and signal quality.

5. **Visual Feedback**: The strategy plots the RSI indicator line and overbought/oversold level lines, providing traders with intuitive visual references for real-time market condition monitoring.

#### Strategy Risks

1. **Consolidation Market Risk**: In sideways, choppy markets, RSI may frequently oscillate within overbought and oversold zones, while MACD might produce multiple crossovers, leading to overtrading and consecutive losses. A solution is to add supplementary trend filters such as moving averages or the ADX indicator.

2. **Parameter Sensitivity**: Strategy performance is sensitive to RSI and MACD parameter settings. The current traditional default parameters may not be suitable for all market environments. Parameter optimization based on specific trading instruments and market characteristics is recommended.

3. **Fixed Take-Profit and Stop-Loss Limitations**: Using fixed percentage-based take-profit and stop-loss levels may not adapt to different market volatility characteristics. High-volatility markets might trigger stop-losses too frequently, while low-volatility markets might struggle to reach take-profit targets.

4. **Lack of Trading Time Control**: The current strategy does not incorporate trading time filters, potentially generating unfavorable signals during periods of poor liquidity or abnormal volatility.

5. **No Position Reversal Mechanism**: Long and short signals in the strategy trigger independently, lacking an effective position reversal mechanism, which may lead to significant losses in counter-position holdings during strong trend markets.

#### Strategy Optimization Directions

1. **Dynamic Parameter Adjustment**: Consider dynamically adjusting RSI overbought/oversold thresholds and MACD parameters based on market volatility (such as the ATR indicator) to adapt to different market environments. Implementation example:
   
```
   atrValue = ta.atr(14)
   dynamicRsiOversold = 30 - (atrValue / close * 100)
   dynamicRsiOverbought = 70 + (atrValue / close * 100)
   
```

2. **Add Trend Filters**: Introduce additional trend confirmation indicators, such as adding the ADX indicator to execute trades only when ADX > 25 (indicating a significant market trend), avoiding frequent trading in oscillating markets:
   
```
   adxValue = ta.adx(14)
   adxFilter = adxValue > 25
   longCondition = (rsi < rsiOversold) and macdCrossUp and adxFilter
   
```

3. **Optimize Capital Management**: Instead of a fixed 100% equity ratio, adopt volatility-based position sizing where position size decreases as volatility increases:
   
```
   positionSize = 100 / (ta.atr(14) / close * 100)
   
```

4. **Implement Time Filtering**: Add trading time window controls to avoid market opening, closing, and low-liquidity periods:
   
```
   timeFilter = (time >= timestamp("00:30:00")) and (time <= timestamp("23:00:00"))
   
```

5. **Improve Take-Profit and Stop-Loss Mechanisms**: Adopt technically-based exit points such as previous highs/lows, support/resistance levels, or ATR multiples as dynamic stop points, rather than fixed percentages:
   
```
   atrValue = ta.atr(14)
   dynamicStopLoss = atrValue * 1.5
   
```

#### Summary

The RSI and MACD Cross-Period Dynamic Trading Strategy is a clearly structured, logically defined quantitative trading system that integrates the strengths of overbought/oversold indicators (RSI) and momentum trend indicators (MACD) to provide relatively reliable trading signals. This strategy is particularly suitable for short-term trading on 15-minute timeframes, with core advantages in its dual-indicator confirmation mechanism and explicit capital risk management rules.

While the strategy design is reasonable, challenges remain in parameter sensitivity and market adaptability. By introducing dynamic parameter adjustments, trend filters, optimized capital management, time filtering, and improved take-profit and stop-loss mechanisms, the strategy's robustness and adaptability can be further enhanced.

Any quantitative strategy requires comprehensive historical backtesting and forward validation, alongside customization to specific market conditions and trader risk preferences. This strategy provides an excellent quantitative trading framework upon which traders can build through secondary development and optimization to construct more refined trading systems.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-03-07 00:00:00
end: 2025-04-06 00:00:00
period: 15m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

// This Pine Script® code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ErayPala

//@version=6
strategy("RSI + MACD Strategy (15min)", overlay=false, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// === INPUTS ===
rsiLength = input.int(14, title="RSI Length")
rsiOverbought = input.int(70, title="RSI Overbought Level")
rsiOversold = input.int(30, title="RSI Oversold Level")

macdFast = input.int(12, title="MACD Fast Length")
macdSlow = input.int(26, title="MACD Slow Length")
macdSignal = input.int(9, title="MACD Signal Smoothing")

takeProfitPerc = input.float(5.0, title="Take Profit (%)") / 100
stopLossPerc = input.float(2.0, title="Stop Loss (%)") / 100

// === INDICATORS ===
rsi = ta.rsi(close, rsiLength)
[macdLine, signalLine, _] = ta.macd(close, macdFast, macdSlow, macdSignal)
macdCrossUp = ta.crossover(macdLine, signalLine)
macdCrossDown = ta.crossunder(macdLine, signalLine)

// === ENTRY CONDITIONS ===
longCondition = (rsi < rsiOversold) and macdCrossUp
shortCondition = (rsi > rsiOverbought) and macdCrossDown

// === STRATEGY ENTRIES ===
if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("TP/SL Long", from_entry="Long", limit=close * (1 + takeProfitPerc), stop=close * (1 - stopLossPerc))

if (shortCondition)
    strategy.entry("Short", strategy.short)
    strategy.exit("TP/SL Short", from_entry="Short", limit=close * (1 - takeProfitPerc), stop=close * (1 + stopLossPerc))

// === PLOT INDICATORS FOR VISUAL FEEDBACK ===
plot(rsi, title="RSI", color=color.orange)
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.green)
hline(50, "Middle Line", color=color.gray)
```

> Detail

https://www.fmz.com/strategy/489658

> Last Modified

2025-04-07 13:50:10
