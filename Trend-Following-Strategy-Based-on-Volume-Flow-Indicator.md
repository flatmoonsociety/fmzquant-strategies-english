
> Name

Trend-Following-Strategy-Based-on-Volume-Flow-Indicator
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy implements trend following trading based on the Volume Indicator (VFI). The strategy determines the direction of market trends by calculating stock price fluctuations and changes in trading volume, and enables buying low and selling high.
### Strategy Principles
1. Calculate the VFI indicator: Calculate the VFI value based on the logarithmic change of the stock price and trading volume, and eliminate shocks through smoothing.
2. Determine the trend direction: when the VFI indicator crosses the 0 axis above, it is a bullish signal, and when it crosses below the 0 axis, it is a bearish signal.
3. Trading signal: Go long when the fast EMA crosses above the slow EMA, and VFI crosses above the buy line; close the position when VFI crosses below the sell line.
4. Stop loss method: Set a fixed stop loss ratio.
This strategy mainly relies on the VFI indicator to determine the trend direction and cooperates with the moving average system to issue trading signals. The VFI indicator reflects market sentiment through stock price fluctuations and trading volume changes, and is a trend tracking indicator. Compared with a single price indicator, the VFI indicator has more comprehensive judgments and can better identify trend turning points and filter shocks.
### Strategic Advantages
1. The VFI indicator is better than a single price indicator in judging trends and can effectively filter out market shocks and false breakthroughs.
2. The moving average system assists judgment and prevents the VFI indicator from sending wrong signals in a volatile market.
3. Set fixed stop loss points to control risks and facilitate risk management.
4. Using the trend following mode, there is no need to guess the market turning point, just follow the trend to obtain excess returns.
5. Parameter settings are flexible and parameters can be adjusted according to the market to adapt to different cycles and varieties.
### Strategy Risk
1. In a volatile market, the VFI indicator may send out wrong signals.
2. The fixed stop loss point may be too large or too small, resulting in premature stop loss or too late stop loss.
3. If the buying and selling parameters are set improperly, it may lead to frequent transactions or missing orders.
4. The trend following strategy cannot catch the reversal and needs to stop losses in time.
5. Improper parameters may lead to entering the market too early or too late.
### Strategy optimization
1. Adjust VFI parameters and optimize index calculation.
2. Adjust the moving average period and optimize the timing of signaling.
3. Dynamically adjust stop loss points and optimize stop loss methods.
4. Combine with other filtering indicators to improve signal quality.
5. Optimize parameter combinations for large periods and small periods respectively.
6. Test the robustness of parameters of different varieties and improve parameter adaptability.
### Summarize
This strategy determines the trend direction based on the VFI indicator and works with the moving average system to filter error signals. Buy low and sell high through trend following without predicting specific reversal points. The advantage of the strategy is that it is better to judge the trend than a single price indicator and can effectively filter out shocks. The main risk is that a volatile market could send out wrong signals. By adjusting parameters and adding other indicators to assist, the stability of the strategy can be improved. Generally speaking, this strategy is based on the VFI indicator and can become a reliable trend following strategy after optimizing parameters and stop loss.
||


### Overview

This strategy implements trend following trading based on Volume Flow Indicator (VFI). It judges the market trend direction by calculating price fluctuations and volume changes, and realizes low buying and high selling.

### Strategy Principle 

1. Calculate VFI indicator: Compute VFI value based on logarithmic price change and volume, and smooth out oscillations through smoothing techniques.

2. Determine trend direction: VFI crossing above 0 is a bullish signal, while crossing below 0 is a bearish signal.  

3. Trading signals: Go long when fast EMA crosses above slow EMA and VFI crosses above buy line; close position when VFI crosses below sell line.

4. Stop loss: Set fixed stop loss percentage.

This strategy mainly relies on VFI to determine the trend direction, combined with moving averages to generate trading signals. VFI reflects market sentiment through price volatility and volume changes, making it a trend following indicator. Compared with single price indicators, VFI provides more comprehensive judgments and identifies trend reversal points better, filtering out consolidations.

### Advantages

1. VFI determines trends better than single price indicators, effectively filtering out consolidations and false breakouts.

2. Moving averages provide supplementary judgements, avoiding incorrect signals from VFI in ranging markets.

