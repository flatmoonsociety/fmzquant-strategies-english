
> Name

Momentum-Dual-Moving-Window-TSI-Indicator Momentum-Dual-Moving-Window-TSI-Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/dda519fa139f2ca310.png)

[trans]

#### 1. Strategy Overview
This strategy is named **Momentum Double Sliding Window TSI Indicator Strategy**. The core idea of ​​this strategy is to use the double EMA sliding window to smooth price changes, and then combine it with the direction change of the trend to construct a momentum indicator that reflects the strength of market buying and selling, namely the TSI indicator, and use it as a trading signal to make buying and selling decisions.
#### 2. Strategy Principle
This strategy uses dual sliding window dual exponential moving averages to calculate price movements. The outer window period is longer, and the inner window period is shorter. Remove some of the randomness from price data through double smoothing.
First calculate the unit change in price:
`pc = change(price)`

The price changes are then double-smoothed using double sliding windows:
`double_smoothed_pc = double_smooth(pc, long, short)`

Then calculate the absolute value of the price change, and also use double sliding windows for double smoothing:
`double_smoothed_abs_pc = double_smooth(abs(pc), long, short)`

Finally, use the smoothed price change divided by the smoothed absolute value of the price change to obtain the TSI indicator that reflects the strength of buying and selling:
`tsi_value = 100 * (double_smoothed_pc / double_smoothed_abs_pc)`

By setting long and short window periods of different lengths, short-term market noise can be filtered out to a certain extent, allowing the TSI indicator to better reflect the buying and selling intensity in mid- to long-term trends. A buy signal is generated when the TSI indicator crosses above its moving average; a sell signal is generated when the TSI indicator crosses below its moving average.
#### 3. Strategic advantages
1. Use double sliding windows to effectively filter out short-term market noise and make indicator responses more accurate.
2. Calculated price changes are also double-smoothed to make the TSI indicator more stable and reliable.
3. Use the ratio of price change to the absolute value of price change to automatically standardize and make it more comparable.
4. Comprehensive consideration of the direction and intensity of price changes as a high-quality indicator for trading decisions
5. Set different parameters to adjust the sensitivity of the indicator as needed.
#### 4. Strategic Risks
1. When the market experiences long-term fluctuations, the TSI indicator may send wrong signals
2. Improper parameter settings will also affect the quality of indicators and signals.
3. Although there are double sliding windows, the indicator is still sensitive to short-term market noise.
4. When the gap between the long and short window periods is too large, indicators and signals may lag behind
It can be optimized by adjusting the window period parameters and appropriately shortening the length of the signal average line; when the market fluctuates, trading can be temporarily stopped to control risks.
#### 5. Optimization direction
1. Test different long and short window period parameter combinations to find the optimal parameters
2. Try other types of moving averages, such as linear weighted moving averages
3. Increase the smoothness of the indicator and construct triple or multiple sliding windows
4. Combine with other auxiliary indicators to optimize the selection of buying and selling points
5. Set a stop-loss strategy and strictly control single losses
#### 6. Summary
This strategy calculates the TSI momentum indicator that reflects the intensity of buying and selling based on double smoothing of price changes. Double sliding windows filter noise, and changes in price changes are also double smoothed, making the indicator more stable and reliable. It uses a standardized ratio and is comparable. The indicator combines the direction and intensity of price changes as a high-quality signal. The sensitivity of the indicator can be freely controlled through parameter adjustment. When parameter optimization and risk control are in place, it is a very practical quantitative trading strategy choice.
||

#### I. Strategy Overview

This strategy is named the **Momentum Dual Moving Window TSI Indicator Strategy**. The core idea of this strategy is to use dual EMA sliding windows to smooth price fluctuations, and then combine the directional changes of the trend to construct a momentum indicator that reflects the buying and selling power in the market, namely the TSI indicator, and use it as a trading signal to make buy and sell decisions.

#### II. Strategy Principle  

This strategy uses dual sliding window double exponential moving averages to calculate price changes. The outer window period is longer and the inner window period is shorter. By double smoothing, part of the randomness in the price data is removed.

First calculate the unit change in price:  

`pc = change(price)`

Then use dual sliding windows to double smooth the price changes:

`double_smoothed_pc = double_smooth(pc, long, short)`

Then calculate the absolute value of the price change, which is also double smoothed using dual sliding windows:  

`double_smoothed_abs_pc = double_smooth(abs(pc), long, short)`

Finally, use the smoothed price change divided by the smoothed absolute price change to get the TSI indicator that reflects the buying and selling power:

`tsi_value = 100 * (double_smoothed_pc / double_smoothed_abs_pc)` 

By setting different lengths of long and short window periods, market noise in the short term can be filtered out to some extent, so that the TSI indicator can better reflect the buying and selling power in medium and long term trends. When the TSI indicator crosses above its moving average, a buy signal is generated; When the TSI indicator falls below its moving average, a sell signal is generated.

#### III. Strategy Advantages  

