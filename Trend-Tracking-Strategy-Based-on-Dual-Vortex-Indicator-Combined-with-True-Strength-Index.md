
> Name

Trend-Tracking-Strategy-Based-on-Dual-Vortex-Indicator-Combined-with-True-Strength-Index
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fc0165ddf6ed7ba2d3.png)
[trans]

## Overview
The name of this strategy is "Trend following strategy of double vortex indicator combined with true strength indicator". This strategy uses the double vortex indicator and the true strength indicator simultaneously to open long and short positions when they send out buy and sell signals, and close the position and exit after a certain band to capture the medium and long-term trend.
## Strategy Principle
This strategy uses both the Double Vortex indicator and the True Strength indicator. The Double Vortex indicator consists of two lines, VI+ and VI-, which reflect the strength of rising and falling prices. The True Strength Indicator includes the TSI Red Line and TSI Blue Line, which measure the strength and direction of price changes.
When the VI+ uptrend strengthens and the VI- downtrend weakens, the Double Swirl indicator will issue a long signal. At this time, if the TSI blue line also crosses the red line, the real strength indicator will also send a long signal. When both indicators send out long signals at the same time, open a long position.
On the contrary, when the VI+ uptrend weakens and the VI- downtrend strengthens, the Double Swirl indicator will issue a short signal. At this time, if the TSI blue line also crosses below the red line, the true strength indicator will also send a short signal. When both indicators send out short signals at the same time, a short position is opened.
With this combination, you can open a position when the mid- to long-term trend begins to establish and follow that trend. When the trend ends, the indicator will also send a signal to close the position. Therefore, this strategy can effectively capture the medium and long-term general trend of prices.
## Strategic advantage analysis
This strategy mainly has the following advantages:
1. Dual indicator filtering can enhance the reliability of signals and avoid false signals.
2. Using medium and long-term indicators can track larger market trends. Short-term indicators are easily disturbed by market noise and miss the general trend.
3. Through parameter adjustment, the position holding time of the strategy can be flexibly adjusted. It allows the strategy to track trends while also controlling single profits and losses.
4. Consider both trend tracking and risk control. Indicators can effectively identify trends and control risks by setting exit bands.

## Strategy risk analysis
There are also some risks with this strategy:
1. Medium and long-term positions are prone to stop losses in volatile market conditions. You can shorten the exit band appropriately or adjust the stop loss to deal with it.
2. The probability of false signals may still occur in dual indicator combinations. Other indicators can be introduced for confirmation, or parameters can be adjusted.
3. The efficiency is low, and funds are occupied during the medium and long-term holding period. Position size can be appropriately adjusted to optimize capital utilization efficiency.
4. Need to rely on trend conditions. In volatile market conditions, position size should be reduced to avoid deadweight losses.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Adding other indicator combinations to form multiple indicator filters can further improve signal quality.
2. Optimize parameter settings to make indicator parameters more consistent with the characteristics of different varieties.
3. Add a dynamic position management mechanism to increase positions in trending markets and reduce positions in volatile markets.
4. Add stop-loss strategies to control risks through trailing stop-loss, shrinking stop-loss, etc.
5. Combined with wave theory, identify larger-level potential trend directions as direction filtering conditions.
6. Use machine learning methods to automatically optimize parameters and trading rules, making the strategy more adaptive and adaptive.
## Summarize
This strategy is generally an excellent medium and long-term trend following strategy. It uses the double vortex indicator and the true strength indicator to give full play to their respective technical advantages, verify each other's signals, and can effectively identify the generation of medium and long-term price trends. Through appropriate parameter adjustment, the risk of a single transaction can be controlled. If optimized in conjunction with more other technical indicators and risk control methods, this strategy can achieve even better results. It is suitable for investors interested in mid- to long-term trend trading.
|| 

# Overview  

This strategy is named "Trend Tracking Strategy Based on Dual Vortex Indicator Combined with True Strength Index". It opens long and short positions when the dual vortex indicator and true strength index issue buy and sell signals, and closes positions after a certain price movement to capture medium- to long-term trends.  

## Strategy Logic  

This strategy uses both the dual vortex indicator and the true strength index (TSI). The dual vortex indicator consists of VI+ and VI- lines, reflecting the magnitude of upward and downward momentum respectively. The TSI has red and blue lines measuring the strength and direction of price changes.  

When VI+ rises and VI- falls, indicating strengthening uptrend and weakening downtrend momentum, the dual vortex indicator generates a long signal. If at the same time, the TSI blue line crosses above the red line, TSI also issues a long signal. The strategy will open a long position when both indicators give out long signals simultaneously.  

Conversely, when VI+ falls and VI- rises, signaling weakening upside momentum and strengthening downside momentum, the dual vortex gives out a short signal. If the TSI blue line crosses below the red line as well, the TSI produces a short signal too. The strategy then opens a short position upon receiving aligned short signals.  