3. Fixed stop loss controls risk and facilitates risk management.

4. Trend following mode generates excess returns without predicting reversals.

5. Flexible parameter tuning adapts to different periods and products.

### Risks

1. VFI may generate incorrect signals during significant fluctuations. 

2. Fixed stop loss could be too wide or too narrow.

3. Ill-configured entry and exit settings lead to over-trading or missing trades.

4. Trend following fails to capture reversals and needs timely stop loss. 

5. Improper parameters cause premature or delayed entry.

### Enhancements

1. Optimize VFI calculation by adjusting parameters.

2. Fine-tune moving average periods for better signal timing.

3. Employ dynamic stop loss instead of fixed one.

4. Add other indicators to filter signals.

5. Optimize parameters separately based on timeframe. 

6. Test robustness across different products.

### Conclusion

This strategy determines the trend direction with VFI and uses moving averages to filter out wrong signals. It realizes low buying/high selling through trend following without predicting reversals. The advantage lies in its superior trend detection over single price indicators and ability to filter out consolidations. The main risk is generating incorrect signals during fluctuations. Optimizing parameters, adding supplementary indicators and stop loss techniques can improve its stability. Overall, with parameter tuning and stop loss optimizations, this VFI based strategy can become a reliable trend following system.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|8|Length|
|v_input_2|0.2|Coef|
|v_input_3|2.5|Volume Cutoff|
|v_input_4|3|Smoothing Period|
|v_input_5|0|Smoothing Type: EMA|ALMA|SMA|WMA|
|v_input_6|-4|Buy Line|
|v_input_7|5|Sell Line|
|v_input_8|5|Stop Loss%|
|v_input_9|200|Long EMA|
|v_input_10|50|short EMA1|
|v_input_11|9|short EM2A|
|v_input_12|false|Visualize Trend|
|v_input_13|true|Apply Filling|
|v_input_14|true|Show Moving Average|
|v_input_15|0|Moving Average Type: SMA|EMA|ALMA|WMA|
|v_input_16|30|Moving Average Length|
|v_input_17|0.85|• ALMA - Offset (global setting)|
|v_input_18|6|• ALMA - Sigma (global setting)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-02 00:00:00
end: 2023-10-06 21:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mohanee
//This strategy is based on VFI indicator published by  UTS.  
//more details of VFI indicator can be found at  [url=http://mkatsanos.com/VFI.html]http://mkatsanos.com/VFI.html[/url] 
// I have added buy line and sell line to the indicator  and tested  SPY stock/index on one hour chart

//@version=4
strategy(title="VFI  strategy [based on VFI indicator published by  UTS]", overlay=false,pyramiding=2, default_qty_type=strategy.fixed,    initial_capital=10000, currency=currency.USD)


// Const
kMaColor = color.aqua
kNeutralColor = color.gray
kBearColor = color.red
kBullColor = color.green

kAlma = "ALMA"
kEma = "EMA"
kSma = "SMA"
kWma = "WMA"


// Input

vfi_length = input(8, title="Length", minval=1)  //default 130
vfi_coef = input(0.2, title="Coef", minval=0.1)
vfi_volCutoff = input(2.5, title="Volume Cutoff", minval=0.1)
vfi_smoothLen = input(3, title="Smoothing Period", minval=1)
vfi_smoothType = input(kEma, title="Smoothing Type", options=[kAlma, kEma, kSma, kWma])

//These are adde by me for the strategy purpose  BEGIN
vfi_buyLine = input(-4, title="Buy Line", minval=-10)
vfi_sellLine = input(5, title="Sell Line", minval=-10)
stopLoss = input(title="Stop Loss%", defval=5, minval=1)
//These are adde by me for the strategy purpose  END

vfi_longEMA = input(200, title="Long EMA", minval=1)
vfi_shortEMA1 = input(50, title="short EMA1", minval=1)
vfi_shortEMA2 = input(9, title="short EM2A", minval=1)

