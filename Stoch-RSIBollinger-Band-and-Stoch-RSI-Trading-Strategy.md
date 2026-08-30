
> Name

Bollinger-Band-and-Stoch-RSI-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy combines the Bollinger Bands indicator and the Stoch RSI indicator to achieve multi-indicator combination trading. It is a typical combination indicator strategy type. The strategy determines the trend direction through Bollinger Bands, and Stoch RSI optimizes the entry timing to generate trading signals.
## Strategy Principle
This strategy is mainly judged based on the following two indicators:
1. Bollinger Bands
Calculate the upper, middle and lower bands in Bollinger Bands. A buy signal is generated when the price breaks upward from the lower band.
2. Stoch RSI 

Calculate the Stoch RSI indicator and generate a buy signal when its K line crosses the D line.
The specific trading logic is: when the Bollinger Band upper limit breakthrough and the Stoch RSI indicator golden cross are met at the same time, a buy position is opened.
The conditions for closing the position are take profit or stop loss: when the price touches the upper or middle track of the Bollinger Band again, take profit and close the position; when the price falls below the lower track of the Bollinger Band again, stop loss and close the position.
## Strategic Advantages
- Combination of Bollinger Bands and Stoch RSI two indicators
- Bollinger Bands determine the general trend, Stoch RSI optimizes entry points
- Stoch RSI can effectively filter out false Bollinger Band breakthroughs
- Stop profit and stop loss on the middle track and lower track, risk control is in place
- Various parameters are adjustable and can be optimized for the market
## Strategy Risk
- The moving average indicator lags behind and you may miss the best entry
- Based only on indicators, slow response to emergencies
- The Bollinger Band range is improperly set, and the stop loss and stop profit are invalid.
- Improper setting of Stoch RSI parameters, resulting in too many false signals
- Need to test parameters separately for different varieties
Risks can be reduced by:
- Optimize parameters to improve the accuracy of entry
- Consider adding other filter indicators for confirmation
- Set trailing stop instead of Bollinger Bands stop
- Test parameters separately according to the characteristics of different varieties
- Properly adjust the position management system
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize Bollinger Band parameters
Adjust the upper and lower rail calculation ratio to find the best parameters
2. Optimize Stoch RSI parameters
Find the best matching K and D values
3. Add MACD and other indicators for secondary confirmation
Avoid relying on a single indicator to create false signals   
4. Use Take Profit Trailing Stop instead of Fixed Stop Loss
trailing stop based on price fluctuations   
5. Test parameter combinations according to different varieties
The parameters of different varieties are not necessarily the same and need to be optimized separately.
## Summarize
This strategy uses Bollinger Bands to determine the trend direction and Stoch RSI to optimize the entry timing, realizing the trading advantages brought by the combination of multiple indicators. However, there are also problems such as parameter optimization is difficult and signal accuracy needs to be improved. We can optimize parameters through strict backtesting, add confirmation indicators for filtering, and constantly revise strategy rules based on backtesting results, thereby improving signal accuracy while maintaining the advantage of combined indicator combination judgment. Only continuous learning and optimization can make the strategy more stable and reliable.
|| 

## Overview

This strategy combines the Bollinger Bands and Stoch RSI indicators for multiple indicator trading. It belongs to the typical combined indicators strategy type. The Bollinger Bands determine trend direction and the Stoch RSI optimizes entry timings for trade signals.

## Strategy Logic

The strategy is based on two main indicators:

1. Bollinger Bands

   Calculate the upper, middle and lower bands. A buy signal is generated when price breaks above the lower band.
   
2. Stoch RSI

   Calculate the Stoch RSI indicator. A buy signal is generated when the K line crosses above the D line.
   
The specific trading logic is: open long when both the Bollinger Bands lower breakout and Stoch RSI golden cross occur together.

The exit logic uses the bands for take profit and stop loss: close for profit when price touches the upper or middle band again, close for loss when price breaks back below the lower band. 

## Advantages 

