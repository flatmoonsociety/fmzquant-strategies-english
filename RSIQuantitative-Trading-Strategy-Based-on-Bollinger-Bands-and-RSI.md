
> Name

Quantitative-Trading-Strategy-Based-on-Bollinger-Bands-and-RSI
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/155fa569be046ccc333.png)
 [trans]

### Overview
This strategy designs a quantitative trading strategy based on Bollinger Bands and the Relative Strength Index (RSI). This strategy combines trend following and overbought and oversold judgments, aiming to enter the market at the beginning of the trend and exit when overbought and oversold to achieve profits.
### Strategy Principles
This strategy uses Bollinger Bands to determine price trends and support and resistance levels. When the price is close to the lower Bollinger Band, it is considered an oversold signal; when the price is close to the upper Bollinger Band, it is considered an overbought signal. At the same time, combine the RSI indicator to determine whether it is oversold or overbought.
The specific trading rules are: enter long when the price is lower than the upper Bollinger Band and RSI is lower than 30; enter short when the price is higher than the upper Bollinger Band and RSI is higher than 70. When exiting, choose the middle line of Bollinger Bands or the Bollinger Band track in the opposite direction as the take-profit level. Stop loss is set as a percentage of the entry price.
### Strategic Advantages
This strategy combines the trend tracking of Bollinger Bands and the overbought and oversold judgment of RSI, and can better grasp the starting point of the trend. At the same time, the take-profit and stop-loss strategies are also relatively clear, which is conducive to risk management.
Compared with the single use of indicators such as Bollinger Bands or RSI, this strategy comprehensively uses a variety of indicators and parameters to improve the accuracy of decision-making. When the parameters are adjusted appropriately, its trading performance will be relatively stable.
### Strategy Risk
This strategy mainly relies on parameter optimization. If the parameters are set improperly, it will face greater risks. For example, if the Bollinger Band cycle parameters do not match, the trend may be missed or false signals may be generated. In addition, take profit and stop loss points also need to be carefully evaluated.
This strategy also has a certain dependence on trading varieties. For varieties with large fluctuations, Bollinger Band parameters need to be adjusted. For varieties whose trends are not obvious, the effect will also be compromised. In addition, strategies are also affected by transaction costs, slippage, and extreme market conditions.
It is recommended to conduct parameter optimization tests, evaluate take-profit and stop-loss levels, and test performance under different varieties and market environments. At the same time, space is reserved for risk management.
### Optimization direction
This strategy can continue to be optimized from the following directions:
1. Evaluate and optimize the parameters of Bollinger Bands and RSI to better match the characteristics of the traded products
2. Add other indicator judgments, such as KDJ, MACD, etc., to form a multi-factor model
3. Evaluate take-profit and stop-loss strategies and set up floating stop-loss or batch-based take-profit
4. Dynamically optimize parameters according to specific varieties and market environment
5. Add machine learning model to judge signal quality and risk level
### Summarize
This strategy integrates Bollinger Bands and RSI indicators to design a relatively complete trend tracking strategy. Through parameter optimization and risk management, there is room for further improvement in its effect and stability. It is recommended to adjust and optimize according to your own needs and risk preferences in order to achieve better performance.
||

### Overview

This strategy designs a quantitative trading strategy based on Bollinger Bands and the Relative Strength Index (RSI). It combines trend tracking and overbought/oversold judgment to enter the market at the beginning of a trend and exit at overbought/oversold levels to profit.

### Strategy Principle 

The strategy uses Bollinger Bands to determine price trends and support/resistance levels. Prices approaching the lower Bollinger Band are seen as an oversold signal, while prices approaching the upper Bollinger Band are seen as an overbought signal. At the same time, it incorporates the RSI indicator to determine if oversold or overbought conditions exist.

The specific trading rules are: go long when the price is below the lower Bollinger Band and the RSI is below 30; go short when the price is above the upper Bollinger Band and the RSI is above 70. For profit taking, set the middle Bollinger Band or the opposite Bollinger Band as the take profit level. The stop loss is set at a certain percentage from the entry price.

### Advantages

The strategy combines Bollinger Bands’ trend tracking ability and RSI’s overbought/oversold judgement to capture good trend start timing. Also, the profit taking and stop loss strategies provide clear risk management. 

Compared to using a single indicator like Bollinger Bands or RSI alone, this strategy utilizes multiple indicators and parameters to improve decision accuracy. With proper parameter tuning, it can achieve relatively stable performance.

### Risks

The strategy relies heavily on parameter optimization. Incorrect parameter settings can lead to missing trends or generating false signals. For example, mismatching Bollinger period may cause such issues. Take profit and stop loss levels also need careful assessment.

