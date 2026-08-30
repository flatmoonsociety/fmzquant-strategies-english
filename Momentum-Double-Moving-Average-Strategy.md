
> Name

Momentum-Double-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c6522bbb85a800484c.png)
[trans]


## Overview
This strategy uses the momentum double moving average crossover method to achieve low risk trading. It uses two moving averages of different periods, the fast line and the slow line, to judge the timing of buying and selling based on their intersection. This strategy aims to capture changes in trends and obtain long-term profits in the general trend.
## Strategy Principle
This strategy uses the intersection of the WMA fast line and the WMA slow line to determine buy and sell signals. The fast line period is half the slow line period. When the fast line crosses the slow line from below, a buy signal is generated; when the fast line crosses the slow line from above, a sell signal is generated. To filter out false signals, it also introduces a moving average momentum difference indicator. Only when the fast and slow lines cross and the indicator meets the form requirements will a trading signal be generated.
Specifically, the key logic in the strategy is:
1. Define prices and parameters: extract OHLC price data; define parameters HullMA period z and price data p.
2. Calculate double moving average: calculate 2-period moving average n2ma and z-period moving average nma.
3. Calculate the difference between moving averages: calculate the difference between two moving averages.
4. Calculate the momentum indicator: calculate the sqn period moving average n1, n2, n3 of the moving average difference.
5. Judgment of crossover: When n1 crosses n2, it is marked green, otherwise it is marked red.
6. Draw the pattern: draw the graphics of n1 and n2.
7. Determine the signal: A signal is generated when the three momentum moving averages n1, n2, and n3 cross in the same direction.
8. Entry and exit: go long when the fast line crosses the slow line and the momentum indicator meets the requirements; go short when the fast line crosses below the slow line and the momentum indicator meets the requirements.
## Strategic Advantages
This strategy combines double moving average crossovers and momentum indicators, which can effectively filter out false signals and only generate trading signals when the trend changes begin, thereby achieving better strategic effects.
1. The intersection of fast and slow lines can determine the timing of trend changes and use the trend to gain profits.
2. Adding momentum indicators can filter out false signals and avoid being misled by the short-term rise and fall of the market.
3. Only trade when the general trend changes to reduce unnecessary trading frequency.
4. Using the moving average period after parameter optimization can make the indicator more consistent with the characteristics of different varieties.
5. Allowing a certain degree of pyreming can stretch the profit cycle.
## Strategy Risk
There are also some risks to be aware of with this strategy:
1. Double moving average crossovers lag behind the judgment of trend changes and may miss the best opportunity for price changes.
2. Improper setting of momentum indicator parameters may be misleading for trading.
3. There is a certain imbalance in the holding time of long and short positions.
4. The strategy does not have a good handling mechanism for market fluctuations.
5. There is a certain risk of over-optimization, and parameters need to be optimized step by step.
Solutions to corresponding risks include:
1. You can consider adding other leading indicators to judge price changes and prepare in advance.
2. The momentum indicator parameters should be appropriately optimized to find the best parameter combination.
3. Consider adding a volatility indicator to help control position time.
4. The position size can be appropriately limited to reduce single losses.
5. Parameter robustness testing should be performed to avoid over-optimization problems.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Try different types of moving average indicators to find the optimal parameters for the variety.
2. Test and add other auxiliary indicators, such as MACD, Bollinger Bands, etc. to identify trend changes.
3. Optimize the timing of entry and accurately determine the starting point of price reversal.
4. Optimize the timing of exits and use trailing stop loss and other methods to lock in profits.
5. Optimize parameters according to the characteristics of different varieties.
6. Use machine learning methods to find the optimal parameter combination.
7. Build a dynamic position management mechanism to control risks.
8. Add quantitative strategy evaluation indicators, such as Sharpe ratio, profit-loss ratio, etc.
9. Use the backtesting engine to evaluate the performance of the strategy on historical data.
## Summarize
To sum up, this momentum double moving average strategy uses moving average crossovers and momentum indicators to determine the turning point of the general trend, which can effectively filter out noise and achieve low-risk transactions. It has the advantages of stable profits and simple implementation, but also has some problems in parameter optimization and risk control. We can make improvements from optimizing the timing of entry and exit, dynamic position management, etc., to make the strategy more adaptable to the characteristics of the market. Adequate verification and rigorous evaluation are key to ensuring the effectiveness of the strategy. In short, this strategy provides a simple and effective idea for quantitative trading, but it requires continuous optimization and verification to generate stable investment returns.
||

## Overview

This strategy uses the momentum double moving average crossover method to implement low risk trading. It utilizes two moving averages of different periods, a fast line and a slow line, to determine entry and exit signals based on their crossover. The goal of this strategy is to capture trend changes and generate long-term profits during major trends.

## Strategy Logic

The strategy generates trading signals based on the crossover of a fast WMA line and a slow WMA line. The period of the fast line is half of the slow line's period. A buy signal is generated when the fast line crosses above the slow line from below. A sell signal is generated when the fast line crosses below the slow line from above. To filter out false signals, it also incorporates a momentum indicator based on the difference between two moving averages. A trade signal is only generated when the MA crossover occurs concurrently with the momentum indicator fulfilling shape requirements.

