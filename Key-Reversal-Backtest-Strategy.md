
> Name

Key-Reversal-Backtest-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3edb5cd27d6e27749e273a19aea836d56244b63b7f352b5efd58ca63d3308134.png)

[trans]

### Overview
The reverse indicator backtesting strategy determines potential short opportunities in the market by detecting whether the stock price reaches a new high and then closes down, which is a short-term trading strategy. This strategy combines visual patterns for pattern recognition to assist in judging price reversal signals, and then performs backtesting to verify the feasibility of the strategy.
### Strategy Principles
The core logic of this strategy is based on the "reverse indicator" theory, which identifies potential short opportunities by judging whether there are obvious signs of a fall after the price reaches a new high. The specific implementation principle is as follows:
1. Define the parameter nLength, which represents the retracement period and is used to determine whether the price has reached a new high;
2. Define variable xHH to store the highest price in the past nLength period;
3. Define variable C1 to determine whether the highest price of the day exceeds xHH, that is, whether it is a new high, and whether the closing price is lower than the closing price of the previous day. If this condition is met, it may be a reverse pattern;
4. Draw a triangle to indicate the K-line that may be a reverse pattern that day;
5. When a reverse pattern is identified, conduct short-term short trading and set up stop-profit and stop-loss logic.
Through the above process, you can effectively identify negative patterns, determine price reversal signals, and conduct short-term short transactions.
### Advantage Analysis
This strategy has several advantages:
1. Based on the actual price pattern, it is more reliable to judge the reversal signal;
2. Combined with graphical indicators, trading signals are more intuitive;
3. Implement stop-profit and stop-loss logic, which is conducive to risk control;
4. Backtesting verifies the feasibility of the strategy and is more convincing.
Generally speaking, this strategy combines multiple factors to judge trading signals and conducts backtest verification. It has high accuracy in judging price reversal and has good practical value.
### Risk Analysis
Although this strategy has obvious advantages, there are also some risks to be aware of:
1. The reverse pattern may not necessarily trigger a trend reversal, and there is a certain risk of false signals;
2. The sample size of a single stock may be small and cannot fully represent the overall market;
3. Improper setting of stop loss points may lead to greater financial losses.
To avoid the above risks, you can consider the following points:
1. Combine more factors to verify trading signals, such as changes in trading volume, etc.;
2. Increase the backtest sample size and combine backtests with different varieties;
3. Optimize and test different stop loss points to find optimal parameters.
### Optimization direction
There are also some directions in which this strategy can be optimized:
1. Add machine learning algorithms to train the model to determine the possibility of negative forms and improve accuracy;
2. Optimize stop loss algorithms, such as trailing stop loss, average stop loss, etc., to reduce single stop loss;
3. Combine sentiment analysis and other factors to determine the probability of market reversal and set dynamic trading signals;
4. Enrich strategy types, such as combining volume and energy indicators, volatility indicators, etc. to determine reversal signals;
5. Use the backtesting and optimization functions of more complex trading systems to increase the flexibility of the strategy.
Through the optimization of the above aspects, the accuracy and practical level of this trading strategy can be further improved.
### Summarize
The biased indicator backtesting strategy identifies short-term reversal signals by judging price patterns and performs backtesting verification, which can effectively capture reversal opportunities. This strategy has intuitive graphical indicators, complete take-profit and stop-loss logic, and has good practical value. Of course, you still need to pay attention to a certain risk of false signals. By continuously optimizing the judgment model and stop loss algorithm, the strategy can be more effective. Overall, this strategy provides new ideas for judging market reversals and is a very promising quantitative trading method.
||

### Overview

The key reversal backtest strategy detects potential short opportunities in the market by checking if stock prices hit new highs and then close lower. It is a short-term trading strategy. This strategy combines visual pattern recognition to assist in identifying price reversal signals, and then backtests to verify the feasibility of the strategy.

### Strategy Principle  

The core logic of this strategy is based on the "key reversal indicator" theory, by judging whether there are obvious signs of decline after the price hits a new high, to identify potential short opportunities. The specific implementation principles are as follows:

1. Define the parameter nLength, which represents the lookback period, to determine whether the price is hitting a new high or not;  

2. Define the variable xHH to store the highest price in the past nLength cycles;

3. Define the variable C1 to determine if today's highest price exceeds xHH, i.e. hitting a new high, while the closing price is lower than the previous day's closing price, which meets the conditions that may be a key reversal pattern;  

