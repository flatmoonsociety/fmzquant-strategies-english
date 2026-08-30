
> Name

Advanced-RSI-Indicator-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b48c171eaa29eec000.png)
[trans]
## Overview
The S&P500 Advanced RSI Indicator Trading Strategy is a medium- and long-term trend following strategy for the S&P500 index. This strategy combines multiple filters to trade on RSI overbought and oversold signals to control risk and reduce false signals.
## Strategy Principle
The core indicator of this strategy is RSI, which determines whether the price is overbought or oversold based on the 2-period RSI value. Go long when the RSI indicator is below the oversold line set, and close the position when the RSI indicator is above the oversold line. In addition, the strategy also sets a series of auxiliary filters for risk control:
1. Weekly RSI filter: Require weekly RSI to be below the setting line to avoid being too aggressive in going long in a bull market
2. MA filter: requires the price to be higher than the specified period MA, ensuring that you only buy after the trend starts
3. Secondary RSI filter: The secondary RSI indicator is also required to be lower than the oversold line to avoid false breakthroughs
4. ATR breakthrough filter: avoid going long after a rapid price drop and control risks
The combination of the above multiple filters can effectively identify medium and long-term price reversal points, control transaction frequency and reduce risks.
## Advantage Analysis
The S&P500 advanced RSI indicator trading strategy has the following advantages:
1. Combined with multiple auxiliary indicator filtering to reduce false signals and achieve higher reliability
2. Control risks through the ATR breakthrough filter to avoid chasing after the price drops sharply.
3. Weekly RSI filter to avoid buying in a bull market and prevent being too aggressive
4. The MA filter requires buying after the price is higher than the trend moving average, ensuring that the trend starts before entering the market.
5. The secondary RSI filter prevents the RSI indicator from producing false breakthroughs and going long.
6. Suitable for medium and long-term positions and will not be traded too frequently
## Risk Analysis
The main risks of this strategy come from the following aspects:
1. There will be a certain lag when using RSI as the main indicator.
2. The filtering conditions are too strict and some opportunities may be missed.
3. In extremely large market conditions, stop loss conditions may be breached
4. Based on simple RSI indicators and filters, the ability to judge complex market conditions is weak.
The corresponding mitigation methods are as follows:
1. Adjust parameters appropriately to prevent missing opportunities
2. Increase the position size to make up for a certain probability of missed purchases
3. Filtering conditions can be relaxed appropriately to increase transaction frequency.
4. Consider combining more indicators to judge complex market conditions
## Optimization direction
This strategy can also be optimized from the following directions:
1. Test and adjust RSI parameters to find the optimal overbought and oversold lines
2. Test the MA moving average cycle parameters and determine the optimal parameters
3. Test and adjust ATR parameters, optimize price breakthrough filtering judgment
4. Try to combine judgment with other indicators to improve your ability to judge complex market conditions.
5. Optimize weekly RSI parameters and determine the optimal parameters of weekly RSI
6. Optimize the parameters of secondary RSI and find the best secondary RSI cycle and overbought and oversold lines
## Summarize
The S&P500 advanced RSI indicator trading strategy uses the RSI indicator to determine the mid- and long-term price trend reversal points, and sets a variety of filter conditions to control risks. This strategy makes full use of the effectiveness of the RSI indicator, which can effectively lock in the medium and long-term trends and avoid entering and exiting the market too frequently. As parameters continue to be optimized, strategy performance is expected to continue to improve. Generally speaking, this strategy is suitable for medium and long-term value investment and is a relatively stable quantitative strategy.
||

## Overview  

The S&P500 Advanced RSI Indicator Trading Strategy is a medium to long term trend following strategy for trading the S&P500 index. This strategy combines multiple filters with RSI overbought and oversold signals to control risk and reduce false signals.  

## Strategy Logic   

The core indicator of this strategy is RSI, using 2 period RSI to determine price overbought and oversold levels. It goes long when RSI drops below the oversold line and closes position when RSI rises above the overbought line. In addition, the strategy has a series of auxiliary filters to control risk:

1. Weekly RSI Filter: Requires weekly RSI to be below a threshold to avoid overly aggressive longs in a bull market.  

2. MA Filter: Requires price to be above a certain MA period to ensure entering after an uptrend has started.

3. Secondary RSI Filter: Requires the secondary RSI indicator also drops below oversold line to avoid false breakouts.  

4. ATR Breakout Filter: Avoids going long after a sharp price drop to control risk.   

The combination of these multiple filters can effectively identify medium to long term price reversal points, control trade frequency and reduce risk.

## Advantage Analysis   

The S&P500 Advanced RSI Indicator Trading Strategy has the following advantages:

1. Combining multiple auxiliary indicators reduces false signals and improves reliability.  

2. The ATR breakout filter controls risk by avoiding buying after a price crash.

3. Weekly RSI filter prevents overly aggressive longs in a bull market.  

4. MA filter ensures entering after an uptrend has started.  

5. Secondary RSI filter avoids false RSI breakouts. 

6. Suitable for medium to long term holding and avoids overtrading.

## Risk Analysis  

The main risks of this strategy come from the following aspects:  

1. RSI as the main indicator has some lagging.  

2. Filter conditions could be too strict and miss opportunities.  

3. Stop loss could be taken out during flash crashes.  

