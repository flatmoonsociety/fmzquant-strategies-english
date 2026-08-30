
> Name

RSI Momentum Reversal Strategy RSI-Momentum-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/e9b6d4c9bb6862aae3ef8fc988792fef8eeb537000ddbe7753c3b6943ca56e23.png)

[trans]

## Overview
The RSI momentum reversal strategy combines the RSI indicator and the direction of the K-line entity to identify overbought and oversold phenomena and conduct reversal trades. This strategy uses both regular RSI and fast RSI, and cooperates with K-line entity filtering to effectively identify reversal opportunities.
## Strategy Principle
This strategy is mainly implemented through the following parts:
1. Connors RSI Indicator
Calculate the conventional RSI, RSI winning rate indicator, and RSI Paris Chart indicator, and take the average of the three as Connors RSI.
2. Fast RSI indicator
Use price movements to calculate fast RSI, reflecting ultra-short-term cycles.
3. K-line entity filtering
It is necessary to go long on the positive line of the entity and short on the negative line to prevent false breakthroughs.
4. Long and short conditions
When the Connors RSI is below 20, and when the fast RSI is below 25, the real positive line appears, go long.
When the Connors RSI is higher than 80, and when the fast RSI is higher than 75, the physical negative line appears, and you go short.
5. Stop loss and exit
Stop loss and exit when the real body turns.
Use Connors RSI to determine the long-term trend reversal point, fast RSI to determine the short-term reversal point, and the K-line entity to ensure the effectiveness of the breakthrough. In this way, reversal opportunities can be effectively discovered, and positions can be opened promptly for reverse operations when overbought or oversold.
## Advantage Analysis
This strategy has the following advantages:
1. Combined with long and short-term indicators
Connors RSI reflects long-term cycles, and fast RSI reflects short-term cycles. The combination of the two can more accurately determine the reversal point.
2. Entity filtering
Only operating when the entity breaks through can reduce losses caused by false breakthroughs.
3. Adjustable parameters
RSI parameters, trading varieties, and trading time periods can be freely adjusted to adapt to different markets.
4. Simple and intuitive
RSI and K-line entities are both basic indicators, and the strategy logic is simple and easy to understand.
5. Easy to implement
Only built-in indicators are used, the amount of code is small, and the implementation difficulty is low.
## Risk Analysis
This strategy faces the following main risks:
1. Risk of reversal failure
After the reversal signal is sent, the price continues to run in the original trend, resulting in losses.
2. Risk of volatile market conditions
Signals are triggered repeatedly during volatile market conditions, resulting in too many invalid transactions.
3. Risk of false breakthrough breakthrough
Entity filtering cannot completely avoid false breakouts.
4. Parameter setting risks
Improper setting of RSI parameters may result in missed trading opportunities or multiple invalid transactions.
5. Special market risk
In special market conditions, the RSI indicator fails and generates wrong signals.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add stop loss mechanism
Optimize the stop loss strategy to make the stop loss more reasonable and reduce the loss of a single transaction.
2. Integrate multiple indicators
Add MACD, KD and other indicator filters to make signals more reliable.
3. Add probability filtering
Judge the probability based on trends, support and resistance, etc. to avoid low-probability transactions.
4. Optimize parameter settings
Conduct parameter testing for different trading varieties and cycles to find the optimal parameters.
5. Avoid special market conditions
Identify special market conditions, suspend trading, and avoid huge losses.
## Summarize
The RSI momentum reversal strategy uses Connors RSI and fast RSI to determine long and short-term reversals, and cooperates with K-line entity filtering to increase signal effectiveness. This strategy has the advantages of indicator combination and flexible parameter adjustment. It can capture reversal opportunities and intervene in transactions promptly when overbought and oversold. However, this strategy also has certain risks such as reversal failure and false breakthroughs. It is necessary to further optimize stop losses, indicator combinations, etc. to reduce risks and improve profitability.
||


## Overview

The RSI momentum reversal strategy identifies overbought and oversold conditions by combining RSI indicators and candlestick body directions for reversal trading. This strategy uses both conventional RSI and fast RSI, along with candlestick body filters, to effectively identify reversal opportunities.

## Strategy Logic

The strategy is mainly implemented through the following parts:

1. Connors RSI indicator

    Calculates conventional RSI, RSI Win Ratio, and RSI Parisian to get Connors RSI as an average.

2. Fast RSI indicator

    Uses price changes to calculate fast RSI, reflecting ultra short-term cycles.

3. Candlestick body filter

    Requires bullish body for long and bearish body for short to prevent false breakouts. 

4. Long and short conditions

    Go long when Connors RSI below 20 and fast RSI below 25 with bullish body.

    Go short when Connors RSI above 80 and fast RSI above 75 with bearish body.

5. Stop loss exit

    Exits with stop loss when candlestick body turns around.

Connors RSI identifies long-term trend reversal points, fast RSI identifies short-term reversals, and candlestick body ensures the validity of breakouts. This allows effectively detecting reversal opportunities and making counter-trend trades during overbought and oversold conditions.

## Advantage Analysis

The advantages of this strategy include:

1. Combining long and short-term indicators

    Connors RSI reflects long-term cycles and fast RSI reflects short-term cycles, combining both can accurately identify reversal points.

2. Candlestick body filter

    Trading only on body breakouts can reduce losses from false breakouts.

3. Adjustable parameters

    RSI parameters, trading products, and trading time frames can be freely adjusted to suit different markets.

4. Simple and intuitive

    RSI and candlestick body are basic indicators, easy-to-understand logic. 