4. Draw triangle to indicate the potential key reversal K-line today;

5. When identifying the key reversal pattern, make short-term short trades and set stop profit and stop loss logic.

Through the above process, potential key reversal patterns can be effectively identified, price reversal signals can be judged, and short-term short trades can be made.

### Advantage Analysis   

The strategy has the following advantages:

1. Identifying reversal signals based on actual price patterns is more reliable; 

2. Visual graphical indicators make trading signals more intuitive;

3. Implementing stop profit and stop loss logic is conducive to risk control;  

4. Backtesting to verify the feasibility of the strategy is more convincing.

Overall, the strategy combines multiple factors to determine trading signals and backtesting to verify the accuracy of price reversals is relatively high, with good practical value.

### Risk Analysis

Although the strategy has obvious advantages, there are still some risks to note:

1. Key reversal patterns do not necessarily lead to trend reversals, there is a certain risk of false signals; 

2. The sample size of a single stock may be small and may not fully represent the overall market;  

3. Improper stop loss point settings can lead to greater capital losses.

To avoid the above risks, the following points can be considered:

1. Verify trading signals with more factors, such as abnormal trading volume;

2. Increase backtest sample size, combination backtest of different varieties;  

3. Optimize and test different stop loss points to find the optimal parameters.

### Optimization Directions   

There are still some directions that can be optimized in this strategy:

1. Increase machine learning algorithms to train models to determine the probability of key reversal patterns to improve accuracy;

2. Optimize stop loss algorithms, such as trailing stop loss, average stop loss, etc., to reduce single stop loss;

3. Incorporate more factors such as sentiment analysis to determine the probability of market reversal and set dynamic trading signals;

4. Enrich strategy types, such as combining momentum indicators, volatility indicators, etc. to determine reversal signals; 

5. Use backtesting and optimization functions of more complex trading systems to improve strategy flexibility.

Through the above aspects of optimization, the accuracy and practical level of this trading strategy can be further improved.

### Summary  

The key reversal backtest strategy identifies short-term reversal signals by judging price patterns, and verifies them through backtesting. It can effectively capture reversal opportunities. This strategy has intuitive graphical indicators and complete stop profit and stop loss logic, with good practical value. Of course, certain false signal risks still need to be noted. By continuously optimizing the judgment model and stop loss algorithm, the effect of the strategy can be better. Overall, this strategy provides new ideas for judging market reversals and is a very promising quantitative trading method.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Take Profit pip|
|v_input_2|10|Stop Loss pip|
|v_input_3|true|Enter the number of bars over which to look for a new high in prices.|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/01/2020
//
// A key reversal is a one-day trading pattern that may signal the reversal of a trend. 
// Other frequently-used names for key reversal include "one-day reversal" and "reversal day."
// How Does a Key Reversal Work?
// Depending on which way the stock is trending, a key reversal day occurs when:
// In an uptrend -- prices hit a new high and then close near the previous day's lows.
// In a downtrend -- prices hit a new low, but close near the previous day's highs
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Key Reversal Down Backtest", shorttitle="KRD Backtest", overlay = true)
input_takeprofit = input(20, title="Take Profit pip", step=0.01)
input_stoploss = input(10, title="Stop Loss pip", step=0.01)
nLength = input(1, minval=1, title="Enter the number of bars over which to look for a new high in prices.")
xHH = highest(high[1], nLength)
C1 = iff(high > xHH and close < close[1], true, false)
plotshape(C1, style=shape.triangledown, size = size.small, color=color.red)
posprice = 0.0
pos = 0
barcolor(nz(pos[1], 0) == -1 ? color.red: nz(pos[1], 0) == 1 ? color.green : color.blue ) 
posprice := iff(C1== true, close, nz(posprice[1], 0)) 
pos := iff(posprice > 0, -1, 0)
if (pos == 0) 
    strategy.close_all()
if (pos == -1)
    strategy.entry("Short", strategy.short)
posprice := iff(low <= posprice - input_takeprofit and posprice > 0, 0 ,  nz(posprice, 0))
posprice := iff(high >= posprice + input_stoploss and posprice > 0, 0 ,  nz(posprice, 0))
```

> Detail

https://www.fmz.com/strategy/439036

> Last Modified

2024-01-17 10:56:52
