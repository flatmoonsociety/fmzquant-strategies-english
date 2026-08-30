
> Name

Trend-Surfing-Hedging-Strategy-Based-on-TSI-and-HMACCI-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/120bfc6da0109ab1c39.png)
[trans]
## Overview
This strategy integrates the bilateral trading signals of TSI and improved CCI indicators, and uses arbitrage to frequently open and close positions, with the purpose of pursuing more stable and sustained profits. The key logic is the fast and slow moving average golden cross and dead cross of the TSI indicator, combined with the long and short signal lines of the HMACCI indicator to determine the market buying and selling direction. Control risks by limiting opening conditions and setting stop loss and take profit logic.
## Strategy Principle
This strategy is mainly based on the combination of TSI and HMACCI indicators.
The TSI indicator consists of a fast moving average and a slow moving average, which are used to determine buy and sell signals. When the fast line breaks through the slow line from bottom to top, it is a buy signal, and vice versa is a sell signal. This can more sensitively capture market changing trends.
The HMACCI indicator uses the Hull moving average instead of the price itself based on the traditional CCI indicator, which can filter out some noise and determine the overbought and oversold ranges. The overbought and oversold range can reconfirm the signal direction of the TSI indicator.
The key logic of the strategy is to combine the judgment results of these two indicators and set certain additional conditions to filter out false signals, such as examining the closing price of the previous K line and the highest and lowest prices multiple periods ago to control the quality of reversal signals.
In terms of opening a position, if the conditions are met, a position will be opened at the market price every time the K-line closes, and both long and short positions will be entered. This can lead to more stable returns, but requires bearing the risk of arbitrage.
In terms of stop-profit and stop-loss, floating stop-loss and profit-taking are set to close all positions. This can well control the risk of unilateral trading.
## Strategic Advantages
This is a relatively stable and reliable high-frequency arbitrage strategy. The main advantages are:
1. Double indicator combination can effectively avoid false signals
2. Open positions on every K line, perform frequent arbitrage operations, and make profit and loss fluctuations more stable.
3. Strict position opening logic and stop loss conditions can control risks
4. Combined with trend and reversal judgment, the error tolerance rate is high
5. No direction preference, suitable for all kinds of market conditions
6. The parameters can be adjusted in a large space and can be optimized for different varieties.
## Risk Analysis
The main risks to be aware of are:
1. More fee losses caused by high-frequency trading
2. It is impossible to perfectly avoid the possibility of being trapped in arbitrage
3. Improper parameter settings may lead to overly aggressive entry
4. The possibility of huge unilateral losses is unbearable in the short term
Risks can be reduced by:
1. Appropriately adjust the frequency of opening positions to reduce the impact of handling fees
2. Optimize indicator parameters to ensure signal quality
3. Increase the stop loss, but you will suffer more arbitrage losses
4. Test parameter settings for different varieties
## Optimization direction
This strategy still has a lot of room for optimization, and the main directions are:
1. Optimize and test parameters such as cycle, length, etc.
2. Try different indicator combinations, such as MACD, BOLL, etc.
3. Modify the position opening logic and set more stringent filtering conditions
4. Optimize the stop-profit and stop-loss strategy to achieve dynamic and breakthrough stop-loss
5. Try machine learning methods to find more stable parameter ranges
6. Test trading types and time periods
7. Combine trend judgment indicators to avoid too aggressive entry and exit in volatile market conditions
## Summarize
Generally speaking, this strategy is a stable, reliable and high fault-tolerant bilateral arbitrage strategy. It combines trend judgment and reversal indicators to obtain stable returns through frequent bilateral openings. At the same time, the strategy itself has strong room for optimization and potential, and is a high-frequency trading idea worthy of in-depth study.
||

## Overview  

This strategy combines the bilateral trading signals of the TSI and improved CCI indicators, and adopts a hedging approach to frequently open and close positions, aiming to pursue more stable continuous profits. The key logic is the golden cross and dead cross of the fast and slow moving averages of the TSI indicator, combined with the buy and sell signals of the HMACCI indicator to determine market direction. Risks are controlled by limiting opening conditions, while stop loss and take profit logics are set.

