
> Name

Long-short strategy based on support level and trend EMA-Support-Level-and-Trend-EMA-Based-Long-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8c8ee1ea8acb36b7324.png)
![IMG](https://www.fmz.com/upload/asset/2d8a8752e242d4969527d.png)




[trans]
#### Overview
This is a long strategy based on support levels and trend EMA. The strategy finds the best entry opportunities by identifying market trends and key support levels, and combines ATR dynamic stop loss and segmented profits to achieve risk management. This strategy mainly focuses on the situation when the price pulls back to the support level in the upward trend, and improves the success rate of the transaction by setting a reasonable risk-reward ratio.
#### Strategy Principle
The strategy uses the 100-period EMA as a trend judgment indicator and confirms an upward trend when the price is above the EMA. At the same time, calculate the lowest price of 10 periods as the short-term support level, and look for entry opportunities when the price pulls back near the support level (support level + 0.5*ATR). After entering the market, adopt the step-by-step profit-making method, take profit at 5 times ATR, close 50% of the position, and completely close the remaining position at 10 times ATR, and set 1 times ATR as a dynamic stop loss. The risk of each transaction is controlled within 3% of the total account value, and risk management is achieved through dynamic calculation of position size.
#### Strategic Advantages
1. Trend following characteristics: judge the trend through EMA and avoid counter-trend trading
2. Dynamic support level: Using the recent 10-period low as support can better reflect the current state of the market.
3. Flexible risk management: dynamic stop loss and profit targets based on ATR to adapt to market fluctuations
4. Segmented profit mechanism: Settlement in batches at different price levels to ensure profits without missing the big market trend
5. Accurate position control: dynamically calculate positions based on stop loss distance to achieve quantitative risk management
#### Strategy Risk
1. Risk of false breakthrough: False breakthrough may occur near the support level, it is recommended to add confirmation indicators
2. Trend reversal risk: The EMA indicator has hysteresis and can easily cause losses at the turning point of the trend.
3. Over-trading risk: Frequent support level triggers may lead to over-trading
4. Slippage risk: You may face larger slippage during violent fluctuations
Solution:
- Add trend confirmation indicator
- Optimize entry conditions
- Set transaction interval limit
- Adjust stop loss range
#### Strategy optimization direction
1. Multi-dimensional trend judgment: combine trend indicators of multiple time periods to improve the accuracy of trend judgment
2. Optimization of entry conditions: Add auxiliary indicators such as trading volume and volatility as entry filter conditions
3. Dynamic parameter optimization: adaptively adjust various parameters according to market conditions
4. Add market sentiment indicators: Introduce market sentiment indicators such as VIX to optimize trading opportunities
5. Improve the profit-taking mechanism: dynamically adjust profit targets according to market fluctuations
#### Summary
This strategy builds a complete trading system by combining trend following and support level pullbacks, and implements risk management through segmented profits and dynamic stops. The core advantage of the strategy lies in its complete risk control mechanism and clear trading logic, but parameters and entry conditions still need to be continuously optimized in practice to adapt to different market environments. It is recommended that traders conduct sufficient backtesting before using it in real trading, and make personalized adjustments to the strategy based on market experience. ||
#### Overview
This is a long-only strategy based on support levels and trend EMA. The strategy identifies optimal entry points by recognizing market trends and key support levels, combining ATR-based dynamic stop-loss and staged profit-taking for risk management. It focuses on price pullbacks to support levels during uptrends and aims to achieve high success rates through reasonable risk-reward ratios.

#### Strategy Principle
The strategy uses a 100-period EMA as a trend indicator, confirming an uptrend when price is above EMA. It calculates 10-period lows as short-term support levels and looks for entry opportunities when price pulls back near support (support + 0.5*ATR). After entry, it implements staged profit-taking, closing 50% position at 5x ATR and the remainder at 10x ATR, with a 1x ATR dynamic stop-loss. Risk is controlled within 3% of account equity per trade through dynamic position sizing.

#### Strategy Advantages
1. Trend-following characteristics: Uses EMA for trend identification, avoiding counter-trend trades
2. Dynamic support levels: Uses recent 10-period lows as support, better reflecting current market conditions
3. Flexible risk management: ATR-based dynamic stop-loss and profit targets, adapting to market volatility
4. Staged profit-taking: Gradual position closure at different price levels, securing profits while maintaining upside potential
5. Precise position sizing: Dynamic calculation based on stop-loss distance, achieving quantified risk management

#### Strategy Risks
1. False breakout risk: Potential false signals near support levels, additional confirmation indicators recommended
2. Trend reversal risk: EMA lag may cause losses at trend turning points
3. Overtrading risk: Frequent support level triggers may lead to excessive trading
4. Slippage risk: Significant slippage possible during volatile periods
Solutions:
- Add trend confirmation indicators
- Optimize entry conditions
- Set trading interval restrictions
- Adjust stop-loss ranges

#### Strategy Optimization Directions
1. Multi-dimensional trend analysis: Incorporate multiple timeframe trend indicators for improved accuracy
2. Entry condition optimization: Add volume, volatility, and other auxiliary indicators as entry filters
3. Dynamic parameter optimization: Adaptive parameter adjustment based on market conditions
4. Market sentiment integration: Include VIX and other sentiment indicators to optimize timing
5. Enhanced profit-taking: Dynamic adjustment of profit targets based on market volatility

#### Summary
The strategy establishes a complete trading system by combining trend following and support level pullbacks, implementing risk management through staged profit-taking and dynamic stop-loss. Its core strengths lie in comprehensive risk control mechanisms and clear trading logic, but continuous optimization of parameters and entry conditions is needed for different market environments. Traders are advised to conduct thorough backtesting before live implementation and make personalized adjustments based on market experience.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-22 00:00:00
end: 2024-05-30 00:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Ultra-Profitable SMC Long-Only Strategy", shorttitle="Ultra_Profit_SMC", overlay=true)

// User Inputs
emaTrendLength = input.int(100, title="Trend EMA Length")  // Faster EMA to align with aggressive trends
supportLookback = input.int(10, title="Support Lookback Period")  // Short-term support zones
atrLength = input.int(14, title="ATR Length")
atrMultiplierSL = input.float(1.0, title="ATR Multiplier for Stop-Loss")
atrMultiplierTP1 = input.float(5.0, title="ATR Multiplier for TP1")
atrMultiplierTP2 = input.float(10.0, title="ATR Multiplier for TP2")
riskPercent = input.float(3.0, title="Risk per Trade (%)", step=0.1)

// Calculate Indicators
emaTrend = ta.ema(close, emaTrendLength)  // Trend EMA
supportLevel = ta.lowest(low, supportLookback)  // Support Level
atr = ta.atr(atrLength)  // ATR

// Entry Conditions
isTrendingUp = close > emaTrend  // Price above Trend EMA
nearSupport = close <= supportLevel + (atr * 0.5)  // Price near support zone
longCondition = isTrendingUp and nearSupport

// Dynamic Stop-Loss and Take-Profit Levels
longStopLoss = supportLevel - (atr * atrMultiplierSL)
takeProfit1 = close + (atr * atrMultiplierTP1)  // Partial Take-Profit at 5x ATR
takeProfit2 = close + (atr * atrMultiplierTP2)  // Full Take-Profit at 10x ATR

// Position Sizing
capital = strategy.equity
tradeRisk = riskPercent / 100 * capital
positionSize = tradeRisk / (close - longStopLoss)

// Execute Long Trades
if (longCondition)
    strategy.entry("Ultra Long", strategy.long, qty=positionSize)

// Exit Conditions
strategy.exit("Partial Exit", from_entry="Ultra Long", limit=takeProfit1, qty_percent=50)  // Exit 50% at TP1
strategy.exit("Full Exit", from_entry="Ultra Long", limit=takeProfit2, qty_percent=100, stop=longStopLoss)  // Exit the rest at TP2

// Plot Indicators
plot(emaTrend, color=color.blue, title="Trend EMA")
plot(supportLevel, color=color.green, title="Support Level", linewidth=2)

```

> Detail

https://www.fmz.com/strategy/483049

> Last Modified

2025-02-21 10:56:01
