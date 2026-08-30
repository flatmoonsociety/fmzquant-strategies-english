
> Name

Grid-Trading-Strategy-Based-on-Moving-Average-System
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d9708b4f9bcdcf41430012792c0fe13becda3e67b50af2c002fc63cc86b35c1e.png)
[trans]

### Overview
This strategy uses the moving average theory to build a grid trading system, judges the market trend through multiple JMA moving average combinations with different parameters, and starts grid trading at the turning point of the trend, aiming to obtain profits from the market's medium and long-term trend conversion.
### Strategy Principles
1. Use JMA moving averages ranging from 1 to 20 periods to form a moving average combination to determine the market trend. When the short-period moving average is higher than the long-period moving average, it is judged to be an upward trend; otherwise, it is a downward trend.
2. At the turning point of the trend, that is, when the short moving average crosses the long moving average from top to bottom or crosses the long moving average from bottom to bottom, start grid trading. In an upward trend, short orders are gradually established; in a downward trend, long orders are gradually established.
3. You can choose whether to filter by the K-line entity color. If enabled, you will only buy on the red K-line and sell on the green K-line. Otherwise, the color of the K-line will not be considered and you will only trade when the trend turns.
4. The stop loss method is trailing stop loss or expiration stop loss. Expiration stop loss refers to closing all positions at the end of the strategy operation cycle.
### Advantage Analysis
1. Using the moving average system to determine trends can effectively determine the turning point of the market's medium and long-term trends.
2. Grid trading can make profits from volatile markets when there is no clear trend. At the same time, stop loss can be configured to control risks.
3. JMA moving average parameters can be customized and optimized for different periods, with high flexibility.
4. You can choose whether to filter by K-line entity color to avoid being misled by false breakthroughs.
### Risk Analysis
1. In a market that fluctuates significantly and has no obvious trend, the risk of stop loss is greater.
2. Errors in the judgment of the moving average system may lead to errors in trading signals.
3. If K-line filtering is enabled, there is a risk that some trading opportunities may be missed.
4. If the grid spacing is set too large, sufficient profits cannot be obtained; if it is too small, there will be too many positions and high cost pressure.
### Optimization direction
1. You can test the parameters of more combinations and find JMA moving average combinations that are more suitable for different varieties.
2. Filter can be combined with other indicators, such as BOLL channel, KD, etc., to improve signal quality.
3. The configuration of grid trading can be optimized, such as grid spacing, number of positions and other parameters.
4. More types of stop loss methods can be considered, such as gap stop loss, trailing stop loss, etc.
### Summarize
This strategy uses the JMA moving average theory to determine trend turning points and start grid trading at the turning point. Profits can be obtained from the conversion of medium and long-term market conditions. Better strategy performance can be obtained through parameter optimization. Generally speaking, this strategy is suitable for mid- to long-term holdings and gradually follows the trend to make profits.
||

### Overview  

This strategy uses moving average theory to build a grid trading system by judging the market trend through multiple sets of JMA moving averages with different parameters. It aims to capture profits during long-term trend reversals in the market.

### Strategy Logic  

1. Use a combination of 1-20 period JMA moving averages to determine the market trend. When the short period MA is above the long period MA, it is judged as an upward trend, and vice versa as a downward trend.  

2. Open grid trades at trend reversal points, when the short MA crosses below or above the long MA. Establish short positions gradually during uptrends, and long positions during downtrends.

3. An option to filter based on candlestick color - only buy on red candles and sell on green candles, otherwise disregard color and trade at trend reversal only.  

4. Exits are either tracking stop loss or time-based exit when strategy duration ends.

### Advantage Analysis 

1. Using MA system to determine trends can effectively identify long-term trend reversals.  

2. Grid trading can capture profits from range-bound markets without clear trends, with stop loss to control risks.

3. Customizable JMA parameters, can optimize for different periods, high flexibility.  

4. Candle filter avoids being misled by false breakouts.

### Risk Analysis   

1. High whip saw markets without clear trends have higher stop loss risks.

2. Judgment errors from MA system may lead to incorrect trade signals.  

