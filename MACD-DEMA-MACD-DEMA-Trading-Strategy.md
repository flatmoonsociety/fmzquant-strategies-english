
> Name

MACD-DEMA-Trading-Strategy MACD-DEMA-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy combines the MACD and DEMA dual-track indicators to form trading signals through the golden cross of the long and short lines. The strategy captures the turning point of the MACD indicator and uses DEMA filtering to denoise to achieve better entry.
## Strategy Principle
1. Calculate the fast line DEMAfast, take the DEMA value of the price, and the period length is fastmacd.
2. Calculate the slow line DEMAslow, take the DEMA value of prices, and the period length is slowmacd.
3. The MACD line is the difference between the fast and slow lines: DEMAfast - DEMAslow.
4. The Signal line is the DEMA value of the MACD line, and the period length is signalmacd.
5. The intersection of long and short lines serves as a trading signal: go long with a golden cross, and go short with a dead cross.
6. Add year, month and day filtering to only send signals within the specified date range.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Combining MACD and DEMA, the indicators are complementary. MACD captures transitions, and DEMA filtering improves signal quality.
2. The DEMA dual-rail design can reduce the hysteresis and noise of the MACD indicator.
3. The intersection of long and short lines is easy to judge, and the signal generation is simple and clear.
4. The trading date range can be flexibly set to adapt to different strategic needs.
5. MACD parameters can be optimized and combined to flexibly respond to various market conditions.
## Risk Analysis
The main risks of this strategy are as follows:
1. As a trend tracking indicator, MACD is not suitable for volatile sideways markets.
2. Long-short crosses may produce false signals and must be effectively filtered.
3. The stop loss strategy is imperfect and it is easy to make the stop loss too large.
4. Parameter optimization is not comprehensive, and the effects of different varieties vary greatly.
5. The transaction date filtering is too rigid and needs to be adjusted dynamically.
Corresponding solutions:
1. Combine with momentum indicators to avoid sideways trading.
2. Add price conditions to filter out false cross signals.
3. Set reasonable initial stop loss and trailing stop loss.
4. Test the effects of multiple varieties of parameters and dynamically optimize.
5. Adjust the filter date according to real-time market conditions.
## Optimization direction
This strategy can consider the following optimization points:
1. Add trading volume indicator for signal filtering.
2. Optimize the MACD parameter combination and test different varieties of data.
3. Set up stop loss strategies, such as fixed stop loss, trailing stop loss, etc.
4. Dynamically adjust the stop loss position according to the degree of market volatility.
5. Track the strength of the trend and adjust the position size.
## Summarize
The MACD DEMA strategy combines the advantages of dual indicators and uses cross signals to capture trends. However, MACD has hysteresis in nature, so attention should be paid to filtering out false signals. In addition, the stop loss strategy needs to be optimized to reduce irrational stop losses. During the real offer, it is recommended to enter the market cautiously based on the parameter optimization results and continue to optimize.
|| 

## Overview 

This strategy combines the MACD and DEMA dual-rail indicators to generate trading signals from crossovers. It captures turning points of the MACD indicator and uses DEMA for filtering to achieve better entries.

## Strategy Principle

1. Calculate fast line DEMAfast as DEMA value of price with period length fastmacd.

2. Calculate slow line DEMAslow as DEMA value of price with period length slowmacd. 

3. MACD Line is difference between fast and slow lines: DEMAfast - DEMAslow.

4. Signal line is DEMA value of MACD line with period signalmacd.

5. Crossovers between MACD and signal lines generate trade signals: long on golden cross, short on death cross.

6. Add date filters to only generate signals within specified date range.

## Advantage Analysis

The main advantages of this strategy are:

1. Combining MACD and DEMA complements the indicators. MACD captures turns, DEMA filters to improve signal quality.

2. DEMA dual rails design reduces lagging and noise of MACD indicator.

3. MACD crossover signals are easy to interpret, clean and simple.

4. Flexible setting of date filters caters to different strategy needs.

5. MACD parameters can be optimized for flexibility across market conditions.

## Risk Analysis

Main risks of this strategy:

1. MACD struggles as trend following indicator in choppy sideways markets. 

2. Crossovers may generate false signals, needs effective filtering.

3. Stop loss strategy not robust, prone to oversized stops.

4. Parameter optimization not comprehensive enough, big performance difference across products.

5. Date filters too rigid, needs dynamic adjustment.

Solutions:

1. Add momentum indicator to avoid sideways market. 

2. Add price conditions to filter out false crosses.

3. Set reasonable initial and trailing stop loss. 

4. Test parameters across products, dynamic optimization.

5. Adjust filter dates based on real-time conditions.

## Optimization Directions

Some potential improvements for the strategy:

1. Add volume filter for crossover signals.

2. Optimize MACD parameter combinations across different products.

3. Add stop strategies like fixed or trailing stop loss. 

4. Dynamically adjust stop loss based on market volatility.

5. Track trend strength for position sizing.

## Summary

The MACD DEMA strategy combines the strengths of both indicators, using crossovers to capture trends. But MACD is inherently lagging, beware of false signals. Also optimize stops to avoid unreasonable liquidation. For live trading, cautious entry based on optimized parameters and continuous improvements are recommended.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|MACD Fast  Line Length|
|v_input_2|26|MACD Slow Line Length|
|v_input_3|9|Signal Line Length|
|v_input_4|2018|yearfrom|
|v_input_5|2019|yearuntil|
|v_input_6|true|monthfrom|
|v_input_7|12|monthuntil|
|v_input_8|true|dayfrom|
|v_input_9|31|dayuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(" MACD DEMA STRATEGY ", overlay=true)

source=close
price=source



fastmacd = input(12,title='MACD Fast  Line Length')
slowmacd = input(26,title='MACD Slow Line Length')
signalmacd = input(9,title='Signal Line Length')

macdslowline1 = ema(close,slowmacd)
macdslowline2 = ema(macdslowline1,slowmacd)
DEMAslow = ((2 * macdslowline1) - macdslowline2 )

macdfastline1 = ema(close,fastmacd)
macdfastline2 = ema(macdfastline1,fastmacd)
DEMAfast = ((2 * macdfastline1) - macdfastline2)

MACDLine = (DEMAfast - DEMAslow)

SignalLine1 = ema(MACDLine, signalmacd)
SignalLine2 = ema(SignalLine1, signalmacd)
SignalLine = ((2 * SignalLine1) - SignalLine2 )


MACDSignal = SignalLine-MACDLine


colorbar= MACDSignal>0?green:red




yearfrom = input(2018)
yearuntil =input(2019)
monthfrom =input(1)
monthuntil =input(12)
dayfrom=input(1)
dayuntil=input(31)







if ( crossover(MACDLine,SignalLine) ) 
    strategy.entry("MMAL", strategy.long, stop=close, oca_name="TREND",  comment="AL")
    
else
    strategy.cancel(id="MMAL")


if (  crossunder(MACDLine,SignalLine) ) 

    strategy.entry("MMSAT", strategy.short,stop=close, oca_name="TREND",  comment="SAT")
else
    strategy.cancel(id="MMSAT")
    
    
    
    
    
    
    
    
    
    
    
    

```

> Detail

https://www.fmz.com/strategy/427265

> Last Modified

2023-09-19 16:10:19
