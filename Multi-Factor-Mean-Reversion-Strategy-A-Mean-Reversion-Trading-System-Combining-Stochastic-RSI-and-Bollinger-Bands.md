
> Name

Multi-Factor-Mean-Reversion-Strategy-A-Mean-Reversion-Trading-System-Combining-Stochastic-RSI-and-Bollinger-Bands
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/77d3049c3f4285dba4b9582cf039f73b6a331203172ab5235efab07835508402.png)
![IMG](assets/images/c50d29e63bc36f805cfddd77b5883cdd4ddfe175dfb007da48250307fb567f55.png)

[trans]

#### Overview
This strategy is a multi-factor mean reversion trading system that combines the Stochastic RSI and Bollinger Bands. It operates on the 5-minute time frame and is mainly used to capture price return opportunities when the market is overbought and oversold. The core idea of ​​the strategy is: buy when the price is at the lower edge of the Bollinger Bands and the stochastic RSI is lower than the oversold area of ​​0.1, and sell when the price is at the upper edge of the Bollinger Bands and the stochastic RSI is higher than the overbought area of ​​0.9. This multi-factor combination effectively enhances the reliability of trading signals and filters out false signals that a single indicator may bring.
#### Strategy Principle
This strategy is based on a combination of two technical indicators:
1. **Stochastic RSI**:
   - First calculate the basic RSI value: `rsi = ta.rsi(request.security(syminfo.tickerid, "5", close), length)`
   - Then calculate the stochastic indicator based on RSI: `k = ta.sma(ta.stoch(rsi, rsi, rsi, length), smoothK)`
   - Then calculate the smoothed moving average of K value: `d = ta.sma(k, smoothD)`
   - Finally, take the average of the K line and the D line as the stochastic RSI indicator: `stochRSI = (k + d) / 2`
2. **Bollinger Bands**:
   - Basis: 20-period simple moving average: `basis = ta.sma(request.security(syminfo.tickerid, "5", close), bbLength)`
   - Standard deviation: `dev = bbStdDev * ta.stdev(request.security(syminfo.tickerid, "5", close), bbLength)`
   - Upper track: middle track plus 2 times the standard deviation: `upperBand = basis + dev`
   - Lower track: middle track minus 2 times the standard deviation: `lowerBand = basis - dev`