By combining signals from both indicators this way, the strategy is able to identify and track nascent medium- to long-term trends. Exit signals are generated when the trends end. Thus, this strategy can effectively capture large trend-following moves in the market.

## Advantage Analysis  

The main advantages of this strategy include:

1. The dual indicator filter improves signal reliability and avoids false signals.  
2. Adopting medium- to long-term indicators allows catching larger trends. Short-term signals tend to be disturbed by market noise.  
3. Flexible adjustment of holding period through parameter tuning. This allows both trend tracking and single trade risk control.
4. Balancing trend following and risk management. Indicators identify trends well. Risk is controlled by setting exit price waves.

## Risk Analysis   

Some risks also exist:

1. Medium- to long-term holding may face whipsaw price actions for stop loss. This can be mitigated by reducing exit wave period or adjusting stop loss properly.  
2. Probability of false signals still exists despite the dual indicator filter. Additional indicator confirmation or parameter tuning helps.
3. Relatively low capital usage efficiency because capital is held for longer holding periods. Position sizing could be adjusted to optimize fund utilization.  
4. Reliance on trending markets. Position sizes should be reduced in range-bound markets to avoid unnecessary losses.

## Optimization Directions

Some ways to optimize the strategy include:  

1. Introducing more indicator combos to strengthen signal quality via multiple filtering.
2. Optimizing parameters to suit different products' characteristics better.  
3. Adding dynamic position sizing to extend positions in trending while reducing sizes in ranging markets.
4. Incorporating stop loss mechanisms like trailing stop loss and partial close stop loss to control risks.
5. Combining Elliott Wave analysis to identify larger degree trends as directional filter.
6. Utilizing machine learning to auto-optimize parameters and rules for enhanced adaptiveness.  

## Conclusion   

In summary, this strategy is an excellent medium- to long-term trend following approach. By leveraging the techniques of dual vortex indicator and TSI, it can recognize emerging mid- to long-term trends reliably. With proper parameter tuning, per trade risks can be managed. Further optimizations by incorporating more indicators and risk control techniques would lead to improved performance. It suits investors interested in mid- to long-term trend trading.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|Long Length|
|v_input_2|13|Short Length|
|v_input_3|13|Signal Length|
|v_input_4|14|Period|
|v_input_5|true|Close after x bar|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-11 00:00:00
end: 2023-12-11 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © hydrelev

//@version=4
strategy("Vortex TSI strategy", overlay=false)
///////////////////INDICATOR TSI
long = input(title="Long Length", type=input.integer, defval=25)
short = input(title="Short Length", type=input.integer, defval=13)
signal = input(title="Signal Length", type=input.integer, defval=13)
price = close
double_smooth(src, long, short) =>
    fist_smooth = ema(src, long)
    ema(fist_smooth, short)
pc = change(price)
double_smoothed_pc = double_smooth(pc, long, short)
double_smoothed_abs_pc = double_smooth(abs(pc), long, short)
tsi_blue = 100 * (double_smoothed_pc / double_smoothed_abs_pc)
tsi_red = ema(tsi_blue, signal)
// plot(tsi_blue, color=#3BB3E4)
// plot(tsi_red, color=#FF006E)
// hline(0, title="Zero")

/////////////////INDICATOR VI
period_ = input(14, title="Period", minval=2)
VMP = sum( abs( high - low[1]), period_ )
VMM = sum( abs( low - high[1]), period_ )
STR = sum( atr(1), period_ )
VIP_blue = VMP / STR
VIM_red = VMM / STR
// plot(VIP_blue, title="VI +", color=#3BB3E4)
// plot(VIM_red, title="VI -", color=#FF006E)

////////////////////STRATEGY
bar=input(1, title="Close after x bar", minval=1, maxval=50)

tsi_long = crossover(tsi_blue, tsi_red)
tsi_short = crossunder(tsi_blue, tsi_red)
vi_long = crossover(VIP_blue, VIM_red)
vi_short = crossunder(VIP_blue, VIM_red)

LongConditionOpen = tsi_long and vi_long ? true : false
LongConditionClose = tsi_long[bar] and vi_long[bar] ? true : false
ShortConditionOpen = tsi_short and vi_short ? true : false
ShortConditionClose = tsi_short[bar] and vi_short[bar] ? true : false

if (LongConditionOpen)
    strategy.entry("Long Entry", strategy.long)
if (LongConditionClose)
    strategy.close("Long Entry")

if (ShortConditionOpen)
    strategy.entry("Short Entry", strategy.short)
if (ShortConditionClose)
    strategy.close("Short Entry")
```

> Detail

https://www.fmz.com/strategy/435143

> Last Modified

2023-12-12 16:23:10
