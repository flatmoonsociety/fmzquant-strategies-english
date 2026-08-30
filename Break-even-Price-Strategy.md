
> Name

Break-even-Price-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6bbb58a9d57a5e262c010e94626d2e3c42371a232116c05719babca7e868d3ba.png)
[trans]


## Overview
The main idea of ​​this strategy is to draw the entry price and breakeven price after opening a position to visually display the position where profits can be obtained if the price breaks through the entry price. This can help traders better manage positions and achieve profit recovery.
## Strategy Principle
The code uses the SMA golden cross to go long and the SMA dead cross to open a short position. Then calculate the entry price and the breakeven price after taking into account the handling fee. The calculation method of the breakeven price is: when going long, the breakeven price is the entry price multiplied by (1+handling fee); when going short, the breakeven price is the entry price multiplied by (1-handling fee). Finally, draw the entry price line and breakeven price line, and fill in color between the two lines.
In this way, as long as the price breaks through the entry price line, it means that a profit has been made. Traders can set take-profit or stop-loss levels based on the breakeven price line to lock in profits.
The code is mainly divided into:
1. Judgment of opening conditions
2. Calculation of entry price and breakeven price
3. Draw entry price line and breakeven price line
4. Fill the color between the two lines
This breakthrough cover price strategy is realized by judging the opening of a position based on simple conditions, calculating the breakeven price, and drawing auxiliary lines.
## Strategic advantage analysis
This strategy has the following advantages:
1. Visually display the profit and loss situation, and you can quickly judge whether the price meets the profit requirements.
2. You can set the stop-profit and stop-loss levels according to the breakeven price line to avoid losses from expanding.
3. The code is concise and easy to understand, easy to implement and adjust.
4. You can integrate it into your own trading strategy and use the breakeven price line to manage positions.
5. The handling fee parameters can be easily modified, applicable to different exchanges and products.
6. You can optimize the opening conditions by adjusting the SMA period.
## Strategy risk analysis
This strategy also has certain risks:
1. The SMA indicator itself has a strong hysteresis and may miss price changes.
2. The breakeven price line cannot completely avoid the occurrence and expansion of losses.
3. The strategy itself has no exit mechanism, and traders need to monitor their own profits and losses.
4. Inaccurate setting of handling fees may lead to errors in the calculation of the capital-guaranteed price.
5. The strategy does not consider the impact of slippage.
6. The strategy lacks a stop-loss mechanism, which may lead to large losses.
The solutions corresponding to the risks are:
1. You can consider switching to a more active indicator, such as MACD.
2. Trend indicators should be used to determine the general direction and avoid opening positions against the trend.
3. It is necessary to add stop-profit and stop-loss logic so that the strategy can automatically exit.
4. Accurate handling fees should be set based on actual exchanges.
5. Fixed slippage can be set to optimize entry and exit.
6. Add a trailing stop to control maximum losses.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Replace the SMA indicator with more advanced indicators such as MACD or KDJ.
2. Add trend judgment indicators to avoid opening positions against the trend.
3. Optimize SMA cycle parameters and improve position opening accuracy.
4. Add stop-profit and stop-loss logic so that the strategy can exit automatically.
5. Set slippage control for backtesting and real trading.
6. Optimize the handling fee parameters to make them closer to actual transactions.
7. Add a trailing stop to limit the maximum loss.
8. Strategies can be copied in different time periods for multi-period combinations.
9. Optimize entry based on changes in trading volume.
10. Parameters can be optimized through machine learning algorithms.
## Summarize
This strategy intuitively shows the profit position when the price breaks through the entry price, and is a simple and practical auxiliary strategy. It has the advantages of concise code and easy implementation, but there are also some risks that need to be paid attention to. We can optimize and improve the strategy from multiple angles to make it more widely applicable and have stronger stability and profitability. Overall, this strategy provides us with a very good reference case and is worthy of further research and application.
||

## Overview

The main idea of this strategy is to plot the entry price and breakeven price after opening a position, to visually display the price level where a breakout above the entry price would result in profit. This can help traders better manage positions and realize profits.

