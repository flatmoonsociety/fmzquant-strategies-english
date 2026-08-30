
> Name

RSI-of-MACD-Trading-Strategy MACD-of-RSI-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the MACD indicator to determine the trend of the RSI indicator to generate trading signals. It belongs to the type of strategy that uses a combination of indicators for filtering.
## Strategy Principle
This strategy is mainly judged based on two parts of indicators:
1. RSI indicator
Calculate the conventional 14-period RSI value.
2. MACD of RSI
Calculate the MACD value for the RSI indicator. By default, the fast line has 12 periods, the slow line has 26 periods, and the signal line has 9 periods.
When the MACD column of RSI turns from negative to positive, that is, when the MACD fast and slow line crosses golden, it is judged to be a bullish trend and a buy is made.
When the MACD of the RSI turns from positive to negative, that is, when the MACD fast and slow lines cross, it is judged to be a short trend and sold.
The MACD exponential smoothed moving average is used here to determine the long-term trend direction of the RSI itself, thereby generating more accurate trading signals.
## Strategic Advantages
- Use MACD to determine the trend direction of RSI and improve signal accuracy
- RSI as the main indicator, MACD as the auxiliary judgment indicator
- MACD exponential smoothing moving average, stable judgment
- Combined indicators verify each other to avoid highs and lows
- Combined with parameter optimization, it can flexibly adapt to market changes
## Strategy Risk
- Both RSI and MACD may lag and have inaccurate signals
- More false signals will appear when MACD parameters are incorrect
- Based only on a combination of indicators and sensitive to emergencies
- The stop loss method can be further refined and improved
- Parameter optimization needs to be tested separately for different varieties
Risks can be reduced by:
- Optimize the parameter combination of RSI and MACD
- Add other indicators or trading rules for confirmation
- Appropriately relax the stop-profit and stop-loss standards to reduce premature exits
- Consider adding a re-entry mechanism
- Adjust position management to prevent excessive losses in a single transaction
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test parameter combinations of RSI and MACD
2. When the MACD signal is issued, add a second confirmation condition
For example, consider the K-line pattern, trading volume or Bollinger Band position, etc.
3. Optimize the stop-profit and stop-loss strategy and change it to trailing stop-loss
4. Add re-entry mechanism
After exiting with a stop loss, the position can be re-established if the trend continues.
5. Adjust positions based on market volatility
Reduce your position when volatility is high and increase your position when volatility is low
## Summarize
This strategy can effectively improve the accuracy and stability of signals by combining two indicators, RSI and MACD, to verify each other and determine the trend direction. However, parameters still need to be optimized and further confirmed with other technical indicators or trading rules to reduce the possibility of being affected by emergencies. At the same time, attention should be paid to the optimization and improvement of stop loss strategies, as well as fund management to dynamically adjust positions. Only by continuous learning and optimization can we adapt to market changes and obtain sustained and stable returns.
|| 

## Overview

This strategy uses the MACD indicator to determine the trend of the RSI indicator, generating trading signals. It belongs to the indicator combo filter strategy type.

## Strategy Logic

The strategy is based on two main indicators:

1. RSI 
   Calculates the regular 14-period RSI.

2. MACD of RSI
   Calculates MACD values on the RSI, with default fast MA 12, slow MA 26, signal line 9.

When MACD of RSI crosses up, the fast and slow MAs golden cross, it determines an uptrend and goes long. 

When MACD crosses down, the fast and slow MAs dead cross, it determines a downtrend and goes short.

The exponential moving averages of MACD help determine the longer term trend of RSI itself, resulting in more accurate signals.

## Advantages

- MACD judges RSI trend direction for higher accuracy
- RSI as primary indicator, MACD as secondary 
- Exponential MAs make trend determination stable
- Combination verifies each other, avoiding whipsaws
- Parameter tuning provides flexibility for different markets

## Risks

- Both RSI and MACD can lag, leading to inaccurate signals
- Wrong MACD parameters may generate more false signals
- Purely indicator-based, sensitive to sudden events
- Stop loss mechanism needs further improvements 
- Parameter optimization required for different products

Risks can be reduced by:

- Optimizing RSI and MACD parameter combinations
- Adding other filters for confirmation
- Relaxing TP/SL to avoid premature exit
- Considering re-entries 
- Position sizing to limit single loss

## Enhancement Directions

The strategy can be improved from:

1. Testing RSI and MACD parameter combinations

2. Adding secondary confirmation when MACD signals

   e.g. candlestick patterns, volume, Bollinger bands etc.

3. Optimizing stops to trailing stops

4. Adding re-entry rules

   Re-establish positions after stops are hit if trend continues

5. Adjusting position sizes by volatility

   Smaller size during high volatility, larger size in low volatility
   
## Summary

This strategy combines RSI and MACD indicators to verify each other for more accurate and stable trend detection. But parameters need optimization, and additional technical filters or trading rules are required for confirmation, avoiding sudden events. Also stop loss mechanisms and dynamic position sizing are important. Continued learning and optimizing is crucial for adapting to changing market conditions for steady profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|12|fastLength|
|v_input_3|26|slowLength|
|v_input_4|9|signalLength|
|v_input_5|6|monthfrom|
|v_input_6|12|monthuntil|
|v_input_7|true|dayfrom|
|v_input_8|31|dayuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy(title = "MACD of RSI", overlay = false)

//////////////////////// RSI ///////////////////////////

src = close, len = input(14, minval=1, title="Length")
up = sma(max(change(src), 0), len)
down = sma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))


//////////////////////// RSI   //////////////////////////

//////////////// MACD  ////////////////////////////

sourcemacd = rsi 

fastLength = input(12, minval=1), slowLength=input(26,minval=1)
signalLength=input(9,minval=1)


fastMA = ema(sourcemacd, fastLength)
slowMA = ema(sourcemacd, slowLength)

macd = fastMA - slowMA
signal = ema(macd, signalLength)
delta=macd-signal

swap1 = delta>0?green:red

plot(delta,color=swap1,style=columns,title='Histo',histbase=0,transp=20)
p1 = plot(macd,color=blue,title='MACD Line')
p2 = plot(signal,color=red,title='Signal')
fill(p1, p2, color=blue)
hline(0)




/////////////////////////MACD  //////////////////////////


// Conditions



longCond = na
sellCond = na
longCond :=  crossover(delta,0)
sellCond :=  crossunder(delta,0)




monthfrom =input(6)
monthuntil =input(12)
dayfrom=input(1)
dayuntil=input(31)



if (  longCond  ) 
    strategy.entry("BUY", strategy.long, stop=close, oca_name="TREND", comment="BUY")
    
else
    strategy.cancel(id="BUY")


if ( sellCond   ) 

    strategy.close("BUY")






```

> Detail

https://www.fmz.com/strategy/427511

> Last Modified

2023-09-21 20:48:50
