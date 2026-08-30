
> Name

Dual-Moving-Average-Crossover-Arrow-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/33058496ab104e2706.png)
[trans]


## Overview
This strategy determines when to buy and sell by calculating the double moving average crossover of the MACD indicator. It draws arrow shapes on the chart to prompt trading signals.
## Principle
This strategy first calculates the difference between the fast line (EMA 12 periods), the slow line (EMA 26 periods) and MACD. Then judge the buying and selling timing based on the golden cross and dead cross of the fast and slow lines and the positive and negative difference of MACD:
1. When the fast line crosses the slow line (golden cross) and the MACD difference crosses 0, it is a buy signal
2. When the fast line crosses the slow line (die cross) and the MACD difference crosses 0, it is a sell signal
In order to filter out false signals, the code also determines the signal condition of the previous K line. The current signal will be triggered only if the previous K-line is a reverse signal (buying turns into selling or selling turns into buying).
In addition, arrow graphics are also drawn in the code to indicate buying and selling opportunities on the K-line.
## Advantages
This strategy has the following advantages:
1. Use double moving average crossover judgment to effectively filter market noise and identify trends.
2. Combined with MACD difference judgment, you can avoid missing orders and misjudgment
3. Use arrows to indicate buying and selling opportunities, making operations more clear.
4. The rules are simple and clear, easy to understand and copy
## Risks and Solutions
There are also some risks with this strategy:
1. Double moving average crossovers can easily generate false signals, which may lead to over-trading. You can adjust the moving average parameters appropriately or add other filtering conditions to reduce false signals.
2. Unable to judge the fluctuations in the trend, losses may occur. This can be avoided by combining a trend indicator such as ADX
3. Fixed buying and selling conditions mechanize the strategy and cannot adapt to market changes. You can try adaptive methods such as machine learning to optimize
## Optimization direction
This strategy can be optimized from the following directions:
1. Test different parameter combinations to find the best fast line, slow line and MACD parameters
2. Add entry conditions, such as trading volume breakthrough to filter signals
3. Add a stop-loss mechanism to control single losses
4. Combine with volatility indicators such as VIX to determine risk appetite
5. Try machine learning models to replace fixed rules to achieve adaptive optimization of strategies
## Summarize
This double moving average cross arrow strategy is generally relatively simple and practical. Through double moving average cross judgment and MACD difference filtering, you can identify the buying and selling points in the medium and long-term trend to avoid missing the price turning point. Arrow tips also make operations clearer and clearer. In the later stage, the stability and profitability of the strategy can be further enhanced by optimizing parameters and adding filtering conditions.
|| 


## Overview  

This strategy identifies buying and selling signals by calculating the crossover of dual moving averages of the MACD indicator. It plots arrows on the chart to indicate trading signals.

## Principles  

The strategy first calculates the fast line (12-period EMA), slow line (26-period EMA) and MACD difference. It then determines long and short signals based on the crossover of the fast and slow lines, as well as the positive/negative value of the MACD difference:

1. When the fast line crosses above the slow line (golden cross) and the MACD difference crosses above 0, it is a buy signal
2. When the fast line crosses below the slow line (death cross) and the MACD difference crosses below 0, it is a sell signal

To filter out false signals, the code also checks the signal of the previous candlestick. The current signal is only triggered if the previous candlestick has an opposite signal (buy vs sell or vice versa).

In addition, arrow shapes are plotted on the chart to indicate buying and selling signals.  

## Advantages  

The advantages of this strategy include:

1. Using dual moving average crossover helps identify trends and filter out market noise  
2. Incorporating MACD difference avoids missing trades and false signals
3. Arrows clearly indicate entries and exits  
4. Simple and easy-to-understand rules facilitate replication  

## Risks and Solutions

Some risks of this strategy:

1. Crossovers may generate false signals and cause over-trading. Parameters can be adjusted or extra filters added to reduce fake signals.  
2. Unable to discern rangings in a trend, potentially leading to losses. Adding trend indicators like ADX can avoid this.
3. Fixed rules cannot adapt to changing markets. Machine learning can potentially optimize this.  