5. Easy to implement

    Uses built-in indicators only, requiring little code and easy to implement.

## Risk Analysis

The main risks of this strategy:

1. Failed reversal risk

    Price continues the original trend after reversal signal, leading to losses.

2. Ranging market risk

    Frequent ineffective signals triggered in ranging markets.

3. False breakout risk

    Candlestick body filter cannot completely avoid false breakouts. 

4. Parameter risk

    Inappropriate RSI parameters may miss trades or trigger multiple ineffective trades.

5. Special market conditions risk

    RSI indicators may fail and generate incorrect signals in special market conditions.

## Optimization Directions

The strategy can be optimized from the following aspects:

1. Add stop loss mechanisms

    Optimize stop loss strategies for more reasonable stops, reducing single trade losses.

2. Integrate multiple indicators

    Add filters like MACD and KD to make signals more reliable.

3. Add probability filters

    Combine trend, support/resistance analysis to avoid low probability trades.

4. Optimize parameter settings

    Test parameters on different products and time frames to find optimum values.

5. Avoid special market conditions

    Identify and avoid trading in special market conditions to prevent huge losses.

## Conclusion

The RSI momentum reversal strategy identifies long and short-term reversals using Connors RSI and fast RSI, with candlestick body filters to increase signal validity. The advantages like indicator combinations and adjustable parameters allow capturing reversals and trading counter-trend when overbought or oversold. But risks like failed reversals and false breakouts remain, requiring further optimizations in stop loss, indicator combinations to reduce risks and improve profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|false|Use Martingale|
|v_input_4|100|Capital, %|
|v_input_5|true|Use CRSI Strategy|
|v_input_6|true|Use FRSI Strategy|
|v_input_7|true|CRSI+FRSI Mode|
|v_input_8|25|RSI limit|
|v_input_9|true|Use Body-filter|
|v_input_10|true|Use Color-filter|
|v_input_11|1900|From Year|
|v_input_12|2100|To Year|
|v_input_13|true|From Month|
|v_input_14|12|To Month|
|v_input_15|true|From day|
|v_input_16|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-07 00:00:00
end: 2023-11-06 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's Connors RSI Strategy v1.0", shorttitle = "CRSI str 1.0", overlay = false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 10)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
usemar = input(false, defval = false, title = "Use Martingale")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
usecrsi = input(true, defval = true, title = "Use CRSI Strategy")
usefrsi = input(true, defval = true, title = "Use FRSI Strategy")
usemod = input(true, defval = true, title = "CRSI+FRSI Mode")
limit = input(25, defval = 25, minval = 1, maxval = 100, title = "RSI limit")
usebod = input(true, defval = true, title = "Use Body-filter")
usecol = input(true, defval = true, title = "Use Color-filter")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//CRSI
rsilen = 3
streaklen = 2
lookback = 100
rsi = rsi(close,rsilen)
upday = close > close[1] ? 1 : 0
downday = close < close[1] ? -1 : 0
upstreak = upday!=0 ? upstreak[1] + upday : 0
downstreak = downday!=0 ? downstreak[1] + downday : 0
streak = upstreak + downstreak
streakrsi = rsi(streak,streaklen)
roc = close/close[1] - 1
roccount = 0
for i=1 to lookback-1
    roccount := roc[i]<roc ? roccount + 1 : roccount
crsi = (rsi + streakrsi + roccount) / 3

//Oscilator
// rsiplot = plot(crsi, title="RSI", style=line, linewidth=1, color=blue)
// band1 = hline(80, title="Upper Line", linestyle=dashed, linewidth=1, color=red)
// band0 = hline(20, title="Lower Line", linestyle=dashed, linewidth=1, color=green)
// fill(band1, band0, color=purple, transp=90)

//Fast RSI
fastup = rma(max(change(close), 0), 7)
fastdown = rma(-min(change(close), 0), 7)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Body Filter
nbody = abs(close - open)
abody = sma(nbody, 10)
body = nbody > abody / 3 or usebod == false

//Color Filter
bar = close > open ? 1 : close < open ? -1 : 0
gbar = bar == 1 or usecol == false
rbar = bar == -1 or usecol == false

//Signals

up1 = rbar and (strategy.position_size == 0 or close < strategy.position_avg_price) and crsi < limit and body and usecrsi
dn1 = gbar and (strategy.position_size == 0 or close > strategy.position_avg_price) and crsi > 100 - limit and body and usecrsi
up2 = rbar and (strategy.position_size == 0 or close < strategy.position_avg_price) and fastrsi < limit and body and usefrsi
dn2 = gbar and (strategy.position_size == 0 or close > strategy.position_avg_price) and fastrsi > 100 - limit and body and usefrsi
exit = ((strategy.position_size > 0 and bar == 1) or (strategy.position_size < 0 and bar == -1)) and body

//Trading
profit = exit ? ((strategy.position_size > 0 and close > strategy.position_avg_price) or (strategy.position_size < 0 and close < strategy.position_avg_price)) ? 1 : -1 : profit[1]
mult = usemar ? exit ? profit == -1 ? mult[1] * 2 : 1 : mult[1] : 1
lot = strategy.position_size == 0 ? strategy.equity / close * capital / 100 * mult : lot[1]

if ((up1 or up2) and usemod == false) or (up1 and up2 and usemod)
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot)

if ((dn1 or dn2) and usemod == false) or (dn1 and dn2 and usemod)
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot)
    
if  exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/431401

> Last Modified

2023-11-07 15:45:15
