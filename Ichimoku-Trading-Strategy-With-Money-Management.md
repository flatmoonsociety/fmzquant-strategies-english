
> Name

Ichimoku-Trading-Strategy-With-Money-Management
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f9957d4947d6080f6558849cd46124ea67ca997c9dc77b8638471f98cb8b896d.png)
[trans]

### Overview
This is a long-only stock trading strategy based on the Ichimoku Kinko Hyo indicator. This strategy uses the basic principles of Ichimoku to determine when to enter and exit the market.
### Strategy Principles
The strategy first calculates the components of the Ichimoku equilibrium, including Tenkan-Sen, Kijun-Sen, leading line (Senkou Span A) and delay line (Senkou Span B).
Enter the market long when the following conditions are met:
- Tianji line crosses the baseline, indicating that the short-term moving average crosses the long-term moving average, which is a golden cross signal
- The price crosses the cloud chart, indicating that the stock price has found support and started to rise.
- The future cloud is red, indicating that the future trend is upward
- The distance between the price and Tianji line is less than 2 times ATR, indicating that the price is not artificially high and is in line with the chasing strategy.
- The price is less than 3 times ATR from the baseline, indicating that the price is not artificially high and is in line with the chasing strategy.
- Both the Tenji Line and the Base Line are above the cloud chart, indicating that the trend of Ichimoku is upward
When the following conditions are met, the position will be closed and exited:
- The Tianji line crosses below the baseline, indicating that the short-term moving average crosses below the long-term moving average, which is a dead cross signal.
- The price falls below the cloud chart, indicating that the stock price has lost support
- Or if the profit exceeds 30%, follow the take-profit strategy
- Or if the loss exceeds 3%, follow the stop loss strategy
### Advantage Analysis
- Use the Ichimoku Balance indicator to judge stock price trends with high accuracy
- Combine with ATR to control the pursuit of rising prices and stop falling, and avoid overbought and oversold
- Judge multiple signals at the same time to avoid false signals
- Cover-up strategy can accelerate profits
### Risk Analysis
- The Ichimoku signal may lag behind and needs to be judged in conjunction with other indicators
- Wrong ATR parameter settings may lead to overbought and oversold conditions
- Cover-up strategy may increase the risk of loss
- Need to manually determine parameters, different stocks have different parameters
### Optimization direction
- Can be combined with other indicators such as MACD and KDJ to confirm signals
- You can increase the take-profit range and reduce the stop-loss range
- Can automatically optimize ATR parameters based on historical data
- You can study the parameter differences of stocks in different industries and establish a parameter pool
### Summarize
This is a very practical stock trading strategy. It uses Ichimoku to judge the trend, ATR to control risks, and make profits by chasing the rise and stopping the fall. This strategy has obvious advantages. After parameter optimization and combination indicator optimization, the effect will be better, and it is suitable for real trading.
||

### Overview

This is an Ichimoku Kinko Hyo indicator based long-only stock trading strategy. The strategy utilizes the basic principles of Ichimoku to determine entries and exits.  

### Strategy Logic

The strategy first calculates the components of Ichimoku, including Tenkan-Sen, Kijun-Sen, Senkou Span A, and Senkou Span B.

Long entry if the following conditions are met:
- Tenkan cross above Kijun, indicating short term MA cross above long term MA, which is a golden cross signal  
- Price above Kumo cloud, indicating the price finds support and starts to rise
- Future Kumo is red, indicating future trend is up
- Price distance from Tenkan < 2 x ATR, indicating price is not overextended for chase strategy  
- Price distance from Kijun < 3 x ATR, indicating price is not overextended for chase strategy
- Tenkan and Kijun above Kumo cloud, indicating Ichimoku trend is up

Exit if the following conditions are met: 
- Tenkan cross below Kijun, indicating dead cross 
- Price penetration Kumo cloud, indicating loss of support
- Profit > 30%, implementing profit taking strategy
- Loss > 3%, implementing stop loss strategy

### Advantage Analysis 

- Utilize Ichimoku to determine price trend with high accuracy
- Incorporate ATR to control chasing, avoiding overbought and oversold
- Filter signals with multiple confirmations, avoiding false signals
- Add-on strategy could accelerate profit

### Risk Analysis

- Ichimoku signals could lag, requiring confirmations from other indicators
- Wrong ATR parameters could lead to overbought and oversold
- Add-on strategy could increase loss risk  
- Parameters need to be tuned manually for different stocks

### Optimization Directions

- Incorporate other indicators like MACD, KDJ for signal confirmation
- Increase profit taking level, decrease stop loss level
- Auto tune ATR parameters based on historical data
- Research parameter differences for various sectors, build parameter pool

### Summary

