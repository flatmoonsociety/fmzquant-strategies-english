
> Name

Super-Trend-Daily-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ddb0fabea6e65a4eb736fdff1edbe1939aa68cdb5a708ed46d8de6e3fc6ab7cf.png)
[trans]
## Overview
Super Trend Daily Reversal Strategy is a quantitative trading strategy that uses super trend indicators to determine market trends, calculates stop losses based on price breakthroughs and average true fluctuation ranges, and uses price change rate indicators to filter super trend signals. This strategy is suitable for daily and higher time periods, and can be used in markets such as digital currencies and stocks.
## Strategy Principle
The core indicator of this strategy is the Super Trend Indicator. The super trend indicator is based on the average true range (ATR), which can more clearly judge the market trend direction. When the price breaks through the upper band of the super trend, it is a bearish signal, and when it breaks through the lower band, it is a bullish signal.
This strategy uses the rate of change indicator (ROC) to filter super trend indicators to avoid invalid signals. Only participate in super trend signals when the price volatility is large, otherwise do not participate.
In terms of stop loss, this strategy provides two stop loss methods: fixed stop loss ratio and automatic indentation stop loss based on ATR. Fixed stop loss is simple and straightforward, and ATR stop loss can adjust the stop loss range according to market volatility.
Entry conditions are when the Super Trend indicator reverses and the Price Rate of Change indicator passes the filter. The exit condition is that the super trend reverses again or breaks through the stop loss line. This strategy follows trend following principles and only allows one position in each direction.
## Advantage Analysis
The biggest advantage of this strategy is that it uses the super trend indicator to determine the trend direction with higher clarity and stability, and has less noise than the ordinary moving average. In addition, the strategy adds a price change rate indicator to effectively filter out some false signals.
The ATR adaptive stop loss mechanism also allows the strategy to adapt to a wider range of market environments. When volatility intensifies, the stop loss will be automatically relaxed to lock in profits to the greatest extent.
Judging from the test results, this strategy performed well in the bull market. In the long-term trend with a larger magnitude, the winning rate is very high and the continuous profit cycle is long.
## Risk Analysis
The main risk faced by this strategy is misjudgment of trend reversal, which may miss reversal signals or generate unnecessary reversal signals. This usually occurs when price moves sideways repeatedly near key support or resistance areas.
In addition, if the stop loss setting is too loose, it will also lead to the expansion of losses. ATR stop loss is adjusted according to market volatility, so the stop loss may be wider during market emergencies.
In view of the above risks, the ATR calculation period can be appropriately shortened or the multiple coefficient of the ATR stop loss can be adjusted. Additional indicators can also be added to identify key support and resistance areas to avoid those areas sending misleading signals.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Adjust the parameters of the super trend indicator, optimize the ATR period and ATR multiple, and make the super trend line smoother.
2. Adjust the parameters of the price change rate indicator, optimize the cycle and change rate thresholds, and reduce false signals.
3. Try different stop loss mechanisms, such as trailing stop loss, or optimize the stop loss width of fixed stop loss.
4. Add additional judgment indicators to determine key support and resistance to avoid errors in judgment of trend reversal.
5. Test the parameter settings and effects of different varieties to find the optimal parameter combination.
6. Carry out backtest optimization to find the best parameter settings.
## Summarize
The super trend daily reversal strategy is generally a relatively stable and reliable trend following strategy. It combines super trend indicators and price change rate indicators for filtering, which can effectively identify the direction of medium and long-term trends. The ATR adaptive stop loss mechanism also allows it to adapt to most market environments. By further optimizing parameter settings and adding judgment indicators, the stability and profitability of this strategy can be improved.
||

## Overview  

The Super Trend Daily Reversal Strategy is a quantitative trading strategy that uses the Super Trend indicator to determine market trends, combines price breakthrough and average true range to calculate stop loss, and uses the price change rate indicator to filter Super Trend signals. This strategy is suitable for daily and higher time frames and can be used in markets like cryptocurrencies and stocks.

## Strategy Logic

The core indicator of this strategy is the Super Trend indicator. The Super Trend indicator is based on Average True Range (ATR) and can more clearly determine the direction of market trends. A breakdown of the Super Trend upper rail is a short signal, and a breakdown of the lower rail is a long signal.

