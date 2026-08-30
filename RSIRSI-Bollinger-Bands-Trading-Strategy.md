
> Name

RSI and Bollinger Bands Quantitative Strategy RSI-Bollinger-Bands-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/808214f3e18630a2f0ecab91738af3c1ea12b70553833804648994173094d528.png)
[trans]

### Overview
This strategy mainly uses the Relative Strength Index (RSI) and Bollinger Bands to judge trading signals. Specifically, it is to go long when the RSI low crosses the lower track of the Bollinger Bands, and to go short when the RSI high crosses the upper Bollinger Band.
### Strategy Principle
The strategy starts by calculating the RSI indicator and Bollinger Bands. The RSI indicator reflects the relative strength of the trading product. When the RSI is lower than the oversold zone (default 30), it means that the trading product is in the oversold zone. Buy at this time. Bollinger Bands include the upper track, middle track and lower track, which can well reflect the price fluctuation range. Buying near the lower track of Bollinger Bands and selling near the upper track can obtain relatively stable signals. This strategy combines the RSI indicator with the Bollinger Bands to determine trading signals. When the RSI indicator rises from the oversold zone to above the oversold zone (default 30), and the price rises from below the Bollinger Bands lower track to above the Bollinger Bands lower track, a buy signal is generated; when the RSI indicator drops from the overbought zone to below the overbought zone (default 70), and the price drops from above the Bollinger Bands upper track to below the Bollinger Bands upper track, a sell signal is generated.
### Strategic Advantages
1. Combine RSI indicator and Bollinger Bands to improve the accuracy of signal judgment
2. The RSI indicator filters out some noise signals
3. Bollinger Bands reflect the general range of current market fluctuations, and the signals are relatively reliable.
4. The trading strategy is strict to avoid invalid transactions.
### Strategy Risk
1. Improper setting of Bollinger Band parameters may make trading signals inaccurate
2. Improper setting of RSI overbought and oversold zone parameters may also affect signal judgment.
3. The strategy is strict and some trading opportunities may be missed.
Risk resolution:
1. Optimize Bollinger Bands parameters and RSI parameters to find the best parameter combination
2. Appropriately relax the trading conditions of the strategy and add a certain amount of invalid transactions to obtain more opportunities
### Strategy optimization direction
1. Test and optimize RSI parameters and Bollinger Band parameters to find the optimal parameters
2. Add stop-loss strategies to control trading risks
3. Consider adding other technical indicators for signal verification, such as MACD, etc.
4. Test the parameter optimization effects of different varieties and time periods

### Summary
This strategy is relatively stable overall and effectively combines the RSI indicator and Bollinger Bands stop loss. Through testing and optimizing parameters, the effectiveness of the strategy can be further improved. At the same time, you also need to be alert to the risk of signal loss that may arise due to stricter strategies. Overall, this strategy is a reliable quantitative trading strategy.
||

### Overview
This strategy mainly uses the Relative Strength Index (RSI) combined with Bollinger Bands for trading signal judgment. Specifically, it goes long when the RSI crosses above the oversold level and below the lower Bollinger Band, and goes short when the RSI crosses below the overbought level and above the upper Bollinger Band.  

### Strategy Logic
The strategy first calculates the RSI indicator and Bollinger Bands. The RSI indicator reflects the relative strength of the trading instrument. When the RSI is below the oversold zone (default 30), it means the instrument is oversold and should buy. Bollinger Bands include upper band, middle band and lower band, which reflects well the fluctuation range of prices. Buying near the lower band and selling near the upper band can provide relatively reliable signals. This strategy combines the RSI indicator and Bollinger Bands for trading signal judgment. It generates buy signal when the RSI rises from the oversold zone to above it (default 30), and price rises from below the lower band to above it; it generates sell signal when the RSI falls from the overbought zone to below it (default 70), and price falls from above the upper band to below it.

### Advantages
1. Combining RSI and Bollinger Bands improves signal accuracy  
2. RSI filters out some noise  
3. Bollinger Bands reflect current market volatility range, reliable signals
4. Strict trading rules, avoids invalid trades

