
> Name

Rainbow-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The Rainbow Moving Average trading strategy is designed based on the Rainbow Moving Average indicator. This strategy determines the trend direction by constructing a rainbow moving average system containing 7 moving averages, and cooperates with the RSI indicator to filter out false signals to achieve low-risk transaction entry.
## Strategy Principle
This strategy mainly achieves the generation of trading signals through the following steps:
1. Construct a rainbow moving average system. The system contains 7 moving averages, the first moving average period is 12, and the source data is the average of the closing prices. The periods of the remaining six moving averages decrease by 3 periods in sequence, and the source data is the value of the previous moving average.
2. Determine the trend direction. If the first moving average is at the top of the Rainbow Moving Average, it is defined as an upward trend; if it is at the bottom, it is defined as a downtrend; if it is in the middle, it is defined as consolidation.
3. Generate trading signals. When the trend of the rainbow moving average system changes from up to down, a sell signal is generated; when the trend changes from down to up, a buy signal is generated; when the trend changes from consolidation to up or down, the current position is closed.
4. RSI filter. Only accept trading signals when the RSI indicator shows normal conditions. The first RSI indicator is required to be between the overbought and oversold areas to avoid false breakthroughs; the second RSI indicator is required not to be located in the middle area to ensure sufficient momentum for a breakthrough.
## Strategic Advantages
This strategy has the following advantages:
1. The Rainbow Moving Average system can accurately determine the trend direction. A combination of multiple moving averages can effectively filter market noise and identify trend reversals.
2. The double filtering mechanism of RSI indicator can effectively filter out false breakthrough signals and avoid being trapped. The first RSI ensures that it is in the normal zone, and the second RSI ensures that the breakout is strong enough.
3. Combined with trend and reversal indicators, you can enter the market in time when the trend turns, and you can avoid chasing the rise and killing the fall.
4. Actively closing positions during the consolidation phase can avoid the risk of regions selection consolidating the market.
5. This strategy has a large space for parameter optimization. By adjusting the moving average period, length ratio, RSI parameters, etc., it can be optimized for different varieties and periods to obtain better results.
## Strategy Risk
This strategy mainly involves the following risks:
1. When the trend reversal is not obvious, an illusory reversal signal may be generated, resulting in trading losses. The moving average period can be appropriately adjusted to make the reversal signal more clear.
2. When the underlying market consolidates in a long-term area, positions will be opened and closed frequently, increasing transaction costs and slippage losses. The filtering intensity during the consolidation phase can be increased by optimizing the RSI parameters.
3. When the reversal is slow, there is time and space for losses to expand after the reversal signal is sent. The period difference of the moving average can be increased to make the signal send out more timely.
4. Improper parameter setting may filter out some correct signals or cause signal lag. Parameters need to be adjusted according to the characteristics of different varieties.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimization of moving average parameters. Parameters such as the period length of the moving average, period difference ratio, and moving average method (SMA or EMA) can be optimized to obtain more accurate trend judgments.
2. RSI parameter optimization. You can optimize RSI's cycle length, overbought area, oversold area, neutral area and other parameters to make filtering more accurate and effective.
3. Time cycle optimization. You can test different time periods and choose the one that best suits the strategy to get the best results.
4. Variety optimization. According to the characteristics of different varieties, parameters or rules can be adjusted to make the strategy work best for that variety.
5. Add a stop-loss and stop-profit mechanism. Based on the backtest results, you can set reasonable stop loss and profit levels to control the risk and profit of a single transaction.
## Summarize
The Rainbow Moving Average trading strategy uses a combination of trend judgment and signal filtering to achieve the effect of capturing signals at trend turning points. This strategy has the characteristics of accurate judgment and controllable risk. Through parameter optimization and rule improvement, it can become a very practical quantitative trading strategy. Overall, this strategy deserves further study and application.
||

## Overview

The Rainbow Moving Average trading strategy is designed based on the Rainbow Moving Average indicator. This strategy identifies trend direction through a rainbow moving average system with 7 moving averages, and filters out false signals with the RSI indicator to achieve low-risk entry.

## Strategy Logic

The strategy generates trading signals through the following steps:

1. Build the rainbow moving average system. It contains 7 moving averages. The first moving average has a period of 12 and takes the closing price as source data. The other 6 moving averages have progressively decreasing periods of 3, with previous moving average as source. 

2. Determine trend direction. If the first moving average is on top of the rainbow, define it as uptrend. If it's at the bottom, define it as downtrend. If it's in the middle, define it as consolidation.

3. Generate signals. When the trend changes from uptrend to downtrend, a sell signal is generated. When the trend changes from downtrend to uptrend, a buy signal is generated. When the trend changes from consolidation to uptrend or downtrend, close existing position. 

