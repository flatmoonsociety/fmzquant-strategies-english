
> Name

Trading strategy based on Bollinger Bands and Fibonacci retracement ratio Bollinger-Bands-Fibonacci-Retracement-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses Bollinger Bands to determine the price channel, and combines it with Fibonacci retracement ratios to determine support and resistance levels to achieve automated trading. The strategy identifies Bollinger Band breakthroughs and tracks retracement points, and conducts buying or selling operations in high-probability retracement areas.
## Strategy Principle
1. Calculate the middle track, upper track and lower track in Bollinger Bands
- Use SMA and ATR to calculate the middle, upper and lower rails    
- Bollinger Bands channels expand and contract with market fluctuations    
2. Calculate the price level corresponding to the Fibonacci retracement ratio
- Take the product of ATR and Fibonacci sequence ratio as the retracement ratio    
- Calculate multiple Fibonacci retracement levels based on the mid-range    
3. Monitor the price to break through the upper and lower Bollinger Bands
- Consider going long when the price breaks through the upper track    
- Consider shorting when the price breaks through the lower band.    
4. Set entry and stop-loss and take-profit near Fibonacci retracement levels
- Enter when price retraces to Fibonacci retracement zone    
- Set Stop Loss and Take Profit on the other side of the retracement zone    
## Advantage Analysis
- Bollinger Bands can clearly identify market fluctuation ranges and trends
- Fibonacci retracement ratio controls key support and resistance areas
- Combined with indicator signals, automatic trading can be realized
- Callback entry increases the success rate and avoids chasing highs and selling lows.
- Can adapt to different cycles and varieties by adjusting parameters
## Risk Analysis
- Bollinger Bands breakthrough may be a false breakthrough, generating false signals
- Unable to accurately predict when price will retrace to Fibonacci levels
- Improper selection of stop loss points may expand losses
- If the correction amplitude is too large or too small, it will affect the strategy effect.
- The strategy fails when the parameters are unreasonable or the market continues to be directional.
- Optimize Bollinger Bands judgment logic, consider more energy indicators, dynamically adjust retracement zones, etc.
## Optimization direction
- Optimize Bollinger Band parameters to improve judgment of trends, support and resistance
- Add volume energy indicator to judge the effectiveness of breakthrough signals
- Use machine learning to assist in determining the probability of callbacks
- Verify trading signals with more technical indicators
-Select reasonable parameters based on product characteristics and trading periods
- Timely adjust the strength of the retracement zone to adapt to changing volatility
## Summarize
This strategy integrates the advantages of Bollinger Bands and Fibonacci Retracement Ratio indicators to identify the trend direction and enter the market at high-probability retracement points. The risk improvement effect can be reduced by optimizing parameters, adding verification indicators, and dynamically adjusting retracement zones. The strategy space can still be expanded, such as adding volume and energy indicators, machine learning, etc. to improve the effect, and it will become mature in continuous optimization.
||


## Overview

This strategy identifies price channels using Bollinger Bands and determines support/resistance levels based on Fibonacci retracement ratios for algorithmic trading. It detects Bollinger Bands breakouts, tracks retracement levels, and enters long/short positions around high-probability pullback zones.

## Strategy Logic

1. Calculating middle, upper and lower bands of Bollinger Bands

    - Middle band is SMA, upper/lower bands are SMA +/- multiples of ATR 

    - Bollinger Bands expand and contract based on market volatility

2. Calculating Fibonacci retracement levels based on ratios

    - Retracement ratios are multiples of ATR * Fibonacci ratios

    - Multiple Fib levels are calculated based on middle band

3. Monitoring price breaking out of Bollinger Bands

    - Consider going long when price breaks above upper band
    
    - Consider going short when price breaks below lower band

4. Entering trades and setting SL/TP around Fib retracement zones

    - Enter trades when price pulls back to Fib zone

    - Set stop loss and take profit on the other side of the zone

## Advantage Analysis

- Bollinger Bands clearly identify market volatility range and trends

- Fibonacci ratios grasp key support and resistance levels  

- Combining indicators allows algorithmic trading

- Pullback entries increase probability of success and avoid chasing

- Adjustable parameters adapt to different periods and products

## Risk Analysis

- Bollinger Bands breakouts may be false signals

- Difficult to predict precisely when price will retrace to Fib levels 

- Improper stop loss placement could increase losses

- Insufficient or excessive pullback magnitude affects strategy

