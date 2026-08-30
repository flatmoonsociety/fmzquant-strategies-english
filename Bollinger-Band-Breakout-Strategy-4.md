
> Name

Bollinger-Band-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/184e2fd7d9c4d59997a.png)
[trans]


## Overview
This strategy uses the Bolbringer Band indicator to determine market trends and combines bandwidth signals to find trading opportunities, aiming to sustain and stabilize the growth of the investment portfolio. According to last year's data backtest, the strategy's profitability reached 78.95%, and the maximum drawdown was only -4.02%. This is one of my series of automated strategies to help your portfolio grow steadily.
You are welcome to adjust parameters for backtesting, and you are also welcome to provide valuable opinions. If you are satisfied with the current results, you can turn it into learning and add alerts to automate your strategy. This requires adding an alert mechanism to the code. If this interests you, I can create related learning based on this strategy.
## Strategy Principle
This strategy uses Bolbolin bands and bandwidth to time entries and exits.
Bolbrin bands include upper, middle and lower lines. The midline is the n-day simple moving average, and the parameter n defaults to 16. The upper limit is the midline + k * standard deviation, the lower limit is the midline - k * standard deviation, and the parameter k defaults to 3. When the price is close to the upper limit, it means that the stock price is too high or overbought. When the price is close to the lower limit, it means that the stock price is too low or oversold.
The Bandwidth indicator shows price movement relative to the midline. It is calculated by (upper line - lower line)/middle line * 1000. When the bandwidth is lower than 20, it means the market is calm or consolidating; when the bandwidth exceeds 50, it means the fluctuations are increasing.
This strategy looks for opportunities to break through the lower limit to go long when the bandwidth is between 20-50. After going long, the take profit line is set to 108% of the opening price, or the stop loss is exited when the upper limit is exceeded.
## Advantage Analysis
This strategy has the following advantages:
1. Using Bolbolin bands to determine the market trend direction can reduce the risk of false breakthroughs.
2. Bandwidth signals can accurately locate volatile market conditions and avoid losses caused by large fluctuations.
3. Backtest data shows that a profit rate of nearly 80% can be obtained in one year, and the risk-return ratio is extremely high.
4. The maximum drawdown is less than 5%, which can effectively control risks and maintain stable growth of the portfolio.
5. The strategy logic is clear and simple, easy to understand and implement, and can be widely used in various digital assets
## Risk Analysis
This strategy also has the following risks:
1. Improper setting of Bolbolin band parameters may result in missing good trading opportunities.
2. When the market continues to be a mad bull or bear market, the trading frequency may be too low and profitability will be limited.
3. Insufficient backtest data, backtest indicators may not be replicated in actual applications
4. Under extreme market conditions, the stop loss point may be breached, resulting in large losses.
5. Excessive transaction fees will also reduce actual profits
Corresponding solutions:
1. Optimize parameters and adjust Bollinger Band cycles for different markets, etc.
2. Introduce other additional indicators to judge trends and respond to abnormal market conditions
3. Collect sufficient data to conduct multiple market backtests to verify the stability of the strategy
4. Adjust the stop loss point appropriately to prevent huge losses in extreme market conditions
5. Choose a trading platform with low handling fees to reduce transaction fees
## Optimization direction
This strategy can be optimized from the following aspects:
1. Bring in volume confirmation to avoid false breakouts
2. Combine with trend indicators to identify trend direction Combine with trend indicators to identify trend direction
3. Use machine learning to tune parameters and auto-adapt to market Use machine learning to tune parameters and auto-adapt to market
4. Add correlation filter to avoid trading uncorrelated assets
5. Optimize take profit/stop loss for more gains during uptrends Optimize take profit/stop loss for more gains during uptrends
6. Introduce more condition filters to increase win rate
7. Test multi-timeframe combinations to profit from multiple cycles Test multi-timeframe combinations to profit from multiple cycles
8. Build indexed portfolio to expand exposure
9. Use machine learning to auto generate & validate new strategies Use machine learning to auto generate & validate new strategies
## Summarize
The overall backtesting effect of this Bolbrin shock breakthrough strategy is good, and it can obtain relatively stable returns in a volatile market. The core ideas of the strategy are simple and clear, easy to master and apply. However, parameter optimization, risk control and portfolio management need to be further improved to achieve stable profits in a complex and ever-changing market. This strategy is a basic trend following strategy, on which more technical indicators and risk control mechanisms can be introduced for optimization, and it can also be combined with machine learning to achieve automated management. Overall, this strategy opens the door to quantitative trading for beginners and provides professionals with the possibility of strategy optimization.
|| 


## Overview

This strategy uses Bollinger Bands to gauge market trend and combines bandwidth signal to identify trading opportunities, aiming for steady growth of the investment portfolio. Backtested with previous year's data, it achieved 78.95% profitability with maximum drawdown of only -4.02%. This is one of my series of automated strategies that helps grow my portfolio steadily.

Feel free to tweak parameters and backtest this strategy. Any comments or ideas are appreciated. 

If you are happy with the existing results and would like to automate this strategy, which can be done via alerts, you need to convert it to a study and add alerts in the code. Let me know if you are interested in that and I can create a study based on this strategy.

