
> Name

Bollinger Band Breakout Stock Strategy Bollinger-Breakout-Stock-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/19e9f1728ba213704d7.png)

[trans]

## Overview
The Bollinger Bands Breakout Stock Strategy is a quantitative trading strategy that tracks stock price movements. It uses the Bollinger Bands indicator to determine whether the price has left the normal fluctuation range and issue trading signals. When the price breaks through the lower limit of the Bollinger Bands, enter the market with a long position; when the price breaks through the upper limit of the Bollinger Bands, enter the market with a short position. This strategy tracks the short-term trend of stock prices and is suitable for short-term operations.
## Strategy Principle
This strategy uses 20 days of stock closing prices to calculate the middle, upper, and lower bands. The middle rail line is a simple moving average of the 20-day closing price; the upper and lower rail lines are respectively composed of the middle rail line plus or minus 2 times the standard deviation. When the stock's closing price breaks through the lower track, it is considered that the stock price has left the normal fluctuation range and has begun a new upward trend. According to the code strategy, enter the market long at this time. The stop loss point is the lowest point of the last 10 K lines, and the take profit point is the highest point of the last 10 K lines. When the stock's closing price breaks through the upper track, it is believed that the stock price has left the normal fluctuation range and has begun a new downward trend. According to the code strategy, short entry is made at this time. The stop loss point is the highest point of the last 10 K lines, and the take profit point is the lowest point of the last 10 K lines. This strategy simply and effectively uses the Bollinger Bands indicator to determine the price trend and fluctuation range, and enter the market early when the price may reverse.
## Advantage Analysis
This strategy has the following main advantages:
1. Use Bollinger Bands to determine the changing points of stock price trends and capture short-term trends efficiently.
2. The risk of retracement is small, and the stop loss point is set at the low point of recent fluctuations, which can effectively control losses.
3. The profit stop point is set at the high point of the recent fluctuation, which can maximize the profit of capturing the unilateral trend market.
4. The strategy idea is simple and clear, easy to understand and modify, and is suitable for beginners in quantitative trading.
## Risk Analysis
There are also some risks with this strategy:
1. The Bollinger Bands indicator is very sensitive to volatility, and improper parameter settings may lead to false signals. Parameters such as the number of cycles should be adjusted appropriately.
2. The price of the stock itself fluctuates greatly, and the stop loss point may be too early to leave the market, making it impossible to continue to follow the trend. The fluctuation range can be appropriately expanded to stop loss.
3. If the breakthrough signal lags behind, there may be excessive floating profit. Early entry should be judged in conjunction with other indicators.
4. The market is unpredictable and it is difficult to grasp the stop-profit and stop-loss. The parameters should be adjusted appropriately based on manual experience.
## Optimization direction
This strategy can be further optimized from the following directions:
1. Combine with other indicators to confirm entry signals, such as sudden increase in trading volume, etc.
2. Dynamically adjust Bollinger Band parameters to better adapt to market fluctuations.
3. Optimize take profit and stop loss strategies, such as trailing stop loss, batch take profit, etc.
4. Test the parameter effects of different stock varieties and find the best applicable range.
5. Add machine learning algorithm to automatically optimize parameter settings.
## Summarize
The overall idea of ​​the Bollinger Bands breakthrough strategy is clear and easy to understand. Using the Bollinger Bands indicator to determine the stock price reversal point has less risk of retracement and can capture short-term unilateral trends. However, there are also problems of certain profit upper limit and time lag. This strategy can be further improved through parameter optimization, stop-profit and stop-loss strategy optimization, and adding other auxiliary indicators. Generally speaking, this strategy is suitable for short-term stock operations and tracking short- and medium-term stock trends.
|| 

## Overview  

The Bollinger breakout stock strategy is a quantitative trading strategy that tracks stock price fluctuations using Bollinger Bands to identify when prices break out of their normal volatility range and generate trade signals. It goes long when prices break below the lower Bollinger Band and goes short when prices break above the upper Bollinger Band. The strategy tracks short-term price trends and is suitable for short-term trading.  

