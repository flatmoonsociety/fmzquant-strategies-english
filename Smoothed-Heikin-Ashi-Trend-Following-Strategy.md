
> Name

Trend following strategy based on smoothed oscillator Smoothed-Heikin-Ashi-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/125f998bbb33dbf8404.png)
[trans]

## Overview
This strategy is based on smoothed oscillators to identify price trends and uses a trend following approach to trade. Go long when the price breaks above the indicator line and go short when the price falls below the indicator line.
## Strategy Principle
This strategy uses a custom smoothed oscillator to identify price trends. The indicator calculates the reversal closing price of the current K line, that is, the theoretical price that can reverse the profit and loss and the color of the trajectory chart. The reversal closing price is then smoothed to obtain the final smoothed oscillator line. When the price is higher (lower) than the indicator line, it means that the market is in an upward (downward) trend.
The strategy uses a breakthrough of the indicator line as a signal to open a position. Go long when the price breaks through the indicator line and go short when the price falls below the indicator line. The stop loss line is set to a certain percentage of the entry price to lock in profits and control risk.
## Strategic Advantages
1. Use custom indicators to identify trends and achieve better backtest performance
2. Use trend tracking, which is roughly in line with quantitative trend trading theory
3. Setting stop loss is beneficial to risk control
## Risk Analysis
1. There is a certain degree of backtracking in the indicator, which may lead to poor strategy performance.
2. Based only on a single indicator, it is easy to generate wrong signals
3. There is room for optimization in stop loss settings, and excessive stop loss may occur.
## Optimization direction
1. Consider combining other indicators to filter trading signals, such as Bollinger Bands, RSI, etc.
2. Test different indicator parameter settings
3. Test and optimize stop loss methods
4. More data testing different varieties and cycles
## Summarize
The overall idea of ​​this strategy is clear, using custom indicators to identify trends and trading in a trend-following manner. Judging from the backtest results, the strategy performed well and has certain potential for real-time application. However, it only relies on a single indicator and there is a certain amount of backtracking, so the signal quality still needs to be verified. In addition, the stop-loss mechanism also needs further testing and optimization. Overall, the strategy concept is feasible, but more work needs to be done to improve the ability to use real offers.
|| 

## Overview

This strategy identifies price trends using a custom smoothed oscillator indicator and trades based on trend following principles. It goes long when price breaks above the indicator line and goes short when price breaks below the line. 

## Strategy Logic

The strategy employs a custom smoothed oscillator that computes the reverse close price required to flip the Heikin Ashi candle color from red to green and vice versa. This reverse close is then smoothed using moving averages to obtain the final oscillator line. Price trading above (below) the line signals an uptrend (downtrend).

The strategy enters trades based on breakouts of the indicator line. Long trades are initiated when price breaks above the line while short trades are initiated on breakdowns below the line. Stop losses are set at a fixed percentage from the entry price to lock in profits and control risk.

## Advantages

1. Custom indicator identifies trends with good backtest results 
2. Trend following approach aligns with quantitative theories
3. Stop loss implementation promotes risk management

## Risks

1. Potential for repainting leading to poor live performance
2. Reliance on a single indicator risks bad signals  
3. Stop loss setting requires further optimization 

## Enhancement Opportunities

1. Incorporate additional filters like Bollinger Bands, RSI etc. 
2. Test different indicator parameters
3. Optimize stop loss placement  
4. More testing across instruments and timeframes

## Conclusion

The strategy demonstrates a clear trend following approach using a custom oscillator indicator. Backtest results are encouraging, indicating potential for live trading. However sole dependence on one repainting indicator and lack of signal quality verification are concerns. Stop loss mechanics also require additional testing and tuning. Overall the strategy concept looks feasible but more work is needed to make it reliably deployable for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Use smoothing Heikin Ashi|
|v_input_string_1|0|Method: SMA|EMA|HMA|VWMA|RMA|
|v_input_2|10|Smoothing period|
|v_input_3|true|Show Info Box|
|v_input_4|2|Prices Decimal Places|
|v_input_5|5|Info Box Offset|
|v_input_6|false|Repaint -  Keep on for live / Off for backtest|
|v_input_float_1|true|Long Stop Loss (%)|
|v_input_float_2|true|Short Stop Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-19 00:00:00
end: 2023-12-26 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/

// © TraderHalai
// This is a backtest of the Smoothed Heikin Ashi Trend indicator, which computes the reverse candle close price required to flip a heikin ashi trend from red to green and vice versa. Original indicator can be found on the scripts section of my profile.

// Default testing parameters are 10% of equity position size, with a 1% stop loss on short and long strategy.opentrades.commission

// This particular back test uses this indicator as a Trend trading tool with a tight stop loss. The equity curve as tested seems promising but requires further work to refine. Note in an actual trading setup, you may wish to use this with volatilty filters as most of the losses are in sideways, low volatility markets.


//@version=5
strategy("Smoothed Heikin Ashi Trend on Chart - TraderHalai BACKTEST", " SHA Trend - BACKTEST", overlay=true)
//Inputs

