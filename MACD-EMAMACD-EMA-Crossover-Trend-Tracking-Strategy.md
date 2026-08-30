
> Name

MACD-EMA Golden Cross Trend Tracking Strategy MACD-EMA-Crossover-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14274a17bd9bd8765a6.png)
[trans]

## Overview
This strategy determines the trend direction by calculating the intersection of the MACD indicator and its moving average signal line, and combines it with the EMA indicator to determine the strength of the current trend to achieve trend tracking. When the MACD line breaks through the signal line from bottom to top, go long, and when it breaks through the signal line from top to bottom, go short. At the same time, the EMA line can also judge the strength of the trend and filter out false breakthroughs.
## Strategy Principle
This strategy is mainly based on the MACD indicator to determine the trend direction and entry timing. The MACD line breaks through the signal line to indicate a reversal in the price trend, so long and short positions are judged based on the direction of the breakthrough. The specific judgment logic is that when the closing price is higher than the EMA average line and the MACD line breaks through the signal line from below, go long; when the closing price is lower than the EMA average line and the MACD line breaks through the signal line from above, go short.
The function of the EMA moving average is to assist in judging the trend. If the price is higher than the EMA moving average, it means that it is in an upward trend. At this time, a breakthrough below the MACD will easily form a running golden cross signal; if the price is lower than the EMA moving average, it means that it is in a downward trend. At this time, a breakthrough above the MACD will easily form a dead cross signal. The length of EMA also determines the mid- to long-term extent of the trend.
Through the above method, you can enter the market in time when the price begins to reverse and form a new trend, thereby achieving the trend following effect.
## Advantage Analysis
This strategy combines dual judgment conditions, not only taking into account the price trend direction, but also using indicators to determine the specific entry opportunity, avoiding the risk of false breakthroughs and enhancing the reliability of the strategy. Compared with using the MACD indicator alone, this strategy can more accurately determine the start of a new trend.
The use of EMA moving average also allows the strategy to filter out the impact of short-term fluctuations to a certain extent and lock in the medium and long-term trends. This is very helpful for exerting the effect of MACD indicator to judge reversal.
In addition, the strategy sets long and short conditions at the same time, which can be applied to the rising and falling market environment, which also enhances the adaptability of the strategy.
## Risk Analysis
The main risk of this strategy is that the MACD indicator itself has a high probability of judging Fakeout, and the signal may be misidentified. At this time, the auxiliary function of EMA is needed, but it may also fail in special market conditions.
In addition, the strategy uses a profit-loss ratio to set stop-loss and stop-profit conditions, which has a certain degree of subjectivity. Improper settings will also affect the effect of the strategy.
Finally, the strategy simply sets the account equity of the opening quantity to 100%, without considering the issue of fund management, which also has certain risks in the real market.

## Optimization direction
This strategy mainly has the following optimization directions:
1. Adding other indicator judgments to form multiple indicator combinations can further avoid the probability of MACD sending out wrong signals. For example, you can consider KDJ, BOLL, etc.
2. The EMA moving average length can be optimized in multiple combinations to find the best parameters for judging the trend direction.
3. The MACD parameter can also be further optimized to find the most accurate parameter value for determining the reversal timing.
4. Add a fund management module, for example, the profit and loss ratio can be used as a dynamic input, and slippage stop loss can also be set.
5. Test the effects of different types of contracts and find the most matching trading type. For example, cryptocurrency, stock index futures, etc.

## Summarize
This MACD EMA golden cross trend tracking strategy is relatively simple and practical overall. It ensures the reliability of the signal through dual indicator judgments and sets reasonable stop-loss and take-profit methods to lock in profits. The main optimization space lies in parameter selection, indicator combination, fund management, etc. If the test is further optimized, I believe this strategy can become one of the most efficient trend following strategies.
||

## Overview  

This strategy determines the trend direction by calculating the crossover between the MACD indicator and its signal line moving average, and judges the strength of the current trend with the EMA indicator to track the trend. It goes long when the MACD line breaks through the signal line upward and goes short when breaking through downward. The EMA line can also judge the strength of the trend to filter out false breakouts.  

## Strategy Logic   

The core of this strategy is to determine the trend direction and entry timing based on the MACD indicator. The crossover between the MACD line and the signal line indicates a reversal in the price trend. Therefore, long and short positions are determined according to the breakout direction. Specifically, when the closing price is above the EMA line and the MACD line breaks through the signal line from below, go long; when the closing price is below the EMA line and the MACD line breaks through the signal line from above, go short.   

