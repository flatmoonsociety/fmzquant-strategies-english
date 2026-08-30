
> Name

Cross-period-Value-Area-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11f7335e1a172edba84.png)
[trans]

### Overview
The core idea of ​​this strategy is to combine the RSI indicators of different periods to determine the current price area, and when it is found that the RSI indicator of a larger period breaks through, take corresponding buying or selling operations in a smaller period. This strategy comprehensively utilizes the advantages of different cycle technical indicators, judges the relative value of the current price through multiple time dimensions, and finds better entry points.
### Strategy Principles
This strategy mainly uses the following steps to determine the price area and find trading opportunities:
1. Calculate the highest point (Swing High) and lowest point (Swing Low) of the RSI indicator in a larger period (such as the daily line)
2. Determine whether the larger period RSI has the highest or lowest point within a given lookback period.
3. If a breakthrough occurs, judge the price trend (long or short) in a smaller period (such as the 5-minute line) and take corresponding buying or selling operations.
For example, when the daily RSI indicator breaks through a new high, we judge that we are currently in a long market, and if the daily RSI breaks through a new low, we judge that we are currently in a short market. In both cases, we take buy and sell operations on the 5-minute line respectively.
### Advantage Analysis
Compared with traditional strategies that only focus on one time period, this strategy has the following advantages:
1. Evaluate relative value at current prices more accurately. Larger cycle indicators such as the daily line can filter short-term market noise and determine large-cycle trends and value areas.
2. Combine different time period indicators to improve the reliability of signals. Relying only on a single periodic indicator is prone to false signals, while multiple periodic indicators sending signals simultaneously are more reliable.
3. Capture short-term opportunities more effectively. Breakthroughs in large cycles such as the daily line point out the big direction for us, and we only need to look for opportunities in short cycles such as 5 minutes to make profits.
4. The retracement is smaller. Combining across time periods helps avoid being trapped. When the big cycle indicators turn around, we will stop the loss and exit in time.
### Risk Analysis
The main risks of this strategy are:
1. Misjudgment of large cycle indicators. When indicators such as daily RSI cannot effectively judge the value area, it will lead to signal errors. This requires optimizing the parameter settings of RSI.
2. The small cycle market does not match the judgment of the large cycle. Sometimes the price trend of a small period will oppose the trend of a large period. At this time, a stop loss needs to be set to control losses.
3. Improper fund management. If risk management is improper and a single loss is too large, it will be difficult to recover. This requires reasonable setting of position management.
### Optimization direction
There is still a lot of room for optimization of this strategy, which can mainly start from the following aspects:
1. Optimization of cycle parameters. More cycle combinations can be tested to find the best parameters.
2. RSI parameter optimization. You can adjust the parameters of RSI to see if the accuracy of judgment can be improved.
3. Add other indicators. You can add more indicators to combine, such as adding moving averages to determine the trend direction.
4. Optimize the stop loss mechanism. The stop loss point can be dynamically adjusted according to the retracement situation.
5. Optimize warehouse management. The specific positions of each transaction can be managed more scientifically and rationally.
### Summarize
This strategy achieves value arbitrage between different time dimensions by evaluating the bullishness of the RSI indicator across cycles. This idea of ​​cross-cycle judgment is worthy of further exploration. We can continue to improve it through parameter optimization, stop loss optimization, combination optimization and other methods to make the strategy more advantageous. In general, this strategy has a unique idea and a lot of room for optimization.
||

### Overview  

The core idea of this strategy is to determine the current price range by combining RSI indicators of different cycles, and to take corresponding buy or sell actions in smaller cycles when there is a breakout in larger cycle RSI. This strategy takes advantage of technical indicators across different periods to judge the relative value of current price from multiple time dimensions and locate better entry points.   

### Strategy Logic  

The main steps for this strategy to determine price range and find trading opportunities are:  

1. Calculate the RSI Swing High and Swing Low based on larger cycle (e.g. daily). 
2. Determine if the larger cycle RSI made a new high or low within the lookback period.  
3. If there is a breakout, judge the price trend (bullish or bearish) in smaller cycle (e.g. 5 min) and take corresponding buy or sell actions.   

For example, when the daily RSI breakout its previous high, we judge that it is currently a bull market. And when the daily RSI break below its previous low, we judge it as a bear market. Under both cases we take long and short actions respectively in the 5 min chart.    

### Advantage Analysis    

Compared with traditional strategies that only focus on one period, this strategy has the following advantages:   

1. More accurate assessment of current relative price value. Larger cycles like daily can filter out short-term market noise and determine overall trend and value area.  

2. Combining indicators across periods improves signal reliability. Relying solely on single period indicator can generate false signals more easily, while concurrent signals from multiple periods is more reliable.   