1. Using dual sliding windows effectively filters out short-term market noise for more accurate indicator reactions  
2. The price change is also double smoothed, making the TSI indicator more stable and reliable  
3. The ratio of price change to absolute price change is used, which is automatically standardized and more comparable  
4. Comprehensively consider the direction and magnitude of price changes as a quality indicator for trading decisions  
5. Setting different parameters allows flexible adjustment of indicator sensitivity

#### IV. Strategy Risks  

1. The TSI indicator may give wrong signals when the market has long-term fluctuations  
2. Improper parameter settings can also affect the quality of indicators and signals  
3. Although there are dual sliding windows, the indicator still has some sensitivity to short-term market noise  
4. When the difference between long and short window periods is too large, indicators and signals may lag  

It can be optimized by adjusting window period parameters and appropriately shortening signal moving average length. When the market fluctuates, trading can be temporarily stopped to control risks.  

#### V. Optimization Directions  

1. Test combinations of different long and short window period parameters to find optimal parameters  
2. Try other types of moving averages, such as Linear Weighted Moving Average  
3. Increase the smoothness of indicators by building triple or multiple sliding windows  
4. Combine other auxiliary indicators to optimize buy/sell point selection  
5. Set stop loss strategies to strictly control single loss  

#### VI. Summary  

This strategy calculates the TSI momentum indicator reflecting buying and selling power based on the double smoothing of price changes. The dual sliding windows filter out noise. The double smoothing of price change variations also makes the indicator more stable and reliable. The standardized ratio makes it comparable. The indicator combines the direction and magnitude of price changes as a high quality signal source. Through parameter adjustment, indicator sensitivity can be freely controlled. With parameter optimization and risk control in place, it is a very practical quantitative trading strategy choice.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|120|Timeframe|
|v_input_2|25|Long Length|
|v_input_3|13|Short Length|
|v_input_4|13|Signal Length|
|v_input_5|300|Период|
|v_input_6|true|From Month|
|v_input_7|true|From Day|
|v_input_8|2017|From Year|
|v_input_9|true|To Month|
|v_input_10|true|To Day|
|v_input_11|9999|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2024-01-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("True Strength Indicator BTCUSD 2H", shorttitle="TSI BTCUSD 2H",initial_capital=1000, commission_value=0.2, commission_type =strategy.commission.percent, default_qty_value=100 , overlay = false, pyramiding=10, default_qty_type=strategy.percent_of_equity)

//BASED ON True Strength Indicator MTF
resCustom = input(title="Timeframe",  defval="120" )
long = input(title="Long Length",  defval=25)
short = input(title="Short Length",  defval=13)
signal = input(title="Signal Length",  defval=13)

length = input(title="Период",  defval=300)

FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
FromYear = input(defval = 2017, title = "From Year", minval = 2017)
ToMonth = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
ToDay = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
ToYear = input(defval = 9999, title = "To Year", minval = 2017)
start = timestamp(FromYear, FromMonth, FromDay, 00, 00) // backtest start window
finish = timestamp(ToYear, ToMonth, ToDay, 23, 59) // backtest finish window
window() => true // create function "within window of time"

price = request.security(syminfo.tickerid,resCustom,close)


double_smooth(src, long, short) =>
    fist_smooth = ema(src, long)
    ema(fist_smooth, short)
pc = change(price)
double_smoothed_pc = double_smooth(pc, long, short)
double_smoothed_abs_pc = double_smooth(abs(pc), long, short)
tsi_value = 100 * (double_smoothed_pc / double_smoothed_abs_pc)
tsi2=ema(tsi_value, signal)
plot(tsi_value, color=lime,linewidth=2)
plot(tsi2, color=red,linewidth=2)

hline(30, title="Zero")
hline(50, title="Zero",linewidth=2)
hline(70, title="Zero")

buy = crossover(tsi_value, tsi2)
sell = crossunder(tsi_value, tsi2)

if(buy)
    strategy.entry("BUY", strategy.long, when = window())
if(sell)
    strategy.entry("SELL", strategy.short, when = window()) 

//greentsi =tsi_value
//redtsi = tsi2

//bgcolor( greentsi>redtsi and rsiserie > 50 ? lime : na, transp=90)
//bgcolor( greentsi<redtsi and rsiserie < 50 ? red : na, transp=90)

//yellow1= redtsi > greentsi and rsiserie > 50 
//yellow2 = redtsi < greentsi and rsiserie < 50 
//bgcolor( yellow1 ? yellow : na, transp=80)
//bgcolor( yellow2  ? yellow : na, transp=50)

//bgcolor( yellow1 and yellow1[1] ? yellow : na, transp=70)
//bgcolor( yellow2  and yellow2[2] ? yellow : na, transp=70)

//bgcolor( rsiserie > 70 ? lime : na, transp=60)
//bgcolor( rsiserie < 30  ? red : na, transp=60)
```

> Detail

https://www.fmz.com/strategy/438019

> Last Modified

2024-01-08 11:20:35
