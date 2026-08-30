
> Name

Triple-High-Price-Volume-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy predicts whether there will be a gap breakthrough opportunity the next day by judging whether price and trading volume form a triple higher high in the late trading period. It is a typical high-frequency trading strategy.
Strategy principle:
1. Calculate the relationship between the high points of three consecutive K lines of price and determine whether there are triple higher high points.
2. Calculate the relationship between three consecutive K-lines of trading volume and determine whether the trading volume has expanded.
3. Determine whether the closing prices all close the Yang line, showing strong characteristics.
4. During the critical period of late trading, if the Above condition is met, it is predicted that a gap breakthrough may occur the next day.
5. Carry out high-leverage operations and seek to cash out and take profits during the opening period after the gap.
Advantages of this strategy:
1. Triple high point price and volume judgments can improve the accuracy of forecasts.
2. Operations during key periods can enlarge profit potential.
3. The profit-taking time is fixed, eliminating decision-making difficulties.
Risks of this strategy:
1. The prediction is only based on simple K-line patterns and is easily trapped by reversals.
2. High-leverage operations are extremely risky, and fund management is particularly critical.
3. There is no way to limit the size of the loss, and there is a possibility of a huge retracement.
In short, this strategy attempts to predict the next day's market through the late trading pattern, and on the premise of clarifying the risk of retracement, can obtain a certain probability of high-leverage profit opportunities. But investors still need to be very cautious.
||

This strategy judges if price and volume make triple higher highs near market close to predict next day gap opportunities. It aims to capitalize on short-term patterns.

Strategy Logic:

1. Check if latest 3 bars make triple higher highs in price.

2. Check if latest 3 bars show increasing volume. 

3. Check if latest 3 bars all closed higher than open. 

4. If above conditions met near market close, predict possible gap next day.

5. Take highly leveraged positions to profit from gap open.

Advantages:

1. Triple high price/volume improves accuracy. 

2. Trading in critical periods maximizes profit potential.

3. Fixed profit-taking avoids decision difficulties.

Risks:

1. Prediction relies simply on candle patterns, prone to reversals and traps.

2. Extremely high leverage entails huge risk, requiring prudent management. 

3. Unable to limit loss size, potentially large drawdowns.

In summary, this strategy attempts to predict next day moves based on end-of-day patterns, providing high probability leveraged profit opportunities balanced with clear loss risks. But extreme caution remains essential.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-13 00:00:00
end: 2023-09-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SharemarketRaja

//@version=4

//Scanner available 

strategy("3 Higher High Price & Vol", overlay=true)

volma = sma(volume, 20)

PriceHH = high > high[1] and high[1] > high[2] 
VolHH = volume > volume[1] and volume[1] > volume[2]
Volma =  volume > volma and volume[1] > volma[1] and volume[2] > volma[2]
Allgreen = close > open and close[1] > open[1] and close[2] > open[2]

PriceLL = low < low[1] and low[1] < low[2]
Allred = close < open and close[1] < open[1] and close[2] < open[2]

Qty = 100
Buy = (PriceHH == true and VolHH == true and Volma == true and Allgreen == true) and time("15", "1515-1530")
Reversal = (PriceLL == true and VolHH == true and Volma == true and Allred == true) and time("15", "1515-1530")


plotshape(Buy, style=shape.arrowup, size=size.large, color=color.green, location=location.belowbar)
plotshape(Reversal, style=shape.arrowup, size=size.large, color=color.red, location=location.belowbar)

strategy.entry(id="L", long=true, when=Buy)
strategy.entry(id="R", long=true, when=Reversal)
// strategy.exit(id="LE", from_entry="L", profit=Profit, loss=Loss)

// strategy.close_all(when=(time("15", "1500-1515")) )
```

> Detail

https://www.fmz.com/strategy/426572

> Last Modified

2023-09-13 14:17:22
