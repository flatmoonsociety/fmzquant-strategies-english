
> Name

Trading strategy RSI-Candlestick-Trading-Strategy based on RSI and K-line patterns
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy combines the Relative Strength Index (RSI) indicator and the K-line pattern pattern. When the RSI reaches the overbought and oversold area, it identifies the specific K-line pattern as an entry signal to achieve trend tracking.
## Strategy Principle
1. Calculate the value of the RSI indicator, taking 30 as the oversold line and 70 as the overbought line.
2. When the RSI goes above 30, it is considered an oversold signal, and when the RSI goes below 70, it is considered an overbought signal.
3. When the above signal appears, determine whether the current K line or the previous K line forms a specific form such as a white/black entity, hammer head/hanging neck line, etc.
4. If the RSI signal and K-line pattern conditions are met at the same time, a buy/sell signal will be generated.
5. Correspondingly, if a long pattern is formed such as a hammer, buy when the RSI is oversold; if a short pattern is formed, such as a shooting star, sell when the RSI is overbought.
6. Identify more complex combination candlestick patterns such as double-line and triple-line forms as entry signals.
7. RSI going back through the midline also serves as a closing signal.
## Strategic Advantages
1. Combine indicators and patterns to filter out false signals and improve the accuracy of entry.
2. Identify K-line patterns and capture obvious trend turning points.
3. Use the overbought and oversold areas of RSI to send signals and increase profit opportunities.
4. Identify the combination of double and triple lines to seize the turning point of a strong trend.
5. RSI returns through the midline as a stop loss/take profit signal, which is beneficial to lock in profits.
## Strategy Risk
1. The RSI indicator lags behind and may miss the turning point.
2. Some K-line patterns have weak signals and may contain false signals.
3. The high point before the breakthrough and the low point before the backtest are not considered as stop loss and take profit signals, and there is a risk of loss.
4. If a trailing stop is not set, a sharp reversal may lead to an expansion of losses.
5. Insufficient backtest data may bias the parameter optimization results.
## Strategy optimization direction
1. Combine with other indicators to filter entry signals, such as MACD, Bollinger Bands, etc.
2. Add a trend line as a stop loss and take profit.
3. Optimize RSI parameters based on backtest results and find the best parameter combination.
4. Optimize stop-loss and stop-profit strategies, such as trailing stop loss, interval stop loss, etc.
5. Test data over a longer period of time to evaluate parameter stability.
6. Adjust parameters according to different varieties and market conditions.
## Summarize
This strategy integrates the advantages of RSI indicator and K-line pattern recognition, and selects high-quality signals to enter the market at overbought and oversold points to achieve the effect of trend following. At the same time, identifying some strong combination form signals can increase the probability of profit. However, there is a certain risk of lag and false signals, and it needs to be used in conjunction with other means and continued to be optimized. Generally speaking, this strategy integrates multiple bullish strategy ideas. If the parameters are tuned in place, it should be able to achieve better results.
||


## Overview

This strategy combines the Relative Strength Index (RSI) indicator with candlestick patterns to identify trend-following entry signals when RSI reaches overbought or oversold levels.

## How It Works

1. Calculate RSI values, with 70 as overbought line and 30 as oversold line.

2. View RSI crossing above 30 as oversold signal, and RSI crossing below 70 as overbought signal.

3. When above signals occur, check if the current or previous candle forms specific patterns like white/black marubozu, hammer/hanging man etc. 

4. If both RSI signal and candlestick condition are met, generate buy/sell signals.

5. Correspondingly, buy on oversold RSI when bullish patterns like hammer occur, and sell on overbought RSI when bearish patterns like shooting star occur.

6. Identify complex combination patterns like tweezer, morning/evening stars for entry signals.

7. RSI crossing midline acts as exit signal.

## Advantages

1. Combining indicator and pattern filters fake signals and improves entry accuracy.

2. Candlestick pattern captures significant trend reversal points. 

3. RSI overbought/oversold signals increase winning opportunities.

4. Double/Triple candlestick combos catch stronger reversals.

5. RSI cross midline helps lock in profits.

## Risks

1. RSI lag may miss reversal points. 

2. Some candlestick signals are weak and give false signals.

3. No stop loss based on recent high/low, risks uncontrolled loss.

4. No trailing stop loss, huge adverse move may enlarge loss.

5. Insufficient backtest data may bias parameter optimization.

## Optimization

1. Add other filters like MACD, Bollinger Bands.

2. Add trendline for stop loss/profit taking.

3. Optimize RSI parameters based on backtest results.

4. Enhance stops like trailing stop, zone stop etc.

5. Test longer datasets to evaluate parameter robustness. 

6. Adjust parameters for different products and market regimes.

## Conclusion

This strategy integrates the strengths of RSI and candlestick pattern recognition to enter on high quality signals at overbought/oversold turning points for trend-following. Strong combo patterns also improve odds. But risks like lag and false signals remain, requiring combination with other techniques and further optimization. Overall it blends multiple winning ideas and may achieve good results if properly parameterized.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|55|RSI Bullish Criteria|
|v_input_3|45|RSI Bearish Criteria|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-15 00:00:00
end: 2023-09-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