4. RSI filter. Only accept signals when RSI shows normal status. The first RSI should be between overbought and oversold zone to avoid false breakout. The second RSI should be outside of middle zone to ensure strong momentum.

## Advantages

The advantages of this strategy include:

1. The rainbow moving average system accurately identifies trend direction. Multiple moving averages combine to filter out market noise and spot trend reversal.

2. The dual RSI filter mechanism effectively avoids false breakout signals and being trapped. The first RSI ensures being in normal zone while the second RSI guarantees strong enough momentum.

3. Combining trend and reversal indicators allows timely entry at trend reversal, while avoiding chasing momentum. 

4. Active position closing during consolidation avoids the risk of range-bound markets.

5. The strategy offers large parameter optimization space, which can be tuned for different products and timeframes to achieve better results.

## Risks

The main risks of this strategy:

1. Unclear trend reversal may generate false signals and cause losses. Adjusting moving average periods can make reversal signals clearer.

2. Frequent opening and closing during long consolidation increases costs and slippage. Optimizing RSI parameters can strengthen filtration in consolidation.

3. Delayed reversal enlarges losses after initial signal. Increasing moving average period difference makes signals timelier. 

4. Improper parameter settings may filter out correct signals or cause signal lagging. Parameters need to be adjusted per product character.

## Optimization Directions 

The strategy can be optimized in the following aspects:

1. Moving average parameter optimization, including period length, period ratio, MA type etc, to make trend judgment more accurate.

2. RSI parameter optimization, including period, overbought/oversold levels, neutral zone etc, to make filtration more precise.

3. Timeframe optimization, to find the optimal timeframe.

4. Product optimization, to adjust parameters and rules to best fit different products. 

5. Adding stop loss and take profit to control risk and profit size.

## Conclusion

The Rainbow Moving Average trading strategy combines trend determination and signal filtering to capture reversal signals effectively. With accurate judgment and controllable risks, this strategy can become very practical after parameter tuning and logic refinement. Overall, it is worth in-depth research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hlc3|0|(?=== Rainbow Moving Average ===)Source: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_2|0|Type: SMA|EMA|
|v_input_3|12|Period|
|v_input_4|3|Displacement|
|v_input_5|blue|(?=== Trend Color ===)Up|
|v_input_6|red|Down|
|v_input_7|yellow|No|
|v_input_8|0|(?=== RSI Filter ===)Filter: Enable|Disable|
|v_input_9|12|(?Over Filter)Period|
|v_input_10|65|Overbought|
|v_input_11|35|Oversold|
|v_input_12|9|(?Middle Filter)Period|
|v_input_13|56|Upper|
|v_input_14|44|Lower|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-28 00:00:00
end: 2023-09-27 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//╔════════════════════════════════════════════════════════════════════════════╗
//║Rainbow Backtesting base on "Rainbow Moving Average" Strategy as below:     ║
//║1.Rainbow Moving Average setup                                              ║
//║- Source: source of 1st MA                                                  ║
//║- Type: SMA/EMA                                                             ║
//║- Period: period of 1st MA                                                  ║
//║- Displacement: period of 2nd MA to 7th MA with source is previous MA       ║
//║2.Trend Define                                                              ║
//║- Up Trend: Main MA moving at the top of Rainbow                            ║
//║- Down Trend: Main MA moving at the bottom of Rainbow                       ║
//║- Sideway: Main MA moving between the top and the bottom of Rainbow         ║
//║3.Signal                                                                    ║
//║- Buy Signal: When Rainbow change to Up Trend.                              ║
//║- Sell Signal: When Rainbow change to Down Trend.                           ║
//║- Exit: When Rainbow change to Sideway.                                     ║
//║4.RSI Filter                                                                ║
//║- "Enable": Only signals have 1st RSI moving between Overbought and Oversold║
//║and 2nd RSI moving outside Middle Channel are accepted.                     ║
//║- The filter may help trader avoid bull trap, bear trap and choppy market.  ║
//╚════════════════════════════════════════════════════════════════════════════╝

