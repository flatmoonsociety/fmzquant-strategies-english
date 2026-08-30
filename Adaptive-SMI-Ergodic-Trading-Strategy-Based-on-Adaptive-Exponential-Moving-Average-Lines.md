
> Name

Quantitative trading strategy Adaptive-SMI-Ergodic-Trading-Strategy-Based-on-Adaptive-Exponential-Moving-Average-Lines based on Adaptive Exponential-Moving-Average-Lines
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/135469392197ddfdfc7.png)
 [trans]

## Overview
This article will provide an in-depth analysis of a quantitative trading strategy based on the Adaptive Exponential Moving Average (AEMA). This strategy uses the infinite volatility form of the Stochastic Momentum Index (SMI), combines the exponential moving average as a signal line, and sets customizable overbought and oversold thresholds to increase the probability of transaction execution.
## Strategy Principle
This strategy uses two different lengths of SMI, namely a short length and a long length. The difference between the two spans can generate trading signals. Additionally, the strategy utilizes an exponential moving average as a signal line. Go long when the short-period SMI crosses above the long-period SMA, and go short when the short-period SMI crosses below the long-period SMA. In order to filter out false signals, long entry signals only appear when the SMI is below the oversold line and the signal line is also below the oversold line; short signals require that the SMI is above the overbought line and the signal line is also above the overbought line. This dual condition setting makes the strategy more sensitive to emergencies and can also effectively avoid false breakthroughs.
## Strategic Advantages
The biggest advantage of this strategy is its adaptability. The strategy uses customizable overbought and oversold thresholds to dynamically adjust the criteria for long and short positions. This mechanism allows the strategy parameters to be adjusted and optimized according to different market environments, thereby adapting to a wider range of market types. In addition, the SMI infinite volatility form also enhances the sensitivity and timeliness of the strategy. Compared with traditional SMI, it has higher denoising effect and smaller lag. This enables the strategy to quickly respond to emergencies and capture short-term trading opportunities.
## Strategy Risk
The biggest risk with this strategy is its dependence on parameter settings. If parameters are set improperly, a large number of invalid trading signals will easily be generated. In addition, as a pulse-type indicator, SMI does not perform satisfactorily on random oscillating markets. When there is a trend reversal with violent price fluctuations, the strategy can easily be trapped. In order to control these risks, it is recommended to adopt strict risk management methods and adjust parameters to adapt to different market environments. Some feasible optimization directions will be proposed below.
## Strategy optimization direction
There are still several ways this strategy can be optimized. First, different combinations of SMA lengths can be tested to find the optimal parameter pair. Second, you can consider setting a stop loss near the entry point to control single losses. Third, you can combine it with other indicators, such as RSI, Bollinger Bands, etc., to set dynamic overbought and oversold lines. Fourth, parameters can be automatically optimized through machine learning algorithms. Fifth, strategies can be integrated into multi-factor models to improve stability.
## Summarize
This article provides an in-depth analysis of the principles, advantages, risks and optimization directions of an adaptive SMI infinite trading strategy. This strategy uses adaptive thresholds and exponential moving averages to filter signals, which can effectively capture short-term market opportunities. Although there is certain parameter dependence, through strict risk control and multi-faceted optimization, this strategy still has considerable practical value. I believe it can play an important role in the practice of quantitative trading and provide effective support for trading decisions.
|| 

## Overview

This article will conduct an in-depth analysis of a quantitative trading strategy based on Adaptive Exponential Moving Average (AEMA) lines. The strategy leverages the ergodic form of the Stochastic Momentum Index (SMI) indicator, together with an Exponential Moving Average serving as the signal line, and incorporates customizable overbought/oversold thresholds to improve the probability of successful trade execution.  


## Strategy Principle 

