
> Name

Dual-Moving-Average-Intelligent-Tracking-Trading-Strategy based on Dual-Moving-Average-Intelligent-Tracking-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16cd6e895ad50f0be6e.png)
[trans]
## Overview
The dual moving average intelligent tracking trading strategy is a trend following strategy based on moving averages and specific indicators. This strategy uses two moving averages with different parameter settings to build a channel, and combines the OTT indicator to set the upper and lower limits of the channel to achieve intelligent tracking of price trends. When the price breaks out of the channel, buy or sell.
## Strategy Principle
This strategy mainly uses two moving averages and OTT indicators to build adaptive channels. The specific principles are as follows:
1. Calculate the fast line MAvg, taking the CLOSE closing price and the custom moving average as input, and the length is 5;
2. Based on MAvg and the set percentage, calculate the upper and lower limits of the channel, the long stop position of the long line and the short stop position of the short line;
3. Calculate the channel moving stop loss MT in the OTT indicator, and calculate the channel price OTT based on the long and short status;
4. When the price breaks through OTT, a trading signal is generated.
The above process of building an adaptive channel allows the strategy to track price changes in real time and generate trading signals.
## Strategic Advantages
This strategy has the following advantages:
1. The double moving average channel structure can effectively capture the price trend;
2. OTT indicator sets channel moving stop to control risks;
3. Adaptive channel structure can quickly respond to price changes;
4. The strategy parameter settings are flexible and can be optimized for different varieties and cycles.
## Strategy Risk
There are also some risks with this strategy:
1. Double moving averages are prone to divergence and may produce false signals;
2. Improper OTT parameter settings may be too aggressive or conservative, affecting strategy performance;
3. The strategy is only based on technical indicators and does not combine fundamental factors.
In response to the above risks, improvements and optimizations can be made through parameter optimization, combined with other indicators or fundamental filtering signals, etc.
## Strategy optimization direction
This strategy can be optimized from the following directions:
1. Optimize the moving average parameters and select a parameter combination suitable for the variety and period;
2. Optimize channel bandwidth parameters and balance tracking sensitivity and stability;
3. Filter signals based on trading volume;
4. Set trading direction filters based on fundamental conditions.
## Summarize
Generally speaking, this strategy is a trend tracking strategy based on dual moving average channels and OTT indicators. The core idea is to build an adaptive channel and use breakthroughs to generate trading signals. This strategy has certain advantages, but there is also room for possible improvement. Through parameter and rule optimization, this strategy can become an efficient quantitative trading strategy worthy of real-time verification.
||

## Overview  

The dual moving average intelligent tracking trading strategy is a trend following strategy based on moving averages and specific indicators. The strategy uses two moving averages with different parameter settings to build a channel and combines the OTT indicator to set the upper and lower limits of the channel to intelligently track price trends. When prices break through the channel, buy or sell operations are executed.

## Strategy Principle

The core methodology of this strategy is to construct an adaptive channel using two moving averages and the OTT indicator, specifically:

1. Calculate the fast line MAvg using CLOSE and custom moving average as input, with a length of 5 periods;  

2. Calculate the long line position LongStop and short line position ShortStop for the channel based on MAvg and preset percentage;

3. Calculate the channel stop loss MT in OTT indicator, and channel price OTT based on long/short direction;  

4. Generate trading signals when price breaks through OTT.

The above process enables real-time tracking of price trend changes, generating trading signals.

## Strategy Advantages

The advantages of this strategy include:

1. The dual moving average channel structure effectively captures price trends; 
2. OTT indicator sets channel stop loss to control risks;
3. Adaptive channel structure responds quickly to price changes;  
4. Flexible parameter tuning for different products and timeframes.

## Strategy Risks

There are also some risks:   

1. Dual moving averages can form divergence resulting in false signals;  
2. Improper OTT parameter settings may be too aggressive or conservative; 
3. The strategy relies solely on technical indicators without considering fundamentals.

Risks can be addressed through parameter optimization, integrating other indicators and fundamentals filters.

## Optimization Directions

The strategy can be optimized in several aspects:

1. Optimize moving average parameters for proper product and timeframes;
2. Optimize channel width parameters balancing sensitivity and stability;
3. Add filters based on trading volume;  
4. Set direction filters based on fundamentals.

## Summary