The strategy uses the Price Change Rate indicator (ROC) to filter the Super Trend indicator to avoid invalid signals. Only participate in Super Trend signals when price volatility is large, otherwise do not participate.

For stop loss, the strategy provides two stop loss methods: fixed stop loss percentage and ATR based adaptive stop loss. Fixed stop loss is simple and direct. ATR stop loss can adjust the stop loss range according to market volatility.

The entry conditions are a reversal of the Super Trend indicator and the price change rate indicator passes the filter. The exit conditions are that Super Trend reverses again or breaks through the stop loss line. The strategy adheres to the trend tracking principle and only allows one position in each direction.

## Advantage Analysis  

The biggest advantage of this strategy is that the Super Trend indicator has higher clarity and stability in judging trend direction compared to ordinary moving averages, with less noise. In addition, the price change rate indicator effectively filters out some false signals.

The ATR adaptive stop loss mechanism also allows the strategy to adapt to a wider market environment. The stop loss will automatically widen during increased volatility to maximize profits.

From the test results, this strategy performs exceptionally well in a bull market. The win rate is very high in long-term trends of significant magnitude, with long consecutive profitable cycles.

## Risk Analysis

The main risk faced by this strategy is misjudgment of trend reversal, which may miss reversal signals or generate unnecessary reversal signals. This often happens when prices oscillate and consolidate around key support/resistance areas.  

In addition, a stop loss that is set too wide can also lead to greater losses. ATR stop loss adjusts according to market volatility, so stops may be pulled wider during market events.

To address these risks, the ATR calculation period can be shortened appropriately or the ATR stop loss multiplier adjusted. Additional indicators can also be added to determine key support/resistance areas to avoid misleading signals from those areas.

## Optimization Directions 

The strategy can be optimized in the following aspects:

1. Adjust the parameters of the Super Trend indicator to optimize the ATR period and ATR multiples to make the Super Trend line smoother.

2. Adjust the parameters of the price change rate indicator to optimize the period and change rate threshold to reduce false signals.  

3. Try different stop loss mechanisms such as trailing stops, or optimize the stop loss amplitude of fixed stops.

4. Add additional judgment indicators to determine key support/resistance and avoid misjudgment of trend reversals.  

5. Test parameter settings and effects on different products to find the optimal parameter combination.  

6. Conduct backtest optimization to find the best parameter settings.

## Conclusion  

Overall, the Super Trend Daily Reversal Strategy is a relatively stable and reliable trend following strategy. It combines the Super Trend indicator and the price change rate indicator for filtering, which can effectively identify the direction of medium and long term trends. The ATR adaptive stop loss mechanism also enables it to adapt to most market environments. Through further optimization of parameter settings and added judgment indicators, the stability and profitability of this strategy can be improved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|════════ Test Period ═══════|
|v_input_2|2017|Backtest Start Year|
|v_input_3|true|Backtest Start Month|
|v_input_4|true|Backtest Start Day|
|v_input_5|2019|Backtest Stop Year|
|v_input_6|12|Backtest Stop Month|
|v_input_7|31|Backtest Stop Day|
|v_input_8|false|══════ Super Trend ══════|
|v_input_9|3|ATR Period|
|v_input_10|1.3|ATR Multiplier|
|v_input_11|false|══════ Rate of Change ══════|
|v_input_12|30|ROC Length|
|v_input_13|6|ROC % Change|
|v_input_14|false|════════ Stop Loss ═══════|
|v_input_15|0|Stop Loss Type: Fixed|ATR Derived|
|v_input_16|6|Fixed Stop Loss %|
|v_input_17|20|ATR Stop Period|
|v_input_18|1.5|ATR Stop Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-22 00:00:00
end: 2024-02-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Super Trend Daily BF ?", overlay=true, precision=2, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075)