/////////////////////////////////////
//@version=2
//@author=sb
strategy("RSI-candlestick Strategy", overlay=true)
src = hlc3, len = input(14, minval=1, title="Length")
up = rma(max(change(src), 0), len)
down = rma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
//plot(rsi, color=purple)
//band1 = hline(70)
//band0 = hline(30)
//band2 = hline(50,linestyle=dotted,color=silver)
//fill(band1, band0, color=#cc99ff, transp=70)
//end premade RSI
oversold = rsi < 30
overbought = rsi > 70
barcolor(oversold? #7fff00 : overbought? red : na )
//
//
level_70 = 70
level_70rsi = rsi > level_70 ? rsi : level_70
level_30 = 30
level_30rsi = rsi < 30 ? rsi : level_30

level_50 = 50
//


//p1 = plot(series=level_70, color=red, linewidth=1, transp=100)
//p2 = plot(series=level_70rsi, color=red, linewidth=1, transp=100)
//p3 = plot(series=level_30, color=green, linewidth=1, transp=100)
//p4 = plot(series=level_30rsi, color=green, linewidth=1, transp=100)
//fill(p1, p2, color=red, transp=50)
//fill(p3, p4, color=#7fff00, transp=50)




/////////////////////////////////////


bullishcriteria = input(title="RSI Bullish Criteria",  defval=55, minval=50, maxval=100)
bearishcriteria = input(title="RSI Bearish Criteria",  defval=45, minval=0, maxval=50)

range = high - low
body = abs(close - open)
oc2 = min(close, open) + body/2
upperwick = high - max(open, close)
lowerwick = min(open, close) - low

isUp = close > open
isTrendUp = rsi(close, 14) >= bullishcriteria
isTrendDown = rsi(close, 14) <= bearishcriteria
isDoji = abs(close-open)/(high-low) < 0.05

// Single Candlestick Pattern
// white marubozu
wm = (isUp) and (upperwick <= 0.05*body) and (lowerwick <= 0.05*body) and isTrendDown
plotshape(wm, color=green, style=shape.triangleup, location=location.belowbar, title='white marubozu',text='wm')
if (not na(rsi))
    if (crossover(rsi, level_30) and (wm or wm[1]))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
// black marubozu
bm = (not isUp) and (upperwick <= 0.05*body) and (lowerwick <= 0.05*body) and isTrendUp
plotshape(bm, color=red, style=shape.triangledown, location=location.abovebar, title='black marubozu',text='bm')

if (not na(rsi))
    if (crossunder(rsi, level_70)and (bm or bm[1]))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
// hammer
h = (isUp) and (lowerwick >= 2*body) and (upperwick <= 0.1*body) and isTrendDown
plotshape(h, color=green, style=shape.triangleup, location=location.belowbar, title='hammer',text='h')

if (not na(rsi))
    if (crossover(rsi, level_30) and (h or h[1]))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
// hanging man
hm = (not isUp) and (lowerwick >= 2*body) and (upperwick <= 0.1*body) and isTrendUp
plotshape(hm, color=red, style=shape.triangledown, location=location.abovebar, title='hanging man',text='hm')

if (not na(rsi))
    if (crossunder(rsi, level_70)and (hm or hm[1]))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
        
// inverted hammer
ih = (isUp) and (upperwick >= 2*body) and (lowerwick <= 0.1*body) and isTrendDown
plotshape(ih, color=green, style=shape.triangleup, location=location.belowbar, title='inverted hammer',text='ih')

//if (not na(rsi))
//    if (crossover(rsi, level_30) and (ih or ih[1]))
//        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
        
// shooting star
ss = (not isUp) and (upperwick >= 2*body) and (lowerwick <= 0.1*body) and isTrendUp
plotshape(ss, color=red, style=shape.triangledown, location=location.abovebar, title='shooting star',text='ss')

if (not na(rsi))
    if (crossunder(rsi, level_70)and (ss or ss[1]))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
        
// Double Candlestick Pattern
// bullish engulfing
bulle = not isDoji[1] and (not isUp[1] and isUp) and (close > open[1] and open < close[1]) and isTrendDown
plotshape(bulle, color=green, style=shape.triangleup, location=location.belowbar, title='bullish engulfing', text='e')

// bearish engulfing
beare = not isDoji[1] and (isUp[1] and not isUp) and (open > close[1] and close < open[1]) and isTrendUp
plotshape(beare, color=red, style=shape.triangledown, location=location.abovebar, title='bearish engulfing',text='e')

// tweezer bottom
twb = (not isUp[1] and isUp) and (min(lowerwick,lowerwick[1])/max(lowerwick,lowerwick[1]) >= 0.99) and (min(low,low[1])/max(low,low[1]) >= 0.99) and isTrendDown
plotshape(twb, color=green, style=shape.triangleup, location=location.belowbar, title='tweezer bottom', text='tb')

if (not na(rsi))
    if (crossover(rsi, level_30) and (twb or twb[1]))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
        
// tweezer top
twt = (isUp[1] and not isUp) and (min(upperwick,upperwick[1])/max(upperwick,upperwick[1]) >= 0.99) and (min(high,high[1])/max(high,high[1]) >= 0.99) and isTrendUp
plotshape(twt, color=red, style=shape.triangledown, location=location.abovebar, title='tweezer top',text='tt')

if (not na(rsi))
    if (crossunder(rsi, level_70)and (twt or twt[1]))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
// Trible Candlestick Pattern
// three white soldier
tws = (not isUp[3] and isUp[2] and isUp[1] and isUp) and (body[1]>body[2]) and (upperwick<0.1*body and lowerwick<0.1*body) and isTrendDown
plotshape(tws, color=green, style=shape.triangleup, location=location.belowbar, title='three white soldiers',text='tws')

if (not na(rsi))
    if (crossover(rsi, level_30) and (tws or tws[1]))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
        
// three black crows
tbc = (isUp[3] and not isUp[2] and not isUp[1] and not isUp) and (body[1]>body[2]) and (upperwick<0.1*body and lowerwick<0.1*body) and isTrendUp
plotshape(tbc, color=red, style=shape.triangledown, location=location.abovebar, title='three black crows',text='tbc')

if (not na(rsi))
    if (crossunder(rsi, level_70)and (tbc or tbc[1]))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
        
// morning star
ms = (not isUp[1]) and (abs(close[1]-open[1])/(high[1]-low[1]) < 0.1) and (close > oc2[2] and close < open[2]) and isTrendDown
plotshape(ms, color=green, style=shape.triangleup, location=location.belowbar, title='morning star',text='ms')

if (not na(rsi))
    if (crossover(rsi, level_30) and (ms or ms[1]))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
        
// evening star
es = (isUp[1]) and (abs(close[1]-open[1])/(high[1]-low[1]) < 0.1) and (close < oc2[2] and close > open[2]) and isTrendUp
plotshape(es, color=red, style=shape.triangledown, location=location.abovebar, title='evening star',text='es')

//if (not na(rsi))
//    if (crossunder(rsi, level_70)and (es or es[1]))
//        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
        
// three inside up
tiu = (not isUp[2]) and (close[1] > oc2[2] and close[1] < open[2]) and (close > high[2]) and isTrendDown
plotshape(tiu, color=green, style=shape.triangleup, location=location.belowbar, title='three inside up',text='tiu')

if (not na(rsi))
    if (crossover(rsi, level_30) and (tiu or tiu[1]))
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
        
// three inside down
tid = (isUp[2]) and (close[1] < oc2[2] and close[1] > open[2]) and (close < low[2]) and isTrendUp
plotshape(tid, color=red, style=shape.triangledown, location=location.abovebar, title='three inside down',text='tid')

if (not na(rsi))
    if (crossunder(rsi, level_70)and (tid or tid[1]))
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")
        
if (not na(rsi))
    if (crossover(rsi, level_70))
        //strategy.exit("RsiSE")
        //if(chk[1]==0 or chk[2]==0 or chk[3]==0 or chk[4]==0 or chk[5]==0 or chk[6]==0 or chk[7]==0 or chk[8]==0 or chk[9]==0 or chk[10]==0)
        //if(crossover(col[1],zero) or crossover(col[2],zero) or crossover(col[3],zero) or crossover(col[4],zero) or crossover(col[5],zero) or crossover(col[6],zero) or crossover(col[7],zero) or crossover(col[8],zero))
        //strategy.entry("RsiLE", strategy.long,0, comment="RsiLE")
        strategy.entry("RsiSE", strategy.short,0, comment="RsiSE")

    if (crossunder(rsi, level_30))
        //strategy.entry("RsiSE", strategy.short,0, comment="RsiSE")
        strategy.entry("RsiLE", strategy.long,0, comment="RsiLE")

//if (not na(rsi))
//    if (crossover(rsi, level_50))
        //strategy.exit("RsiSE")
        //if(chk[1]==0 or chk[2]==0 or chk[3]==0 or chk[4]==0 or chk[5]==0 or chk[6]==0 or chk[7]==0 or chk[8]==0 or chk[9]==0 or chk[10]==0)
        //if(crossover(col[1],zero) or crossover(col[2],zero) or crossover(col[3],zero) or crossover(col[4],zero) or crossover(col[5],zero) or crossover(col[6],zero) or crossover(col[7],zero) or crossover(col[8],zero))
//        strategy.entry("RsiSE", strategy.short,0, comment="RsiSE")
//    else
//        strategy.exit("RsiSE")
//    if (crossunder(rsi, level_50))
//        strategy.entry("RsiLE", strategy.long,0, comment="RsiLE")
//    else
//        strategy.exit("RsiLE")
```

> Detail

https://www.fmz.com/strategy/427616

> Last Modified

2023-09-22 17:10:39