In summary, this is a trend following strategy based on a dual moving average channel and OTT indicator. The core idea is constructing an adaptive channel and generating signals when prices breakout. The strategy has merits but also room for improvements. With parameter tuning and logic optimization, it has the potential to become an efficient quant trading strategy worth deploying.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Period|
|v_input_2|true|Sihirli Yüzde|
|v_input_3|0|Hareketli Ortalama Türü: VAR|EMA|WMA|TMA|SMA|WWMA|ZLEMA|TSF|
|v_input_4|10|Kanal Periyodu|
|v_input_5|21|Averaj Uzunluğu|
|v_input_6|20200101|Başlangıç Tarihi (YYYYMMDD)|
|v_input_7|20201231|Bitiş Tarihi (YYYYMMDD)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-11 00:00:00
end: 2024-02-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="BugRA_Trade_Strategy", shorttitle="BugRA_Trade_Strategy", overlay=true)

// Kullanıcı Girdileri
length = input(5, title="Period", minval=1)
percent = input(1, title="Sihirli Yüzde", type=input.float, step=0.1, minval=0)
mav = input(title="Hareketli Ortalama Türü", defval="VAR", options=["SMA", "EMA", "WMA", "TMA", "VAR", "WWMA", "ZLEMA", "TSF"])
wt_n1 = input(10, title="Kanal Periyodu")
wt_n2 = input(21, title="Averaj Uzunluğu")
src = close

// Tarih Aralığı Girdileri
startDate = input(20200101, title="Başlangıç Tarihi (YYYYMMDD)")
endDate = input(20201231, title="Bitiş Tarihi (YYYYMMDD)")

// Tarih Filtresi Fonksiyonu
isDateInRange() => true

// Özel Fonksiyonlar
Var_Func(src, length) =>
    valpha = 2 / (length + 1)
    vud1 = src > src[1] ? src - src[1] : 0
    vdd1 = src < src[1] ? src[1] - src : 0
    vUD = sum(vud1, length)
    vDD = sum(vdd1, length)
    vCMO = (vUD - vDD) / (vUD + vDD)
    varResult = 0.0
    varResult := nz(valpha * abs(vCMO) * src + (1 - valpha * abs(vCMO)) * nz(varResult[1]))
    varResult

Wwma_Func(src, length) =>
    wwalpha = 1 / length
    wwma = 0.0
    wwma := wwalpha * src + (1 - wwalpha) * nz(wwma[1])
    wwma

Zlema_Func(src, length) =>
    zxLag = floor(length / 2)
    zxEMAData = src + (src - src[zxLag])
    zlema = ema(zxEMAData, length)
    zlema

Tsf_Func(src, length) =>
    lrc = linreg(src, length, 0)
    lrs = lrc - linreg(src, length, 1)
    tsf = lrc + lrs
    tsf

getMA(src, length) =>
    ma = mav == "SMA" ? sma(src, length) :
         mav == "EMA" ? ema(src, length) :
         mav == "WMA" ? wma(src, length) :
         mav == "TMA" ? sma(sma(src, ceil(length / 2)), floor(length / 2) + 1) :
         mav == "VAR" ? Var_Func(src, length) :
         mav == "WWMA" ? Wwma_Func(src, length) :
         mav == "ZLEMA" ? Zlema_Func(src, length) :
         mav == "TSF" ? Tsf_Func(src, length) : na

// Strateji Hesaplamaları
MAvg = getMA(src, length)
fark = MAvg * percent * 0.01
longStop = MAvg - fark
longStopPrev = nz(longStop[1], longStop)
longStop := MAvg > longStopPrev ? max(longStop, longStopPrev) : longStop
shortStop = MAvg + fark
shortStopPrev = nz(shortStop[1], shortStop)
shortStop := MAvg < shortStopPrev ? min(shortStop, shortStopPrev) : shortStop

dir = 1
dir := nz(dir[1], dir)
dir := dir == -1 and MAvg > shortStopPrev ? 1 : dir == 1 and MAvg < longStopPrev ? -1 : dir
MT = dir==1 ? longStop: shortStop
OTT = MAvg > MT ? MT*(200+percent)/200 : MT*(200-percent)/200

plot(OTT, title="BugRA", color=color.rgb(251, 126, 9))

// Alım ve Satım Koşulları
longCondition = crossover(src, OTT) and isDateInRange()
shortCondition = crossunder(src, OTT) and isDateInRange()

// Strateji Giriş ve Çıkış Emirleri
if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.close("Long")

```

> Detail

https://www.fmz.com/strategy/442010

> Last Modified

2024-02-18 15:58:08
