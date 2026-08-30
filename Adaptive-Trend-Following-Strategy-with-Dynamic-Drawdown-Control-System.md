
> Name

Adaptive-Trend-Following-Strategy-with-Dynamic-Drawdown-Control-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1351ef9e99eaaf385ef.png)

[trans]
#### Overview
This strategy is a comprehensive trading system that combines trend following and risk control. It uses the 200-period exponential moving average (EMA) as a trend filter, the relative strength index (RSI) as an entry signal, and integrates stop loss, take profit, and maximum retracement control mechanisms. The main feature of the strategy is to strictly control risks through dynamic retracement tracking while maintaining the advantages of trend following.
#### Strategy Principle
The core logic of the strategy includes the following key components:
1. Trend identification: Use the 200-period EMA as the main trend judgment indicator. Only when the price is above the EMA will you consider going long.
2. Momentum confirmation: Use the RSI indicator as a momentum confirmation tool. Entry is only allowed when the RSI value exceeds the set threshold (default 50).
3. Risk management:
   - Set percentage stop loss (default 20%) and take profit (default 40%)
   - Dynamic retracement tracking system that automatically closes all positions when the overall strategy retracement exceeds the set limit (default 30%)
4. Position management: Use the account equity percentage (default 10%) for position control
#### Strategic Advantages
1. Strong adaptability: Through the combination of EMA and RSI, the strategy can adapt to different market environments
2. Improved risk control: multi-level risk control mechanism, including stop loss, stop profit and retracement limits
3. Scientific fund management: use the account equity percentage for position management to avoid risks caused by fixed lot sizes
4. Strong execution: clear strategy logic, clear signals, and easy to execute automatically
5. Good scalability: core components can be adjusted independently to facilitate further optimization
#### Strategy Risk
1. Trend reversal risk: EMA, as a lagging indicator, may not respond promptly enough when the trend reverses.
2. Volatile market risk: Frequent false signals may occur in a volatile market.
3. Parameter sensitivity: The strategy effect is more sensitive to parameter settings and requires careful tuning.
4. Impact of slippage: When the market fluctuates violently, stop-loss and take-profit orders may face the risk of slippage.
Solution:
- Add trend confirmation mechanism
-Introducing market environment identification system
- Adopt adaptive parameter optimization
- Use smart order execution strategies
#### Strategy optimization direction
1. Market environment identification: add volatility indicators and adjust strategy parameters according to different market environments
2. Dynamic parameter optimization: Introduce machine learning algorithms to achieve adaptive adjustment of parameters
3. Signal filtering optimization: increase auxiliary indicators such as trading volume and improve signal quality
4. Enhanced risk control: introduce a dynamic stop loss mechanism and adjust the stop loss position according to market fluctuations
5. Multi-time period analysis: Integrate signals from multiple time periods to improve the accuracy of trading decisions
#### Summary
This strategy builds a complete trading system by combining trend following and strict risk control. Its core advantages lie in the completeness of risk management and the clarity of strategic logic. Through multi-level risk control mechanisms, strategies can effectively control drawdowns while pursuing returns. Although there are some inherent risks, there is still considerable room for improvement in the strategy through the suggested optimization directions. ||
#### Overview
This strategy is a comprehensive trading system that combines trend following with risk control. It utilizes a 200-period Exponential Moving Average (EMA) as a trend filter, Relative Strength Index (RSI) as entry signals, while integrating stop-loss, take-profit, and maximum drawdown control mechanisms. The strategy's main feature is maintaining trend following advantages while strictly controlling risk through dynamic drawdown tracking.

#### Strategy Principle
The core logic includes several key components:
1. Trend Identification: Uses 200-period EMA as the primary trend indicator, only considering long positions when price is above EMA.
2. Momentum Confirmation: Uses RSI as a momentum confirmation tool, allowing entry only when RSI exceeds the set threshold (default 50).
3. Risk Management:
   - Percentage-based stop-loss (default 20%) and take-profit (default 40%)
   - Dynamic drawdown tracking system, automatically closing all positions when total strategy drawdown exceeds the set limit (default 30%)
4. Position Management: Uses account equity percentage (default 10%) for position control