### Risks
1. Improper Bollinger Bands parameters may cause inaccurate signals
2. Inappropriate RSI overbought/oversold zone setup may impact judgements
3. Strategy is strict, may miss some opportunities  

Solutions:
1. Optimize Bollinger Bands and RSI parameters to find best combination
2. Relax conditions moderately, allow some invalid trades for more chances

### Optimization Directions 
1. Test and optimize RSI and Bollinger parameters for optimum  
2. Add stop loss to control risks
3. Consider adding other indicators like MACD for signal verification  
4. Test optimization results across different products and timeframes

### Summary
The overall strategy is robust, effectively combines RSI and Bollinger Bands for stop loss. Further improvement can be achieved by testing and optimizing parameters. Also need to be aware of potential signal missing risks due to strict rules. In general, this is a reliable quantitative trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2019|Start Year|
|v_input_2|4|Start Month|
|v_input_3|true|Start Day|
|v_input_4|false|Start Hour|
|v_input_5|false|Start Minute|
|v_input_6|9|RSI Period Length|
|v_input_7|30|RSIL|
|v_input_8|69|RSIh|
|v_input_9|60|Bollinger Period Length|
|v_input_10|2|Bb|
|v_input_11|true|Enable Bar Color?|
|v_input_12|true|Enable Background Color?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("BB + RSI 20MIN,", shorttitle="BBRSI 20MIN", overlay=true )
     
     // Strategy Tester Start Time
sYear = input(2019, title = "Start Year")
sMonth = input(04, title = "Start Month", minval = 01, maxval = 12)
sDay = input(01, title = "Start Day", minval = 01, maxval = 31)
sHour = input(00, title = "Start Hour", minval = 00, maxval = 23)
sMinute = input(00, title = "Start Minute", minval = 00, maxval = 59)
startTime = true


///////////// RSI
RSIlength = input(9,title="RSI Period Length") 
RSIoverSold = input(30, minval=1,title="RSIL")
RSIoverBought = input(69, minval=1,title="RSIh")
price = open
vrsi = rsi(price, RSIlength)


///////////// Bollinger Bands
BBlength = input(60, minval=1,title="Bollinger Period Length")
BBmult = input(2.0, minval=0.001, maxval=50,title="Bb")
BBbasis = sma(price, BBlength)
BBdev = BBmult * stdev(price, BBlength)
BBupper = BBbasis + BBdev
BBlower = BBbasis - BBdev
source = close
buyEntry = crossover(source, BBlower)
sellEntry = crossunder(source, BBupper)
plot(BBbasis, color=aqua,title="Bollinger Bands SMA Basis Line")
p1 = plot(BBupper, color=silver,title="Bollinger Bands Upper Line")
p2 = plot(BBlower, color=silver,title="Bollinger Bands Lower Line")
fill(p1, p2)


///////////// Colors
switch1=input(true, title="Enable Bar Color?")
switch2=input(true, title="Enable Background Color?")
TrendColor = RSIoverBought and (price[1] > BBupper and price < BBupper) and BBbasis < BBbasis[1] ? red : RSIoverSold and (price[1] < BBlower and price > BBlower) and BBbasis > BBbasis[1] ? green : na
barcolor(switch1?TrendColor:na)
bgcolor(switch2?TrendColor:na,transp=50)


///////////// RSI + Bollinger Bands Strategy
if (not na(vrsi))

    if (crossover(vrsi, RSIoverSold) and crossover(source, BBlower))
        strategy.entry("RSI_BB_L", strategy.long and startTime, stop=BBlower,  comment="RSI_BB_L")
    else
        strategy.cancel(id="RSI_BB_L")
        
    if (crossunder(vrsi, RSIoverBought) and crossunder(source, BBupper))
        strategy.entry("RSI_BB_S", strategy.short and startTime, stop=BBupper,comment="RSI_BB_S")
    else
        strategy.cancel(id="RSI_BB_S")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/439866

> Last Modified

2024-01-24 14:56:02