The EMA line serves to assist in judging the trend. If the price is above the EMA line, it indicates an upward trend. At this time, a breakthrough from the MACD below is likely to form a golden cross signal. If the price is below the EMA line, it indicates a downward trend. At this time, a breakthrough from above the MACD is likely to form a death cross signal. The EMA length also determines the mid-to-long term degree of the trend judgment.   

In this way, we can enter the market in a timely manner when the price begins to reverse to form a new trend, achieving a trend tracking effect.   


## Advantage Analysis   

This strategy combines dual judgment conditions, taking into account both the trend direction of prices and using indicators to determine specific entry timing, avoiding the risk of false breakouts, and enhances the reliability of the strategy. Compared with using the MACD indicator alone, this strategy can more accurately determine the start of a new trend.   

The application of the EMA line also enables the strategy to filter out the effects of short-term fluctuations and lock in medium and long term trends to some extent. This is very helpful for developing the effectiveness of the MACD indicator in judging reversal.  

In addition, the strategy sets conditions for both long and short, which can be applied to bull and bear kite markets, thus enhancing the adaptability of the strategy.   


## Risk Analysis

The main risk of this strategy is that the MACD indicator itself has a high probability of misjudging Fakeout signals. At this point, the auxiliary function of the EMA line is needed, but failures can still happen in special market conditions.   

In addition, the strategy adopts a profit factor to set stop loss and take profit conditions, which involves some subjectivity. Improper settings may also affect strategy performance.   

Finally, the strategy simply sets the position size to 100% of the account's equity without considering the issue of fund management, which also poses some risks in live trading.  


## Optimization Directions

The main optimization directions for this strategy include:

1. Increase other indicators for judgment to form multiple indicator combinations to further avoid the probability of MACD generating wrong signals. For example, KDJ and BOLL can be considered.  

2. The EMA line length can be multi-parameter optimized to find the optimal parameters for judging trend direction.  

3. The MACD parameters can also be further optimized to find the most accurate values for determining reversal timing.

4. Add a capital management module. For example, the profit factor can be used as a dynamic input, and slippage stops can also be set.  

5. Test the effects on different types of contracts, such as cryptocurrencies, index futures, etc. to find the most suitable trading variety.


## Conclusion   

Overall, this MACD EMA Crossover Trend Tracking strategy is relatively simple and practical. It ensures signal reliability through dual indicator conditions and locks in profits through reasonable stop loss and take profit methods. The main optimization space lies in parameter selection, indicator combinations, capital management, etc. With further optimization and testing, it is believed that this strategy can become one of the most efficient trend tracking strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|FromMonth|
|v_input_2|true|FromDay|
|v_input_3|2020|FromYear|
|v_input_4|true|ToMonth|
|v_input_5|true|ToDay|
|v_input_6|9999|ToYear|
|v_input_7|15|EMA Timeframe|
|v_input_8|206|EMA Length|
|v_input_9|15|Fast Length|
|v_input_10|24|Slow Length|
|v_input_11_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_12|9|Signal Smoothing|
|v_input_13|true|Simple MA (Oscillator)|
|v_input_14|true|Simple MA (Signal Line)|
|v_input_15|true|Enable long?|
|v_input_16|true|Enable short?|
|v_input_17|1.9|ProfitfactorLong|
|v_input_18|46|Lowest Low Lookback|
|v_input_19|2.1|ProfitfactorShort|
|v_input_20|25|highest high lookback|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy(title="MACD EMA Strategy", shorttitle="MACD EMA STRAT", overlay = true, pyramiding = 0, max_bars_back=3000, calc_on_order_fills = false, commission_type =  strategy.commission.percent, commission_value = 0, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, initial_capital=5000, currency=currency.USD)

// Time Range
FromMonth=input(defval=1,title="FromMonth",minval=1,maxval=12)
FromDay=input(defval=1,title="FromDay",minval=1,maxval=31)
FromYear=input(defval=2020,title="FromYear",minval=2016)
ToMonth=input(defval=1,title="ToMonth",minval=1,maxval=12)
ToDay=input(defval=1,title="ToDay",minval=1,maxval=31)
ToYear=input(defval=9999,title="ToYear",minval=2017)
start=timestamp(FromYear,FromMonth,FromDay,00,00)
finish=timestamp(ToYear,ToMonth,ToDay,23,59)
window()=>true

// STEP 2:
// See if this bar's time happened on/after start date
afterStartDate = true

