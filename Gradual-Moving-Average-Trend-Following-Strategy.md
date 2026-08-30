
> Name

Gradual-Moving-Average-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12e6ebd68be3a809e98.png)

[trans]

## Overview
The gradient moving average trend following strategy uses a variety of moving averages of different periods to capture trend changes in prices, supplemented by oscillator indicators to determine overbought and oversold areas, to achieve a trend following trading strategy of buying low and selling high. This strategy is suitable for medium and long-term positions and tracking obvious trend markets.
## Strategy Principle
This strategy uses multiple sets of moving averages such as 18-period, 26-period, and 36-period to capture price trends. When the short-term moving average crosses the long-term moving average, it is considered to be in an upward trend, so go long; when the short-term moving average crosses below the long-term moving average, it is considered to be in a downward trend, so go short.
At the same time, the strategy also uses oscillator indicators such as MACD, RSI, and EFI to determine overbought and oversold areas. For example, if the MACD column line turns from negative to positive, go long, and from positive to negative, go short; go short when RSI falls from a high level, and go long when it rebounds from a low level; go long when the EFI indicator is less than 0, and go short when it is greater than 0.
Entry rules:
Long order: The short moving average crosses the long moving average AND MACD>0 AND RSI rebounds from a low level AND EFI<0
Short order: The short moving average crosses the long moving average AND MACD<0 AND RSI falls back from highs AND EFI>0
Stop loss rules:
Stop loss for long orders: EFI indicator is greater than the threshold AND the price falls below the specified moving average
Stop loss for short orders: EFI indicator is less than the threshold AND the price rises above the specified moving average
## Strategic Advantages
1. Using multiple sets of moving averages to capture trends, nonlinearity meetings one has to be inclusive robustness and anti-fragility are key characteristics that help ensure resilience over time to capture major trend change points.
2. Use a combination of oscillator indicators to determine overbought and oversold areas to avoid chasing highs and selling lows.
3. Stop-loss rules comprehensively consider trends and capital flows to effectively control risks.
4. The strategy parameters have been optimized through repeated backtesting and can be adapted to most market environments.
5. The operating frequency is moderate and the trading signals are relatively stable, enabling long-term holding and tracking trends.
## Risk Analysis
1. A sharp drop caused by an unexpected event may cause the stop-loss effect, and the stop-loss range should be appropriately increased.
2. The trading frequency may be too high in volatile market conditions. Parameters should be adjusted appropriately to reduce the trading frequency.
3. Holding a position for too long may lead to an expansion of losses. The moving average period should be appropriately shortened and losses should be stopped in a timely manner.
4. There is a risk of over-fitting during backtesting, and the actual effect needs to be tested.
## Optimization direction
1. Optimize transaction frequency and income and find the best parameter combination.
2. Add machine learning algorithms to dynamically optimize parameters and adapt to market changes.
3. Add an adaptive stop loss mechanism and use different stop loss ranges for different market conditions.
4. Combine more indicators to determine the timing of entry and improve the stability of the strategy.
5. Add fund management strategies, control the size of single positions, and manage overall risks.
## Summarize
The gradient moving average trend tracking strategy uses multiple moving averages to determine the trend direction and combines indicators to filter entry opportunities. It can effectively track the general trend and achieve the purpose of stable returns for long-term holdings. The strategy has achieved certain stability through parameter optimization, but the risk control and adaptive mechanisms still need to be further improved to reduce retracement and improve the winning rate. Overall, as a simple and practical trend tracking solution, this strategy has strong scalability as its core concept and is worthy of further research.
||


## Overview

The Gradual Moving Average Trend Following Strategy uses multiple moving averages of different periods to capture price trend changes, combined with oscillator indicators to determine overbought and oversold areas, forming a low-buying and high-selling trend following trading strategy. This strategy is suitable for medium-to-long term holding positions to track significant trending markets.

## Strategy Logic

The strategy employs multiple sets of moving averages, like 18-, 26-, 36-period MAs, to capture price trends. When shorter MAs cross above longer MAs, it signals an upward trend, thus going long. When shorter MAs cross below longer MAs, it indicates a downward trend, thus going short.

Meanwhile, oscillator indicators like MACD, RSI, EFI are used to identify overbought and oversold conditions. For example, MACD turning from negative to positive suggests going long, while turning from positive to negative suggests going short. RSI retreating from high levels is a signal for shorting, while rebounding from low levels is a signal for going long. EFI below 0 means going long, while above 0 means going short.

Entry rules:

Long: Short MA crossover up Long MA AND MACD>0 AND RSI rebounds from lows AND EFI<0  

Short: Short MA crossover down Long MA AND MACD<0 AND RSI retreats from highs AND EFI>0

Stop loss rules: 

Long SL: EFI above threshold AND price breaks below specified MA  

Short SL: EFI below threshold AND price breaks above specified MA

## Advantages

1. Multiple MAs capture major trend change points. 

2. Oscillator combos avoid chasing highs and selling lows.

3. SL rules consider both trends and money flow, effectively controlling risks.

4. Optimized parameters through extensive backtesting, adaptive to most market environments. 

5. Medium trading frequency, stable signals, suitable for long-term trend tracking.

## Risks

1. Sudden crashes may invalidate SL, SL range should be widened.

2. Too many signals during ranging markets, parameters should be adjusted.

3. Holding too long may amplify losses, shorter MAs can take quicker SL. 

4. Backtest overfitting, real trading results pending validation.

## Improvements

1. Optimize parameters for higher returns and suitable frequency.

2. Add machine learning algorithms to dynamically optimize parameters.

3. Build adaptive SL mechanism based on different market conditions. 

4. Add more filters to determine better entry signals.

5. Incorporate position sizing strategies to control single bet size.

## Conclusion

