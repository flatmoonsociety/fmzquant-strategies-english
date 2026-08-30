
> Name

DEMA Fast Double Exponential Moving Average StrategyDEMA-Double-Exponential-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The DEMA fast double exponential moving average strategy is a short-term trading strategy based on DEMA (double exponential moving average). This strategy combines the smoothness of the moving average and the quick response advantage of the EMA, aiming to use the intersection of the DEMA line to capture short-term price trends and achieve profits.
## Strategy Principle
This strategy mainly relies on the golden cross and dead cross of DEMA fast line and DEMA slow line to judge buy and sell signals.
Specifically, the formula for calculating the express line is:
`demaFast = 2 * ema(close, fastPeriod) - ema(ema(close, fastPeriod), fastPeriod)`

The calculation formula for the slow line is:
`demaSlow = 2 * ema(close, slowPeriod) - ema(ema(close, slowPeriod), slowPeriod)`

Among them, fastPeriod and slowPeriod represent the parameter periods of the fast line and the slow line respectively.
When the fast line crosses the slow line, a buy signal is generated, and when the fast line crosses below the slow line, a sell signal is generated.
```python
buy = crossover(demaSlow, demaFast)  
sell = crossunder(demaSlow, demaFast)
```

This strategy determines the specific trading direction based on the intersection of the DEMA line.
## Advantage Analysis
Compared with traditional moving averages, DEMA lines are more sensitive and can respond faster to price changes. This allows the strategy to capture more short-term trading opportunities.
In addition, the DEMA line also combines the smoothing characteristics of the moving average, which can filter out some market noise and avoid generating false signals.
In addition, this strategy uses a combination of fast and slow lines, which can avoid virtual crossovers to a certain extent. The fast line and slow line parameter settings are different, and the cross signal is more reliable.
Therefore, the DEMA fast double exponential moving average strategy overall has the advantages of fast response, filtering noise, and stable and reliable signals.
## Risk Analysis
Although the DEMA line is more stable than the EMA line, there is still the risk of a virtual crossover, resulting in false signals. For this point, the period parameters of the fast and slow lines can be appropriately adjusted to ensure that the fast line is sensitive enough and the slow line is stable enough.
In addition, as a short-term trading strategy, it is more sensitive to transaction costs. If the transaction frequency is too high or the volume of each transaction is set too small, transaction costs may have a certain impact on profits. Therefore, it is necessary to set transaction parameters reasonably and control costs.
Finally, any technical indicator strategy cannot completely avoid stop loss situations, and it needs to be combined with reasonable fund management to control risks.
## Optimization direction
This strategy still has room for optimization:
1. You can test different combinations of period parameters to find the best parameter combination.
2. You can add other technical indicators to confirm trading signals, such as RSI, etc., to avoid the occurrence of false signals.
3. Can be optimized for stop loss situations. For example, set a trailing stop to lock in profits, etc.
4. Fund management strategies can be optimized, such as adjusting trading volume based on account funds or introducing volatility to adjust positions.
## Summarize
The DEMA fast double exponential moving average strategy is generally a relatively stable short-term trading strategy. It has fast response speed and also has certain smooth filtering capabilities. Compared with indicators such as SMA, this strategy can capture more short-term opportunities. Through parameter optimization and supporting measures, the stability and profitability of strategy earnings can be further improved. Generally speaking, this strategy is suitable for investors who have needs for high-frequency short-term trading.

|| 


## Overview

The DEMA double exponential moving average strategy is a short-term trading strategy based on the DEMA (Double Exponential Moving Average). It combines the smoothness of moving averages and the fast response of EMAs, aiming to capture short-term price trends and generate profits by trading on DEMA crossovers.

## Strategy Logic

The strategy mainly relies on golden crosses and death crosses between the DEMA fast line and DEMA slow line to determine buy and sell signals. 

Specifically, the fast line is calculated as:

`demaFast = 2 * ema(close, fastPeriod) - ema(ema(close, fastPeriod), fastPeriod)`

And the slow line is:

`demaSlow = 2 * ema(close, slowPeriod) - ema(ema(close, slowPeriod), slowPeriod)`

Where fastPeriod and slowPeriod represent the periods of the fast and slow line respectively.

When the fast line crosses above the slow line, a buy signal is generated. When the fast line crosses below the slow line, a sell signal is generated.