3. Candle filter risks missing some trading opportunities.

4. If grid spacing is too wide, insufficient profits; too narrow may result in too many positions and high costs.

### Optimization Directions  

1. Test more parameter combinations to find optimal JMA MA combinations for different products.  

2. Incorporate other filters like BOLL bands, KD etc to improve signal quality.

3. Optimize grid configurations like grid spacing, entry lots etc.  

4. Consider more stop loss methods like gap based, trailing stops etc.

### Conclusion  

This strategy judges reversals using JMA theory and opens grid trades at turning points to capture profits from long-term trend shifts. Performance can be further improved through parameter optimization. Overall it is suitable for medium-long term holdings to gradually track and profit from trending moves.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Lot|
|v_input_4|false|Use Color-filter|
|v_input_5|1900|From Year|
|v_input_6|2100|To Year|
|v_input_7|true|From Month|
|v_input_8|12|To Month|
|v_input_9|true|From day|
|v_input_10|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-27 00:00:00
end: 2024-01-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2019

//@version=3
strategy(title = "Noro's Fishnet Strategy", shorttitle = "Fishnet str", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot")
usecf = input(false, defval = false, title = "Use Color-filter")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//JMA
jmax(src, len) =>
    beta = 0.45*(len-1)/(0.45*(len-1)+2)
    alpha = pow(beta, 3)
    L0=0.0, L1=0.0, L2=0.0, L3=0.0, L4=0.0
    L0 := (1-alpha)*src + alpha*nz(L0[1])
    L1 := (src - L0[0])*(1-beta) + beta*nz(L1[1])
    L2 := L0[0] + L1[0]
    L3 := (L2[0] - nz(L4[1]))*((1-alpha)*(1-alpha)) + (alpha*alpha)*nz(L3[1])
    L4 := nz(L4[1]) + L3[0]
	L4

ma01 = jmax(close, 10)
ma02 = jmax(close, 20)
ma03 = jmax(close, 30)
ma04 = jmax(close, 40)
ma05 = jmax(close, 50)
ma06 = jmax(close, 60)
ma07 = jmax(close, 70)
ma08 = jmax(close, 80)
ma09 = jmax(close, 90)
ma10 = jmax(close, 100)
ma11 = jmax(close, 110)
ma12 = jmax(close, 120)
ma13 = jmax(close, 130)
ma14 = jmax(close, 140)
ma15 = jmax(close, 150)
ma16 = jmax(close, 160)
ma17 = jmax(close, 170)
ma18 = jmax(close, 180)
ma19 = jmax(close, 190)
ma20 = jmax(close, 200)

trend = 0
trend := ma01 > ma20 ? 1 : ma01 < ma20 ? -1 : trend[1]
col = trend == 1 ? #00FF7F : #DC143C

plot(ma01, transp = 0, color = col)
plot(ma02, transp = 0, color = col)
plot(ma03, transp = 0, color = col)
plot(ma04, transp = 0, color = col)
plot(ma05, transp = 0, color = col)
plot(ma06, transp = 0, color = col)
plot(ma07, transp = 0, color = col)
plot(ma08, transp = 0, color = col)
plot(ma09, transp = 0, color = col)
plot(ma10, transp = 0, color = col)
plot(ma11, transp = 0, color = col)
plot(ma12, transp = 0, color = col)
plot(ma13, transp = 0, color = col)
plot(ma14, transp = 0, color = col)
plot(ma15, transp = 0, color = col)
plot(ma16, transp = 0, color = col)
plot(ma17, transp = 0, color = col)
plot(ma18, transp = 0, color = col)
plot(ma19, transp = 0, color = col)
plot(ma20, transp = 0, color = col)

//Trading
lot = 0.0
lot := strategy.equity / close * capital / 100

if trend == 1 and (close < open or usecf == false)
    strategy.entry("Long", strategy.long, needlong ? lot : na)

if trend == -1 and (close > open or usecf == false)
    strategy.entry("Short", strategy.short, needshort ? lot : na)
    
```

> Detail

https://www.fmz.com/strategy/437558

> Last Modified

2024-01-03 17:18:22
