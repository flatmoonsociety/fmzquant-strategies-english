
> Name

Momentum Breakout Bollinger Band Trading Strategy Bollinger-Band-Momentum-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17da033e71d890788b5.png)
[trans]
## Overview
This strategy combines the Bollinger Band indicator and the trading volume indicator to identify opportunities for strong breakthroughs above the Bollinger Band in a high trading volume environment and carry out buying operations. At the same time, combined with the moving average indicator, determine the trend direction and reduce the risk of locked positions.
## Strategy Principle
1. Use the Bollinger Band indicator to determine whether the price breaks through the upper Bollinger Band.
2. Use the trading volume indicator to determine whether the current trading volume is significantly higher than the average trading volume in the past period.
3. When the trading volume is active and the price breaks through the upper Bollinger Band, perform a buying operation.
4. Use the moving average indicator to determine short-term and medium-term trends, and close positions and stop losses in a timely manner when the trend is unfavorable.
This strategy mainly considers three factors: price, momentum and trend. When the price breaks through the upper Bollinger Band and enters the buying zone, a large influx of funds leads to a surge in trading volume, indicating that there is strong market support and momentum. At this time, open a long position. Then combine the moving average to determine the market trend to avoid locking up the position. Obtain the benefits brought by the market through price selection, timely tracking of funds and reduction of short position risks.
## Strategic Advantages
1. The trading signals are accurate and false breakthroughs are avoided. Combined with trading volume indicators, only buy in real strong markets to reduce position risks.
2. Judging the trend direction through the moving average can stop losses in time and reduce short position losses.
3. A quantitative strategy that integrates multiple indicators for decision-making is implemented, and the parameters can be flexibly adjusted to adapt to different varieties and cycles.
4. The code structure is clear, which increases the readability of the strategy. Organize indicator calculations, trading signals, opening and closing logic, etc. into modules to facilitate later maintenance.
## Strategy Risk
1. As an indicator of fluctuation range, Bollinger Bands may be ineffective in extreme market conditions. If there are abnormal fluctuations, buying signals will be missed or false signals will be generated.
2. When the trading volume is insufficient, the strategy cannot make a profit. If the overall trading volume of the market is insufficient, it will be difficult to make a profit even if a buy signal is generated.
3. As a trend judgment indicator, the moving average may also be invalid and cannot completely guarantee stop loss.
4. Improper parameter settings will also affect strategy returns. For example, if the trading time window is set too short, trend reversal will be missed.
## Strategy optimization direction
1. You can consider adding more technical indicators to judge trends and support resistance levels to improve the stop loss effect, such as K-line patterns, channel indicators, key support levels, etc.
2. Increase the possibility of machine learning models to determine real breakthroughs and reduce the false signal rate. For example, deep learning models such as LSTM.
3. Optimize fund management strategies, such as dynamically adjusting positions, tracking stop loss lines, etc. Reduce the impact of a single loss.
4. Test more varieties and time period parameters. Adjust Bollinger Band parameters, trading volume parameters, etc. to optimize strategies that adapt to the market.

## Summarize
This strategy integrates Bollinger Bands indicators and trading volume indicators to identify buying opportunities in strong markets. At the same time, use the moving average indicator to determine the trend and stop losses in time. Compared with a single technical indicator, it has higher accuracy and stop-loss ability. Through the addition of modular design, trend judgment and stop-loss strategies, a breakthrough trading strategy is formed that is easy to optimize and maintain.
||

## Overview

This strategy combines Bollinger Band indicator and volume indicators to identify strong momentum breakout opportunities above Bollinger upper band when trading volume is high, and enters long positions. It also uses moving average indicators to determine trend direction and reduce the risk of holding dead positions.

## Strategy Logic

1. Use Bollinger Band indicator to determine if price breaks out above the upper band. 
2. Use trading volume indicators to determine if current volume is significantly higher than past period average.
3. Enter long position when trading volume is high and price breaks out above Bollinger upper band.  
4. Use moving average indicators to determine short term and medium term trend to cut loss in time.

This strategy mainly considers three factors: price level, momentum and trend. When price breaks out the Bollinger upper band into the buy zone, surge in trading volume indicates strong momentum and capital inflow. This is the right timing to enter long position. Then it uses moving averages to determine market trend to avoid holding dead positions. By combining price action, momentum and risk control, it aims to capture profits from strong trends.  

## Advantages

1. Accurate signals, avoids false breakout. Combining volume filter, it only buys on real strong momentum, reducing risk.

2. Able to cut loss in time via moving average trend determination, reducing holding loss. 

3. Implemented quantitative strategy combining multiple indicators for decision making. Flexible parameters tuning for different products and timeframes.

4. Clear code structures, easy to read and maintain. Modular design of indicators calculation, signal generation and position management.

## Risks

1. Bollinger Bands could fail during extreme price swings, missing signals or generating false signals. 

2. No profits when overall trading volume is low. Buy signals may not be profitable without enough trading volume.

3. Moving averages trend determination could also fail, unable to fully ensure effective stop loss.  

4. Improper parameter tuning also affects strategy profitability. For example, trading time window set too short may miss trend reversal.

## Optimization Directions

1. Add more technical indicators for better trend and support/resistance analysis, improving stop loss, e.g. candlestick patterns, channels, key support levels.

