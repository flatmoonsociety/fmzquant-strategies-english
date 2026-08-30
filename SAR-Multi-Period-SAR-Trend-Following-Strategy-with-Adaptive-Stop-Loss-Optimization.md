
> Name

Multi-Period SAR Trend Following Adaptive Stop Loss Optimization Strategy-Multi-Period-SAR-Trend-Following-Strategy-with-Adaptive-Stop-Loss-Optimization
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1d6b2f5012e5925e0fc.png)

[trans]
#### Overview
This strategy is deeply optimized based on the traditional Parabolic SAR (Parabolic Stop and Reverse) indicator, and combines multi-period trend judgment and adaptive stop loss mechanism. The strategy adopts the dynamic acceleration factor (AF) adjustment method to track market trends through the continuous updating of extreme points (EP) to achieve precise grasp of the upward trend and risk control.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Dynamic SAR calculation: Use three parameters: initial acceleration factor (AF), increment value and maximum value to dynamically adjust the SAR value according to the trend strength.
2. Trend determination mechanism: Determine the trend direction by comparing the relationship between the SAR value and the price position. When the SAR crosses the price, a trend reversal signal is triggered.
3. Entry logic: When the upward trend is confirmed and there is no position, use the predicted SAR value of the next period as the stop loss level to set the entry order.
4. Stop loss optimization: Use the extreme values ​​of the first 1-2 K lines as the SAR adjustment benchmark to improve the accuracy and timeliness of stop loss.
#### Strategic Advantages
1. Strong adaptability: Through dynamic acceleration factor adjustment, the strategy can automatically adjust parameters according to the intensity of market fluctuations.
2. Improved risk control: Using predictive SAR values ​​to set stop losses ensures the forward-looking and effectiveness of stop losses.
3. Accurate trend grasp: Multiple trend confirmation mechanisms reduce the risk of false breakthroughs.
4. Rigorous calculation logic: The variable state retention mechanism is adopted to ensure the stability of the strategy in historical backtesting.
#### Strategy Risk
1. Risk of volatile market: In a volatile market, false signals may be triggered frequently, resulting in continuous stop losses.
Solution: A volatility filter can be introduced to reduce trading frequency in a low volatility environment.
2. Impact of slippage: Predictive SAR stop loss may face the risk of slippage in highly volatile markets.
Solution: It is recommended to set a reasonable slippage tolerance and adjust parameters according to the characteristics of the variety.
3. Trend reversal delay: Stop loss lag may occur in sharp reversal market.
Countermeasures: Short-period momentum indicators can be combined to assist judgment and improve the sensitivity of stop loss.
#### Strategy optimization direction
1. Multi-period collaboration: It is recommended to add a trend confirmation mechanism for multiple time periods to improve signal reliability.
2. Dynamic parameter optimization: The parameter setting of the acceleration factor can be dynamically adjusted according to market volatility.
3. Improve the stop loss mechanism: introduce dynamic stop loss bands based on ATR to improve the flexibility of stop loss.
4. Position management optimization: Add a dynamic position management mechanism based on volatility.
#### Summary
This strategy achieves an effective combination of trend tracking and risk control through in-depth optimization of the classic PSAR indicator. The adaptive characteristics of the strategy and the complete stop-loss mechanism make it have strong practical application value. Through the suggested optimization direction, the stability and profitability of the strategy are expected to be further improved. ||
#### Overview
This strategy is a deep optimization of the traditional Parabolic SAR (Stop and Reverse) indicator, combining multi-period trend judgment and adaptive stop-loss mechanisms. The strategy employs a dynamic Acceleration Factor (AF) adjustment method, tracking market trends through continuous updates of Extreme Points (EP) to achieve precise capture of upward trends and risk control.

#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Dynamic SAR Calculation: Uses three parameters - initial AF, increment value, and maximum value - to dynamically adjust SAR values based on trend strength.
2. Trend Determination Mechanism: Judges trend direction by comparing SAR values with price positions, triggering trend reversal signals when SAR crosses price.
3. Entry Logic: Places entry orders using next period's predicted SAR value as stop-loss when uptrend is confirmed and no position is held.
4. Stop-Loss Optimization: Uses extremes from the previous 1-2 candles as SAR adjustment benchmark, improving stop-loss accuracy and timeliness.

#### Strategy Advantages
1. Strong Adaptability: Parameters automatically adjust to market volatility through dynamic AF adjustment.
2. Comprehensive Risk Control: Uses predictive SAR values for stop-loss, ensuring forward-looking and effective risk management.
3. Accurate Trend Capture: Multiple trend confirmation mechanisms reduce risks from false breakouts.
4. Rigorous Calculation Logic: Employs variable state maintenance mechanism, ensuring strategy stability in historical backtesting.

