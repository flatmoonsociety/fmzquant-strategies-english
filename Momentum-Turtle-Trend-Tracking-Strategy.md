
> Name

Momentum-Turtle-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1e3de510a555ede9ddd.png)

[trans]

## Overview
The Momentum Turtle Trend Following Strategy is a trend following strategy based on the Turtle Trading Rules. It uses the Turtle indicator to identify trends and combines it with the momentum indicator to filter out some noise trades. The main advantage of this strategy is the ability to capture strong price trends and achieve excess returns.
## Strategy Principle
This strategy uses the basic breakout system from the Turtle indicator to determine trend direction. Specifically, when the closing price is higher than the highest price in the past 20 days, it is a bullish signal, and the strategy is to go long; when the closing price is lower than the lowest price in the past 20 days, it is a bearish signal, and the strategy is to go short.
In order to filter out some noise trading, this strategy also adds a momentum factor. If the price volatility is less than 5 ATR, the strategy will not enter the trade. This can avoid losses caused by small trades caused by short and long positions.
After opening a position, the strategy uses the N value breakout exit in the turtle principle to stop the loss. This system sets stops based on the highest and lowest prices of the last 20 days. For example, the stop loss price for a long order is 2N ATR below the lowest price in the past 20 days. The strategy's profit stop method is relatively simple, set to 10% of the total assets of the account.
## Advantage Analysis
The biggest advantage of this strategy is that it combines trend following and momentum management at the same time. The Turtle Trading System can accurately capture the mid-term price trend and avoid being disturbed by market noise. Adding ATR momentum filtering can further reduce the number of unnecessary transactions, thereby greatly increasing profit margins.
Specifically, this strategy has the following advantages:
1. The Turtle indicator is accurate and reliable in judging trends and can effectively track mid-term trends.
2. The momentum filtering mechanism can reduce unnecessary transactions and avoid losing money in the number of transactions.
3. Risk control measures are in place to stop losses in time when the trend reverses.
4. Overall, the strategy parameters are fully optimized and highly consistent with the Turtle Principle.
## Risk Analysis
Although this strategy has a lot of room for optimization, it also has some potential risks that need to be guarded against:
1. Unable to solve the problem of excessive fluctuations in long-term positions. The position sizing of the Turtle system does not consider volatility factors, which may lead to excessive losses in a single transaction.
2. When the market reverses violently, the stop loss price may be breached, resulting in greater than expected losses.
3. The system does not set a profit target, and excessive positions are prone to occur. This will bring the risk of holding on to orders.
## Optimization direction
Based on the above risk analysis, this strategy also has the following main optimization directions:
1. You can consider adding a dynamic position algorithm with volatility adjustment, so that you can proactively reduce your position when the position loss reaches a certain level.
2. Add a reversal mechanism and consider reducing positions or reverse shorting when forming patterns similar to head-and-shoulders tops and double tops.
3. Increase profit target setting. When the accumulated profits reach a certain proportion of the total assets of the account, you can partially reduce your position and recover your profits.
## Summarize
The Momentum Turtle trend following strategy is generally a very practical medium and long-term trend following solution. It also combines the turtle indicator to determine trends and the ATR indicator's shock filtering, which can effectively lock in strong price trends. In addition, the risk control and parameter optimization of the strategy are also very well done, which can reduce the magnitude of retracements. If you continue to add modules such as dynamic position management, reversal mechanism and profit target, the effect of this strategy can be further improved.
||
## Overview

The Momentum Turtle Trend Tracking strategy is a trend following strategy based on the Turtle Trading rules. It uses the Turtle Indicators to identify trends and combines momentum metrics to filter out some noise trades. The main advantage of this strategy is the ability to capture strong price trends and achieve excess returns.  

## Strategy Principle  

This strategy uses the breakout system in the Turtle Indicators to determine the trend direction. Specifically, when the closing price is higher than the highest price over the past 20 days, it is a bullish signal and goes long; when the closing price is lower than the lowest price over the past 20 days, it is a bearish signal and the strategy goes short.

To filter out some noise trades, this strategy also incorporates a momentum factor. If the price fluctuation is less than 5 ATRs, the strategy will not enter trades. This avoids losses from whipsaws in sideways markets.   

After opening positions, the strategy uses the N-breakout exits in the original Turtle rules for stop loss. This system sets the stop loss based on the highest and lowest prices over the past 20 days. For example, the stop loss for long positions would be 2N ATRs below the lowest low over the past 20 days. The profit taking for this strategy is simple - set at 10% of total account value.

