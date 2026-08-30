
> Name

Advanced-WaveTrend-and-EMA-Ribbon-Fusion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1bcae696820841889e6.png)

[trans]
#### Overview
This strategy is an advanced trading system that combines the WaveTrend oscillator and EMA moving average bands. By fusing these two technical indicators, a trading strategy is formed that can accurately capture the turning points of market trends. The strategy adopts dynamic stop-profit and stop-loss settings to pursue higher returns while protecting the safety of funds.
#### Strategy Principle
The core of the strategy is to identify trading signals through the synergy of the WaveTrend indicator and eight EMA moving averages. The WaveTrend indicator measures overbought and oversold conditions by calculating the deviation of price from a moving average. The EMA moving average band confirms the trend direction through the intersection of moving averages of different periods. Specifically:
1. When EMA2 crosses above EMA8, or a blue triangle signal appears (EMA2 crosses above EMA3) and there is no blood diamond pattern, the long signal is triggered
2. When EMA8 crosses EMA2, or a blood diamond pattern appears, a short signal is triggered.
3. The stop loss setting adopts the extreme point after the previous reverse signal, which can effectively control risks.
4. The take-profit target is set to 2-3 times the stop-loss distance, reflecting a good risk-return ratio.
#### Strategic Advantages
1. The double confirmation mechanism improves the reliability of trading signals
2. Dynamic stop loss settings can better adapt to market fluctuations
3. Have a clear risk-benefit ratio setting
4. The use of EMA moving average bands helps determine the overall market trend.
5. The WaveTrend indicator can effectively identify overbought and oversold conditions in the market.
6. The strategy has clear logic and is easy to understand and execute.
#### Strategy Risk
1. Frequent false signals may occur in volatile markets
2. Dynamic stop loss may be easily triggered during violent fluctuations
3. Indicators calculated based on historical data may become invalid when the market changes drastically.
4. The use of multiple technical indicators may cause signal lag
Solution:
- Volatility filter can be added to reduce false signals that shake the market
- Consider using looser stop loss settings
- Added trend strength confirmation mechanism
#### Strategy optimization direction
1. Introduce market volatility indicators (such as ATR) to dynamically adjust the stop loss distance
2. Add a trading volume confirmation mechanism to improve signal reliability
3. Consider adding a trend strength filter to only trade in strong trending markets
4. Optimize WaveTrend parameters to better adapt to different market environments
5. Study the synergy of signals in different time periods
#### Summary
This is a complete trading system that combines trend following and oscillators from technical analysis. Through the combined use of WaveTrend and EMA moving average bands, you can not only grasp the general trend, but also enter the market in time at the turning point of the trend. The dynamic stop-profit and stop-loss management mechanism provides good risk control capabilities for the strategy. The optimization space of the strategy mainly lies in improvements in signal filtering and risk management. ||
#### Overview
This strategy is an advanced trading system that combines the WaveTrend oscillator indicator with EMA ribbons. By integrating these two technical indicators, it creates a trading strategy capable of accurately capturing market trend reversal points. The strategy employs dynamic stop-loss and take-profit settings to pursue higher returns while protecting capital.

#### Strategy Principles
The core of the strategy lies in the synergistic use of the WaveTrend indicator and eight EMA lines to identify trading signals. The WaveTrend indicator measures market overbought and oversold conditions by calculating the deviation between price and moving averages. The EMA ribbon confirms trend direction through crossovers of different period moving averages. Specifically:
1. Long signals are triggered when EMA2 crosses above EMA8, or when a blue triangle signal appears (EMA2 crosses above EMA3) without a blood diamond pattern
2. Short signals are triggered when EMA8 crosses above EMA2, or when a blood diamond pattern appears
3. Stop-loss is set at the extreme point after the previous counter signal, effectively controlling risk
4. Take-profit targets are set at 2-3 times the stop-loss distance, demonstrating a good risk-reward ratio

#### Strategy Advantages
1. Dual confirmation mechanism improves trading signal reliability
2. Dynamic stop-loss settings better adapt to market volatility
3. Clear risk-reward ratio settings
4. EMA ribbon helps determine overall market trends
5. WaveTrend indicator effectively identifies market overbought/oversold conditions
6. Clear strategy logic that's easy to understand and execute

#### Strategy Risks
1. May generate frequent false signals in ranging markets
2. Dynamic stops may be easily triggered during severe volatility
3. Indicators based on historical data may fail during market regime changes
4. Multiple technical indicators may lead to signal lag
Solutions:
- Add volatility filters to reduce false signals in ranging markets
- Consider using wider stop-loss settings
- Add trend strength confirmation mechanisms

#### Optimization Directions
1. Introduce volatility indicators (like ATR) for dynamic stop-loss adjustment
2. Add volume confirmation mechanism to improve signal reliability
3. Consider adding trend strength filters to trade only in strong trend markets
4. Optimize WaveTrend parameters for better adaptation to different market conditions
5. Study signal synergy across different timeframes

#### Summary
This is a complete trading system that combines trend following and oscillator indicators in technical analysis. Through the coordinated use of WaveTrend and EMA ribbons, it can both capture major trends and enter timely at trend reversal points. The dynamic stop-loss and take-profit management mechanism provides good risk control capability. Strategy optimization potential mainly lies in improving signal filtering and risk management.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-06 00:00:00
end: 2025-01-04 08:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("VuManChu Cipher A Strategy", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1.0)

