
> Name

Gradient-MACD-Quant-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12c8a3c1c6306ad467a.png)
[trans]

### Overview
This strategy calculates Heikin-Ashi candle lines, smooths K-line prices, and combines MACD indicators to send trading signals to achieve a quantitative trading strategy that tracks medium and long-term trends.
### Strategy Principles
1. Calculate the Heikin-Ashi opening price, closing price, highest price, and lowest price, draw the Heikin-Ashi candle line, and smooth the K-line price trend.
2. Set MACD parameters: fast line length 12, slow line length 26, signal line length 9.
3. Calculate the difference between DEA slow line, DEA fast line and MACD. Draw a MACD histogram.
4. When the MACD difference crosses above 0, go long; when the MACD difference crosses below 0, go short.
5. Set year, month, and day filter conditions to only trade within the specified time period.
### Advantage Analysis
1. Heikin-Ashi candle lines can effectively filter out market noise and identify trends.
2. MACD can provide a clearer trend buying and selling point.
3. Combining Heikin-Ashi and MACD can improve the quality of buying and selling points and increase profitable trades.
4. Set time filter conditions to determine the best trading period based on historical data backtesting and improve profitability.
### Risk Analysis
1. When the trend reverses, large losses may occur.
2. Improper MACD parameter settings can generate too many invalid signals.
3. The time filtering conditions are too rigid and may miss better trading opportunities.
Countermeasures:
1. Set stop loss and stop profit to control single loss.
2. Optimize MACD parameters and determine the best parameter combination.
3. Combine with other indicators to determine local trends.
### Optimization direction
1. Test different parameter combinations to find the optimal parameters.
2. Add a stop loss mechanism, such as leaving a stop loss/trailing stop loss.
3. Combine with EMA, KDJ and other indicators to determine the reversal point.
4. Add quantity and energy indicators to avoid quantity and energy divergence.
### Summarize
This strategy implements a quantitative strategy based on trend tracking by calculating the Heikin-Ashi candle line smoothing price and using the MACD Tradingview indicator to determine the trend direction and entry point. Compared with the ordinary MACD strategy, it smoothes the price curve, filters out some noise, and can judge the trend direction more clearly. Through the combination of parameter optimization, stop loss mechanism, and other indicators, the stability and profitability of the strategy can be further enhanced.
||


### Overview  

This strategy calculates Heikin-Ashi candlesticks to smooth price lines and combines MACD indicator to generate trading signals, implementing a quantitative strategy that tracks medium-to-long term trends.

### Strategy Logic   

1. Calculate Heikin-Ashi open, close, high and low prices to plot Heikin-Ashi candlesticks and smooth price trends.  

2. Set MACD parameters: fast length 12, slow length 26, signal length 9.

3. Calculate DEA slow line, DEA fast line and MACD histogram. Plot MACD histogram.

4. Go long when MACD histogram crosses above 0; Go short when crossing below 0.

5. Add year, month and day filters to limit trading to specified time range.

### Advantage Analysis   

1. Heikin-Ashi candlesticks filter out market noise effectively to identify trends. 

2. MACD provides clear trend trading signals.  

3. Combining Heikin-Ashi and MACD improves signal quality and profitability.

4. Time filters help optimize trading schedule based on historical performance.

### Risk Analysis

1. Potential large losses during trend reversal.  

2. Improper MACD parameters may generate excessive worthless signals. 

3. Rigid time filters may miss good trading opportunities.

Countermeasures:  

1. Set stop loss/take profit to limit losses.

2. Optimize MACD parameters to determine best combination.  

3. Add indicators to determine local trends. 

### Optimization Directions   

1. Test different parameter combinations to find optimum.  

2. Add stop loss mechanisms like trailing stop loss.

3. Add indicators like EMA, KDJ to determine reversal points. 

4. Add volume indicators to avoid divergence.

### Summary
This strategy smoothes price action with Heikin-Ashi candlesticks and determines trend direction and entry signals with MACD Tradingview indicator to implement a trend-following quant strategy. Compared with regular MACD strategies, it filters out some noise for clearer trend identification. Further enhancements on parameter optimization, stop loss, and combo indicators can improve its stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|MACD Fast  Line Length|
|v_input_2|26|MACD Slow Line Length|
|v_input_3|9|Signal Line Length|
|v_input_4|2020|yearfrom|
|v_input_5|2042|yearuntil|
|v_input_6|true|monthfrom|
|v_input_7|12|monthuntil|
|v_input_8|true|dayfrom|
|v_input_9|31|dayuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-18 00:00:00
end: 2023-12-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("MACD ASHI BARS .v1 ", overlay=false,default_qty_type = strategy.percent_of_equity, default_qty_value = 100,commission_type=strategy.commission.percent,commission_value=0.1,slippage=1)

// Calculation HA Values 
haopen  = 0.0
haclose = (open + high + low + close) / 4
haopen := na(haopen[1]) ? (open + close) / 2 : (haopen[1] + haclose[1]) / 2
hahigh  = max(high, max(haopen, haclose))
halow   = min(low,  min(haopen, haclose))

// HA colors
hacolor = haclose > haopen ? color.green : color.red
src=haclose



fastmacd = input(12,title='MACD Fast  Line Length')
slowmacd = input(26,title='MACD Slow Line Length')
signalmacd = input(9,title='Signal Line Length')

macdslowline1 = sma(src,slowmacd)
macdslowline2 = sma(macdslowline1,slowmacd)
DEMAslow = ((2 * macdslowline1) - macdslowline2 )

macdfastline1 = sma(src,fastmacd)
macdfastline2 = sma(macdfastline1,fastmacd)
DEMAfast = ((2 * macdfastline1) - macdfastline2)

MACDLine = (DEMAfast - DEMAslow)

SignalLine = sma(MACDLine, signalmacd)

delta = MACDLine-SignalLine




swap1 = delta>0?color.green:color.red



plot(delta,color=swap1,style=plot.style_columns,title='Histo',histbase=0,transp=20)
p1 = plot(MACDLine,color=color.blue,title='MACD Line')
p2 = plot(SignalLine,color=color.red,title='Signal')
fill(p1, p2, color=color.blue)
hline(0)



yearfrom = input(2020)
yearuntil =input(2042)
monthfrom =input(1)
monthuntil =input(12)
dayfrom=input(1)
dayuntil=input(31)







if ( crossover(delta,0)  and   year >= yearfrom and year <= yearuntil and month>=monthfrom and month <=monthuntil and dayofmonth>=dayfrom and dayofmonth < dayuntil) 
    strategy.entry("MMAL", strategy.long, stop=close, oca_name="TREND",  comment="AL")
    
else
    strategy.cancel(id="MMAL")


if (  crossunder(delta,0) and  year >= yearfrom and year <= yearuntil and month>=monthfrom and month <=monthuntil and dayofmonth>=dayfrom and dayofmonth < dayuntil ) 

    strategy.entry("MMSAT", strategy.short,stop=close, oca_name="TREND",  comment="SAT")
else
    strategy.cancel(id="MMSAT")
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    

```

> Detail

https://www.fmz.com/strategy/435901

> Last Modified

2023-12-19 16:14:50
