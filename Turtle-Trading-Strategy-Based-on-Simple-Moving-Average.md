
> Name

Turtle-Trading-Strategy-Based-on-Simple-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/bc85af93f4b46d790f.png)
[trans]

## Overview
This strategy achieves profits by calculating two sets of simple moving averages with different parameters and using them as signals for opening and closing positions. This strategy was first proposed by American trader Richard Dennis in 1983 and relied on simple rules to achieve stable profits. It was later further promoted by Curtis Faith and is widely known.
## Strategy Principle
This strategy calculates two sets of fast and slow lines simultaneously. The fast line parameters are set to a position opening period of 20 days and a position closing period of 10 days; the slow line parameters are a position opening period of 55 days and a position closing period of 20 days. When the price crosses the highest value of the fast line's position building period, a long order signal is triggered; when the price falls below the lowest value of the position building period, a short order signal is triggered. In the same way, long orders are closed when the price goes below the lowest value of the closing period; short orders are closed when the price goes above the highest value of the closing period. The logic of opening and closing positions in the slow line is the same as that in the fast line.
This strategy relies on the moving average theory to achieve profits. That is, when the short-term average crosses the long-term average, it is regarded as a signal of rising prices; when it crosses below, it is a signal of falling prices. The fast and slow lines in this strategy play a similar role.
## Strategic Advantages
1. The rules are simple and clear, easy to understand and implement, and suitable for beginners to learn;
2. The standards for opening and closing positions are clear and frequent transactions are avoided;
3. Combining fast and slow dual moving averages can smooth the noise caused by price changes and generate clearer trading signals;
4. Using multiple sets of parameters to combine, you can control risks and prevent wrong transactions;
5. Long-term stable profitability has been verified in the real market.
## Risks and Solutions
1. The strategy itself is relatively mechanized, unable to make judgments on special market conditions, and has a certain profit upper limit;
   - You can try to introduce more indicators or models based on machine learning to assist decision-making
2. As a marker indicator, the moving average has a certain lag;
   - The cycle of opening and closing positions can be appropriately shortened
3. Unable to limit the maximum drawdown.
   - Stop loss points can be set
## Optimization direction
1. Add a stop loss module to control the maximum retracement
2. Combine with other indicators to filter signals
3. Dynamically adjust moving average parameters
4. Add a data processing module to eliminate the impact of abnormal data
5. Determine trends using machine learning models
## Summarize
This strategy is a typical trend following strategy. Rely on simple double moving averages to establish trading rules and obtain stable profits by tracking market trends. This strategy is easy to understand and implement, has clear signals for opening positions, and long-term real market verification of profits, making it very suitable for beginners to learn and research. It also lays the foundation for more complex quantitative trading. Through continuous optimization, better performance can be expected.
||


## Overview

This strategy generates profit by calculating two groups of simple moving averages with different parameters and using them as signals for opening and closing positions. The strategy was first proposed by American trader Richard Dennis in 1983. By following simple rules, it achieved steady profits and was further popularized by Curtis Faith, widely known as the "turtle trading strategy".

## Principles

The strategy simultaneously computes two groups of fast and slow lines. The fast line parameters are set to 20 days for opening positions and 10 days for closing positions. The slow line parameters are 55 days and 20 days respectively. When the price crosses above the highest value of the fast line's opening period, it triggers a long signal. When the price falls below the lowest value of the fast line's opening period, it triggers a short signal. Similarly, when the price falls below the lowest value of the fast line's closing period, it closes long positions. When the price breaks through the highest value of the fast line's closing period, it closes short positions. The slow line has the same logic for opening and closing positions as the fast line.

The strategy relies on the moving average theory to make profits. That is, when the short-term moving average crosses above the long-term one, it is considered a bullish signal. When it crosses below, it signals a downward trend. The fast and slow lines in this strategy play similar roles.

## Advantages

1. Simple and clear rules, easy to understand and implement, suitable for beginners;  
2. Clear criteria for opening and closing positions, avoiding frequent trading;
3. Combining fast and slow dual moving averages smooths out price fluctuations and generates clearer trading signals;  
4. The use of multiple parameter sets helps control risks and prevents erroneous trades;
5. Steady profits in the long run, validated in live trading.

## Risks and Mitigations 

1. The strategy itself is mechanical and cannot make judgments about special market conditions, thus having profit limitations;
   - Attempt to incorporate more indicators or machine learning models to aid decision-making
2. Moving averages as lagging indicators have some latency;
   - Appropriately shorten the opening and closing periods
3. Unable to limit maximum drawdown.
   - Set stop-loss points

## Optimization Directions

1. Add stop-loss module to control maximum drawdown
2. Incorporate other indicators to filter signals
3. Dynamically adjust moving average parameters  
4. Add data processing module to eliminate impacts of abnormal data
5. Incorporate machine learning models to determine trends

## Summary

This is a typical trend-following strategy. By establishing trading rules based on simple dual moving averages and tracking market trends, it achieves steady profits. The strategy is easy to understand and implement with clear opening signals and long-term verified profits from live trading, making it very suitable for beginners to learn and research. It also lays the foundation for more complex quantitative trading. Further optimizations can lead to even better performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|enter_fast|
|v_input_2|10|exit_fast|
|v_input_3|55|enter_slow|
|v_input_4|20|exit_slow|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-28 00:00:00
end: 2023-12-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
//coded by tmr0
//original idea from «Way of the Turtle: The Secret Methods that Turned Ordinary People into Legendary Traders» (2007) CURTIS FAITH
strategy("20 years old Turtles strategy by tmr0", shorttitle = "Turtles", overlay=true)

enter_fast = input(20, minval=1)
exit_fast = input(10, minval=1)
enter_slow = input(55, minval=1)
exit_slow = input(20, minval=1)

fastL = highest(enter_fast)
fastLC = lowest(exit_fast)
fastS = lowest(enter_fast)
fastSC = highest(exit_fast)

slowL = highest(enter_slow)
slowLC = lowest(exit_slow)
slowS = lowest(enter_slow)
slowSC = highest(exit_slow)

enterL1 = high > fastL[1]
exitL1 = low <= fastLC[1]
enterS1 = low < fastS[1]
exitS1 = high >= fastSC[1]

enterL2 = high > slowL[1]
exitL2 = low <= slowLC[1]
enterS2 = low < slowS[1]
exitS2 = high >= slowSC[1]


//bgcolor(exitL1 or exitL2? red: enterL1 or enterL2? navy:white)

strategy.entry("fast L", strategy.long, when = enterL1)
strategy.entry("fast S", strategy.short, when = enterS1)
strategy.close("fast L", when = exitL1)
strategy.close("fast S", when = exitS1)

strategy.entry("slow L", strategy.long, when = enterL2)
strategy.entry("slow S", strategy.short, when = enterS2)
strategy.close("slow L", when = exitL2)
strategy.close("slow S", when = exitS2)
//zl=0
//z=strategy.netprofit / 37 * koef  //ежемесячная прибыль
//z=strategy.grossprofit/strategy.grossloss
//z1=plot (z, style=line, linewidth=3, color = z>zl?green:red, transp = 30)
//hline(zl, title="Zero", linewidth=1, color=gray, linestyle=dashed)
```

> Detail

https://www.fmz.com/strategy/437037

> Last Modified

2023-12-29 16:45:51
