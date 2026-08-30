
> Name

Breakout-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

### Strategy Overview
The breakout tracking strategy is a long-only short-term trading strategy. It monitors whether the price breaks through the upper Bollinger Band, and if it breaks through, it will enter the long direction. There are two options for exiting: the first is to close the position when the price breaks through the lower Bollinger Band; the second is to close the position when the price falls below the central axis. This strategy ignores the impact of slippage and fees.
### Strategy Principles
1. When the price breaks through the upper Bollinger Band, enter the market long.
2. There are two ways to exit:
- Option 1: Close the position when the price falls below the lower Bollinger Band
- Option 2: Close the position when the price falls below the Bollinger Bands central axis
3. The impact of slippage and handling fees is not considered when calculating returns.
This strategy uses the Bollinger Bands indicator to determine trends and overbought and oversold conditions. Bollinger Bands consists of a central axis, an upper track, and a lower track. The central axis is a simple moving average of n-day closing prices, and the upper and lower rails are channel bands drawn based on standard deviation. The upper and lower rails can be regarded as resistance and support lines for future prices.
When the price breaks through the upper track, it means that a bull market is forming and you can go long. When the price falls below the lower track, it indicates that a bear market is coming and positions should be closed. The central axis represents the average level of prices.
The advantage of this strategy is that it uses Bollinger Bands to determine the trend direction, which can reduce the risk of false breakthroughs. It only goes long when the trend appears, which is in line with the idea of ​​trend trading. And there are two different exit methods, you can choose a more appropriate method according to market conditions.
### Strategic Advantages
- Using Bollinger Bands to determine trends can reduce the risk of false breakthroughs
- Only go long in trending bull markets, in line with trend trading ideas
- Provide two different exit methods to flexibly respond to market changes
- Ignore slippage and handling fees, making it easier to calculate profits
- Suitable for various time periods and can be used for intraday and trend trading
### Risk warning
- There is a certain risk of false breakthroughs, and the Bollinger Bands indicator cannot be completely avoided.
- Ignoring slippage and fees will overestimate actual returns
- You cannot profit in a bear market by only going long
- Parameters, such as breakthrough cycles, central axis cycles, etc., should be appropriately adjusted to adapt to market changes
### Summarize
Overall, the breakthrough tracking strategy is a trend tracking strategy with relatively high optimization and controllable risks. It determines the trend direction based on the Bollinger Bands indicator, chooses the long direction when the trend appears, and provides two exit mechanisms to control risks. This strategy is simple to operate, easy to implement, and suitable for various time periods. However, we need to pay attention to guard against false breakthroughs and make parameter adjustments to adapt to the complex and changeable market environment.
||
This is an SEO optimized article about the Donchain Breakout strategy: 

### Strategy Overview

The breakout tracking strategy is a long-only short-term trading strategy. It monitors whether the price breaks out above the Bollinger Band upper rail and goes long if the breakout happens. There are two exit options: the first is to exit when the price breaks down below the Bollinger Band lower rail, and the second is to exit when the price breaks down below the middle line. This strategy ignores the impact of slippage and commissions on profit calculation.

### Strategy Logic

1. Go long when the price breaks out above the Bollinger Band upper rail.  

2. There are two exit options:

    - Option 1: Exit when the price breaks down below the Bollinger Band lower rail.

    - Option 2: Exit when the price breaks down below the Bollinger Band middle line.
    
3. Slippage and commissions are not considered in profit calculation.

The strategy utilizes the Bollinger Bands indicator to determine the trend and overbought/oversold situation. The Bollinger Bands consist of a middle line, an upper rail and a lower rail. The middle line is a simple moving average of the closing prices over n periods. The upper and lower rails are plotted based on standard deviation to form an envelop channel. The upper and lower rails can be seen as the future resistance and support levels of the price.

When the price breaks out above the upper rail, it signals that an uptrend is forming and a long position can be initiated. When the price breaks down below the lower rail, it indicates the coming of a downtrend and the position should be closed. The middle line represents the average price level. 

The advantage of this strategy is that it uses Bollinger Bands to determine the trend direction, which can reduce the risk associated with false breakouts. It only goes long when an uptrend emerges, which aligns with the trend trading mentality. Also, there are two different exit options that can be selected based on market conditions.

### Advantages of the Strategy

- Uses Bollinger Bands to determine trends, reducing the risk of false breakouts

- Only goes long in uptrends, aligning with trend trading mentality 

- Provides two exit options to flexibly adapt to market changes

- Ignores slippage and commissions, making profit calculation simpler

- Applicable to different time frames, for intraday and trend trading

### Risk Warnings

- Still has some risks of false breakouts, which Bollinger Bands cannot completely avoid

- Ignoring slippage and commissions overestimates actual profits

- Being long-only means no profit can be made in downtrends

- Parameters like breakout period, middle line period should be adjusted for market changes

### Conclusion

Overall, the breakout tracking strategy is a highly optimized, risk-controlled trend following strategy. It uses Bollinger Bands to determine the trend direction and goes long when a trend emerges, with two exit mechanisms to control risks. The strategy is simple to implement and applicable to different time frames. But false breakouts should be watched out for, and parameters should be adjusted accordingly to adapt to the complex and ever-changing markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2|true|Exit Option|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-09-14 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Senthaamizh

//Break out trading system works best in a weekly chart and daily chart of Nifty and BankNifty
//@version=4

strategy("Donchain BO",shorttitle = "DBO",default_qty_type = strategy.percent_of_equity,default_qty_value = 100, overlay=true)
length = input(20, minval=1)
exit = input(1, minval=1, maxval=2,title = "Exit Option") // Use Option 1 to exit using lower band; Use Option 2 to exit using basis line

lower = lowest(length)
upper = highest(length)
basis = avg(upper, lower)

l = plot(lower, color=color.blue)
u = plot(upper, color=color.blue)
plot(basis, color=color.orange)
fill(u, l, color=color.blue)

longCondition = crossover(close,upper[1])
if (longCondition)
    strategy.entry("Long", strategy.long)

if(exit==1)
    if (crossunder(close,lower[1]))
        strategy.close("Long")

if(exit==2) 
    if (crossunder(close,basis[1]))
        strategy.close("Long")




```

> Detail

https://www.fmz.com/strategy/426895

> Last Modified

2023-09-15 12:36:43
