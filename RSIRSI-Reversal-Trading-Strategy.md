
> Name

RSI advance and exit two-way trading strategy RSI-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the RSI indicator to determine market trends and send trading signals in overbought and oversold areas, aiming to capture the market's short-term adjustment trends. It combines moving average indicators and stop-profit and stop-loss logic to filter trading signals and control risks.
## Strategy Principle
1. Calculate the RSI(14) indicator value and set the overbought line to 67 and the oversold line to 44.
2. When the RSI goes above the overbought line, a sell signal is issued; when the RSI goes below the oversold line, a buy signal is issued.
3. Superimpose moving average filtering. Only when the closing price is lower than yesterday's average price, a sell signal will be issued when the RSI is overbought; only when the closing price is higher than yesterday's average price, a buy signal will be issued when the RSI is oversold.
4. Set take profit and stop loss logic. You can choose a fixed number of points to take profit and stop loss, or take profit based on the RSI value.
## Advantage Analysis
1. Use the RSI indicator to determine overbought and oversold conditions and capture short-term adjustment opportunities.
2. Use moving averages to filter to avoid reverse operations in trending markets.
3. Set up stop-profit and stop-loss to control single losses.
4. Capture reversal opportunities on the eve of a trend reversal.
## Risks and Solutions
1. RSI has hysteresis and may divergence resulting in false signals. The solution is to adjust the parameters appropriately or use them in combination with other indicators.
2. The fixed stop loss may be too large or too small. You can choose a more flexible trailing stop dynamic stop loss.
3. The fixed take profit may be taken too early or the take profit point is too small. Consider taking profit based on RSI value or ATR.
4. Unable to effectively filter the volatile trend market, which may lead to frequent opening of positions and losses. RSI parameters can be adjusted appropriately or other filtering conditions added.
## Optimization direction
1. Test the RSI indicator effects of different period parameters.
2. Adjust the parameters of RSI and test different overbought and oversold lines.
3. Try different types of moving averages or other filtering indicators.
4. Test the effects of fixed take-profit and stop-loss and dynamic take-profit and stop-loss.
5. Optimize the values ​​of take profit and stop loss to make them more in line with the law of market fluctuations.
6. Add entry filter conditions to avoid opening positions in volatile market conditions.
7. Consider combining multiple time periods for verification to improve signal quality.
## Summarize
This strategy uses the RSI indicator to determine overbought and oversold conditions, and combines moving averages and take-profit and stop-loss for two-way trading. Market reversal opportunities can be captured in the short term. After parameter optimization and filtering conditions are supplemented, the profit effect of the strategy can be further improved and risks can be controlled. This strategy is suitable for investors who are sensitive to short-term changes and pursue high-frequency trading.
||

## Overview

This strategy uses the RSI indicator to judge market trends and generate trading signals when overbought or oversold conditions occur. It aims to capture short-term reversal moves in the market. It also incorporates moving averages and profit-taking/stop-loss logic to filter signals and control risks.

## Strategy Logic

1. Calculate 14-period RSI and set overbought line at 67 and oversold line at 44. 

2. When RSI crosses above overbought line, a sell signal is generated. When RSI crosses below oversold line, a buy signal is generated.

3. Add moving average filter. Sell signals only occur when close is below previous day's MA; Buy signals only occur when close is above previous day's MA.

4. Incorporate profit-taking and stop-loss logic. Either fixed points or RSI-based exits can be used.

## Advantage Analysis 

1. Captures short-term reversal opportunities using RSI overbought/oversold levels.

2. Moving average filter avoids trading against the trend. 

3. Profit-taking and stop-loss controls single trade loss.

4. Can catch trend reversal opportunities early.

## Risks and Solutions

1. RSI lag may cause false signals. Adjust parameters or combine with other indicators.

2. Fixed stop-loss may be too wide or too narrow. Consider trailing stop.

3. Fixed profit-taking may exit too early or target too small. Consider RSI or ATR based exits.

4. Fails to filter ranging markets, causing over-trading and losses. Adjust RSI parameters or add filters.

## Optimization Directions

1. Test RSI parameters on different timeframes.

2. Adjust overbought/oversold RSI levels. 

3. Try different moving averages or other filters.

4. Test fixed versus dynamic profit targets/stops.

5. Optimize profit/stop values to fit market volatility.

6. Add filters to avoid whipsaws in ranging markets.

7. Consider multiple timeframe confluence to improve signal quality.

## Summary

This strategy trades reversals using RSI combined with moving averages and profit-taking/stop-loss logic. It aims to capture short-term turns in the market. Further parameter optimization and additional filters can improve profitability while reducing risks. It suits investors who are sensitive to short-term moves and seek frequent trading.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|length|
|v_input_2|44|overSold|
|v_input_3|67|overBought|
|v_input_4|0.0576923077|AvgPrice - n|
|v_input_5|false|Тейк-профіт по RSI|
|v_input_6|73|RSI тейк по лонгу|
|v_input_7|44|RSI тейк по шорту|
|v_input_8|250|Маржа|
|v_input_9|3|Плече|
|v_input_10|false|Тейк-профіт|
|v_input_11|4500|Тейк-профіт у тіках|
|v_input_12|false|Стоп-лосс|
|v_input_13|false|Стоп-лосс у тіках|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2023-09-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//© профешинил хомячело
//@version = 4

