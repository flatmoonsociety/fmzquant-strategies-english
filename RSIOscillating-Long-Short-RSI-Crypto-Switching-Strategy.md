
> Name

Oscillating-Long-Short-RSI-Crypto-Switching-Strategy Oscillating-Long-Short-RSI-Crypto-Switching-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9f62b112e2b6907c15.png)

[trans]

## Overview
The oscillating long-short RSI currency exchange strategy is a quantitative trading strategy for cryptocurrencies. It combines the market technical indicators RSI and ICHIMOKU indicators to identify long and short signals when prices fluctuate, allowing you to buy low and sell high. It is suitable for medium and long-term periods, such as more than 3-4 hours.
## Strategy Principle
The strategy is mainly based on the following indicators and rules:
**ICHIMOKU indicator**
- Tenkan line: the midpoint of the highest and lowest price of the past 20 K lines
- Kijun line: the midpoint of the highest and lowest price of the past 50 K lines
- Senkou A line: the midpoint of Tenkan line and Kijun line
- Senkou B line: the midpoint of the highest and lowest price of the past 120 K lines
- Chikou line: the first 30 K lines of the current K line closing price
**RSI indicator**
- The range is 0-100
- Above 50 is a long signal, below 50 is a short signal
**Admission Rules**
Long entry: Tenkan line crosses Kijun line (golden cross) and price breaks through Senkou A&B line, while RSI is above 50
Short entry: Tenkan line crosses below Kijun line (death cross) and price falls below Senkou A&B line, while RSI is below 50
**Exit Rules**
Stop loss and exit immediately when a signal opposite to entry appears.
This strategy comprehensively considers medium and long-term trends, short-term liquidity and overbought and oversold conditions to capture reversal opportunities in volatile markets. It also sets stop-loss rules to avoid huge losses.
## Advantage Analysis
**1. Comprehensive judgment of multiple indicators to ensure high certainty**
This strategy also considers ICHIMOKU's trend and support and resistance judgments, RSI's overbought and oversold conditions, and the liquidity of the K-line entity direction to ensure the reliability of the signal.
**2. Suitable for volatile market conditions and frequent profits**
The cryptocurrency market is highly volatile, and this strategy can fully capture reversal opportunities in volatile markets and achieve frequent buying low and selling high.
**3. Prevent chasing the rise and killing the fall, and the risks are controllable**
The strategy comprehensively considers the medium- and long-term trends and short-term situations, which can avoid the risk of chasing the rise and killing the fall, and at the same time, set a stop loss to avoid risks.

## Risk Analysis
**1. You may miss some of the running quotes**
This strategy is mainly based on reversal. When a long-term running market occurs, the strategy will frequently oscillate and attack funds.
**2. A single variety cannot diversify risks**
The strategy only trades a single variety and cannot diversify market systemic risks.
**3. Stop loss occurs under extreme market conditions**
In extreme market conditions, such as short gaps, energy bursts, etc., the strategy may trigger stop loss and be forced to leave the market.

## Optimization direction
**1. Add stop loss strategy to reduce single loss**
You can set a trailing stop loss or balance percentage stop loss to lock in profits and prevent profits from returning to zero.
**2. Combined with stock index correlation, diversify market risks**
You can look for trading opportunities in varieties with strong correlation with stock indexes to diversify market systemic risks.
**3. Add conditional filtering and reduce invalid transactions**
Conditional filters such as price volatility and trading volume changes can be set to avoid invalid reversal signals and increase the probability of profit.

## Summarize
The volatile long-short RSI currency exchange strategy comprehensively uses the ICHIMOKU indicator and the RSI indicator to determine the reversal point of the cryptocurrency, which is suitable for buying low and selling high to make profits in a volatile market. It also sets stop loss rules to control risks. This strategy can further enhance the effect by optimizing the stop-loss mechanism, diversifying risks through correlation and setting up conditional filters, and is worthy of real-time verification.
||

## Overview  

The Oscillating Long-Short RSI Crypto Switching Strategy is a quantitative trading strategy designed for cryptocurrencies. It combines the technical indicator RSI with the ICHIMOKU indicator to identify long and short signals during price oscillations and achieve buying low and selling high. It is suitable for medium to long term timeframes such as 3-4 hours or longer.

## Strategy Logic  

The strategy is mainly based on the following indicators and rules:  

**ICHIMOKU Indicator** 
- Tenkan Line: Midpoint of highest and lowest price of last 20 bars  
- Kijun Line: Midpoint of highest and lowest price of last 50 bars
- Senkou A Line: Midpoint of Tenkan and Kijun Line
- Senkou B Line: Midpoint of highest and lowest price of last 120 bars  
- Chikou Line: Closing price of 30 bars ago

**RSI Indicator**
- Range from 0 to 100
- Above 50 indicates bullish signal, below 50 indicates bearish signal

**Entry Rules**   
Long entry: Tenkan cross above Kijun (golden cross) and price breaks through Senkou A&B Lines, with RSI above 50 at the same time  
Short entry: Tenkan cross below Kijun (death cross) and price breaks down Senkou A&B Lines, with RSI below 50 at the same time  

**Exit Rules**  
Exit with opposite signal  

The strategy takes into account the medium to long term trend, short term capital flow and overbought/oversold conditions to capture reversal opportunities during oscillation. It also sets stop loss rules to avoid huge losses.  

## Advantage Analysis   

**1. Judgment based on multiple indicators ensures high certainty**  

The strategy considers ICHIMOKU’s trend and support/resistance judgment, RSI’s overbought/oversold conditions, as well as capital flow based on the direction of candle body. This ensures reliable signals.   