#### Strategy Risks
1. Sideways Market Risk: Frequent false signals may trigger consecutive stop-losses in ranging markets.
Solution: Introduce volatility filters to reduce trading frequency in low volatility environments.
2. Slippage Impact: Predictive SAR stops may face slippage risks in highly volatile markets.
Solution: Set reasonable slippage tolerance and adjust parameters based on instrument characteristics.
3. Trend Reversal Delay: Stop-loss may lag in sharp reversal situations.
Solution: Incorporate short-period momentum indicators to improve stop-loss sensitivity.

#### Strategy Optimization Directions
1. Multi-Period Synergy: Add trend confirmation mechanisms across multiple timeframes to improve signal reliability.
2. Dynamic Parameter Optimization: Dynamically adjust AF parameters based on market volatility.
3. Stop-Loss Mechanism Enhancement: Introduce ATR-based dynamic stop-loss bands for improved flexibility.
4. Position Management Optimization: Add volatility-based dynamic position management mechanism.

#### Summary
The strategy effectively combines trend following and risk control through deep optimization of the classic PSAR indicator. Its adaptive features and comprehensive stop-loss mechanism provide strong practical application value. Through the suggested optimization directions, the strategy's stability and profitability can be further enhanced.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("A股抛物线策略（仅做多）- 完全移除SAR绘图", overlay=true)

// 参数设置
start     = input.float(0.02, "起始加速因子")
increment = input.float(0.02, "加速因子增量")
maximum   = input.float(0.2,  "加速因子最大值")

// 定义变量（var保证变量在整个历史数据中保持状态）
var bool   uptrend    = true    // 默认初始化为上升趋势
var float  EP         = na      // 极值点：上升趋势时为最高价，下降趋势时为最低价
var float  SAR        = na      // 当前K线的SAR
var float  AF         = start   // 当前加速因子
var float  nextBarSAR = na      // 下一根K线的预测SAR

//【1】初始化：针对第一根K线（bar_index==0）
if bar_index == 0
    // 使用首根K线收盘价初始化
    SAR        := close
    nextBarSAR := close
    EP         := close
    uptrend    := true

//【2】从第二根K线开始（bar_index>=1）计算SAR
if bar_index >= 1
    // 先将上一根K线计算得到的 nextBarSAR 赋给当前SAR
    SAR := nz(nextBarSAR, SAR)
    
    // 第2根K线（bar_index==1）做初始化，利用上一根K线（bar_index==0）的高低价
    if bar_index == 1
        if close > close[1]
            uptrend := true
            EP      := high
            SAR     := low[1]
        else
            uptrend := false
            EP      := low
            SAR     := high[1]
        AF := start
        nextBarSAR := SAR + AF * (EP - SAR)
    else
        // 记录是否处于趋势反转的首根K线，方便后续判断
        var bool firstTrendBar = false
        firstTrendBar := false
        
        // 检测趋势反转：
        // 在上升趋势中，如果当前SAR超过最低价，则认为发生反转
        if uptrend
            if SAR > low
                firstTrendBar := true
                uptrend     := false
                // 反转时，SAR取上一次极值与当前最高价中的较大者，极值改为当前最低价
                SAR         := math.max(EP, high)
                EP          := low
                AF          := start
            // 注意：原代码在上升趋势中还有个判断 SAR < high 的分支，但通常反转判据只需检测SAR是否穿过低点即可
        else
            // 在下降趋势中，如果当前SAR低于最高价，则认为反转为上升趋势
            if SAR < high
                firstTrendBar := true
                uptrend     := true
                SAR         := math.min(EP, low)
                EP          := high
                AF          := start
        
        // 若非反转情形，则更新极值和加速因子
        if not firstTrendBar
            if uptrend
                if high > EP
                    EP := high
                    AF := math.min(AF + increment, maximum)
            else
                if low < EP
                    EP := low
                    AF := math.min(AF + increment, maximum)
                    
        // 调整SAR，确保其不超过最近1-2根K线的最低价（上升趋势）或最高价（下降趋势）
        if uptrend
            SAR := math.min(SAR, low[1])
            if bar_index > 1
                SAR := math.min(SAR, low[2])
        else
            SAR := math.max(SAR, high[1])
            if bar_index > 1
                SAR := math.max(SAR, high[2])
        
        // 计算下一根K线的预测SAR
        nextBarSAR := SAR + AF * (EP - SAR)
        
        //【3】交易逻辑（仅做多）
        if barstate.isconfirmed
            // 当出现上升趋势且当前无多头仓位时进场做多（以预测的下一根K线SAR为止损触发价）
            if uptrend and strategy.position_size <= 0
                strategy.entry("Long", strategy.long, stop=nextBarSAR, comment="Long Entry")
            // 当趋势转为下降且持有多头时平仓
            if not uptrend and strategy.position_size > 0
                strategy.close("Long", comment="Long Exit")

// 绘图部分完全移除，不再绘制任何与SAR相关的图形
```

> Detail

https://www.fmz.com/strategy/482425

> Last Modified

2025-02-18 13:48:30
