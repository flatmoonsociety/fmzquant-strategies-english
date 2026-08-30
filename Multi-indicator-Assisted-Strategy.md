
> Name

Multi-indicator-Assisted-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy comprehensively uses a variety of technical indicators such as EMA, RSI, MACD, energy tide, Bollinger Bands, etc. to judge the price trend from multiple angles and find a better entry point. At the same time, a variety of parameter setting combinations are provided for users to adjust to achieve personalized strategies.
## Strategy Principle
1. Use 3EMA (5 periods, 9 periods, 21 periods) to determine the price trend; EMA moving average crosses show trend changes.
2. The RSI indicator determines overbought and oversold conditions. If RSI is lower than the low point, it is an oversold signal, and if it is higher than the high point, it is an overbought signal.
3. The MACD indicator looks at the moving average difference. If DIFF breaks through DEA ​​upward, it is a bullish signal, and if DIFF breaks through DEA ​​downward, it is a bearish signal.
4. The energy tide indicator SAR displays the current trend direction and can assist in judgment.
5. The upper and lower rails of the Bollinger Bands show the support and pressure positions, and the price breaks through the upper and lower rails to indicate a trend change.
6. According to the user's choice, when the indicator sends a signal in the same direction, the corresponding buying and selling operations will be taken.
## Strategic Advantages
1. Comprehensive judgment of multiple indicators can avoid misleading by a single indicator.
2. Provide combination parameter adjustment, users can choose the best indicator combination according to their needs.
3. EMA, MACD and other indicators can accurately judge trend changes.
4. The RSI indicator can effectively identify overbought and oversold opportunities.
5. SAR and Bollinger Bands can show trend turning points in time.
## Strategy Risk
1. There are fewer opportunities to make judgments based on multiple indicator combinations, and better opportunities may be missed.
2. There is no way to filter when a single indicator sends an error signal.
3. Users may choose inappropriate parameter combinations, resulting in frequent or infrequent transactions.
4. There are no risk management measures such as STOP LOSS.
5. There is insufficient backtest data to fully verify the effectiveness of the strategy.
Corresponding solutions:
1. Adjust parameters and expand the indicator THRESHHOLD to provide more trading opportunities.
2. Add other indicators for combined verification to avoid false signals.
3. Provide more indicator choices to facilitate users to test the best combination.
4. Add stop-loss strategies and other measures to limit risks.
5. Historical backtesting in more markets to determine the best parameters.
## Strategy optimization direction
1. Test more indicator combinations to find the best matching indicator.
2. Add machine learning modules and use more data to improve strategies.
3. Add a trend filter to decide whether to trade based on the trend direction.
4. Optimize fund management strategies to adapt to more market environments.
5. Develop automatic parameter optimization programs to realize intelligent strategies.
## Summarize
This strategy uses a combination of multiple technical indicators to achieve a comprehensive judgment of price trends and avoid the shortcomings of relying on a single indicator. It can be further optimized by adjusting indicator parameters, adding verification modules, introducing AI, etc., so as to obtain more trading opportunities that are consistent with the strategy concept while maintaining the robustness of the strategy.
|| 

## Overview

This strategy combines EMA, RSI, MACD, PSAR, Bollinger Bands and other technical indicators for overall trend judgment from multiple angles, finding optimal entry opportunities. It provides multiple parameter setting options for adjustable personalized strategies.

## Strategy Logic

1. Use 3 EMAs (5-, 9-, 21-period) to determine price trend. EMA crossovers signal trend changes.

2. RSI judges overbought/oversold levels. RSI below lower level signifies oversold; above upper level overbought. 

3. MACD checks moving average difference. DIFF crossing above DEA is bullish signal and below is bearish.

4. PSAR indicates current trend direction for additional context.

5. Bollinger Bands show support/resistance levels. Price breaking bands suggests trend change.

6. Take long/short positions when indicators give aligned signals based on user selection.

## Advantages

1. Multiple indicators avoid misleading signals from single indicator.