2. Add machine learning models to judge real breakout possibilities, reducing false signals. e.g. LSTM deep learning models.

3. Optimize capital management strategies like dynamic position sizing, trailing stop loss to reduce single trade loss impact.  

4. Test more products and timeframes, adjust parameters like Bollinger Bands, volume window to improve strategy robustness.


## Conclusion

This strategy integrates Bollinger Band and trading volume indicators to identify strong momentum buying opportunities, with moving averages ensuring effective stop loss. Compared to single indicator strategies, it has higher accuracy and risk control capabilities. With modular design, trend filters and stop loss mechanisms, it forms an easy-to-optimize momentum breakout trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|length1|
|v_input_2|3|length3|
|v_input_3|7|length7|
|v_input_4|9|length9|
|v_input_5|14|length14|
|v_input_6|20|length20|
|v_input_7|60|length60|
|v_input_8|120|length120|
|v_input_9|50|Daily MA length|
|v_input_10|10|Weekly MA length|
|v_input_11|20|length|
|v_input_12_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_13|2|StdDev|
|v_input_14|1.5|exp|
|v_input_15|true|exp1|
|v_input_16|2.5|exp2|
|v_input_17|false|Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-05 00:00:00
end: 2024-02-04 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © KAIST291

//@version=4
initial_capital=1000
strategy("prototype", overlay=true)
length1=input(1)
length3=input(3)
length7=input(7)
length9=input(9)
length14=input(14)
length20=input(20)
length60=input(60)
length120=input(120)
ma1= sma(close,length1)
ma3= sma(close,length3)
ma7= sma(close,length7)
ma9= sma(close,length9)
ma14=sma(close,length14)
ma20=sma(close,length20)
ma60=sma(close,length60)
ma120=sma(close,length120)
rsi=rsi(close,14)
// BUYING VOLUME AND SELLING VOLUME //
BV = iff( (high==low), 0, volume*(close-low)/(high-low))
SV = iff( (high==low), 0, volume*(high-close)/(high-low))
vol = iff(volume > 0, volume, 1)
dailyLength = input(title = "Daily MA length", type = input.integer, defval = 50, minval = 1, maxval = 100)
weeklyLength = input(title = "Weekly MA length", type = input.integer, defval = 10, minval = 1, maxval = 100)
//-----------------------------------------------------------
Davgvol = sma(volume, dailyLength)
Wavgvol = sma(volume, weeklyLength)
//-----------------------------------------------------------
length = input(20, minval=1)
src = input(close, title="Source")
mult = input(2.0, minval=0.001, maxval=50, title="StdDev")
mult2= input(1.5, minval=0.001, maxval=50, title="exp")
mult3= input(1.0, minval=0.001, maxval=50, title="exp1")
mult4= input(2.5, minval=0.001, maxval=50, title="exp2")
basis = sma(src, length)
dev = mult * stdev(src, length)
upper = basis + dev
lower = basis - dev
dev2= mult2 * stdev(src, length)
Supper= basis + dev2
Slower= basis - dev2
dev3= mult3 * stdev(src, length)
upper1= basis + dev3
lower1= basis - dev3
dev4= mult4 * stdev(src, length)
upper2=basis + dev4
lower2=basis - dev4
offset = input(0, "Offset", type = input.integer, minval = -500, maxval = 500)
plot(basis, "Basis", color=#FF6D00, offset = offset)
p1 = plot(upper, "Upper", color=#2962FF, offset = offset)
p2 = plot(lower, "Lower", color=#2962FF, offset = offset)
fill(p1, p2, title = "Background", color=color.rgb(33, 150, 243, 95))
//----------------------------------------------------
exit=(close-strategy.position_avg_price / strategy.position_avg_price*100)
bull=( BV>SV and BV>Davgvol)
bull2=(BV>SV and BV>Davgvol)
bux =(close>Supper and close>Slower and volume<Davgvol)
bear=(SV>BV and SV>Davgvol)
con=(BV>Wavgvol and rsi>80)
imInATrade = strategy.position_size != 0
highestPriceAfterEntry = valuewhen(imInATrade, high, 0)
// STRATEGY LONG //
if (bull and close>upper1 and close>Supper and high>upper and rsi<80)
    strategy.entry("Long",strategy.long)

if (strategy.position_avg_price*1.02<close)
    strategy.close("Long")
else if (low<ma9 and strategy.position_avg_price<close)
    strategy.close("Long")
else if (ma20>close and strategy.position_avg_price<close )
    strategy.close("Long")
else if (rsi>80 and strategy.position_avg_price<close)
    strategy.close("Long")
else if (strategy.openprofit < strategy.position_avg_price*0.9-close)
    strategy.close("Long")
else if (high<upper and strategy.position_avg_price<close)
    strategy.close("Long")
//////////////////////////////////////////////////////////////////////////////////

//////////////////////////////////////////////////////////////////////////////////
strategy.entry("Short",strategy.short,when=low<ma20 and low<lower1 and close<Slower and crossunder(ma60,ma120))

if (close<strategy.position_avg_price*0.98)
    strategy.close("Short")

else if (rsi<20)
    strategy.close("Short")


```

> Detail

https://www.fmz.com/strategy/441054

> Last Modified

2024-02-05 10:53:46
