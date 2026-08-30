
> Name

Quantitative trading strategy Up-versus-Down-Close-Candles-Strategy-with-EMA-filter-and-Session-Timeframes based on K-line closing price long and short comparison and EMA filtering
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1a29f85af8c63fac3db.png)
[trans]

## 1. Strategy Overview
The name of this strategy is "Quantitative trading strategy based on K-line closing price long and short comparison and EMA filtering". This strategy counts the number of long K-lines and short K-lines composed of the closing prices of K-lines within a certain period in the recent period, combined with EMA filtering, to determine long and short signals when it meets the trading time period.
## 2. Strategy principles
The core logic of this strategy is to count the number of K-lines upCloseCount and the number of K-lines that closed down in the recent lookback period. At the same time, the EMA indicator is used to determine the price trend and serves as a filter. Only when the price is higher than the EMA will long be considered, and only when the price is lower than the EMA will short be considered. In addition, the strategy also sets the trading time periods session1 and session2, and only trades within these two time periods.
The specific judgment logic is:
Long signal trigger conditions: inSession is true (within the trading time period) and upCloseCount > downCloseCount (the number of rising closing K lines is larger) and close > ema (the closing price is higher than EMA) and currentSignal is not "long" (currently no position)
Short signal trigger conditions: inSession is true and downCloseCount > upCloseCount (the number of falling closing K lines is larger) and close < ema (the closing price is lower than EMA) and currentSignal is not "short" (currently there is no position)
## 3. Analysis of strategic advantages
1. Determine price trends and market psychology by counting long and short comparisons of K-line closing prices within a certain historical period, which has a certain trend following effect.
2. Use EMA indicators to filter price trends to avoid erroneous transactions in volatile markets.
3. Set a specific trading time period to avoid trading in noisy market conditions during non-main trading time periods.
4. Consider the balance between trends and frequent trading
## 4. Strategic Risk Analysis
1. In a sideways market, the long and short positions of the closing price are more likely to be misled, leading to unnecessary losses.
2. Improper setting of EMA parameters will also lead to poor filtering effect.
3. If the trading time period is not set properly, a large number of trading opportunities will be lost or transactions will be made by mistake.
4. Gap prices caused by emergencies cannot be effectively tracked
Countermeasures:
1. Optimize EMA parameters and find the best balance
2. Optimize trading time periods
3. Combine with stop loss strategy to control single loss
## 5. Strategy optimization direction
1. Optimize the trading time period and find the best trading time period
2. Optimize parameters for EMA period and smoothness
3. Add a stop loss mechanism based on ATR
4. Add an identification module for emergencies to avoid the risk of gap market conditions
5. Consider combining with other indicators to find better filtering entry conditions
6. Test the performance differences of different varieties and adjust parameters according to the differences
## 6. Summary
This strategy counts the number of long and short K-lines composed of K-line closing prices within a certain historical period, and combines the filtering effect of the EMA indicator to identify trend signals in a specific trading time period. It has a certain trend tracking effect. However, there is also a certain risk of mistaken trading, which needs to be improved through parameter optimization, stop loss strategies, signal filtering and other methods, and the effect can be verified in backtesting.
|| 

## 1. Strategy Overview  

This strategy is named "Up versus Down Close Candles Strategy with EMA filter and Session Timeframes". It counts the number of up close and down close candles in a certain lookback period to determine the market sentiment, combined with EMA filter and trading in specific sessions, to identify long and short signals.  

## 2. Strategy Logic  

The core logic is to count the number of up close candles (upCloseCount) and down close candles (downCloseCount) in the recent lookback period. If upCloseCount is larger, it indicates a bullish market. If downCloseCount is larger, it indicates a bearish market. EMA indicator is used as a filter, only considering long when price > EMA, and short when price < EMA. It also sets session1 and session2 as trading sessions.  

Detailed logic:  

Long signal triggers when: inSession is true (in trading sessions) and upCloseCount > downCloseCount (more up close candles) and close > ema (close price higher than EMA) and currentSignal is not "long" (no existing position).   

Short signal triggers when: inSession is true and downCloseCount > upCloseCount (more down close candles)  and close < ema (close price lower than EMA) and currentSignal is not "short" (no existing position).

## 3. Advantage Analysis   

1. Captures market sentiment and trend by comparing up close/down close candles history   
2. Use EMA filter to avoid trading in ranging markets  
3. Avoid noise in non-major trading hours by setting sessions  
4. Balance between trend following and trading frequency  

## 4. Risk Analysis

1. Can be misled in sideways markets  
2. Improper EMA parameter may cause ineffective filter
3. Missing opportunities if session set inappropriately  
4. Unable to capture gap caused by events

Solutions:
1. Optimize EMA parameter  
2. Optimize trading sessions   
3. Add stop loss based on ATR  
4. Identify events, avoid gaps

## 5. Optimization Directions  

1. Optimize trading sessions  
2. Optimize EMA parameters  
3. Add ATR based stop loss  
4. Identify events, avoid gaps  
5. Combining with other indicators for better filter  
6. Test and adjust across products

## 6. Summary  

This strategy identifies trend signals by comparing up close and down close candles and using EMA filter, within preset trading sessions. It has some trend following effect but also risks of false signals. Improve by optimizing parameters, adding stop loss, enhancing filters etc. Evaluate thoroughly in backtest.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Lookback Period|
|v_input_2|50|EMA Period|
|v_input_3|0900-1200|Time Frame 1 Session|
|v_input_4|1300-1600|Time Frame 2 Session|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-26 00:00:00
end: 2023-12-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Up vs Down Close Candles Strategy with EMA and Session Time Frames", shorttitle="UvD Strat EMA Session", overlay=true)

// User input to define the lookback period, EMA period, and session strings for time frames
int lookback = input(20, title="Lookback Period")
int emaPeriod = input(50, title="EMA Period")
string session1 = input("0900-1200", title="Time Frame 1 Session")
string session2 = input("1300-1600", title="Time Frame 2 Session")

// Calculate the EMA
float ema = ta.ema(close, emaPeriod)

// State variable to track the current signal
var string currentSignal = na

// Counting up-close and down-close candles within the lookback period
int upCloseCount = 0
int downCloseCount = 0

if barstate.isnew
    upCloseCount := 0
    downCloseCount := 0
    for i = 0 to lookback - 1
        if close[i] > close[i + 1]
            upCloseCount += 1
        else if close[i] < close[i + 1]
            downCloseCount += 1

// Define the long (buy) and short (sell) conditions with EMA filter and session time frame
bool inSession = time(timeframe.period, session1) or time(timeframe.period, session2)
bool longCondition = inSession and upCloseCount > downCloseCount and close > ema and currentSignal != "long"
bool shortCondition = inSession and downCloseCount > upCloseCount and close < ema and currentSignal != "short"

// Enter or exit the market based on conditions
if longCondition
    currentSignal := "long"
    strategy.entry("Buy", strategy.long)

if shortCondition
    currentSignal := "short"
    strategy.entry("Sell", strategy.short)

// Exit logic for long and short positions
if currentSignal == "long" and strategy.position_size <= 0
    strategy.close("Sell")

if currentSignal == "short" and strategy.position_size >= 0
    strategy.close("Buy")

plot(ema, color=color.blue, title="EMA")

```

> Detail

https://www.fmz.com/strategy/436755

> Last Modified

2023-12-27 14:38:28
