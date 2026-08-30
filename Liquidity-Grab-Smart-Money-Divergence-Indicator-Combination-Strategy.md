
> Name

Liquidity-Grab-Smart-Money-Divergence-Indicator-Combination-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8be1d638362a5a887eb.png)
![IMG](https://www.fmz.com/upload/asset/2d839791650ec47c1fa0a.png)



[trans]

#### Overview
The strategy of combining liquidity capture and intelligent fund divergence indicators is a quantitative trading method based on technical analysis. By identifying liquidity capture events and intelligent fund divergence signals in the market, it combines trend confirmation and dynamic risk management systems to make trading decisions. The core idea of ​​this strategy is to capture the structural change points in the market, that is, the critical moments when large institutional investors (intelligent funds) may change direction after absorbing liquidity, thereby seizing high-probability entry opportunities.
#### Strategy Principle
The working mechanism of this strategy is based on multiple technical indicators and market structure analysis:
1. **Liquidity Capture Identification**: By monitoring whether the price sweeps past the recent high/low (defined by the lookback parameter) and subsequently reverses. Specifically, when the price hits a new high in the lookback cycle but the closing price is lower than the high point of the previous K line, it is determined to be liquidity capture at the high point; when the price hits a new low in the lookback cycle but the closing price is higher than the low point of the previous K line, it is determined to be liquidity capture at the low point.
2. **Smart Fund Divergence**: Compare the price trend with the RSI indicator to look for divergences. A bullish divergence forms when the price makes a new low but the RSI does not. A bearish divergence forms when the price makes a new high but the RSI does not. This divergence usually indicates that the market's internal momentum is inconsistent with price action, suggesting that a reversal may be imminent.
3. **Trend confirmation filter**: Use the 50-period simple moving average (SMA) as a trend judgment tool, and only execute transactions when the trend direction is consistent. When the price is above the SMA, it is considered to be in an uptrend, and only long positions are considered; when the price is below the SMA, it is considered to be in a downtrend, and only short positions are considered.
4. **Dynamic Risk Management**: Set dynamic stop loss and profit targets based on the ATR (Average True Range) indicator. The stop loss is set to 1.5 times the current ATR value, and the profit target is set to 2 times the stop loss distance (ie 3 times the ATR value).
The trading signal generation logic is:
- Long signal: Low liquidity capture identified + RSI bullish divergence confirmed + Price above SMA
- Short signal: High liquidity capture recognized + RSI bearish divergence confirmed + Price below SMA
#### Strategic Advantages
1. **High probability reversal point identification**: By combining liquidity capture and intelligent fund divergence, this strategy can more accurately capture market structural turning points and reduce the probability of false signals.
2. **Trend filtering mechanism**: Due to the addition of SMA trend confirmation, the strategy avoids counter-trend trading and only looks for entry opportunities in the direction of the main trend, improving the success rate of transactions.
3. **Adaptive risk management**: The dynamic stop-loss mechanism based on ATR enables risk control to automatically adjust according to market volatility and maintain appropriate risk exposure under different market environments.
4. **Optimized risk-return ratio**: The strategy adopts a risk-return setting of 1:2 (stop loss is 1.5 times ATR, profit target is 3 times ATR), and the mathematical expectation value is more advantageous.
5. **Multiple confirmation mechanism**: Trading signals need to meet multiple conditions (liquidity capture, divergence signals, trend confirmation), which reduces the possibility of false signals and enhances the robustness of transactions.
6. **Adapt to market cycle changes**: Since this strategy can be used for both long and short positions, it can adapt to different market cycles and environments and is not limited to markets in one direction.
#### Strategy Risk
1. **Over-optimization risk**: The strategy relies on multiple parameters (RSI length, lookback period, moving average period, ATR parameters, etc.), and there is the possibility of over-optimization (over-fitting), which may lead to good backtesting results but poor real-time performance.
2. **Signal lag**: Due to the use of indicators such as moving averages and RSI, some signals may lag, resulting in insufficient timely entry or missing the best entry point.
3. **Liquidity risk**: In a low-liquidity market environment, the concept of liquidity capture may not be obvious enough, resulting in a decline in signal quality.
4. **Risk of violent market fluctuations**: During periods of abnormal market fluctuations, ATR may suddenly increase, causing the stop loss position to be too far away and increasing the risk of a single transaction.
5. **Poor performance in volatile markets**: In sideways volatile markets with no obvious trend, this strategy may generate more false signals, leading to frequent stop losses.
6. **Parameter sensitivity**: Strategy performance is more sensitive to parameter selection, and different markets and time frames may require different parameter settings.
#### Strategy optimization direction
1. **Dynamic parameter adjustment**: You can consider introducing an adaptive parameter mechanism to dynamically adjust the RSI length, lookback period and MA period according to market volatility and trend intensity to adapt to different market environments.
2. **Add trading volume confirmation**: Adding trading volume analysis to liquidity capture and divergence judgment can improve signal quality. Liquidity capture on high volumes is generally more meaningful, indicating that more market participants are trapped.
3. **Multi-time frame analysis**: Introducing a multi-time frame confirmation mechanism, which only executes transactions when the trend direction of higher time frames is consistent, can further reduce the probability of false signals.
4. **Optimize the take-profit mechanism**: You can consider taking profits in batches or adopting a moving stop-loss strategy instead of a simple fixed-proportion take-profit to better capture trending market conditions.
5. **Add market environment filtering**: Introduce volatility indicators (such as ATR ratio or Bollinger bandwidth) to identify the market environment, adjust strategy parameters or suspend trading in high volatility or sideways markets.
6. **Machine learning enhancement**: Consider using machine learning methods to optimize parameter selection or signal quality assessment to improve the adaptability and robustness of the strategy.
7. **Add reverse thinking mechanism**: In extreme market conditions (such as RSI being severely overbought and oversold), you can consider adding reverse signal logic to avoid entering the market when the market is about to reverse.
#### Summarize
The strategy of combining liquidity capture with intelligent fund divergence indicators is a comprehensive trading system based on market microstructure and technical indicators. It captures high-probability trading opportunities by identifying traces of large fund operations and changes in intrinsic momentum. This strategy combines price action analysis, technical indicator divergence and trend confirmation, supplemented by dynamic risk management, to form a relatively complete trading framework.
The biggest advantage of this strategy is its ability to capture market structural change points, that is, critical moments when large institutions may change direction after completing liquidity collection. Through the multiple confirmation mechanism and trend filtering, the strategy reduces the probability of false signals and improves transaction quality. However, strategies also face challenges such as parameter optimization, false signals, and market adaptability.
In order to further enhance the strategy performance, you can consider introducing dynamic parameter adjustment, multi-time frame analysis, trading volume confirmation and optimization of the profit-taking mechanism and other improvement measures. Overall, this strategy provides an effective framework for capturing market turning points, and through sound risk management and continuous optimization, has the potential to become a robust trading system. ||
#### Overview

The Liquidity Grab & Smart Money Divergence Indicator Combination Strategy is a quantitative trading approach based on technical analysis that identifies liquidity grab events and smart money divergence signals in the market, combined with trend confirmation and dynamic risk management systems for trading decisions. The core idea of this strategy is to capture structural market turning points—key moments when large institutional investors (smart money) may change direction after absorbing liquidity, thereby seizing high-probability entry opportunities.

#### Strategy Principles

The strategy operates based on multiple technical indicators and market structure analysis:

1. **Liquidity Grab Identification**: Monitors whether price sweeps recent highs/lows (defined by the lookback parameter) followed by a reversal. Specifically, when price makes a new high within the lookback period but closes below the previous candle's high, it's identified as a high liquidity grab; when price makes a new low but closes above the previous candle's low, it's identified as a low liquidity grab.

2. **Smart Money Divergence**: Compares price movement with the RSI indicator to look for divergence patterns. When price makes a new low but RSI doesn't make a new low, a bullish divergence forms; when price makes a new high but RSI doesn't make a new high, a bearish divergence forms. This divergence typically indicates that the market's internal momentum doesn't align with price movement, suggesting a potential reversal.

3. **Trend Confirmation Filter**: Uses a 50-period Simple Moving Average (SMA) as a trend determination tool, executing trades only when aligned with the trend direction. When price is above the SMA, it's considered an uptrend and only long positions are considered; when price is below the SMA, it's considered a downtrend and only short positions are considered.

4. **Dynamic Risk Management**: Sets dynamic stop-loss and profit targets based on the ATR (Average True Range) indicator. Stop-loss is set at 1.5 times the current ATR value, and the profit target is set at twice the stop-loss distance (i.e., 3 times the ATR value).

The trade signal generation logic is:
- Long signal: Low liquidity grab identified + RSI bullish divergence confirmed + Price above SMA
- Short signal: High liquidity grab identified + RSI bearish divergence confirmed + Price below SMA

#### Strategy Advantages

1. **High-Probability Reversal Point Identification**: By combining liquidity grabs and smart money divergence, the strategy can more accurately capture structural market turning points, reducing the probability of false signals.

2. **Trend Filtering Mechanism**: With SMA trend confirmation added, the strategy avoids counter-trend trading and only seeks entry opportunities in the direction of the main trend, improving the success rate of trades.

3. **Adaptive Risk Management**: The ATR-based dynamic stop-loss mechanism allows risk control to adjust automatically according to market volatility, maintaining appropriate risk exposure in different market environments.

4. **Optimized Risk-Reward Ratio**: The strategy employs a 1:2 risk-reward setting (stop-loss at 1.5x ATR, profit target at 3x ATR), providing a more advantageous mathematical expectation.

5. **Multiple Confirmation Mechanism**: Trade signals must meet multiple conditions (liquidity grab, divergence signal, trend confirmation), reducing the possibility of erroneous signals and enhancing trading robustness.

6. **Adaptation to Market Cycle Changes**: Since the strategy can both go long and short, it can adapt to different market cycles and environments, not limited to a single market direction.

#### Strategy Risks

1. **Over-Optimization Risk**: The strategy relies on multiple parameters (RSI length, lookback period, moving average period, ATR parameters, etc.), creating the possibility of over-optimization (overfitting), which may lead to good backtest results but poor live trading performance.

2. **Signal Lag**: Due to the use of moving averages and RSI indicators, some signals may appear with a lag, resulting in untimely entries or missed optimal entry points.

3. **Insufficient Liquidity Risk**: In low-liquidity market environments, the concept of liquidity grabs may not be as evident, leading to decreased signal quality.

4. **Extreme Market Volatility Risk**: During periods of abnormal market volatility, ATR may suddenly expand, causing stop-loss positions to be placed too far away and increasing single-trade risk.

5. **Poor Performance in Ranging Markets**: In sideways, ranging markets with no clear trend, the strategy may produce more false signals, resulting in frequent stop-losses.

6. **Parameter Sensitivity**: Strategy performance is relatively sensitive to parameter selection, and different markets and timeframes may require different parameter settings.

#### Strategy Optimization Directions

1. **Dynamic Parameter Adjustment**: Consider introducing an adaptive parameter mechanism that dynamically adjusts RSI length, lookback period, and MA period based on market volatility and trend strength to adapt to different market environments.

2. **Volume Confirmation Addition**: Incorporate volume analysis in liquidity grab and divergence judgment to improve signal quality. High-volume liquidity grabs typically hold more significance, indicating more market participants being trapped.

3. **Multiple Timeframe Analysis**: Introduce a multiple timeframe confirmation mechanism, executing trades only when aligned with higher timeframe trend direction, which can further reduce the probability of false signals.

4. **Profit-Taking Mechanism Optimization**: Consider implementing partial profit-taking or trailing stop-loss strategies instead of simple fixed-ratio profit-taking to better capture trending market movements.

5. **Market Environment Filtering**: Introduce volatility indicators (such as ATR ratio or Bollinger Bandwidth) to identify market environments and adjust strategy parameters or pause trading during high volatility or sideways ranging markets.

6. **Machine Learning Enhancement**: Consider using machine learning methods to optimize parameter selection or signal quality assessment, improving strategy adaptability and robustness.

7. **Counter-Logic Mechanism**: In extreme market conditions (such as severe RSI overbought/oversold), consider adding reverse signal logic to avoid entering positions when the market is about to reverse.

#### Summary

The Liquidity Grab & Smart Money Divergence Indicator Combination Strategy is a comprehensive trading system based on market microstructure and technical indicators, capturing high-probability trading opportunities by identifying traces of large capital operations and internal momentum changes. This strategy combines price action analysis, technical indicator divergence, and trend confirmation, supplemented by dynamic risk management, forming a relatively complete trading framework.

The strategy's greatest advantage lies in its ability to capture structural market turning points—critical moments when large institutions may change direction after completing liquidity collection. Through multiple confirmation mechanisms and trend filtering, the strategy reduces the probability of erroneous signals and improves trading quality. However, the strategy also faces challenges related to parameter optimization, false signals, and market adaptability.

To further enhance strategy performance, consider introducing dynamic parameter adjustment, multiple timeframe analysis, volume confirmation, and optimized profit-taking mechanisms. Overall, this strategy provides an effective framework for capturing market turning points and, with proper risk management and continuous optimization, has the potential to become a robust trading system.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-25 00:00:00
end: 2025-03-24 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Liquidity Grab + Smart Money Divergence Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=1)

