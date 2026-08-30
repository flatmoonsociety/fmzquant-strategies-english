
> Name

Momentum-Filtering-Moving-Average-Strategy Momentum-Filtering-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/940a2eace662f21762.png)
[trans]

### Overview
This is a moving average trading strategy built using momentum filtering technology. It filters small price fluctuations by setting a price change threshold, and only selects large price changes to participate in the calculation, thereby improving the stability of the strategy.
### Strategy Principles
The core indicator of this strategy is the momentum-filtered Chande Momentum Oscillator (CMO). The Chande Momentum Oscillator is a type of momentum indicator. It determines the long and short momentum by calculating the ratio of the sum of the absolute values ​​of the long and short days and the sum of the price rise and fall differences. This strategy improves it and sets a minimum price change threshold parameter Filter. Only when the price change exceeds this threshold, it will participate in the calculation of CMO. This filters out a large number of small fluctuations in the market, making the indicator more stable and reliable.
On the basis of calculating the indicator, it sets the upper line TopBand and the lower line LowBand. When the indicator exceeds these two lines, a trading signal is generated. Finally, the reverse input parameter reverse can invert the original signal to achieve reverse operation.
### Advantage Analysis
This is a very stable and reliable trend following strategy. Due to the use of momentum filtering technology, it can effectively filter market noise and prevent arbitrage. There is a large space for optimization of strategy parameters, and strategy indicators can be optimized by adjusting parameters such as Filter, TopBand, and LowBand. It also has a reverse trading function and can flexibly adapt to different market environments.
### Risk Analysis
This strategy is mainly based on trend following, so it is prone to false signals and losses in consolidating markets. In addition, improper parameter optimization can also lead to excessive trading frequency or unstable signals. Finally, improper use of reverse trading parameters may lead to unnecessary losses.
In order to reduce these risks, parameters should be reasonably optimized to make the signal more stable and reliable; avoid using this strategy in consolidation markets and choose more suitable strategic tools; use the reverse trading function with caution and avoid turning it on when the Parameter optimization is not good.
### Optimization direction
This strategy can be optimized from the following directions:
1. Optimize the Filter parameter value to ensure that the market noise is filtered while also ensuring that the transaction frequency is not too low.
2. Optimize the parameter range of TopBand and LowBand to match the market fluctuation range to prevent false signals.
3. Use methods such as walk forward analysis to dynamically optimize parameters to adapt the strategy parameters to market changes.
4. Add stop-loss and take-profit logic and set reasonable stop-loss points to control losses.
5. Combine with other indicator filtering, such as MACD, KD, etc., to avoid erroneous transactions in non-trending markets.

### Summarize
This is a very practical trend following strategy. It uses momentum filtering technology, which can effectively suppress market noise and make signals clearer and more reliable. Through parameter optimization and logic optimization, it can be tuned into a reliable and stable quantitative trading tool. However, you still need to pay attention to prevent risks caused by use in consolidation markets and improper parameter optimization. Overall, this is a very promising strategy template.
||  

### Overview  

This is a moving average trading strategy built with momentum filtering techniques. It sets a threshold for price changes to filter out small price fluctuations, only selecting large price movements for calculation, thereby improving the stability of the strategy.  

### Strategy Logic

The core indicator of this strategy is the Chande Momentum Oscillator (CMO) filtered by momentum. The Chande Momentum Oscillator is a kind of momentum indicator that judges the momentum of trends by calculating the ratio of the sum of the absolute values of up days and down days to the sum of price rises and falls. This strategy improves it by setting a minimum threshold of price changes called Filter. Only when the price change exceeds this threshold will it participate in the CMO calculation. This filters out a lot of small fluctuations in the market and makes the indicator more stable and reliable.

Based on the indicator calculation, it sets upper line TopBand and lower line LowBand. When the indicator exceeds these two lines, trading signals are generated. Finally, the reverse input parameter can reverse the original signals to realize reverse operation.

### Advantage Analysis  

