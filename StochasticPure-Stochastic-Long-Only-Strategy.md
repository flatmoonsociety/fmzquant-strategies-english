
> Name

Pure-Stochastic Long-Only-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy only gives entry and exit signals based on the Stochastic indicator, and is a typical Stochastic indicator strategy that only does long but not short. It is a long entry when the K line crosses the D line in the oversold zone and the closing price exceeds the previous day's highest price. It is simple and easy to close the position when the take-profit or stop-loss conditions are triggered.
## Strategy Principle
The main logic of this strategy is:
1. Calculate the Stochastic K value and D value
2. When the K line crosses the D line above the oversold zone and the closing price breaks through the previous day's highest price, enter the market long.
3. Set the trailing stop when the closing price crosses the fast EMA
4. When the K line crosses the D line or the K line enters the overbought zone, close the position and take profit.
When the Stochastic K value breaks through the D value in the oversold zone, it means that the price may reverse and rise. Combined with the closing price breaking through the previous day's highest price, the entry signal can be effectively confirmed.
EMA trailing stop can lock in profits. When a sell signal appears on the K-line in the overbought zone, the position will be closed before taking profit.
This strategy is only long-term and is suitable for unilateral market types such as the stock market. The operation is simple and easy to implement.
## Advantage Analysis
- Use the Stochastic indicator to identify oversold areas
- The combination of K line and D line can avoid false signals
- Closing price breakout increases entry certainty
- Combining stop-loss and take-profit strategies to control risks
- Simple logic and easy-to-implement take-profit strategy
## Risks and Responses
- Stochastic may have error signals
- There is a certain risk of loss
- Cannot take profit at the top of the trend
Countermeasures:
1. Optimize Stochastic parameters and improve accuracy
2. Use trailing stop loss to control risk
3. Combine with other indicators to predict trend reversal
## Strategy optimization direction
This strategy can be expanded from the following aspects:
1. Increase short-selling opportunities and make the strategy applicable to the whole market
2. Adjust stop loss width based on volatility
3. Use machine learning to optimize parameters
4. Integrate mobile take-profit strategies and dynamically track take-profit points
5. Combine other strategies to establish a multi-factor system
## Summarize
This strategy is a pure Stochastic long strategy that uses indicators to identify oversold areas for entry, stop loss and take profit combined with risk control. This strategy is simple and practical, suitable for unilateral market types such as the stock market. By expanding short-selling opportunities, parameter optimization and other dimensions, the strategy can be optimized into a more comprehensive and reliable system.
|| 

## Overview

This is a pure Stochastic strategy that uses the indicator for entry and exit signals, going long only. It enters long when K line crosses above D line in oversold zone with close above previous high, and exits on profit taking or stop loss triggers. Simple and easy to implement.

## Strategy Logic

The main logic is:  

1. Calculate Stochastic K and D values
2. Enter long when K crosses above D in oversold zone and close breaks previous high
3. Set moving stop loss below fast EMA on close 
4. Take profit when K crosses below D or K enters overbought zone

K crossing D in oversold suggests potential upside reversal. Close breaking high adds confidence. 

EMA stop locks in profits. K crossing D in overbought acts as profit take signal.

Going long only, it suits instruments like equities with one-sided trends. Simple to implement.

## Advantages

- Uses Stochastic to identify oversold regions
- K and D lines avoid false signals
- Close breakout adds confidence  
- Stop loss and take profit manages risks
- Simple logic makes it easy to implement 

## Risks and Mitigation

- Potential for Stochastic false signals
- Has some loss risks
- Unable to take profit at trend tops

Mitigations:

1. Optimize parameters for greater accuracy
2. Use moving stops to control loss risks
3. Add indicators to predict trend reversal

## Enhancement Opportunities

The strategy can be enhanced by:

1. Adding short side opportunities for full market coverage
2. Adaptive stops based on volatility
3. Machine learning for parameter optimization
4. Incorporate trailing take profit strategy  
5. Portfolio combinations to build multifactor system

## Conclusion

This is a pure Stochastic long strategy using the indicator for oversold entries and managed exits. Simple and practical, it fits instruments like equities well. Expanding to the short side, parameter optimization can make it a more robust system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|length|
|v_input_2|80|OverBought|
|v_input_3|20|OverSold|
|v_input_4|7|smoothK|
|v_input_5|4|smoothD|
|v_input_6|5|emaperiodf|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-12 14:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version= 4
// see for original idea:  http://www.enricomalverti.com/2016/12/stocastico/
// https://sauciusfinance.altervista.org
strategy(title="Pure Stochastic long only", overlay = false, max_bars_back=500)

// INPUTS & calculations
length = input(10, minval=1)
OverBought = input(80, minval = 50, step = 10)
OverSold = input(20, minval = 10, step = 5)
smoothK = input(7, minval=1)
smoothD = input(4, minval=1)
k = sma(stoch(close, high, low, length), smoothK)
d = sma(k, smoothD)
// We keep EMA 7 (n period of stochastic /2) as target price
emaperiodf = input(5, minval = 1)
emaf = ema(close,emaperiodf)
entryl = k > d and k <= OverSold and close >= high[1]
/// Entry
strategy.entry("Long", true, when = entryl)

middle = (OverBought+OverSold)/2
close1= crossunder(close,emaf)// **close under EMA fast**
close2= k < d and k > middle
close3 = (k >= OverBought)
// exits.
strategy.close("Long", when = close1, comment="stop Ema Fast")
strategy.close("Long", when = close2, comment ="cross k&d")
strategy.close("Long", when = close3, comment = "high value of K")


plot(k, color=#0000FF,  linewidth= 2, title="k Stoch")
plot(d, color=#787B86, linewidth= 1, title="d stoch signal")
plot(OverBought)
plot(OverSold)
```

> Detail

https://www.fmz.com/strategy/427302

> Last Modified

2023-09-19 21:22:11
