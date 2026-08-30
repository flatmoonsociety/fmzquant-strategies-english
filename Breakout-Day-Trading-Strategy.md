
> Name

Breakout-Day-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is a simple intraday trading strategy based on moving averages, suitable for the GBPUSD 1-hour time period chart. It only enters when the London market opens and exits when the London market closes, making it ideal for trend breakout trading during the London session.
### Strategy Principles
This strategy uses two moving averages, a very fast one and a very slow one. The specific logic is as follows:
1. Only break into the market when London opens (8 o'clock). The judgment method is that if the closing price or the highest price breaks through the fast moving average, you can go long, and if the closing price or the lowest price breaks through the fast moving average, you can go short.
2. At the same time, the closing price of the previous K line is required to be higher than the slow moving average to go long, and lower than the slow moving average to go short, so as to filter out non-trend situations.
3. The stop loss is set to a minimum value, only 50-100 points.
4. Do not set a take profit and leave the market unconditionally when London closes (15 o'clock).
### Advantage Analysis
This is a very simple breakout strategy, but it has the following advantages due to its reasonable use of the trend characteristics of the London session:
1. Only enter the market when the trend is clear to avoid the risk of market shock.
2. Only conduct breakout trading during the London session, taking full advantage of the high volatility of this period.
3. Use a small stop loss to withstand a certain degree of rebound.
4. Leave the venue unconditionally to avoid the risk of staying overnight.
### Risk Analysis
There are also some risks with this strategy:
1. When there is no clear trend during the London session, there may be no trading for a long time.
2. The risk of being stopped due to a small stop loss. After the breakthrough, there may be a certain degree of rebound, resulting in a stop loss.
3. The risk of premature departure brought by the fixed departure time. During strong trends, it may be necessary to extend the holding period.
The countermeasures are to appropriately relax the entry rules, use trailing stop loss to lock in profits, and appropriately adjust the exit time according to market conditions.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Add other indicator filters, such as RSI, Bollinger Bands, etc., to further avoid market shocks.
2. Optimize the moving average combination and test the moving average effects of different parameters.
3. Test different stop loss point sizes to find the best stop loss range.
4. Adjust the exit time in real time according to the specific market conditions, rather than leaving the market at the closing moment.
5. Test the effect on other currency pairs and other time periods.
6. Add risk control modules, such as fund management, transaction size calculation, etc.
### Summarize
This strategy is overall a very simple and practical London session breakout strategy. The advantage is that the rules are simple and clear, and some trading risks can be avoided by rationally using period characteristics. At the same time, there is also some room for optimization. If optimization and testing continue, the stability and profitability of the strategy can be further improved. Overall, this strategy provides a reference framework and model for efficiently utilizing London session breakout trading ideas.
||


## Overview

This is a simple day trading strategy based on moving averages, suitable for GBPUSD 1-hour timeframe. It only enters at the London open and exits at the London close, making it ideal for trend breakout trading during the London session.  

## Strategy Logic

The strategy uses two moving averages, one very fast and one very slow. The logic is as follows:

1. Only enter at the London open (8 AM) when price breaks the fast MA. Go long if close or high breaks above fast MA, go short if close or low breaks below fast MA.

2. Require previous bar's close to be above slow MA for long, below slow MA for short, to filter out non-trending moves. 

3. Use a very small stop loss of 50-100 points.

4. No take profit, exits unconditionally at the London close (15:00).

## Advantage Analysis 

This is a very simple breakout strategy, but by properly utilizing the London session trend characteristics, it has the following advantages:

1. Only enters in clear trends, avoiding choppy market risks. 

2. Trades breakouts only during London high volatility period.

3. Small stop loss can withstand some retracement. 

4. Unconditional exit avoids overnight risks.

## Risk Analysis

The strategy also has some risks:

1. May stay flat for long periods when London has no clear trend.

2. Stop loss risks of being stopped out on retracements.

3. Early exit risks when strong trends require extended holding periods.

Mitigations include widening entry rules, using trailing stops to lock in profits, and dynamically adjusting exit time based on market conditions.

## Optimization Directions

The strategy can be improved in several areas:

1. Add other filters like RSI, Bollinger Bands to further avoid choppy markets.

2. Optimize moving average combinations by testing different parameters. 

3. Test different stop loss sizes to find optimal range.

4. Dynamically adjust exit time based on price action rather than fixed time.

5. Test other currency pairs and timeframes. 

6. Add risk management like position sizing based on account size.

## Summary

Overall this is a very simple and practical London session breakout strategy. It benefits from avoiding certain trading risks by properly utilizing session characteristics. There are also areas for further optimizations to improve robustness and profitability. The strategy provides a useful framework and template for effectively trading London session breakouts.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|NY Open On|
|v_input_2|false|NY Session On|
|v_input_3|false|NY Close On|
|v_input_4|false|Aussie Open On|
|v_input_5|false|Aussie Session On|
|v_input_6|false|Aussie Close On|
|v_input_7|false|Asia Open On|
|v_input_8|false|Asia Session On|
|v_input_9|false|Asia Close On|
|v_input_10|true|Euro Open On|
|v_input_11|true|Euro Session On|
|v_input_12|true|Euro Close On|
|v_input_13|true|Show On Chart|
|v_input_14|true|From Day|
|v_input_15|true|From Month|
|v_input_16|2020|From Year|
|v_input_17|31|To Day|
|v_input_18|12|To Month|
|v_input_19|2020|To Year|
|v_input_20|2|len|
|v_input_21_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_22|200|Length slow|
|v_input_23_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_24|66|sl|
|v_input_25|true|Risk % of equity |


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-08 00:00:00
end: 2023-10-08 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

// strategy(title="2 ma breakout",shorttitle="2 ma breakout", initial_capital=10000,overlay=true, commission_type = strategy.commission.cash_per_contract, commission_value = 0.00008 )
timeinrange(res, sess) => time(res, sess) != 0

//Change false to false = You have to turn on, won't show up by default
//****Always use lowercase letters

doNYOpen = input(defval=false, type = input.bool, title="NY Open On")
doNYSession = input(defval=false, type = input.bool, title="NY Session On")
doNYClose = input(defval=false, type = input.bool, title="NY Close On")

doAussieOpen = input(defval=false, type = input.bool, title="Aussie Open On")
doAussieSession = input(defval=false, type = input.bool, title="Aussie Session On")
doAussieClose = input(defval=false, type = input.bool, title="Aussie Close On")

doAsiaOpen = input(defval=false, type = input.bool, title="Asia Open On")
doAsiaSession = input(defval=false, type = input.bool, title="Asia Session On")
doAsiaClose = input(defval=false, type = input.bool, title="Asia Close On")

doEurOpen = input(defval=true, type = input.bool, title="Euro Open On")
doEurSession = input(defval=true, type = input.bool, title="Euro Session On")
doEurClose = input(defval=true, type = input.bool, title="Euro Close On")

//You can copy and paste these colors. white - silver - gray - maroon - red - purple - fuchsia - green - lime
//   olive - yellow - navy - blue - teal - aqua - orange 

nySessionStart = color.olive
nySession = color.olive
nySessionEnd = color.olive
asiaSessionStart = color.blue
asiaSession = color.blue
asiaSessionEnd = color.blue
europeSessionStart = color.red
europeSession = color.red
europeSessionEnd = color.red
colorwhite = color.white

//****Note ---- Use Military Times --- So 3:00PM = 1500


bgcolor(doAsiaSession and timeinrange(timeframe.period, "1800-0400") ? asiaSession : na, transp=75)
//bgcolor(timeinrange(timeframe.period, "0000-0300") ? color.white  : na, transp=75)
bgcolor(doEurSession and timeinrange(timeframe.period, "0300-1100") ? europeSession : na, transp=75)
bgcolor(doNYSession and timeinrange(timeframe.period, "0800-1600") ? nySession : na, transp=75)

active = input(true, title="Show On Chart")
pricehigh = security(syminfo.tickerid, '60', high[0])
pricelow = security(syminfo.tickerid, '60', low[0])
//Daily Plots
offs_daily = 0 
hiHighs = 0
loLows = 0
//plot(timeinrange(timeframe.period, "0000-0300") and pricehigh ? pricehigh  : na, title="Previous Daily High", style=plot.style_line, linewidth=2, color=color.gray)
//plot(timeinrange(timeframe.period, "0000-0300") and pricelow ? pricelow : na, title="Previous Daily Low", style=plot.style_linebr, linewidth=2, color=color.gray)

if(timeinrange(timeframe.period, "0000-0300"))
    hiHighs = highest(high, 3)
    loLows = lowest(low, 3)
    

// From Date Inputs
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2020, title = "From Year", minval = 1970)
 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2020, title = "To Year", minval = 1970)
 
