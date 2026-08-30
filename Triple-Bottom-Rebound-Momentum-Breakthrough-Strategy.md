
> Name

Triple-Bottom-Rebound-Momentum-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2fa88088c9448f366747853bf4463c8490412f54f0f8b0c80e77f26876acc5fe.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on technical analysis, which mainly conducts transactions by identifying triple bottom patterns and momentum breakout signals in the market. The strategy combines multiple technical indicators such as moving average (MA) crossover, true range (ATR), price channel, etc. to build a complete trading system. This strategy achieves automatic identification and transaction execution of triple bottom rebound patterns through a programmed approach.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Use the intersection of fast (5-period) and slow (20-period) moving averages to confirm market trend direction
2. The program automatically identifies three consecutive low points (low1, low2, low3) to form a triple bottom pattern.
3. Use the ATR indicator to calculate volatility and set dynamic stop loss and take profit levels.
4. After the third bottom, when the price breaks through the previous rebound high, combine the moving average cross signal to confirm the long opportunity
5. Establish parallel channels to visualize price movement ranges and provide additional market reference
6. Set dynamic stop loss and take profit conditions based on ATR during transaction execution
#### Strategic Advantages
1. Combine multiple technical indicators to improve the reliability of trading signals
2. Use ATR to dynamically adjust stop loss and take profit positions to adapt to changes in market volatility.
3. Automatically identify triple bottom patterns to reduce the influence of subjective judgments
4. Set trading interval limits to avoid excessive trading
5. Provide clear reference to market structure through visualization tools (parallel channels and labels)
6. The strategy logic is clear and easy to maintain and optimize.
#### Strategy Risk
1. False signals may appear in highly volatile markets
2. The identification process of triple bottom patterns may be affected by market noise
3. Fixed ATR multiples may not be suitable for all market environments
4. Continuous losses may occur during periods of dramatic trend transitions
5. The setting of trading interval may miss some valid signals.
#### Strategy optimization direction
1. Introduce trading volume indicators to confirm the effectiveness of rebounds
2. Dynamically adjust ATR multiples according to different market environments
3. Add trend strength filter to improve the quality of trading signals
4. Optimize the triple bottom identification algorithm to improve accuracy
5. Introduce market fluctuation cycle analysis and optimize trading interval settings
6. Consider adding symmetry analysis of price patterns
#### Summary
This strategy implements a triple bottom rebound breakthrough trading strategy through a programmed approach, combining multiple technical indicators and risk management methods, and has good practicality. Through continuous optimization and improvement, the strategy is expected to achieve better performance in actual trading. It is recommended to conduct sufficient backtest verification before real trading, and adjust parameter settings according to specific market conditions.
|| 

#### Overview
This strategy is a quantitative trading system based on technical analysis, primarily focusing on identifying triple bottom patterns and momentum breakthrough signals in the market. The strategy combines multiple technical indicators including Moving Average (MA) crossovers, Average True Range (ATR), and price channels to build a complete trading system. Through programmatic implementation, it achieves automated identification of triple bottom rebound patterns and trade execution.

#### Strategy Principles
The core logic includes the following key elements:
1. Using fast (5-period) and slow (20-period) moving average crossovers to confirm market trend direction
2. Automatically identifying three consecutive low points (low1, low2, low3) to form a triple bottom pattern
3. Utilizing ATR indicator to calculate volatility and set dynamic stop-loss and take-profit levels
4. Confirming long entry signals when price breaks above previous rebound high after the third bottom, combined with MA crossover signals
5. Establishing parallel channels to visualize price movement ranges for additional market reference
6. Implementing ATR-based dynamic stop-loss and take-profit conditions during trade execution

#### Strategy Advantages
1. Combines multiple technical indicators to enhance signal reliability
2. Uses ATR to dynamically adjust stop-loss and take-profit levels, adapting to market volatility changes
3. Automates triple bottom pattern identification, reducing subjective judgment
4. Implements trade interval restrictions to prevent overtrading
5. Provides clear market structure reference through visualization tools (parallel channels and labels)
6. Features clear strategy logic for easy maintenance and optimization

#### Strategy Risks
1. May generate false signals in highly volatile markets
2. Triple bottom pattern identification process may be affected by market noise
3. Fixed ATR multipliers may not suit all market conditions
4. May experience consecutive losses during trend reversal periods
5. Trade interval settings might miss some valid signals

#### Strategy Optimization Directions
1. Incorporate volume indicators to confirm rebound validity
2. Dynamically adjust ATR multipliers based on different market conditions
3. Add trend strength filters to improve trading signal quality
4. Optimize triple bottom identification algorithm to increase accuracy
5. Incorporate market cycle analysis to optimize trade interval settings
6. Consider adding price pattern symmetry analysis

#### Summary
This strategy implements a triple bottom rebound breakthrough trading system programmatically, combining multiple technical indicators and risk management measures with good practicality. Through continuous optimization and improvement, the strategy shows promise for better performance in actual trading. It is recommended to conduct thorough backtesting before live trading and adjust parameters according to specific market conditions.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-08 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/