**2. Suitable for oscillation, frequent profit-taking**

Cryptocurrency market has large fluctuations. This strategy can fully capture reversal opportunities during oscillations and achieve frequent buying low and selling high.  

**3. Prevent chasing rises and beating retreats, controllable risk**   

The strategy comprehensively considers medium and long term trends and short term situations to avoid the risk of chasing rises and beating retreats. Meanwhile, stop loss prevents risk.


## Risk Analysis  

**1. May miss some trending opportunities**  

The strategy focuses mainly on reversal, which may lead to frequent whipsaws during prolonged trending phases.  

**2. Single symbol, unable to diversify risk**   

The strategy trades only a single symbol and cannot diversify against systematic market risk.  

**3. Stop loss triggered during extreme moves**   

During extreme market conditions like gap or spikes, stop loss may be triggered forcing exit.  


## Optimization Directions   

**1. Add stop loss for lower single loss**

Moving stop loss or percentage stop loss can be used to lock in profits and prevent full retracement.  

**2. Correlate with indexes to diversify market risk**   

Look for trading opportunities among highly correlated symbols to diversify systematic market risk.  

**3. Additional filters to reduce invalid trades**  

Filters like price volatility or volume changes can be added to avoid invalid reversal signals and improve profitability rate.


## Conclusion  

The Oscillating Long-Short RSI Crypto Switching Strategy combines ICHIMOKU and RSI indicators to identify reversal points for cryptocurrencies, suitable for buying low and selling high profit-taking during oscillations. It also sets stop loss rules to control risk. The strategy can be further enhanced by optimizing stop loss mechanism, diversifying risks through correlation and adding conditional filters, worth live testing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Use Heikin Ashi Candles in Algo Calculations|
|v_input_2|20|Tenkan-Sen Bars|
|v_input_3|50|Kijun-Sen Bars|
|v_input_4|120|Senkou-Span B Bars|
|v_input_5|30|Chikou-Span Offset|
|v_input_6|30|Senkou-Span Offset|
|v_input_7|true|Long Entry|
|v_input_8|true|Short Entry|
|v_input_9|true|From Day|
|v_input_10|true|From Month|
|v_input_11|2019|From Year|
|v_input_12|31|To Day|
|v_input_13|12|To Month|
|v_input_14|2021|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-17 00:00:00
end: 2023-12-24 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=4

strategy(title="Ichimoku + RSI Crypto trending strategy", overlay=true, initial_capital = 1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.1, pyramiding=1  )

UseHAcandles    = input(true, title="Use Heikin Ashi Candles in Algo Calculations")
//
// === /INPUTS ===

// === BASE FUNCTIONS ===

haClose = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, close) : close
haOpen  = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, open) : open
haHigh  = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, high) : high
haLow   = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, low) : low


//Inputs
ts_bars = input(20, minval=1, title="Tenkan-Sen Bars")
ks_bars = input(50, minval=1, title="Kijun-Sen Bars")
ssb_bars = input(120, minval=1, title="Senkou-Span B Bars")
cs_offset = input(30, minval=1, title="Chikou-Span Offset")
ss_offset = input(30, minval=1, title="Senkou-Span Offset")
long_entry = input(true, title="Long Entry")
short_entry = input(true, title="Short Entry")

//Volatility
//vollength = input(defval=1, title="VolLength")
//voltarget = input(defval=0., type=input.float, step=0.1, title="Volatility Target")
//Difference = abs((haClose - haOpen)/((haClose + haOpen)/2) * 100)
//MovingAverage = sma(Difference, vollength)
//highvolatility = MovingAverage > voltarget

////////////////////////////////////////////////////////////////////////////////
// BACKTESTING RANGE
 
// From Date Inputs
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2019, title = "From Year", minval = 1970)
 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2021, title = "To Year", minval = 1970)
 
// Calculate start/end date and time condition
startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true
 
////////////////////////////////////////////////////////////////////////////////

middle(len) => avg(lowest(len), highest(len))

// Ichimoku Components
tenkan = middle(ts_bars)
kijun = middle(ks_bars)
senkouA = avg(tenkan, kijun)
senkouB = middle(ssb_bars)

//RSI
change = change(haClose)
gain = change >= 0 ? change : 0.0
loss = change < 0 ? (-1) * change : 0.0
avgGain = rma(gain, 14)
avgLoss = rma(loss, 14)
rs = avgGain / avgLoss
rsi = 100 - (100 / (1 + rs))

ss_high = max(senkouA[ss_offset-1], senkouB[ss_offset-1])
ss_low = min(senkouA[ss_offset-1], senkouB[ss_offset-1])

// Entry/Exit Signals
tk_cross_bull = tenkan > kijun
tk_cross_bear = tenkan < kijun
cs_cross_bull = mom(haClose, cs_offset-1) > 0
cs_cross_bear = mom(haClose, cs_offset-1) < 0
price_above_kumo = haClose > ss_high
price_below_kumo = haClose < ss_low
rsi_bullish = rsi > 50
rsi_bearish = rs < 50
bullish = tk_cross_bull and cs_cross_bull and price_above_kumo and rsi_bullish //and highvolatility
bearish = tk_cross_bear and cs_cross_bear and price_below_kumo and rsi_bearish //and highvolatility

strategy.entry("Long", strategy.long, when=bullish and long_entry and time_cond)
strategy.entry("Short", strategy.short, when=bearish and short_entry and time_cond)

strategy.close("Long", when=bearish and not short_entry and time_cond)
strategy.close("Short", when=bullish and not long_entry and time_cond)



```

> Detail

https://www.fmz.com/strategy/436511

> Last Modified

2023-12-25 13:49:48
