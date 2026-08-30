
> Name

Trend-Following-Strategy-Based-on-Hull-Moving-Average-and-True-Range
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14952cbb0a04ee6a4cf.png)
 [trans]

## Overview
The core idea of ​​this strategy is to combine the Hull moving average and true range (ATR) to identify the market trend direction, and enter the market after the trend direction is confirmed. Specifically, it calculates the difference between the Hull moving average within a certain period and the Hull moving average of the previous period. When the difference rises, it is judged to be a bullish trend, and when the difference falls, it is judged to be a bearish trend. At the same time, combine the ATR indicator to judge the amplitude, and choose to enter when the trend direction is confirmed and the amplitude continues to expand.
## Strategy Principle
This strategy is mainly based on two indicators: Hull moving average and ATR.
The Hull Moving Average is a trend-following indicator developed by American futures trader Alan Hull. The Hull moving average is similar to the moving average, but the Hull moving average has higher sensitivity and can capture price changes more quickly. An adjustable parameter hullLength is set in the strategy to control the period length of the Hull moving average. By calculating the difference between the Hull moving average of the current period and the previous period, the current price trend direction can be determined.
ATR stands for Average True Range, which is the true amplitude. It reflects the magnitude of daily price fluctuations. When volatility increases, the true volatility will increase; when volatility decreases, the true volatility will decrease. Parameters such as atrLength and atrSmoothing are set in the strategy to control the calculation method of ATR. And draw it on the chart as one of the entry indicators.
Specifically, the strategy logic is:
1. Calculate the Hull moving average currentHullMA of the current period (hullLength setting) and the Hull moving average previousHullMA of the previous period
2. Calculate the difference between the two hullDiff = currentHullMA - previousHullMA
3. When hullDiff > 0, it is judged to be a long trend; when hullDiff < 0, it is judged to be a short trend.
4. At the same time, calculate the ATR value of a certain period (atrLength setting) as the amplitude indicator of the trend
5. When it is judged to be a bull trend, and the ATR value is greater than price and price is greater than the price before atrLength period, go long; when it is judged to be a short trend, and the ATR value is less than price and price is less than the price before atrLength period, go short
6. Determine the closing signal by the positive or negative value of hullDiff
## Strategic advantage analysis
This strategy has the following advantages:
1. Combined with trend judgment and volatility indicators, you can choose to enter the market when the price trend is clear and volatility increases to avoid being trapped in a volatile market.
2. The Hull moving average is more responsive to price changes and can quickly determine the new trend direction.
3. ATR can reflect market volatility and enthusiasm, providing a basis for selecting entry time points.
4. There are many adjustable parameters, and the best parameter combination can be obtained through optimization.
## Risk Analysis
This strategy also has some risks:
1. Neither Hull moving average nor ATR can completely avoid the problem of false breakthroughs, and it is still possible to be trapped.
2. Improper parameter settings may lead to frequent transactions or insufficient sensitivity, thus affecting the strategy effect.  
3. Unable to effectively respond to violent market conditions, such as rapid rises, breakthroughs or plummets.
Corresponding solutions:
1. Set a loose stop loss appropriately to avoid being stuck by breakthroughs.
2. Optimize parameters through repeated testing to make the indicators more consistent with different market environments. 
3. When a violent market situation comes, suspend the strategy operation.
## Optimization direction
The optimization space of this strategy is still relatively large, and we can mainly start from the following aspects:
1. Test different Hull moving average cycle parameters to find the cycle setting that best suits the current market environment.
2. Test different combinations of ATR cycle parameters to find the cycle that best captures market enthusiasm.
3. Try different types of ATR smoothing methods (RMA, SMA, EMA, etc.) to see which method works best.  
4. Optimize the opening conditions, such as combining the combination of volatility indicators Reaction and ATR to judge the conditions.
5. Optimize the stop loss method and appropriately relax the stop loss range to avoid being trapped.
## Summarize
This strategy integrates the trend tracking ability of Hull moving average and the heat indicator judgment ability of ATR. While confirming the trend, it selects a volatile and positive time point to enter the market, which can filter out some invalid signals. The optimization of indicator parameters and the use of risk management methods can further enhance the effectiveness of the strategy. In general, this strategy combines multiple factors of trend tracking and popularity judgment, and can achieve better results when the parameters are adjusted and optimized in place.
||

## Overview

The core idea of this strategy is to identify market trend directions by combining Hull moving average and average true range (ATR), and enter positions after the trend direction is confirmed. Specifically, it calculates the difference between the Hull moving averages of a certain period and the previous period. When the difference rises, it indicates a bullish trend; when the difference declines, it indicates a bearish trend. At the same time, the ATR index is used to determine the amplitude. It enters positions when the trend direction is confirmed and the amplitude keeps expanding.

## Strategy Logic

This strategy mainly relies on two types of indicators: Hull moving average and ATR.

