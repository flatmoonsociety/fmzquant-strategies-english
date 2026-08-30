
> Name

Heiken-Ashi-Moving-Average-Crossover-Strategy-with-MACD-Filter-V3 Heiken-Ashi-Moving-Average-Crossover-Strategy-with-MACD-Filter-V3
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1019fb6adcaf3a9e43a.png)

[trans]

## Overview
This strategy generates trading signals by calculating the moving average crossover of Hein Ash candles, and combines MACD as a filter condition to achieve a relatively stable trading system.
## Strategy Principle
1. Calculate the opening and closing prices of Hein Ash candles
2. Calculate fast moving average (EMA) and slow moving average (SMA)
3. When the fast moving average crosses the slow moving average, a buy signal is generated
4. When the fast moving average crosses below the slow moving average, a sell signal is generated
5. If MACD filtering is enabled, a buy signal will only be generated when the MACD column crosses the 0 axis above, and a sell signal will be generated only when the MACD column crosses the 0 axis below.
## Advantage Analysis
1. Hein-Ash candles can effectively filter out market noise and make moving average crossover signals more reliable.
2. Combined with moving averages of different periods, multiple confirmations can be used to avoid false breakthroughs
3. MACD filtering helps further avoid false signals and improve signal quality
4. Using Hein Ash candles to calculate the moving average can reduce Scientistå1⁄4 è ́±è ̄ã2022å1 ́11æ10æ¥10:33
This V3 version of the Hein Ash candle strategy generates trading signals by calculating the moving average crossover of Hein Ash candles, and combines MACD as a filter condition. It is greatly improved compared to the V1 and V2 versions.
Overall, this strategy has the following advantages:
1. Hein Ash candles can effectively filter out market noise, making moving average crossover signals clearer and more reliable.
2. Using a combination of fast and slow moving averages can avoid being deceived by false breakthroughs of a single moving average.
3. Adding the MACD filtering mechanism can further avoid false signals and improve the accuracy of entry.
4. Use moving averages of different periods to achieve confirmation of multiple time frames, which also improves the reliability of the signal.
5. Using Hein-Ash candles to calculate moving averages can reduce the retracement caused by ordinary K-lines.
6. The parameters of this strategy are set reasonably, the operation frequency is moderate, and stable returns can be obtained without high-frequency trading.
However, this strategy also has some risks that need to be noted:
1. In volatile market conditions, there may be repeated transactions with multiple position adjustments.
2. MACD as a filtering indicator may also fail, leading to the generation of false signals.
3. The moving average system is sensitive to parameter settings, so you need to carefully test the best parameter combination.
4. When holding positions for a long time, you need to pay attention to major market changes caused by emergencies.
5. It is still necessary to manually judge large-level trends to avoid losses caused by counter-trend trading.
In general, as a relatively mature moving average strategy, this strategy can obtain stable investment returns under the premise of reasonable parameter adjustment. However, traders still need to pay attention to risks, adjust positions in a timely manner, and use this strategy based on trend judgment.
||


## Overview

This strategy generates trading signals by calculating the moving average crossover of Heiken Ashi candles, combined with MACD as a filter condition. It implements a relatively stable trading system.

## Strategy Logic

1. Calculate the open and close prices of Heiken Ashi candles.

2. Calculate fast moving average (EMA) and slow moving average (SMA). 

3. When fast MA crosses above slow MA, a buy signal is generated.

4. When fast MA crosses below slow MA, a sell signal is generated.

5. If MACD filter is enabled, buy signals are only generated when MACD histogram crosses above 0 line, and sell signals are only generated when MACD histogram crosses below 0 line.

## Advantage Analysis 

1. Heiken Ashi candles effectively filter out market noise, making MA crossover signals more reliable.

2. Combining MAs of different periods avoids false breakouts from single MA. 

3. MACD filter further avoids false signals and improves signal quality.

4. Using Heiken Ashi to calculate MA reduces drawdowns from regular candles. 

5. The strategy has reasonable parameters and moderate trading frequency, allowing stable profits without high frequency trading.

## Risk Analysis

However, some risks need to be noticed:

1. Repeated position adjustments may occur in ranging markets.

2. MACD filter may fail in some cases, resulting in false signals.

3. MA systems are sensitive to parameter tuning, requiring careful optimization.

4. Long holding positions need to monitor events that may cause significant market changes. 

5. Manual judgement of major trends is still needed to avoid losses from counter-trend trading.

In conclusion, this is a relatively mature MA strategy that can provide steady profits with proper parameter tuning. But traders still need to watch out for risks, adjust positions accordingly, and combine trend analysis when applying it.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|60|Heikin Ashi Candle Time Frame|
|v_input_2|true|Heikin Ashi Candle Time Frame Shift|
|v_input_3|180|Heikin Ashi EMA Time Frame|
|v_input_4|false|Heikin Ashi EMA Time Frame Shift|
|v_input_5|true|Heikin Ashi EMA Period|
|v_input_6|true|Heikin Ashi EMA Shift|
|v_input_7|30|Slow EMA Period|
|v_input_8|true|Slow EMA Shift|
|v_input_9|false|With MACD filter|
|v_input_10|15|MACD Time Frame|
|v_input_11|true|MACD Shift|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-24 00:00:00
end: 2023-10-24 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Heiken-Ashi Strategy  V3 by wziel

// strategy("Heiken-Ashi Strategy  V3",shorttitle="WZIV3",overlay=true,default_qty_value=10000,initial_capital=10000,currency=currency.USD)
res = input(title="Heikin Ashi Candle Time Frame",  defval="60")
hshift = input(1,title="Heikin Ashi Candle Time Frame Shift")
res1 = input(title="Heikin Ashi EMA Time Frame",  defval="180")
mhshift = input(0,title="Heikin Ashi EMA Time Frame Shift")
fama = input(1,"Heikin Ashi EMA Period")
test = input(1,"Heikin Ashi EMA Shift")
sloma = input(30,"Slow EMA Period")
slomas = input(1,"Slow EMA Shift")
macdf = input(false,title="With MACD filter")
res2 = input(title="MACD Time Frame",  defval="15")
macds = input(1,title="MACD Shift")




//Heikin Ashi Open/Close Price
ha_t = heikinashi(syminfo.tickerid)
ha_open = security(ha_t, res, open[hshift])
ha_close = security(ha_t, res, close[hshift])
mha_close = security(ha_t, res1, close[mhshift])

//macd
[macdLine, signalLine, histLine] = macd(close, 12, 26, 9)
macdl = security(ha_t,res2,macdLine[macds])
macdsl= security(ha_t,res2,signalLine[macds])

//Moving Average
fma = ema(mha_close[test],fama)
sma = ema(ha_close[slomas],sloma)
plot(fma,title="MA",color=lime,linewidth=2,style=line)
plot(sma,title="SMA",color=red,linewidth=2,style=line)


//Strategy
golong =  crossover(fma,sma) and (macdl > macdsl or macdf == false )
goshort =   crossunder(fma,sma) and (macdl < macdsl or macdf == false )

strategy.entry("Buy",strategy.long,when = golong)
strategy.entry("Sell",strategy.short,when = goshort)




```

> Detail

https://www.fmz.com/strategy/430121

> Last Modified

2023-10-25 11:26:17
