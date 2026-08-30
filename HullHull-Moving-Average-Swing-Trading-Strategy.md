
> Name

Hull Moving Average Oscillation Trading Strategy Hull-Moving-Average-Swing-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a short-term trading strategy based on the Hull Moving Average indicator. The strategy uses the golden cross of the Hull moving average to form a buying and selling signal, which is a trend following strategy.
## Strategy Principle
This strategy is mainly based on the Hull Moving Average indicator, which consists of two moving averages. First, calculate the medium-term moving average nma of the price, with the period HullPeriod. Then calculate the price's fast moving average n2ma, with a period half of nma. When n2ma crosses nma above, a buy signal is issued, and when n2ma crosses below nma, a sell signal is issued.
In order to filter out some false signals, the strategy also introduces the Hull line (Hull_Line). The Hull line is the linear regression result of calculating the difference between nma and n2ma. When the price diverges from the Hull line, the strategy will skip buy and sell signals.
Specifically, the policy rules are as follows:
1. Calculate nma, period hullperiod
2. Calculate n2ma, the period is half of the period of nma
3. Calculate the difference diff between n2ma and nma
4. Perform a moving average with a period of sqrt (hullperiod) on the diff to obtain the Hull line Hull_Line
5. Send a buy signal when price crosses the Hull line
6. Send a sell signal when the price breaks below the Hull line
7. If the price diverges from the Hull line, skip the signal
8. Enter the market with a certain proportion of the position and use the exit stop loss method to stop the loss.
## Advantage Analysis
This strategy has the following advantages:
1. Based on Hull moving average, it can quickly capture the trend and follow the trend.
2. Use Hull line to filter false signals and improve signal quality
3. Good retracement and profit-loss ratio, suitable for short-term operations
4. Flexible parameter adjustment to adapt to different market environments
5. Using reversal stop loss can stop losses in time and control risks.
6. Combined with seasonality, systemic risks in a specific period of time can be avoided
## Risk Analysis
There are also some risks with this strategy:
1. Trend-following strategies cannot achieve round-the-clock trading
2. When the trend reverses, large losses will occur
3. The moving average system lags behind and cannot capture turning points in time.
4. Short-term transactions are frequent and transaction fees are high
5. Improper parameter settings may lead to reduced returns in volatile markets.
In response to the above risks, the following measures can be taken to control them:
1. Adopt Martingale stop loss strategy to control single loss
2. Optimize parameters and test the robustness of parameters in different market environments
3. Combine trend judgment indicators to avoid chasing ups and downs during reversals.
4. Increase the holding time and reduce the frequency of transactions
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Combined with the momentum indicator, determine the starting point of the trend and better plan the entry.
2. Add machine learning models to assist in judging the direction and intensity of trends.
3. Use adaptive parameter settings to adjust parameters according to the real-time market
4. Configure a multi-time period Hull system and configure different positions in different periods.
5. Combine trading volume energy indicators to avoid false breakthroughs with insufficient volume energy.
6. Add a volatility-based position management module to dynamically adjust positions based on volatility.
## Summarize
The Hull moving average oscillation trading strategy is overall a very practical short-term tracking strategy. It uses the Hull moving average system to determine the trend direction to achieve the purpose of following the trend. It has higher signal quality and Parameters flexibility than a single moving average system. The advantage of this strategy is that it can quickly capture the trend reversal and make profits with a lower retracement; the disadvantage is that it cannot cope with the trend reversal. We can control risks through parameter optimization, stop loss strategy improvement, and adding auxiliary models to make the strategy run stably in more market environments.
||

## Overview

This strategy is a short-term trading strategy based on the Hull Moving Average indicator. The strategy uses the golden cross and dead cross of the Hull Moving Average lines to generate trading signals, belonging to a trend-following strategy.

## Strategy Logic