//EMA
emasrc = close
res = input(title="EMA Timeframe", type=input.resolution, defval="15")
len1 = input(title="EMA Length", type=input.integer, defval=206)
col1 = color.yellow
// Calculate EMA
ema1 = ema(emasrc, len1)
emaSmooth = security(syminfo.tickerid, res, ema1, barmerge.gaps_on, barmerge.lookahead_off)
// Draw EMA
plot(emaSmooth, title="EMA", linewidth=1, color=col1)

//MACD
fast_length = input(title="Fast Length", type=input.integer, defval=15)
slow_length = input(title="Slow Length", type=input.integer, defval=24)
src = input(title="Source", type=input.source, defval=close)
signal_length = input(title="Signal Smoothing", type=input.integer, minval = 1, maxval = 50, defval = 9)
sma_source = input(title="Simple MA (Oscillator)", type=input.bool, defval=true)
sma_signal = input(title="Simple MA (Signal Line)", type=input.bool, defval=true)
zeroline = 0

// Plot colors
col_grow_above = #26A69A
col_grow_below = #FFCDD2
col_fall_above = #B2DFDB
col_fall_below = #EF5350
col_macd = #0094ff
col_signal = #ff6a00

// Calculating
fast_ma = sma_source ? sma(src, fast_length) : ema(src, fast_length)
slow_ma = sma_source ? sma(src, slow_length) : ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal ? sma(macd, signal_length) : ema(macd, signal_length)
hist = macd - signal
//plot(hist, title="Histogram", style=plot.style_columns, color=(hist>=0 ? (hist[1] < hist ? col_grow_above : col_fall_above) : (hist[1] < hist ? col_grow_below : col_fall_below) ), transp=0 )
//plot(macd, title="MACD", color=col_macd, transp=0)
//plot(signal, title="Signal", color=col_signal, transp=0)
//plot(zeroline, title="Zero Line", color=color.black, transp=0)

///////////////////////////LONG////////////////////////////////////////////////////////////////////

enablelong = input(true, title="Enable long?")

//Long Signal
upcondition = close > emaSmooth and close[1] > emaSmooth[1]
macdunderhis = macd < zeroline
macdcrossup = crossover(macd, signal)

longcondition = upcondition and macdunderhis and macdcrossup

//strategy buy long
if (longcondition) and (afterStartDate) and strategy.opentrades < 1 and (enablelong == true)
    strategy.entry("long", strategy.long)

//////////////////////////////////////SHORT//////////////////////////////////////////////////////////////////////////////////

enableshort = input(true, title="Enable short?")

//Short Signal
downcondition = close < emaSmooth and close[1] < emaSmooth[1]
macdoverhis = macd > zeroline
macdcrosunder = crossunder(macd, signal)

shortcondition = downcondition and macdoverhis and macdcrosunder

//strategy buy short
if (shortcondition) and (afterStartDate) and strategy.opentrades < 1 and (enableshort == true)
    strategy.entry("short", strategy.short)


//////////////////////////////////////EXIT CONDITION//////////////////////////////////////////////////////////////////////////////////
bought = strategy.position_size[1] < strategy.position_size
sold = strategy.position_size[1] > strategy.position_size
barsbought = barssince(bought)
barssold = barssince(sold)
//////LOWEST LOW//////
//Lowest Low LONG
profitfactorlong = input(title="ProfitfactorLong", type=input.float, step=0.1, defval=1.9)
loLen = input(title="Lowest Low Lookback", type=input.integer,
  defval=46, minval=2)
stop_level_long = lowest(low, loLen)[1]

if strategy.position_size>0 
    profit_level_long = strategy.position_avg_price + ((strategy.position_avg_price - stop_level_long[barsbought])*profitfactorlong)
    strategy.exit(id="TP/ SL", stop=stop_level_long[barsbought], limit=profit_level_long)

//Lowest Low SHORT
profitfactorshort = input(title="ProfitfactorShort", type=input.float, step=0.1, defval=2.1)
highLen = input(title="highest high lookback", type=input.integer,
  defval=25, minval=2)
stop_level_short = highest(high, highLen)[1]

if strategy.position_size<0 
    profit_level_short = strategy.position_avg_price - ((stop_level_short[barssold] - strategy.position_avg_price)*profitfactorshort)
    strategy.exit(id="TP/ SL", stop=stop_level_short[barssold], limit=profit_level_short)
    
//PLOTT TP SL
plot(stop_level_long, title="SL Long", linewidth=1, color=color.red)
plot(stop_level_short, title="SL Short", linewidth=1, color=color.red)
```

> Detail

https://www.fmz.com/strategy/442000

> Last Modified

2024-02-18 15:17:36
