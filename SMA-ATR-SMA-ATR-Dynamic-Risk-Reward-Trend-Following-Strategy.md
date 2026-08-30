
> Name

SMA-ATR Dynamic Risk-Reward Ratio Trend Following Strategy-SMA-ATR-Dynamic-Risk-Reward-Trend-Following-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8400f5418a52a57bb7b.png)
![IMG](https://www.fmz.com/upload/asset/2d8cabb1eab6f0ec2ae59.png)



[trans]
#### Overview
The SMA-ATR Dynamic Risk-Reward Trend Following Strategy is a technical analysis-driven quantitative trading system that cleverly combines the Triple Simple Moving Average (SMA) and True Range (ATR) indicators to identify market trends and execute trades. The core feature of this strategy is to use a dynamic risk-reward ratio to automatically adjust the take-profit level according to specific market conditions, thereby optimizing trading performance in different market environments. The strategy uses 7, 25 and 99 period SMA cross signals to determine entry points, and uses the ATR indicator to set stop loss and take profit positions to form a complete trend following trading system.
#### Strategy Principle
The strategy works based on a multi-period moving average crossover system combined with dynamic risk management:
1. **Trend identification mechanism**:
   - Build a multi-level trend confirmation system using triple SMA (7, 25 and 99 periods)
   - A long signal is triggered when the short-term SMA (7 periods) crosses the medium-term SMA (25 periods) and the price is above the long-term SMA (99 periods)
   - A short signal is triggered when the short-term SMA (7 periods) crosses below the medium-term SMA (25 periods) and the price is below the long-term SMA (99 periods)
2. **Dynamic risk-reward ratio adjustment**:
   - The default risk-reward ratio is 2.0x
   - Under certain conditions (short-term SMA crosses with long-term SMA or medium-term SMA), the risk-reward ratio automatically increases to 6.0x
   - This adjustment allows the strategy to pursue higher profit targets when strong trend signals occur
3. **ATR-based risk management**:
   - Calculate volatility using 14-period ATR multiplied by custom multiplier (default 1.0)
   - Long stop loss is set at the low minus the ATR value
   - Short stop loss is set at the high plus the ATR value
   - Take profit level is calculated based on current price plus or minus (ATR times risk to reward ratio)
The core logic of the strategy is to confirm the trend direction through the multi-period moving average, while dynamically adjusting the risk-return rate according to market conditions, pursuing higher returns in a strong trend environment, and achieving intelligent risk management.
#### Strategic Advantages
1. **Multi-level trend confirmation**:
   - Triple SMA system provides multi-level trend confirmation to reduce false breakout trades
   - The combination of short-term, medium-term and long-term SMA effectively filters out market noise
   - Price's position relative to the long-term SMA provides additional trend confirmation, enhancing signal reliability
2. **Dynamic Risk Management**:
   - The risk-reward ratio is automatically adjusted according to signal strength to optimize fund management
   - Pursue higher returns when there are strong signals (such as short-term SMA crossing with long-term SMA)
   - Flexible risk management framework adapts to different market conditions
3. **Stop loss strategy based on market volatility**:
   - The ATR indicator ensures that stop loss levels are set based on actual market volatility
   - Adaptive stop-loss mechanism that automatically expands the stop-loss range when volatility increases and narrows the stop-loss range when volatility decreases
   - The stop-loss design takes into account the natural fluctuations of prices and reduces the probability of being triggered by market noise.
4. **Complete trading system**:
   - The strategy contains clear entry, exit and risk management rules to form a complete trading system
   - Automate execution to reduce emotional interference
   - Adaptive parameter adjustments suitable for different market conditions
#### Strategy Risk
1. **Trend reversal risk**:
   - As a trend following strategy, it may not perform well when the market is sideways or reversing quickly.
   - Triple SMA system may produce frequent false signals in volatile markets
   - Mitigation method: Additional filters (such as volatility indicators or momentum confirmations) can be added to reduce the frequency of trades in volatile markets
2. **Limitations of Fixed ATR Multiplier**:
   - The current strategy uses a fixed ATR multiplier (1.0) and may not be suitable for all market environments
   - Fixed multipliers can cause stops to be too wide or too narrow during periods of extreme volatility
   - Solution: Consider implementing an adaptive ATR multiplier and dynamically adjust it based on historical volatility statistics
3. **Parameter sensitivity**:
   - The choice of SMA period (7, 25, 99) may have a significant impact on strategy performance
   - Over-optimization risk - a specific combination of parameters may only perform well under specific market conditions
   -Risk Mitigation: Conduct robustness testing to evaluate the impact of small changes in parameters on strategy performance
4. **Slippage and Liquidity Risk**:
   - In illiquid markets or periods of high volatility, you may face execution slippage issues
   - ATR-based Stop Loss and Take Profit may not be sufficient to protect capital during extreme market conditions
   - Workaround: Increase margin requirements, reduce position size, or suspend trading if volatility is unusually high
#### Strategy optimization direction
1. **Add filtering signal mechanism**:
   - Add trend strength indicators (such as ADX) and only trade when the confirmed trend strength reaches the threshold
   - Integrate trading volume confirmation, requiring trading volume to increase when a signal appears, improving signal quality
   - Principle: Multi-indicator confirmation can significantly reduce false signals and improve the winning rate
2. **Implement adaptive parameters**:
   - Change the fixed SMA period to dynamic parameters that automatically adjust based on market volatility or periodicity
   - Adjust the ATR multiplier based on historical volatility statistics, using smaller multipliers during periods of low volatility and larger multipliers during periods of high volatility
   - Benefits: Adaptive parameters can better adapt to different market environments and improve strategy robustness
3. **Optimize the dynamic risk-return adjustment mechanism**:
   - Change the current binary risk-reward mechanism (2.0 or 6.0) to a continuously adjusted model
   - Dynamically adjust the risk-reward ratio based on trend strength indicators (such as ADX), market volatility or recent trading performance
   - Reasons for improvement: More detailed risk-return adjustments can more accurately reflect market conditions and optimize fund management effects.
4. **Add time filter**:
   - Analyze strategy performance in different time periods (intraday, intra-day, and inter-week) to avoid trading during periods of poor performance
   - Consider market seasonal factors and adjust trading frequency in specific market environments
   - Advantages: Time filtering can avoid trading during statistically unfavorable periods, improving overall performance
5. **Integrated machine learning model**:
   - Use machine learning algorithms to predict the reliability of SMA crossover signals
   - Train models based on historical data to identify market patterns with high probability of profit
   - Value: Machine learning can discover complex patterns that are difficult to capture with traditional technical indicators and improve strategy prediction capabilities.
#### Summarize
The SMA-ATR dynamic risk-to-reward ratio trend following strategy provides a well-structured trend following trading system that identifies market trends through multi-period moving averages and combines with the ATR indicator to achieve dynamic risk management. The most significant innovation of the strategy is that the risk-reward ratio is automatically adjusted according to specific market conditions, allowing the trading system to pursue higher returns in a strong trend environment while maintaining robust risk control in regular transactions.
This strategy combines the classic elements of technical analysis (SMA crossover, ATR stop loss) with modern quantitative trading concepts (dynamic risk management), and is suitable for medium and long-term trend following transactions. While the strategy may face challenges in volatile markets, its performance in different market environments can be further improved through suggested optimization directions such as adding filters, adaptive parameters, and machine learning integration.
Overall, this is a quantitative trading strategy that balances simplicity and effectiveness, providing a solid framework for trend following traders, while enhancing the strategy's adaptability and profit potential with dynamic risk management elements.
||
#### Overview
The SMA-ATR Dynamic Risk-Reward Trend Following Strategy is a technical analysis-driven quantitative trading system that cleverly combines triple Simple Moving Averages (SMA) and Average True Range (ATR) indicators to identify market trends and execute trades. The core feature of this strategy is its dynamic risk-reward ratio, which automatically adjusts profit targets based on specific market conditions, thereby optimizing trading performance across different market environments. The strategy uses SMA crossovers with periods of 7, 25, and 99 to determine entry points, and utilizes the ATR indicator to set stop-loss and take-profit levels, forming a complete trend-following trading system.

#### Strategy Principles

The strategy operates based on a combination of multi-period moving average crossover systems and dynamic risk management:

1. **Trend Identification Mechanism**:
   - Uses triple SMAs (7, 25, and 99 periods) to establish a multi-layered trend confirmation system
   - Triggers a long signal when the short-term SMA (7-period) crosses above the medium-term SMA (25-period) and price is above the long-term SMA (99-period)
   - Triggers a short signal when the short-term SMA (7-period) crosses below the medium-term SMA (25-period) and price is below the long-term SMA (99-period)

2. **Dynamic Risk-Reward Ratio Adjustment**:
   - Default risk-reward ratio is 2.0
   - Under specific conditions (when short-term SMA crosses the long-term SMA or medium-term SMA), the risk-reward ratio automatically increases to 6.0
   - This adjustment allows the strategy to pursue higher profit targets when strong trend signals appear

3. **ATR-Based Risk Management**:
   - Uses 14-period ATR multiplied by a custom multiplier (default 1.0) to calculate volatility
   - Long stop-loss is set at the low minus the ATR value
   - Short stop-loss is set at the high plus the ATR value
   - Take-profit levels are calculated based on current price plus or minus (ATR multiplied by the risk-reward ratio)

The core logic of the strategy is to confirm trend direction through multi-period moving averages while dynamically adjusting the risk-reward ratio based on market conditions, pursuing higher returns in strong trending environments and implementing intelligent risk management.

#### Strategy Advantages

1. **Multi-Layered Trend Confirmation**:
   - Triple SMA system provides multi-layered trend confirmation, reducing false breakout trades
   - The combination of short, medium, and long-term SMAs effectively filters market noise
   - Price position relative to the long-term SMA provides additional trend confirmation, enhancing signal reliability

2. **Dynamic Risk Management**:
   - Risk-reward ratio automatically adjusts based on signal strength, optimizing capital management
   - Pursues higher returns when strong signals (such as short-term SMA crossing long-term SMA) occur
   - Flexible risk management framework adapts to different market conditions

3. **Volatility-Based Stop-Loss Strategy**:
   - ATR indicator ensures stop-loss levels are set based on actual market volatility
   - Adaptive stop-loss mechanism automatically widens stop-loss range when volatility increases and narrows it when volatility decreases
   - Stop-loss design considers natural price fluctuations, reducing the probability of being triggered by market noise

4. **Complete Trading System**:
   - Strategy includes clear entry, exit, and risk management rules, forming a complete trading system
   - Automated execution reduces emotional interference
   - Adaptive parameter adjustments suitable for different market conditions

#### Strategy Risks

1. **Trend Reversal Risk**:
   - As a trend-following strategy, it may perform poorly in ranging markets or during rapid reversals
   - The triple SMA system may generate frequent false signals in oscillating markets
   - Mitigation method: Additional filters (such as volatility indicators or momentum confirmation) can be added to reduce trading frequency in oscillating markets

2. **Limitations of Fixed ATR Multiplier**:
   - The current strategy uses a fixed ATR multiplier (1.0), which may not be suitable for all market environments
   - During periods of extreme volatility, a fixed multiplier may result in stop-losses that are too wide or too narrow
   - Solution: Consider implementing an adaptive ATR multiplier that dynamically adjusts based on historical volatility statistics

3. **Parameter Sensitivity**:
   - The selection of SMA periods (7, 25, 99) may significantly impact strategy performance
   - Risk of over-optimization - specific parameter combinations may only perform well under specific market conditions
   - Risk mitigation: Conduct robustness testing to evaluate the impact of small parameter changes on strategy performance

4. **Slippage and Liquidity Risk**:
   - May face execution slippage issues in low liquidity markets or during high volatility periods
   - ATR-based stop-losses and take-profits may not be sufficient to protect capital under extreme market conditions
   - Solution: Increase margin requirements, reduce position size, or pause trading during abnormally high volatility

#### Strategy Optimization Directions

1. **Add Signal Filtering Mechanisms**:
   - Incorporate trend strength indicators (such as ADX), only trading when trend strength reaches a threshold
   - Integrate volume confirmation, requiring increased volume when signals appear to improve signal quality
   - Rationale: Multi-indicator confirmation can significantly reduce false signals and improve win rate

2. **Implement Adaptive Parameters**:
   - Change fixed SMA periods to dynamic parameters that automatically adjust based on market volatility or cyclicality
   - Adjust the ATR multiplier based on historical volatility statistics, using smaller multipliers during low volatility periods and larger multipliers during high volatility periods
   - Benefit: Adaptive parameters can better accommodate different market environments, improving strategy robustness

3. **Optimize Dynamic Risk-Reward Adjustment Mechanism**:
   - Transform the current binary risk-reward mechanism (2.0 or 6.0) into a continuous adjustment model
   - Dynamically adjust the risk-reward ratio based on trend strength indicators (such as ADX), market volatility, or recent trading performance
   - Improvement rationale: More detailed risk-reward adjustments can more accurately reflect market conditions, optimizing capital management effects

4. **Add Time Filters**:
   - Analyze strategy performance across different time periods (intraday, daily, weekly), avoiding trading during underperforming periods
   - Consider market seasonality factors, adjusting trading frequency in specific market environments
   - Advantage: Time filtering can avoid trading during statistically unfavorable periods, improving overall performance

5. **Integrate Machine Learning Models**:
   - Use machine learning algorithms to predict the reliability of SMA crossover signals
   - Train models based on historical data to identify high-probability profitable market patterns
   - Value: Machine learning can discover complex patterns difficult to capture with traditional technical indicators, enhancing strategy prediction capabilities

#### Summary

The SMA-ATR Dynamic Risk-Reward Trend Following Strategy provides a well-structured trend-following trading system that identifies market trends through multi-period moving averages and implements dynamic risk management using the ATR indicator. The most significant innovation of the strategy is its automatic adjustment of the risk-reward ratio based on specific market conditions, allowing the trading system to pursue higher returns in strong trending environments while maintaining robust risk control during regular trading.

This strategy combines classic elements of technical analysis (SMA crossovers, ATR stop-losses) with modern quantitative trading concepts (dynamic risk management), making it suitable for medium to long-term trend-following trading. While the strategy may face challenges in oscillating markets, through the suggested optimization directions (such as adding filters, adaptive parameters, and machine learning integration), its performance across different market environments can be further improved.

Overall, this is a quantitative trading strategy that balances simplicity and effectiveness, providing trend-following traders with a reliable framework while enhancing the strategy's adaptability and profit potential through dynamic risk management elements.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-14 00:00:00
end: 2024-11-27 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("TRH Backtest SMA ATR Variable RR", overlay=true)

// SMA Settings
sma7 = ta.sma(close, 7)
sma25 = ta.sma(close, 25)
sma99 = ta.sma(close, 99)

// ATR Settings
atrLength = input.int(14, title="ATR Length")
atrMultiplier = input.float(1.0, title="ATR Multiplier")
atr = ta.atr(atrLength) * atrMultiplier

// Entry and Exit Conditions
longCondition = ta.crossover(sma7, sma25) and close > sma99
shortCondition = ta.crossunder(sma7, sma25) and close < sma99
longCross = ta.crossover(sma7, sma99) or ta.crossover(sma7, sma25)
shortCross = ta.crossunder(sma7, sma99) or ta.crossunder(sma7, sma25)

// Trade Execution
if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

// Variable Risk Reward
riskRewardRatio = 2.0
if (longCross or shortCross)
    riskRewardRatio = 6.0

// ATR Based Stop Loss and Take Profit
longStopLoss = low - atr
shortStopLoss = high + atr
longTakeProfit = close + (atr * riskRewardRatio)
shortTakeProfit = close - (atr * riskRewardRatio)

// Apply Stop Loss and Take Profit
strategy.exit("Exit Long", "Long", stop=longStopLoss, limit=longTakeProfit)
strategy.exit("Exit Short", "Short", stop=shortStopLoss, limit=shortTakeProfit)

```

> Detail

https://www.fmz.com/strategy/486571

> Last Modified

2025-03-14 09:45:55