## Strategy Logic

This strategy uses Bollinger Bands and bandwidth to determine entries and exits.

Bollinger Bands include upper band, middle band and lower band. The middle band is a n-period simple moving average, default n = 16. The upper band is middle band + k * standard deviation, lower band is middle band - k * standard deviation, default k = 3. When price approaches upper band, it indicates overvaluation or overbought. When price approaches lower band, it indicates undervaluation or oversold.

Bandwidth indicator shows the volatility of price relative to the middle band. It is calculated by (upper band - lower band)/middle band * 1000. When bandwidth is below 20, it indicates low volatility or consolidation. When bandwidth exceeds 50, it represents increased volatility.

This strategy looks for long opportunities when bandwidth is between 20-50 and price breaks below lower band. After going long, take profit is set at 108% of entry price, or a stop loss exit when price breaks above upper band.

## Advantage Analysis

The advantages of this strategy include:

1. Bollinger Bands gauge trend direction, reducing risks from false breakouts

2. Bandwidth signal accurately locates range-bound action, avoiding large losses from big swings

3. Backtest shows nearly 80% profitability over 1 year, extremely high risk-reward ratio

4. Maximum drawdown under 5%, effectively controls risk and maintains steady portfolio growth

5. Simple and clear logic, easy to understand and implement, widely applicable to various assets

## Risk Analysis

The risks of this strategy include:

1. Poor Bollinger parameter settings may miss good trading opportunities 

2. Low trading frequency during persistent bull or bear markets, profitability constrained

3. Insufficient backtest data, actual performance may differ from backtest

4. Stop loss may be taken out during extreme moves, leading to large losses

5. High transaction costs also reduce actual profits

Solutions:

1. Optimize parameters and adjust Bollinger period based on market

2. Introduce additional indicators to handle abnormal market conditions

3. Gather sufficient data and backtest across various markets to verify stability

4. Adjust stop loss appropriately to prevent large losses from extreme moves

5. Select trading platforms with low commissions to reduce transaction costs

## Optimization Directions

This strategy can be improved in the following aspects:

1. Add volume confirmation to avoid false breakouts

2. Combine with trend indicators to identify trend direction  

3. Use machine learning to auto tune parameters and adapt to market

4. Add correlation filter to avoid trading uncorrelated assets

5. Optimize take profit/stop loss for more gains during uptrends

6. Introduce more condition filters to increase win rate

7. Test multi-timeframe combinations to profit from multiple cycles  

8. Build indexed portfolio to expand exposure

9. Use machine learning to auto generate & validate new strategies

## Conclusion

Overall this Bollinger Band breakout strategy backtested well and can produce steady returns in range-bound markets. The core logic is simple and clear, easy to grasp and apply. But further improvements in parameter optimization, risk control and portfolio management are needed for stable profits in complex markets. This is a basic trend-following strategy, and can be enhanced by introducing more technical indicators and risk management mechanisms, or combined with machine learning for automation. In summary, this strategy opens the door to algorithmic trading for beginners, and also provides possibilities for experienced traders to optimize strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|16|length|
|v_input_2|3|mult|
|v_input_3|50|BBW Upper Threshold|
|v_input_4|20|BBW Lower Threshold|
|v_input_5|2019|Backtest Start Year|
|v_input_6|true|Backtest Start Month|
|v_input_7|true|Backtest Start Day|
|v_input_8|2020|Backtest Stop Year|
|v_input_9|12|Backtest Stop Month|
|v_input_10|31|Backtest Stop Day|
|v_input_11|8|Take Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-30 00:00:00
end: 2023-11-06 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Bollinger Bands BAT/USDT 30min", overlay=true )

/// Indicators
///Bollinger Bands
source = close
length = input(16, minval=1)
mult = input(3, step=0.1, minval=0.001, maxval=50)
basis = sma(source, length)
dev = mult * stdev(source, length)

upper = basis + dev
lower = basis - dev

plot(basis, color=color.red)
p1 = plot(upper, color=color.blue)
p2 = plot(lower, color=color.blue)
fill(p1, p2)

//Bollinger bands width
bbw = (upper-lower)/basis*1000
//plot(bbw, color=color.blue)

upper_bbw_input = input(title="BBW Upper Threshold", step=1, minval=0, defval=50)
lower_bbw_input = input(title="BBW Lower Threshold", step=1, minval=0, defval=20)


// Backtesting Period
testStartYear = input(2019, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testStopYear = input(2020, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)

testPeriod() => true

// Take Profit
tp_inp = input(8, title='Take Profit %', step=0.1)/100
take_level = strategy.position_avg_price * (1 + tp_inp)

//Entry Strategy
entry_long = crossover(source, lower) and (bbw < upper_bbw_input) and (bbw > lower_bbw_input)
exit_long = cross(high,upper) or close < lower

if testPeriod()

    strategy.entry(id="LongBB", long=true, comment="LongBB", when=entry_long)
    strategy.exit("Take Profit Long","LongBB",limit=take_level)
    strategy.close(id="LongBB", when=exit_long )


```

> Detail

https://www.fmz.com/strategy/431394

> Last Modified

2023-11-07 15:08:36
