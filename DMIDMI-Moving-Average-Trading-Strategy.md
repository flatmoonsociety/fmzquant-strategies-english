
> Name

DMI Multiplier Moving Average Trading StrategyDMI-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

A new quantitative trading strategy that is mainly based on the DMI indicator to identify the bottom and top of the market. This article will introduce in detail the principles, advantages and possible risks of this trading strategy.
## Strategy Principle
The full name of the DMI indicator is the Average Directional Movement Index. It was proposed by Welles Wilder in the 1970s and is used to judge the trend and strength of the market. The DMI indicator consists of three lines:
- +DI: represents the strength of the upward trend
- -DI: represents the strength of the downward trend
- ADX: represents the average strength of the trend
When +DI crosses -DI, ​​it means that the upward trend has strengthened, and you can consider going long; when -DI crosses +DI, it means that the downward trend has strengthened, and you can consider going short.
The core logic of this strategy is:
1. When the +DI line crosses 10 and the -DI line crosses 40, go long
2. When the -DI line crosses 10 and the +DI line crosses 40, go short.
That is to say, when the reverse DI line is significantly stronger than the forward DI line, it can be judged that the current trend is about to reverse, and then you can appropriately intervene to perform reverse operations.
In order to filter out confusion, this strategy uses the moving average of DI, and the specific parameters are set as:
- The period length of both +DI and -DI is 11
- ADX has a smoothing period of 11
Control the frequency of trading signals by adjusting the moving average parameters.
This strategy is mainly used in NIFTY50 index options trading, but can also be used in other varieties. In specific transactions, choose at-the-money options and set the stop loss to 20%. If the loss exceeds 10%, the position will be increased. However, if the loss expands to exceed 20% of the initial investment, the stop loss will be eliminated.
## Strategic Advantages
Compared with the simple DI crossover strategy, this strategy uses the moving average filter of the DI indicator, which can effectively reduce whipsaw and reduce the number of transactions, thereby reducing transaction costs and slippage losses.
Compared with a simple trend following strategy, this strategy is more accurate in judging trend reversal points and can capture trading opportunities near turning points in a timely manner.
The parameter optimization of this strategy is relatively simple and easy to achieve effect optimization.
## Risk warning
This strategy only gives the direction of the trading signal, and the specific stop-loss and take-profit requirements need to be set according to personal risk preference.
The DMI indicator may produce a large number of false signals when in the consolidation area, so this strategy should be avoided in non-trending markets.
DI crossover cannot predict the trend turning point 100%, and there are certain timing errors. Trading signals should be verified appropriately in conjunction with other indicators.
## Summarize
This strategy can effectively identify trend reversal opportunities through the screening of DI moving averages. Compared with other trend following strategies, it has the advantage of stronger reversal recognition ability. Generally speaking, the parameter optimization of this strategy is flexible and suitable for use as a module of the quantitative trading system. When using it, you need to pay attention to guard against false signals and properly evaluate the market trend.
||

Recently I have developed a new quantitative trading strategy mainly based on the DMI indicator to identify bottoms and tops in the market. This article will explain in detail the rationale, advantages and potential risks of this trading strategy.

## Strategy Logic  

The DMI indicator, short for Average Directional Movement Index, was created by Welles Wilder in the 1970s to gauge the trend and strength of the market. The DMI consists of three lines:

- +DI: representing the strength of uptrend
- -DI: representing the strength of downtrend
- ADX: representing the overall trend strength

When +DI crosses above -DI, it indicates strengthening uptrend and long position can be considered. When -DI crosses above +DI, it signals strengthening downtrend and short position can be considered.

The core logic of this strategy is:

1. Go long when +DI drops below 10 and -DI rises above 40
2. Go short when -DI drops below 10 and +DI rises above 40

That is to say, when the reverse DI diverges significantly from the forward DI, it can be judged that the current trend is likely to reverse, and reverse trading position can be taken appropriately. 

To filter noise, this strategy adopts moving average of DI with parameters set as:

- Period of +DI and -DI is 11
- Smoothing period of ADX is 11

By tuning the moving average parameters, the frequency of trading signals can be adjusted.

This strategy is mainly applied to trading NIFTY50 index options. It can also be used on other products. Specifically for trading, choose at-the-money options, set stop loss at 20%, add positions if loss exceeds 10%, but stop out if loss expands over 20% of initial capital.

## Advantages of the Strategy

Compared to simple DI cross strategies, this strategy uses DI moving averages to filter noise and reduce trades, thus lowering transaction costs and slippage. 

Compared to pure trend following strategies, this strategy is more precise at catching trend reversal points, enabling timely entries around turns.

The strategy optimization is simple with flexible parameters for performance tuning.

## Risk Warnings

This strategy only provides directional signals. Specific requirements on stop loss and take profit should be set according to personal risk preference.

DMI may produce many false signals during range-bound periods. Avoid using this strategy in non-trending markets.

DI crossovers cannot fully predict trend reversals. There could be some timing errors. Other indicators should be used to validate the trading signals.

## Conclusion

By screening with DI moving averages, this strategy can effectively identify trend reversal opportunities. Compared to other trend following strategies, it has the advantage of stronger reversal recognition abilities. Overall, this strategy has flexible parameter tuning and can be used as a module in quantitative trading systems. Pay attention to false signals and properly assess the market regime when using it.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|11|ADX Smoothing|
|v_input_int_2|11|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-05 00:00:00
end: 2023-09-12 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © email_analysts
// This code gives indication on the chart to go long based on DMI and exit based on RSI. 
//Default value has been taken as 14 for DMI+ and 6 for RSI.
//@version=5
strategy(title="DMI Strategy", overlay=false)
lensig = input.int(11, title="ADX Smoothing", minval=1, maxval=50)
len = input.int(11, minval=1, title="DI Length")
up = ta.change(high)
down = -ta.change(low)
plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
trur = ta.rma(ta.tr, len)
plus = fixnan(100 * ta.rma(plusDM, len) / trur)
minus = fixnan(100 * ta.rma(minusDM, len) / trur)
sum = plus + minus
adx = 100 * ta.rma(math.abs(plus - minus) / (sum == 0 ? 1 : sum), lensig)
//plot(adx, color=#F50057, title="ADX")
plot(plus, color=color.green, title="+DI")
plot(minus, color=color.red, title="-DI")
hlineup = hline(40, color=#787B86)
hlinelow = hline(10, color=#787B86)

buy = plus < 10 and minus > 40
if buy
    strategy.entry('long', strategy.long)

sell = plus > 40 and minus < 10
if sell
    strategy.entry('short', strategy.short)


```

> Detail

https://www.fmz.com/strategy/426579

> Last Modified

2023-09-13 14:42:19