The Gradual Moving Average Trend Following Strategy effectively tracks major trends by identifying the trend direction with multiple MAs and entering on filtered signals, achieving stable profits through long-term holding. The strategy has shown robustness through parameter optimization but still requires improvements in risk control and adaptivity to reduce drawdowns and increase win rate. Overall, the core philosophy demonstrates strong potential for further research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|58|longitud_sma|
|v_input_int_1|18|Length1|
|v_input_int_2|18|Length2|
|v_input_int_3|26|Length3|
|v_input_int_4|36|Length4|
|v_input_int_5|78|Length5|
|v_input_int_6|true|Length6|
|v_input_int_7|1500|Length7|
|v_input_int_8|58|Length8|
|v_input_int_9|3000|Length9|
|v_input_int_10|2|Length10|
|v_input_int_11|14|Length11|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-25 00:00:00
end: 2023-10-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © murdocksilva

//@version=5

strategy("Daily_Mid Term_Consulting BOLT")

//calculo longuitud
longuitud = input(58, title= "longitud_sma")


px = ta.sma(close, 1)
px2 = ta.sma(low, 1)

Length1 = input.int(18)
Length2 = input.int(18)
Length3 = input.int(26)
Length4 = input.int(36)
Length5 = input.int(78)
Length6 = input.int(1)
Length7 = input.int(1500)
Length8 = input.int(58)
Length9 = input.int(3000)
Length10 = input.int(2)
Length11 = input.int(14)
ma1 = ta.sma(low, Length1)
ma2 = ta.sma(high, Length2)
ma3 = ta.sma(close, Length3)
ma4 = ta.sma(close, Length4)
ma5 = ta.sma(close, Length5)
ma6 = ta.sma(close, Length6)
ma7 = ta.sma(close, Length7)
ma8 = ta.sma(close, Length8)
ma9 = ta.sma(close, Length9)
ma10 = ta.sma(close, Length10)
ma11 = ta.sma(close, Length11)

// calculo EFI
efi = (close[1]-close) * volume / 1000
efi_indicador = (efi[1] + efi) / 2

//Variable  RSI - calculo desv estandar
b = (px-ma10)*(px-ma10)
b2 = (px[1]-ma10[1])*(px[1]-ma10[1])
c = b + b2
c2 = c / 2
desv = math.sqrt(c2)/10

//calculo MACD
macd = ma4 - ma5

//calculo RSI
rsi = ta.rsi(close, 9)

// calculo Divergencia
ma = ta.sma(close, longuitud)
dist = close - ma
porcentaje = dist * 100 / close
ma_dista = ta.sma(porcentaje, 333)

//condición de entrada y salida long
long = ma1[1] < ma1 and ma2[1] < ma2 and macd > 0 and px > ma3 and efi_indicador < 9 and px > ma7 and macd[1] < macd
clong = efi_indicador > 22000 and px < ma8
strategy.entry("BUY", strategy.long, when = long)
strategy.close("BUY", when = clong)

//condición de entrada y salida short
short = ma1[1] > ma1 and ma2[1] > ma2 and macd < 0 and px < ma3 and efi_indicador > 9 and macd[1] > macd 
cshort =  efi_indicador < 14000 and px > ma8 and ma11 > desv
strategy.entry("SELL", strategy.short, when = short)
strategy.close("SELL", when = cshort)

//SL Y TP
//strategy.exit("long exit", "Daily_Mid Term_Consulting BOLT", profit = close * 40 / syminfo.mintick, loss = close * 0.02 / syminfo.mintick)
//strategy.exit("shot exit", "Daily_Mid Term_Consulting BOLT", profit = close * 40 / syminfo.mintick, loss = close * 0.02 / syminfo.mintick)

// GRAFICA smas
plot(ma1, color=color.new(color.orange, 0))
plot(ma2, color=color.new(color.orange, 0))
plot(ma3, color=color.new(color.orange, 0))
plot(ma4, color=color.new(color.orange, 0))
plot(ma5, color=color.new(color.orange, 0))
plot(ma6, color=color.new(color.green, 0))
plot(ma7, color=color.new(color.orange, 0))
plot(ma8, color=color.new(color.orange, 0))
plot(ma9, color=color.new(color.orange, 0))
//GRAFICA MACD
plot(macd, color=color.new(color.red, 0), style = plot.style_columns)
//GRAFICA DIVERGENCIA
plot(porcentaje, style = plot.style_columns)
//GRAFICA MA DIVERGENCIA
plot(ma_dista, color=color.new(color.white, 0))
//GRAFICA MA DIVERGENCIA
plot(desv, color=color.new(color.blue, 0))
//GRAFICA EFI
plot(efi_indicador, color=color.new(color.yellow, 0))
// GRAFICA RSI
l1 = hline(70, color=color.new(color.green, 0))
l2 = hline(30, color=color.new(color.green, 0))
plot(rsi, color=color.new(color.white, 0))




//prueba 1 stop loss and take profit
//sl = 0.05
//tp = 0.1    
//calculo de precio para sl y tp
//longstop=strategy.position_avg_price*(1-sl)
//longprofit=strategy.position_avg_price*(1+tp)

//shortstop=strategy.position_avg_price*(1+sl)
//shortprofit=strategy.position_avg_price*(1-tp)

//if (long)
  //  strategy.exit("BUY", strategy.long)

//sl and tp  long|short
//if strategy.entry("BUY", strategy.long)

//if strategy.position_avg_price > 0
//strategy.exit("BUY", limit = longprofit, stop = longstop)

//if strategy.position_avg_price < 0
//strategy.exit("SELL", limit = shortprofit, stop=shortstop)
```

> Detail

https://www.fmz.com/strategy/430272

> Last Modified

2023-10-26 17:08:43