## Advantage Analysis 

The biggest advantage of this strategy is that it combines both trend following and momentum management. The Turtle system can accurately capture mid-term trends in prices without being disturbed by market noise. The additional ATR momentum filter further reduces unnecessary number of trades, thus greatly increasing profit potential.   

Specifically, this strategy has the following strengths:  

1. Turtle indicators accurately identify trends and track mid-term trends.  
2. Momentum filters reduce unnecessary trades and avoid losing on trade frequency.
3. Solid risk control measures allow timely stop losses when trends reverse.  
4. Overall the strategy tuning aligns well with original Turtle principles.  

## Risk Analysis

Although there is large potential for further optimization, the strategy also carries some risks to guard against:  

1. Fails to address excessive fluctuations for long-term holdings. Turtle position sizing does not consider volatility which may lead to oversized losses.
2. Stop loss prices risk being taken out during extreme reversals, leading to higher than expected losses.  
3. Lack of profit targets means excessive holdings and risk of holding underwater positions.  

## Enhancement Opportunities  

Based on the above risks, the main optimization opportunities include:  

1. Consider dynamic position sizing models adjusted for volatility to trim size on losing trades.  
2. Add reversal mechanisms to reduce or reverse on topping patterns like head & shoulders or double tops. 
3. Add profit targets so that holdings are reduced when cumulative profits reach a % of total capital.   

## Conclusion  

Overall the Momentum Turtle Trend Tracking strategy is a robust system for mid to long term trend following. It combines Turtle indicators for trend identification and ATR filters for volatility management to capture strong trends. Additionally risk controls and parameter tuning are solid to reduce drawdowns. Further enhancements like dynamic sizing, reversals and profit taking can improve performance.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2017|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2029|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|31|Backtest Stop Day|
|v_input_7|30|roclength|
|v_input_8|7|pcntChange|
|v_input_9|2|Stop Loss %|
|v_input_10|5000|Take Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-23 00:00:00
end: 2023-11-22 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Heiken Ashi BF ?", overlay=false, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075)

/////////////// Time Frame ///////////////
testStartYear = input(2017, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2029, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() => true

///////////// HA /////////////
haTicker = heikinashi(syminfo.tickerid)
haOpen = security(haTicker, "D", open)
haHigh = security(haTicker, "D", high)
haLow = security(haTicker, "D", low)
haClose = security(haTicker, "D", close)

///////////// Rate Of Change ///////////// 
source = close
roclength = input(30, minval=1)
pcntChange = input(7.0, minval=1)
roc = 100 * (source - source[roclength]) / source[roclength]
emaroc = ema(roc, roclength / 2)
isMoving() => emaroc > (pcntChange / 2) or emaroc < (0 - (pcntChange / 2))

/////////////// Strategy ///////////////
long = haOpen < haClose and isMoving()
short = haOpen > haClose and isMoving()

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

sl_inp = input(2.0, title='Stop Loss %') / 100
tp_inp = input(5000.0, title='Take Profit %') / 100
 
take_level_l = strategy.position_avg_price * (1 + tp_inp)
take_level_s = strategy.position_avg_price * (1 - tp_inp)

since_longEntry = barssince(last_open_long_signal != last_open_long_signal[1])
since_shortEntry = barssince(last_open_short_signal != last_open_short_signal[1]) 

slLong = in_long_signal ? strategy.position_avg_price * (1 - sl_inp) : na
slShort = strategy.position_avg_price * (1 + sl_inp)
long_sl = in_long_signal ? slLong : na
short_sl = in_short_signal ? slShort : na

/////////////// Execution ///////////////
if testPeriod()
    strategy.entry("L",  strategy.long, when=long)
    strategy.entry("S", strategy.short, when=short)
    strategy.exit("L SL", "L", stop=long_sl, limit=take_level_l, when=since_longEntry > 0)
    strategy.exit("S SL", "S", stop=short_sl, limit=take_level_s, when=since_shortEntry > 0)

/////////////// Plotting ///////////////
plotcandle(haOpen, haHigh, haLow, haClose, title='HA Candles', color = haOpen < haClose ? color.lime : color.red)
bgcolor(isMoving() ? long ? color.lime : short ? color.red : na : color.white, transp=70)
bgcolor(long_signal ? color.lime : short_signal ? color.red : na, transp=50)
```

> Detail

https://www.fmz.com/strategy/432979

> Last Modified

2023-11-23 11:53:27