## Strategy Logic

The code enters long when SMA crossover happens and enters short on SMA crossunder. It then calculates the entry price and breakeven price after fees. The breakeven price is calculated as: for long, breakeven price = entry price * (1 + fees); for short, breakeven price = entry price * (1 - fees). Finally, it plots the entry price line and breakeven price line, filling the area between them.   

This way, once the price breaks through the entry price line, it means the trade is now profitable. Traders can use the breakeven line to set take profit or stop loss levels to lock in profits.

The key components of the code are:

1. Entry condition checks
2. Calculation of entry and breakeven prices  
3. Plotting the entry and breakeven price lines
4. Filling color between the two lines

With simple condition checks for entry, breakeven price calculation, and plotting of auxiliary lines, the break-even price strategy is implemented.

## Advantage Analysis

The advantages of this strategy include:

1. Intuitive display of profit/loss, can quickly judge if price has reached profit target.

2. Can use breakeven line to set take profit/stop loss levels to avoid increasing losses. 

3. Simple and easy to understand code, easy to implement and adjust.

4. Can be incorporated into own trading strategies, using breakeven line to manage positions.

5. Easy to modify fee parameters for different exchanges and products. 

6. Can optimize entry by adjusting SMA periods.

## Risk Analysis

The risks of this strategy include:

1. SMA has lagging nature, may miss price changes.

2. Breakeven line cannot completely avoid losses.

3. No exit mechanism, traders need to monitor P/L themselves.

4. Incorrect fee settings may cause wrong breakeven calculation.

5. Slippage is not considered. 

6. No stop loss, may lead to large losses.

The solutions are:

1. Consider more sensitive indicators like MACD.

2. Add trend indicator to avoid counter trend trades.

3. Add take profit and stop loss logic for automatic exits.

4. Set accurate fees based on actual exchange. 

5. Add fixed slippage for optimal entries and exits. 

6. Add trailing stop loss to limit max loss.

## Improvement Areas

Some ways to optimize the strategy:

1. Replace SMA with more advanced indicators like MACD or KDJ.

2. Add trend filter to avoid counter trend trades.

3. Optimize SMA periods for better entry precision. 

4. Add take profit and stop loss logic for automatic exits.

5. Set slippage for backtest and live trading.

6. Optimize fee settings to match reality.

7. Add trailing stop loss to limit max loss.

8. Run strategy on multiple timeframes for diversification.

9. Incorporate volume changes to improve entry.

10. Use machine learning to optimize parameters.

## Conclusion

This strategy intuitively displays the breakeven price level where a breakout can result in profits. It is a simple and practical auxiliary strategy with advantages like simple code and easy implementation. But risks need to be addressed too. We can optimize it from many aspects to make it more robust and profitable. Overall it provides a great reference example worth studying and applying.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.25|Price Change in %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-15 00:00:00
end: 2023-11-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © NikitaDoronin
//@version=4

strategy("Plot Break-even Price", overlay=true)

/// Break-even calculation
ep = 0.0
ep := na(ep[1]) ? na : ep[1]

p = 0.0
p := na(p[1]) ? na : p[1]

/// Fees Input
fee_inp = input(0.25, title='Price Change in %', step=0.1)/100

/// Your Strategy calculation
longCondition = crossover(sma(close, 14), sma(close, 28))
shortCondition = crossunder(sma(close, 14), sma(close, 28))

/// Stategy Entry
if (longCondition)
    ep := close
    p := close * (1 + fee_inp)
    strategy.entry("My Long Entry Id", strategy.long)

if (shortCondition)
    ep := close
    p := close * (1 - fee_inp)
    strategy.entry("My Short Entry Id", strategy.short)

/// Plot Break-even Price 
p1 = plot(ep, color = color.red, transp = 85)
p2 = plot(p, color = color.green)
fill(p1, p2, color = color.red, transp = 85)
```

> Detail

https://www.fmz.com/strategy/432310

> Last Modified

2023-11-16 11:16:25
