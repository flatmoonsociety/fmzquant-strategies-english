
> Name

Momentum-Indicator-Aggregation-Trading-Strategy based on momentum indicator aggregation trading strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/dc9df152428ade2217.png)
[trans]
### Overview
This strategy comprehensively uses a variety of technical indicators such as moving averages, MACD, RSI, Bollinger Bands, etc., to achieve the aggregation of multiple buy and sell signals, forming a relatively complete momentum indicator aggregation trading strategy.
### Strategy Principles
The core logic of the strategy is to aggregate buy and sell signals from multiple technical indicators. Specifically, it mainly includes the following aspects:
1. Moving average indicator: Calculate the fast moving average and the slow moving average. When the fast line crosses the slow line, a buy signal is generated, and when it crosses below, a sell signal is generated.
2. MACD indicator: Calculate the MACD line and signal line. When the MACD line crosses the signal line, a buy signal is generated, and when it crosses below, a sell signal is generated.
3. RSI indicator: Calculate the RSI value to determine whether it has entered the overbought or oversold area, and combine the golden cross and death cross of the RSI line and the central axis 50 line to generate buy and sell signals.
4. Bollinger Band indicator: Determine whether the price breaks through the upper and lower rails, and generate buy and sell signals based on the signal returning to the middle rail.
5. Exit judgment: Set the stop-profit and stop-loss standards, and actively exit the position when it reaches a certain ratio.
Each of the above signal modules is independent of each other. The strategy will monitor these signals in real time, open a long position when a buy signal is triggered, and a short position when a sell signal is triggered, to achieve dynamic aggregation of profit orders.
### Advantage Analysis
This strategy has the following advantages:
1. Rich signal sources: Combining buy and sell signals from a variety of technical indicators, it is not easy to miss market opportunities.
2. Reduce false signals: The aggregate verification of different indicator signals can reduce the adverse effects of false signals of certain indicators to a certain extent.
3. Consider both trends and reversals: Using trend indicators such as moving averages and reversal indicators such as RSI and MACD can achieve good results in different market conditions.
4. Automatic stop-profit and stop-loss: The strategy has a built-in automatic stop-profit and stop-loss mechanism, which can effectively control risks and avoid loss expansion.
### Risk Analysis
There are also some risks in this strategy, mainly reflected in the following aspects:
1. Risk of indicator failure: Under certain market conditions, each indicator may experience certain failures, causing signal deviation.
2. The problem of over-aggregation: If signals are too aggregated, it is easy to cause insufficient indicator resolution and miss some opportunities.
3. Parameter optimization is difficult: Because there are many indicators, parameter optimization will be difficult, and improper indicator parameter settings may also affect strategy performance.
4. High turnover rate: Strategy signals are more frequent, which will result in a higher turnover rate and increase transaction costs.
### Optimization direction
There is still some room for optimization in this strategy, which can mainly start from the following aspects:
1. Test and optimize each indicator and parameter to find the best indicator combination.
2. Automatically find optimal parameters through machine learning methods to avoid exhaustive manual parameter optimization.
3. Test different indicator weight aggregation methods to find the optimal solution for signal aggregation.
4. Add an adaptive stop-loss mechanism, which can automatically adjust the stop-loss standard according to market fluctuations.
5. Add a position opening algorithm, control the proportion of a single position opening, and reduce the risk of a single transaction.
### Summarize
Overall, this strategy is a relatively typical and universal momentum indicator aggregation trading strategy. It comprehensively uses the buy and sell signals of a variety of common technical indicators, and improves strategy performance through signal aggregation. Compared with a single indicator strategy, it has the advantages of more abundant signal sources and more comprehensive identification of trends and reversals. At the same time, the difficulty of parameter optimization and the increased risk of indicator failure are also issues that need attention. Through further testing and optimization, this strategy can become a very practical quantitative trading tool.
||

### Overview

This strategy integrates multiple technical indicators including moving average, MACD, RSI and Bollinger bands to generate a variety of buy and sell signals, forming a relatively complete momentum indicator aggregation trading strategy.  

### Strategy Logic  

The core logic of the strategy is to aggregate the buy and sell signals of multiple technical indicators, which mainly includes the following aspects:

1. Moving average indicator: Calculate the fast and slow moving average lines and generate buy signals when the fast line crosses above the slow line, and sell signals when crossing below.  

2. MACD indicator: Calculate the MACD line and signal line, generating buy signals when the MACD line crosses above the signal line, and sell signals when crossing below.

3. RSI indicator: Calculate RSI values to determine if it enters overbought or oversold zones, combined with the golden cross and death cross of RSI line and middle line 50 to generate trading signals.  

4. Bollinger bands indicator: Determine if prices break through upper and lower bands, combined with signals of returning to middle band to generate trading signals.

5. Exit criteria: Set stop profit and stop loss standards, exit positions when reaching certain percentages.

The signals of each indicator modules work independently. The strategy monitors these signals in real time, goes long when buy signals triggered and goes short when sell signals triggered, to dynamically aggregate profitable positions.

### Advantage Analysis   

The advantages of this strategy includes:

