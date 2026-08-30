
> Name

Trading-Strategy-Based-on-Market-Facilitation-Index Trading-Strategy-Based-on-Market-Facilitation-Index
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy uses the Market Facilitation Index (MFI) to determine the degree of trending in the market and whether a trend reversal is likely to occur. It evaluates the efficiency of price movement by calculating the relationship between price range and trading volume, thereby generating trading signals.
## Strategy Principle
1. Calculate the market promotion index, the formula is: (highest price-lowest price)/trading volume*10000
2. Set the buy and sell thresholds. For example, when MFI is greater than 1, a buy signal is generated, and when MFI is less than 0.8, a sell signal is generated.
3. Go long when the MFI goes above the buy threshold and go short when it goes below the sell threshold.
4. Set different colors for K lines according to signals to visually display market conditions
5. Optional reversal of trading signal direction
## Advantage Analysis
1. Strong ability to evaluate market trends and price movement efficiency
2. Simple parameter setting and easy determination of thresholds
3. The trading signals are clear and easy to judge and execute.
4. Intuitive K-line coloring visually displays market conditions
5. You can choose to go long or short as needed
## Risk Analysis
1. Unable to judge the strength of the trend, and there is a risk of insufficient profits
2. Unable to distinguish between normal fluctuations and trend reversals
3. Easily affected by emergencies and produce false signals
4. There is a certain lag and you may miss the best entry point
5. Unable to establish a stop-loss mechanism and unable to control a single loss
## Optimization direction
1. Test different parameter threshold settings
2. Add volume and price related indicators for confirmation
3. Combine with indicators such as moving averages to determine the trend direction
4. Establish a stop-loss strategy to control risks
5. Set position management rules and adjust positions according to the market
6. Test the real offer effect in different varieties and cycles
## Summarize
This strategy uses the MFI indicator to determine the degree of market trend and give simple trading signals. It is necessary to further optimize parameter settings and establish a stop-loss mechanism to strictly control risks. However, the overall idea is clear and feasible, and it can be used as a component of trend following strategies and has practical value.
|| 
## Overview

This strategy uses the Market Facilitation Index (MFI) to judge the market's trending condition and possibility of trend reversal. It generates trading signals by calculating the relationship between price range and volume to evaluate the efficiency of price movement.

## Strategy Logic 

1. Calculate MFI, formula: (Highest - Lowest) / Volume * 10000

2. Set buy and sell thresholds, such as buy when MFI > 1 and sell when MFI < 0.8

3. Go long when MFI crosses above buy threshold, go short when crossing below sell threshold  

4. Color code bars based on signals for visual representation 

5. Option to reverse signal directions

## Advantage Analysis

1. Strong ability to evaluate market trending and price movement efficiency

2. Simple parameter setup, easy to determine thresholds

3. Clear trading signals, easy to interpret and execute

4. Visual bar colors intuitively display market conditions 

5. Flexibility to go long or short as needed

## Risk Analysis

1. Unable to determine trend strength, risks insufficient profit

2. Cannot differentiate normal fluctuations or real reversals

3. Prone to false signals from sudden events 

4. Has some lag, may miss best entry points

5. No stop loss mechanism, unable to control single loss

## Optimization Directions

1. Test different parameter threshold values

2. Add volume-price indicators for confirmation 

3. Incorporate moving averages to determine trend direction

4. Establish stop loss strategies for risk control

5. Define position sizing rules to adjust with markets

6. Test performance in live markets across different instruments and timeframes

## Summary

This strategy uses MFI to judge market trending conditions and provide simple trade signals. Further improvements in parameter optimization, stop losses etc. are needed for strict risk control. But the logic is clear and feasible to serve as part of a trend following strategy, thus having practical value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|6.2|SellZone|
|v_input_2|true|BuyZone|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 12/09/2018
// The Market Facilitation Index is an indicator that relates price range to 
// volume and measures the efficency of price movement. Use the indicator to 
// determine if the market is trending. If the Market Facilitation Index increased, 
// then the market is facilitating trade and is more efficient, implying that the 
// market is trending. If the Market Facilitation Index decreased, then the market 
// is becoming less efficient, which may indicate a trading range is developing that 
// may be a trend reversal.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Market Facilitation Index (MFI) Backtest", shorttitle="MFI")
SellZone = input(6.2, minval=0.01, step = 0.01)
BuyZone = input(1, minval=0.01, step = 0.01)
reverse = input(false, title="Trade reverse")
hline(BuyZone, color=green, linestyle=line)
hline(SellZone, color=red, linestyle=line)
xmyVol = volume
xmyhigh = high
xmylow = low
nRes = (xmyhigh - xmylow) / xmyVol * 10000
pos = iff(nRes > BuyZone, 1,
       iff(nRes < SellZone, -1, nz(pos[1], 0)))
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )        
plot(nRes, color=green, title="MFI", style = histogram)
```

> Detail

https://www.fmz.com/strategy/427262

> Last Modified

2023-09-19 15:56:29
