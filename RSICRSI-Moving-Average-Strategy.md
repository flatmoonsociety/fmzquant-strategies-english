
> Name

CRSI-Moving-Average-Strategy based on moving average superimposed RSI strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1806cdee425fbcbabec.png)
[trans]

## Overview
This strategy builds a custom comprehensive indicator CRSI by calculating the mean of RSI, positive and negative indicators and price change percentage rankings, and calculates its simple moving average MA to determine price trends and generate trading signals.
## Strategy Principle
This strategy first calculates the 3-day RSI of the price to determine whether the price is overheated or too cold; at the same time, it calculates the positive and negative indicators of the price to determine the price movement trend; in addition, it also calculates the percentage ranking ROC of the price to determine the relative change speed of the price. Then take the average of these three indicators to construct a custom comprehensive indicator CRSI. CRSI can reflect the comprehensive trend of prices. Finally, calculate the 2-day simple moving average MA of CRSI. When the MA crosses above the 40 level, go long; when the MA crosses below the 70 level, close the position.
## Advantage Analysis
This strategy builds a customized CRSI indicator by combining multiple indicators to make trading signals more reliable. RSI can judge whether the price is too hot or too cold, the positive and negative indicators can judge the price momentum, and the ROC can judge the speed of price change. Combining them together forms the CRSI indicator, making trading signals more comprehensive and reliable. In addition, the use of MA can also further filter out false signals.
## Risk Analysis
Although this strategy uses a combination of multiple indicators, it may still produce false signals in specific market environments. For example, in a volatile market, indicators such as RSI and ROC may generate frequent buying and selling signals, but in fact there is no obvious price trend; or after an emergency occurs, multiple indicators may lag behind, risking delays in generating trading signals. These situations may lead to strategic trading losses. These risks can be reduced by optimizing parameters or adding other filtering conditions.
## Optimization direction
The following aspects can be considered to optimize this strategy: 1) Optimize the parameters of RSI, positive and negative indicators, and ROC to make the CRSI indicator more stable and reliable; 2) Add other auxiliary indicators for combination, such as KDJ, MACD, etc., to make the signal more comprehensive; 3) Optimize the parameters of MA to reduce the risk of delay; 4) Add stop loss conditions to control single losses; 5) Combine with longer period indicators to determine the trend situation and avoid frequent transactions in volatile markets.
## Summarize
This strategy builds a CRSI custom indicator by calculating the moving averages of RSI, positive and negative lines, and ROC, and then calculates the MA of CRSI, and performs buying and selling operations when the Golden Cross and Death Cross occur between the MA and the specified price level. This multi-indicator combination can make trading signals more stable and reliable. However, this strategy still needs to further optimize parameters and add auxiliary indicators and filtering conditions to reduce the impact of false signals and market environment and improve stable profitability.
||

## Overview

This strategy constructs a custom composite indicator CRSI by taking the average of RSI, bull/bear power and price rate of change percentage rank, and trades based on the moving average of CRSI crossing fixed levels.

## Strategy Logic

The strategy first calculates the 3-day RSI of price to gauge whether price is overbought or oversold. Meanwhile, it calculates the bull/bear power of price to judge the momentum. It also calculates the percentage rank of price rate of change (ROC) to check the relative speed of price change. Then it takes the mean of these three indicators to construct a custom composite indicator CRSI, which reflects the overall condition of price. Finally it calculates the 2-day simple moving average (MA) of CRSI. When MA crosses above the level of 40, it goes long. When MA crosses below the level of 70, it exits long positions.

## Advantage Analysis 

This strategy combines multiple indicators to construct the custom CRSI indicator, making trading signals more reliable. RSI can tell whether price is overheated or oversold. Bull/bear power can judge the momentum. ROC checks how fast price is changing. Combining them together into CRSI makes trading signals more comprehensive and reliable. Additionally, the use of MA also helps filter out false signals.  

## Risk Analysis

Although this strategy uses multiple indicators for a combo, it still risks generating false signals in certain market conditions. For instance, in range-bound markets, RSI, ROC and other indicators may produce frequent buy and sell signals while actually price has no clear trend. Or some indicators may lag and delay generating trading signals after a sudden event happens. These situations can cause losses. The risks could be reduced by optimizing parameters or adding other filtering conditions.

## Optimization Directions

Here are some aspects that could optimize this strategy: 1) Optimize the parameters of RSI, bull/bear power and ROC to make CRSI more steady and reliable; 2) Add other auxiliary indicators like KDJ, MACD into the combo for more comprehensive signals; 3) Optimize the MA parameters to lower the delay risk; 4) Add stop loss conditions to control single loss; 5) Incorporate longer-term indicators to judge trend status, avoiding overtrading in range-bound markets.  

## Conclusion

This strategy constructs a custom indicator CRSI based on the mean of RSI, bull/bear power and ROC, and trades on the MA of CRSI crossing fixed levels. Such a multi-indicator combo can make trading signals more stable and reliable. But this strategy still calls for further optimization on parameters, auxiliary indicators and filtering conditions to reduce false signals and the impacts of market regimes, so as to improve steady profitability.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
src = close, lenrsi = 3, lenupdown = 2, lenroc = 100, malengt = 2, low = 40, high = 70, a = 1, vlow = 20
updown(s) => 
    isEqual = s == s[1]
    isGrowing = s > s[1]
    ud = 0.0
    ud := isEqual ? 0 : isGrowing ? (nz(ud[1]) <= 0 ? 1 : nz(ud[1])+1) : (nz(ud[1]) >= 0 ? -1 : nz(ud[1])-1)
    ud
rsi = rsi(src, lenrsi)
updownrsi = rsi(updown(src), lenupdown)
percentrank = percentrank(roc(src, 1), lenroc)
crsi = avg(rsi, updownrsi, percentrank)
MA = sma(crsi, malengt)

band1 = 70
band0 = 40
band2 = 20

ColorMA = MA>=band0 ? lime : red

p1 = plot(MA, title="BuyNiggers", style=line, linewidth=4, color=ColorMA)

p2 = plot(low, title="idk", style=line, linewidth=2, color=blue)
p3 = plot(high, title="idk2", style=line, linewidth=2, color=orange)
p4 = plot(vlow, title="idk3", style=line, linewidth=1, color=red)

//@version=2
strategy("CMARSI")


if crossover(MA, band0)
    strategy.entry("buy", strategy.long, 1, when=strategy.position_size <= 0)
    
if crossunder(MA, band1)
    strategy.exit("close", "buy",  1, profit=1, stop=1)
    



plot(strategy.equity)

```

> Detail

https://www.fmz.com/strategy/440880

> Last Modified

2024-02-02 18:12:17
