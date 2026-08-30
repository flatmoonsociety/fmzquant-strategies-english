
> Name

Moving-Average-Tracking-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/20d9c5b6ac78553a2170790c54438b360ef2cf5a7aa6587c89255efbe8d5ce5c.png)

[trans]

### Overview
This strategy is based on tracking the moving average and combining MACD indicator filtering to make trading decisions. Go long when the fast moving average crosses the slow moving average, go short when the fast moving average crosses below the slow moving average, and the MACD indicator can be used to filter out false breakthroughs.
### Strategy Principles
This strategy is mainly based on the following principles:
1. Use Heikin Ashi candle charts to filter market noise and identify trends.
2. If the fast moving average crosses the slow moving average, it means that the price has entered an upward trend, so go long; if it crosses below, it means that the price has entered a downward trend, so go short.
3. The MACD indicator can be used to identify price trends and filter out false breakthroughs. When the MACD histogram is greater than 0, it is a long market, and when it is less than 0, it is a short market.
4. Specifically, the strategy first calculates the opening and closing prices of Heikin Ashi candlesticks. Then calculate the fast EMA and slow EMA. Go long when the fast EMA crosses above the slow EMA, and go short when it crosses below. At the same time, it is combined with the MACD indicator to filter out false breakthrough signals.
### Strategic Advantages
1. Use Heikin Ashi candle charts to filter noise and help determine the trend direction.
2. The golden cross and dead cross system of fast and slow EMA is a mature trading strategy that can follow the trend.
3. Combined with the MACD indicator, it can filter out false breakthroughs and bring more accurate trading signals.
4. This strategy has a large space for parameter optimization, and can be optimized by adjusting the EMA period, MACD parameters, etc.
5. The strategy idea is simple and intuitive, easy to understand and implement, and is suitable for use in high-volatility digital currency markets.
### Strategy Risk
1. The strategy is only based on technical indicators and does not combine with fundamental analysis, which may lead to losses due to missing major news.
2. Improper EMA period setting may result in a large number of false signals, resulting in losses.
3. The MACD filtering effect depends on the parameter settings. Improper settings may not effectively filter out false breakthroughs.
4. Sudden rises and falls caused by unexpected events may cause the stop loss to be broken down and result in large losses.
5. It is difficult to set a stop loss in highly volatile market conditions, and there is a risk of expanding losses.
### Strategy optimization
1. Optimize the EMA cycle parameters and find the best parameter combination.
2. Optimize MACD parameters and improve the ability to identify trends.
3. Add other technical indicators to filter signals, such as RSI, KD, etc.
4. Determine the trading range based on trend lines, support and pressure levels, etc.
5. Adjust parameters according to the characteristics of different cryptocurrencies.
6. Add a stop loss strategy to control single losses.
### Summarize
The overall idea of ​​this strategy is clear and easy to understand, and better trading signals can be obtained through fast and slow EMA combined with MACD indicator filtering. However, there are certain systemic risks, which require parameter optimization and risk control. This strategy is suitable for highly volatile digital currency markets, but requires regular optimization and updates to maintain stable returns. Through continuous improvement, this strategy is expected to become a stable and profitable trend following strategy.
||


### Overview

This strategy is based on tracking moving averages combined with MACD indicator filtering for trade decision-making. It goes long when the fast moving average crosses above the slow moving average, and goes short when the fast MA crosses below the slow MA. Meanwhile, MACD indicator can be used to filter false breakouts.

### Strategy Logic

The strategy is mainly based on the following principles:

1. Using Heikin Ashi candles can filter market noise and identify trends. 

2. Fast MA crossing above slow MA indicates an upward trend, go long; crossing below indicates a downward trend, go short.

3. MACD indicator can identify price trends and filter false breakouts. MACD histogram above 0 indicates a bullish market, below 0 indicates a bearish market.

4. Specifically, the strategy first calculates the open and close prices of the Heikin Ashi candles. Then it calculates the fast and slow EMA lines. It goes long when fast EMA crosses above slow EMA, and goes short when fast EMA crosses below slow EMA. MACD indicator is used to filter false breakout signals.

### Advantages

1. Heikin Ashi candles can filter noise and help determine trend direction.

2. Fast and slow EMA cross system is a mature trading strategy that follows the trend. 

3. MACD filter provides more accurate trading signals by reducing false breakouts.

4. The strategy has large optimization space by adjusting EMA periods, MACD parameters etc.

5. Simple and intuitive strategy logic, easy to understand and implement, suitable for highly volatile crypto markets.

### Risks

1. The strategy relies solely on technical indicators without fundamental analysis, may miss major news events and cause losses.

2. Improper EMA period settings may generate excessive false signals and losses.

3. MACD filter depends on parameter tuning, improper settings may fail to filter false breakouts effectively.

4. Sudden price spikes may hit stop loss and cause large losses.

5. Difficult to set proper stop loss in volatile markets, risks of loss amplification.

### Optimization

1. Optimize EMA period parameters to find optimal combinations.

2. Optimize MACD parameters to improve trend identification ability. 

3. Add other technical indicators like RSI, KD etc. to filter signals.

4. Determine trading range based on trendlines, support/resistance levels etc.

5. Adjust parameters according to different crypto characteristics. 

6. Add stop loss strategies to control single trade loss amount.

### Summary

The strategy has clear and easy-to-understand logic. Trading signals can be obtained from fast/slow EMA cross and MACD filter. But there are inherent system risks that need parameter optimization and risk management. The strategy suits the highly volatile crypto markets but requires regular updates for steady profits. With continuous improvements, it has the potential to become a stable profitable trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|Heikin Ashi Candle Time Frame|
|v_input_2|true|Heikin Ashi Candle Time Frame Shift|
|v_input_3|180|Heikin Ashi EMA Time Frame|
|v_input_4|false|Heikin Ashi EMA Time Frame Shift|
|v_input_5|true|Heikin Ashi EMA Period|
|v_input_6|true|Heikin Ashi EMA Shift|
|v_input_7|10|Slow EMA Period|
|v_input_8|true|Slow EMA Shift|
|v_input_9|false|With MACD filter|
|v_input_10|12|MACD Time Frame|
|v_input_11|true|MACD Shift|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Heikin Ashi Strategy  V3 by breizh29

// strategy("Heikin Ashi Strategy  V3",shorttitle="HAS V3",overlay=true,default_qty_value=100,initial_capital=100,currency=currency.EUR) 
res = input(title="Heikin Ashi Candle Time Frame",  defval="30")
hshift = input(1,title="Heikin Ashi Candle Time Frame Shift")
res1 = input(title="Heikin Ashi EMA Time Frame",  defval="180")
mhshift = input(0,title="Heikin Ashi EMA Time Frame Shift")
fama = input(1,"Heikin Ashi EMA Period")
test = input(1,"Heikin Ashi EMA Shift")
sloma = input(10,"Slow EMA Period")
slomas = input(1,"Slow EMA Shift")
macdf = input(false,title="With MACD filter")
res2 = input(title="MACD Time Frame",  defval="12")
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

https://www.fmz.com/strategy/430040

> Last Modified

2023-10-24 14:39:08
