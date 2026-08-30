
> Name

MACD-Trend-Following-Strategy MACD-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f6d05cd9dcb100633345dc48c93df3792d683d7038bbe6c272bd283f7a3db090.png)
[trans]

## Overview
The name of this strategy is MACD trend following strategy. It is a quantitative strategy that uses the MACD indicator to determine the price trend and follow the trend for trading. This strategy aims to capture mid- to long-term trends and adjust positions in a timely manner when the trend turns.
## Strategy Principle
This strategy uses the MACD indicator to determine price trends. The MACD indicator is a breakthrough indicator, consisting of the fast EMA (12th) and the slow EMA (26th). Their difference constitutes the MACD columnar line, and the 9-day EMA of the columnar line constitutes the signal line of MACD. When the MACD line crosses the signal line, it is a golden cross, indicating that the price is in an upward trend; when the MACD line crosses below the signal line, it is a dead cross, indicating that the price is in a downward trend.
This strategy first calculates the MACD line and signal line, and then calculates the difference delta between the MACD line and the signal line. When delta crosses above 0, a buy signal is generated, when delta crosses below 0, a sell signal is generated, and positions are adjusted based on these two signals. In order to filter out the noise, the strategy also introduces an EMA moving average, which will only generate a real trading signal when the price breaks through this moving average.
Specifically, the strategy logic is as follows:
1. Calculate MACD line, signal line and difference delta
2. Determine when delta crosses above or below 0 to confirm the trend turning point
3. Calculate EMA moving average as a filter
4. When delta crosses 0 and the price is above EMA, a buy signal is generated
5. When delta crosses 0 and the price is below EMA, a sell signal is generated
Through such a design, this strategy can trade in line with the medium and long-term trends, adjust positions in a timely manner when the trend changes, and avoid being misled by short-term market noise.
## Strategic Advantages
This strategy has the following advantages:
1. Use MACD to determine trend turning points and accurately determine buying and selling opportunities.
2. Use EMA filter to avoid being disturbed by short-term market noise
3. Only follow the medium and long-term trends to avoid being trapped by the volatile market.
4. The transaction logic is simple and clear, and the code is easy to understand and modify.
5. The trading frequency of the strategy can be freely controlled through parameter adjustment
6. High capital utilization rate, able to fully track medium and long-term trends
## Strategy Risk
There are also some risks to be aware of with this strategy:
1. As a trend following indicator, MACD is prone to produce false signals in volatile markets.
2. The EMA filter may filter out some valid trading opportunities
3. Improper parameter settings may lead to too high or too low transaction frequency
4. Unable to respond to short-term market changes and insensitive to emergencies
5. There is a certain lag, and the best time for a trend turning point may be missed.
Countermeasures:
1. Optimize parameters and adjust EMA filter parameters to reduce misjudgments
2. Combine with other indicators as an aid to discover more trading opportunities
3. Set stop loss to control single loss
4. Appropriately shorten the position holding time to ensure the flexibility of the strategy
## Strategy optimization
This strategy can also be optimized from the following aspects:
1. Add other indicators to judge, form a combination of indicators, and improve accuracy
2. Add a stop-profit and stop-loss mechanism to better control risks
3. Combine with trading volume indicators to avoid false breakthroughs
4. Adaptively adjust parameters according to the market environment to improve the adaptability of the strategy
5. Optimize the specific logic of buying and selling, and improve the timing of entry and exit.
6. Build positions in stages to better track trends and reduce risks
Through the optimization of indicator combinations, stop-loss and take-profit, adaptive parameters and other methods, the effect of this strategy can be greatly improved.
## Summarize
Generally speaking, this MACD trend following strategy uses a simple and effective MACD indicator to determine the mid- and long-term trends, and designs a clearer trend following trading logic. It has the ability to capture trends and certain risk control measures. With further optimization and improvement, this strategy can become a very practical quantitative trading system. It is suitable for investors who pursue long-term stable returns rather than short-term profits.
||
## Overview 

This strategy is named the MACD Trend Following Strategy. It is a quantitative strategy that utilizes the MACD indicator to determine price trends and follows the trends to trade. The strategy aims to capture mid-to-long-term trends and adjust positions in a timely manner when trend reversals occur.

## Strategy Logic