//@version=4
strategy("Rainbow Strategy Backtesting",overlay=false)
//++++++++++++++++++++++++++++++++++++++++++++++++++
//+++++++++++++ Rainbow Moving Average +++++++++++++
//++++++++++++++++++++++++++++++++++++++++++++++++++
rainbow_tt="=== Rainbow Moving Average ==="
ma1_source=input(hlc3,title="Source",type=input.source, inline="set1", group=rainbow_tt)
rb_type=input("SMA",title="Type",options=["SMA","EMA"], inline="set1", group=rainbow_tt)
ma1_len=input(12,title="Period", inline="set2", group=rainbow_tt)
dis_len=input(3,title="Displacement", inline="set2", group=rainbow_tt,minval=2)
trend_tt="=== Trend Color ==="
up_col=input(color.new(color.blue,0),title="Up",inline="Color",group=trend_tt)
dn_col=input(color.new(color.red,0),title="Down",inline="Color",group=trend_tt)
sw_col=input(color.new(color.yellow,0),title="No",inline="Color",group=trend_tt)
//1st
ma1=rb_type=="SMA"?sma(ma1_source,ma1_len):ema(ma1_source,ma1_len)
//2nd
ma2=rb_type=="SMA"?sma(ma1,dis_len):ema(ma1,dis_len)
//3rd
ma3=rb_type=="SMA"?sma(ma2,dis_len):ema(ma2,dis_len)
//4
ma4=rb_type=="SMA"?sma(ma3,dis_len):ema(ma3,dis_len)
//5
ma5=rb_type=="SMA"?sma(ma4,dis_len):ema(ma4,dis_len)
//6
ma6=rb_type=="SMA"?sma(ma5,dis_len):ema(ma5,dis_len)
//7
ma7=rb_type=="SMA"?sma(ma6,dis_len):ema(ma6,dis_len)
//MinMax
rb_max=max(ma1,ma2,ma3,ma4,ma5,ma6,ma7)
rb_min=min(ma1,ma2,ma3,ma4,ma5,ma6,ma7)
dir_col=
       ma1==rb_max?up_col:
       ma1==rb_min?dn_col:
       sw_col
dir_style=shape.circle
plotshape(dir_col[1]==dir_col?0:na,title="Trend",style=dir_style,color=dir_col,location=location.absolute)
//++++++++++++++++++++++++++++++++++++++
//+++++++++++++ RSI Filter +++++++++++++
//++++++++++++++++++++++++++++++++++++++
rsi_tt="=== RSI Filter ==="
rsi_filter=input("Enable",title="Filter",options=["Enable","Disable"],inline="set",group=rsi_tt)
over_tt="Over Filter"
rsi_len_1=input(12,title="Period",inline="set",group=over_tt)
rsi_ovb=input(65,title="Overbought",inline="set",group=over_tt)
rsi_ovs=input(35,title="Oversold",inline="set",group=over_tt)
rsi_1=rsi(close,rsi_len_1)
mid_tt="Middle Filter"
rsi_len_2=input(9,title="Period",inline="set",group=mid_tt)
rsi_mid_top=input(56,title="Upper",inline="set",group=mid_tt)
rsi_mid_bot=input(44,title="Lower",inline="set",group=mid_tt)
rsi_2=rsi(close,rsi_len_2)
//Status
var rsi_status="None"
if (rsi_1>rsi_ovs and rsi_1<rsi_ovb) and (rsi_2[1]<rsi_mid_bot or rsi_2[1]>rsi_mid_top)
    rsi_status:="Normal"
else
    rsi_status:="None"
//Signal
BuySignal= 
       rsi_filter=="Disable"?
       dir_col[1]!=up_col
       and
       dir_col[0]==up_col
       :
       dir_col[1]!=up_col
       and
       dir_col[0]==up_col
       and
       rsi_status=="Normal"
       
SellSignal= 
       rsi_filter=="Disable"?
       dir_col[1]!=dn_col
       and
       dir_col[0]==dn_col
       :
       dir_col[1]!=dn_col
       and
       dir_col[0]==dn_col
       and
       rsi_status=="Normal"
       
exit=
       (dir_col[1]!=sw_col
       and
       dir_col[0]==sw_col)
buycol =
       BuySignal?
       up_col: na

sellcol =
       SellSignal?
       dn_col: na

exitcol =
       exit?
       sw_col: na

buy_style=shape.arrowup
sell_style=shape.arrowdown
exit_style=shape.square
plotshape(BuySignal?0:na,title="Buy",text="Buy",style=buy_style,color=buycol,location=location.absolute)
plotshape(SellSignal?0:na,title="Sell",text="Sell",style=sell_style,color=sellcol,location=location.absolute)
plotshape(exit?0:na,title="Exit",text="Exit",style=exit_style,color=exitcol,location=location.absolute)

filter=
       rsi_filter=="Enable"?
       dir_col[1]!=dir_col 
       and BuySignal==false 
       and SellSignal==false 
       and exit==false:
       na
filter_style=shape.xcross
filtercol=
       filter?
       dir_col:na
plotshape(filter?0:na,title="Filter",text="Filter",style=filter_style,color=filtercol,location=location.absolute)

//+++++++++++++++++++++++++++++++++++++++++++++++++
//++++++++++++++++++ Backtesting ++++++++++++++++++
//+++++++++++++++++++++++++++++++++++++++++++++++++
strategy.entry("Long", strategy.long, when=BuySignal)
strategy.close("Long", when=exit or filter)
strategy.entry("Short", strategy.short, when=SellSignal)
strategy.close("Short", when=exit or filter)
//EOF
```

> Detail

https://www.fmz.com/strategy/428053

> Last Modified

2023-09-28 11:01:59
