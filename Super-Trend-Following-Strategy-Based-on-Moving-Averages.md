
> Name

Multiple Moving Average Trend Following Strategy Super-Trend-Following-Strategy-Based-on-Moving-Averages
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/29839fdb7f8d5df86edbc3b5dbfa99e2677bd21875b0d03b5e6ae815200ae9fb.png)
[trans]
## Overview
This strategy is a typical trend following strategy. It uses multiple sets of moving averages of different periods to determine market trends, enter the market when the trend is established, and exit when the short-term trend reverses.
## Strategy Principle
This strategy uses 4 sets of moving averages: 9-day line, 21-day line, 50-day line and 200-day line. They respectively represent different time dimensions.
When the short-term moving average breaks through the long-term moving average from bottom to top, the market is considered to be in an upward trend; when the short-term moving average falls below the long-term moving average from top to bottom, the market is considered to be in a downward trend.
The strategy uses the 9-day line as a reference to determine the arrangement relationship of several other moving averages to determine the overall trend direction. The specific logic is:
Long entry conditions: closing price > 9-day line and 9-day line > 21-day line and 21-day line > 50-day line and 50-day line > 200-day line
Short entry conditions: closing price < 9-day line and 9-day line < 21-day line and 21-day line < 50-day line and 50-day line < 200-day line
Among them, the relationship between the closing price and the 9-day line determines the short-term trend, the relationship between the 9-day line and the 21-day line determines the short-term trend, the relationship between the 21-day line and the 50-day line determines the mid-term trend, and the relationship between the 50-day line and the 200-day line determines the long-term trend. Only when the relationships between the four sets of moving averages are consistent, the market trend is judged to be established and a trading signal is issued.
Exit conditions: If the closing price falls below the 21-day moving average, all long orders will be closed; if the closing price rises above the 21-day moving average, all short orders will be closed.
## Strategic Advantages
1. Using multiple sets of moving averages to determine trends can effectively filter out the market noise of non-mainstream trends and capture medium and long-term trends.
2. The entry conditions are strict, and trend judgments in multiple time dimensions need to be effective to avoid being trapped by short-term adjustments.
3. Stop losses promptly and effectively control risks.
## Risks and Solutions
1. In the long-term sideways market, it is easy to generate a large number of false signals, thereby increasing trading risks. By optimizing parameters, you can adjust the number of periods of the moving average and filter out some noise.
2. In violent market conditions, the moving average often crosses or crosses yellow. At this time, other factors need to be combined to determine the true trend. You can add indicators such as RSI and MACD for confirmation to avoid missing the big market trend.
## Optimization direction
1. Parameter optimization. Different parameter combinations can be tested to find the optimal parameters. Such as adjusting the number of periods of the moving average, adding or adjusting stop loss conditions, etc.
2. Add quality filtering. For example, when entering the market, judge whether the trading volume is enlarged to avoid short jumps due to insufficient volume. Or judge whether the fluctuation is amplified to avoid shock consolidation.
3. Add other technical indicator confirmations to avoid sending wrong signals in violent market conditions. You can consider adding RSI, MACD and other indicators to make multi-factor judgments.
## Summarize
Overall, this strategy is a typical and practical trend following strategy. It uses multiple sets of moving averages to determine trends, has strict entry conditions, and can effectively lock in medium and long-term trends. At the same time, combined with timely stop loss, you can control risks. Through parameter optimization and adding confirmation indicators, the stability and profitability of the strategy can be further improved. It is suitable for investors who like to follow trends for long-term operations.
||

## Overview  

This strategy is a typical trend following strategy. It uses multiple sets of moving averages with different periods to determine the market trend. It enters the market when the trend is established and exits when the short-term trend reverses.   

## Strategy Principle

The strategy employs 4 groups of moving averages: 9-day, 21-day, 50-day and 200-day lines. They represent different timeframes respectively.  

When the short-term moving average crosses over the long-term one upwards, it is determined that the market enters an uptrend. When it crosses downwards, the market is seen to be in a downtrend.   

The strategy takes the 9-day MA as a reference to observe the alignment of the other MAs, thereby judging the overall trend direction. Specifically, the logic is:

Long entry conditions: Close > 9-day MA and 9-day MA > 21-day MA and 21-day MA > 50-day MA and 50-day MA > 200-day MA.  

Short entry conditions: Close < 9-day MA and 9-day MA < 21-day MA and 21-day MA < 50-day MA and 50-day MA < 200-day MA.  

Here the relationship between close price and 9-day MA determines the shortest-term trend, while that between 9-day and 21-day MA judges short-term trend, 21-day and 50-day medium-term trend, 50-day and 200-day long-term trend. Only when the relationships of all the four MA pairs conform can a valid trend be established to generate trading signals.   

Exit conditions: close price crosses below 21-day MA, flatten all long positions; crosses above 21-day MA, flatten all short positions.   

## Advantages of the Strategy   

1. Adopting multiple MAs to determine the trend can filter out market noises from non-mainstream moves and capture medium-to-long term trends.  

2. Strict entry conditions require valid judgments across different timeframes, avoiding being trapped by short-term corrections.  

3. Timely stop loss helps effectively control risks.    

## Risks and Solutions 

1. In long-term rangebound markets, excessive false signals may occur and increase trading risks. This can be avoided by optimizing parameters and adjusting MA periods to filter out some noises.  

