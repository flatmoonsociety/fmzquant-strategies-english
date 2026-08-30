
> Name

Equilibrium line PSAR indicator trading strategy Heikin-Ashi-PSAR-Trend-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy uses a combination of equilibrium line graphics and PSAR indicators to determine trends and generate trading signals. This strategy relies on the noise reduction characteristics of the equilibrium line and cooperates with the PSAR indicator to determine the trend reversal point to capture the medium and long-term trend.
Strategy principle:
1. Calculate the opening price, closing price, highest price, and lowest price of the equilibrium line.
2. Determine the long and short trends based on the color of the equilibrium line entity.
3. Calculate the PSAR indicator and determine the trend reversal when it breaks through from top to bottom or bottom to top.
4. When the equilibrium line is long, PSAR breaks downward to go long; when the equilibrium line is short, PSAR breaks upward and goes short.
5. PSAR is adaptively adjusted according to new highs, new lows and acceleration factors.
Advantages of this strategy:
1. The equalization line filters the noise and the PSAR captures the inversion. Combination improves accuracy.
2. PSAR parameters are adaptive and can respond to market changes.
3. The rules are clear and easy to implement, which is conducive to parameter optimization.
Risks of this strategy:
1. Both the equilibrium line and PSAR have hysteresis problems, and the best entry point may be missed.
2. PSAR is prone to produce false signals under a volatile trend.
3. Strict capital management is required to hedge the risk of reversal trading.
In short, this strategy uses the equilibrium line to determine the general trend, and PSAR to identify the specific entry point and perform trend tracking operations. Lagging problems and false reversal risks require vigilance, but long-term stable returns can be obtained through optimization.
||

This strategy combines Heikin-Ashi candlesticks and the PSAR indicator for trend identification and trade signals. It uses Heikin-Ashi noise filtering with PSAR for trend reversal detection, aiming to capture medium-long term trends.

Strategy Logic:

1. Calculate Heikin-Ashi open, close, high and low. 

2. Candle color determines interim bull/bear trend.

3. Calculate PSAR and identify trend reversal when it crosses Heikin-Ashi price.

4. Go long on PSAR downtrend and short on PSAR uptrend.

5. PSAR adapts based on new highs/lows and acceleration factor.

Advantages:

1. Combination improves accuracy - Heikin-Ashi filters noise, PSAR catches reversals.

2. Adaptive PSAR adjustable to changing market conditions.

3. Clear rules benefit parameter optimization.

Risks:  

1. Lagging Heikin-Ashi and PSAR may miss best entries.

2. PSAR prone to false signals in choppy trends.

3. Strict risk management needed to defend against whipsaws.

In summary, this strategy pairs Heikin-Ashi for trend context with PSAR for timing. Lag and false signals require caution but can be overcome through optimization for long-term steady gains.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|PSAR Start|
|v_input_2|0.02|PSAR Increment|
|v_input_3|0.2|PSAR Max|
|v_input_4|2018|Start Year|
|v_input_5|true|Start Month|
|v_input_6|true|Start Day|
|v_input_7|2100|End Year|
|v_input_8|true|End Month|
|v_input_9|true|End Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-12 00:00:00
end: 2023-09-11 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuantNomad - Heikin-Ashi PSAR Strategy", shorttitle = "HA-PSAR[QN]", overlay = false)

////////////
// INPUTS //

start      = input(0.02, title = "PSAR Start")
increment  = input(0.02, title = "PSAR Increment")
maximum    = input(0.2,  title = "PSAR Max")

start_year  = input(2018, 'Start Year',  input.integer)
start_month = input(1,    'Start Month', input.integer)
start_day   = input(1,    'Start Day',   input.integer)

end_year  = input(2100, 'End Year',  input.integer)
end_month = input(1,    'End Month', input.integer)
end_day   = input(1,    'End Day',   input.integer)

date_start = timestamp(start_year, start_month, start_day, 00, 00)
date_end   = timestamp(end_year,   end_month,   end_day,   00, 00)

// if time is in correct period
time_cond = time >= date_start and time <= date_end

// Calculation HA Values 
haopen  = 0.0
haclose = (open + high + low + close) / 4
haopen := na(haopen[1]) ? (open + close) / 2 : (haopen[1] + haclose[1]) / 2
hahigh  = max(high, max(haopen, haclose))
halow   = min(low,  min(haopen, haclose))

// HA colors
hacolor = haclose > haopen ? color.green : color.red

psar        = 0.0 // PSAR
af          = 0.0 // Acceleration Factor
trend_dir   = 0   // Current direction of PSAR
ep          = 0.0 // Extreme point
trend_bars  = 0

sar_long_to_short = trend_dir[1] == 1  and haclose <= psar[1] // PSAR switches from long to short
sar_short_to_long = trend_dir[1] == -1 and haclose >= psar[1] // PSAR switches from short to long

trend_change = barstate.isfirst[1] or sar_long_to_short or sar_short_to_long

// Calculate trend direction
trend_dir    := barstate.isfirst[1] and haclose[1] > haopen[1] ? 1 : 
   barstate.isfirst[1] and haclose[1] <= haopen[1] ? -1 : 
   sar_long_to_short ? -1 : 
   sar_short_to_long ?  1 : nz(trend_dir[1])

trend_bars := sar_long_to_short ? -1 : 
              sar_short_to_long ?  1 : 
              trend_dir ==  1   ? nz(trend_bars[1]) + 1 : 
              trend_dir == -1   ? nz(trend_bars[1]) - 1 : 
              nz(trend_bars[1])

// Calculate  Acceleration Factor
af := trend_change ? start : 
   (trend_dir == 1 and hahigh > ep[1]) or  
   (trend_dir == -1 and low < ep[1]) ? 
   min(maximum, af[1] + increment) : 
   af[1]

// Calculate extreme point
ep := trend_change and trend_dir == 1 ? hahigh :  
   trend_change and trend_dir == -1 ? halow : 
   trend_dir == 1 ? max(ep[1], hahigh) : 
   min(ep[1], halow)

// Calculate PSAR
psar := barstate.isfirst[1] and haclose[1] > haopen[1] ? halow[1] : 
   barstate.isfirst[1] and haclose[1] <= haopen[1] ? hahigh[1] : 
   trend_change ? ep[1] :    
   trend_dir == 1 ? psar[1] + af * (ep - psar[1]) : psar[1] - af * (psar[1] - ep) 

plotcandle(haopen, hahigh, halow, haclose, title = "HA", color = hacolor)
plot(psar, style=plot.style_cross, color=trend_dir == 1 ? color.green : color.red,  linewidth = 2)

// Strategy
strategy.entry("long",  true,  when = sar_short_to_long and time_cond)
strategy.entry("short", false, when = sar_long_to_short and time_cond)

```

> Detail

https://www.fmz.com/strategy/426489

> Last Modified

2023-09-12 15:16:17
