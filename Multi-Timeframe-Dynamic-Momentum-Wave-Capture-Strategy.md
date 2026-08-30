
> Name

Multi-Timeframe-Dynamic-Momentum-Wave-Capture-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8d372270a1ea2e41bab.png)
![IMG](https://www.fmz.com/upload/asset/2d918d01a5ae5e95d6492.png)



[trans]

## Overview
The multi-period dynamic momentum fluctuation capturing strategy is a quantitative trading method designed for short-term traders to efficiently capture market fluctuations at the 2-minute level. This strategy cleverly combines moving average channels, momentum swing indicators and multi-period confirmation mechanisms to form a complete trading system. The core of the strategy is to use the price channel constructed by the 200 moving average to determine the direction of the market's general trend. At the same time, an improved version of the WaveTrend indicator is used to capture reversal opportunities in the overbought and oversold areas of the market, and the 12EMA is used as a precise entry signal filter. In addition, the strategy also integrates hourly level trend confirmation, dynamic stop loss setting and risk-based position management, forming a comprehensive and systematic trading framework.
#### Strategy Principle
The core principle of this strategy is based on multi-level signal confirmation and precise risk control. The specific implementation logic is as follows:
1. **Trend Judgment Layer**: The strategy uses the 200 moving average to apply to high prices and low prices to build a price channel, and combines the closing price of the hourly chart to determine the direction of the general trend. When the hourly closing price is above the channel, the system tends to go long; when the hourly closing price is below the channel, the system tends to go short.
2. **Momentum Wave Layer**: The strategy uses an improved version of the WaveTrend indicator to capture changes in market momentum. The WaveTrend indicator is calculated through the custom function `f_wavetrend`, which includes the fluctuation trend line (wt1) and the signal line (wt2). When the indicator reaches the overbought level (50) or the oversold level (-50), the system will record the extreme price and calculate the number of continuous overbought and oversold conditions.
3. **Entry confirmation layer**: The strategy combines multiple conditions to confirm the entry signal:
   - Long condition: hourly price is above the channel + (the oversold state continues for a specified number of bars or the WaveTrend indicator golden cross) + the current closing price is greater than 12EMA
   - Short selling conditions: The hourly price is below the channel + (the overbought state continues for a specified number of bars or the WaveTrend indicator crosses) + the current closing price is less than 12EMA
4. **Risk Management**: The strategy uses dynamic stops and risk-based position calculation methods:
   - The long stop loss is set to the smaller of the extreme low and the 200 low price moving average * 0.998
   - The short stop loss is set to the larger of the extreme high and the 200 high price moving average * 1.002
   - Position size is calculated by dividing the preset risk amount by the risk per unit (the difference between entry price and stop loss price)
5. **Profit Target**: The system automatically sets the profit target position based on the preset risk-reward ratio (default 3 times).
#### Strategic Advantages
1. **Multi-level confirmation mechanism**: The strategy integrates a multi-period and multi-indicator confirmation mechanism, significantly improving signal quality. Through the combination of hourly chart trend direction and short-period momentum indicators, false signals are effectively reduced.
2. **Dynamic Risk Management**: Compared with the fixed-point stop-loss setting, the dynamic stop-loss method of this strategy is more in line with the market structure. Through the combination of extreme points and moving averages, it provides a more reasonable risk boundary for each transaction.
3. **Accurate position control**: The strategy adopts a position calculation method based on a fixed risk amount, which can maintain consistent risk exposure regardless of changes in market volatility, effectively preventing excessive losses in a single transaction.
4. **Strong adaptability**: Through parametric design, the strategy can adapt to different market environments. Users can adjust parameters such as EMA length, overbought and oversold thresholds, risk amount, and risk-reward ratio to better adapt the strategy to specific markets.
5. **Visual assistance**: The strategy provides a wealth of visual elements, including moving average channels, momentum waveforms, trend background colors and entry marks, to help traders understand the market status and strategy logic more intuitively.
#### Strategy Risk
Although this strategy has multiple advantages, there are still potential risks:
1. **Trend mutation risk**: Although the strategy uses hourly trend confirmation, under the influence of major news or black swan events, the market may reverse sharply, causing the stop loss to be triggered quickly. The solution is to pause trading before important economic data or news releases, or to add additional volatility filters.
2. **Low liquidity risk**: In markets or periods with low trading volume, slippage may increase or transaction difficulties may occur, affecting strategy performance. It is recommended to use this strategy during main trading hours and avoid products with less market liquidity.
3. **Parameter optimization risk**: Over-optimizing parameters may cause the strategy to perform well in historical tests but have poor results in real trading. It is recommended to use forward validation method and robustness testing to evaluate the reliability of parameters and avoid overfitting.
4. **Continuous Loss Risk**: Although the strategy has strict risk control, you may still encounter continuous losses, especially in volatile markets. It is recommended to set limits on the maximum daily loss and the maximum number of consecutive losses, and suspend trading to re-evaluate the market environment when necessary.
5. **Technical dependence risk**: The strategy relies on technical indicators such as EMA and WaveTrend, which may fail under certain market conditions. Consider adding a fundamental filter or other non-correlated indicators to improve the robustness of your strategy.
#### Strategy optimization direction
Based on in-depth analysis of the strategy code, optimization can be made from the following aspects:
1. **Time filter introduction**: The current strategy does not consider trading time factors. You can add a time filter to avoid high volatility periods before the market opens and closes, or focus on specific efficient trading periods.
2. **Dynamic Parameter Adaptation**: The overbought and oversold thresholds and the number of confirmations can be automatically adjusted according to market volatility, allowing the strategy to maintain optimal performance in different market environments. For example, you can use the ATR indicator to adjust the threshold, raising the threshold in high-volatility markets and lowering the threshold in low-volatility markets.
3. **Multi-indicator comprehensive scoring**: In addition to the existing WaveTrend indicators, auxiliary indicators such as RSI, MACD or CCI can be introduced to establish a comprehensive scoring system. Trading signals will only be triggered when most indicators reach consensus.
4. **Dynamic adjustment of profit target**: The current strategy uses a fixed risk-reward ratio to set profit targets. Dynamic profit targets based on support, resistance levels or volatility can be considered to better adapt to the market structure.
5. **Partial Profit Mechanism**: Add a batch closing mechanism, lock in part of the profit after reaching a certain profit, and continue to hold the remaining positions to capture larger market trends, balancing the needs of risk control and profit maximization.
6. **Transaction cost optimization**: Transaction cost factors are not considered in the strategy. Slippage and commission settings can be added, and entry logic can be optimized to reduce unnecessary transaction frequency and improve net profit performance.
#### Summarize
The multi-period dynamic momentum fluctuation capturing strategy is a short-term trading system with a complete structure and clear logic. It provides traders with high-quality entry signals by combining moving average channels, momentum fluctuation indicators and multi-period confirmation mechanisms. The biggest feature of this strategy is its comprehensive risk management system, including dynamic stop loss setting and risk-based position control, which effectively ensures the safety of funds.
Although there are potential risks such as market mutations and parameter optimization, the robustness and adaptability of the strategy can be further improved by introducing optimization measures such as time filters, dynamic parameter adaptation, and multi-index comprehensive scoring. This strategy is particularly suitable for quantitative traders who pursue efficient short-term trading while focusing on risk control.
By setting parameters appropriately and continuously monitoring and optimizing, this strategy has the potential to become an important tool in traders' arsenal, helping them seize trading opportunities and achieve stable profits in rapidly volatile markets. ||
## Overview

The Multi-Timeframe Dynamic Momentum Wave Capture Strategy is a sophisticated quantitative trading approach designed for short-term traders operating on a 2-minute timeframe to efficiently capture market waves. This strategy ingeniously combines EMA channels, momentum wave indicators, and multi-timeframe confirmation mechanisms to form a comprehensive trading system. The core concept revolves around utilizing a 200 EMA-based price channel to determine the market's primary trend direction, while employing an enhanced WaveTrend indicator to capture reversal opportunities in overbought and oversold areas, with a 12 EMA serving as a precise entry signal filter. Additionally, the strategy integrates hourly trend confirmation, dynamic stop-loss settings, and risk-based position management to create a thorough and systematic trading framework.

#### Strategy Principles

The core principles of this strategy are based on multi-level signal confirmation and precise risk control, with specific implementation logic as follows:

1. **Trend Determination Layer**: The strategy applies the 200 EMA separately to high and low prices to construct a price channel, combined with hourly chart closing prices to determine the major trend direction. When the hourly closing price is above the channel, the system favors long positions; when the hourly closing price is below the channel, the system favors short positions.

2. **Momentum Wave Layer**: The strategy employs an enhanced WaveTrend indicator to capture market momentum changes. The WaveTrend indicator is calculated through a custom function `f_wavetrend`, which includes a wave trend line (wt1) and a signal line (wt2). When the indicator reaches overbought (50) or oversold (-50) levels, the system records extreme price values and counts the duration of overbought or oversold conditions.

3. **Entry Confirmation Layer**: The strategy combines multiple conditions to confirm entry signals:
   - Long condition: Hourly price above the channel + (Oversold condition persisting for a specified number of bars or WaveTrend indicator golden cross) + Current closing price greater than 12 EMA
   - Short condition: Hourly price below the channel + (Overbought condition persisting for a specified number of bars or WaveTrend indicator death cross) + Current closing price less than 12 EMA

4. **Risk Management Layer**: The strategy employs dynamic stop-losses and risk-based position calculation:
   - Long stop-loss is set at the smaller value between the extreme low point and 200 low price EMA*0.998
   - Short stop-loss is set at the larger value between the extreme high point and 200 high price EMA*1.002
   - Position size is calculated by dividing the preset risk amount by the per-unit risk (difference between entry price and stop-loss price)

5. **Profit Target**: The system automatically sets profit target levels based on a preset risk-reward ratio (default is 3x).

#### Strategy Advantages

1. **Multi-level Confirmation Mechanism**: The strategy integrates multi-timeframe, multi-indicator confirmation mechanisms, significantly improving signal quality. By combining hourly chart trend direction with short-term momentum indicators, false signals are effectively reduced.

2. **Dynamic Risk Management**: Compared to fixed-point stop-loss settings, this strategy's dynamic stop-loss method better aligns with market structure, providing more reasonable risk boundaries for each trade through the combination of extreme points and moving averages.

3. **Precise Position Control**: The strategy adopts a position calculation method based on fixed risk amounts, maintaining consistent risk exposure regardless of market volatility changes, effectively preventing excessive losses in individual trades.

4. **Strong Adaptability**: Through parametric design, the strategy can adapt to different market environments. Users can adjust EMA lengths, overbought/oversold thresholds, risk amounts, and risk-reward ratios to better suit specific markets.

5. **Visual Assistance**: The strategy provides rich visualization elements, including EMA channels, momentum waveforms, trend background colors, and entry markers, helping traders more intuitively understand market conditions and strategy logic.

#### Strategy Risks

Despite its multiple advantages, the strategy still has the following potential risks:

1. **Trend Reversal Risk**: Although the strategy uses hourly trend confirmation, markets may experience sharp reversals under major news or black swan events, causing stop-losses to be quickly triggered. The solution is to pause trading before important economic data or news releases, or to add additional volatility filters.

2. **Low Liquidity Risk**: In markets or time periods with lower trading volume, increased slippage or difficulty in execution may occur, affecting strategy performance. It is recommended to use this strategy during main trading sessions and avoid instruments with poor market liquidity.

3. **Parameter Optimization Risk**: Excessive parameter optimization may lead to a strategy that performs excellently in historical testing but poorly in live trading. Forward validation methods and robustness tests are recommended to assess parameter reliability and avoid overfitting.

4. **Consecutive Loss Risk**: Despite strict risk control, consecutive losses may still occur, especially in range-bound markets. It is advisable to set limits on maximum daily losses and maximum consecutive losing trades, pausing trading to reassess market conditions when necessary.

5. **Technical Dependency Risk**: The strategy relies on technical indicators such as EMA and WaveTrend, which may fail under certain market conditions. Consider adding fundamental filters or other non-correlated indicators to improve strategy robustness.

#### Strategy Optimization Directions

Based on in-depth analysis of the strategy code, optimization can be pursued in the following areas:

1. **Time Filter Introduction**: The current strategy does not consider trading time factors. Time filters could be added to avoid high volatility periods at market open and close, or to focus on specific efficient trading sessions.

2. **Dynamic Parameter Adaptation**: Overbought/oversold thresholds and confirmation bar counts could be automatically adjusted according to market volatility, maintaining optimal performance across different market environments. For example, ATR indicators could be used to adjust thresholds—raising them in high-volatility markets and lowering them in low-volatility markets.

3. **Multi-indicator Comprehensive Scoring**: Besides the existing WaveTrend indicator, auxiliary indicators such as RSI, MACD, or CCI could be introduced to establish a comprehensive scoring system, triggering trading signals only when multiple indicators reach consensus.

4. **Dynamic Profit Target Adjustment**: The current strategy uses a fixed risk-reward ratio to set profit targets. Consider dynamic profit targets based on support/resistance levels or volatility to better adapt to market structure.

5. **Partial Profit Mechanism**: Add a scaled exit mechanism to secure partial profits when reaching certain profitability levels, while holding remaining positions to capture larger movements, balancing risk control and profit maximization.

6. **Trading Cost Optimization**: The strategy does not account for trading costs. Adding slippage and commission settings and optimizing entry logic to reduce unnecessary trading frequency could improve net profit performance.

#### Summary

The Multi-Timeframe Dynamic Momentum Wave Capture Strategy is a well-structured, logically sound short-term trading system that provides traders with high-quality entry signals by combining EMA channels, momentum wave indicators, and multi-timeframe confirmation mechanisms. The strategy's greatest feature is its comprehensive risk management system, including dynamic stop-loss settings and risk-based position control, effectively safeguarding capital.

Despite potential risks such as market reversals and parameter optimization challenges, the strategy's robustness and adaptability can be further enhanced by introducing time filters, dynamic parameter adaptation, and multi-indicator comprehensive scoring systems. This strategy is particularly suitable for quantitative traders who pursue efficient short-term trading while emphasizing risk control.

With reasonable parameter settings and continuous monitoring and optimization, this strategy has the potential to become an important tool in a trader's arsenal, helping them capture trading opportunities in rapidly fluctuating markets and achieve stable profits.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-03-16 00:00:00
end: 2025-04-15 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Enhanced Momentum Wave Catcher", overlay=true,
  default_qty_type=strategy.cash,
  default_qty_value=10000,
  initial_capital=10000,
  currency="USD")