```python
buy = crossover(demaSlow, demaFast)
sell = crossunder(demaSlow, demaFast) 
```

The strategy determines the trading direction based on DEMA line crossovers.

## Advantage Analysis

Compared to traditional moving averages, DEMA lines are more sensitive and can react to price changes faster. This allows the strategy to capture more short-term trading opportunities.

Also, DEMA lines incorporate the smoothness of moving averages, which helps filter out some market noise and avoid false signals.

In addition, the fast and slow line combo avoids false crossovers to some extent. With different parameter settings, crossovers are more reliable.

In summary, the DEMA double exponential moving average strategy has the advantages of fast response, noise filtering, and stable reliable signals.

## Risk Analysis

Although more stable than EMAs, DEMA lines can still suffer from false crossovers, generating incorrect signals. This can be addressed by fine tuning the period parameters of the fast and slow line to ensure enough sensitivity and stability.

Also, as a short-term strategy, it is sensitive to trading costs. High trading frequency or small trade sizing may erode profits. Reasonable trade parameters should be set to control costs.

Lastly, no technical indicator strategy can completely avoid stop loss. Proper risk management should be implemented to limit downside. 

## Optimization Directions 

There are still rooms for optimization:

1. Test different period combinations to find the optimal parameters.

2. Incorporate other indicators like RSI to confirm signals and avoid false signals. 

3. Optimize stop loss mechanisms, like trailing stop loss to lock in profits.

4. Optimize capital management, like position sizing based on account size, or volatility adjusted sizing.

## Conclusion

The DEMA double exponential moving average strategy is overall a stable short-term trading strategy. It has fast response and smoothing capabilities. Compared to SMAs, it can capture more short-term opportunities. With parameter tuning and proper mechanisms, the strategy's profitability and stability can be further improved. It suits investors who desire high-frequency short-term trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|32|DEMA FAST Period|
|v_input_2|2|DEMA SLOW Period|
|v_input_3|120|Resolution  - not lower than chart|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-19 00:00:00
end: 2023-09-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

strategy(title = "DEMA Strategy", shorttitle = "DEMA Strategy",initial_capital=1000, commission_value=0.2, commission_type =strategy.commission.percent, default_qty_value=100 , overlay = false, pyramiding=10, default_qty_type=strategy.percent_of_equity)
//@Moneros 2017
//Based on The DEMA is a fast-acting moving average that is more responsive to market changes than a traditional moving average
// !!!!  IN ORDER TO AVOID REPAITING ISSUES !!!!
// !!!!  DO NOT VIEW IN LOWER RESOLUTIONS THAN res/2 PARAMETER  !!!!
// for example res = 120 view >= 60m  res = 60 view >= 30m
// the length of the DEMA sampling shouldn't be longer than a candle 



// Best profits tested on BTCUSD
//res = 105 slowPeriod = 2 fastPeriod = 32
//res = 125 slowPeriod = 3 fastPeriod = 21
//res = 120 slowPeriod = 2 fastPeriod = 32 
//res = 130 slowPeriod = 1 fastPeriod = 24 
//res = 40 slowPeriod = 4 fastPeriod = 93 
//res = 60 slowPeriod = 1 fastPeriod = 67 

fastPeriod    = input(defval = 32, title = "DEMA FAST Period", minval = 2)
slowPeriod = input(defval = 2, title = "DEMA SLOW Period", minval = 1)
res = input(title="Resolution  - not lower than chart", defval="120")


demaFast =  request.security(syminfo.tickerid, res, 2 * ta.ema(close, fastPeriod) - ta.ema(ta.ema(close, fastPeriod), fastPeriod)  )
demaSlow  = request.security(syminfo.tickerid,res, 2 * ta.ema(close, slowPeriod) - ta.ema(ta.ema(close, slowPeriod), slowPeriod)  )



plot(demaFast,color=color.red)
plot(demaSlow,color=color.lime)

buy = ta.crossover(demaSlow, demaFast)
sell = ta.crossunder(demaSlow, demaFast)


// value [1] for avoid repaiting bottom bars
bgcolor( buy[1] ? color.lime : na, transp=0)
bgcolor( sell[1] ? color.red : na, transp=0)


strategy.entry("BUY", strategy.long, 1, when = buy)
strategy.entry("SELL", strategy.short, 1, when = sell ) 



```

> Detail

https://www.fmz.com/strategy/427926

> Last Modified

2023-09-26 20:28:11
