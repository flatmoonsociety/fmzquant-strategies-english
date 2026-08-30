
> Name

SUPERTREND trend following long take profit and stop loss strategySUPERTREND-Trend-following-Long-Position-with-Stop-loss-and-Take-profit-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/19dd3f1c70e2138d7a2.png)

[trans]
#### Overview
This strategy uses the Supertrend indicator to time trade entries and exits. Supertrend is a trend following indicator that combines the concepts of dynamic support, resistance and price breakouts. This strategy is designed to capture strong uptrends while tightly controlling risk and trading with a risk-to-reward ratio of 1:5. When the price breaks through the Supertrend upper track, open a long position and set the stop loss and take profit prices according to the preset risk-reward ratio. Once the price falls below the Supertrend lower band, the strategy will close the long position.
#### Strategy Principle
1. Calculate the upper and lower rails of the Supertrend indicator. Supertrend uses ATR (Average True Range) and factors to calculate dynamic support and resistance levels.
2. Check the conditions for opening a long position: when the closing price breaks through the Supertrend upper track, open a long position.
3. Calculate stop-loss and take-profit prices: Based on the current closing price and the preset risk-reward ratio (such as 1:5), calculate the stop-loss price and take-profit price.
4. Submit a long order: Open a long position at the calculated stop loss price and take profit price.
5. Check the long position closing conditions: when the closing price falls below the Supertrend lower track, close the long position.
#### Advantage Analysis
1. Trend following: Supertrend indicator can effectively capture strong trends and help strategies make profits in upward trends.
2. Dynamic stop loss: By using ATR to calculate dynamic support and resistance levels, Supertrend provides dynamic stop loss levels for the strategy to control risk.
3. Risk-reward control: This strategy allows users to preset a risk-reward ratio (such as 1:5) to control the risk and potential reward of each transaction.
4. Simple and easy to use: The strategy logic is clear and easy to understand and implement.
#### Risk Analysis
1. Trend Reversal: In a sudden trend reversal, this strategy may suffer losses as it relies on trend continuation.
2. Parameter sensitivity: The performance of the strategy may be sensitive to Supertrend’s parameters (such as ATR factor and ATR length). Improper parameters can lead to false signals.
3. Lack of volatility: In low-volatility market environments, this strategy may not work well because prices may fluctuate between the upper and lower bands, resulting in frequent transactions and fee losses.
#### Optimization direction
1. Dynamic parameter optimization: Implement parameter optimization procedures to dynamically adjust Supertrend parameters according to different market conditions. This can improve the adaptability and robustness of the strategy.
2. Combine with other indicators: Combine with other technical indicators, such as RSI or MACD, to confirm trend strength and filter out false signals.
3. Market environment adaptation: Develop logic to identify different market conditions (such as trends, shocks), and adjust strategy parameters or disable strategies accordingly.
4. Fund management optimization: Optimize position size and risk management rules to improve the risk-adjusted return of the strategy.
#### Summary
This strategy utilizes the Supertrend indicator to track strong uptrends while tightly controlling risk. It provides a simple yet effective framework for capturing trending opportunities. However, strategies may face risks such as trend reversal and parameter sensitivity. The strategy can be further improved through dynamic parameter optimization, combining other indicators, adapting to market conditions and optimizing money management. Overall, this Supertrend strategy provides a solid foundation for trend following trading.
|| 

#### Overview
This strategy utilizes the Supertrend indicator to determine entry and exit points for trades. Supertrend is a trend-following indicator that combines the concepts of dynamic support/resistance and price breakouts. The strategy aims to capture strong uptrends while strictly controlling risk, and it trades with a 1:5 risk-reward ratio. When the price breaks above the Supertrend upper band, it enters a long position and sets a stop-loss and take-profit price based on the predefined risk-reward ratio. Once the price breaks below the Supertrend lower band, the strategy closes the long position.