This is a very practical stock trading strategy, utilizing Ichimoku for trend and ATR for risk control, profiting from chase strategy with stop loss. The advantages are obvious. Further optimizations on parameters and combining indicators would make it even better for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|Tenkan-Sen Period|
|v_input_int_2|26|Kijun-Sen Period|
|v_input_int_3|52|Senkou-Span B Period|
|v_input_int_4|26|Chikou-Span Offset|
|v_input_int_5|26|Senkou-Span Offset|
|v_input_int_6|true|Start Date|
|v_input_int_7|true|Start Month|
|v_input_int_8|1980|Start Year|
|v_input_int_9|true|En Date|
|v_input_int_10|true|End Month|
|v_input_int_11|2100|End Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// Author Obarut
//@version=5
strategy("İchimoku Strategy With Money Management",overlay=true)

//Inputs
ts_period = input.int(9, minval=1, title="Tenkan-Sen Period")
ks_period = input.int(26, minval=1, title="Kijun-Sen Period")
ssb_period = input.int(52, minval=1, title="Senkou-Span B Period")
cs_offset = input.int(26, minval=1, title="Chikou-Span Offset")
ss_offset = input.int(26, minval=1, title="Senkou-Span Offset")


// Back Testing Period

fromday = input.int(defval=1,title="Start Date",minval=1,maxval=31) 
frommonth = input.int(defval=1,title="Start Month",minval=1,maxval=12)
fromyear = input.int(defval=1980,title="Start Year",minval=1800, maxval=2100)
today = input.int(defval=1,title="En Date",minval=1,maxval=31)
tomonth = input.int(defval=1,title="End Month",minval=1,maxval=12)
toyear =input.int(defval=2100,title="End Year",minval=1800,maxval=2200)


start=timestamp(fromyear,frommonth,fromday,00,00)
finish=timestamp(toyear,tomonth,today,00,00)
timewindow= time>=start and time<=finish

middle(len) => math.avg(ta.lowest(len), ta.highest(len))

// Ichimoku Components

tenkan = middle(ts_period)
kijun = middle(ks_period)
senkouA = math.avg(tenkan, kijun)
senkouB = middle(ssb_period)


atr = ta.atr(14)
ss_above = math.max(senkouA[ss_offset-1], senkouB[ss_offset-1])
ss_below = math.min(senkouA[ss_offset-1], senkouB[ss_offset-1])

// Price Distance From Tenkan

distance = close - tenkan

// Price Distance from Kijun

distancek = close - kijun

// Entry/Exit Signals

tk_cross_kijun_bull = tenkan >= kijun
tk_cross_kijun_bear = tenkan <= kijun
cs_cross_bull = ta.mom(close, cs_offset-1) > 0
cs_cross_bear = ta.mom(close, cs_offset-1) < 0
price_above_kumo = close > ss_above
pbsenkA = close < ss_above
pasenkB = close > ss_below
price_below_kumo = close < ss_above
future_kumo_bull = senkouA > senkouB
future_kumo_bear = senkouA < senkouB
// Price Distance From Tenken
disbull = distance < 2*atr
//Price Distance From Kijun
disbullk = distancek < 3*atr
//Price Above Tenkan Condition
patk = close > tenkan
// Kijun Above Senkou Span Condition
kjasenkA = kijun > ss_above
// Price Below Kijun Condition
pbkijun = close < kijun

//Bullish Condition

bullish= tk_cross_kijun_bull and cs_cross_bull and price_above_kumo and future_kumo_bull and patk and disbull and disbullk 
     and (tenkan>ss_above) and (kijun>ss_above)

if(bullish and timewindow )
    strategy.entry("Long Entry", strategy.long)

// Bearish Condition

bearish=tk_cross_kijun_bear and pbsenkA and cs_cross_bear  
      or pbkijun or price_below_kumo 

lastentryprice = strategy.opentrades.entry_price(strategy.opentrades - 1)

// Take Profit or Stop Loss in Bearish

if(bearish and timewindow or (close>1.30*lastentryprice and close<kijun ) or (close< 0.93*lastentryprice))
    strategy.close("Long Entry")




if(time>finish)
    strategy.close_all("time up")


plot(tenkan, color=#0496ff, title="Tenkan-Sen")
plot(kijun, color=#991515, title="Kijun-Sen")
plot(close, offset=-cs_offset+1, color=#2e640e, title="Chikou-Span")
sa=plot(senkouA, offset=ss_offset-1, color=color.rgb(17, 122, 21), title="Senkou-Span A")
sb=plot(senkouB, offset=ss_offset-1, color=color.rgb(88, 8, 8), title="Senkou-Span B")
fill(sa, sb, color = senkouA > senkouB ? color.rgb(198, 234, 198) : color.rgb(208, 153, 153), title="Cloud color")
```

> Detail

https://www.fmz.com/strategy/435158

> Last Modified

2023-12-12 17:32:08
