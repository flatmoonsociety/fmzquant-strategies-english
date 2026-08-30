
> Name

Dual-Reversal-Momentum-Index-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/39d6246f4179b8ef6dd6ed46176badddf4c805846897102057db886657206dd0.png)
[trans]

## Overview
This strategy is a trading strategy that uses the two-way reversal momentum index indicator. This strategy constructs a reversal momentum index by calculating the highest price, lowest price, and closing price within a certain period of time, and calculates its moving average to form a trading signal. Trading signals are generated when the index reverses downward from the overbought zone or reverses upward from the oversold zone. This strategy also sets a breakout stop loss mechanism.
## Strategy Principle
The core indicator of this strategy is the Stochastic Momentum Index (SMI). The calculation formula of SMI is as follows:
$$SMI = \frac{Close-(HH+LL)/2}{AVGDIFF/2}*100$$

Among them, HH is the highest price in the past N days, LL is the lowest price in the past N days, N is determined by parameter a; AVGDIFF is the M-day moving average of HH-LL, and M is determined by parameter b.
The SMI index reflects price reversal characteristics. When the stock price is close to the highest point in the last N days, the SMI is close to 100, indicating that the stock is overbought; when it is close to the lowest point in the last N days, the SMI is close to -100, indicating that the stock is oversold. A buy/sell signal is issued when the SMI reverses downward from the 100 level or reverses upward from the -100 level.
This strategy uses the M-day moving average SMA of SMI as the trading signal line. When the SMI reverses downward from the overbought zone and falls below the SMA, a buy signal is generated; when the SMI reverses upward from the oversold zone and breaks below the SMA, a sell signal is generated.
At the same time, the strategy determines the K-line entity breakthrough to set a stop loss.
## Strategic Advantages
This strategy has the following advantages:
1. Using the price reversal principle, you can generate trading signals at trend reversal points and capture reversal opportunities.
2. The SMI index combines the highest price, lowest price and closing price to comprehensively judge overbought and oversold conditions, and the signal is relatively reliable.
3. Set a stop loss based on the K-line entity breakthrough, which can promptly stop the loss and exit the position and effectively control risks.
4. The strategy has fewer parameters and is easy to implement and optimize.
## Strategy Risk
This strategy also has some risks:
1. In reversal trading, it is difficult to determine when the reversal will be successful, and the trend reversal may be captured after multiple losses.
2. Misjudgment of reversal timing may lead to amplified losses.
3. The entity may be too sensitive when it breaks through the stop loss, and the probability of being stuck is high.
Corresponding solutions:
1. Optimize SMI parameters and adjust reversal transaction frequency.
2. Combine with other indicators to determine the reversal time point.
3. Adjust the entity size stop loss parameter to prevent it from being too sensitive.
## Strategy optimization
This strategy can be optimized from the following directions:
1. Optimize parameters a and b of SMI and adjust the sensitivity of inversion capture.
2. Add other indicators to judge to avoid missing the main trend direction. For example, combining moving averages, volatility indicators, etc.
3. Add stop loss methods to prevent the stop loss from being too sensitive or slow. You can consider trailing stop loss, curve stop loss, etc.
4. Use machine learning models to determine the probability of reversal success and avoid reversing failed transactions.
## Summary
Overall, this strategy is a two-way trading strategy that uses the reversal index SMI. The advantage is that it uses the price reversal characteristics to generate trading signals at the reversal point, which can capture more short-term trading opportunities. However, there are also some typical reversal trading risks, and parameters and stop losses need to be optimized to prevent losses from amplifying. Generally speaking, this strategy is suitable for investors who are interested in reversal trading, but risks must be controlled by combining judgment with other indicators and strict stop loss.
||

## Overview 
This strategy is based on the Dual Reversal Momentum Index indicator for trading. It calculates a reversal momentum index over a certain time period using highest price, lowest price, and closing price, and generates trading signals when the index reverses down from the overbought zone or reverses up from the oversold zone. It also sets a breakout stop loss mechanism.

## Strategy Logic
The core indicator of this strategy is Stochastic Momentum Index (SMI). The calculation formula of SMI is:  

$$SMI = \frac{Close-(HH+LL)/2}{AVGDIFF/2}*100$$

Where HH is the highest price over the past N days, LL is the lowest price over past N days, N is determined by parameter a; AVGDIFF is the M-day moving average of HH-LL, M is determined by parameter b.