Specifically, the key logic includes:

1. Define price input and parameters: get OHLC price data; define parameters HullMA period z, price data p.

2. Calculate dual MAs: compute 2-period MA n2ma, z-period MA nma.

3. Compute MA difference: calculate difference between two MAs diff.  

4. Compute momentum indicator: calculate moving average of diff - n1, n2, n3 with period sqn.

5. Determine crossover: mark n1 above n2 as green, otherwise red. 

6. Plot shapes: plot n1 and n2.

7. Identify signals: generate signal when n1, n2, n3 align in same direction. 

8. Enter and exit: go long when fast line above slow line and momentum indicator agrees; go short when fast line below slow line and momentum indicator agrees.

## Advantages

Combining dual MA crossover and momentum indicator, this strategy can effectively filter out false signals and only generate trades at the start of trend changes, thus producing good strategy performance.

1. MA crossover detects changes in trend, profiting from trends.

2. Momentum indicator filters out false signals, avoiding being misled by short-term fluctuations.

3. Only trading on major trend changes reduces unnecessary trading frequency.

4. Parameter optimization fits the characteristics of different products. 

5. Allowing some degree of pyramiding stretches out profit cycles.

## Risks

There are also some risks to be aware of:

1. Dual MA crossover has lag in detecting trend changes, potentially missing best timing.

2. Improper parameter settings on momentum indicator may generate bad signals. 

3. Imbalance exists between long and short holding periods.

4. The strategy lacks mechanisms to handle choppy market conditions well.  

5. Risk of over-optimization exists, requiring stepwise optimization of parameters.

Some solutions:

1. Consider adding other leading indicators to detect price changes early.

2. Optimize parameters of momentum indicator to find best combinations.

3. Add volatility indicator to control holding period.

4. Limit position sizing to reduce single loss.

5. Test for parameter robustness to avoid over-optimization.

## Improvement Directions

The strategy can be improved in the following aspects:

1. Test different types of MAs to find optimal parameters for each product.

2. Add other indicators like MACD, Bollinger Bands to determine trend changes.

3. Optimize entry timing to accurately determine turning points. 

4. Optimize exits using trailing stops to lock in profits.

5. Perform parameter optimization according to product characteristics. 

6. Employ machine learning to find optimal parameter combinations. 

7. Build dynamic position sizing mechanisms to control risks.

8. Add quantitative metrics like Sharpe ratio, profit factor for strategy evaluation.

9. Assess performance on historical data using backtesting engine.

## Summary

In summary, this momentum double MA strategy identifies major trend reversal points using MA crossover and momentum, enabling low-risk trading. It has advantages like stable profits and simple implementation, but also issues to improve like parameter optimization and risk control. We can refine areas like entry/exit timing, dynamic position sizing to better adapt to market conditions. Extensive validation and evaluation are critical for ensuring robust strategy performance. Overall, this strategy provides a simple yet effective approach to quantitative trading, but requires continuous optimizations and validations to generate consistent investment returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|60|HullMA cross|
|v_input_2_ohlc4|0|Price data: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-10 00:00:00
end: 2023-11-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
//OCTOPUS Indicator Strategy
strategy("FAVEL corp. Indicator Strategy", shorttitle="FAVEL corp. Monarch", overlay=true, default_qty_type=strategy.percent_of_equity, max_bars_back=420, default_qty_value=20, calc_on_order_fills= true, calc_on_every_tick=true, pyramiding=0)
z=input(defval=60,title="HullMA cross")
p=input(ohlc4,title="Price data")
n2ma=2*wma(p,round(z/2))
nma=wma(p,z)
diff=n2ma-nma
sqn=round(sqrt(z))
n2ma1=2*wma(p[1],round(z/2))
nma1=wma(p[1],z)
diff1=n2ma1-nma1
sqn1=round(sqrt(z))
n2ma2=2*wma(p[2],round(z/2))
nma2=wma(p[2],z)
diff2=n2ma2-nma2
sqn2=round(sqrt(z))
n1=wma(diff,sqn)
n2=wma(diff1,sqn)
n3=wma(diff2,sqn)
c=n1>n2?green:red
n1e=plot(n1, color=c, linewidth=1, offset=2)
n2e=plot(n2, color=c, linewidth=1, offset=2)
fill(n1e, n2e, color=c, transp=75)
plot(cross(n1, n2) ? n1 : na, style = circles,color=c, linewidth = 4)
closelong = p<p[1] and n1<n3
if (closelong)
    strategy.close("BUY")
closeshort = p>p[1] and n1>n3
if (closeshort)
    strategy.close("SELL")
longCondition = strategy.opentrades<1 and n1>n2 and p>p[1] and n1>n3
if (longCondition)
    strategy.entry("BUY",strategy.long)
shortCondition = strategy.opentrades<1 and n1<n2 and p<p[1] and n1<n3
if (shortCondition)
    strategy.entry("SELL",strategy.short)
```

> Detail

https://www.fmz.com/strategy/432419

> Last Modified

2023-11-17 17:00:32