4. Simple RSI and filters have limited capabilities in complex market conditions.

Corresponding mitigations:

1. Adjust parameters to avoid missing trades.  

2. Increase position sizing to account for some missed trades.

3. Relax filter conditions moderately to increase trade frequency.  

4. Consider combining more indicators for complex market analysis.

## Optimization Directions   

The strategy can be further optimized in the following directions:

1. Test adjusting RSI parameters to find optimal overbought/oversold lines.  

2. Test MA period parameters to determine optimal values.

3. Test adjusting ATR parameters to optimize price breakout filters.  

4. Try combining other indicators for better analysis of complex markets.   

5. Optimize weekly RSI parameters to find optimal settings.

6. Optimize secondary RSI parameters including period and overbought/oversold lines.   

## Conclusion  

The S&P500 Advanced RSI Indicator Trading Strategy identifies medium to long term trend reversal points using RSI and multiple filter conditions to control risk. It utilizes the strengths of RSI effectively to lock in medium/long term trends and avoid overtrading. As parameters continue to be optimized, strategy performance can continue improving. Overall it is suitable for medium to long term value investing and is a relatively stable quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|Base RSI Length|
|v_input_2|10|Overbought Level|
|v_input_3|90|Oversold Level|
|v_input_4|70|Overbought Level Exit|
|v_input_5|true|Enable Weekly RSI Filter|
|v_input_6|30|Weekly Oversold Level|
|v_input_7|70|Weekly OverOverbought Level|
|v_input_8|2|weeklyRsiLength|
|v_input_9|false|Enable MA Filter|
|v_input_10|100|WMA Length|
|v_input_11|4|Exit RSI Length|
|v_input_12|4|Daily RSI Length|
|v_input_13|false|Enable 2nd RSI Filter|
|v_input_14|14|2nd RSI Filter Length|
|v_input_15|20|2nd RSI Filter Oversold Level|
|v_input_16|true|Enable ATR Filter|
|v_input_17|14|Number of Days ATR Average|
|v_input_18|2|ATR Filter Factor|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-06 00:00:00
end: 2024-02-05 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// Lets connect on LinkedIn (https://www.linkedin.com/in/lets-grow-with-quality/)
// Optimized for S&P500 Daily. Use it as a buy confirmation on certain levels (Springs, Pullbacks, ...) or let it run 
// without "Weekly RSI Filter" and pyramiding for 4 x more trades.
// This strategy is optimized for minimum drawdowns and has several filters on board for use on different securities

strategy("S&P500 RSI2 Studio", overlay=true)

baseLength = input(2, title="Base RSI Length")
overSold = input(10, title="Overbought Level")
overBought = input(90, title="Oversold Level")
overBoughtExit = input(70, title="Overbought Level Exit")
enableWeeklyRsiFilter = input(true, title="Enable Weekly RSI Filter")
weeklyOverSold = input(30, title="Weekly Oversold Level")
weeklyOverBought = input(70, title="Weekly OverOverbought Level")
weeklyRsiLength = input(2, title="weeklyRsiLength")

enableWmaFilter = input(false, title="Enable MA Filter")
wmaLength = input(100, title="WMA Length")

exitRsiLength = input(4, title="Exit RSI Length")
dailyRsiLength = input(4, title="Daily RSI Length")

enable2ndRSIFilter = input(false, title="Enable 2nd RSI Filter")
SecRSIFilterLengh = input(14, title="2nd RSI Filter Length")
SecRSIFilterOverSold = input(20, title="2nd RSI Filter Oversold Level")

enableAtrFilter = input(true, title="Enable ATR Filter")
numAtrDays = input(14, title="Number of Days ATR Average")
atrFilterFactor = input(2, title="ATR Filter Factor")

weeklyRsi = request.security(syminfo.tickerid, "W", ta.wma(ta.rsi(close, weeklyRsiLength), 1))
exitRsi = request.security(syminfo.tickerid, "D", ta.wma(ta.rsi(close, exitRsiLength), 2))
dailyRsi = request.security(syminfo.tickerid, "D", ta.wma(ta.rsi(close, dailyRsiLength), 2))
price = close

priceDropCondition = ta.atr(1) >= ta.atr(numAtrDays) * atrFilterFactor
preventEarlyEntry = not priceDropCondition

vrsi = ta.wma(ta.rsi(price, baseLength), 2)
wma = ta.wma(price, wmaLength)


buyCond1 = ta.crossunder(vrsi, overSold)
buyCond2 = enableWeeklyRsiFilter ? weeklyRsi < weeklyOverSold : true
buyCond3 = enable2ndRSIFilter ? ta.wma(ta.rsi(close, SecRSIFilterLengh),2) < SecRSIFilterOverSold : true
buyCond4 = enableWmaFilter ? price > ta.wma(close, wmaLength) : true
buyCond5 = enableAtrFilter ? preventEarlyEntry : true
 
buy = buyCond1 and buyCond2 and buyCond3 and buyCond4 and buyCond5

if (not na(vrsi))
    if buy 
        strategy.entry("RSI2 Studio", strategy.long, comment="Long")

if (exitRsi > overBoughtExit)
    strategy.close("RSI2 Studio", comment="Close Long")
```

> Detail

https://www.fmz.com/strategy/441158

> Last Modified

2024-02-06 11:47:59
