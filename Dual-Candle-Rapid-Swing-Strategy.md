
> Name

Dual-Candle-Rapid-Swing-Strategy

> Author

ChaoZhang

> Strategy Description


[trans]
Double K-line speed band strategy
This strategy calculates the combination of daily trading volume changes and NVI indicators to determine the market swings within the very short term for trading.
Specifically, it calculates the number of days when daily trading volume decreases from the previous day, and forms an oscillator through changes in the NVI value. Go long when the indicator turns from negative to positive and the second K line is still positive; go short when the indicator turns from positive to negative and the second K line is still negative.
The advantage of this strategy is that it captures very short-term gaps and only requires 2 K lines to form a trading signal and achieve profits. However, this high-frequency trading method has the risk of over-optimization, and the effect may vary greatly in different market time periods.
In addition, such short-term transactions also have a certain dependence on transaction fees, and parameters need to be adjusted for specific varieties. At the same time, errors in trading decisions within a very small period of time may also cause losses. Only by strictly controlling the capital size of a single transaction can this double K-line strategy be applied for a long time.
||

This strategy combines calculations of daily volume change and the NVI indicator to trade short-term market swings.

Specifically, it counts the number of days volume is lower than previous day, and uses NVI value change to form an oscillator. Long signals are generated when the oscillator flips from negative to positive, and remains positive on the 2nd candle. Short signals occur on the flip from positive to negative, while still negative on 2nd candle.

The advantage of this strategy is capitalizing on short-term gaps within just 2 candles. However, such high frequency trading risks overoptimization, with performance varying greatly across market time periods.

Also, trading fees can be a concern for such short-term trades, requiring parameter tuning per instrument. And slight errors in decisions within small timeframes could lead to losses. Only by strictly controlling per trade position sizes can this dual candle strategy be applied successfully over the long run.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|═════════ DESDE ════════|
|v_input_2|true|Mes|
|v_input_3|true|Dia|
|v_input_4|2018|Año|
|v_input_5|true|═════════ HASTA ════════|
|v_input_6|31|Mes|
|v_input_7|12|Dia|
|v_input_8|9999|Año|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-04 00:00:00
end: 2023-09-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//
// ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ //

strategy(title = "Strategy Only 2 Candles",
         shorttitle = "SO2C",
         overlay = true,
         precision = 8,
         calc_on_order_fills = true,
         calc_on_every_tick = true,
         backtest_fill_limits_assumption = 0,
         default_qty_type = strategy.percent_of_equity,
         default_qty_value = 100,
         initial_capital = 1000,
         currency = currency.USD,
         linktoseries = true)

//
// ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ //

backTestSectionFrom = input(title = "═════════ DESDE ════════", defval = true, type = input.bool)

FromMonth       = input(defval = 1, title = "Mes", minval = 1)
FromDay         = input(defval = 1, title = "Dia", minval = 1)
FromYear        = input(defval = 2018, title = "Año", minval = 2014)

backTestSectionTo = input(title = "═════════ HASTA ════════", defval = true, type = input.bool)
ToMonth         = input(defval = 31, title = "Mes", minval = 1)
ToDay           = input(defval = 12, title = "Dia", minval = 1)
ToYear          = input(defval = 9999, title = "Año", minval = 2014)

backTestPeriod() => (time > timestamp(FromYear, FromMonth, FromDay, 00, 00)) and (time < timestamp(ToYear, ToMonth, ToDay, 23, 59))

//
// ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ //

nvi = 0.0
nvi := iff(volume < volume[1], nz(nvi[1]) + (close - close[1]) / close[1], nz(nvi[1]))
nvim = ema(nvi, 15)
nvimax = highest(nvim, 90)
nvimin = lowest(nvim, 90)
azul = (nvi - nvim) * 100 / (nvimax - nvimin)

// VARIABLES
var compra_activada = 0
var compra = true
var compra_1 = true
var cerrar_compra= 0
var venta_activada = 0
var venta = true
var venta_1 = true
var cerrar_venta= 0

// COMPRA
compra := azul > azul[1] and azul > 0 and azul[1] < 0
if (compra == 1 )
    compra_activada := 1

// CIERRE COMPRA
cerrar_compra :=  compra_activada[2] == 1 ? 1 : 0
if (cerrar_compra == 1)
    compra_activada := 0

// VENTA
venta := azul < azul[1] and azul < 0 and azul[1] > 0 
if (venta == 1 )
    venta_activada := 1
    
// CIERRE COMPRA
cerrar_venta :=  venta_activada[2] == 1 ? 1 : 0
if (cerrar_venta == 1)
    venta_activada := 0

// ESTRATEGIA
if (backTestPeriod())
    strategy.entry("Compra", true, when = compra == 1  )
    strategy.entry("Venta", false, when = venta == 1  )
    strategy.close("Compra", when = cerrar_compra == 1 )
    strategy.close("Venta", when = cerrar_venta == 1 )


```

> Detail

https://www.fmz.com/strategy/426365

> Last Modified

2023-09-11 15:12:08
