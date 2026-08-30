
> Name

Z-Score-Momentum-Trading-System-with-ATR-Stop-Loss-and-Risk-Reward-Optimization
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8a83fb86f74136e2eb3.png)
![IMG](https://www.fmz.com/upload/asset/2d927ec64154f02eb0b85.png)




[trans]
#### Overview
This strategy is a complete trading system that combines multiple technical indicators, mainly based on Z-score to measure outliers in trading volume and K-line body size, and uses ATR (Average True Range) to set dynamic stop loss levels. The system also integrates risk-return ratio (RR) to optimize profit targets and provides reliable trading signals through multi-dimensional technical analysis.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Z-score analysis: Calculate trading volume and the standard deviation of K-line entities to identify abnormal market activity
2. Trend confirmation: Confirm the trend direction by analyzing the high, low and closing prices of adjacent K lines
3. ATR stop loss: Use dynamic ATR value to set stop loss position to provide more flexible risk control
4. Risk-return ratio: automatically calculate the profit target based on the set RR ratio
5. Visual Markers: Mark trading signals and key price levels on charts
#### Strategic Advantages
1. Multi-dimensional signal confirmation: combine trading volume, price momentum and trend direction to improve the reliability of trading signals
2. Dynamic risk management: realize adaptive stop loss through ATR, and better adapt to market fluctuations
3. Flexible parameter configuration: allows adjustment of Z-score threshold, ATR multiple and risk-benefit ratio
4. Precise entry timing: Use Z-score outliers to identify key trading opportunities
5. Clear visualization: Entry points, stop loss levels and profit targets are clearly marked on the chart
#### Strategy Risk
1. Parameter sensitivity: The settings of Z-score threshold and ATR multiple directly affect transaction frequency and risk control
2. Dependence on market environment: fewer trading signals may be generated in a low volatility environment
3. Computational complexity: Multiple indicator calculations may cause signal generation delays
4. Slippage risk: In fast markets, you may face deviations between the actual execution price and the signal price.
5. False breakthrough risk: False breakthrough signals may be triggered in a consolidating market
#### Strategy optimization direction
1. Market environment filtering: Add market volatility filter to dynamically adjust parameters under different market environments
2. Signal confirmation mechanism: Introduce more technical indicators for cross-validation, such as RSI or MACD
3. Position management optimization: dynamic position adjustment based on volatility and account risk
4. Multi-time period analysis: Integrate trend confirmation of higher time periods to improve transaction success rate
5. Signal filtering optimization: add additional filtering conditions to reduce false signals
#### Summary
This strategy builds a complete trading system by combining Z-score analysis, ATR stop loss, and risk-reward ratio optimization. The advantage of the system lies in multi-dimensional signal confirmation and flexible risk management, but it is still necessary to pay attention to the impact of parameter settings and market environment. Through the suggested optimization directions, the strategy can further improve its stability and adaptability. ||
#### Overview
This strategy is a comprehensive trading system that combines multiple technical indicators, primarily based on Z-score to measure volume and candlestick body size anomalies, while using ATR (Average True Range) for dynamic stop-loss placement. The system also integrates Risk-Reward Ratio (RR) for profit target optimization and provides reliable trading signals through multi-dimensional technical analysis.

#### Strategy Principles
The core logic of the strategy is based on several key components:
1. Z-score Analysis: Calculates standard deviations of trading volume and candlestick bodies to identify market activity anomalies
2. Trend Confirmation: Analyzes adjacent candlestick highs/lows and closing prices to confirm trend direction
3. ATR Stop-Loss: Uses dynamic ATR values for stop-loss placement, providing flexible risk control
4. Risk-Reward Ratio: Automatically calculates profit targets based on the set RR ratio
5. Visual Markers: Indicates trading signals and key price levels on the chart

#### Strategy Advantages
1. Multi-dimensional Signal Confirmation: Combines volume, price momentum, and trend direction for improved signal reliability
2. Dynamic Risk Management: Implements adaptive stop-loss through ATR, better accommodating market volatility
3. Flexible Parameter Configuration: Allows adjustment of Z-score thresholds, ATR multiplier, and risk-reward ratio
4. Precise Entry Timing: Uses Z-score anomalies to identify key trading opportunities
5. Clear Visualization: Clearly marks entry points, stop-loss levels, and profit targets on the chart

#### Strategy Risks
1. Parameter Sensitivity: Z-score thresholds and ATR multiplier settings directly affect trading frequency and risk control
2. Market Environment Dependency: May generate fewer signals in low-volatility environments
3. Computational Complexity: Multiple indicator calculations may lead to signal generation delays
4. Slippage Risk: May face execution price discrepancies from signal prices in fast markets
5. False Breakout Risk: Potential for triggering incorrect breakout signals in ranging markets

#### Strategy Optimization Directions
1. Market Environment Filtering: Add volatility filters to dynamically adjust parameters in different market conditions
2. Signal Confirmation Mechanism: Introduce additional technical indicators for cross-validation, such as RSI or MACD
3. Position Management Optimization: Implement dynamic position sizing based on volatility and account risk
4. Multiple Timeframe Analysis: Integrate higher timeframe trend confirmation to improve trade success rate
5. Signal Filtering Enhancement: Add additional filtering conditions to reduce false signals

#### Summary
This strategy builds a complete trading system by combining Z-score analysis, ATR stop-loss, and risk-reward optimization. The system's strengths lie in its multi-dimensional signal confirmation and flexible risk management, while attention must be paid to parameter settings and market environment impacts. Through the suggested optimization directions, the strategy can further enhance its stability and adaptability.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-01 00:00:00
end: 2025-02-18 08:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("admbrk | Candle Color & Price Alarm with ATR Stop", overlay=true, initial_capital=50, default_qty_type=strategy.cash, default_qty_value=200, commission_type=strategy.commission.percent, commission_value=0.05, pyramiding=3)

// **Risk/Reward ratio (RR) as input**
rr = input.float(2.0, title="Risk/Reward Ratio (RR)", step=0.1)

// **Z-score calculation function**
f_zscore(src, len) =>
    mean = ta.sma(src, len)     
    std = ta.stdev(src, len)
    (src - mean) / std

// **Z-score calculations**
len = input(20, "Z-Score MA Length")
z1 = input.float(1.5, "Threshold z1", step=0.1)
z2 = input.float(2.5, "Threshold z2", step=0.1)

z_volume = f_zscore(volume, len)
z_body = f_zscore(math.abs(close - open), len)

i_src = input.string("Volume", title="Source", options=["Volume", "Body size", "Any", "All"])

float z = na
if i_src == "Volume"
    z := z_volume
else if i_src == "Body size"
    z := z_body
else if i_src == "Any"
    z := math.max(z_volume, z_body)
else if i_src == "All"
    z := math.min(z_volume, z_body)

// **Determine trend direction**
green = close >= open
red = close < open

// **Long and Short signals**
longSignal = barstate.isconfirmed and red[1] and low < low[1] and green
shortSignal = barstate.isconfirmed and green[1] and high > high[1] and red

long = longSignal and (z >= z1)
short = shortSignal and (z >= z1)

// **ATR calculation (for ATR Stop)**
atrLength = input.int(14, title="ATR Length")
atrMultiplier = input.float(1.5, title="ATR Stop Multiplier")
atrValue = ta.atr(atrLength)

// **ATR-based stop-loss calculation**
long_atr_stop = close - atrValue * atrMultiplier
short_atr_stop = close + atrValue * atrMultiplier

// **Stop-loss setting (set to the lowest/highest wick of the last two bars)**
long_sl = ta.lowest(low, 2)  // Long stop-loss (lowest of the last 2 bars)
short_sl = ta.highest(high, 2) // Short stop-loss (highest of the last 2 bars)

// **Take-profit calculation (with RR)**
long_tp = close + (close - long_sl) * rr
short_tp = close - (short_sl - close) * rr

triggerAlarm(symbol)=>
    status = close
    var string message = na
    alarmMessageJSON = syminfo.ticker + message +"\\n" + "Price: " + str.tostring(status) 
    
if long
    // Open Long position
    strategy.entry("Long", strategy.long)
    strategy.exit("Long Exit", from_entry="Long", stop=math.max(long_sl, long_atr_stop), limit=long_tp)
    

if short
    // Open Short position
    strategy.entry("Short", strategy.short)
    strategy.exit("Short Exit", from_entry="Short", stop=math.min(short_sl, short_atr_stop), limit=short_tp)
    

// **Coloring the candles (BUY = Green, SELL = Red)**
barcolor(long ? color.green : short ? color.red : na)

// **Add entry/exit markers on the chart**
plotshape(long, title="BUY Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small, text="BUY")
plotshape(short, title="SELL Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small, text="SELL")

// **Plot TP and SL markers on exits**
exitLong = strategy.position_size < strategy.position_size[1] and strategy.position_size[1] > 0
exitShort = strategy.position_size > strategy.position_size[1] and strategy.position_size[1] < 0

plotshape(exitLong, title="Long Exit", location=location.abovebar, color=color.blue, style=shape.labeldown, size=size.tiny, text="TP/SL")
plotshape(exitShort, title="Short Exit", location=location.belowbar, color=color.orange, style=shape.labelup, size=size.tiny, text="TP/SL")

// **Add alerts**
alertcondition(long, title="Long Signal", message="Long signal triggered!")
alertcondition(short, title="Short Signal", message="Short signal triggered!")

```

> Detail

https://www.fmz.com/strategy/482829

> Last Modified

2025-02-27 17:41:05