SMI shows the reversal characteristic of prices. When the stock price approaches the highest point over the past N days, SMI is close to 100, indicating overbought of the stock; when it approaches the lowest point over the past N days, SMI is close to -100, indicating oversold. The buy/sell signals are generated when SMI reverses down from the 100 level or reverses up from the -100 level.

The strategy uses the M-day moving average SMA of SMI as the trading signal line. When SMI reverses down from the overbought zone and breaks below SMA, a buy signal is generated. When SMI reverses up from the oversold zone and breaks above SMA, a sell signal is generated. 

Also, the strategy judges the candlestick body breakout for stop loss.

## Advantage Analysis
The advantages of this strategy are:

1. Utilizing the price reversal principle, it can generate trading signals at reversal points and capture reversal opportunities.  

2. SMI combines highest price, lowest price and closing price for judging overbought and oversold conditions, making more reliable signals.

3. With candlestick body breakout stop loss, it can exit positions in time and effectively control risks.

4. The strategy has few parameters and is easy to implement and optimize.

## Risk Analysis  
There are also some risks for this strategy:

1. Reversal trading finds it hard to determine the exact timing of successful reversals, and may incur multiple losses before capturing trend reversal.

2. Wrong judgement of reversal points may lead to amplified losses.  

3. The body breakout stop loss may be too sensitive with high probability of being trapped.

The solutions are:
1. Optimize SMI parameters to adjust reversal trading frequency.  

2. Combine other indicators to determine reversal timing.

3. Adjust body size for stop loss to prevent being too sensitive.

## Optimization
The strategy can be optimized in the following aspects:

1. Optimize parameters a and b of SMI to adjust the sensitivity of capturing reversals.  

2. Add other indicators for judgement to avoid missing major trend directions, e.g. moving averages, volatility indicators etc.

3. Add more stop loss methods to prevent being too sensitive or insensitive, such as trailing stop loss, curve stop loss etc. 

4. Incorporate machine learning models to judge the probability of reversal success, avoiding failed reversal trades.

## Conclusion
In conclusion, this is a dual-direction trading strategy based on the reversal momentum index SMI. The advantage lies in capturing more short-term trading opportunities by utilizing price reversal and generating signals at reversal points. But there are also typical risks of reversal trading. Parameter tuning and stop loss optimization are needed to prevent amplified losses. Overall speaking, this strategy suits investors interested in reversal trading, but must incorporate other indicators and strict stop loss to control risks.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Capital, %|
|v_input_4|5|Percent K Length|
|v_input_5|3|Percent D Length|
|v_input_6|50|SMI Limit|
|v_input_7|2018|From Year|
|v_input_8|2100|To Year|
|v_input_9|true|From Month|
|v_input_10|12|To Month|
|v_input_11|true|From day|
|v_input_12|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-01 00:00:00
end: 2023-11-30 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's Stochastic Strategy v1.0", shorttitle = "Stochastic str 1.0", overlay = false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings 
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
a = input(5, "Percent K Length")
b = input(3, "Percent D Length")
limit = input(50, defval = 50, minval = 1, maxval = 100, title = "SMI Limit")
fromyear = input(2018, defval = 2018, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Stochastic Momentum Index
ll = lowest (low, a)
hh = highest (high, a)
diff = hh - ll
rdiff = close - (hh+ll)/2
avgrel = ema(ema(rdiff,b),b)
avgdiff = ema(ema(diff,b),b)
SMI = avgdiff != 0 ? (avgrel/(avgdiff/2)*100) : 0
SMIsignal = ema(SMI,b)

//Lines
plot(SMI, color = blue, linewidth = 3, title = "Stochastic Momentum Index")
plot(SMIsignal, color = red, linewidth = 3, title = "SMI Signal Line")
plot(limit, color = black, title = "Over Bought")
plot(-1 * limit, color = black, title = "Over Sold")
plot(0, color = blue, title = "Zero Line")

//Body
body = abs(close - open)
abody = sma(body, 10)

//Signals
up = SMIsignal < -1 * limit and close < open
dn = SMIsignal > limit and close > open
exit = ((strategy.position_size > 0 and close > open) or (strategy.position_size < 0 and close < open)) and body > abody / 2

//Trading
lot = strategy.position_size == 0 ? strategy.equity / close * capital / 100 : lot[1]

if up
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Bottom", strategy.long, needlong == false ? 0 : lot)

if dn
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Top", strategy.short, needshort == false ? 0 : lot)
    
if  exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/436490

> Last Modified

2023-12-25 12:02:57