2. Customizable parameters allow users to select optimal combinations.

3. Accurate trend change detection from EMA, MACD etc. 

4. RSI efficiently identifies oversold/overbought opportunities.

5. SAR and Bollinger Bands reveal turning points.

## Risks

1. Fewer multi-indicator signal occurrences may miss good opportunities.

2. No filtering when single indicator gives false signal.

3. Users may choose suboptimal parameter sets leading to over/undertrading.

4. No risk management limits like STOP LOSS. 

5. Insufficient backtest data to fully validate strategy.

Possible solutions:

1. Widen indicator thresholds to provide more signals.

2. Add other indicators to filter out false signals.

3. Provide more indicator options for users to test combinations. 

4. Incorporate stop loss and other risk management.

5. Backtest on more markets to optimize parameters.

## Optimization Directions

1. Test more indicator combinations to find best matches.

2. Add machine learning modules for more data-driven improvements.

3. Incorporate trend filtering to determine trade direction.

4. Optimize money management for more market environments.

5. Develop auto parameter optimization for intelligent improvements.

## Summary

This strategy applies multiple technical indicators for comprehensive trend analysis, avoiding overreliance on single indicators. It can be further enhanced via parameter tuning, adding validation modules, integrating AI etc, to provide more quality signals while maintaining robustness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Strategy: rsi|ema|macd|psr|off|BB|ema5|
|v_input_2|0|background color: rsi|ema|macd|psr|off|exchange|BB|ema5|
|v_input_3|false|Show ema5?|
|v_input_4|true|Show ema9?|
|v_input_5|true|Show ema21?|
|v_input_6|false|Show ema50?|
|v_input_7|false|Show ema100?|
|v_input_8|true|Show ema200|
|v_input_9|true|Color oversold and overbought bars?|
|v_input_10|true|Show Parabolic Sar|
|v_input_11|true|Show Bollinger Bands?|
|v_input_12|false|Show Daily Pivots?|
|v_input_13|true|linewidth|
|v_input_14|true|sar points width|
|v_input_15|40|oversold rsi|
|v_input_16|65|overbought rsi|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-17 00:00:00
end: 2023-09-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("f.society", title="f.society", overlay=true)
//@Author: rick#1414
// -----------------------------------------------------
// f.society : Pone 3EMA: 5, 9, 21, 50, 100, 200, SAR, 
// velas azules en sobreventa y velas moradas sobre compra 
// SAR 0.02, 0.02, 0.2 , Bandas de Bollinger
// estrategia de compra y venta con rsi, macd o psr
// color de fondo: ema, rsi (color azul sobreventa 35, 25 (mas intenso))
// -----------------------------------------------------
// Como agregar a Trading view:
// 1 Cerrar todos los otros indicadores antes de añadirlo
// 2. Ir a la página de inicio TradingView.com
// 3. En la parte inferior, haga clic en Editor Pine // ver imagen: // https://cdn.discordapp.com/attachments/407267549047422976/407393815112974336/unknown.png
// 4. borrar todo el texo y reemplazar con todo el contenido de este archivo
// 5. Pulse el botón "Añadir a trazar" (Add to graph)
// -----------------------------------------------------
// revisar opciones de on y off segun indicadores deseados
// https://cdn.discordapp.com/attachments/405885820114042883/412115277883506700/unknown.png
// se puede cambiar la estrategia desde este menu desplegable para señales buy/sell

