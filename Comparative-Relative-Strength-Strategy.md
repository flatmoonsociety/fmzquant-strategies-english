
> Name

Comparative-Relative-Strength-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]  

## Strategy Principle
The Comparative Relative Strength strategy generates trading signals by calculating the relative strength of two markets. When the compared market shows strength against the benchmark market, it can be regarded as a buy signal; when it shows weakness, it is a sell signal.
The specific transaction logic is:
1. Select the market to be compared, such as a specific stock
2. Choose a benchmark market, such as the S&P 500 Index
3. Calculate the strength ratio of the compared market relative to the benchmark market
4. When the ratio is greater than the overbought line, go long the market being compared
5. When the ratio is less than the oversold area, short the compared market
6. Set a callback line and close the position when the price falls.
By calculating the relative strength of two markets, this strategy can identify undervalued opportunities and avoid overvalued situations.
## Strategic Advantages
- Compare relative strengths and weaknesses and identify undervalued opportunities
- Set a callback line to avoid continuing to follow the rise and kill the fall
- Simple and clear operating rules
## Strategy Risk
- Need to choose a suitable benchmark market for comparison
- Overbought and oversold areas require optimized judgment
- Only long or short positions cannot capture the full market opportunities
## Summarize
The Comparative Relative Strength strategy finds arbitrage opportunities by comparing the strength of two markets. However, its parameter settings and stop-loss strategies need to be carefully evaluated.

||

## Strategy Logic 

The comparative relative strength strategy generates trades by comparing the relative strength of two markets. Outperformance of the comparison market versus the benchmark is seen as a buy signal, underperformance as a sell signal.

The logic is:

1. Select comparison market, e.g. a stock

2. Select benchmark market, e.g. S&P 500 index 

3. Compute ratio of comparison market vs benchmark 

4. Go long the comparison when ratio exceeds overbought level

5. Go short when ratio falls below oversold zone

6. Set pullback line to close positions when price falls back

By comparing relative strength, the strategy aims to uncover undervalued opportunities and avoid overvalued conditions.

## Advantages

- Compares relative strength to find undervaluation 

- Pullback line avoids chasing trends

- Simple and clear rules

## Risks

- Appropriate benchmark needs selection

- Overbought/oversold zones require optimization

- LONG/SHORT only misses full opportunities

## Summary

The relative strength strategy identifies arbitrage chances by comparing two markets. But parameter tuning and stop strategies require prudent assessment.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|BTC_USDT:swap|b|
|v_input_2|10|len|
|v_input_3|0.9988|BuyBand|
|v_input_4|0.996|SellBand|
|v_input_5|0.9975|CloseBand|
|v_input_6|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-07 00:00:00
end: 2023-09-13 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 10/03/2017
// Comparative Relative Strength Strategy for ES
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy("Comparative Relative Strength Strategy", shorttitle="CRS")
a = syminfo.tickerid 
b = input("BTC_USDT:swap") 
len = input(10) 
BuyBand = input(0.9988, step = 0.0001)
SellBand = input(0.9960, step = 0.0001)
CloseBand = input(0.9975, step = 0.0001)
reverse = input(false, title="Trade reverse")
hline(CloseBand, color=blue, linestyle=hline.style_dashed)
hline(SellBand, color=red, linestyle=hline.style_solid)
hline(BuyBand, color=green, linestyle=hline.style_solid)
as = security(a, timeframe.period, close) 
bs = security(b, timeframe.period, close) 
nRes = sma(as/bs, len)
pos = iff(nRes > BuyBand, 1,
	     iff(nRes < SellBand, -1,
	      iff(pos[1] == 1 and nRes < CloseBand, 0,
	       iff(pos[1] == -1 and nRes > CloseBand, 0, nz(pos[1], 0)))))
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	 
if (possig == 0)
    strategy.close("Long", when = possig == 0)	 
    strategy.close("Short", when = possig == 0)	 
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(as/bs, title="CRS", color=gray) 
plot(nRes, color=navy)
```

> Detail

https://www.fmz.com/strategy/426832

> Last Modified

2023-09-14 17:58:19
