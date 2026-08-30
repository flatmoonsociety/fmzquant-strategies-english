
> Name

Historical Volatility Range Breakout Trading StrategyVolatility-Range-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans] 

## Overview
This strategy determines trading signals based on the historical range of price movements. It calculates the difference between the highest price and the lowest price within a certain period, and forms a fluctuation range through the moving average. When the price breaks through the upper and lower rails of the range, a trading signal is generated. It is a trend following strategy based on price breakouts.
## Strategy Principle
The core indicator of this strategy is the historical volatility of price. The specific calculation method is:
1. Calculate the difference between the highest price and lowest price of N bars in the past, recorded as HL
2. Calculate the average avg(H, L) of the highest and lowest prices of the past N bars.
3. Volatility = HL / avg(H, L)
Where N is the "Volatility Length" parameter.
After getting the volatility, calculate the upper and lower rails:
Upper track = current close + current close * volatility
Lower track = current close - current close * volatility
The upper and lower rails are then smoothed by the WMA moving average, and the parameter is "Average Length".
When the price breaks through the upper band, go long; when the price breaks through the lower band, go short.
The closing signal is given according to the "Exit Type" parameter:
1. When the Exit Type is Volatility MA, the price falls back below the WMA moving average and the position is closed;
2. When the Exit Type is Range Crossover, the price breaks the upper and lower rails and closes the position.
## Strategic Advantages
- Use price volatility, suitable for capturing trending market conditions
- WMA moving average processing makes the range more stable and reliable
- Breakthrough entry makes it easy to grasp the trend turning point
- Loss can be stopped in time if it breaks the moving average or the upper and lower rails
- There is a large space for parameter optimization and can be adjusted for different markets
## Strategy Risk
- Range breakthroughs are prone to the risk of rising and falling.
- It is easy to suffer large losses when the trend reverses
- WMA moving average is sometimes not sensitive enough to identify trend turning points
- Optimizing parameters is not easy and requires a lot of trial and error.
- The risk of retracement is high, so you need to pay attention to fund management
Risks can be reduced by:
- Optimize parameters to make the interval more stable and reliable
- Add other indicators to judge to avoid highs and lows
- Reduce transaction SIZE and focus on fund management
- Consider adding a re-entry mechanism
## Optimization direction
This strategy can be optimized from the following aspects:
1. Parameter optimization  
Find the best parameter combination by testing different Length parameters.
2. Add other indicators for judgment
For example, when the price breaks through the upper track, if MACD also crosses golden at the same time, enter the market to go long.
3. Optimize stop loss methods
It can be optimized to a flexible trailing stop instead of a simple range breakout stop.
4. Add re-entry mechanism
After exiting at stop loss, if the trend continues, you can set re-entry conditions and track the trend again.
5. Optimize warehouse management
Trading positions can be dynamically adjusted according to market volatility.
## Summarize
Generally speaking, this strategy is more suitable for trending markets. It uses the upper and lower rails of volatility to judge the direction and intensity of the trend, and cooperates with the WMA moving average to form a more reliable trading range, thereby generating breakthrough buying and selling points. But there are also some problems, such as lagging trend judgment and stop loss methods that can be improved. We need to conduct a lot of backtesting and optimization based on real trading data, adjust parameter settings and strategy rules, and reduce the probability of mistakes in and out, so that the strategy can perform better in different markets. At the same time, strict fund management is also the key to whether this strategy can be profitable in the long term.
|| 

## Overview

This strategy generates trading signals based on the historical volatility range of the price. It calculates the difference between the highest and lowest prices over a certain period, and forms a volatility range using moving averages. Trading signals are triggered when the price breaks through the upper or lower bands of the range. It belongs to the trend-following breakout strategies.

## Strategy Logic

The core indicator is the historical volatility of the price. The specific calculation is:

1. Calculate the difference between the highest and lowest prices over the past N bars, called HL

2. Calculate the average of the highest and lowest prices over N bars, avg(H, L)  

3. Volatility = HL / avg(H, L)

Where N is the "Volatility Length" parameter. 

After getting the volatility, the bands are calculated as:

Upper Band = Current close + Current close * Volatility

Lower Band = Current close - Current close * Volatility

The bands are then smoothed by WMA with period set as "Average Length".

When price breaks above the upper band, go long. When price breaks below the lower band, go short.

Exit signals are defined by "Exit Type":

1. If Exit Type is Volatility MA, exit when price crosses back below WMA. 

2. If Exit Type is Range Crossover, exit when price crosses back below the bands.

## Advantages