Transaction logic:
- Buying conditions: `stochRSI < 0.1 and close <= lowerBand` (Stochastic RSI is below 0.1 and the price touches or breaks through the lower Bollinger Band)
- Sell condition: `stochRSI > 0.9 and close >= upperBand` (Stochastic RSI is above 0.9 and the price touches or breaks the upper Bollinger Band)
Appearance logic:
- Long closing: Stochastic RSI rises above 0.2: `exitBuyCondition = stochRSI > 0.2`
- Short closing: Stochastic RSI drops below 0.8: `exitSellCondition = stochRSI < 0.8`
The strategy also sets the entry price, stop loss and take profit parameters, but in the code the stop loss values ​​are set to 0 and 1 respectively, and the take profit values ​​are set to 0.8 and 0.2 respectively. These parameters need to be optimized based on the actual trading assets.
#### Strategic Advantages
1. **Multi-factor collaborative confirmation**: By combining the two technical indicators of stochastic RSI and Bollinger Bands, the strategy can more accurately identify overbought and oversold areas, reduce false signals, and improve trading efficiency.
2. **Mean Reversion Concept**: The strategy is based on the theoretical basis that market prices tend to return to the mean. This concept has been verified in many financial markets, and is especially suitable for volatile sideways markets.
3. **Quantitative entry and exit criteria**: The strategy provides clear entry and exit conditions, reducing subjective judgment and helping traders maintain discipline.
4. **Strong adaptability**: Various parameters in the strategy (such as RSI length, Bollinger Band standard deviation multiple, etc.) can be adjusted by inputting parameters, so that the strategy can adapt to different market environments and trading varieties.
5. **Visual support**: The strategy code contains indicator visualization part, which facilitates traders to monitor and analyze.
6. **5-minute time frame**: The strategy is based on the 5-minute time frame, which can capture short-term trading opportunities and is suitable for day traders.
#### Strategy Risk
1. **Risk in trending market**: In a strong trending market, the mean reversion strategy may frequently produce false signals, leading to continuous losses. The solution is to add a trend filter that only enables the strategy when the market is sideways.
2. **False Breakout Risk**: The price may temporarily break through the Bollinger Bands and then return, resulting in a false signal. The solution is to add a confirmation mechanism, such as requiring the price to maintain a certain time or range after breaking through the Bollinger Bands.
3. **Unreasonable stop loss settings**: The stop loss settings (0 and 1) in the current code may not be applicable to actual transactions. The solution is to set a reasonable stop loss ratio based on the volatility characteristics of the trading variety.
4. **Excessive parameter optimization**: Over-optimizing parameters may cause the strategy to perform well on historical data but fail in future real trading. The solution is to use the rolling window method for parameter optimization to avoid overfitting.
5. **Lack of market environment adaptability**: Different market environments (such as high volatility and low volatility) may require different parameter settings. The solution is to establish a volatility adaptive mechanism to dynamically adjust parameters according to market conditions.
6. **Influence of slippage and transaction costs**: High-frequency trading strategies are greatly affected by slippage and transaction costs. The solution is to fully consider these factors in backtesting and real trading, and may need to increase the signal threshold to reduce the number of transactions.
#### Strategy optimization direction
1. **Add trend filter**: Trend indicators such as ADX (Average Directional Index) can be introduced. When the ADX value is higher than a certain threshold (such as 25), it indicates that the market is in a strong trend. At this time, the mean reversion strategy can be suspended or the parameters can be adjusted.
2. **Optimize stop loss mechanism**: The stop loss setting of the current strategy is not perfect enough. You can consider using ATR (average true volatility) to set dynamic stop loss, for example: `stopLoss = entryPrice - (atrValue * 1.5)` (long) or `stopLoss = entryPrice + (atrValue * 1.5)` (short).
3. **Increase trading volume confirmation**: When the entry signal is triggered, trading volume confirmation conditions can be added, such as requiring the current trading volume to be higher than the average trading volume of the previous N periods, to ensure that there is sufficient market liquidity to support price reversal.
4. **Time filter**: Some markets have large and irregular fluctuations in specific time periods (such as before and after opening and closing). You can add a time filter to avoid these periods.
5. **Introduction of machine learning optimization**: Machine learning algorithms (such as random forest or neural network) can be used to optimize the weight or parameters of each indicator so that the strategy can better adapt to different market environments.
6. **Add backtest robustness testing**: Implement Monte Carlo simulation or step-by-step backtesting to evaluate the robustness of the strategy under different market conditions.
7. **Dynamic Parameter Adjustment**: Automatically adjust the standard deviation multiple of Bollinger Bands according to market volatility, using higher multiples in high volatility environments and lower multiples in low volatility environments.
#### Summarize
"Multi-factor mean reversion strategy: Mean reversion trading system combining stochastic relative strength indicator and Bollinger Bands" is a trading strategy based on technical analysis, which combines stochastic RSI and Bollinger Band indicators to identify overbought and oversold conditions in the market and capture trading opportunities when prices return to the mean. The core advantage of this strategy lies in the multi-factor confirmation mechanism and clear quantitative trading rules. However, in practical applications, we still need to pay attention to issues such as risks in trending markets and excessive parameter optimization.
By adding trend filters, optimizing stop-loss mechanisms, introducing trading volume confirmation and implementing dynamic parameter adjustments, this strategy has the potential to achieve more stable performance in various market environments. For traders pursuing mean reversion trading opportunities, this strategy provides a systematic framework, but successful application still requires traders to make personalized adjustments based on their own experience and risk management capabilities. ||
#### Overview

This strategy is a multi-factor mean reversion trading system that combines the Stochastic Relative Strength Index (Stochastic RSI) and Bollinger Bands. It operates on a 5-minute timeframe, primarily designed to capture price reversion opportunities during market overbought and oversold conditions. The core concept of the strategy is to buy when the price is at the lower Bollinger Band and the Stochastic RSI is below 0.1 (oversold region), and to sell when the price is at the upper Bollinger Band and the Stochastic RSI is above 0.9 (overbought region). This multi-factor combination effectively enhances the reliability of trading signals, filtering out potential false signals that might arise from using a single indicator.

#### Strategy Principles

The strategy is based on the combination of two technical indicators:

1. **Stochastic Relative Strength Index (Stochastic RSI)**:
   - First, calculate the basic RSI value: `rsi = ta.rsi(request.security(syminfo.tickerid, "5", close), length)`
   - Then calculate the stochastic based on RSI: `k = ta.sma(ta.stoch(rsi, rsi, rsi, length), smoothK)`
   - Next, calculate the smoothed moving average of K: `d = ta.sma(k, smoothD)`
   - Finally, take the average of K and D lines as the Stochastic RSI: `stochRSI = (k + d) / 2`