1. Rich signal sources with various indicator signals, not easy to miss opportunities. 

2. Reduce false signals by verifying signals with different indicators.  

3. Good adaptability to trends and reversals with both trending and mean-reverting indicators. 

4. Automatic stop profit and stop loss mechanism helps control risks.

### Risk Analysis

There are also some risks existed in this strategy:

1. Invalidity risk of indicators under certain market conditions.

2. Oversimplification problem when aggregating too many signals, leads to insufficient resolution.

3. Difficulties in parameter optimization with many indicators.  

4. High turnover rate and increased trading costs.


### Optimization Directions

There are some rooms for further optimizations:  

1. Test and optimize the combinations of indicators and parameters.

2. Use machine learning methods to find optimal parameters automatically. 

3. Test different weighting methods for signal aggregation.  

4. Add adaptive stop loss mechanisms based on market volatility.

5. Add opening algorithms to control single opening proportions for better risk control.


### Conclusion

In conclusion, this is a typical and universal momentum indicator aggregation trading strategy, which integrates trading signals from various common technical indicators and improves performance through signal aggregation. Compared with single indicator strategies, it has the advantages of more abundant signal sources and better identification of trends and reversals. Meanwhile, the difficulties in parameter optimization and increased invalidity risks should also be noticed. With further testing and optimization, this strategy can become a very practical quantitative trading tool.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2019|BackTestBaşlangıç Tarihi|
|v_input_int_1|50|EMA Kısa Periyodu|
|v_input_int_2|100|EMA Uzun Periyodu|
|v_input_int_3|50|Hareketli Ortalama Periyodu|
|v_input_int_4|12|MACD Hızlı Periyodu|
|v_input_int_5|26|MACD Yavaş Periyodu|
|v_input_int_6|9|MACD Sinyal Periyodu|
|v_input_int_7|14|RSI Periyodu|
|v_input_int_8|70|RSI Aşırı Alım Eşiği|
|v_input_int_9|30|RSI Aşırı Satım Eşiği|
|v_input_int_10|20|Bollinger Bantları Periyodu|
|v_input_float_1|2|Bollinger Bantları Standart Sapması|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Kesin Etkili Analiz V1 - Artun Sinan", overlay=true)
//indicator("Kesin Etkili Analiz V1 - Artun Sinan", overlay=true)

//BackTest
yearin = input (2019, title="BackTestBaşlangıç Tarihi")

// Göstergelerin parametrelerini tanımlayın
emaShrtPeriod = input.int(title="EMA Kısa Periyodu", defval=50, minval=1)
emaLngPeriod = input.int(title="EMA Uzun Periyodu", defval=100, minval=1)

maPeriod = input.int(50, "Hareketli Ortalama Periyodu", minval=1)
fast = input.int(12, "MACD Hızlı Periyodu", minval=1)
slow = input.int(26, "MACD Yavaş Periyodu", minval=1)
signal = input.int(9, "MACD Sinyal Periyodu", minval=1)
rsiPeriod = input.int(14, "RSI Periyodu", minval=1)
rsiOverbought = input.int(70, "RSI Aşırı Alım Eşiği", minval=50, maxval=100)
rsiOversold = input.int(30, "RSI Aşırı Satım Eşiği", minval=0, maxval=50)
bbPeriod = input.int(20, "Bollinger Bantları Periyodu", minval=1)
bbStd = input.float(2, "Bollinger Bantları Standart Sapması", minval=0.1)

//EMA göstergesi ayarları
ema1 = ta.ema (close,emaShrtPeriod)
ema2 = ta.ema (close, emaLngPeriod)

emaCrossUp = ema1 >= ema2
emaCrossDown = ema2 < ema1

plot(ema1, title="EMAKısa", color=color.rgb(0, 255, 13))
plot(ema2, title="EMAUzun", color=color.rgb(255, 251, 1))



// Göstergeleri hesaplayın
ma = ta.sma(close, maPeriod) // Hareketli ortalama
[macd, macdsignal, macdhist] = ta.macd(close, fast, slow, signal) // MACD
rsi = ta.rsi(close, rsiPeriod) // RSI
[upper, middle, lower] = ta.bb(close, bbPeriod, bbStd) // Bollinger Bantları

// Alım veya satım sinyalleri üretin
buySignal = false
sellSignal = false

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Fibonacci seviyelerini tanımlayın
fibLevels = array.new_float(7) // Fibonacci seviyelerini tutacak bir dizi oluşturun
array.set(fibLevels, 0, 0.0) // %0 seviyesini ayarlayın
array.set(fibLevels, 1, 0.236) // %23.6 seviyesini ayarlayın
array.set(fibLevels, 2, 0.382) // %38.2 seviyesini ayarlayın
array.set(fibLevels, 3, 0.5) // %50 seviyesini ayarlayın
array.set(fibLevels, 4, 0.618) // %61.8 seviyesini ayarlayın
array.set(fibLevels, 5, 0.786) // %78.6 seviyesini ayarlayın
array.set(fibLevels, 6, 1.0) // %100 seviyesini ayarlayın