- Volatility catches trending moves well  
- WMA makes the bands more stable and reliable
- Breakout signals catch trend turns timely
- Exits based on WMA/bands cut losses fast
- Much room for parameter tuning for different markets

## Risks

- Breakouts may whipsaw with price reversing 
- Risks large losses at trend reversals
- WMA sometimes lags in detecting trend turns
- Parameter optimization not easy, needs much trial and error
- Larger drawdowns, need good risk management

Risks can be reduced by:

- Optimizing parameters for more reliable bands
- Adding other indicators to avoid whipsaws
- Smaller sizes and better risk management 
- Considering re-entries

## Optimization Directions

The strategy can be improved by:

1. Parameter tuning

  Test different Length values to find optimal combinations.
  
2. Adding other indicators

  For example, when price breaks above upper band, check if MACD also golden crosses.
  
3. Better stop loss

  Optimizing to trailing stops instead of simple range break stops.
  
4. Re-entries

  Set re-entry rules to catch trends again after stops.

5. Position sizing
  
  Dynamically adjust sizes based on market volatility.

## Summary

This strategy works well for trending markets in general by using volatility-based bands to gauge trend strength and WMA to form reliable trading ranges for breakout signals. But some issues exist like lagging trend detection, improvable stops, etc. Extensive backtesting and optimization is needed using real data to adjust parameters and rules, reducing false signals and making it robust across different market conditions. Also strict risk management is key for long-term profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|100|Average Length|
|v_input_int_2|100|Volatility Length|
|v_input_source_1_close|0|Volatility Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_source_2_close|0|Exit Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_string_1|0|Exit Type: Volatility MA|Range Crossover|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-13 00:00:00
end: 2023-09-20 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © wbburgin

//@version=5
strategy("Volatility Range Breakout Strategy [wbburgin]", shorttitle = "VRB Strategy [wbburgin]", overlay=true,
 pyramiding=20,max_bars_back=2000,initial_capital=10000)

wma(float priceType,int length,float weight) =>
    norm = 0.0
    sum = 0.0
    for i = 0 to length - 1
        norm := norm + weight
        sum := sum + priceType[i] * weight
    sum / norm

// This definition of volatility uses the high-low range divided by the average of that range.
volatility(source,length) =>
    h = ta.highest(source,length)
    l = ta.lowest(source,length)
    vx = 2 * (h - l) / (h + l)
    vx

vm1 = input.int(100,"Average Length")
volLen = input.int(100,"Volatility Length")
vsrc = input.source(close,"Volatility Source")
cross_type = input.source(close,"Exit Source")
exit_type = input.string("Volatility MA",options=["Volatility MA","Range Crossover"],title="Exit Type")

volatility = volatility(vsrc,volLen)

highband1 = close + (close * volatility)
lowband1 = close - (close * volatility)
hb1 = wma(highband1,vm1,volatility)
lb1 = wma(lowband1,vm1,volatility)
hlavg = math.avg(hb1,lb1)

upcross = ta.crossover(high,hb1)    //Crossing over the high band of historical volatility signifies a bullish breakout
dncross = ta.crossunder(low,lb1)    //Crossing under the low band of historical volatility signifies a bearish breakout

vlong = upcross
vshort = dncross
vlong_exit = switch
    exit_type == "Volatility MA" => ta.crossunder(cross_type,hlavg)
    exit_type == "Range Crossover" => ta.crossunder(cross_type,hb1)
vshort_exit = switch
    exit_type == "Volatility MA" => ta.crossover(cross_type,hlavg)
    exit_type == "Range Crossover" => ta.crossover(cross_type,lb1)

if vlong
    strategy.entry("Long",strategy.long)
if vlong_exit
    strategy.close("Long")
if vshort
    strategy.entry("Short",strategy.short)
if vshort_exit
    strategy.close("Short")

plot(hlavg,color=color.white,title="Weighted Volatility Moving Average")
t = plot(hb1,color=color.new(color.red,50),title="Volatility Reversal Band - Top")
b = plot(lb1,color=color.new(color.green,50),title="Volatility Reversal Band - Bottom")

alertcondition(vlong,"Volatility Long Entry Signal")
alertcondition(vlong_exit,"Volatility Long Exit Signal")
alertcondition(vshort,"Volatility Short Entry Signal")
alertcondition(vshort_exit,"Volatility Short Exit Signal")

fill(t,b,color=color.new(color.aqua,90))
```

> Detail

https://www.fmz.com/strategy/427507

> Last Modified

2023-09-21 20:38:29
