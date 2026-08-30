
> Name

Dual-Moving-Average-Trend-Following-Strategy-with-Risk-Management
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1bfc9d0f1ab2bac93ce.png)

[trans]
#### Overview
This strategy is a trend following trading system based on the intersection of the 110-day and 200-day exponential moving averages (EMA). The strategy determines the market trend by observing the crossing of the short-period EMA over the long-period EMA, and combines the stop-loss and take-profit mechanisms to control risks. After confirming the trend signal, the system will automatically execute corresponding long and short trading operations while monitoring position risks in real time.
#### Strategy Principle
The core logic of the strategy is based on the continuity characteristics of the price trend, and the trend conversion signal is captured through the intersection of EMA110 and EMA200. When the short-term moving average (EMA110) crosses the long-term moving average (EMA200), it indicates that an upward trend has formed, and the system sends a long signal; when the short-term moving average crosses below the long-term moving average, it indicates that a downward trend has formed, and the system sends a short signal. In order to control risks, the strategy will set a 1% stop loss level and a 0.5% take profit level every time a position is opened to protect vested profits and limit possible losses.
#### Strategic Advantages
1. Strong trend grasping ability: Capturing mid- and long-term trends through double moving average crossovers can effectively filter short-term market noise
2. Improved risk control: integrated stop-loss and stop-profit mechanisms, which can effectively control the risk of a single transaction
3. Rigorous execution logic: reverse positions will be automatically closed before opening new positions to avoid repeated positions.
4. Clear signal prompts: The trading signals are intuitively displayed through the signal prompt form in the upper right corner of the interface.
5. Reasonable parameter setting: choosing 110 days and 200 days as the moving average period can better balance sensitivity and stability
#### Strategy Risk
1. Volatile market risk: Frequent trading may lead to losses in a volatile market.
2. Slippage risk: You may face large transaction slippage when the market fluctuates violently.
3. Trend reversal risk: Stop loss may not be timely enough when the trend suddenly reverses
4. Parameter optimization risk: Over-optimizing parameters may lead to policy overfitting
5. Systemic risk: You may face systemic risks when the market fluctuates violently.
#### Strategy optimization direction
1. Introduce trading volume indicators: combine with trading volume analysis to confirm the validity of the trend
2. Optimize the stop loss mechanism: consider using trailing stop loss or ATR dynamic stop loss
3. Add trend filter: add trend strength indicator to filter weak trend signals
4. Improve position management: dynamically adjust position size based on trend strength
5. Add retracement control: set the maximum retracement limit and suspend trading when the threshold is reached.
#### Summary
This strategy captures trends through moving average crossovers and combines stop-loss and take-profit mechanisms to manage risks. The overall design is reasonable and the logic is rigorous. Although it may perform poorly in volatile markets, the stability and profitability of the strategy can be further improved through the suggested optimization directions. The strategy is suitable for medium and long-term investors who pursue stable returns. ||
#### Overview
This strategy is a trend-following trading system based on the crossover of 110-day and 200-day Exponential Moving Averages (EMA). It identifies market trends through the intersection of short-term and long-term EMAs, incorporating stop-loss and take-profit mechanisms for risk control. The system automatically executes long and short positions upon trend confirmation while continuously monitoring position risk.

#### Strategy Principle
The core logic relies on the continuity of price trends, using EMA110 and EMA200 crossovers to capture trend reversal signals. When the shorter-term moving average (EMA110) crosses above the longer-term moving average (EMA200), it signals an uptrend formation, triggering a long position. Conversely, when the shorter-term moving average crosses below the longer-term moving average, it signals a downtrend formation, triggering a short position. For risk management, the strategy sets a 1% stop-loss and 0.5% take-profit level for each position to protect profits and limit potential losses.

#### Strategy Advantages
1. Strong trend capture capability: Effectively filters short-term market noise through dual moving average crossovers
2. Comprehensive risk control: Integrated stop-loss and take-profit mechanisms effectively control single-trade risk
3. Rigorous execution logic: Automatically closes reverse positions before opening new ones, avoiding position overlap
4. Clear signal indication: Trade signals are clearly displayed in the top-right corner table
5. Reasonable parameter settings: 110-day and 200-day periods balance sensitivity and stability

#### Strategy Risks
1. Sideways market risk: Frequent trading in range-bound markets may lead to losses
2. Slippage risk: Significant slippage may occur during high market volatility
3. Trend reversal risk: Stop-losses may not trigger quickly enough during sudden trend reversals
4. Parameter optimization risk: Over-optimization may lead to strategy overfitting
5. Systemic risk: Exposure to systemic risks during extreme market conditions

#### Strategy Optimization Directions
1. Incorporate volume indicators: Confirm trend validity through volume analysis
2. Optimize stop-loss mechanism: Consider implementing trailing stops or ATR-based dynamic stops
3. Add trend filters: Integrate trend strength indicators to filter weak signals
4. Improve position management: Dynamically adjust position sizes based on trend strength
5. Implement drawdown control: Set maximum drawdown limits to pause trading when thresholds are reached

#### Summary
The strategy captures trends through moving average crossovers while managing risk through stop-loss and take-profit mechanisms, demonstrating sound design and logical rigor. Although it may underperform in ranging markets, the suggested optimizations can further enhance strategy stability and profitability. The strategy is suitable for medium to long-term investors seeking steady returns.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA110/200 Cross with Stop-Loss and Take-Profit", overlay=true)

// 定义EMA110和EMA200
ema110 = ta.ema(close, 110)
ema200 = ta.ema(close, 250)

// 画出EMA
plot(ema110, color=color.blue, title="EMA110")
plot(ema200, color=color.red, title="EMA200")

// 计算交叉信号
longCondition = ta.crossover(ema110, ema200)  // EMA110上穿EMA200，做多
shortCondition = ta.crossunder(ema110, ema200)  // EMA110下穿EMA200，做空

// 设置止损和止盈
stopLoss = 0.01  // 止损1%
takeProfit = 0.005  // 止盈0.5%

// 判断是否已有仓位
isLong = strategy.position_size > 0  // 当前是否为多头仓位
isShort = strategy.position_size < 0  // 当前是否为空头仓位

// 执行策略：做多时平空，做空时平多
if (longCondition and not isLong)  // 如果满足做多条件并且当前没有多头仓位
    if (isShort)  // 如果当前是空头仓位，先平空
        strategy.close("Short")
    strategy.entry("Long", strategy.long)  // 执行做多
    strategy.exit("Take Profit/Stop Loss", "Long", stop=close * (1 - stopLoss), limit=close * (1 + takeProfit))

if (shortCondition and not isShort)  // 如果满足做空条件并且当前没有空头仓位
    if (isLong)  // 如果当前是多头仓位，先平多
        strategy.close("Long")
    strategy.entry("Short", strategy.short)  // 执行做空
    strategy.exit("Take Profit/Stop Loss", "Short", stop=close * (1 + stopLoss), limit=close * (1 - takeProfit))

// 在表格中显示信号
var table myTable = table.new(position.top_right, 1, 1)
if (longCondition and not isLong)
    table.cell(myTable, 0, 0, "Buy Signal", text_color=color.green)
if (shortCondition and not isShort)
    table.cell(myTable, 0, 0, "Sell Signal", text_color=color.red)

```

> Detail

https://www.fmz.com/strategy/475597

> Last Modified

2024-12-20 14:30:29