This strategy is mainly based on the Hull Moving Average indicator. The Hull Moving Average line consists of two moving averages. First it calculates the median moving average line nma of the price, with a period of hullperiod. Then it calculates the fast moving average line n2ma, with a period of half of the nma's. When n2ma crosses above nma, a buy signal is generated. When n2ma crosses below nma, a sell signal is generated.

To filter out some false signals, the strategy also introduces the Hull Line (Hull_Line). The Hull Line is a linear regression result of the difference between nma and n2ma. When there is divergence between the price and the Hull Line, the strategy will skip the trading signal. 

Specifically, the strategy rules are as follows:

1. Calculate the nma, with period hullperiod

2. Calculate the n2ma, with period half of the nma period 

3. Calculate the difference diff between n2ma and nma

4. Moving average the diff with period sqrt(hullperiod), get and get the Hull Line Hull_Line
5. When price crosses above Hull Line, a buy signal is generated

6. When price crosses below Hull Line, a sell signal is generated

7. If there is divergence between price and Hull Line, skip the signal

8. Enter with a certain percentage of the position, adopt exit stop loss

## Advantage Analysis

The advantages of this strategy include:

1. Based on Hull Moving Average, it can quickly capture the trend and follow the trend

2. Use Hull Line to filter false signals and improve signal quality

3. Good risk-reward ratio and drawdown, suitable for short-term trading

4. Flexible parameter tuning, adaptable to different market environments

5. Adopt reversal stop loss, can stop loss in time and control risks

6. Combine seasonality to avoid systemic risks in specific time periods

## Risk Analysis

This strategy also has some risks:

1. Trend following strategy, cannot trade all day long

2. Larger losses when trend reverses 

3. Lagging of moving averages, cannot timely capture turning points

4. High trading frequency leads to higher trading costs

5. Inappropriate parameter settings may lead to lower profitability in range-bound markets

To control these risks, we can take the following measures:

1. Adopt martingale stop loss strategy to control single loss

2. Optimize parameters and test robustness in different market environments 

3. Combine trend judging indicators to avoid chasing trends during reversals

4. Increase holding time to lower trading frequency

## Optimization Directions

This strategy can also be optimized in the following aspects:

1. Combine momentum indicators to locate the starting point of trends for better entry

2. Add machine learning models to assist in judging trend direction and strength

3. Adopt adaptive parameter setting to adjust parameters based on real-time market dynamics

4. Configure multi-timeframe Hull systems, with different position sizes for different timeframes

5. Combine volume indicators to avoid false breakouts with insufficient momentum

6. Add volatility-based position sizing model to dynamically adjust position sizes based on volatility

## Summary

The Hull Moving Average Swing Trading Strategy is an efficient short-term trend following strategy overall. It uses the Hull Moving Average system to determine the trend direction for the purpose of following the trend. Compared with single moving average systems, it has higher signal quality and Parameters flexibility. The advantage of this strategy lies in quickly capturing trend changes with relatively small drawdowns. The weakness is the inability to cope with trend reversals. We can use Parameter optimization, stop loss strategies, adding auxiliary models etc. to control risks and make the strategy robust in more market environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|210|HullMA Period|
|v_input_2_open|0|Price data: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|true|From Month|
|v_input_4|true|From Day|
|v_input_5|2020|From Year|
|v_input_6|true|To Month|
|v_input_7|true|To Day|
|v_input_8|9999|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-06 00:00:00
end: 2023-10-06 00:00:00
period: 6h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//                               Hull Moving Average Swing Trader by SEASIDE420
strategy("Hull Moving Average Swing Trader", shorttitle="HMA_Swing_Trader", default_qty_type=strategy.percent_of_equity, default_qty_value=100, calc_on_order_fills=true, calc_on_every_tick=true, pyramiding=0)
hullperiod = input(title="HullMA Period", type=input.integer, defval=210, minval=1)
price = input(open, type=input.source, title="Price data")
FromMonth = input(defval=1, title="From Month", minval=1, maxval=12)
FromDay = input(defval=1, title="From Day", minval=1, maxval=31)
FromYear = input(defval=2020, title="From Year", minval=2017)
ToMonth = input(defval=1, title="To Month", minval=1, maxval=12)
ToDay = input(defval=1, title="To Day", minval=1, maxval=31)
ToYear = input(defval=9999, title="To Year", minval=2017)
start = timestamp(FromYear, FromMonth, FromDay, 00, 00)
finish = timestamp(ToYear, ToMonth, ToDay, 23, 59)
window() => true
n2ma = 2 * wma(price, round(hullperiod / 2))
nma = wma(price, hullperiod)
diff = n2ma - nma
sqn = round(sqrt(hullperiod))
n2ma1 = 2 * wma(price[1], round(hullperiod / 2))
nma1 = wma(price[1], hullperiod)
diff1 = n2ma1 - nma1
n1 = wma(diff, sqn)
n2 = wma(diff1, sqn)
Hull_Line = n1 / n1 * n2
Hull_retracted = if n1 > n2
    Hull_retracted = Hull_Line - 2