#### Strategy Advantages
1. Strong Adaptability: Through EMA and RSI combination, the strategy can adapt to different market environments
2. Comprehensive Risk Control: Multi-level risk control mechanisms including stop-loss, take-profit, and drawdown limits
3. Scientific Capital Management: Uses account equity percentage for position management, avoiding risks from fixed position sizing
4. Strong Execution: Clear strategy logic and signals, easy to automate
5. Good Scalability: Core components can be adjusted independently, facilitating further optimization

#### Strategy Risks
1. Trend Reversal Risk: EMA as a lagging indicator may not respond timely to trend reversals
2. Choppy Market Risk: May generate frequent false signals in sideways markets
3. Parameter Sensitivity: Strategy performance is sensitive to parameter settings, requiring careful tuning
4. Slippage Impact: Stop-loss and take-profit orders may face slippage risk in volatile markets
Solutions:
- Enhanced trend confirmation mechanisms
- Introduction of market environment recognition system
- Adaptive parameter optimization
- Smart order execution strategies

#### Strategy Optimization Directions
1. Market Environment Recognition: Add volatility indicators to adjust strategy parameters based on different market conditions
2. Dynamic Parameter Optimization: Introduce machine learning algorithms for adaptive parameter adjustment
3. Signal Filter Optimization: Add volume and other auxiliary indicators to improve signal quality
4. Enhanced Risk Control: Introduce dynamic stop-loss mechanisms to adjust stop positions based on market volatility
5. Multi-timeframe Analysis: Integrate signals from multiple timeframes to improve trading decision accuracy

#### Summary
This strategy builds a complete trading system by combining trend following with strict risk control. Its core advantages lie in the completeness of risk management and clarity of strategy logic. Through multi-level risk control mechanisms, the strategy can effectively control drawdown while pursuing returns. Although there are some inherent risks, the strategy still has significant room for improvement through the suggested optimization directions.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-19 00:00:00
end: 2024-12-19 00:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title="Disruptor Trend-Following (Drawdown < 30%)", shorttitle="DisruptorStrategyDD", overlay=true)

//-----------------------------------------------------
// User Inputs
//-----------------------------------------------------
emaLen         = input.int(200,  "Long EMA Length",    minval=1)
rsiLen         = input.int(14,   "RSI Length",         minval=1)
rsiThreshold   = input.float(50, "RSI Buy Threshold",  minval=1, maxval=100)
stopLossPerc   = input.float(20, "Stop-Loss %",        minval=0.1, step=0.1)
takeProfitPerc = input.float(40, "Take-Profit %",      minval=0.1, step=0.1)
ddLimit        = input.float(30, "Max Drawdown %",     minval=0.1, step=0.1)

//-----------------------------------------------------
// Indicators
//-----------------------------------------------------
emaValue       = ta.ema(close, emaLen)
rsiValue       = ta.rsi(close, rsiLen)

//-----------------------------------------------------
// Conditions
//-----------------------------------------------------
longCondition  = close > emaValue and rsiValue > rsiThreshold
exitCondition  = close < emaValue or rsiValue < rsiThreshold

//-----------------------------------------------------
// Position Tracking
//-----------------------------------------------------
var bool inTrade = false

if longCondition and not inTrade
    strategy.entry("Long", strategy.long)

if inTrade and exitCondition
    strategy.close("Long")

inTrade := strategy.position_size > 0

//-----------------------------------------------------
// Stop-Loss & Take-Profit
//-----------------------------------------------------
if inTrade
    stopPrice       = strategy.position_avg_price * (1 - stopLossPerc / 100)
    takeProfitPrice = strategy.position_avg_price * (1 + takeProfitPerc / 100)
    strategy.exit("Exit", from_entry="Long", stop=stopPrice, limit=takeProfitPrice)

//-----------------------------------------------------
// Dynamic Drawdown Handling
//-----------------------------------------------------
var float peakEquity = strategy.equity
peakEquity := math.max(peakEquity, strategy.equity)

currentDrawdownPerc = (peakEquity - strategy.equity) / peakEquity * 100
if currentDrawdownPerc > ddLimit
    strategy.close_all("Max Drawdown Exceeded")

//-----------------------------------------------------
// Plotting
//-----------------------------------------------------
plot(emaValue, title="EMA 200", color=color.yellow, linewidth=2)
plotchar(rsiValue, title="RSI", char='•', location=location.bottom, color=color.new(color.teal, 60))

```

> Detail

https://www.fmz.com/strategy/475634

> Last Modified

2024-12-20 16:59:37
