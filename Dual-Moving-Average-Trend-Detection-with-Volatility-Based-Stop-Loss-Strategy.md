
> Name

Dual-Moving-Average-Trend-Detection-with-Volatility-Based-Stop-Loss-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8548e431c041b320c10.png)
![IMG](https://www.fmz.com/upload/asset/2d97bf063525bdaf6b4d5.png)


[trans]
#### Overview
This strategy is a trend-following trading system that combines an exponential moving average (EMA) with a stop-loss mechanism based on true range (ATR). The strategy uses 9-period and 21-period EMA to identify market trends, and uses ATR to dynamically adjust the stop loss position, achieving an organic combination of trend tracking and risk control.
#### Strategy Principle
The core logic of the strategy consists of two main parts: trend judgment and risk control. In terms of trend judgment, the market trend is determined by monitoring the intersection of the fast EMA (9 periods) and the slow EMA (21 periods). When the fast line crosses the slow line, a long signal is triggered; when the fast line crosses below the slow line, a short signal is triggered. In terms of risk control, the strategy uses the ATR indicator to calculate dynamic stop loss positions. Specifically, the stop-loss point for long positions is set to the entry price minus 1.5 times the ATR value, and the stop-loss point for short positions is set to the entry price plus 1.5 times the ATR value.
#### Strategic Advantages
1. High accuracy of trend identification: By using EMA with two different periods, it can effectively filter market noise and improve the accuracy of trend judgment.
2. Flexible risk control: The dynamic stop-loss mechanism based on ATR can adaptively adjust according to market volatility, providing a looser stop-loss space when volatility intensifies, and tightening the stop-loss position when volatility weakens.
3. Strong parameter adjustability: The key parameters of the strategy (EMA cycle, ATR cycle, ATR multiplier) can be optimized and adjusted according to different market characteristics and trading cycles.
4. The implementation is simple and easy to understand: the strategy logic is clear and the code structure is concise, making it easy to understand and maintain.
#### Strategy Risk
1. Shock market risk: In a sideways shock market, moving average crossover signals are frequent, which may lead to over-trading and continuous stop losses.
2. Lagging risk: The EMA indicator itself has a certain degree of lag and may not respond in time when the market turns rapidly.
3. Risk of stop loss setting: The choice of ATR multiple needs to weigh the stop loss space and profit opportunities. Improper setting may lead to premature stop loss or excessive risk taking.
#### Strategy optimization direction
1. Introduce trend strength confirmation: you can add trend strength indicators (such as ADX) as trading filter conditions, and only enter the market when the trend is clear.
2. Dynamically adjust the ATR multiplier: The ATR multiplier can be automatically adjusted according to the market fluctuation cycle to improve the adaptability of stop loss settings.
3. Increase profit targets: You can set dynamic profit targets based on ATR to achieve dynamic management of risk-return ratio.
4. Add trading volume confirmation: Add trading volume analysis when confirming entry signals to improve the reliability of trading signals.
#### Summary
This strategy builds a complete trend following trading system by combining moving average crossover to determine the trend and ATR dynamic stop loss. The advantage of the strategy lies in objective judgment standards and flexible risk control, but it also requires attention to deal with the risk of volatile markets and signal lag issues. There is still room for improvement in the strategy by adding trend strength confirmation and optimizing stop loss settings. Overall, this is a trend following strategy with a solid foundation and clear logic, suitable as the basis for building more complex trading systems.  ||
#### Overview
This strategy is a trend-following trading system that combines Exponential Moving Averages (EMA) with a stop-loss mechanism based on the Average True Range (ATR). The strategy uses 9-period and 21-period EMAs to identify market trends while utilizing ATR to dynamically adjust stop-loss positions, achieving an organic combination of trend following and risk control.

#### Strategy Principle
The core logic of the strategy consists of two main components: trend determination and risk control. For trend determination, market trends are identified by monitoring the crossover between the fast EMA (9-period) and slow EMA (21-period). A long signal is triggered when the fast line crosses above the slow line, and a short signal is triggered when the fast line crosses below the slow line. For risk control, the strategy uses the ATR indicator to calculate dynamic stop-loss positions. Specifically, the stop-loss point for long positions is set at the entry price minus 1.5 times the ATR value, while the stop-loss point for short positions is set at the entry price plus 1.5 times the ATR value.

#### Strategy Advantages
1. High trend identification accuracy: By using two EMAs with different periods, the strategy effectively filters market noise and improves trend judgment accuracy.
2. Flexible risk control: The ATR-based dynamic stop-loss mechanism can adaptively adjust according to market volatility, providing wider stop-loss space during increased volatility and tighter stops during reduced volatility.
3. Strong parameter adaptability: Key parameters (EMA periods, ATR period, ATR multiplier) can be optimized for different market characteristics and trading timeframes.
4. Simple and understandable implementation: The strategy logic is clear, and the code structure is concise, making it easy to understand and maintain.

#### Strategy Risks
1. Sideways market risk: In ranging markets, frequent EMA crossover signals may lead to overtrading and consecutive stop-losses.
2. Lag risk: EMAs inherently have some lag, which may result in delayed reactions to rapid market reversals.
3. Stop-loss setting risk: The choice of ATR multiplier requires balancing between stop-loss space and profit opportunity; improper settings may lead to premature stops or excessive risk exposure.

#### Strategy Optimization Directions
1. Introduce trend strength confirmation: Add trend strength indicators (such as ADX) as trading filters to enter only during clear trends.
2. Dynamic adjustment of ATR multiplier: Automatically adjust the ATR multiplier based on market volatility cycles to improve stop-loss adaptability.
3. Add profit targets: Set dynamic profit targets based on ATR to achieve dynamic risk-reward ratio management.
4. Include volume confirmation: Add volume analysis for entry signal confirmation to improve trading signal reliability.

#### Summary
This strategy builds a complete trend-following trading system by combining EMA crossover trend determination with ATR dynamic stop-loss. The strategy's strengths lie in its objective judgment criteria and flexible risk control, but attention must be paid to sideways market risks and signal lag issues. There is significant room for improvement through adding trend strength confirmation, optimizing stop-loss settings, and other enhancements. Overall, this is a trend-following strategy with solid foundations and clear logic, suitable as a basis for building more complex trading systems.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-20 00:00:00
end: 2024-05-31 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"TRB_USDT"}]
*/