The strategy also depends on the trading instrument. For highly volatile assets, Bollinger Band parameters need to be adjusted accordingly. For instruments with unclear trends, the performance may suffer as well. Also affected by transaction costs, slippage and extreme market events.

Parameter optimization testing is recommended to evaluate profit taking/stop loss levels and performance across different assets and market regimes. Maintain risk management buffers. 


### Optimization Directions

Several aspects can be improved:

1. Evaluate and optimize parameters for Bollinger Bands and RSI to better match the trading instrument characteristics  

2. Incorporate additional indicators like KDJ, MACD to build a multifactor model

3. Assess profit taking/stop loss strategies, such as trailing stop loss or scaled exit

4. Conduct dynamic parameter tuning based on specific assets and market conditions

5. Add machine learning models to judge signal quality and risk levels

### Summary

This strategy integrates Bollinger Bands and RSI for a comprehensive trend following system. There is further room for improving effectiveness and stability through parameter tuning and risk management. Custom adjustments and optimizations are recommended based on individual needs and risk preference for better performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Longitud BB|
|v_input_2|2|Multiplicador BB|
|v_input_3|D|Marco de Tiempo BB|
|v_input_4|14|Longitud RSI|
|v_input_5|70|Nivel de sobrecompra RSI|
|v_input_6|30|Nivel de sobreventa RSI|
|v_input_7|0|Take Profit (banda): Central|Opuesta|
|v_input_8|2|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-01 00:00:00
end: 2023-11-30 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("BB + RSI Estrategia", overlay=true)

longitud = input(20, title="Longitud BB", minval=5, maxval=50, step=1)
multiplicador = input(2.0, title="Multiplicador BB", type=input.float, step=0.1)
timeframe_bb = input("D", title="Marco de Tiempo BB", type=input.resolution)
rsi_length = input(14, title="Longitud RSI", minval=5, maxval=50, step=1)
rsi_overbought = input(70, title="Nivel de sobrecompra RSI", minval=50, maxval=80, step=1)
rsi_oversold = input(30, title="Nivel de sobreventa RSI", minval=20, maxval=50, step=1)
take_profit = input("Central", title="Take Profit (banda)", options=["Central", "Opuesta"])
stop_loss = input(2.00, title="Stop Loss", type=input.float, step=0.10)

var SL = 0.0

[banda_central, banda_superior, banda_inferior] = security(syminfo.tickerid, timeframe_bb, bb(close, longitud, multiplicador))
rsi_value = rsi(close, rsi_length)

comprado = strategy.position_size > 0
vendido = strategy.position_size < 0

if not comprado and not vendido
    if close < banda_inferior and rsi_value < rsi_oversold
        // Realizar la compra
        cantidad = round(strategy.equity / close)
        strategy.entry("Compra", strategy.long, qty=cantidad, when=cantidad > 0)
        SL := close * (1 - (stop_loss / 100))

    if close > banda_superior and rsi_value > rsi_overbought
        // Realizar la Venta
        cantidad = round(strategy.equity / close)
        strategy.entry("Venta", strategy.short, qty=cantidad, when=cantidad > 0)
        SL := close * (1 + (stop_loss / 100))

if comprado
    // Verificar el take profit
    if take_profit == "Central" and close >= banda_central
        strategy.close("Compra", comment="TP")
        SL := 0

    if take_profit == "Opuesta" and close >= banda_superior
        strategy.close("Compra", comment="TP")
        SL := 0
    // Verificar el stop loss
    if close <= SL
        strategy.close("Compra", comment="SL")
        SL := 0

if vendido
    // Verificar el take profit
    if take_profit == "Central" and close <= banda_central
        strategy.close("Venta", comment="TP")
        SL := 0

    if take_profit == "Opuesta" and close <= banda_inferior
        strategy.close("Venta", comment="TP")
        SL := 0
    // Verificar el Stop loss
    if close >= SL
        strategy.close("Venta", comment="SL")
        SL := 0

// Salida
plot(SL > 0 ? SL : na, style=plot.style_circles, color=color.red)
g1 = plot(banda_superior, color=color.aqua)
plot(banda_central, color=color.red)
g2 = plot(banda_inferior, color=color.aqua)
fill(g1, g2, color=color.aqua, transp=97)

// Dibujar niveles de sobrecompra/sobreventa del RSI
hline(rsi_overbought, "RSI Overbought", color=color.red)
hline(rsi_oversold, "RSI Oversold", color=color.green)
```

> Detail

https://www.fmz.com/strategy/435979

> Last Modified

2023-12-20 15:39:19