## Enhancement Opportunities

Some ways to improve the strategy:

1. Test different parameter combinations to find optimal settings for the fast line, slow line and MACD
2. Add extra entry conditions like volume breakouts to filter signals
3. Incorporate stop loss to control single trade loss  
4. Use volatility indicators like VIX to gauge risk appetite  
5. Try machine learning models instead of fixed rules to create adaptive optimization  

## Summary  

The dual moving average crossover arrow strategy is fairly simple and practical. By using crossover of two moving averages and MACD difference filtering, it identifies entries and exits during intermediate and long term trends, avoiding missing price reversals. The arrow signals also provide clear operation guidance. Further improvements in stability and profitability can be achieved through parameter tuning, extra filters and adaptive optimization.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-14 00:00:00
end: 2023-11-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Daniels stolen code
strategy(shorttitle="Daniels Stolen Code", title="Daniels Stolen Code", overlay=true, calc_on_order_fills=true, pyramiding=0)

//Define MACD Variables
fast = 12, slow = 26
fastMACD = ema(hlc3, fast)
slowMACD = ema(hlc3, slow)
macd = fastMACD - slowMACD
signal = sma(macd, 9)
hist = macd - signal
currMacd = hist[0]
prevMacd = hist[1]
currPrice = hl2[0]
prevPrice = hl2[1]

buy = currPrice > prevPrice and currMacd > prevMacd
sell = currPrice < prevPrice and currMacd < prevMacd
neutral = (currPrice < prevPrice and currMacd > prevMacd) or (currPrice > prevPrice and currMacd < prevMacd)
//Plot Arrows

timetobuy = buy==1 and (sell[1]==1 or (neutral[1]==1 and sell[2]==1) or (neutral[1]==1 and neutral[2]==1 and sell[3]==1) or (neutral[1]==1 and neutral[2]==1 and neutral[3]==1 and sell[4]==1) or (neutral[1]==1 and neutral[2]==1 and neutral[3]==1 and neutral[4]==1 and sell[5]==1) or (neutral[1]==1 and neutral[2]==1 and neutral[3]==1 and neutral[4]==1 and neutral[5]==1 and sell[6]==1))
timetosell = sell==1 and (buy[1]==1 or (neutral[1]==1 and buy[2]==1) or (neutral[1]==1 and neutral[2]==1 and buy[3]==1) or (neutral[1]==1 and neutral[2]==1 and neutral[3]==1 and buy[4]==1) or (neutral[1]==1 and neutral[2]==1 and neutral[3]==1 and neutral[4]==1 and buy[5]==1) or (neutral[1]==1 and neutral[2]==1 and neutral[3]==1 and neutral[4]==1 and neutral[5]==1 and buy[6]==1))

plotshape(timetobuy, color=blue, location=location.belowbar, style=shape.arrowup)
plotshape(timetosell, color=red, location=location.abovebar, style=shape.arrowdown)
//plotshape(neutral, color=black, location=location.belowbar, style=shape.circle)


//Test Strategy
// strategy.entry("long", true, 1, when = timetobuy and time > timestamp(2017, 01, 01, 01, 01)) // buy by market if current open great then previous high
// strategy.close("long", when = timetosell and time > timestamp(2017, 01, 01, 01, 01))

strategy.order("buy", true, 1, when=timetobuy==1 and time > timestamp(2019, 01, 01, 01, 01))
strategy.order("sell", false, 1, when=timetosell==1 and time > timestamp(2019, 01, 01, 01, 01))



// strategy.entry(id = "Short", long = false, when = enterShort())
// strategy.close(id = "Short", when = exitShort())

//strategy.entry("long", true, 1, when = open > high[1]) // enter long by market if current open great then previous high
// strategy.exit("exit", "long", profit = 10, loss = 5) // ge
```

> Detail

https://www.fmz.com/strategy/432805

> Last Modified

2023-11-21 17:00:49