// Options
estrategia = input(defval="rsi", title = "Strategy", options=["ema","rsi","macd","psr","off","BB","ema5"])
in_bkcolor = input(defval="rsi", title = "background color", options=["ema","rsi","macd","psr","off","exchange","BB","ema5"])
e5 = input(title="Show ema5?", type=bool, defval=false)
e9 = input(title="Show ema9?", type=bool, defval=true)
e21 = input(title="Show ema21?", type=bool, defval=true)
e50 = input(title="Show ema50?", type=bool, defval=false)
e100 = input(title="Show ema100?", type=bool, defval=false)
e200 = input(title="Show ema200", type=bool, defval=true)
in_rsi = input(title="Color oversold and overbought bars?", type=bool, defval=true)
in_sar = input(title="Show Parabolic Sar", type=bool, defval=true)
in_bb = input(title="Show Bollinger Bands?", type=bool, defval=true)
sd = input(false, title="Show Daily Pivots?")
linew = input(1, title="linewidth", minval=0)
sarw = input(1, title="sar points width", minval=0)
ovs = input(40, title="oversold rsi", minval=0)
ovb = input(65, title="overbought rsi", minval=0)



//pf = input(false,title="Show Filtered Pivots")
pf=false

// 3 ema
src = close // input(close, title="Source")
//len9 = input(9, minval=1, title="ema9 Length")
//len21 = input(21, minval=1, title="ema21 Length")
//len200 = input(200, minval=1, title="ema200 Length")
len5=5
len9=9
len21=21
len50=50
len100=100
len200=200
ema5 = ema(src, len5)
ema9 = ema(src, len9)
ema21 = ema(src, len21)
ema50= ema(src, len50)
ema100 = ema(src, len100)
ema200 = ema(src, len200)
plot(e5? ema5 : na, title="EMA5", linewidth=linew, color=purple)
plot(e9? ema9 : na, title="EMA9", linewidth=linew, color=blue)
plot(e21? ema21 : na, title="EMA21", linewidth=linew, color=red)
plot(e50? ema50 : na, title="EMA50", linewidth=linew, color=green)
plot(e100? ema100 : na, title="EMA100", linewidth=linew, color=lime)
plot(e200? ema200 : na, title="EMA200", linewidth=linew, color=yellow)

// RSI Color
//lenR = input(14, minval=1, title="RSI Length")
lenR=14
//up = rma(max(change(src), 0), lenR)
//down = rma(-min(change(src), 0), lenR)
//vrsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
vrsi=rsi(close,lenR)
//plot(vrsi,title="vrsi")
oversold = vrsi < ovs
overbought = vrsi > ovb
barcolor(in_rsi? oversold? #0000FF : overbought? #ff00ff:na : na)

// SAR
plot(in_sar? sar(0.02, 0.02, 0.2): na, style=cross, linewidth=sarw, color=blue, title="sar")

// BB
//length = input(20, title="Bollinger length", minval=1)
length=20
//mult = input(2.0, title="Bollinger stdDev", minval=0.001, maxval=50)
mult=2.0
basis = sma(src, length)
dev = mult * stdev(src, length)
upper = basis + dev
lower = basis - dev
plot(in_bb? basis :na, color=red, linewidth=linew, title="BB basis")
p1 = plot(in_bb? upper :na, color=blue, linewidth=linew, title="BB upper")
p2 = plot(in_bb? lower :na, color=blue, linewidth=linew, title="BB lower")
fill(p1, p2)

//background
bgcolor(in_bkcolor=="exchange"? #0000FF40 : in_bkcolor=="rsi"? vrsi < (ovs-15) ? #0000FF50  : vrsi < ovs ? #0000FF30 :( vrsi < ovb ? #ff00ff10 : #ff00ff20): in_bkcolor=="ema"?(ema9>ema21?#ff00ff10  : #0000FF20):in_bkcolor=="BB"?(lower>close?#ff00ff10 : close>upper?#0000FF20:#ff00ff10): in_bkcolor=="ema5"?(ema5>ema21?#ff00ff10  : #0000FF20):na)


// Strategy
if estrategia == "ema"
    strategy.entry("buy", true, 1, when= crossover(ema9,ema21) ),
    strategy.entry("sell", false, 1, when = crossover(ema21,ema9)) 
else
    if estrategia =="rsi"
        strategy.entry("buy", true, 1, when= vrsi <ovs),
        strategy.entry("sell", false, 1, when = vrsi > ovb or crossover(close,upper)) 
    else 
        if estrategia =="macd"    
            [macdLine, signalLine, histLine] = macd(close, 12, 26, 9),
            //bgcolor(macdLine > signalLine ? #98c8ff : #ff8b94),
            strategy.entry("buy", true, 1, when= macdLine>=signalLine ),
            strategy.entry("sell", false, 1, when = macdLine<signalLine) 
        else 
            if estrategia=="psr"
                leftBars = 4 //input(4)
                rightBars = 2 //input(2)
                swh = pivothigh(leftBars, rightBars)
                swl = pivotlow(leftBars, rightBars)
                swh_cond = not na(swh)
                hprice = 0.0
                hprice := swh_cond ? swh : hprice[1]
                le = false
                le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])
                if (le)
                    strategy.entry("buy", strategy.long, comment="buy", stop=hprice + syminfo.mintick)
                swl_cond = not na(swl)
                lprice = 0.0
                lprice := swl_cond ? swl : lprice[1]
                se = false
                se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])
                if (se)
                    strategy.entry("sell", strategy.short, comment="sell", stop=lprice - syminfo.mintick)
            else
                if estrategia=="BB"
                    strategy.entry("buy", true, 1, when= crossover(lower,close) ),
                    strategy.entry("sell", false, 1, when = crossover(close,upper)) 
                else
                    if estrategia=="ema5"
                        strategy.entry("buy", true, 1, when= crossover(ema5,ema21) ),
                        strategy.entry("sell", false, 1, when = crossover(ema21,ema5)) 