## Strategy Principle   

The strategy is mainly based on the combination of the TSI and HMACCI indicators.   

The TSI indicator contains a fast moving average and a slow one to determine trading signals. When the fast line breaks through the slow line upwards, it is a buy signal, and vice versa for sell signals. This can capture changes in market trends more sensitively.   

The HMACCI indicator is based on the traditional CCI indicator using Hull Moving Average instead of price itself, which can filter out some noise and judge overbought and oversold zones. The overbought and oversold zones can further confirm the signal direction of the TSI indicator.   

The key logic of the strategy is to combine the judgments of these two indicators and set certain additional conditions to filter out false signals, such as examining the previous bar's closing price and maximum and minimum prices over multiple periods to control the quality of reversal signals.  

For opening positions, if conditions are met, market orders are placed each time the bar closes, going both long and short. This can obtain more stable returns, but undertakes the risks of a hedging strategy.  

For take profit and stop loss, floating stop loss and close all orders when reaching target profit are set. This can effectively control the risks of one-way trades.  

## Advantages of the Strategy  

This is a relatively stable and reliable high frequency hedging strategy. The main advantages are:  

1. Combination of dual indicators can effectively avoid false signals  
2. Frequent hedging operations every bar leads to more stable fluctuations in profit and loss
3. Strict opening logic and stop loss conditions can control risks  
4. Combining trend and reversal judgments leads to higher fault tolerance   
5. No directional bias, suitable for various market conditions  
6. Large adjustable parameter space, can be optimized for different products  

## Risk Analysis   

The main risks to note are:    

1. More fee loss caused by high frequency trading 
2. Impossibility to perfectly avoid being locked in a hedge
3. Overly aggressive entry if parameters not set properly  
4. Difficulty to withstand one-way huge losses in short term  

Risks can be reduced through:  

1. Adjust opening frequency appropriately to lower fee impact  
2. Optimize indicator parameters to ensure signal quality  
3. Increase stop loss amplitude but suffer more hedging losses
4. Test parameters on different products
   
## Optimization Directions  

There is still large room for optimizing this strategy, mainly:
  
1. Optimizing parameters like period, length etc. through testing  
2. Trying different indicator combinations e.g. MACD, BOLL etc. 
3. Modifying opening logic, setting stricter filters   
4. Optimizing take profit and stop loss strategies e.g. dynamic, breakout stops 
5. Using machine learning methods to find more stable parameter ranges
6. Testing on different trading products and timeframes  
7. Combining trend detection to avoid overly aggressive trades in range-bound markets  

## Conclusion   

Overall this strategy is a stable, reliable hedging strategy with high fault tolerance. It combines trend and reversal indicators, obtaining steady returns through frequent dual-directional trading. Also, the strategy itself has strong potential for optimization, and represents a worthwhile high frequency trading idea to research further.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|TSI Long Length|
|v_input_2|25|TSI Short Length|
|v_input_3|13|TSI Signal Length|
|v_input_4|33|HMACCI Length|
|v_input_5_open|0|Price Source: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_6|50|Line Distance|
|v_input_7|8|Candles Look Back|
|v_input_8|3000|Stop Loss|
|v_input_9|3000|Target Profit Close All|
|v_input_10|true|FromMonth|
|v_input_11|true|FromDay|
|v_input_12|2020|FromYear|
|v_input_13|true|ToMonth|
|v_input_14|true|ToDay|
|v_input_15|9999|ToYear|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the suns bipolarity
//©SeaSide420
//@version=4
strategy(title="TSI HMA CCI", default_qty_type=strategy.cash,default_qty_value=1000,commission_type=strategy.commission.percent,commission_value=0.001)
long = input(title="TSI Long Length", type=input.integer, defval=25)
short = input(title="TSI Short Length", type=input.integer, defval=25)
signal = input(title="TSI Signal Length", type=input.integer, defval=13)
length = input(33, minval=1, title="HMACCI Length")
src = input(open, title="Price Source")
ld = input(50, minval=1, title="Line Distance")
CandlesBack = input(8,minval=1,title="Candles Look Back")
StopLoss= input(3000,minval=1, title="Stop Loss")
TargetProfitAll= input(3000,minval=1, title="Target Profit Close All")
FromMonth=input(defval=1,title="FromMonth",minval=1,maxval=12)
FromDay=input(defval=1,title="FromDay",minval=1,maxval=31)
FromYear=input(defval=2020,title="FromYear",minval=2020)
ToMonth=input(defval=1,title="ToMonth",minval=1,maxval=12)
ToDay=input(defval=1,title="ToDay",minval=1,maxval=31)
ToYear=input(defval=9999,title="ToYear",minval=2017)
start=timestamp(FromYear,FromMonth,FromDay,00,00)
finish=timestamp(ToYear,ToMonth,ToDay,23,59)
window()=>true
ul = (ld)
ll = (ld-ld*2)
ma = hma(src, length)
cci = (src - ma) / (0.015 * dev(src, length))
price = close
double_smooth(src, long, short) =>
	fist_smooth = ema(src, long)
	ema(fist_smooth, short)