// Calculate start/end date and time condition
startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true


len = input(2)
src = input(close, title="Source")
out = sma(src, len)

lena = input(200, minval=1, title="Length slow")
srca = input(close, title="Source")
outa = ema(srca, lena)

//tp = input(100, title="tp")
sl = input(66, title="sl")
// if(smabool)
//     out := sma(src, len)
// else if(emabool)
//     out := ema(src, len)
// else if(hmabool)
//     out := hma(src, len)
// else if(vmabool)
//     out := wma(src, len)  
// else if(vwmabool)
//     out := vwma(src, len)   
// else if(smmabool)
//     out := sma(src, len)  
 
plot(out, color=color.white, title="MA")
plot(outa, color=color.white, title="MA")

longC = timeinrange(timeframe.period, "0300-0400") and (crossover(close,out) or crossover(high,out)) and close[1] > outa and time_cond
shortC = timeinrange(timeframe.period, "0300-0400") and (crossunder(close,out) or crossunder(low,out)) and close[1] < outa and time_cond



//inputlondon = input(false, title="london session")
//inputny = input(false, title="new york session")

//if(inputlondon==true)

strategy.initial_capital = 50000

//MONEY MANAGEMENT--------------------------------------------------------------
balance = strategy.netprofit + strategy.initial_capital //current balance
floating = strategy.openprofit          //floating profit/loss
risk = input(1,type=input.float,title="Risk % of equity ")/100           //risk % per trade

