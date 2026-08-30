
> Name

Moving-Average-Aggregation-Williams-Commercial-Bid-Ask-Pressure-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/23ff6e6f3823645d009310f8ce4e06b0597742a707f660c69227de1c6bf860f2.png)
[trans]

The main idea of ​​this strategy is to use the Williams Business District buying and selling pressure indicator to determine the accumulation and distribution stages of the market, in order to discover the divergence between the price and the Williams indicator, thereby generating trading signals. When safe assets reach new highs but the Williams indicator does not hit new highs, it represents allocation by game participants and should be sold; when safe assets hit new lows but the Williams indicator does not hit new lows, it represents accumulation by game participants and should be bought.
The principles of the strategy are detailed below:
This strategy is based on the Williams Business District buying and selling pressure indicator, which reflects the buying and selling pressure in the market and determines whether the market is controlled by buyers or sellers. The Williams indicator determines price accumulation and distribution by calculating the closing price, highest price, and lowest price. When the price hits a new high but the Williams indicator does not hit a new high, it represents distribution and you should sell; when the price hits a new low but the Williams indicator does not hit a new low, it means accumulation and you should buy.
This strategy uses the Williams indicator to judge the accumulation and distribution of the market to discover price divergences and generate trading signals. At the same time, use the moving average to smooth the Williams indicator to avoid false signals. When the Williams indicator is above its moving average, it is the accumulation phase; when it is below its moving average, it is the distribution phase. When a divergence is found, if it is a long position, it will be sold in the distribution stage and bought in the accumulation stage; if it is a short position, the opposite will be done.
The main advantages of this strategy are:
1. Able to accurately judge the buying and selling pressure of the market and capture the turning point of the price trend.
2. Use moving averages to smooth the indicator curve to avoid generating false signals.
3. The rules are clear and easy to understand and implement.
4. Parameters can be flexibly adjusted to suit different market environments.
The main risks and solutions are as follows:
1. The Williams indicator may produce false signals, and moving averages can alleviate this problem to a certain extent.
2. If parameters are set improperly, price changes may be missed or false signals may be generated. Parameters should be adjusted to suit different cycles.
3. Pay attention to the impact of emergencies on prices and suspend trading plans if necessary.
The main optimization directions of this strategy are:
1. Test more parameter combinations to find the best parameters.
2. Add other technical indicators for combination to improve signal accuracy.
3. Add stop-loss strategies to reduce single losses.
4. Optimize the timing of entry and enter after the trend becomes clearer.
In general, this strategy uses the Williams Business District buying and selling pressure indicator to judge the willingness of market game participants, and then combines it with the moving average to find price divergence, thereby generating trading signals. This strategy is easy to understand and implement. It can be applied to different markets by adjusting parameters and can also be optimized in many aspects. It is worthy of in-depth study and application.
|| 

The main idea of this strategy is to use the Williams Commercial Bid-Ask Pressure Indicator to judge the accumulation and distribution stages of the market, so as to discover the divergence between price and Williams Indicator and generate trading signals. When the security reaches a new high but the Williams Indicator does not reach a new high, it represents distribution by game participants and should sell. When the security reaches a new low but the Williams Indicator does not reach a new low, it represents accumulation by game participants and should buy.

The strategy principle is described in detail as follows:

This strategy is based on the Williams Commercial Bid-Ask Pressure Indicator, which reflects the buying and selling pressure in the market and judges whether the market is controlled by buyers or sellers. The Williams Indicator calculates the accumulation and distribution of prices based on the closing price, highest price and lowest price. When the price reaches a new high but the Williams Indicator does not reach a new high, it represents distribution and should sell. When the price reaches a new low but the Williams Indicator does not reach a new low, it represents accumulation and should buy.

This strategy uses the Williams Indicator to judge the accumulation and distribution of the market in order to discover price divergence and generate trading signals. At the same time, it uses moving averages to smooth the Williams Indicator to avoid false signals. When the Williams Indicator is above its moving average, it is in an accumulation stage. When below the moving average, it is in a distribution stage. When divergence occurs, go long in accumulation stage and go short in distribution stage. 

The main advantages of this strategy are:

1. Accurately judge the buying and selling pressure in the market and capture inflection points of price trends.

2. Use moving averages to smooth the indicator curve and avoid false signals. 

3. The rules are clear and easy to understand and implement.

4. Flexible parameter adjustment adaptable to different market environments.

The main risks and solutions are:

1. Williams Indicator may generate false signals. Moving averages can alleviate this to some extent.

2. Improper parameter settings may miss price reversals or generate false signals. Parameters should be adjusted to adapt to different cycles.

3. Pay attention to the impact of sudden events on prices and suspend trading plans if necessary.

The main directions for optimizing this strategy are:

1. Test more parameter combinations to find the optimal parameters.  

2. Add other technical indicators for combination to improve signal accuracy.

3. Add stop loss strategies to reduce single loss.

4. Optimize entry timing to enter after trend becomes more obvious.

In summary, this strategy uses the Williams Commercial Bid-Ask Pressure Indicator to judge the willingness of market participants, combined with moving averages to discover price divergence, thus generating trading signals. This strategy is easy to understand and implement, adaptable to different markets through parameter adjustment, and can be optimized in many ways, worth in-depth research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-01 00:00:00
end: 2023-11-30 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 23/01/2018
// Accumulation is a term used to describe a market controlled by buyers;
// whereas distribution is defined by a market controlled by sellers.
// Williams recommends trading this indicator based on divergences:
//
//  Distribution of the security is indicated when the security is making 
//  a new high and the A/D indicator is failing to make a new high. Sell.
//
//  Accumulation of the security is indicated when the security is making 
//  a new low and the A/D indicator is failing to make a new low. Buy.
//
//You can change long to short in the Input Settings
//WARNING:
//- For purpose educate only
//- This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Smoothened Williams Accumulation/Distribution (Williams AD)", shorttitle="Williams AD")
Length = input(14, step = 1)
reverse = input(false, title="Trade reverse")
hline(0, color=blue, linestyle=line)
xPrice = close
xWAD = iff(close > nz(close[1], 0), nz(xWAD[1],0) + close - low[1], 
         iff(close < nz(close[1],0), nz(xWAD[1],0) + close - high[1],0))
xWADMA = sma(xWAD, Length)
pos = iff(xWAD > xWADMA, 1,
       iff(xWAD < xWADMA, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )           
plot(xWAD, color=green, title="Williams AD")
plot(xWADMA, color=red, title="MA(AD)")
```

> Detail

https://www.fmz.com/strategy/434609

> Last Modified

2023-12-07 17:48:42
