
> Name

Moving-Average-Percentage-Reversal-Strategy Moving-Average-Percentage-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
The Moving Average Percent Reversal Strategy determines when to buy or sell by calculating the percentage difference between price and the moving average. A trading signal is generated when the price deviates from the moving average by a certain percentage.
Specifically, the trading logic of the strategy is:
1. Calculate the difference between the price and the moving average of length N
2. Convert the difference into percentage form, that is, divide the difference by the price
3. When the percentage difference is greater than the preset upper limit (such as 5%), go short
4. When the percentage difference is less than the preset lower limit (such as -3%), go long
5. You can choose the reversal signal, that is, long is reversed into short, and short is reversed into long.
If N is 14, the upper limit is set to 5%, and the lower limit is set to -3%, then:
- Go short when the price is 5% above the 14-day moving average
- Go long when the price is 3% below the 14-day moving average
By adjusting N, upper and lower limit parameters, the sensitivity of the strategy can be controlled.
## Strategic Advantages
- Use percentage form to avoid being affected by the absolute value of the price
- Parameters can be adjusted according to the market and suitable for different cycles
- Use the BREAK strategy to catch trend turning points earlier
## Strategy Risk
- Percent difference cannot determine trend direction
- It is easy to send out wrong signals and needs to be filtered
- The moving average lags behind and cannot catch the turning point in time
## Summarize
The moving average percentage strategy determines the buying and selling point by calculating the percentage difference between the price and the moving average, and uses the BREAK strategy to capture the turning point of the trend. It can adapt to different market environments by adjusting parameters. However, there is also a certain risk of hysteresis and false positives, and optimization and filtering are required.
||

## Strategy Logic 

The moving average percentage reversal strategy generates trading signals by calculating the percentage differential between price and a moving average. 

Trades are taken when the percentage gap between price and the MA reaches preset levels.

Specifically, the logic is:

1. Calculate the absolute difference between price and an N-period MA
2. Convert the difference to percentage terms, i.e. divide by price
3. Go short when the percentage gap exceeds an upper threshold (e.g. 5%) 
4. Go long when the percentage gap falls below a lower threshold (e.g. -3%)
5. Optionally reverse signals (longs become shorts, shorts become longs)

E.g. with N=14, upper limit=5%, lower limit=-3%:

- Go short when price is >5% above the 14-day MA
- Go long when price is <3% below the 14-day MA

Parameters N, upper/lower limits can adjust sensitivity.

## Advantages

- Percentage gaps account for changing price levels  
- Adjustable parameters suit different cycles
- BREAK strategy aims to catch trend turning points early

## Risks

- Percentage gaps alone cannot confirm trend direction
- Prone to false signals, needs additional filters
- MAs lagging, may not catch reversals promptly

## Summary

The MA percentage strategy uses the percentage gap between price and MA to identify potential turning points, with a BREAK approach. Adjustable parameters can adapt to varying market conditions, but lag and whipsaws are risks needing mitigation.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|0.54|SellZone|
|v_input_3|0.03|BuyZone|
|v_input_4|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 30/07/2018
// Percent difference between price and MA
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Percent difference between price and MA Backtest")
Length = input(14, minval=1)
SellZone = input(0.54, minval=0.01, step = 0.01)
BuyZone = input(0.03, minval=0.01, step = 0.01)
reverse = input(false, title="Trade reverse")
hline(BuyZone, color=green, linestyle=line)
hline(SellZone, color=red, linestyle=line)
xSMA = sma(close, Length)
nRes = abs(close - xSMA) * 100 / close
pos = iff(nRes < BuyZone, 1,
       iff(nRes > SellZone, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="PD MA")
```

> Detail

https://www.fmz.com/strategy/426774

> Last Modified

2023-09-14 14:53:53