/////////////// Time Frame ///////////////
_1 = input(false,  "════════ Test Period ═══════")
testStartYear = input(2017, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2019, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() => true

///////////// Super Trend /////////////
_2 = input(false,  "══════ Super Trend ══════")
length = input(title="ATR Period", type=input.integer, defval=3)
mult = input(title="ATR Multiplier", type=input.float, step=0.1, defval=1.3)

atr = mult * atr(length)

longStop = hl2 - atr
longStopPrev = nz(longStop[1], longStop)
longStop :=  close[1] > longStopPrev ? max(longStop, longStopPrev) : longStop

shortStop = hl2 + atr
shortStopPrev = nz(shortStop[1], shortStop)
shortStop := close[1] < shortStopPrev ? min(shortStop, shortStopPrev) : shortStop

dir = 1
dir := nz(dir[1], dir)
dir := dir == -1 and close > shortStopPrev ? 1 : dir == 1 and close < longStopPrev ? -1 : dir

///////////// Rate Of Change ///////////// 
_3 = input(false,  "══════ Rate of Change ══════")
source = close
roclength = input(30, "ROC Length",  minval=1)
pcntChange = input(6, "ROC % Change", minval=1)
roc = 100 * (source - source[roclength]) / source[roclength]
emaroc = ema(roc, roclength / 2)
isMoving() => emaroc > (pcntChange / 2) or emaroc < (0 - (pcntChange / 2))

///////////////  Strategy  /////////////// 
long = dir == 1 and dir[1] == -1 and isMoving()
short = dir == -1 and dir[1] == 1 and isMoving()

last_long = 0.0
last_short = 0.0
last_long := long ? time : nz(last_long[1])
last_short := short ? time : nz(last_short[1])

long_signal = crossover(last_long, last_short)
short_signal = crossover(last_short, last_long)

last_open_long_signal = 0.0
last_open_short_signal = 0.0
last_open_long_signal := long_signal ? open : nz(last_open_long_signal[1])
last_open_short_signal := short_signal ? open : nz(last_open_short_signal[1])

last_long_signal = 0.0
last_short_signal = 0.0
last_long_signal := long_signal ? time : nz(last_long_signal[1])
last_short_signal := short_signal ? time : nz(last_short_signal[1])

in_long_signal = last_long_signal > last_short_signal
in_short_signal = last_short_signal > last_long_signal

last_high = 0.0
last_low = 0.0
last_high := not in_long_signal ? na : in_long_signal and (na(last_high[1]) or high > nz(last_high[1])) ? high : nz(last_high[1])
last_low := not in_short_signal ? na : in_short_signal and (na(last_low[1]) or low < nz(last_low[1])) ? low : nz(last_low[1])

since_longEntry = barssince(last_open_long_signal != last_open_long_signal[1]) 
since_shortEntry = barssince(last_open_short_signal != last_open_short_signal[1]) 

/////////////// Dynamic ATR Stop Losses ///////////////
_4 = input(false,  "════════ Stop Loss ═══════")
SL_type = input("Fixed", options=["Fixed", "ATR Derived"], title="Stop Loss Type")
sl_inp = input(6.0, title='Fixed Stop Loss %') / 100
atrLkb = input(20, minval=1, title='ATR Stop Period')
atrMult = input(1.5, step=0.25, title='ATR Stop Multiplier') 
atr1 = atr(atrLkb)

longStop1 = 0.0
longStop1 :=  short_signal ? na : long_signal ? close - (atr1 * atrMult) : longStop1[1]
shortStop1 = 0.0
shortStop1 := long_signal ? na : short_signal ? close + (atr1 * atrMult) : shortStop1[1]

slLong = in_long_signal ? strategy.position_avg_price * (1 - sl_inp) : na
slShort = strategy.position_avg_price * (1 + sl_inp)
long_sl = in_long_signal ? slLong : na
short_sl = in_short_signal ? slShort : na

/////////////// Execution ///////////////
if testPeriod()
    strategy.entry("L", strategy.long, when=long)
    strategy.entry("S", strategy.short, when=short)
    strategy.exit("L SL", "L", stop = SL_type == "Fixed" ? long_sl : longStop1, when=since_longEntry > 0)
    strategy.exit("S SL", "S", stop = SL_type == "Fixed" ? short_sl : shortStop1, when=since_shortEntry > 0)

/////////////// Plotting /////////////// 
bgcolor(long_signal ? color.lime : short_signal ? color.red : na, transp=30)
bgcolor(isMoving() ? dir == 1 ? color.lime : color.red : color.white , transp=80)
```

> Detail

https://www.fmz.com/strategy/442538

> Last Modified

2024-02-22 16:22:28