vfi_showTrend = input(false, title="Visualize Trend")
vfi_showFill = input(true, title="Apply Filling")
vfi_showMa = input(true, title="Show Moving Average")
vfi_maType = input(kSma, title="Moving Average Type", options=[kAlma, kEma, kSma, kWma])
vfi_maLength = input(30, title="Moving Average Length", minval=1)
vfi_almaOffset = input(0.85, title="• ALMA - Offset (global setting)", minval=0.0, maxval=1.0, step=0.05) // more smoothness (closer to 1) vs. more responsiveness (closer to 0)
vfi_almaSigma = input(6.0, title="• ALMA - Sigma (global setting)", minval=0.0, step=0.05) // the larger sigma the smoother ALMA


// Functionality

isRising(sig) =>
    sig > sig[1]
    
isFlat(sig) =>
    sig == sig[1]

vfi_trendColor(sig) =>
    isFlat(sig) ? kNeutralColor : isRising(sig) ? kBullColor : kBearColor
    
vfi_color(sig) =>
    isFlat(sig) ? kNeutralColor : sig > 0 ? kBullColor : kBearColor
    
osc_color(sig) =>
    sig == 0 ? kNeutralColor : sig > 0 ? kBullColor : kBearColor

smooth(t, sig, len) =>
    ma = float(sig)         // None
    if t == kSma            // Simple
        ma := sma(sig, len)
    if t == kEma            // Exponential
        ma := ema(sig, len)
    if t == kWma            // Weighted
        ma := wma(sig, len)
    if t == kAlma           // Arnaud Legoux
        ma := alma(sig, len, vfi_almaOffset, vfi_almaSigma)
    ma

calc_vfi(fviPeriod, smoothType, smoothLen, coef, vCoef) =>
    avg = nz(hlc3)
    inter = log(avg) - log(avg[1])
    vInter = stdev(inter, 30)
    cutOff = coef * vInter * close
    vAve = smooth(kSma, volume[1], fviPeriod)
    vMax = vAve * vCoef
    vC = min(volume, vMax)
    mf = avg - avg[1]
    vCp = iff(mf > cutOff, vC, iff(mf < -cutOff, -vC, 0))
    sVfi = sum(vCp, fviPeriod) / vAve
    vfi = smooth(smoothType, sVfi, smoothLen)
    
value_vfi = calc_vfi(vfi_length, vfi_smoothType, vfi_smoothLen, vfi_coef, vfi_volCutoff)
value_ma = smooth(vfi_maType, value_vfi, vfi_maLength)

longEMAval= ema(close, vfi_longEMA)
shortEMAval1= ema(close, vfi_shortEMA1)
shortEMAval2= ema(close, vfi_shortEMA2)

color_vfi = vfi_showTrend ? vfi_trendColor(value_vfi) : vfi_color(value_vfi)
color_osc = vfi_showFill ? osc_color(value_vfi) : na
color_ma = vfi_showMa ? kMaColor : na


// Drawings

plot_vfi = plot(value_vfi, title="VFI", color=color_vfi, linewidth=1)
plot_fill = plot(0, color=color_vfi, editable=false)
fill(plot_vfi, plot_fill, title="Oscillator Fill", color=color_osc, transp=75) 
hline(vfi_buyLine, color=color.green, title="Buy Line", linewidth=2, linestyle=hline.style_dashed)
hline(vfi_sellLine, color=color.purple, title="Sell Line", linewidth=2, linestyle=hline.style_dashed)
plot(value_ma, title="MA", color=color_ma, linewidth=2)

strategy.entry(id="VFI LE", long=true,  when=crossover(value_vfi,vfi_buyLine)  and ( shortEMAval1 >= longEMAval  ))

//strategy.close(id="VFI LE", comment="Exit",   when=crossunder(value_vfi,vfi_sellLine))
strategy.close(id="VFI LE", comment="TP Exit",   when=crossunder(value_vfi,vfi_sellLine) and close>strategy.position_avg_price)
//strategy.close(id="VFI LE", comment="Exit",   when=  (shortEMAval1 > shortEMAval2 )  and crossunder(close, shortEMAval2))

//stoploss
stopLossVal =   strategy.position_avg_price -  (strategy.position_avg_price*stopLoss*0.01) 
strategy.close(id="VFI LE", comment="SL Exit",   when=crossunder(value_vfi,vfi_sellLine) and close < stopLossVal)



```

> Detail

https://www.fmz.com/strategy/428887

> Last Modified

2023-10-10 14:51:13