// Input settings
length = input(14, "RSI Length")
lookback = input(5, "Lookback Bars")
src = close
maLength = input(50, "MA Length")
atrLength = input(14, "ATR Length")
atrMultiplier = input(1.5, "ATR Multiplier")

// RSI Calculation
rsiValue = ta.rsi(src, length)

// Moving Average Trend Filter
ma = ta.sma(close, maLength)
trendUp = close > ma
trendDown = close < ma

// ATR for dynamic stop-loss and take-profit
atr = ta.atr(atrLength)
sl = atr * atrMultiplier

// Detect liquidity grab (sweep of recent high/low)
sweepHigh = ta.highest(high, lookback) == high and close < high[1]
sweepLow = ta.lowest(low, lookback) == low and close > low[1]

// Detect Smart Money Divergence
bullishDivergence = sweepLow and (rsiValue > ta.lowest(rsiValue, lookback))
bearishDivergence = sweepHigh and (rsiValue < ta.highest(rsiValue, lookback))

// Trade signals with trend confirmation
buySignal = bullishDivergence and trendUp
sellSignal = bearishDivergence and trendDown

// Execute trades with stop-loss and take-profit
if buySignal
    strategy.entry("Buy", strategy.long)
    strategy.exit("Sell", from_entry="Buy", stop=close - sl, limit=close + sl * 2)
if sellSignal
    strategy.entry("Sell", strategy.short)
    strategy.exit("Buy", from_entry="Sell", stop=close + sl, limit=close - sl * 2)

// Plot signals on chart
plotshape(buySignal, location=location.belowbar, color=color.green, style=shape.labelup, size=size.small, title="Buy Signal")
plotshape(sellSignal, location=location.abovebar, color=color.red, style=shape.labeldown, size=size.small, title="Sell Signal")
plot(ma, title="50 MA", color=color.blue)

```

> Detail

https://www.fmz.com/strategy/488156

> Last Modified

2025-03-25 15:12:43
