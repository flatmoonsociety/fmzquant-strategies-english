
> Name

Price-Channel-Robot-White-Box-Strategy Price-Channel-Robot-White-Box-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/97976d763a8e1779e57301e7717b867659c3e0fc62b62c7bf67c6e728614dd52.png)
[trans]
### Overview
The Price Channel Robot white box strategy is a simple mechanized trading strategy based on the Price Channel indicator. It uses the upper and lower limits of the price channel to determine entry and exit timing. This strategy is long-term for long-term and short-term for short-term.
### Strategy Principles
The core logic of the price channel robot white box strategy is:
1. Use the highest and lowest functions to calculate the highest and lowest prices of the recent len K-lines, which are defined as the upper and lower limits of the price channel.
2. Calculate the middle price of the price channel: (highest price + lowest price)/2
3. When the price crosses the upper limit of the price channel, open a long position
4. When the price falls below the lower limit of the price channel, open a short position
5. When the price falls back to the middle price of the price channel, close the position
The strategy also has some configurable parameters:
- Price channel length len: default 50 K lines
- Opening type: long and short positions can be configured separately
- Open position amount: Default is 100% of account equity
- Stop loss: You can choose whether to use the middle price of the price channel as stop loss
- Trading time: Configurable to only trade within a specified date range
By adjusting these parameters, the strategy can be better adapted to different varieties and market environments.
### Advantage Analysis
The price channel robot white box strategy has the following advantages:
1. The strategy logic is simple, easy to understand and implement
2. Make full use of price channel indicators to determine trends and reversals
3. There are many configurable parameters and strong adaptability.
4. Built-in stop-loss mechanism to limit losses
5. Support time filtering to avoid the impact of major events
Overall, this strategy is a simple and practical trend tracking strategy that can achieve good results after parameter tuning.
### Risk Analysis
There are also some risks with the Price Channel Robot white box strategy:
1. The price channel indicator is sensitive to the parameter len, and different time periods and varieties need to be independently tested and optimized.
2. Trailing stop loss carries the risk of arbitrage, and the stop loss distance needs to be adjusted according to market volatility.
3. Under sideways and volatile market conditions, more unnecessary transactions will occur, increasing transaction costs and slippage losses.
In order to reduce these risks, the following aspects need to be optimized:
1. Use the Walk Forward Analysis method to automatically optimize parameters
2. Add a buffer zone to the stop loss price to avoid the possibility of arbitrage
3. Add trend judgment indicators to avoid sideways and volatile market transactions.
### Optimization direction
There is room for further optimization of the price channel robot white box strategy:
1. Increase the judgment of the general cycle trend and avoid counter-trend transactions
2. Set parameters based on price differences between different varieties and take advantage of arbitrage opportunities
3. Add a random buffer to the stop loss price to reduce the probability of arbitrage
4. Dynamically adjust the price channel parameter len according to market volatility
5. Use deep learning methods to train agent optimization strategies for specific varieties
Through these optimization methods, it is expected to further improve the stability and profitability of the strategy.
### Summarize
The Price Channel Robot White Box Strategy is a simple yet practical strategy for following trends. It uses the price channel indicator to determine trend direction and reversal points and make trading decisions based on this. This strategy is easy to understand and implement, and can obtain good returns after parameter tuning. At the same time, there are certain risks, and parameters and stop losses need to be optimized to reduce risks. Overall, this strategy has broad application prospects and optimization potential, and is worthy of exploration and practice.
||

### Overview

The Price Channel Robot White Box Strategy is a simple mechanical trading strategy based on the price channel indicator. It uses the upper and lower limits of the price channel to determine entry and exit points. The strategy goes long on uptrend and goes short on downtrend.  

### Strategy Logic

The core logic of the Price Channel Robot White Box Strategy is:  

1. Use highest and lowest functions to calculate the highest high and lowest low of recent len bars, defined as upper and lower limits of the price channel
2. Calculate middle price of price channel: (highest high + lowest low) / 2
3. Go long when price breaks above the upper limit of price channel  
4. Go short when price breaks below the lower limit of price channel
5. Close position when price pulls back to the middle price of price channel

The strategy also has some configurable parameters:  