// Tepe ve dip noktasını belirleyin
highpoint = ta.highest (high, 20) // Son 30 mum çubuğunun en yüksek değerini alın
lowpoint = ta.lowest (low, 20) // Son 30 mum çubuğunun en düşük değerini alın
diff = highpoint - lowpoint // Tepe ve dip noktası arasındaki farkı hesaplayın

// Fibonacci seviyelerini hesaplayın
fib0 = lowpoint + diff * array.get(fibLevels, 0) // %0 seviyesini hesaplayın
fib1 = lowpoint + diff * array.get(fibLevels, 1) // %23.6 seviyesini hesaplayın
fib2 = lowpoint + diff * array.get(fibLevels, 2) // %38.2 seviyesini hesaplayın
fib3 = lowpoint + diff * array.get(fibLevels, 3) // %50 seviyesini hesaplayın
fib4 = lowpoint + diff * array.get(fibLevels, 4) // %61.8 seviyesini hesaplayın
fib5 = lowpoint + diff * array.get(fibLevels, 5) // %78.6 seviyesini hesaplayın
fib6 = lowpoint + diff * array.get(fibLevels, 6) // %100 seviyesini hesaplayın

// Alım sinyali: Fiyat %61,8 seviyesinden yukarı yönlü kırılırsa ve MACD çizgisi sinyal çizgisinin üzerine çıkarsa, alım pozisyonu açın
alSignal = close > fib4 and ta.crossover(macd, macdsignal)

// Satım sinyali: Fiyat %61,8 seviyesinden aşağı yönlü kırılırsa ve MACD çizgisi sinyal çizgisinin altına inerse, satım pozisyonu açın
satSignal = close < fib4 and ta.crossunder(macd, macdsignal)

// Çıkış sinyali: Fiyat %38,2 Fibonacci seviyesine ulaşırsa veya belirli bir yüzde oranında kar veya zarar elde ederseniz, pozisyonu kapatın
exitSignal = close >= fib2 or close <= strategy.position_avg_price * 0.95 // Kar oranı olarak %5, zarar oranı olarak %5 belirledik

plot(fib0, title="%0", color=color.rgb(25, 0, 255))
plot(fib1, title="%23.6", color=color.rgb(25, 0, 255))
plot(fib2, title="%38.2", color=color.rgb(25, 0, 255))
plot(fib3, title="%50", color=color.rgb(25, 0, 255))
plot(fib4, title="%61.8", color=color.rgb(25, 0, 255))
plot(fib5, title="%78.6", color=color.rgb(25, 0, 255))
plot(fib6, title="%100", color=color.rgb(25, 0, 255))
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// Hareketli ortalama kesişimi sinyali
maCrossUp = ta.crossover(ma, close) // Fiyat hareketli ortalamanın üzerine çıkarsa
maCrossDown = ta.crossunder(ma, close) // Fiyat hareketli ortalamanın altına inerse

// MACD çizgisi ve sinyal çizgisi kesişimi sinyali // Histogram yerine çizgiler
macdCrossUp = ta.crossover(macd, macdsignal) // MACD çizgisi sinyal çizgisinin üzerine çıkarsa
macdCrossDown = ta.crossunder(macd, macdsignal) // MACD çizgisi sinyal çizgisinin altına inerse

// RSI aşırı alım veya aşırı satım sinyali ve 50 seviyesi kesişimi sinyali // Sinyalleri birleştir
// Eşik değerleri doğrudan kullanın
rsiOverboughtSignal = rsi > rsiOverbought and ta.crossover(rsi, 50) // RSI değeri aşırı alım eşiğinin üzerindeyse ve 50 seviyesini yukarı keserse
rsiOversoldSignal = rsi < rsiOversold and ta.crossunder(rsi, 50) // RSI değeri aşırı satım eşiğinin altındaysa ve 50 seviyesini aşağı keserse

// Bollinger Bantları kırılımı sinyali ve orta bant geri dönüşü sinyali // Sinyalleri birleştir
bbBreakUp = close > upper and ta.crossover(close, middle) // Fiyat üst banttan çıkarsa ve orta banta geri dönerse
bbBreakDown = close < lower and ta.crossunder(close, middle) // Fiyat alt banttan inerse ve orta banta geri dönerse

// Sinyalleri birleştirin
buySignal := maCrossUp or macdCrossUp or rsiOversoldSignal or bbBreakUp or emaCrossUp and yearin >= year
sellSignal := maCrossDown or macdCrossDown or rsiOverboughtSignal or bbBreakDown or emaCrossDown and yearin >= year

// Sinyalleri grafikte oklar ile gösterin
plotshape(buySignal, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small)
plotshape(sellSignal, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small)

plot(macd, title="MACD", color=color.blue) // MACD çizgisini mavi renkte çizin
plot(macdsignal, title="Sinyal", color=color.orange) // Sinyal çizgisini turuncu renkte çizin


if buySignal
    strategy.entry("Enter Long", strategy.long)
else if sellSignal
    strategy.entry("Enter Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/442349

> Last Modified

2024-02-21 11:59:22
