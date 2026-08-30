
> Name

Dual-SSL-Strategy-with-EMA-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1e8c49a698355cb5ffc.png)
[trans]

## Overview
This strategy combines the double trend indicator and the moving average indicator, uses the double trend indicator to determine the market trend direction, and uses the moving average to confirm the trend. It is a trend following strategy. Combining stop loss to control risks is a relatively stable strategy.
## Strategy Principle
1. Calculate the upper track formed by yesterday's closing price and the SMA average of the highest price in the specified period, and the lower track formed by yesterday's closing price and the SMA average of the lowest price in the specified period.
2. Compare the relationship between the current closing price and the upper and lower rails to determine the current trend direction. If the closing price is higher than the upper track, it is judged to be long; if the closing price is lower than the lower track, it is judged to be short.
3. Calculate the 200-period closing price SMA as the criterion for judging the medium and long-term trend.
4. When it is judged to be long, if the closing price breaks through the SMA moving average from bottom to top, a buy signal is generated; when it is judged to be short, if the closing price breaks through the SMA moving average from top to bottom, a sell signal is generated.
5. After entering a long position, if the closing price breaks below the upper rail, it will be used as a signal to close the position; after entering a short position, if the closing price breaks above the lower rail, it will be a signal to close the position.
6. Set a fixed proportion of the stop loss point. If the closing price falls below the stop loss point, the stop loss order will be activated.
## Strategic Advantages
1. Use the double trend indicator to determine the trend direction, which can effectively identify the trend and enhance the probability of entering the right direction.
2. The addition of moving average can filter out some noise signals and avoid wrong transactions in volatile market conditions.
3. Use stop loss to control the risk of single loss, which can effectively avoid excessive losses.
4. The strategy operation is relatively simple, easy to understand and implement, and is suitable for beginners to practice.
## Strategy Risk
1. The double trend indicator is more sensitive to parameter settings. Different combinations of period parameters will lead to large differences in results. The optimization of parameters needs to be tested carefully.
2. If the moving average is too long, it will filter out more trading opportunities; if the moving average is too short, the denoising effect will be poor. The setting of the moving average cycle parameters needs to be weighed.
3. If the stop loss point is set too wide, it will not be able to achieve good risk control; if it is too narrow, it will be easily triggered by regular price fluctuations to exit. Stop loss range needs to be set carefully.
4. The strategy relies heavily on parameter optimization. If the parameters are set improperly, the trend direction may not be correctly identified, resulting in incorrect trading decisions.
## Strategy optimization direction
1. You can test combinations of different cycle parameters to find parameters that make the double trend indicator more accurate in judging the trend.
2. You can test moving average indicators of different periods and find the best moving average parameters that balance the denoising effect and retain the signal.
3. You can try to design an adaptive stop loss mechanism based on the degree of market volatility to make the stop loss closer to the market conditions.
4. You can also try to add other indicators for assistance, such as volume and price confirmation, multi-time frame smoothness, etc., to improve the stability of the strategy.
5. The optimized strategy can be verified using walk forward analysis to ensure that the parameters are still robust.
## Summarize
This strategy integrates the advantages of dual trend indicators and moving averages, and is a trend following strategy with large room for parameter optimization. Through reasonable parameter setting and optimization, better strategy performance can be obtained. However, attention should be paid to controlling the risk of over-optimization of parameters and ensuring parameter robustness. Overall, this strategy is suitable for use as a case for strategy exploration and learning.
||


## Overview

This strategy integrates the Dual SSL indicator and moving average indicator, using the Dual SSL indicator to determine market trend direction, and moving averages for trend confirmation. It belongs to a trend following strategy. With the addition of a stop loss to control risk, it is a relatively stable strategy.

## Strategy Logic

1. Calculate the upper rail by taking the SMA of the highest price over a specified period vs. yesterday's close. Calculate the lower rail by taking the SMA of the lowest price over a specified period vs. yesterday's close.

2. Compare the current closing price with the upper and lower rails to determine the current trend direction. If the closing price is above the upper rail, the trend is determined as bullish. If the closing price is below the lower rail, the trend is determined as bearish.

3. Calculate the 200-period SMA of closing prices as a benchmark for medium to long term trends. 

4. When bullish, if the closing price breaks above the SMA from below, a buy signal is generated. When bearish, if the closing price breaks below the SMA from above, a sell signal is generated.

5. After entering a long position, if the closing price breaks below the upper rail, it is a close signal. After entering a short position, if the closing price breaks above the lower rail, it is a close signal.

6. Set a fixed percentage stop loss point. If the closing price breaks below the stop loss point, the stop loss order is triggered.

## Advantages

1. Using the Dual SSL indicator to determine trend direction can effectively identify trends and increase the probability of entering in the right direction.

2. Adding moving averages can filter out some noise signals and avoid wrong trades in choppy markets. 

