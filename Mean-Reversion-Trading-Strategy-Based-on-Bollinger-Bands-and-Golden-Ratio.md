
> Name

Mean-Reversion-Trading-Strategy-Based-on-Bollinger-Bands-and-Golden-Ratio
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1626699f83c0d48f3d4.png)
[trans]


## Overview
This strategy uses the golden section of Bollinger Bands and combines it with moving average shape judgment to conduct regression transactions. When the price touches the Bollinger Bands golden section, it is regarded as a buying signal, and the equilibrium return characteristics of the price are used to obtain profits.
## Strategy Principle
1. Calculate the middle track, upper track and golden section lower track of Bollinger Bands
- Middle track: n-period weighted moving average vwma
- Upper rail: middle rail + standard deviation of k * n periods
- Golden section lower track: middle track - 0.618 * standard deviation of n periods
2. Determine the form
- The 50-day moving average crosses the 200-day moving average, which is in line with the upward trend
- Price touches or falls below the lower golden section as a buy signal
3. Exit
- When the price crosses the upper track of Bollinger Bands, it is considered that the price has left the lower track and returned, and the position is closed at this time.
4. Stop loss
- Set a fixed percentage stop loss, such as 5%
## Strategic Advantages
1. Using vwma instead of sma as the middle track of Bollinger Bands can better reflect the moving trend of prices.
2. The golden section is an important support/resistance area, which provides the basis for return
3. The moving averages are arranged in long positions to ensure that the general trend is upward.
4. Fixed stop loss ensures single loss control
## Strategy Risk
1. The golden section is not a definite support, and the price may fall directly below it.
2. Fixed stop loss may be too arbitrary and should be adjusted based on market fluctuations.
3. The long moving average arrangement may also be a false breakthrough and should be judged in conjunction with more indicators.
4. The return length is uncertain and a reasonable take-profit exit point needs to be set.
## Optimization direction
1. Different parameter combinations can be tested, such as Bollinger Band cycle, standard deviation multiples, fixed stop loss percentage, etc.
2. More indicators can be added to determine the market trend and return probability, such as MACD, KD, etc.
3. You can consider dynamic stop loss, stop loss based on ATR or trailing stop loss
4. You can optimize the take-profit strategy, such as moving take-profit, batch take-profit, etc.
## Summarize
This strategy uses the Bollinger Bands golden section to carry out equilibrium return trading. It has the advantages of clear trading logic, simple parameter setting, and controllable drawdowns. However, there are also certain risks, and further testing and optimization are required, and more technical indicator judgments and stop-loss/take-profit tools need to be added before it can be actually applied. Overall, this strategy provides an idea for quantitative trading using the golden section rule, which is worthy of further exploration.
||


## Overview

This strategy uses the golden ratio line of Bollinger Bands combined with moving average formations to trade mean reversions. When the price touches the golden ratio line, it is considered a buy signal to take advantage of the mean reverting tendency.

## Strategy Logic

1. Calculate Bollinger Bands middle band, upper band and golden ratio lower band

- Middle band: vwma of n periods 
- Upper band: Middle band + k * n period standard deviation
- Golden ratio lower band: Middle band - 0.618 * n period standard deviation

2. Judge formations

- 50-day MA above 200-day MA, indicates uptrend
- Price touches or below golden ratio lower band, as buy signal  

3. Exit

- When price breaks above BB upper band, price is considered to have moved away from lower band, close position

4. Stop loss

- Set fixed percentage stop loss, e.g. 5%

## Advantages

1. Using vwma instead of sma for BB middle line better reflects price movement

2. Golden ratio is important support/resistance, provides basis for reversion

3. MA in uptrend ensures overall trend is up

4. Fixed stop loss controls loss for each trade

## Risks

1. Golden ratio line is not guaranteed support, price may break through

2. Fixed stop loss may be arbitrary, should consider adjusting based on volatility

3. MA uptrend may be false breakout, should check more indicators  

4. Unsure of reversion length, need reasonable profit taking exit

## Enhancement

1. Test different combinations of parameters like BB period, SD multiplier, fixed stop loss percentage etc.

2. Add more indicators to determine market trend and reversion probability, e.g. MACD, KD etc.  

3. Consider dynamic stops, such as ATR or trailing stops

4. Optimize profit taking like moving profit stop, partial profit taking etc.

## Summary 

This strategy trades mean reversions using BB golden ratio line, with clear logic, simple parameters, and controllable drawdown. But also has risks, requires further testing and optimization, adding more technical indicators for trend and better stops/exits before actual use. Overall provides idea of using golden ratio in quant trading, worth exploring further.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|BB Length|
|v_input_2_hlc3|0|Source: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_3|1.5|multplier|
|v_input_4|5|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-01 00:00:00
end: 2023-10-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mohanee

//@version=4

strategy(title="Bollinger Band with Fib Golden Ratio (0.618)",  shorttitle="Bollinger Band with Fib Golden Ratio" , overlay=true, pyramiding=1,     default_qty_type=strategy.percent_of_equity,  default_qty_value=20, initial_capital=10000, currency=currency.USD)  

length = input(50,title="BB Length" , minval=1)
src1 = input(hlc3, title="Source")
//mult1 = input(1.33, minval=0.001, maxval=50)
mult = input(1.5,title="multplier", minval=0.001, maxval=50)

stopLoss=input(5,title="Stop Loss",minval=1)

basis = vwma(src1, length)
dev = mult * stdev(src1, length)

//dev3 = mult3 * stdev(src, length)

upper_618= basis + (0.618*dev)
lower_618= basis - (0.618*dev)

//lower_618_dev3= basis - (0.618*dev3)



plot_upper618= plot(upper_618, color=color.purple, linewidth=2, title="0.618")
plot(basis, color=color.purple,style=plot.style_circles,  linewidth=2)

plot_lower618= plot(lower_618, color=color.purple, linewidth=2, title="0.618 entry")
//plot_lower618_dev3= plot(lower_618_dev3, color=color.red, linewidth=1, title="0.618 stop")

//plot_lower618= plot(lower_618, color=color.purple, linewidth=1, title="0.618 entry")

ema200=ema(close,200)
ema50=ema(close,50)

plot (ema200, title="ema200", color=color.orange, linewidth=2)
plot (ema50, title="ema50", color=color.blue , linewidth=2)


longCondition= ema50 > ema200

strategy.entry(id="BB_Fib618", long=true, when = longCondition and ( close < lower_618  or  low <= lower_618)  )

strategy.close(id="BB_Fib618",  comment="points="+tostring(close - strategy.position_avg_price,  "###.##") , when = strategy.position_size >= 1  and crossover(close,upper_618 )) 

//stoploss exit
stopLossVal = strategy.position_size>=1 ?  strategy.position_avg_price * ( 1 - (stopLoss/100) ) : 0.00
strategy.close(id="BB_Fib618", comment="SL="+tostring(close - strategy.position_avg_price,  "###.##"), when=abs(strategy.position_size)>=1 and close < stopLossVal ) //and close > strategy.position_avg_price )

```

> Detail

https://www.fmz.com/strategy/432347

> Last Modified

2023-11-16 16:52:55
