
> Name

Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is designed based on the golden cross and dead cross principle of double moving averages. When the short-term moving average crosses the long-term moving average, go long; when the short-term moving average crosses below the long-term moving average, close the position. The strategy is simple and easy to understand, suitable for novices to learn.
## Strategy Principle
This strategy is mainly based on two moving average indicators, sma(close, 14) and sma(close, 28).
First define the long and short moving averages:
```pine
short_ma = sma(close, 14)
long_ma = sma(close, 28)
```

Then judge the entry and exit according to the golden cross and dead cross:
```pine  
longCondition = crossover(short_ma, long_ma)
shortCondition = crossunder(short_ma, long_ma)
```

Go long when the short-term moving average crosses the long-term moving average:
```pine
strategy.entry("Buy", strategy.long, when = longCondition) 
```

Close the position when the short-term moving average crosses below the long-term moving average:
```pine
strategy.close_all(when = shortCondition)
```

The principle of this strategy is simple and clear. It uses the golden cross of the double moving average to judge, and has certain trend tracking capabilities.
## Advantage Analysis
- The principles of the strategy are simple and easy to understand, and even novices can use them easily
- Use the golden cross and dead cross of the moving average to determine the trend, and have certain trend tracking capabilities
- You can customize the moving average period and optimize strategy parameters
- Stop loss points can be set to control single losses
## Risk Analysis
- The dual moving average strategy is sensitive to market fluctuations and may result in multiple losing transactions.
- The moving average is lagging and may miss the price reversal point
- Positions established close to moving average intersections are likely to be locked up
- It is necessary to optimize the moving average cycle parameters, and the effects of different cycles may be different.
- Unable to stop losses quickly when trends change violently
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the moving average cycle parameters and find the best parameter combination
You can try different short-term and long-term moving average cycles to find the best combination. For example, (5, 10), (10, 20), (20, 60) and other parameter comparison tests.
2. Add filtering conditions to avoid false signals
Filter conditions such as trading volume and spread can be added when the moving average crosses to avoid excessive transactions in a volatile market.
3. Add stop loss strategy
Set a stop loss point or use the moving average as a stop loss line to control single losses.
4. Combined with other indicators
You can add MACD, KDJ and other auxiliary indicators for combined trading to improve the strategy effect.
5. Optimize entry points
Find better entry points near the moving average rather than establishing positions close to the moving average. For example, enter the market at a point where the moving average deviates.
## Summarize
The concept of the double moving average strategy is simple and easy for novices to use. However, this strategy is sensitive to market fluctuations and involves a certain risk of loss. We can improve the strategy effect by optimizing parameters, adding filter conditions, setting stop losses, and adding other indicators. In strong trends, this strategy can achieve good results. However, during periods of market volatility, it is recommended to use caution or stop losses to control risks.
[/trans]

||


## Overview

This strategy is designed based on the golden cross and death cross of dual moving averages. It goes long when the short period moving average crosses above the long period moving average, and closes position when the short period moving average crosses below the long period moving average. The strategy is simple and easy to understand, suitable for beginners to learn.

## Strategy Logic

The strategy is mainly based on the sma(close, 14) and sma(close, 28) indicators. 

First define the short and long moving averages:

```pine
short_ma = sma(close, 14)  
long_ma = sma(close, 28)
```

Then determine entry and exit based on golden cross and death cross:

```pine
longCondition = crossover(short_ma, long_ma)
shortCondition = crossunder(short_ma, long_ma) 
```

Go long when the short MA crosses above the long MA:

```pine
strategy.entry("Buy", strategy.long, when = longCondition)
```

Close position when the short MA crosses below the long MA:

```pine
strategy.close_all(when = shortCondition) 
```

The logic is simple and clear, utilizing the crossovers of dual MAs to determine entries and exits. It has some trend following capacity.


## Advantage Analysis 

- Simple logic, easy for beginners to use
- Utilizes MA crossovers to determine trends
- Customizable MA periods for parameter optimization
- Allows stop loss to control single trade loss

## Risk Analysis

- Sensitive to market fluctuation, may generate multiple losing trades
- Lagging nature of MAs, may miss price reversal points
- Prone to being trapped near MA crossover points
- Need to optimize MA periods, different periods may lead to different results
- Unable to quickly cut loss when trend changes violently

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize MA periods to find the best combination

Test different short and long MA periods, such as (5, 10), (10, 20), (20, 60) etc to find the optimal combination.

2. Add filters to avoid false signals 

Add filters like trading volume, price gap etc. near MA crossovers to avoid excessive trades in ranging markets.

3. Incorporate stop loss 

Set stop loss price or use MA as stop loss line to control single trade loss.

4. Combine with other indicators

Add auxiliary indicators like MACD, KDJ etc. to improve strategy performance. 

5. Optimize entry points

Find better entry points near MAs instead of entering right at the crossover. For example, enter on MA divergence points.

## Summary

The dual MA strategy is simple for beginners to use. But it is sensitive to market fluctuations and has risks of losses. We can improve it by optimizing parameters, adding filters, incorporating stop loss, combining other indicators etc. It can perform well in strong trends but should be used with caution or proper stop loss in ranging markets.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.6|minGainPercent|
|v_input_2|true|avg_protection|
|v_input_3|true|gain_protection|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=2
// strategy("Tester", pyramiding = 50, default_qty_type = strategy.cash, default_qty_value = 20, initial_capital = 2000, commission_type = strategy.commission.percent, commission_value = 0.25)

minGainPercent = input(0.6)
gainMultiplier = minGainPercent * 0.01 + 1


longCondition = crossover(sma(close, 14), sma(close, 28))
shortCondition = crossunder(sma(close, 14), sma(close, 28))


avg_protection = input(1)
gain_protection = input(1)


strategy.entry("Buy", strategy.long, when = longCondition    and (avg_protection >= 1 ? (na(strategy.position_avg_price) ? true : close <= strategy.position_avg_price) : true))
strategy.close_all(when = shortCondition  and (gain_protection >=1 ? (close >= gainMultiplier * strategy.position_avg_price) : true))
```

> Detail

https://www.fmz.com/strategy/427487

> Last Modified

2023-09-21 16:40:01
