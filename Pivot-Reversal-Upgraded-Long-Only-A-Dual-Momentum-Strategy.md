
> Name

Pivot-Reversal-Upgraded-Long-Only-A-Dual-Momentum-Strategy Based on Pivot Points and Least Squares Moving Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/0ec911eb5ebc35c0c53319dacf11f758caf55090ec69394e233d38df52d51842.png)
[trans]

### Overview
This is a long-only quantitative trading strategy that combines the advantages of the pivot point reversal strategy and the least squares moving average strategy. This strategy follows the main trend into the market in a bull market, and determines the reversal signal to go long after observing the formation of the upper rail of the pivot point; at the same time, it requires the closing price to be higher than the least squares moving average before opening a long position, making the strategy more stable.
### Strategy Principles
This strategy combines the pivot point reversal strategy and the least squares moving average strategy. The pivot point reversal strategy calculates the highest and lowest prices of a certain trading day in the past to obtain the upper and lower rails. When the price breaks through the upper track, it is judged as a reversal signal. The least squares moving average is a trend judgment indicator that can better approximate the price. This strategy will go long if the closing price is higher than the minimum diradial line when the upper rail of the pivot point is formed.
Specifically, this strategy first calculates the highest price of the past 3 K lines and the lowest price of the past 16 K lines to obtain the upper and lower rails of the pivot point. When the upper rail is formed, open a long position; when the next lower rail is formed, close the position. At the same time, it requires the closing price to be higher than the 20-day least squares moving average to open a position.
### Strategic Advantages
1. Combine the advantages of the two strategies to make trading decisions more stable and reliable
2. The pivot point strategy can determine reversal points, and the least squares moving average filters out false breakthroughs, reducing trading risks.
3. Only doing long positions is in line with most people’s psychological expectations.
4. The strategy is simple and clear, easy to understand and optimize
5. Moderate transaction frequency, suitable for medium and long-term operations
### Risk Analysis
1. Failure to seize the opportunity of rapid market declines
2. There is a certain delay and some rising opportunities may be missed.
3. Large losses will occur when the bull-bear transition occurs.
Solution:
1. Appropriately shorten the calculation cycle and reduce delays
2. Adjust moving average parameters to optimize participation
3. Add stop loss strategy to reduce single loss
### Optimization direction
1. Add a variety of trend indicator combinations to improve judgment accuracy
2. Add machine learning model prediction results to guide decision-making
3. Combine with volatility indicators to control position size
4. Optimize parameters and improve strategy winning rate
5. Test longer time period data to verify stability
### Summarize
This strategy integrates the advantages of the pivot point reversal strategy and the least squares moving average strategy, and controls risks while judging trend reversal. It is a robust strategy. It has a simple structure, is easy to understand and test, and is very suitable for quantitative trading beginners to learn and practice. However, this strategy is only long-term and cannot profit from falling prices. This is its main limitation. By introducing more indicators and machine learning and other methods for optimization, the stability and tracking capabilities of the strategy can be further enhanced, resulting in better performance.
||

### Overview  

This is a long-only quantitative trading strategy that combines the advantages of the pivot point reversal and least square moving average strategies. It follows the major trend during a bull market and determines reversal signals after observing the pivot point upper rail to go long. At the same time, it requires the closing price to be above the Least Squares Moving Average before opening long positions to make the strategy more stable.

### Strategy Logic  

The strategy integrates pivot point reversal and least square moving average strategies. The pivot point reversal strategy calculates the highest and lowest prices over a certain number of trading days to obtain the upper and lower rails. When prices break through the upper rail, it is judged as a reversal signal. The Least Squares Moving Average is a trend-judging indicator that can better approximate prices. This strategy goes long when the pivot point upper rail is formed and the closing price is higher than the least square line.  

Specifically, the strategy first calculates the highest price of the last 3 bars and the lowest price of the last 16 bars to obtain the upper and lower pivot point rails. It goes long when the upper rail is formed. When the next lower rail is formed, it closes positions. At the same time, it requires the closing price to be higher than the 20-day Least Squares Moving Average before opening long positions.

### Advantages  

1. Combines the strengths of two strategies for more stable and reliable trading decisions  

2. Pivot point strategy judges reversal points, while LSMA filters false breakouts, reducing trading risks   

3. Only goes long, in line with most people's psychological expectations  
   
4. Simple and clear strategy logic, easy to understand and optimize
   
5. Moderate trading frequency, suitable for medium-to-long-term operations

### Risk Analysis 

1. Unable to capture opportunities in rapid decline  

2. Certain lag exists, may miss some upward opportunities  

3. Larger losses when the market trend reverses  

Solutions:  

1. Appropriately shorten the calculation cycle to reduce lag  

2. Adjust MA parameters to optimize participation  

3. Add stop loss to reduce single loss

### Optimization Directions  

1. Add multiple trend indicators to improve accuracy  

2. Incorporate machine learning prediction to guide decisions
  
3. Combine volatility indicators to control position sizing   

4. Optimize parameters to improve win rate  

5. Test longer time frame data to verify stability  

### Summary  

This strategy integrates the strengths of pivot point reversal and LSMA strategies to control risks while judging trend reversals. With simple structure for easy understanding and testing, it is perfect for beginner quants to learn and practice. But its long side only approach prevents profiting from market declines, a major limitation. Further improvements in stability and tracking ability could be achieved by introducing more indicators and machine learning optimization for better performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Day|
|v_input_2|true|From Month|
|v_input_3|2010|From Year|
|v_input_4|31|To Day|
|v_input_5|12|To Month|
|v_input_6|2031|To Year|
|v_input_7|20|Length MA|
|v_input_8_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_9|3|leftBars|
|v_input_10|16|rightBars|
|v_input_11|true|multiplier|
|v_input_12|100|risk|
|v_input_13|true|leverage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-18 00:00:00
end: 2023-12-24 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//@author exlux99

strategy(title = "Pivot Reversal Upgraded long only", overlay = true,  pyramiding=1,initial_capital = 100, default_qty_type= strategy.percent_of_equity, default_qty_value = 100, calc_on_order_fills=false, slippage=0,commission_type=strategy.commission.percent,commission_value=0.1)
/////////////
//time

fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2010, title = "From Year", minval = 1970)
 //monday and session 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2031, title = "To Year", minval = 1970)

startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true
//

length = input(title="Length MA", type=input.integer, defval=20)
offset = 0//input(title="Offset", type=input.integer, defval=0)
src = input(close, title="Source")
lsma = linreg(src, length, offset)

//LSMA
leftBars = input(3)
rightBars = input(16)
swh = pivothigh(leftBars, rightBars)
swl = pivotlow(leftBars, rightBars)
swh_cond = not na(swh)
hprice = 0.0
hprice := swh_cond ? swh : hprice[1]
le = false
le := swh_cond and time_cond? true : (le[1] and high > hprice ? false : le[1])
//leverage
multiplier=input(1.0, step=0.5)
g(v, p) => round(v * (pow(10, p))) / pow(10, p)
risk     = input(100)
leverage = input(1.0, step = 0.5)
c = g((strategy.equity * leverage / open) * (risk / 100), 4)

//entry
strategy.entry("long", strategy.long,c, when=le and close > lsma, comment="long", stop=(hprice + syminfo.mintick) * multiplier)

    
swl_cond = not na(swl)
lprice = 0.0
lprice := swl_cond ? swl : lprice[1]
se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])
strategy.close("long", when=se)



```

> Detail

https://www.fmz.com/strategy/436545

> Last Modified

2023-12-25 17:47:11