2. During violent trends, MA crosses happen frequently. Other factors are needed then to determine real trend, e.g. combining indicators like RSI and MACD for confirmation, in case strong moves are missed.  

## Optimization Directions   

1. Parameter optimization. Test different parameter combinations to find out the optimum. Such as adjusting MA periods, adding or modifying stop loss criteria etc.  

2. Improve quality filter. For instance, check if volume surges on entry to avoid insufficient momentum, or examine volatility to avoid oscillations.  

3. Introduce confirmation from more technical indicators to avoid wrong signals amid fierce market moves. Consider applying tools like RSI and MACD for multi-factor decision-making.  

## Summary   

Overall this is a typical and practical trend following strategy. It adopts multiple MAs to determine trends, has strict entry rules to lock in medium-to-long term trends. Together with timely stop loss, it helps control risks. Further improvements on stability and profitability can be achieved through ways like parameter optimization and adding confirmation indicators. It suits investors who prefer following the trend for long-term trading.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|rsi-length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-29 00:00:00
end: 2024-02-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © shayak1

//@version=5
strategy('Super SR', overlay=true)

r = input.int(14,"rsi-length",1,100)
rsi = ta.rsi(close,r)

len1 = 9
len2 = 21
len3 = 50
len4 = 200

ema1 = ta.ema(close, len1)
ema2 = ta.ema(close, len2)
ema3 = ta.ema(close, len3)
ema4 = ta.ema(close, len4)

plot(ema1,color= color.green)
plot(ema2,color= color.yellow)
plot(ema3,color= color.orange)
plot(ema4,color= color.red)


// *** entries 
Long1 = close > ema1
Long2 = ema1 > ema2
Long3 = ema2 > ema3
Long4 = ema3 > ema4
buy_condition = Long1 and Long2 and Long3 and Long4 and strategy.position_size == 0

if (buy_condition and strategy.position_size <= 1)
    strategy.entry("B", strategy.long)

Short1 = close < ema1
Short2 = ema1< ema2
Short3 = ema2< ema3
Short4 = ema3< ema4
sell_condition = Short1 and Short2 and Short3 and Short4 and strategy.position_size == 0

//if (sell_condition)
//    strategy.entry("S", strategy.short)

// trailing SL
//Long_sl = min(strategy.position_avg_price * 0.95, strategy.pos


//EXIT CONDITIONS

exit_long = ta.crossunder(close, ema2)
exit_short = ta.crossover(close, ema2)

if(exit_long)
    strategy.close("B", "LE", qty_percent=100)
if(exit_short)
    strategy.close("S", "SE", qty_percent=100)

//==============================================================================
//INSERT SECTION
//This section is where users will be required to insert the indicators they
//would like to use for their NNFX Strategy.
//==============================================================================
//INSERT - CONFIRMATION INDICATOR 1
//==============================================================================


//==============================================================================
//INSERT - CONFIRMATION INDICATOR 2
//==============================================================================


//==============================================================================
//INSERT - VOLUME INDICATOR
//==============================================================================


//==============================================================================
//INSERT - BASELINE INDICATOR
//==============================================================================


//==============================================================================
//INSERT - EXIT INDICATOR
//==============================================================================


//==============================================================================
//INSERT - CONTINUATION TRADES INDICATOR
//==============================================================================


//==============================================================================
//COMPLETED SECTION
//This section has been optimised to work with the above indicators the user
//has inserted above. The user does not require to change any code below and
//is completed and optimised for the full NNFX strategy. Users may wish to 
//customise this section of code if they wish to alter the NNFX strategy.
//==============================================================================
//COMPLETE - BACKTEST DATE RANGE
//==============================================================================
// start_day = input.int(1,"start day",1,31)
// start_month = input.int(1,"start month",1,12)
// start_year = input.int(1,"start year",2010,2023)



//==============================================================================
//COMPLETE - CURRENCY CONVERSION
//==============================================================================


//==============================================================================
//COMPLETE - ATR MONEY MANAGEMENT
//==============================================================================


//==============================================================================
//COMPLETE - USER INPUT CONDITIONS - C1
//==============================================================================


//==============================================================================
//COMPLETE - USER INPUT CONDITIONS - C2
//==============================================================================


//==============================================================================
//COMPLETE - USER INPUT CONDITIONS - Vol
//==============================================================================


//==============================================================================
//COMPLETE - USER INPUT CONDITIONS - Bl
//==============================================================================


//==============================================================================
//COMPLETE - USER INPUT CONDITIONS - Exit
//==============================================================================


//==============================================================================
//COMPLETE - CONTINUATION TRADES
//==============================================================================


//==============================================================================
//COMPLETE - ONE CANDLE RULE
//==============================================================================


//==============================================================================
//COMPLETE - BRIDGE TOO FAR
//==============================================================================


//==============================================================================
//COMPLETE - BASELINE AND ATR RULE
//==============================================================================


//==============================================================================
//COMPLETE - ENTRY CONDITIONS
//==============================================================================


//==============================================================================
//COMPLETE - ENTRY ORDERS
//==============================================================================


//==============================================================================
//COMPLETE - TAKE PROFIT AND STOP LOSS CONDITIONS
//==============================================================================


//==============================================================================
//COMPLETE - EXIT ORDERS
//==============================================================================


//==============================================================================
//COMPLETE - CLOSE ORDERS
//==============================================================================


//==============================================================================
```

> Detail

https://www.fmz.com/strategy/441058

> Last Modified

2024-02-05 11:10:41
