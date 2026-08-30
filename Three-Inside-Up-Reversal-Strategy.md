
> Name

Three-Inside-Up-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10fc9d799add7abfc1e.png)

[trans]


## Overview
The three-inside rising reversal strategy is a reversal trading strategy that realizes buying low and selling high by identifying specific three K-line patterns. It consists of three K lines. The first and second K lines form a yang swallowing yin. The opening price of the third K line is higher than the closing price of the previous day, and the closing price is higher than the highest price of the first two K lines. This K-line combination indicates the possibility of a short-term decline turning into an increase, and is a signal for reversal operations.
## Strategy Principle
The key judgment conditions of this strategy are:
1. The first K line: Yin line, the opening price is higher than the closing price
2. The second K line: Yang line, the closing price is higher than the opening price, and the closing price is lower than the opening price of the previous K line
3. The third K line: Yang line, the opening price is higher than the closing price of the previous K line, and the closing price is higher than the highest price of the previous two K lines.
When this signal is detected, we take a short position and set take profit and stop loss conditions. The specific transaction logic is as follows:
1. When an upward trend within three days is detected, enter the market at the opening price of the positive line and go short.
2. Set the take-profit condition: If the price rise reaches the entered take-profit point, the transaction will be ended and the short position will be closed.
3. Set stop loss conditions: If the price falls by the input stop loss points, the transaction will be ended and the short position will be closed.
4. When the price reaches the take-profit or stop-loss point, clear the position and wait for the next round of trading signals.
In this way, we can go short in time when we judge an upward reversal signal, decisively stop profit and stop loss when the profit reaches expectations or a loss beyond the controllable range occurs, and realize the reversal trading strategy of buying low and selling high.
## Strategic Advantages
- Capture reversal points and achieve the purpose of reversal trading
- Short high points and long low points, in line with trend trading logic
- Has clear entry, take-profit, and stop-loss mechanisms
- Simple three K-line pattern, easy to identify and implement
- Customizable stop-profit and stop-loss points to control risks
- The code implementation is concise and clear, easy to understand and optimize
In summary, this strategy has the characteristics of capturing reversals, controlling risks, being simple and reliable, and is a practical and efficient short-term reversal trading strategy.
## Strategy Risk
- The reversal pattern judgment is inaccurate and may become a non-reversal signal.
- If the stop-profit and stop-loss points are not set properly, you may stop the loss too early or miss out on larger profits.
- The strategy expects frequent trading, and there is a risk of over-trading
- There is still room for optimization in aspects such as buying and selling point identification and position management.
- Careful stock selection is required, this strategy is more suitable for stocks with volatile characteristics
- The impact of handling fees and slippage costs on profits needs to be considered
- Need to continuously optimize monitoring and respond to market changes in a timely manner
Generally speaking, by optimizing parameter settings, strict stock selection, continuous monitoring and other measures, the trading risk of this strategy can be controlled.
## Optimization direction
- Optimize K-line morphological parameters and improve recognition accuracy
- Optimize the stop-profit and stop-loss mechanism to achieve a better risk-return balance
- Combined with other technical indicators to filter signals to improve decision-making accuracy
- Add a position management mechanism to dynamically adjust positions according to market conditions
- Optimize fund management to achieve better profit and loss balance
- Test different holding times and determine the best holding period
- Optimize the code structure and add comments to make the strategy clearer
- Add real-time simulation comparison to test the effectiveness of the strategy
- Adjust the stock pool and test the adaptability of strategic industries and individual stocks
- Continuously track strategy performance, identify problems in a timely manner and adjust strategies
## Summarize
The three-in-one rising reversal strategy identifies three specific K-line patterns and makes profits by shorting when a short-term downtrend reversal signal is detected. The strategy has the advantages of clear trading logic, a stop-profit and stop-loss mechanism to control risks, and is easy to implement and optimize. It is a reliable and practical short-term reversal trading strategy. However, there are also certain uncertain risks, and it is necessary to avoid risks through parameter optimization, risk control and continuous tracking optimization, and obtain stable excess returns in the real market.
||


## Overview

The Three Inside Up reversal strategy is a reversal trading strategy that aims to buy low and sell high by identifying specific three-bar candlestick patterns. It consists of three bars where the first two form a bullish harami pattern and the third bar opens above the previous close and closes above the highs of the first two bars. This candlestick combination indicates a potential reversal from a downtrend to an uptrend and signals an opportunity to enter a reversal trade.

## Strategy Logic

The key conditions for this strategy are:

1. Bar 1: Bearish candle, open higher than close 

