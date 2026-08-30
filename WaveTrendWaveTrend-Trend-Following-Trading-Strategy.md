
> Name

Trend following strategy based on WaveTrend indicatorWaveTrend-Trend-Following-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the WaveTrend indicator to determine the direction of the price trend and generate trading signals at trend turning points. It is a trend following strategy.
## Strategy Principle
1. Calculate the WaveTrend oscillator. When it is positive, it is judged to be a long market, and when it is negative, it is judged to be a short market.
2. The WaveTrend indicator generates buy and sell signals when it turns.
3. Option to only trade long positions.
4. Arrows can be enabled to mark WaveTrend turning points.
5. Set the background color to visually determine the trend direction.
6. The policy rules are simple, clear and easy to implement.
## Advantage Analysis
1. The WaveTrend indicator is sensitive to trend changes and can capture opportunities early.
2. Visual background color and arrow mark form an intuitive signal.
3. The default parameters are simple and practical.
4. The code is concise and easy to understand and modify.
5. You can choose to only go long or short according to your needs.
## Risk Analysis
1. The WaveTrend indicator may produce false signals resulting in unnecessary losses.
2. Unable to judge the strength of the trend, there is a risk of chasing tops and bottoms.
3. As a trend following strategy, the WaveTrend indicator is prone to arbitrage in volatile markets.
4. Improper parameter settings will also affect the strategy effect.
5. Failure to set a stop loss may result in large losses.
## Optimization direction
1. Test different combinations of WaveTrend parameters to find the optimal parameters.
2. Add other indicators to filter signals to avoid false signals.
3. Add a stop-loss strategy to control risk.
4. Evaluate the need to go long or short only.
5. You can choose whether to use arrow marks according to market conditions.
6. Optimize fund management strategies and improve income stability.
## Summarize
This strategy uses the WaveTrend indicator to determine trend changes for trading. It has the advantage of being simple and easy to use, but it also has certain risks. Through parameter optimization, stop loss strategy, signal filtering and other improvements, it can be built into a stable and efficient trend following strategy.
||


## Overview 

This strategy uses the WaveTrend indicator to determine trend direction and generate trading signals at turning points. It belongs to trend following strategies.

## Strategy Logic

1. Calculate WaveTrend oscillator, positive value indicates uptrend and negative value downtrend.

2. WaveTrend direction change produces buy and sell signals. 

3. Option to only trade long side.

4. Enable arrows to mark WaveTrend turning points.

5. Background color for intuitive trend visualization.

6. Simple and clear strategy rules easy to implement.

## Advantages

1. WaveTrend sensitive in catching trend turns early.

2. Visualized arrows and background color make intuitive signals.

3. Simple and practical default parameters. 

4. Concise code easy to understand and modify.

5. Flexibility to only trade long or short.

## Risks

1. WaveTrend may generate false signals causing unnecessary losses.

2. Unable to determine trend strength, risks of chasing.

3. Prone to whipsaws in ranging markets.

4. Improper parameters negatively affect performance.

5. No stop loss may lead to large losses.

## Enhancement

1. Test parameter combinations to find optimum.

2. Add filters with other indicators to avoid false signals.

3. Incorporate stop loss strategy for risk control.

4. Evaluate necessity of only long or short.

5. Toggle arrows based on market conditions. 

6. Optimize money management for more stable returns.

## Conclusion

This strategy trades WaveTrend direction changes simply and viably, but has some risks. Improvements like parameter optimization, stops, filters can make it a stable and efficient trend following system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Only Long?|
|v_input_2|true|Need new-trend-arrows?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-12 00:00:00
end: 2023-09-19 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// (c) Noro
//2017

//@version=2

strategy(title="Noro's WaveTrend Strategy v1.0", shorttitle = "WaveTrend str 1.0", overlay = true)

//settings
onlylong = input(true, title = "Only Long?")
usearr = input(true, title = "Need new-trend-arrows?")

//WTO ("WaveTrend Oscilator") method by LazyBear
//Start of LazyBear's code
esa = ema(hlc3, 10)
d = ema(abs(hlc3 - esa), 10)
ci = (hlc3 - esa) / (0.015 * d)
tci = ema(ci, 21)
//End of LazyBear's code

WTOtrend = tci > 0 ? 1 : tci < 0 ? -1 : 0

//background
col = WTOtrend == 1 ? 1 : WTOtrend == -1 ? -1 : col[1]
bgcolor = col == 1 ? lime : col == -1 ? red : na
bgcolor(bgcolor, transp=70)

//arrows
posi = WTOtrend == 1 ? 1 : WTOtrend == -1 ? -1 : posi[1]
arr = usearr == true ? posi == 1 and posi[1] < 1 ? 1 : posi == -1 and posi[1] > -1 ? -1 : na : na
plotarrow(arr == 1 ? 1 : na, title = "UpArrow", colorup = blue, colordown = blue, maxheight = 60, minheight = 50, transp = 0)
plotarrow(arr == -1 ? -1 : na, title = "DnArrow", colorup = blue, colordown = blue, maxheight = 60, minheight = 50, transp = 0)

//trading
longCondition = posi == 1 and posi[1] < 1
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = posi == -1 and posi[1] > -1
if (shortCondition)
    strategy.entry("Short", strategy.short, onlylong == true ? 0 : na)
```

> Detail

https://www.fmz.com/strategy/427387

> Last Modified

2023-09-20 15:50:08