// === 函数定义 ===
// WaveTrend函数
f_wavetrend(_src, _chlen, _avg, _malen) =>
    _esa = ta.ema(_src, _chlen)
    _de = ta.ema(math.abs(_src - _esa), _chlen)
    _ci = (_src - _esa) / (0.015 * _de)
    _tci = ta.ema(_ci, _avg)
    _wt1 = _tci
    _wt2 = ta.sma(_wt1, _malen)
    [_wt1, _wt2]

// EMA Ribbon函数
f_emaRibbon(_src, _e1, _e2, _e3, _e4, _e5, _e6, _e7, _e8) =>
    _ema1 = ta.ema(_src, _e1)
    _ema2 = ta.ema(_src, _e2)
    _ema3 = ta.ema(_src, _e3)
    _ema4 = ta.ema(_src, _e4)
    _ema5 = ta.ema(_src, _e5)
    _ema6 = ta.ema(_src, _e6)
    _ema7 = ta.ema(_src, _e7)
    _ema8 = ta.ema(_src, _e8)
    [_ema1, _ema2, _ema3, _ema4, _ema5, _ema6, _ema7, _ema8]

// === 变量声明 ===
var float stopPrice = na      // 止损价格变量
var float targetPrice = na    // 止盈价格变量
var float lastLongPrice = na
var float lastShortPrice = na
var float highestSinceLastLong = na
var float lowestSinceLastShort = na

// === WaveTrend参数 ===
wtChannelLen = input.int(9, title = 'WT Channel Length')
wtAverageLen = input.int(13, title = 'WT Average Length')
wtMASource = hlc3
wtMALen = input.int(3, title = 'WT MA Length')

// === EMA Ribbon参数 ===
ema1Len = input.int(5, "EMA 1 Length")
ema2Len = input.int(11, "EMA 2 Length")
ema3Len = input.int(15, "EMA 3 Length")
ema4Len = input.int(18, "EMA 4 Length")
ema5Len = input.int(21, "EMA 5 Length")
ema6Len = input.int(24, "EMA 6 Length")
ema7Len = input.int(28, "EMA 7 Length")
ema8Len = input.int(34, "EMA 8 Length")

// === 计算指标 ===
// WaveTrend计算
[wt1, wt2] = f_wavetrend(wtMASource, wtChannelLen, wtAverageLen, wtMALen)

// WaveTrend交叉条件
wtCross = ta.cross(wt1, wt2)
wtCrossDown = wt2 - wt1 >= 0

// EMA Ribbon计算
[ema1, ema2, ema3, ema4, ema5, ema6, ema7, ema8] = f_emaRibbon(close, ema1Len, ema2Len, ema3Len, ema4Len, ema5Len, ema6Len, ema7Len, ema8Len)

// === 交易信号 ===
longEma = ta.crossover(ema2, ema8)
shortEma = ta.crossover(ema8, ema2)
redCross = ta.crossunder(ema1, ema2)
blueTriangle = ta.crossover(ema2, ema3)
redDiamond = wtCross and wtCrossDown
bloodDiamond = redDiamond and redCross

// 更新最高最低价
if not na(lastLongPrice)
    highestSinceLastLong := math.max(high, nz(highestSinceLastLong))
if not na(lastShortPrice)
    lowestSinceLastShort := math.min(low, nz(lowestSinceLastShort))

// === 交易信号条件 ===
longCondition = longEma or (blueTriangle and not bloodDiamond)
shortCondition = shortEma or bloodDiamond

// === 执行交易 ===
if (longCondition)
    // 记录多头入场价格
    lastLongPrice := close
    // 重置最高价跟踪
    highestSinceLastLong := high
    
    stopPrice := nz(lowestSinceLastShort, close * 0.98)  // 使用前一个空头信号后的最低价作为止损
    float riskAmount = math.abs(close - stopPrice)
    targetPrice := close + (riskAmount * 2)  // 止盈为止损距离的2倍
    
    strategy.entry("做多", strategy.long)
    strategy.exit("多头止盈止损", "做多", limit=targetPrice, stop=stopPrice)

if (shortCondition)
    // 记录空头入场价格
    lastShortPrice := close
    // 重置最低价跟踪
    lowestSinceLastShort := low
    
    stopPrice := nz(highestSinceLastLong, close * 1.02)  // 使用前一个多头信号后的最高价作为止损
    float riskAmount = math.abs(stopPrice - close)
    targetPrice := close - (riskAmount * 3)  // 止盈为止损距离的2倍
    
    strategy.entry("做空", strategy.short)
    strategy.exit("空头止盈止损", "做空", limit=targetPrice, stop=stopPrice)

// === 绘制信号 ===
plotshape(longCondition, style=shape.triangleup, color=color.green, location=location.belowbar, size=size.small, title="做多信号")
plotshape(shortCondition, style=shape.triangledown, color=color.red, location=location.abovebar, size=size.small, title="做空信号")

// 绘制止损线
plot(strategy.position_size > 0 ? stopPrice : na, color=color.red, style=plot.style_linebr, linewidth=2, title="多头止损线")
plot(strategy.position_size < 0 ? stopPrice : na, color=color.red, style=plot.style_linebr, linewidth=2, title="空头止损线")

// 绘制止盈线
plot(strategy.position_size > 0 ? targetPrice : na, color=color.green, style=plot.style_linebr, linewidth=2, title="多头止盈线")
plot(strategy.position_size < 0 ? targetPrice : na, color=color.green, style=plot.style_linebr, linewidth=2, title="空头止盈线")
```

> Detail

https://www.fmz.com/strategy/477580

> Last Modified

2025-01-06 15:21:57