The strategy uses the MACD indicator to determine price trends. The MACD is a breakout indicator formed by the fast EMA line (12-day) and the slow EMA line (26-day). The difference between these two lines forms the MACD histogram, and the 9-day EMA of the histogram is the MACD signal line. When the MACD line crosses above the signal line, it is a golden cross, indicating an upward trend. When the MACD line crosses below the signal line, it is a dead cross, indicating a downward trend.

The strategy first calculates the MACD line and signal line, then computes the difference delta between the two lines. When delta crosses above 0, a buy signal is generated. When delta crosses below 0, a sell signal is generated. Based on these two signals, the strategy adjusts positions accordingly. To filter out noise, the strategy also introduces an EMA line - valid trade signals are only generated when the price breaks through this EMA line. 

Specifically, the strategy logic is:

1. Calculate the MACD line, signal line and the difference delta
2. Determine if delta crossing above or below 0 signifies a trend reversal  
3. Compute an EMA line to serve as a filter
4. When delta crosses above 0 and price is above EMA, generate buy signal
5. When delta crosses below 0 and price is below EMA, generate sell signal

With this design, the strategy is able to follow mid-to-long-term trends and quickly adjust positions when trends reverse. It avoids being misled by short-term market noises.

## Advantages

The strategy has the following advantages:

1. Use MACD to accurately detect trend reversal points for entry and exit timing
2. Adopt EMA filter to avoid interference from short-term market noises  
3. Only follow mid-to-long-term trends, avoiding whipsaws in ranging markets
4. Simple and clear logic, easy to understand and modify the code
5. Flexibility in controlling trading frequency by adjusting parameters
6. High capital utilization to fully track mid-to-long-term trends

## Risks

There are some risks to be mindful of:

1. MACD as a trend following indicator can generate false signals in choppy markets
2. EMA filter may filter out some valid trading opportunities
3. Improper parameter settings may lead to over- or under-trading
4. Unable to respond to short-term market changes due to lagging nature
5. May miss optimal timing at trend turning points due to lag

Solutions:

1. Optimize parameters and adjust EMA filter to reduce false signals
2. Incorporate other indicators for confirmation to uncover more trades 
3. Implement stop loss to control loss on single trades
4. Shorten holding period to improve flexibility  

## Optimization

The strategy can be further optimized in the following ways:

1. Add other indicators to form a combined system for higher accuracy
2. Introduce profit taking and stop loss mechanisms for better risk control
3. Incorporate volume indicators to avoid false breakouts 
4. Adapt parameters dynamically based on market conditions to improve robustness
5. Refine entry and exit logic to improve timing
6. Scale in positions to better follow trends and reduce risk

Significant improvement can be achieved through methods like indicator combos, adaptive parameters, stop loss/profit taking etc.

## Conclusion

In summary, the MACD Trend Following Strategy utilizes the simple and effective MACD indicator to identify mid-to-long-term trends, and implements a clear trend following logic. It has the capacity to capture trends as well as reasonable risk control measures. With further optimizations, the strategy can become a very practical quant trading system. It suits investors seeking steady long-term gains over short-term profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|false|Short|
|v_input_3|false|Use EMA filter|
|v_input_4|5|EMA filter period|
|v_input_5|12|fastLength|
|v_input_6|26|slowlength|
|v_input_7|9|MACDLength|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-14 00:00:00
end: 2023-10-27 05:20:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title = "Noro's MACD Strategy v1.0", shorttitle = "MACD str 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value=100.0, pyramiding=0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(false, defval = false, title = "Short")
usefil = input(false, defval = false, title = "Use EMA filter")
lenfil = input(5, defval = 5, minval = 1, maxval = 50, title = "EMA filter period")

fastLength = input(12)
slowlength = input(26)
MACDLength = input(9)

MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD

//Signals
ema = ema(close, lenfil)
trend = crossover(delta, 0) == true ? 1 : crossunder(delta, 0) == true ? -1 : trend[1]
up = trend == 1 and (low < ema or usefil == false) ? 1 : 0
dn = trend == -1 and (high > ema or usefil == false) ? 1 : 0

plot(ema, color = black, transp = 0)

if (up == 1)
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na)

if (dn == 1)
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na)

```

> Detail

https://www.fmz.com/strategy/432230

> Last Modified

2023-11-15 17:08:15