The Hull moving average is a trend-following indicator developed by American futures trader Alan Hull. Similar to moving averages, the Hull moving average has higher sensitivity and can capture price changes and trends faster. The strategy sets an adjustable parameter hullLength to control the period of the Hull moving average. By calculating the difference between the current period's Hull MA and previous period's, it determines the current price trend direction.

ATR stands for Average True Range. It reflects the amplitude of daily price fluctuations. When volatility increases, ATR rises; when volatility declines, ATR falls. The strategy sets parameters like atrLength and atrSmoothing to control the ATR calculation. And ATR is plotted on the chart as one reference for entries.

Specifically, the strategy logic is:  

1. Calculate current period Hull MA (hullLength) and previous period Hull MA. 
2. Calculate the difference: hullDiff = currentHullMA - previousHullMA
3. When hullDiff > 0, it indicates a bullish trend. When hullDiff < 0, it indicates a bearish trend.
4. Calculate ATR (atrLength) of a period as an amplitude benchmark.
5. When bullish trend is identified and ATR > price > price of atrLength periods ago, go long. When bearish and ATR < price < price of atrLength periods ago, go short.  
6. Use the positive/negative of hullDiff to determine close signals.

## Advantage Analysis 

The advantages of this strategy:

1. Combining trend judgment and volatility index, it can enter positions when price trend is clear and volatility rises to avoid whipsaws in range-bound markets.
2. Hull MA responds faster to price changes and can quickly identify new trend directions.
3. ATR reflects market volatility and heat, providing guidance for entry timings.  
4. Multiple adjustable parameters can be optimized for best parameter combinations.

## Risk Analysis

Some risks of this strategy:

1. Both Hull MA and ATR cannot completely avoid false breakouts and thus holds the risk of being trapped.
2. Improper parameter settings may lead to over-trading or insufficient sensitivity, undermining strategy efficacy. 
3. It cannot handle violent price actions like sharp spikes or crashes effectively.

Solutions:

1. Set proper stop loss to avoid being trapped by false breakouts.
2. Test and optimize parameters to fit different market environments.
3. Suspend strategy when facing violent volatility.  

## Optimization Directions 

There is still large room for optimization:

1. Test different hullLength parameters to find the optimal settings for current markets.
2. Test ATR period combinations to grasp market heat the best.  
3. Try different ATR smoothing methods to see which performs the best.
4. Optimize entry conditions with other volatility indicators like Reaction combined with ATR. 
5. Optimize stop loss to avoid being trapped.

## Conclusion

This strategy integrates the trend following capacity of Hull MA and the heat judgment ability of ATR. It enters positions when trend is confirmed and volatility rises to filter out some invalid signals. Further enhancement can be achieved by parameter optimization and better risk management. In summary, this strategy combines multiple factors of trend tracking and heat judgment. When parameters are fine-tuned, it can deliver good results.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Hull Length|
|v_input_2|50|ATR Length|
|v_input_3|0|ATR Smoothing: RMA|SMA|EMA|WMA|
|v_input_4_ohlc4|0|Price data: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-07 00:00:00
end: 2024-01-14 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//                                                Hull cross and ATR
strategy("Hull cross and ATR", shorttitle="H&ATR", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, calc_on_order_fills=true, calc_on_every_tick=true, pyramiding=0)
keh=input(title="Hull Length",defval=50)
length = input(title="ATR Length", defval=50, minval=1)
smoothing = input(title="ATR Smoothing", defval="RMA", options=["RMA", "SMA", "EMA", "WMA"])
p=input(ohlc4,title="Price data")
n2ma=2*wma(p,round(keh/2))
nma=wma(p,keh)
diff=n2ma-nma
sqn=round(sqrt(keh))
n2ma1=2*wma(p[1],round(keh/2))
nma1=wma(p[1],keh)
diff1=n2ma1-nma1
sqn1=round(sqrt(keh))
n1=wma(diff,sqn)
n2=wma(diff1,sqn)
ma_function(source, length) => 
    if smoothing == "RMA"
        rma(p, length)
    else
        if smoothing == "SMA"
            sma(p, length)
        else
            if smoothing == "EMA"
                ema(p, length)
            else
                wma(p, length)
plot(ma_function(tr(true), length), title = "ATR", color=black, transp=50)
closelong = n1<n2
if (closelong)
    strategy.close("buy")
closeshort = n1>n2
if (closeshort)
    strategy.close("sell")
if (ma_function(tr(true), length)<p and p>p[length] and n1>n2)
    strategy.entry("buy", strategy.long, comment="BUY")
if (ma_function(tr(true), length)>p and p<p[length] and n1<n2)
    strategy.entry("sell", strategy.short, comment="SELL")
```

> Detail

https://www.fmz.com/strategy/438824

> Last Modified

2024-01-15 15:26:08