#### Strategy Principles
1. Calculate the upper and lower bands of the Supertrend indicator. Supertrend uses ATR (Average True Range) and a factor to calculate dynamic support and resistance levels.
2. Check for long entry conditions: When the closing price breaks above the Supertrend upper band, enter a long position.
3. Calculate stop-loss and take-profit prices: Based on the current closing price and the predefined risk-reward ratio (e.g., 1:5), calculate the stop-loss and take-profit prices.
4. Submit a long order: Open a long position with the calculated stop-loss and take-profit prices.
5. Check for long exit conditions: When the closing price breaks below the Supertrend lower band, close the long position.

#### Advantage Analysis
1. Trend-following: The Supertrend indicator can effectively capture strong trends, helping the strategy profit from uptrends.
2. Dynamic stop-loss: By using ATR to calculate dynamic support and resistance levels, Supertrend provides a dynamic stop-loss for the strategy to control risk.
3. Risk-reward control: The strategy allows users to predefine a risk-reward ratio (e.g., 1:5) to control the risk and potential reward for each trade.
4. Simplicity: The strategy logic is straightforward and easy to understand and implement.

#### Risk Analysis
1. Trend reversals: In sudden trend reversals, the strategy may suffer losses as it relies on the continuity of the trend.
2. Parameter sensitivity: The strategy's performance may be sensitive to the parameters of the Supertrend, such as the ATR factor and ATR length. Inappropriate parameters may lead to false signals.
3. Lack of volatility: In low volatility market conditions, the strategy may underperform as prices may oscillate between the upper and lower bands, leading to frequent trades and losses due to slippage and commissions.

#### Optimization Directions
1. Dynamic parameter optimization: Implement a parameter optimization routine to dynamically adjust Supertrend parameters based on different market conditions. This can improve the adaptability and robustness of the strategy.
2. Combine with other indicators: Incorporate other technical indicators, such as RSI or MACD, to confirm trend strength and filter out false signals.
3. Market condition adaptation: Develop logic to identify different market conditions (e.g., trending, ranging) and adjust strategy parameters or disable the strategy accordingly.
4. Money management optimization: Optimize position sizing and risk management rules to improve the risk-adjusted returns of the strategy.

#### Summary
This strategy leverages the Supertrend indicator to follow strong uptrends while strictly controlling risk. It provides a simple yet effective framework for capturing trending opportunities. However, the strategy may face risks such as trend reversals and parameter sensitivity. Further improvements can be made through dynamic parameter optimization, combining with other indicators, adapting to market conditions, and optimizing money management. Overall, this Supertrend strategy offers a solid foundation for trend-following trading.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-05-01 00:00:00
end: 2024-05-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Supertrend Strategy with 1:5 Risk Reward", overlay=true)

// Supertrend Indicator
factor = input(3.0, title="ATR Factor")
atrLength = input(10, title="ATR Length")

[supertrendUp, supertrendDown] = ta.supertrend(factor, atrLength)

supertrend = ta.crossover(ta.lowest(close, 1), supertrendDown) ? supertrendDown : supertrendUp

plot(supertrend, title="Supertrend", color=supertrend == supertrendUp ? color.green : color.red, linewidth=2, style=plot.style_line)

// Strategy parameters
risk = input(1.0, title="Risk in %")
reward = input(5.0, title="Reward in %")
riskRewardRatio = reward / risk

// Entry and exit conditions
longCondition = ta.crossover(close, supertrendUp)
if (longCondition)
    // Calculate stop loss and take profit levels
    stopLossPrice = close * (1 - (risk / 100))
    takeProfitPrice = close * (1 + (reward / 100))
    
    // Submit long order
    strategy.entry("Long", strategy.long, stop=stopLossPrice, limit=takeProfitPrice)

// Exit conditions
shortCondition = ta.crossunder(close, supertrendDown)
if (shortCondition)
    strategy.close("Long")

```

> Detail

https://www.fmz.com/strategy/454363

> Last Modified

2024-06-17 16:32:24