2. **Bollinger Bands**:
   - Middle Band (Basis): 20-period simple moving average: `basis = ta.sma(request.security(syminfo.tickerid, "5", close), bbLength)`
   - Standard Deviation: `dev = bbStdDev * ta.stdev(request.security(syminfo.tickerid, "5", close), bbLength)`
   - Upper Band: Middle Band plus 2 times standard deviation: `upperBand = basis + dev`
   - Lower Band: Middle Band minus 2 times standard deviation: `lowerBand = basis - dev`

Trading Logic:
- Buy Condition: `stochRSI < 0.1 and close <= lowerBand` (Stochastic RSI below 0.1 and price touching or breaking through the lower Bollinger Band)
- Sell Condition: `stochRSI > 0.9 and close >= upperBand` (Stochastic RSI above 0.9 and price touching or breaking through the upper Bollinger Band)

Exit Logic:
- Long Position Close: Stochastic RSI rises above 0.2: `exitBuyCondition = stochRSI > 0.2`
- Short Position Close: Stochastic RSI falls below 0.8: `exitSellCondition = stochRSI < 0.8`

The strategy also sets entry price, stop loss, and take profit parameters, but in the code, the stop loss values are set to 0 and 1, and take profit values are set to 0.8 and 0.2 respectively. These parameters need to be optimized based on the actual trading asset.

#### Strategy Advantages

1. **Multi-Factor Collaborative Confirmation**: By combining Stochastic RSI and Bollinger Bands, the strategy can more accurately identify overbought and oversold areas, reducing false signals and improving trading efficiency.

2. **Mean Reversion Concept**: The strategy is based on the theoretical foundation that market prices tend to revert to the mean, a concept that has been validated in many financial markets and is particularly suitable for ranging markets with oscillations.

3. **Quantified Entry and Exit Criteria**: The strategy provides clear entry and exit conditions, reducing subjective judgment and helping traders maintain discipline.

4. **High Adaptability**: The various parameters in the strategy (such as RSI length, Bollinger Bands standard deviation multiplier, etc.) can be adjusted through input parameters, allowing the strategy to adapt to different market environments and trading instruments.

5. **Visual Support**: The strategy code includes indicator visualization components, making it convenient for traders to monitor and analyze.

6. **5-Minute Timeframe**: The strategy is based on a 5-minute timeframe, capable of capturing short-term trading opportunities, making it suitable for intraday traders.

#### Strategy Risks

1. **Risks in Trending Markets**: In strong trending markets, mean reversion strategies may frequently generate false signals, leading to consecutive losses. The solution is to add a trend filter, enabling the strategy only when the market is ranging.

2. **False Breakout Risk**: Prices may temporarily break through the Bollinger Bands before reverting, causing erroneous signals. The solution is to add confirmation mechanisms, such as requiring the price to maintain a certain duration or magnitude after breaking through the Bollinger Bands.

3. **Unreasonable Stop Loss Settings**: The current stop loss settings in the code (0 and 1) may not be applicable to actual trading. The solution is to set reasonable stop loss percentages based on the volatility characteristics of the trading instrument.

4. **Over-Optimization of Parameters**: Excessive parameter optimization may cause the strategy to perform well on historical data but fail in future live trading. The solution is to use a rolling window method for parameter optimization to avoid overfitting.

5. **Lack of Market Environment Adaptability**: Different market environments (such as high volatility vs. low volatility) may require different parameter settings. The solution is to establish a volatility adaptive mechanism to dynamically adjust parameters based on market conditions.

6. **Impact of Slippage and Trading Costs**: High-frequency trading strategies are significantly affected by slippage and trading costs. The solution is to fully consider these factors in backtesting and live trading, and possibly raise signal thresholds to reduce the number of trades.

#### Strategy Optimization Directions

1. **Add Trend Filters**: Introduce trend indicators such as ADX (Average Directional Index). When the ADX value is above a specific threshold (e.g., 25), indicating that the market is in a strong trend, the mean reversion strategy can be paused or parameters adjusted.

2. **Optimize Stop Loss Mechanism**: The current stop loss settings in the strategy are not fully developed. Consider using ATR (Average True Range) to set dynamic stop losses, for example: `stopLoss = entryPrice - (atrValue * 1.5)` (for long positions) or `stopLoss = entryPrice + (atrValue * 1.5)` (for short positions).