// pivots

// Classic Pivot
pivot = (high + low + close ) / 3.0
// Filter Cr
bull= pivot > (pivot + pivot[1]) / 2 + .0025
bear= pivot < (pivot + pivot[1]) / 2 - .0025
// Classic Pivots
r1 = pf and bear ? pivot + (pivot - low) : pf and bull ? pivot + (high - low) : pivot + (pivot - low)
s1 = pf and bull ? pivot - (high - pivot) : pf and bear ? pivot - (high - low) : pivot - (high - pivot)
r2 = pf ? na : pivot + (high - low)
s2 = pf ? na : pivot - (high - low)
//Pivot Average Calculation
smaP = sma(pivot, 3)
//Daily Pivots 
dtime_pivot = security(syminfo.tickerid, 'D', pivot[1])
dtime_pivotAvg = security(syminfo.tickerid, 'D', smaP[1])
dtime_r1 = security(syminfo.tickerid, 'D', r1[1]) 
dtime_s1 = security(syminfo.tickerid, 'D', s1[1]) 
dtime_r2 = security(syminfo.tickerid, 'D', r2[1]) 
dtime_s2 = security(syminfo.tickerid, 'D', s2[1])
offs_daily = 0
plot(sd and dtime_pivot ? dtime_pivot : na, title="Daily Pivot",style=line, color=fuchsia,linewidth=linew) 
plot(sd and dtime_r1 ? dtime_r1 : na, title="Daily R1",style=line, color=#DC143C,linewidth=linew) 
plot(sd and dtime_s1 ? dtime_s1 : na, title="Daily S1",style=line, color=lime,linewidth=linew) 
plot(sd and dtime_r2 ? dtime_r2 : na, title="Daily R2",style=line, color=maroon,linewidth=linew) 
plot(sd and dtime_s2 ? dtime_s2 : na, title="Daily S2",style=line, color=#228B22,linewidth=linew) 


// References:
// get number of bars since last green bar
//plot(barssince(close >= open), linewidth=3, color=blue)
//bgcolor(close < open ? #ff8b94   : #98c8ff , transp=10)
//http://www.color-hex.com/
//   #98c8ff    light blue
//    #ff8b94   red   #b21c0e
//       #7d1d90    purple
//    #0029ff blue
//    #fffa86   yellow
```

> Detail

https://www.fmz.com/strategy/427731

> Last Modified

2023-09-24 13:17:50