pc = change(price)
double_smoothed_pc = double_smooth(pc, long, short)
double_smoothed_abs_pc = double_smooth(abs(pc), long, short)
tsi_value = 100 * (double_smoothed_pc / double_smoothed_abs_pc)*10
tsi_value2=ema(tsi_value/10, signal)*10
cc = color.white
ct = color.new(color.gray, 90)
if cci<ll or cci[1]<ll
    cc:=color.red
if cci>ul or cci[1]>ul
    cc:=color.green
if cci<ul and cci>ll
    cc:=color.new(color.yellow, 90)
ccc = color.white
if cci>ul
    ccc:=color.green
if cci<cci[1] and cci<ul and cci>ll
    ccc:=color.red
if cci<ll
    ccc:=color.red
if cci>cci[1] and cci>ll and cci<ul
    ccc:=color.green
tsiplot= plot(tsi_value, color=color.lime)
tsiplot2=plot(tsi_value2, color=color.red)    
colorchange2 =tsi_value>tsi_value2?color.lime:color.orange
fill(tsiplot, tsiplot2, color=colorchange2, title="TSIBackground", transp=50)
band1 = hline(ul, "Upper Band 1", color=ct, linestyle=hline.style_dashed)
band0 = hline(ll, "Lower Band 1", color=ct, linestyle=hline.style_dashed)
fill(band1, band0, color=cc, title="MidBandBackground", transp=0)
band2 = hline(ul, "Upper Band 2", color=ct, linestyle=hline.style_dashed)
band3 = hline(ll, "Lower Band 2", color=ct, linestyle=hline.style_dashed)
cciplot2 = plot(cci, "CCIvHMA 2", color=color.black, transp=0, linewidth=5)
cciplot = plot(cci, "CCIvHMA", color=ccc, transp=0, linewidth=3)
hline(0, title="Zero")
hline(420, title="420")
hline(-420, title="-420")
fill(cciplot, cciplot2, color=ccc, title="CCIBackground", transp=0)
LongCondition=cci>cci[1] and cci>ll and src>src[CandlesBack] and tsi_value>tsi_value2
ShortCondition=cci<cci[1] and cci<ul and src<src[CandlesBack] and tsi_value<tsi_value2
plotshape(LongCondition, title="BUY", style=shape.circle, location=location.top, color=color.green)
plotshape(ShortCondition, title="SELL", style=shape.circle, location=location.top, color=color.red)
if  strategy.openprofit>TargetProfitAll
    strategy.close_all(when=window(),comment="close all profit target")
if LongCondition and strategy.openprofit>-1
    strategy.order("BUY", strategy.long,when=window())
if ShortCondition and strategy.openprofit>-1
    strategy.order("SELL", strategy.short,when=window())
strategy.exit("SL exit a sell", "SELL", loss = StopLoss,when=window())     
strategy.exit("SL exit a buy", "BUY", loss = StopLoss,when=window()) 
```

> Detail

https://www.fmz.com/strategy/439709

> Last Modified

2024-01-23 11:26:14