- Ineffective parameters or persistent trending markets could invalidate strategy

- Enhancing Bollinger Bands logic, considering volume, dynamic zone adjustment, etc.

## Optimization Directions

- Optimize Bollinger Bands parameters for better trend and S/R judgment

- Add volume indicators to validate breakout signals

- Utilize machine learning for pullback probability prediction

- Incorporate more technical indicators for signal validation

- Select reasonable parameters based on product characteristics and trading sessions

- Timely adjust pullback zone strength for changing volatility

## Conclusion

This strategy combines the strengths of Bollinger Bands and Fibonacci retracements to identify trends and enter at high-probability pullback levels. Risks can be reduced and results improved by parameter optimization, additional signal validation, dynamic zone adjustment, etc. There is room for expansion by incorporating volume, machine learning models, etc. The strategy can be further refined through continuous optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|false|Offset|
|v_input_4|1.618|Fibonacci Ratio 1|
|v_input_5|2.618|Fibonacci Ratio 2|
|v_input_6|4.236|Fibonacci Ratio 3|
|v_input_7|false|Use Reverse Buy?|
|v_input_8|0|Fibonacci Buy: Fibo 1|Fibo 2|Fibo 3|
|v_input_9|false|Use Reverse Sell?|
|v_input_10|0|Fibonacci Sell: Fibo 1|Fibo 2|Fibo 3|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-27 00:00:00
end: 2023-09-26 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(shorttitle="BBands Fibo", title="Bollinger Bands Fibonacci Ratios", overlay=true)

length      =   input(20, minval=1, type=input.integer, title="Length")
src         =   input(close, title="Source")
offset      =   input(0, "Offset", type = input.integer, minval = -500, maxval = 500)
fibo1       =   input(defval=1.618, title="Fibonacci Ratio 1")
fibo2       =   input(defval=2.618, title="Fibonacci Ratio 2")
fibo3       =   input(defval=4.236, title="Fibonacci Ratio 3")

fiboBuyReverse = input(false, title = "Use Reverse Buy?")
fiboBuy       =   input(options = ["Fibo 1", "Fibo 2", "Fibo 3"],defval = "Fibo 1", title="Fibonacci Buy")
fiboSellReverse = input(false, title = "Use Reverse Sell?")
fiboSell       =   input(options = ["Fibo 1", "Fibo 2", "Fibo 3"],defval = "Fibo 1", title="Fibonacci Sell")

sma = sma(src, length)
atr = atr(length)

ratio1 = atr * fibo1
ratio2 = atr * fibo2
ratio3 = atr * fibo3

upper3 = sma + ratio3
upper2 = sma + ratio2
upper1 = sma + ratio1

lower1 = sma - ratio1
lower2 = sma - ratio2
lower3 = sma - ratio3

plot(sma, style=0, title="Basis", color=color.orange, linewidth=2, offset = offset)

upp3 = plot(upper3, transp=90, title="Upper 3", color=color.teal, offset = offset)
upp2 = plot(upper2, transp=60, title="Upper 2", color=color.teal, offset = offset)
upp1 = plot(upper1, transp=30, title="Upper 1", color=color.teal, offset = offset)

low1 = plot(lower1, transp=30, title="Lower 1", color=color.teal, offset = offset)
low2 = plot(lower2, transp=60, title="Lower 2", color=color.teal, offset = offset)
low3 = plot(lower3, transp=90, title="Lower 3", color=color.teal, offset = offset)

fill(upp3, low3, title = "Background", color=color.new(color.teal, 95))

targetBuy = fiboBuy == "Fibo 1" ? upper1 : fiboBuy == "Fibo 2" ? upper2 : upper3
targetBuy := fiboBuyReverse == false ? targetBuy : fiboBuy == "Fibo 1" ? lower1 : fiboBuy == "Fibo 2" ? lower2 : lower3
buy = low < targetBuy and high > targetBuy

targetSell = fiboSell == "Fibo 1" ? lower1 : fiboSell == "Fibo 2" ? lower2 : lower3
targetSell := fiboSellReverse == false ? targetSell : fiboSell == "Fibo 1" ? upper1 : fiboSell == "Fibo 2" ? upper2 : upper3
sell = low < targetSell and high > targetSell

strategy.entry("Buy", true, when = buy)
strategy.entry("Sell", false, when = sell)

```

> Detail

https://www.fmz.com/strategy/427994

> Last Modified

2023-09-27 16:52:05
