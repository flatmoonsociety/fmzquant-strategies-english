
> Name

Momentum-Trading-Strategy-Based-on-Trend-Tracking-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/991f185363219d82071b8ddd5aed4532f02c171a3e26f51dbabc1493b7a36954.png)
[trans]

## Overview
This strategy is based on the momentum indicator RSI and the trend following stop loss indicator SuperTrend, and designs a medium and long-term momentum trading strategy. This strategy is mainly used to identify the trend momentum existing in stock prices, and cooperate with stop loss to lock in profits and reduce the probability of significant retracement.
## Principle
1. Use RSI to identify trending momentum in stocks
The RSI indicator can effectively identify trends in stock prices. When RSI is above 60, it is an overbought zone, indicating that the current stock is in a strong upward trend; when RSI is below 40, it is an oversold zone, indicating that the current stock is in a downward trend.
This strategy generates a buy signal when the RSI is greater than 60, indicating that the upward momentum in the stock price has been recognized and that you can buy and go long.
2. Use SuperTrend for trend following stop loss
SuperTrend is a trend following stop loss indicator that calculates a dynamic stop loss line based on ATR and the price itself. When the price breaks through this stop loss line, it means that the trend has reversed and the current position should be stopped.
This strategy uses the stop loss line calculated by the SuperTrend indicator as the stop loss position of the strategy. When the price breaks through the stop loss line, the position will be closed immediately and the stop loss will be closed.
## Advantages
1. Identify trend momentum, profit from momentum
Using the RSI indicator can effectively identify the trend momentum existing in the stock price, so that you can enter the market early when the price forms a trend, and the potential profit space is greater.
2. Stop loss to control risks and lock in profits
Through the stop loss line of the SuperTrend indicator, you can stop the loss and leave the market in time to avoid excessive retracement. At the same time, you can also gradually raise the stop loss line to lock in profits as the trend progresses.
3. The strategy logic is clear and simple
This strategy uses a combination of two indicators. Each indicator has a clear meaning. The strategy logic is simple and clear, easy to understand and verify.
## Risk
1. Stop loss triggered due to false breakthrough
During the consolidation period, the price may experience some short-term breakthroughs and then quickly pull back false breakthroughs. This may cause the stop loss line to be triggered, resulting in some unnecessary losses.
2. Performance follows the market and has a certain correlation.
This strategy identifies trend momentum in stocks, so its performance will follow the trend of the broader market to a certain extent. When the market corrects, the strategy may incur additional losses.
3. Failure to recognize trend reversals
This strategy focuses on identifying and tracking trends and cannot effectively identify trend reversals. Once a sudden trend reversal occurs, it may be difficult for the strategy to stop losses in time, resulting in larger losses.
## Optimization direction
1. Optimize RSI parameters and improve recognition accuracy
You can test different RSI parameters and find the best parameter combination to improve RSI's accuracy in identifying trends.
2. Optimize stop loss strategy and reduce stop loss rate
You can try different types of stop loss methods, such as waiting for a certain period before leaving the market, to avoid being stopped out by high-frequency false breakthroughs.
3. Add trend reversal signals
You can consider adding indicators such as MACD to identify trend reversals in advance and avoid large losses after a strong trend reversal.
4. Consider appropriate hedging options
When the market faces major adjustments, you can consider adding a certain hedging portfolio to reduce the market correlation of the strategy.
## Summarize
This strategy uses the two key elements of RSI identification of trend momentum and SuperTrend's trend tracking stop loss to construct a simple and practical medium and long-term momentum strategy. This strategy can effectively track trends while controlling risks with stop loss. By optimizing parameters and adding reversal signals, the performance of the strategy can be further enhanced. Overall, this strategy has strong practicality.
||

## Overview

This strategy is based on the momentum indicator RSI and the trend tracking stop loss indicator SuperTrend, and designs a medium-to-long term momentum trading strategy. The strategy is mainly used to identify the trend momentum in stock prices and lock in profits with stop loss to reduce the probability of major retracements.

## Principles 

1. Identify trend momentum in stock prices using RSI

    The RSI indicator can effectively identify trends in stock prices. RSI above 60 is overbought zone, indicating that the stock is in a strong uptrend; RSI below 40 is oversold zone, indicating that the stock is in a downtrend.

    This strategy generates a buy signal when RSI is greater than 60, indicating that upward momentum is identified in stock prices, so we can buy.

2. Use SuperTrend for trend tracking stop loss

    SuperTrend is a trend tracking stop loss indicator, which calculates a dynamic stop loss line based on ATR and price itself. When the price breaks through this stop loss line, it indicates a trend reversal, so the current position should be stopped out.

    This strategy uses the stop loss line calculated by the SuperTrend indicator as the stop loss for the strategy. When the price breaks through the stop loss line, the position will be closed immediately.

## Advantages

1. Identify trend momentum, profit from momentum

    Using the RSI indicator can effectively identify the trend momentum in stock prices, so that we can get in early in the trend, and the potential profit space is greater.

2. Stop loss controls risk and locks in profit 

    Through the stop loss line of the SuperTrend indicator, we can stop loss in time to avoid excessive drawdowns. We can also gradually raise the stop loss line to lock in profits as the trend progresses.