//@version=5
strategy("反彈三次突破策略", overlay=true, initial_capital=100000, commission_value=0.001425, slippage=1)

// === 參數設定 ===
fast_length = input.int(5, title="快速均線週期")
slow_length = input.int(20, title="慢速均線週期")
atr_period = input.int(14, title="ATR 週期")
atr_factor = input.float(2.0, title="ATR 因子")
profit_factor = input.float(2.0, title="止盈因子")

// === 計算均線 ===
fast_ma = ta.ema(close, fast_length)
slow_ma = ta.ema(close, slow_length)

// === 均線交叉訊號 ===
long_signal = ta.crossover(fast_ma, slow_ma)
short_signal = ta.crossunder(fast_ma, slow_ma)

// === 計算 ATR ===
atr = ta.atr(atr_period)

// === 反彈三次突破策略 ===
var float low1 = na
var float low2 = na
var float low3 = na
var bool trend_down = false
var bool long_breakout = false
var line lower_line = na
var line upper_line = na

if (na(low1) or na(low2) or na(low3))
    // 初始化低點
    low1 := na
    low2 := na
    low3 := na

if (close < low3 or na(low3))
    // 更新低點
    low1 := low2
    low2 := low3
    low3 := close
    trend_down := true

if (trend_down and close > low2 and close > low1)
    // 確認反轉且第三次反彈比第二次高
    trend_down := false
    long_breakout := true

// 清除前一個反彈通道
if (not na(lower_line))
    line.delete(lower_line)
if (not na(upper_line))
    line.delete(upper_line)

// 繪製新的反彈通道
if (not na(low1) and not na(low3))    
    lower_line := line.new(x1=bar_index[2], y1=low1, x2=bar_index, y2=low3, color=color.yellow, width=2)
    upper_line := line.new(x1=bar_index[2], y1=low1 + (low3 - low1), x2=bar_index, y2=low3 + (low3 - low1), color=color.yellow, width=2)

// === 進出場條件 ===
var float last_long_exit = na
var float last_short_exit = na
var float stop_loss_long = na
var float take_profit_long = na
var float stop_loss_short = na
var float take_profit_short = na

var label stop_loss_label_long = na
var label take_profit_label_long = na
var label stop_loss_label_short = na
var label take_profit_label_short = na

if (long_signal or long_breakout)
    if na(last_short_exit) or (time - last_short_exit) > 2 * 60 * 60 * 1000  // 確保多頭出場後有一段時間間隔
        // 做多
        strategy.entry("做多", strategy.long)
        // 止損設置為最近低點下方
        stop_loss_long := low3 - atr_factor * atr
        take_profit_long := close + profit_factor * atr  // 設定止盈位置
        strategy.exit("止盈/止損", "做多", stop=stop_loss_long, limit=take_profit_long)
        last_long_exit := time  // 記錄多頭出場時間

        // 刪除之前的止盈止損標籤
        if (not na(stop_loss_label_long))
            label.delete(stop_loss_label_long)
        if (not na(take_profit_label_long))
            label.delete(take_profit_label_long)

        // 繪製新的止盈止損標籤
        stop_loss_label_long := label.new(x=bar_index, y=stop_loss_long, text=str.tostring(math.round(stop_loss_long * 10) / 10), color=color.red, style=label.style_label_down, textcolor=color.white, size=size.small)
        take_profit_label_long := label.new(x=bar_index, y=take_profit_long, text=str.tostring(math.round(take_profit_long * 10) / 10), color=color.green, style=label.style_label_up, textcolor=color.white, size=size.small)

if (short_signal)
    if na(last_long_exit) or (time - last_long_exit) > 2 * 60 * 60 * 1000  // 確保空頭出場後有一段時間間隔
        // 做空
        strategy.entry("做空", strategy.short)
        // 止損設置為最近高點上方
        stop_loss_short := high + atr_factor * atr
        take_profit_short := close - profit_factor * atr  // 設定止盈位置
        strategy.exit("止盈/止損", "做空", stop=stop_loss_short, limit=take_profit_short)
        last_short_exit := time  // 記錄空頭出場時間

        // 刪除之前的止盈止損標籤
        if (not na(stop_loss_label_short))
            label.delete(stop_loss_label_short)
        if (not na(take_profit_label_short))
            label.delete(take_profit_label_short)

        // 繪製新的止盈止損標籤
        stop_loss_label_short := label.new(x=bar_index, y=stop_loss_short, text=str.tostring(math.round(stop_loss_short * 10) / 10), color=color.red, style=label.style_label_down, textcolor=color.white, size=size.small)
        take_profit_label_short := label.new(x=bar_index, y=take_profit_short, text=str.tostring(math.round(take_profit_short * 10) / 10), color=color.green, style=label.style_label_up, textcolor=color.white, size=size.small)
```

> Detail

https://www.fmz.com/strategy/477961

> Last Modified

2025-01-10 15:49:30