3. More effectively capitalizing short-term opportunities. Large cycle breakout points out overall direction, while we only need to locate opportunity in small cycles like 5 mins to profit.  

4. Smaller drawdowns. Combining cross periods helps avoid being trapped. We can exit quickly when large cycle indicators start to reverse.  

### Risk Analysis   

The main risks of this strategy lies in:  

1. Wrong judgement in large cycle indicators. Ineffective value area determination in daily RSI etc can lead to faulty signals. Parameter tuning of RSI is needed to improve accuracy.  

2. Divergence between small cycle price move and large cycle determination. Sometimes short-term moves counteract big picture trends. We need to set proper stop loss to control the loss.  

3. Improper risk management. Excessive loss in single trade due to poor position sizing could lead to unrecoverable drawdown. Reasonable sizing rules must be implemented.

### Optimization Directions   

There is still large room to improve this strategy, mainly from the following aspects:   

1. Period parameter tuning. Test more period combinations to find optimal parameters.  

2. RSI parameter tuning. Adjust RSI lookback etc parameters to improve judgement accuracy.
3. Add more indicators. Bring in more indicators like MA to assist judging trend direction.   
4. Improve stop loss mechanism. Dynamically adjust stop loss points based on drawdown conditions.
5. Optimize position sizing rules. Manage specific position sizes for each trade more scientifically.  

### Conclusion  

This strategy realizes cross period arbitrage between different time dimensions by assessing bullish condition in cross period RSIs. Such idea of cross period judgement deserves further exploitation. We can keep improving it via parameter tuning, stop loss optimization, indicator combinations to make it more advantageous. Overall speaking, this strategy has a unique idea and huge potential to be enhanced.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|Look Back Period (2nd Timeframe)|
|v_input_2|180|Second Momentum Timeframe|
|v_input_3|true|Breaks in lines|
|v_input_4|11|Bars back to check for a swing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy("Swing MTF", shorttitle="Swing MTF", overlay=false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, initial_capital = 10000, slippage = 5)
//
otf_period = input(defval=2, title="Look Back Period (2nd Timeframe)")
otf = input(defval="180", title="Second Momentum Timeframe")

// Function to dectect a new bar
is_newbar(res) =>
    t = time(res)
    change(t) != 0 ? true : false

// Check how many bars are in our upper timeframe
since_new_bar = barssince(is_newbar(otf))
otf_total_bars = na
otf_total_bars := since_new_bar == 0 ? since_new_bar[1] : otf_total_bars[1]

//Calculate RSI Values
ctf_rsi = rsi(open, otf_period)

breakline=input(title="Breaks in lines", defval = true, type=bool)

so = request.security(syminfo.tickerid, otf, rsi(open, otf_period))
sc = request.security(syminfo.tickerid, otf, rsi(close, otf_period))


final_otf_so = na
final_otf_so := barstate.isrealtime ? since_new_bar == otf_total_bars ? so : final_otf_so[1] : so

final_otf_sc = na
final_otf_sc := barstate.isrealtime ? since_new_bar == otf_total_bars ? sc : final_otf_sc[1] : sc

barsback = input(11, title='Bars back to check for a swing')
// showsig = input(false, title='Show Signal Markers')
 
swing_detection(index)=>
    swing_high = false
    swing_low = false
    start = (index*2) - 1 // -1 so we have an even number of
    swing_point_high = final_otf_so[index]
    swing_point_low = final_otf_sc[index]
    
    //Swing Highs
    for i = 0 to start
        swing_high := true
        if i < index 
            if final_otf_so[i] > swing_point_high 
                swing_high := false
                break
        // Have to do checks before pivot and after seperately because we can get
        // two highs of the same value in a row. Notice the > and >= difference
        if i > index
            if final_otf_so[i] >= swing_point_high 
                swing_high := false
                break
        
    //Swing lows
    for i = 0 to start
        swing_low := true
        if i < index
            if final_otf_sc[i] < swing_point_low 
                swing_low := false
                break  
        // Have to do checks before pivot and after seperately because we can get
        // two lows of the same value in a row. Notice the > and >= difference
        if i > index
            if final_otf_sc[i] <= swing_point_low 
                swing_low := false
                break 
        
    [swing_high, swing_low]
 
// Check for a swing
[swing_high, swing_low] = swing_detection(barsback)
 

long =  final_otf_so > final_otf_sc
short = final_otf_so < final_otf_sc

if swing_low and long
    strategy.entry("My Long Entry Id", strategy.long)


if swing_high and short
    strategy.entry("My Short Entry Id", strategy.short)
```

> Detail

https://www.fmz.com/strategy/435088

> Last Modified

2023-12-12 10:58:22