## Strategy Logic  

The strategy calculates the middle band, upper band and lower band using 20-day closing prices. The middle band is a 20-day simple moving average, while the upper and lower bands are placed at a distance of 2 standard deviations from the middle band. 

When stock closing prices break below the lower band, it signals that prices have broken out of the normal volatility range and are starting a new uptrend. The strategy would go long at this point based on the code. The stop loss is set at the lowest low of the recent 10 bars, while take profit is set at the highest high of recent 10 bars.

When prices break above the upper band, it signals the start of a new downtrend. The strategy would go short here. Stop loss is the 10-bar highest level and take profit is the 10-bar lowest level.  

The strategy effectively utilizes Bollinger Bands to identify trend changes and volatility range, entering early when prices are likely to reverse.  

## Advantage Analysis

The main advantages of this strategy are:

1. Effectively identifies trend change points using Bollinger Bands, catching short-term trends efficiently.  

2. Smaller drawdown risk due to stop loss set at recent lowest swing low, which limits losses.

3. Take profit set at the recent highest level allows maximizing profits from one-sided trend moves.  

4. Simple and clear logic, easy to understand and modify, suitable for quant trading beginners.

## Risk Analysis   

There are also some risks to consider:

1. Bollinger Bands are very sensitive to volatility changes, inappropriate parameters may cause false signals. Parameters like period should be adjusted accordingly.  

2. High stock price fluctuations, stop loss triggered too early, unable to ride the trend. Can consider widening bands for stop loss.

3. Signal delay, may cause excessive unrealized profits. Other indicators can be added to identify earlier entries.  

4. Market unpredictability makes take profit/stop loss difficult, manual intervention required to fine tune parameters.

## Improvement Areas

Some ways to further improve the strategy:

1. Add other indicators to confirm signals, e.g. volume spike.  

2. Dynamically adjust Bollinger parameters to fit changing volatility.

3. Enhance stop loss/take profit, e.g. trailing stop loss, staged profit taking.  

4. Test parameters across different stocks to find best fit.  

5. Introduce machine learning to auto optimize parameters.

## Summary   

The Bollinger breakout strategy has clear logic to identify reversals. Limited drawdown risk allows catching short-term trends. But also has profit target limitations and signal delay issues. Can be improved via parameter tuning, better stop loss/take profit, adding filters etc. Suitable for short-term stock trading to track medium-term trends.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-14 00:00:00
end: 2023-12-14 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

// Initial settings
strategy("Bulle de bollinger", overlay = true)

// Parameter Settings
mdl = sma(close, 20)
dev = stdev(close, 20)

upr = mdl + 2*dev
lwr = mdl - 2*dev

// Plot
plot(mdl, color = color.green) // Plot moving average
p1 = plot(upr, color = color.red) // Plot Upper_band
p2 = plot(lwr, color = color.green) // Plot lower band
fill(p1, p2, color = color.blue) // Fill transparant color between the 2 plots

// Strategy entry & close

if open[1] < lwr[1] and close[1] < lwr[1] // Previous price lower than lower band and current close is higher than lower band
    stop_level = lowest(10)
    profit_level = highest(10)
    strategy.entry(id = 'bb_buy', long = true)
    strategy.exit("TP/SL", "bb_buy", stop=stop_level, limit=profit_level)
    
if open[1] > upr[1] and close[1] > upr // Previous price is higher than higher band & current close is lower the higher band
    stop_level = highest(10)
    profit_level = lowest(10)
    //strategy.entry(id = 'bb_sell', long = false)
    //strategy.exit("TP/SL", "bb_sell", stop=stop_level, limit=profit_level)
```

> Detail

https://www.fmz.com/strategy/435515

> Last Modified

2023-12-15 16:20:57
