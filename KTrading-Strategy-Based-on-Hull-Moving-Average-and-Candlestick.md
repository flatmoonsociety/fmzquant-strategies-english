
> Name

Trading-Strategy-Based-on-Hull-Moving-Average-and-Candlestick
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The core idea of ​​this strategy is to compare the values ​​of the Hull Moving Average (HMA) and the K-line to generate buy and sell signals. Buy when HMA is above the K line and sell when HMA is below the K line.
## Principle
First, the strategy calculates the HMA of a certain period through the hma() function. Then, obtain the opening price of the previous K line as a comparison benchmark. If the HMA is higher than the opening price of the previous K line, a buy signal is generated; if the HMA is lower than the opening price of the previous K line, a sell signal is generated.
The entry condition of the strategy is to enter the market only when the price breaks through the HMA in the opposite direction. That is, only buy when the price breaks through the HMA from below; sell only when the price breaks through the HMA from above. This prevents the signal from being triggered repeatedly by a volatile market.
The exit condition of the strategy is to stop loss when the price falls back to the other side of the HMA. For example, if the price falls below the HMA after buying, stop loss and sell.
Generally speaking, this strategy uses the smoothing characteristics of HMA to identify the main trend direction and generate signals. At the same time, requiring price breakthroughs to filter out false signals can avoid being repeatedly trapped by market fluctuations.
## Advantage Analysis
1. Using HMA instead of SMA can better identify trends and filter shocks.
2. The breakthrough mechanism can reduce the probability of being trapped and repeatedly opening positions.
3. Using the previous K-line price instead of the current price to judge can avoid drawing back trace curves.
4. The rules are simple and clear, suitable for parameter optimization and robot trading.
5. Can be flexibly applied to any variety and cycle, and has universal applicability.
## Risks and improvements
1. Improper setting of HMA parameters may lead to missed trends or excessive sensitivity. You can teste different period parameters to find the best value.
2. A single indicator is easily thrown out of the market by breakthrough retries. You can consider combining other indicators to filter signals.
3. The stop loss point is close to the HMA and is easily stuck by another breakthrough. It can be appropriately extended to the support and resistance level.
4. Unable to judge the direction and strength of the trend, consider adding trend classification indicators.
5. Fixed stop loss points lead to large fluctuations in risk and return. You can try following stop loss or capital management.
## Summarize
Overall, this strategy is relatively simple and practical, with clear core ideas. Use HMA to determine the main trend direction and filter out false signals with breakthroughs. It can avoid repeated opening and holding of positions in a volatile market. Good results can be obtained through parameter optimization. However, as a strategy based on a single indicator, its reliability and winning rate still have certain limitations. It is recommended to use it in conjunction with other technical indicators or fund management methods to greatly improve stability. Overall, this strategy provides a simple and effective idea for quantitative trading and is worthy of in-depth study and application.
||

## Overview

The core idea of this strategy is to compare the Hull Moving Average (HMA) with candlestick values to generate buy and sell signals. It will buy when HMA is above candlestick and sell when HMA is below candlestick.

## Principles 

Firstly, the strategy calculates HMA of a certain period using hma() function. Then it gets the open price of the previous candlestick as benchmark. If HMA is higher than previous candle open price, a buy signal is generated. If HMA is lower than previous candle open price, a sell signal is generated.

The entry conditions are that the price needs to break HMA in reverse direction before entering the market. That means it will buy only when price breaks above HMA from below. It will sell only when price breaks below HMA from above. This avoids being whipsawed by oscillating markets.

The exit conditions are to stop loss when price falls back to the other side of HMA. For example, if price drops below HMA after buying, it will stop loss sell.

In summary, this strategy identifies the major trend direction using the smoothness of HMA to generate signals. Meanwhile, it requires price breakout to filter false signals and avoid being whipsawed by market noise.

## Advantage Analysis 

1. Using HMA instead of SMA can better identify trends and filter noise.

2. The breakout mechanism can reduce the probability of being trapped and opening repetitive positions.

3. Adopting previous candle price rather than current price avoids curve fitting. 

4. The rules are simple and clear, suitable for parameter optimization and robot trading.

5. Can be flexibly applied to any instrument and timeframe, with universality.

## Risks and Improvements

1. Improper HMA parameter setting may miss trends or be too sensitive. Can teste different periods to find optimal values.

2. Relying on single indicator is prone to be stopped out by breakout retries, consider combining other indicators to filter signals. 

3. Stop loss is too close to HMA, may be trapped again by subsequent breakout. Can appropriately widen stop to support/resistance. 

4. Unable to determine trend direction and strength. Consider adding trend classification indicators.

5. Fixed stop loss causes large fluctuation in risk/reward. Can try adaptive stops or money management. 

## Conclusion

This strategy is relatively simple and practical overall with a clear core idea. It identifies the major trend with HMA and filters fake signals with breakout. It avoids being whipsawed by choppy markets. Proper parameter optimization can achieve decent results. However, reliability and win rate are still limited as a single indicator strategy. It's recommended to combine with other technical indicators or money management methods to significantly improve robustness. In conclusion, this strategy provides a simple and effective approach for quantitative trading, which is worth in-depth research and application.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Hull MA Period|
|v_input_2|D|Candle Resolution|
|v_input_3_open|0|Source of Price: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SeaSide420. Any timeFrame/pair , Hull Moving Average vs Candle
//@version=4
strategy("Hull Moving Average vs Candle",shorttitle="HMA-vs-Candle",overlay=true,default_qty_type=strategy.percent_of_equity,default_qty_value=100,commission_type=strategy.commission.cash_per_order,commission_value=1.00,slippage=1)
Period=input(title="Hull MA Period",type=input.integer,defval=50,minval=1)
Resolution=input(title="Candle Resolution", type=input.resolution,defval="D")
Price=input(title="Source of Price",type=input.source,defval=open)
HMA=hma(Price,Period)
Candle=security(syminfo.tickerid,Resolution,Price,barmerge.gaps_off,barmerge.lookahead_off)
change_color=HMA>Candle?color.green:color.red
plot1=plot(Candle,color=change_color,title="Candle Line",linewidth=2,transp=50)
plot2=plot(HMA[1],color=change_color,title="Hull MA Line",linewidth=2,transp=50)
fill(plot1,plot2,color=change_color,transp=50)
strategy.close("BUY",when=Price<HMA and HMA<Candle,comment="close buy entry")
strategy.close("SELL",when=Price>HMA and HMA>Candle,comment="close sell entry")
if (Price>HMA and HMA>Candle and Price>Price[1])
    strategy.entry("BUY",strategy.long)
if (Price<HMA and HMA<Candle and Price<Price[1])
    strategy.entry("SELL",strategy.short)



//                                                                   /L'-, 
//                               ,'-.           /MM . .             /  L '-, 
//     .                    _,--dMMMM\         /MMM  `..           /       '-, 
//     :             _,--,  )MMMMMMMMM),.      `QMM   ,<>         /_      '-,' 
//     ;     ___,--. \MM(    `-'   )M//MM\       `  ,',.;      .-'* ;     .' 
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
//                                                                                        ~ priceless artwork by SeaSide420
```

> Detail

https://www.fmz.com/strategy/427437

> Last Modified

2023-09-21 10:31:58