2. Bar 2: Bullish candle, close higher than open and lower than Bar 1 open

3. Bar 3: Bullish candle, open higher than Bar 2 close and close higher than highs of Bars 1 and 2

When this pattern is detected, we take a short position and set profit take and stop loss levels. The trading logic is as follows:

1. Enter short at the open of Bar 3 when Three Inside Up pattern is identified

2. Set profit target: Close trade and flatten position if price rises by the input number of profit points  

3. Set stop loss: Close trade and flatten if price declines by the input number of loss points

4. Clear position when target or stop is hit, await next signal

This allows us to quickly enter a short when an uptrend reversal signal is identified, and realize gains or limit losses using pre-defined profit and stop levels, implementing a low buy high sell reversal strategy.

## Advantages

- Captures reversal points for reversal trading

- Shorts tops and buys bottoms aligning with trends  

- Clear entry, profit take, and stop loss mechanics

- Simple 3-bar pattern, easy to identify and implement

- Customizable profit take and stop loss points to control risk

- Code is simple, clean, easy to understand and optimize

In summary, this strategy leverages pattern recognition, risk management, simplicity, and reliability making it an effective short-term reversal trading strategy.

## Risks

- Pattern may be misidentified, leading to false signals

- Inadequate profit take or stop loss levels could lead to premature exit or missed profits

- Frequent trading increases overtrading risk 

- Entry, position sizing, and management can be further optimized

- Careful stock selection required, better for volatile stocks

- Impact of commissions and slippage on profits

- Requires ongoing monitoring and tuning for changing markets

Proper parameter optimization, stock selection, monitoring and other measures can help control the risks.

## Enhancement Opportunities

- Optimize pattern parameters to improve accuracy

- Refine profit take and stop loss for better risk-reward

- Add filters using other indicators to improve signal reliability 

- Incorporate dynamic position sizing aligned to market conditions

- Optimize capital allocation for better profit balancing

- Test different holding periods to determine optimal duration

- Streamline code with comments for clarity

- Backtest versus live performance to validate efficacy

- Adjust stock universe and test sector and name fit

- Continuously track performance and tune as required

## Conclusion

The Three Inside Up Reversal strategy aims to profit from shorting tops when an uptrend reversal signal is identified based on a specific three-candlestick pattern. With clear logic, risk controls, ease of use, and optimization potential, it is a reliable and practical short-term reversal trading strategy. But uncertainties exist requiring ongoing optimizations, risk management, and monitoring to generate consistent excess returns in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Take Profit pip|
|v_input_2|20|Stop Loss pip|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-29 00:00:00
end: 2023-10-29 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 12/02/2019
//    This is a three candlestick bullish reversal pattern consisting of a 
//    bullish harami pattern formed by the first 2 candlesticks then followed 
//    by up candlestick with a higher close than the prior candlestick.
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title = "Three Inside Up Backtest", overlay = true)
input_takeprofit = input(20, title="Take Profit pip", step=0.01)
input_stoploss = input(20, title="Stop Loss pip", step=0.01)
barcolor(open[2] > close[2] ? close[1] > open[1] ? close[1] <= open[2] ? close[2] <= open[1] ? close[1] - open[1] < open[2] - close[2] ? close > open ? close > close[1] ? open > open[1] ? close > open[2] ? yellow :na :na : na : na : na:na : na : na : na)
posprice = 0.0
pos = 0.0
barcolor(nz(pos[1], 0) == -1 ? red: nz(pos[1], 0) == 1 ? green : blue ) 
posprice := open[2] > close[2] ? close[1] > open[1] ? close[1] <= open[2] ? close[2] <= open[1] ? close[1] - open[1] < open[2] - close[2] ? close > open ? close > close[1] ? open > open[1] ? close > open[2]  ? close :nz(posprice[1], 0) :nz(posprice[1], 0) : nz(posprice[1], 0) : nz(posprice[1], 0) :nz(posprice[1], 0):nz(posprice[1], 0):nz(posprice[1], 0):nz(posprice[1], 0):nz(posprice[1], 0) 
pos := iff(posprice > 0, -1, 0)
if (pos == 0) 
    strategy.close_all()
if (pos == -1)
    strategy.entry("Short", strategy.short)
posprice := iff(low <= posprice - input_takeprofit and posprice > 0, 0 ,  nz(posprice, 0))
posprice := iff(high >= posprice + input_stoploss and posprice > 0, 0 ,  nz(posprice, 0))
```

> Detail

https://www.fmz.com/strategy/430583

> Last Modified

2023-10-30 15:36:07