// Inputs
fastEmaLength = input.int(12, "12 EMA Length", minval=1)
slowEmaHighLength = input.int(200, "200 High EMA Length", minval=1)
slowEmaLowLength = input.int(200, "200 Low EMA Length", minval=1)
oversoldLevel = input.int(-50, "Oversold Level")
overboughtLevel = input.int(50, "Overbought Level")
riskAmount = input.float(100.0, "Risk Amount ($)", minval=1.0)
rrRatio = input.float(3.0, "Risk-Reward Ratio", minval=0.1)
confirmationBars = input.int(1, "Confirmation Bars After Extreme", minval=0)

// Calculate EMAs
fastEma = ta.ema(close, fastEmaLength)
slowEmaHigh = ta.ema(high, slowEmaHighLength)
slowEmaLow = ta.ema(low, slowEmaLowLength)

// Hourly close
hourlyClose = request.security(syminfo.tickerid, "60", close)

// Enhanced Momentum Wave Calculation
f_wavetrend(src, chlen, avg, malen) =>
    esa = ta.ema(src, chlen)
    de = ta.ema(math.abs(src - esa), chlen)
    ci = (src - esa) / (0.015 * de)
    wt1 = ta.ema(ci, avg)
    wt2 = ta.sma(wt1, malen)
    wtCrossUp = ta.crossover(wt1, wt2)
    wtCrossDown = ta.crossunder(wt1, wt2)
    [wt1, wt2, wtCrossUp, wtCrossDown]