//@version=5
strategy("EMA 9/21 + ATR SL Strategy", shorttitle="EMA+ATR", overlay=true)

// ===== Input Parameters ===== //
emaFastLen  = input.int(9,  "Fast EMA")
emaSlowLen  = input.int(21, "Slow EMA")
atrLen      = input.int(14, "ATR Length")
atrMult     = input.float(1.5, "ATR Multiplier")

// ===== EMA Calculation ===== //
emaFast = ta.ema(close, emaFastLen)
emaSlow = ta.ema(close, emaSlowLen)

// ===== ATR Calculation ===== //
atrValue = ta.atr(atrLen)

// ===== Conditions for Entry ===== //
longCondition  = ta.crossover(emaFast, emaSlow)   // Long when 9 EMA crosses above 21 EMA
shortCondition = ta.crossunder(emaFast, emaSlow)  // Short when 9 EMA crosses below 21 EMA

// ===== Entry Commands ===== //
if longCondition
    strategy.entry("Long", strategy.long)

if shortCondition
    strategy.entry("Short", strategy.short)

// ===== Set Stop-Loss Using ATR ===== //
//
// For LONG: stop-loss = entry price - (atrMult * ATR)
// For SHORT: stop-loss = entry price + (atrMult * ATR)
//
// Note: You can adjust the atrMult values based on market volatility
//
if strategy.position_size > 0
    // If holding LONG, define stop-loss below the entry price
    strategy.exit("Exit Long", "Long", stop = strategy.position_avg_price - atrMult * atrValue)

if strategy.position_size < 0
    // If holding SHORT, define stop-loss above the entry price
    strategy.exit("Exit Short", "Short", stop = strategy.position_avg_price + atrMult * atrValue)

```

> Detail

https://www.fmz.com/strategy/482669

> Last Modified

2025-02-27 17:57:02