3. Simple and clear strategy logic

    This strategy uses a combination of two indicators, each with a clear meaning, and the strategy logic is simple and clear, easy to understand and verify.

## Risks

1. Stop loss triggered by false breakouts

    During consolidation periods, prices may have some short-term false breakouts followed by quick pullbacks. This could trigger the stop loss line and cause some unnecessary losses.

2. Performance correlates with the broader market

    This strategy identifies trend momentum in stocks, so its performance will correlate to some extent with the broader market. When the market adjusts, the strategy may produce additional losses. 

3. Failure to identify trend reversals

    This strategy focuses on identifying and tracking trends, and cannot effectively identify trend reversals. In case of a sudden trend reversal, the strategy may fail to stop loss in time, leading to larger losses.

## Optimization Directions

1. Optimize RSI parameters for higher accuracy

    Test different RSI parameters to find the optimal combination to improve RSI's accuracy in trend identification.

2. Optimize stop loss strategies to lower stop loss rate

    Try different types of stop loss methods, such as waiting for a period before exiting, to avoid being stopped out by high frequency false breakouts.

3. Add trend reversal signals

    Consider adding indicators like MACD to identify trend reversals early, avoiding large losses after strong trend reversals.

4. Consider appropriate hedging

    During significant market corrections, appropriate hedging combos can be added to reduce the strategy's market correlation.

## Summary

This strategy builds a simple and practical medium-to-long term momentum strategy with the two key elements of identifying trend momentum using RSI and trend tracking stop loss using SuperTrend. The strategy can effectively track trends while controlling risk with stop loss. Further enhancements can be made through optimizing parameters and adding reversal signals. Overall, the strategy has strong practical utility.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-02 00:00:00
end: 2023-11-01 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//
// ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ 
//  -----------------------------------------------------------------------------
//  Copyright 2021 Amey Tavkar
//  Momentum Trading Strategy (Weekly Chart) script may be freely distributed under the MIT license.
//
//  Permission is hereby granted, free of charge, 
//  to any person obtaining a copy of this software and associated documentation files (the "Software"), 
//  to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, 
//  publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, 
//  subject to the following conditions:
//
//  The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
//
//  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, 
//  EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
//  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, 
//  DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
//  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
//
//  -----------------------------------------------------------------------------
//
//  Description
//  ===========
//  The strategy will open position when there is momentum in the stock
//  The strategy will ride up your stop loss based on the super trend.
//  The strategy will close your operation when the market price crossed the stop loss.
//  The strategy will close operation when the line based on the volatility will crossed
//
//  
//  -----------------------------------------------------------------------------
//  Disclaimer:
//    1. I am not licensed financial advisors or broker dealers. I do not tell you 
//       when or what to buy or sell. I developed this software which enables you 
//       execute manual or automated trades multplierFactoriplierFactoriple trades using TradingView. The 
//       software allows you to set the criteria you want for entering and exiting 
//       trades.
//    2. Do not trade with money you cannot afford to lose.
//    3. I do not guarantee consistent profits or that anyone can make money with no 
//       effort. And I am not selling the holy grail.
//    4. Every system can have winning and losing streaks.
//    5. Money management plays a large role in the results of your trading. For 
//       example: lot size, account size, broker leverage, and broker margin call 
//       rules all have an effect on results. Also, your Take Profit and Stop Loss 
//       settings for individual pair trades and for overall account equity have a 
//       major impact on results. If you are new to trading and do not understand 
//       these items, then I recommend you seek education materials to further your
//       knowledge.
//
//    YOU NEED TO FIND AND USE THE TRADING SYSTEM THAT WORKS BEST FOR YOU AND YOUR 
//    TRADING TOLERANCE.
//
//    I HAVE PROVIDED NOTHING MORE THAN A TOOL WITH OPTIONS FOR YOU TO TRADE WITH THIS PROGRAM ON TRADINGVIEW.
//    
//    I accept suggestions to improve the script.
//    If you encounter any problems I will be happy to share with me.
//  -----------------------------------------------------------------------------
//
// ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒
strategy("Momentum Trading Strategy (Weekly Chart)", precision = 2, overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 10)

//Entry
[fastSupertrend, fastSupertrendDir]  = supertrend(5, 1)
rsi = rsi(close, 14)
entry = close > fastSupertrend and rsi > 60
strategy.entry("Long", strategy.long, when = entry)
plotshape(entry and strategy.opentrades == 0,color=color.green,text="Buy",location=location.belowbar,style=shape.labelup,textcolor=color.white, size = size.normal)
plot(fastSupertrendDir == -1 and strategy.opentrades == 1  ? fastSupertrend : na, title="Active Trade", style=plot.style_linebr, linewidth=2, color=color.blue)

//Exit
exit = close < fastSupertrend
strategy.close("Long", when = exit)
plotshape(exit and strategy.opentrades == 1,color=color.red,text="Sell",style=shape.labeldown,textcolor=color.white, size=size.normal)
```

> Detail

https://www.fmz.com/strategy/430834

> Last Modified

2023-11-02 13:59:20