[wt1, wt2, wtCrossUp, wtCrossDown] = f_wavetrend(hlc3, 9, 12, 3)

// Track extremes with improved detection
var int oversoldBars = 0
var int overboughtBars = 0
var float extremeLow = na
var float extremeHigh = na

// Enhanced extreme detection
if wt2 <= oversoldLevel
    oversoldBars := oversoldBars + 1
    extremeLow := na(extremeLow) ? low : math.min(low, extremeLow)
else
    oversoldBars := 0
    extremeLow := na

if wt2 >= overboughtLevel
    overboughtBars := overboughtBars + 1
    extremeHigh := na(extremeHigh) ? high : math.max(high, extremeHigh)
else
    overboughtBars := 0
    extremeHigh := na

// Hourly Channel Status
var bool hourlyAboveChannel = false
var bool hourlyBelowChannel = false

if barstate.isconfirmed
    if hourlyClose > slowEmaHigh
        hourlyAboveChannel := true
        hourlyBelowChannel := false
    else if hourlyClose < slowEmaLow
        hourlyAboveChannel := false
        hourlyBelowChannel := true

// Entry Conditions with improved wave detection
longCondition = hourlyAboveChannel and (oversoldBars > confirmationBars or wtCrossUp) and close > fastEma
shortCondition = hourlyBelowChannel and (overboughtBars > confirmationBars or wtCrossDown) and close < fastEma