3. **Add Volume Confirmation**: When entry signals are triggered, add volume confirmation conditions, such as requiring the current trading volume to be higher than the average trading volume of the previous N periods, to ensure sufficient market liquidity to support price reversal.

4. **Time Filter**: Some markets experience high and irregular volatility during specific time periods (such as around market open and close). Adding a time filter can help avoid these periods.

5. **Introduce Machine Learning Optimization**: Use machine learning algorithms (such as random forests or neural networks) to optimize the weights or parameters of various indicators, enabling the strategy to better adapt to different market environments.

6. **Enhance Backtest Robustness Testing**: Implement Monte Carlo simulations or walk-forward testing to evaluate the robustness of the strategy under different market conditions.

7. **Dynamic Parameter Adjustment**: Automatically adjust the standard deviation multiplier of Bollinger Bands based on market volatility, using higher multipliers in high-volatility environments and lower multipliers in low-volatility environments.

#### Summary

The "Multi-Factor Mean Reversion Strategy: A Mean Reversion Trading System Combining Stochastic RSI and Bollinger Bands" is a trading strategy based on technical analysis. It identifies market overbought and oversold conditions by combining Stochastic RSI and Bollinger Bands indicators to capture trading opportunities when prices revert to the mean. The core advantage of this strategy lies in its multi-factor confirmation mechanism and clear quantified trading rules. However, in practical application, attention still needs to be paid to risks in trending markets and issues such as parameter over-optimization.

By adding trend filters, optimizing stop loss mechanisms, introducing volume confirmation, and implementing dynamic parameter adjustments, this strategy has the potential to achieve more stable performance in various market environments. For traders pursuing mean reversion trading opportunities, this strategy provides a systematic framework, but successful application still requires traders to make personalized adjustments based on their own experience and risk management capabilities.[/trans]




> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-09 00:00:00
end: 2025-04-08 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Stochastic RSI & Bollinger Bands Backtest (5 Min)", overlay=true)

// Input parameters
length = input.int(14, title="Stochastic RSI Length")
smoothK = input.int(3, title="Stochastic RSI %K")
smoothD = input.int(3, title="Stochastic RSI %D")
bbLength = input.int(20, title="Bollinger Bands Length")
bbStdDev = input.float(2.0, title="Bollinger Bands StdDev")

// Calculate Stochastic RSI on 5-minute timeframe
rsi = ta.rsi(request.security(syminfo.tickerid, "5", close), length)
k = ta.sma(ta.stoch(rsi, rsi, rsi, length), smoothK)
d = ta.sma(k, smoothD)
stochRSI = (k + d) / 2

// Calculate Bollinger Bands on 5-minute timeframe
basis = ta.sma(request.security(syminfo.tickerid, "5", close), bbLength)
dev = bbStdDev * ta.stdev(request.security(syminfo.tickerid, "5", close), bbLength)
upperBand = basis + dev
lowerBand = basis - dev

// Buy conditions
buyCondition = stochRSI < 0.1 and close <= lowerBand
sellCondition = stochRSI > 0.9 and close >= upperBand

// Plot Bollinger Bands
plot(upperBand, color=color.red, title="Upper Band")
plot(lowerBand, color=color.green, title="Lower Band")
plot(basis, color=color.blue, title="Basis")

// Plot Stochastic RSI
hline(0.1, "Oversold", color=color.green)
hline(0.9, "Overbought", color=color.red)
plot(stochRSI, color=color.orange, title="Stochastic RSI")

// Backtest logic
var float entryPrice = na
var float stopLoss = na
var float takeProfit = na

if (buyCondition and strategy.position_size == 0)
    entryPrice := close
    stopLoss := 0
    takeProfit := 0.8
    strategy.entry("Buy", strategy.long)

if (sellCondition and strategy.position_size == 0)
    entryPrice := close
    stopLoss := 1
    takeProfit := 0.2
    strategy.entry("Sell", strategy.short)

// Exit conditions
exitBuyCondition = stochRSI > 0.2
exitSellCondition = stochRSI < 0.8

if (exitBuyCondition and strategy.position_size > 0)
    strategy.close("Buy", when=exitBuyCondition)

if (exitSellCondition and strategy.position_size < 0)
    strategy.close("Sell", when=exitSellCondition)
```

> Detail

https://www.fmz.com/strategy/489893

> Last Modified

2025-04-09 17:05:23