- Price channel length len: default 50 bars
- Trade direction: long, short can be configured separately  
- Trade size: default 100% of account equity
- Stop loss: option to use middle price as stop loss
- Trading hours: only trade within configured date range  

By adjusting these parameters, the strategy can be better adapted to different products and market environments.   

### Advantage Analysis

The Price Channel Robot White Box Strategy has the following advantages:  

1. Simple logic, easy to understand and implement
2. Make full use of price channel indicator to determine trend and reversal  
3. Highly configurable parameters for better adaptability 
4. Built-in stop loss mechanism to limit losses
5. Support time filter to avoid impacts of major events  

In summary, it is a simple yet practical trend following strategy, which can achieve decent results after parameter tuning.

### Risk Analysis  

The Price Channel Robot White Box Strategy also has some risks:   

1. Price channel indicator is sensitive to parameter len, independent testing and optimization needed for different timeframes and products  
2. Tracking stop loss has risk of being stopped out prematurely, stop loss distance needs adjustment based on market volatility
3. Excessive meaningless trades during range-bound and sideways markets, increasing transaction costs and slippage  

To reduce these risks, optimization needs to be done in the following aspects:  

1. Use Walk Forward Analysis to auto optimize parameters  
2. Add buffer zone to stop loss price to avoid being stopped out
3. Add trend filter to avoid trading in sideways market  

### Optimization Directions

There is room for further optimization of the Price Channel Robot White Box Strategy:  

1. Add judgement of higher timeframe trend to avoid counter trend trading  
2. Use price spread between correlated products to set parameters and utilize arbitrage opportunities
3. Add random buffer to stop loss price to reduce chance of stopped out
4. Dynamically adjust price channel parameter len based on market volatility  
5. Train agent with deep learning methods to optimize strategy for specific products   

These optimization techniques could help further improve the stability and profitability of the strategy.  

### Summary  

The Price Channel Robot White Box Strategy is a simple yet practical trend following strategy. It identifies trend direction and reversal points using the price channel indicator to make trading decisions. The strategy is easy to understand and implement, and can achieve decent returns after parameter tuning. There are also certain risks that need to be mitigated through optimizing parameters and stop loss. Overall, the strategy has broad application prospects and optimization potential, worth exploring and practicing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|true|Stop-loss|
|v_input_4|100|Lot, %|
|v_input_5|50|Price Channel Length|
|v_input_6|true|Show lines|
|v_input_7|false|Show Background|
|v_input_8|1900|From Year|
|v_input_9|2100|To Year|
|v_input_10|true|From Month|
|v_input_11|12|To Month|
|v_input_12|true|From day|
|v_input_13|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-21 00:00:00
end: 2024-02-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro

//@version=4
strategy(title = "Robot WhiteBox Channel", shorttitle = "Robot WhiteBox Channel", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0, commission_value = 0.1)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
needstop = input(true, defval = true, title = "Stop-loss")
lotsize = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot, %")
len = input(50, minval = 1, title = "Price Channel Length")
showll = input(true, defval = true, title = "Show lines")
showbg = input(false, defval = false, title = "Show Background")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Price Channel
h = highest(high, len)
l = lowest(low, len)
center = (h + l) / 2

//Lines
pccol = showll ? color.black : na
slcol = showll ? color.red : na
plot(h, offset = 1, color = pccol)
plot(center, offset = 1, color = slcol)
plot(l, offset = 1, color = pccol)

//Background
size = strategy.position_size
bgcol = showbg == false ? na : size > 0 ? color.lime : size < 0 ? color.red : na
bgcolor(bgcol, transp = 70)

//Trading
truetime = time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)
lot = 0.0
lot := size != size[1] ? strategy.equity / close * lotsize / 100 : lot[1]
if h > 0
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, stop = h, when = strategy.position_size <= 0 and truetime)
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, stop = l, when = strategy.position_size >= 0 and truetime)
    strategy.entry("S Stop", strategy.long, 0, stop = center, when = strategy.position_size[1] <= 0 and needstop)
    strategy.entry("L Stop", strategy.short, 0, stop = center, when = strategy.position_size[1] >= 0 and needstop)
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
    strategy.cancel("Long")
    strategy.cancel("Short")
```

> Detail

https://www.fmz.com/strategy/443040

> Last Modified

2024-02-28 17:51:14