// Dynamic Stops
longStop = math.min(extremeLow, slowEmaLow * 0.998)
shortStop = math.max(extremeHigh, slowEmaHigh * 1.002)

// Position Sizing
calculatePositionSize(entryPrice, stopPrice) =>
    riskPerUnit = math.abs(entryPrice - stopPrice)
    riskPerUnit > 0 ? riskAmount / riskPerUnit : na

// Execute Trades
if longCondition and not na(longStop)
    strategy.entry("Long", strategy.long, qty=calculatePositionSize(close, longStop))
    strategy.exit("Long Exit", "Long", stop=longStop, limit=close + (rrRatio * (close - longStop)))

if shortCondition and not na(shortStop)
    strategy.entry("Short", strategy.short, qty=calculatePositionSize(close, shortStop))
    strategy.exit("Short Exit", "Short", stop=shortStop, limit=close - (rrRatio * (shortStop - close)))

// Enhanced Visuals
plot(fastEma, "12 EMA", color=color.orange, linewidth=2)
plot(slowEmaHigh, "200 High EMA", color=color.red, linewidth=1)
plot(slowEmaLow, "200 Low EMA", color=color.green, linewidth=1)

// Wave visualization
plot(wt2, "Momentum Wave", color=#7E57C2, linewidth=2)
hline(oversoldLevel, "Oversold", color=color.red, linestyle=hline.style_dashed)
hline(overboughtLevel, "Overbought", color=color.green, linestyle=hline.style_dashed)

// Channel status
bgcolor(hourlyAboveChannel ? color.new(color.green, 90) : 
       hourlyBelowChannel ? color.new(color.red, 90) : 
       color.new(color.gray, 90))

// Entry markers
plotshape(longCondition, "Long Entry", style=shape.triangleup, 
         location=location.belowbar, color=color.green, size=size.small)
plotshape(shortCondition, "Short Entry", style=shape.triangledown, 
         location=location.abovebar, color=color.red, size=size.small)
```

> Detail

https://www.fmz.com/strategy/490787

> Last Modified

2025-04-16 14:53:29