This is a very stable and reliable trend-following strategy. By adopting momentum filtering techniques, it can effectively filter out market noise and prevent being trapped. The strategy has large parameter optimization space, parameters like Filter, TopBand, LowBand, etc. can be adjusted to optimize the strategy indicator. It also has reverse trading functionality that can flexibly adapt to different market environments.  

### Risk Analysis

The strategy mainly relies on trend-following, so it is prone to generating false signals and losses in range-bound markets. In addition, improper parameter optimization can also lead to excessive trading frequency or unstable signals. Finally, improper use of the reverse trading parameter may lead to unnecessary losses.  

To reduce these risks, parameters should be reasonably optimized to make the signals more stable and reliable; avoid using this strategy in range-bound markets, choose more suitable strategy tools; use reverse trading functions with caution, avoid enabling it when parameter optimization is not ideal.

### Optimization Directions

The strategy can be optimized in the following aspects:  

1. Optimize the Filter parameter value, ensure filtering market noise while keeping trading frequency not too low.

2. Optimize the parameter range of TopBand and LowBand to match the market volatility range to prevent false signals.  

3. Use walk forward analysis and other methods to dynamically optimize parameters so that strategy parameters adapt to market changes.  

4. Add stop loss logic and set reasonable stop loss points to control losses.

5. Filter with other technical indicators like MACD, KD to avoid false trades in non-trending markets.


### Summary  

This is a very practical trend-following strategy. It adopts momentum filtering techniques to effectively curb market noise and make clearer and more reliable signals. Through parameter optimization and logic optimization, it can be tuned into a reliable and stable quantitative trading tool. Still, risks from using it in range-bound markets and improper parameter optimization need to be noted. In general, this is a strategy template with great application prospects.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Length|
|v_input_2|3|Filter|
|v_input_3|70|TopBand|
|v_input_4|-70|LowBand|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-11 00:00:00
end: 2023-12-11 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 02/03/2017
// This indicator plots a CMO which ignores price changes which are less 
// than a threshold value. CMO was developed by Tushar Chande. A scientist, 
// an inventor, and a respected trading system developer, Mr. Chande developed 
// the CMO to capture what he calls "pure momentum". For more definitive 
// information on the CMO and other indicators we recommend the book The New 
// Technical Trader by Tushar Chande and Stanley Kroll.
// The CMO is closely related to, yet unique from, other momentum oriented 
// indicators such as Relative Strength Index, Stochastic, Rate-of-Change, etc. 
// It is most closely related to Welles Wilder`s RSI, yet it differs in several ways:
// - It uses data for both up days and down days in the numerator, thereby directly 
// measuring momentum;
// - The calculations are applied on unsmoothed data. Therefore, short-term extreme 
// movements in price are not hidden. Once calculated, smoothing can be applied to the 
// CMO, if desired;
// - The scale is bounded between +100 and -100, thereby allowing you to clearly see 
// changes in net momentum using the 0 level. The bounded scale also allows you to 
// conveniently compare values across different securities.
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
fFilter(xSeriesSum, xSeriesV, Filter) =>
    iff(xSeriesV > Filter, xSeriesSum, 0)

strategy(title="CMOfilt", shorttitle="CMOfilt")
Length = input(9, minval=1)
Filter = input(3, minval=1)
TopBand = input(70, minval=1)
LowBand = input(-70, maxval=-1)
reverse = input(false, title="Trade reverse")
hline(0, color=gray, linestyle=line)
hline(TopBand, color=red, linestyle=line)
hline(LowBand, color=green, linestyle=line)
xMom = close - close[1]
xMomAbs = abs(close - close[1])
xMomFilter = fFilter(xMom, xMomAbs, Filter)
xMomAbsFilter = fFilter(xMomAbs,xMomAbs, Filter)
nSum = sum(xMomFilter, Length)
nAbsSum = sum(xMomAbsFilter, Length)
nRes =   100 * nSum / nAbsSum
pos = iff(nRes > TopBand, 1,
	     iff(nRes < LowBand, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1 )
    strategy.entry("Long", strategy.long)
if (possig == -1 )
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=blue, title="CMOfilt")

```

> Detail

https://www.fmz.com/strategy/435105

> Last Modified

2023-12-12 12:35:05