The strategy uses two SMIs of different lengths, one short and one long, and the difference in span between them generates trading signals. In addition, the strategy also utilizes an Exponential Moving Average as the signal line. It goes long when the shorter period SMI crosses above the longer period SMA, and goes short when the opposite happens. To filter out false signals, long entry signals only appear when the SMI is below the oversold line and the signal line is also below the oversold line; short entry signals require the SMI to be above the overbought line and the signal line also above the overbought line. This dual condition setup makes the strategy more sensitive to sudden events, while also effectively avoiding false breakouts.  

## Advantages

The biggest advantage of this strategy lies in its adaptability. The strategy uses customizable overbought/oversold thresholds to dynamically adjust long and short criteria according to different market environments. This mechanism allows the strategy parameters to be optimized and adapted to a wider range of market conditions. In addition, the ergodic form of the SMI also enhances the sensitivity and timeliness of the strategy. Compared to the traditional SMI, it has higher noise reduction and smaller lag. This allows the strategy to respond quickly to sudden events and capture short-term trading opportunities.  

## Risks

The biggest risk of this strategy is its reliance on parameter settings. Improper parameter settings can easily generate a large number of invalid trading signals. In addition, as a pulse-type indicator, the SMI does not perform well in choppy random markets. The strategy can also easily get caught in violent trend reversal with extreme price fluctuations. To control these risks, it is recommended to adopt strict risk management measures while adjusting parameters to suit different market environments. Some feasible optimization directions will be proposed below.

## Optimization Directions

There are still several optimizable aspects of the strategy. First, different combinations of SMA lengths can be tested to find the optimal parameter pair. Second, stop losses can be considered near entry points to control per trade loss. Third, other indicators like RSI and Bollinger Bands can be combined to set dynamic overbought/oversold lines. Fourth, parameters can be automatically optimized through machine learning algorithms. Fifth, the strategy can be integrated into multi-factor models to improve stability.  

## Conclusion

This article has conducted an in-depth analysis of the principle, advantages, risks and optimization directions of an adaptive SMI ergodic trading strategy. Through the use of adaptive thresholds and signal filtering with exponential moving averages, the strategy can effectively capture short-term market opportunities. Despite certain parameter dependence, with stringent risk control and multi-dimensional optimizations, the strategy still possesses considerable practical value. It is believed that this strategy can play an important role in quantitative trading practices, providing effective support for trading decisions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|12|Long Length|
|v_input_int_2|5|Short Length|
|v_input_int_3|5|Signal Line Length|
|v_input_float_1|-0.4|Oversold|
|v_input_float_2|0.4|Overbought|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-10 00:00:00
end: 2023-12-17 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © DraftVenture

//@version=5
strategy(title="Adaptive SMI Ergodic Strategy", shorttitle="Adaptive SMI Strategy", overlay = false)
longlen = input.int(12, minval=1, title="Long Length")
shortlen = input.int(5, minval=1, title="Short Length")
siglen = input.int(5, minval=1, title="Signal Line Length")
overS = input.float(-0.4, title = "Oversold", step = 0.01)
overB = input.float(0.4, title = "Overbought", step = 0.01)
erg = ta.tsi(close, shortlen, longlen)
sig = ta.ema(erg, siglen)
plot(erg, color = color.yellow, title = "SMI")
plot(sig, color = color.purple, title="Signal")
hline(0, title = "Zero", color = color.gray, linestyle = hline.style_dotted)
h0 = hline(overB, color = color.gray, title = "Overbought Threshold")
h1 = hline(overS, color = color.gray, title = "Oversold Threshold")
fill(h0, h1, color=color.rgb(25, 117, 192, 90), title = "Background")

longEntry = ta.crossover(erg, sig) and erg > overS and sig < overS
shortEntry = ta.crossunder(erg, sig) and erg < overB and sig > overB

if longEntry
    strategy.entry("Long", strategy.long)

if shortEntry
    strategy.entry("Short", strategy.short)

// ______ _________ 
// ___  //_/__  __ \
// __  ,<  __  /_/ /
// _  /| | _  ____/ 
// /_/ |_| /_/   
```

> Detail

https://www.fmz.com/strategy/435705

> Last Modified

2023-12-18 10:34:55