- Combines Bollinger Bands and Stoch RSI
- Bands judge overall trend, Stoch RSI optimizes entry
- Stoch RSI filters false band breakouts
- Middle and lower bands provide exits
- Multiple adjustable parameters for optimizations

## Risks

- MA-based indicators lag, missing best entries 
- Purely indicator-driven, slow reaction to sudden events
- Improper band settings invalidate stops
- Bad Stoch RSI parameters generate false signals
- Separate parameter tuning needed for different products

Risks can be reduced by:

- Optimizing parameters for higher accuracy
- Adding confirming filters like MACD
- Using trailing stops instead of band stops 
- Testing parameters for different products
- Adjusting position sizing system

## Enhancement Directions

The strategy can be improved by:

1. Optimizing Bollinger Bands parameters

   Adjust upper/lower calculation ratios for best fit
   
2. Optimizing Stoch RSI parameters

   Finding optimal K and D values
   
3. Adding confirming indicators like MACD

   Avoid false signals relying on single indicator
   
4. Using trailing profit stops instead of fixed stops

   Trail stops based on price volatility
   
5. Testing parameters separately for different products

   Optimal parameters vary across different products

## Summary 

This strategy leverages the Bollinger Bands for trend direction and Stoch RSI for entry optimization, taking advantage of a multi-indicator approach. But challenges like difficult parameter optimization and signal accuracy exist. Rigorous backtesting for parameter optimization, adding filters, and continuously adjusting rules based on results can improve accuracy while retaining the strengths of a combined system. Persistent optimizations lead to robustness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|bblength|
|v_input_2|2|Multiplier for BB Upper Band|
|v_input_3|2|Multiplier for BB Lower Band|
|v_input_4|6|lengthrsi|
|v_input_5|20|overSold|
|v_input_6|70|overBought|
|v_input_7|3|smoothK|
|v_input_8|3|smoothD|
|v_input_9|14|lengthRSI|
|v_input_10|14|lengthStoch|
|v_input_11_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_12|6|monthfrom|
|v_input_13|12|monthuntil|
|v_input_14|true|dayfrom|
|v_input_15|31|dayuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy(title = "BB+RSI v2", overlay = true)

price=close
////////// ///////  BB /////////////////////////

bblength = input(50)
bbupmult =input(2,step=0.1,title="Multiplier for BB Upper Band")
bblowmult = input(2,step=0.1,title="Multiplier for BB Lower Band")

basis =  sma(close,bblength)

devup = bbupmult * stdev(close, bblength)
devlow = bblowmult * stdev(close, bblength)

upper = basis + devup
lower = basis - devlow
plot(basis, color=red)
p1 = plot(upper, color=blue)
p2 = plot(lower, color=blue)
fill(p1, p2)


bbbuy= crossover(price,lower)
bbsell = crossunder(price,upper) or price>upper or crossunder(price,basis)



//////////////////// BB //////////////////////




////////////////////////  S RSI  /////////////////////

lengthrsi = input(6)
overSold = input( 20 )
overBought = input( 70 )
vrsi = rsi(price, lengthrsi)

smoothK = input(3, minval=1)
smoothD = input(3, minval=1)
lengthRSI = input(14, minval=1)
lengthStoch = input(14, minval=1)
src = input(close, title="RSI Source")

rsi1 = rsi(src, lengthRSI)
k = sma(stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK)
d = sma(k, smoothD)

SRSIbuy=crossover(k,d)

////////////////////// S  RSI  ///////////////////////

// Conditions



longcond = bbbuy and SRSIbuy
closelong = bbsell


monthfrom =input(6)
monthuntil =input(12)
dayfrom=input(1)
dayuntil=input(31)



if (  longcond ) 
    strategy.entry("BUY", strategy.long, stop=close, oca_name="TREND",  comment="BUY")
    
else
    strategy.cancel(id="BUY")


if ( closelong  ) 

    strategy.close("BUY")






```

> Detail

https://www.fmz.com/strategy/427515

> Last Modified

2023-09-21 21:02:02
