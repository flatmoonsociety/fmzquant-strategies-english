
> Name

Dynamic-Position-Sizing-Quant-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1e3e3abce5fe52cebd8.png)
[trans]
## Overview
The core idea of ​​this strategy is to dynamically adjust the position size of each transaction based on account equity. It can automatically increase positions when making profits and reduce positions when losing money, thus achieving automatic amplification of the compound interest effect.
## Strategy Principle
This strategy achieves dynamic position adjustment through the following key steps:
1. Set parameters such as leverage ratio and maximum position as restrictions
2. Calculate the account equity divided by the leverage ratio to obtain the base position size
3. Compare the base position size and the maximum position setting, and take the minimum value between the two as the actual position
4. Adjust the position size to the calculated actual position when opening a position
5. The position size will be adjusted in real time based on changes in profit and loss amount and account equity.
The above steps ensure the rationality of the position size and avoid risks caused by excessive positions. At the same time, the position size is linked to the account equity and automatically amplifies with profits.
## Strategic Advantages
This strategy has several advantages:
1. Achieve dynamic adjustment of position size without manual intervention
2. The position size is linked to the account equity, which can automatically realize the compound interest effect.
3. Set leverage and maximum position as constraints to control risk exposure
4. The logic is clear and simple, easy to understand and secondary development
5. Easy to be embedded into other strategies and highly scalable
## Strategy Risk
There are also some risks with this strategy:
1. When the position is enlarged, the loss will also be enlarged, and there is a risk of missing the reversal opportunity.
2. The position size is linked to the account equity in real time, and may be adjusted too frequently under special market conditions.
3. Improper setting of the maximum position may lead to the risk of excess positions
4. Setting leverage too high can also lead to excessive concentration of risk
The above risks can be mitigated through reasonable parameter settings and appropriate reserved funds.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Add sliding point settings to make adjustments smoother
2. Optimize the calculation formula of position size and introduce other factors
3. Static locking of position sizes under specific market conditions
4. Set the minimum unit change amount for position adjustment to avoid too frequent adjustments
5. Add conditional judgment rules for position adjustment to prevent unnecessary adjustments
Through the above optimization points, the strategic behavior can be made more stable and controllable, and position size adjustments can be avoided to be too sensitive and frequent.
## Summarize
This strategy implements the dynamic adjustment function of positions based on account equity, which can automatically amplify the profit effect. It sets leverage and maximum position as risk control, and the logic is simple and clear, easy to understand and secondary development. We also analyzed the advantages, disadvantages and risks of the strategy, and gave some optimization suggestions. Overall, this strategy provides a flexible and easy-to-use idea for realizing automated compound interest trading.
||

## Overview

The core idea of this strategy is to dynamically adjust the position size of each trade based on account equity. It can automatically increase position size when profitable and decrease position size when losing, thereby achieving the automatic leverage effect of compounding.   

## Strategy Logic

The strategy achieves dynamic position sizing through the following key steps:

1. Set parameters like leverage ratio, max position size as constraints  
2. Calculate benchmark position size by dividing account equity by leverage ratio
3. Compare benchmark size with max size setting, take the smaller one as actual size  
4. Adjust position size to the calculated actual size when opening positions
5. Position size will change in real-time with PnL changes and account equity fluctuations

The above steps ensure reasonable position sizing, avoid over-leverage risks, while linking size to equity to achieve auto-compounding as profits increase.

## Advantages

The strategy has the following advantages:

1. Achieves dynamic position sizing without manual intervention  
2. Links position size to equity to achieve compounding effect automatically 
3. Sets leverage and max size as risk limits  
4. Simple and clear logic, easy to understand and customize
5. Easy to incorporate into other strategies, highly extensible    

## Risks

There are also some risks:

1. Magnified losses when position size increases, risk of missing reversals
2. Frequent adjustments in extreme market conditions due to real-time linkage to equity
3. Inappropriate max size setting can lead to over-leverage
4. Excessive leverage multiplying risks

Risks can be mitigated through prudent parameter settings, capital buffering etc.

## Enhancement Opportunities 

The strategy can be enhanced in the following ways:  

1. Add slippage to smooth adjustments
2. Optimize position sizing formula by incorporating other factors 
3. Statically lock sizes in specific market conditions
4. Set minimum step size for adjustments to avoid excessive changes
5. Add conditional rules to prevent unnecessary adjustments

The above enhancements can make the strategy behavior more stable and controllable, avoiding sensitivity and frequent position size changes.

## Conclusion   

The strategy achieves equity-based dynamic position sizing to automatically magnify profits. It sets leverage and max size as risk controls, with simple and clear logic for ease of understanding and customization. We also analyzed its pros and cons and risks, along with some optimization suggestions. Overall, it provides a flexible and practical approach to achieve automated compound growth in trading.  


[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10000|leverage|
|v_input_2|25|max position size|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of Tendies Heist LLC, 2021
//@version=4
strategy("Tendies Heist Auto Compounding Example", overlay=true)

    
leverage = input(10000)

maxps = input(25, "max position size")
strategy.risk.max_position_size(maxps)

balance = max(1,floor(strategy.equity / leverage))

o        = 1
ps       = true
size     = 0.
balance2 = size[1] < balance
balance3 = size[1] > balance
l        = balance3
w        = balance2

if ps
    size := w ? size[1]+o : l ? size[1]-o : nz(size[1],o)
if size > maxps
    size := maxps

longCondition = crossover(sma(close, 14), sma(close, 28))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long,qty=size)

shortCondition = crossunder(sma(close, 14), sma(close, 28))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short,qty=size)
```

> Detail

https://www.fmz.com/strategy/442381

> Last Modified

2024-02-21 14:52:10