3. Using a stop loss to control single trade risk can effectively avoid excessive losses.

4. The strategy logic is relatively simple and easy to understand, suitable for beginners to practice on.

## Risks

1. The Dual SSL indicator is sensitive to parameter tuning, different period combinations can lead to very different results. Parameters should be carefully optimized.

2. A MA that is too long filters out too many trading opportunities, while one too short fails to denoise effectively. A balanced MA period should be used.

3. A stop loss range set too wide fails to control risk effectively, while one too tight may be triggered by normal price fluctuations. The stop loss range needs to be set carefully. 

4. The strategy relies heavily on parameter optimization. Incorrect parameters may fail to identify trends correctly, leading to wrong trading decisions.

## Optimization Directions 

1. Test different period combinations to find parameters that can improve trend determination accuracy for the Dual SSL indicator.

2. Test different period MAs to find the optimal balance between denoising and preserving signals.

3. Explore adaptive stop losses that adjust based on market volatility to make the stop loss more responsive. 

4. Incorporate other indicators for confirmation, such as volume, multi-timeframe confluence, to improve robustness.

5. Walk forward analysis should be conducted on the optimized strategy to ensure robustness.

## Conclusion

This strategy combines the strengths of the Dual SSL indicator and moving averages. With significant potential for parameter optimization, it is a trend following strategy. With reasonable parameter tuning and optimization, good results can be achieved. However, the risk of overfitting should be controlled to ensure robustness. Overall, this strategy serves as a good example for exploration and learning.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|2|Stop Loss|
|v_input_1|10|Period|
|v_input_2|10|Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-30 00:00:00
end: 2023-11-05 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
//@Isaac
//Estrategia vista en ▼▼
//YT: Trading Zone
strategy('SSL Strategy + EMA 200 AND Stop Loss', overlay=true)

ema = ta.ema(close, 200)

stop_loss = input.float(2.00, title='Stop Loss', step=0.10)

period = input(title='Period', defval=10)
len = input(title='Period', defval=10)
smaHigh = ta.sma(high, len)
smaLow = ta.sma(low, len)
Hlv = int(na)
Hlv := close > smaHigh ? 1 : close < smaLow ? -1 : Hlv[1]
sslDown = Hlv < 0 ? smaHigh : smaLow
sslUp = Hlv < 0 ? smaLow : smaHigh


cruceArriba = ta.crossover(sslUp, sslDown)
cruceAbajo = ta.crossunder(sslUp, sslDown)

alcista = (close > ema ) and (cruceArriba) 
bajista = (close < ema) and (cruceAbajo)

var SL = 0.0
//Cerrar compra por cruce
por_cruce = ta.crossunder(sslUp, sslDown)

//Cerrar venta por cruce
por_cruceAB = ta.crossunder(sslDown, sslUp)

//Cerrar compra y venta por stop loss
Stop = SL

comprado = strategy.position_size > 0
vendido = strategy.position_size < 0

UTmpconvertL = strategy.position_avg_price * (1 + 0.1)
UTmpdefineL = (UTmpconvertL > close and strategy.openprofit > 0.1)
UTSPL = UTmpdefineL

SPL = UTSPL

///////////////////////////////////////////////////////////////////////

UTmpconvertLS = strategy.position_avg_price * (1 + 0.1)
UTmpdefineLS = (UTmpconvertLS > close and strategy.openprofit > 0.1)
UTSPLS = UTmpdefineLS

SPLS = UTSPLS

////////////////////////////////////////////////////////////////////////

if not comprado and not vendido and alcista
    cantidad = (strategy.equity / close)
    strategy.entry('Compra', strategy.long, qty=cantidad, comment="Long")
    SL := sslDown


if comprado and not vendido and por_cruce and SPL
    strategy.close("Compra", comment="Exit Long")
    SL := 0
    
if comprado and not vendido and Stop
    strategy.exit('Compra', stop=Stop, comment="SL")
    SL := 0

///////////////////////////////////////////////////////////////////

if not comprado and not vendido and bajista
    cantidad = (strategy.equity / close)
    strategy.entry('Venta', strategy.short, qty=cantidad, comment="Short")
    SL := sslDown

if not comprado and vendido and por_cruceAB and SPLS
    strategy.close("Venta", comment="Exit Short")
    SL := 0
    
if not comprado and vendido and Stop
    strategy.exit('Venta', stop=Stop, comment="SLS")
    SL := 0



plot(Stop > 0 ? Stop : na, style=plot.style_circles, color=color.new(color.yellow,0))
plot(ema)
plot(sslDown, linewidth=2, color=color.new(color.red, 0))
plot(sslUp, linewidth=2, color=color.new(color.lime, 0))



```

> Detail

https://www.fmz.com/strategy/431284

> Last Modified

2023-11-06 16:52:11
