
> Name

Dual-Channel-Donchian-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2a5dd74038a69fffec33c656108f2635bf0b404089e2c57510fc186a881a62ea.png)
[trans]

This strategy is based on the Donchian Channel indicator and implements the trading strategy of buying upper track breakthroughs and selling lower track breakthroughs.
#### Strategy Principle
The strategy implements buy and sell signals respectively by calculating the upper and lower rails of different parameters.
Upper rail calculation formula: Upper rail = highest value (length 1)
Lower rail calculation formula: Lower rail = lowest value (length 2)
The calculation formula of the central axis is: central axis = (upper rail + lower rail)/2
When the closing price exceeds the upper band, a buy signal is generated; when the closing price is below the lower band, a sell signal is generated.
The advantage of this strategy is that it can achieve more flexible trading rules by adjusting the parameters of the upper and lower rails.
#### Strategic Advantages
1. You can customize the upper and lower rail parameters so that the buying and selling rules can be independently controlled and more flexible.
2. By measuring the average position of the upper and lower rails through the central axis indicator, you can more clearly judge price breakthroughs.
3. Tang Qian Channel has trend tracking performance and can effectively capture trend opportunities.
4. The strategy is simple to operate and easy to implement.
#### Strategy Risk
1. It is easy to produce false breakthroughs and needs to be filtered in combination with other indicators.
2. It is impossible to judge the trend divergence, which requires manual or other indicators.
3. Improper setting of upper and lower rail parameters may lead to being too aggressive or conservative, so you need to pay attention to parameter adjustment.
#### Strategy optimization direction
1. You can consider combining indicators such as moving averages to filter out false breakthroughs.
2. The real breakthrough probability can be determined by combining volatility indicators.
3. The upper and lower rail parameters can be dynamically adjusted to implement adaptive trading rules.

#### Summarize
This strategy achieves flexible breakthrough operations through the dual-track Tang Qian channel. The strategy is simple and easy to operate, but there is a certain probability of false breakthroughs. Filtering can be performed through parameter optimization and combination with other indicators to improve the strategy effect.
||


This strategy is based on the Donchian Channel indicator to implement trading signals on upper and lower band breakouts. 

#### Strategy Logic

The strategy calculates upper and lower bands with different parameters to generate buy and sell signals respectively.

Upper Band Formula: Upper = Highest(length1)
Lower Band Formula: Lower = Lowest(length2) 
Mid Line Formula: Mid Line = (Upper + Lower) / 2

When close price breaks above upper band, a buy signal is generated. When close price breaks below lower band, a sell signal is generated.

The advantage of this strategy is the flexibility to customize upper and lower band parameters for more flexible trading rules.

#### Advantages

1. Customizable upper and lower band parameters for independent long and short control.

2. Mid line indicator shows average position of bands for clearer breakout judgment.  

3. Donchian Channel has trend following characteristic to catch trend opportunities.

4. Simple logic and easy to implement.

#### Risks

1. Vulnerable to false breakouts, needs filter from other indicators.

2. Unable to detect trend divergence, requires manual or other indicator combination.

3. Improper parameter tuning leads to over-aggressiveness or over-conservativeness.

#### Enhancement Directions 

1. Incorporate moving averages etc. to filter false breakouts.

2. Add volatility measures to quantify true breakout probability. 

3. Dynamically adjust upper and lower band parameters for adaptive trading rules.

#### Conclusion

This strategy implements flexible breakout trading via dual-band Donchian Channel. Simple logic but contains certain false breakout probabilities. Can be improved by parameter tuning, filters and supplementary indicators.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Upper Channel|
|v_input_2|20|Lower Channel|
|v_input_3|false|Offset Bars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-19 00:00:00
end: 2023-12-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Modified Donchian Channel with separate adjustments for upper and lower levels, with offset
// Strategy to buy on break upper Donchian and sell on lower Donchian
strategy("Donchian Backtest", overlay=true)

length1 = input(20, minval=1, title="Upper Channel")
length2 = input(20, minval=1, title="Lower Channel")
offset_bar = input(0,minval=0, title ="Offset Bars")
max_length = max(length1,length2)

upper = highest(length1)
lower = lowest(length2)

basis = avg(upper, lower)

l = plot(lower, style=line, linewidth=3, color=red, offset=1)
u = plot(upper, style=line, linewidth=3, color=green, offset=1)

plot(basis, color=yellow, style=line, linewidth=1, title="Mid-Line Average")
//break upper Donchian (with 1 candle offset) (buy signal)
break_up = (close >= upper[1])
//break lower Donchian (with 1 candle offset) (sell signal)
break_down = (close <= lower[1])


if break_up
    strategy.entry("buy", strategy.long,1)
if break_down
    strategy.close("buy")

//plot(strategy.equity)


    


```

> Detail

https://www.fmz.com/strategy/436595

> Last Modified

2023-12-26 10:18:51