temp01 = balance * risk     //Risk in USD
temp02 = temp01/sl        //Risk in lots
temp03 = temp02*100      //Convert to contracts
size = temp03 - temp03%1 //Normalize to 1000s (Trade size)
if(size < 1)
    size := 1         //Set min. lot size


strategy.entry("long",1,when=longC)
//strategy.close("long", when = crossunder(close,out) or not (timeinrange(timeframe.period, "0300-1000")))
strategy.close("long", when =  not (timeinrange(timeframe.period, "0300-0945")))
strategy.exit("x_long","long", loss = sl)
     
    
strategy.entry("short",0,when=shortC)
//strategy.close("short",when = crossover(close,out) or not (timeinrange(timeframe.period, "0300-1000")))
strategy.close("short",when = not (timeinrange(timeframe.period, "0300-0945")))

strategy.exit("x_short","short", loss = sl)

//strategy.exit("closelong", "RSI_BB_LONG" , profit = close * 0.01 / syminfo.mintick, loss = close * 0.01 / syminfo.mintick, alert_message = "closelong")
//strategy.exit("closeshort", "RSI_BB_SHORT" , profit = close * 0.01 / syminfo.mintick, loss = close * 0.01 / syminfo.mintick, alert_message = "closeshort")


```

> Detail

https://www.fmz.com/strategy/428812

> Last Modified

2023-10-09 16:56:21