strategy("RSI Strategy Professional Хомячело", overlay=false)
length = input( 14 )
overSold = input( 44 )
overBought = input( 67 )
price = open
rsi = rsi(price, length)
band1 = hline(overSold, "overSold12", color=#C0C0C0)
band0 = hline(overBought, "overBought12", color=#C0C0C0)
plot(rsi, "RSI", color=color.red)
fill(band1, band0, color=color.black, transp=90, title="Background")
src = close
a = sma(src, 1)
aaa = strategy.opentrades + 1

n = input(defval = 0.0576923077, title = "AvgPrice - n")
//n = 0.0576923077

buysignal = crossover(rsi, overSold) and (a < (strategy.position_avg_price - n) or strategy.opentrades == 0)
sellsignal = crossunder(rsi, overBought) and (a > (strategy.position_avg_price + n) or strategy.opentrades == 0)


// crossover(rsi, overSold)
// crossunder(rsi, overBought)
if (not na(rsi))
    if(buysignal)
        strategy.entry("LONG", strategy.long, comment = tostring(a) + "\n(" + tostring(aaa) + ")")
        n += 1000
    if(sellsignal)
        strategy.entry("SHORT", strategy.short, comment = tostring(a) + "\n(" + tostring(aaa) + ")")
        n += 1000

//лонги орні       
    if(rsi < 15 and strategy.opentrades != 5 and a < (strategy.position_avg_price - n))
        strategy.entry("LONG", strategy.long, comment = "ЙОБАНИЙ НАСРАВ ТА БЕРИ ЛОНГ НА ВСЬО ШО Є НАХУЙ\n" + tostring(a) + "\n(" + tostring(aaa) + "!!!)")
    if(rsi < 20 and strategy.opentrades != 5 and a < (strategy.position_avg_price - n))
        strategy.entry("LONG", strategy.long, comment = "ЛОНГ НА ВСЮ КОТЛЄТУ\n" + tostring(a) + "\n(" + tostring(aaa) + "!!!)")
//шорти орні
    if(rsi > 85 and strategy.opentrades != 5 and a < (strategy.position_avg_price - n))
        strategy.entry("SHORT", strategy.short, comment = "ЙОБАНИЙ НАСРАВ ТА БЕРИ ШОРТ НА ВСЬО ШО Є НАХУЙ\n" + tostring(a) + "\n(" + tostring(aaa) + "!!!)")
    if(rsi > 80 and strategy.opentrades != 5 and a < (strategy.position_avg_price - n))
        strategy.entry("SHORT", strategy.short, comment = "ШОРТ НА ВСЮ КОТЛЄТУ\n" + tostring(a) + "\n(" + tostring(aaa) + "!!!)")


//стоп-лосс і ціль

//rsi
rsion = input(defval = false, title = "Тейк-профіт по RSI")
rcl = input(defval = 73.0, title = "RSI тейк по лонгу")
rcs = input(defval = 44.0, title = "RSI тейк по шорту")
possize = input(defval = 250.0, title = "Маржа")
posp = input(defval = 3.0, title = "Плече")

//tick
ut = input(defval = false, title = "Тейк-профіт")
tar = input(defval = 4500.0, title = "Тейк-профіт у тіках")
us = input(defval = false, title = "Стоп-лосс")
stop = input(defval = 0.0, title = "Стоп-лосс у тіках")
tar:=tar/syminfo.mintick
stop:=stop/syminfo.mintick

if(ut==true and us==false)
    strategy.exit(id="LX", from_entry = "LONG", profit = tar, comment = "ТейкL")
    strategy.exit(id="SX", from_entry = "SHORT", profit = tar, comment = "ТейкS")
if(us==true and ut==false)
    strategy.exit(id="LX", from_entry = "LONG", loss = stop, comment = "СтопL")
    strategy.exit(id="SX", from_entry = "SHORT", loss = stop, comment = "СтопS")
    
if(ut==true and us==true)
    strategy.exit(id="LX", from_entry = "LONG", profit = tar, loss = stop, comment ="Тейк/СтопL")
    strategy.exit(id="SX", from_entry = "SHORT", profit = tar, loss = stop, comment ="Тейк/СтопS")
    
//закриття по rsi
if(rsion == 1 )
    pr = round(((a / strategy.position_avg_price - 1) * possize * posp), 2)
    ppr = round(((a / strategy.position_avg_price - 1) * 100 * posp), 2)
    spr = round((1 - (a / strategy.position_avg_price)) * possize * posp, 2)
    sppr = round((100 - (a / strategy.position_avg_price * 100)) * posp, 2)
    
    if(rsi > rcl)
        strategy.close(id="LONG", comment = "LT\n" + tostring(ppr) + "%\n" + tostring(pr) + "$\n" + tostring(a))
    if(rsi < rcs)
        strategy.close(id="SHORT", comment = "ST\n" + tostring(sppr) + "%\n" + tostring(spr) + "$\n" + tostring(a))
```

> Detail

https://www.fmz.com/strategy/428101

> Last Modified

2023-09-28 16:09:39