else
    Hull_retracted = Hull_Line + 2
c1 = Hull_retracted + n1 - price
c2 = Hull_retracted - n2 + price
c4 = n1 > n2 ? color.green : color.red
c2p = plot(c2, color=color.black, linewidth=1)
c3p = plot(price, color=color.black, linewidth=1)
fill(c3p, c2p, color=c4, transp=75)
//plot(cross(c1, c2) ? c1 : na, style=plot.style_circles, color=c4, linewidth=4)
if price < c2
    strategy.close("BUY", when=window())
if price > c2
    strategy.close("SELL", when=window())
if price > c2 and price[1] > c1
    strategy.entry("BUY", strategy.long, when=window())
if price < c1 and price[1] < c2
    strategy.entry("SELL", strategy.short, when=window())  //        /L'-, 
//                               ,'-.      `   ````                 /  L '-, 
//     .                    _,--dMMMM\        `   ` ` '`..         /       '-, 
//     :             _,--,  )MMMMMMMMM),.      `     ,<>          /_      '-,' 
//     ;     ___,--. \MM(    `-'   )M//MM\          ,',.;      .-'* ;     .' 
//     |     \MMMMMM) \MM\       ,dM//MMM/     ___ < ,; `.      )`--'    / 
//     |      \MM()M   MMM)__   /MM(/MP'  ___, \  \ `  `. `.   /__,    ,' 
//     |       MMMM/   MMMMMM( /MMMMP'__, \     | /      `. `-,_\     / 
//     |       MM     /MMM---' `--'_ \     |-'  |/         `./ .\----.___ 
//     |      /MM'   `--' __,-  \""   |-'  |_,               `.__) . .F. )-. 
//     |     `--'       \   \    |-'  |_,     _,-/            J . . . J-'-. `-., 
//     |         __  \`. |   |   |         \    / _           |. . . . \   `-.  F 
//     |   ___  /  \  | `|   '      __  \   |  /-'            F . . . . \     '` 
//     |   \  \ \  /  |        __  /  \  |  |,-'        __,- J . . . . . \ 
//     |    | /  |/     __,-  \  ) \  /  |_,-     __,--'     |. .__.----,' 
//     |    |/    ___     \    |'.  |/      __,--'           `.-;;;;;;;;;\ 
//     |     ___  \  \     |   |  `   __,--'                  /;;;;;;;;;;;;. 
//     |     \  \  |-'\    '    __,--'                       /;;;;;;;;;;;;;;\ 
// \   |      | /  |      __,--'                             `--;;/     \;-'\ 
//  \  |      |/    __,--'                                   /  /         \  \ 
//   \ |      __,--'                                        /  /           \  \ 
//    \|__,--'                                          _,-;M-K,           ,;-;\ 
//                                                     <;;;;;;;;           '-;;;; 
//                                                                                  :D

```

> Detail

https://www.fmz.com/strategy/428614

> Last Modified

2023-10-07 15:24:31