i_useSmooth =       input ( true, "Use smoothing Heikin Ashi")
i_smoothingMethod = input.string("SMA", "Method", options=["SMA", "EMA", "HMA", "VWMA", "RMA"])
i_smoothingPeriod = input ( 10, "Smoothing period")

i_infoBox   =       input ( true, "Show Info Box"        )
i_decimalP  =       input ( 2,    "Prices Decimal Places") 
i_boxOffSet =       input ( 5,    "Info Box Offset"      )
i_repaint   =       input (false,  "Repaint -  Keep on for live / Off for backtest")

i_longLossPerc = input.float(title="Long Stop Loss (%)",minval=0.0, step=0.1, defval=1) * 0.01

i_shortLossPerc = input.float(title="Short Stop Loss (%)", minval=0.0, step=0.1, defval=1) * 0.01


timeperiod = timeframe.period

//Security functions to avoid repaint, as per PineCoders
f_secureSecurity(_symbol, _res, _src) => request.security(_symbol, _res, _src[1], lookahead = barmerge.lookahead_on)
f_security(_symbol, _res, _src, _repaint) => request.security(_symbol, _res, _src[_repaint ? 0 : barstate.isrealtime ? 1 : 0])[_repaint ? 0 : barstate.isrealtime ? 0 : 1]
f_secSecurity2(_symbol, _res, _src) => request.security(_symbol, _res, _src[1])


candleClose = f_security(syminfo.tickerid, timeperiod, close, i_repaint)
candleOpen = f_security(syminfo.tickerid, timeperiod, open, i_repaint)
candleLow = f_security(syminfo.tickerid, timeperiod, low, i_repaint)
candleHigh = f_security(syminfo.tickerid, timeperiod, high, i_repaint)

haTicker = ticker.heikinashi(syminfo.tickerid)
haClose = f_security(haTicker, timeperiod, close, i_repaint)
haOpen = f_security(haTicker, timeperiod, open, i_repaint)
haLow = f_security(haTicker, timeperiod, low, i_repaint)
haHigh= f_security(haTicker, timeperiod, high, i_repaint)


reverseClose = (2 * (haOpen[1] + haClose[1])) - candleHigh - candleLow - candleOpen

if(reverseClose < candleLow)
    reverseClose := (candleLow + reverseClose) / 2

if(reverseClose > candleHigh)
    reverseClose := (candleHigh + reverseClose) / 2
    
//Smoothing
    
smaSmoothed = ta.sma(reverseClose, i_smoothingPeriod)
emaSmoothed = ta.ema(reverseClose, i_smoothingPeriod)
hmaSmoothed = ta.hma(reverseClose, i_smoothingPeriod)
vwmaSmoothed = ta.vwma(reverseClose, i_smoothingPeriod)
rmaSmoothed = ta.rma(reverseClose, i_smoothingPeriod)

shouldApplySmoothing = i_useSmooth and i_smoothingPeriod > 1 

smoothedReverseClose = reverseClose

if(shouldApplySmoothing)
    if(i_smoothingMethod == "SMA")
        smoothedReverseClose := smaSmoothed
    else if(i_smoothingMethod == "EMA")
        smoothedReverseClose := emaSmoothed
    else if(i_smoothingMethod == "HMA")
        smoothedReverseClose := hmaSmoothed
    else if(i_smoothingMethod == "VWMA")
        smoothedReverseClose := vwmaSmoothed
    else if(i_smoothingMethod == "RMA")
        smoothedReverseClose := rmaSmoothed
    else 
        smoothedReverseClose := reverseClose // Default to non-smoothed for invalid smoothing type
    
haBull = candleClose >= smoothedReverseClose
haCol = haBull ? color.green : color.red


//Overall trading strategy
if(ta.crossover(candleClose, smoothedReverseClose))
    strategy.entry("LONG", strategy.long, stop=smoothedReverseClose)
else
    strategy.cancel("LONG")

if(ta.crossunder(candleClose, smoothedReverseClose))
    strategy.entry("SHORT", strategy.short, stop=smoothedReverseClose)
else
    strategy.cancel("SHORT")
    

longStopPrice  = strategy.position_avg_price * (1 - i_longLossPerc)
shortStopPrice = strategy.position_avg_price * (1 + i_shortLossPerc)



plot(series=(strategy.position_size > 0) ? longStopPrice : na,
     color=color.red, style=plot.style_cross,
     linewidth=2, title="Long Stop Loss")
plot(series=(strategy.position_size < 0) ? shortStopPrice : na,
     color=color.red, style=plot.style_cross,
     linewidth=2, title="Short Stop Loss")
     
plot(smoothedReverseClose, color=haCol)

if (strategy.position_size > 0)
    strategy.exit(id="XL STP", stop=longStopPrice)

if (strategy.position_size < 0)
    strategy.exit(id="XS STP", stop=shortStopPrice)

```

> Detail

https://www.fmz.com/strategy/436768

> Last Modified

2023-12-27 15:41:37
