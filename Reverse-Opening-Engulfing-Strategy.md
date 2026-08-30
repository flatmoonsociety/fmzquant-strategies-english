
> Name

Reverse-Opening-Engulfing-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12918e9fcf2d93d72e9.png)
[trans]
## Overview
The reverse opening engulfing strategy is a simple intraday trading strategy based on a stock's first candlestick. The core idea of ​​this strategy is to determine the direction of the rise or fall when the first K line appears after the market opens each day, and make reverse operations. If the first K line is a red Yang line, go long; if the first K line is a green Yin line, go short. This strategy also sets up stop-loss and take-profit exit mechanisms.
## Strategy Principle
The principle of this strategy is based on the particularity of the first K line after the opening. At the opening of the market, the power confrontation between the long and short sides is the most intense, and the probability of a market reversal is high. Determining the rise and fall direction of the first K-line and doing the opposite is the core idea of ​​this strategy.
Specifically, after the opening of a new day, the strategy will record the opening price, closing price, and rise and fall of the first K line. If the opening price is higher than the closing price (green negative line), it means the short side wins, so go long; if the opening price is lower than the closing price (red positive line), it means the long side wins, then go short. Through such reverse operations, the strategy attempts to hunt for reversal opportunities after the opening.
At the same time, the strategy also sets up a stop-loss and take-profit mechanism, including a long stop-loss price, a long take-profit price, a short stop-loss price, and a short take-profit price, to control the risk and profit of long and short positions to avoid excessive losses or premature cutting.
## Advantage Analysis
The reverse opening engulfing strategy has the following advantages:
1. The idea is simple and clear, easy to understand and implement.
2. Take advantage of the high predictive value characteristics of the opening period to seize the reversal opportunity.
3. Set stop loss and stop profit at the same time to effectively control risks.
4. The strategic ideas are universal and applicable to most stocks.
5. Participation costs are low and funds are easy to control.
## Risk Analysis
The reverse opening engulfing strategy also has certain risks, which mainly include:
1. The probability of failure of the opening reversal. If the reversal signal of the first K line fails, it may cause large losses.
2. Unable to effectively filter low-quality stocks. This strategy does not provide sufficient fundamental analysis of stocks and may select some bad stocks with poor fundamentals.
3. Unable to effectively control the systemic risks of emergencies, such as the impact of major negative news.
4. Improper stop-loss and stop-profit settings may cause losses to expand or profits to shrink.
## Optimization direction
The reverse opening engulfing strategy can be optimized from the following aspects:
1. Add validity testing of opening reversal signals to avoid invalid signals. For example, combined with trading volume analysis.
2. Combine stock fundamentals and technical indicators to select stock pools and filter out low-quality stocks.
3. Add a monitoring module for major events and news to control systemic risks.
4. Use genetic algorithms, machine learning and other methods to dynamically optimize the settings of stop loss and profit.
## Summary
The reverse opening engulfing strategy tries to seize the reversal opportunity after the opening by judging the direction of the first K line and making reverse operations. This strategy has a simple idea, low participation cost, and certain practical value. But we must also be clearly aware of the risks involved, and constantly improve and optimize the strategy in practice to make it more robust and reliable.
||

## Overview
The Reverse Opening Engulfing Strategy is a simple intraday trading strategy based on the first candlestick after the opening. The core idea of this strategy is to judge the uptrend or downtrend of the first candlestick when it appears after the opening every day, and take counter operations. If the first candlestick is a red yang line, go long; if the first candlestick is a green yin line, go short. The strategy also sets up stop loss and take profit mechanisms for exiting positions.

## Strategy Logic  
The principle behind this strategy is the peculiarity of the first candlestick after opening. When the market opens, the forces of longs and shorts confront most intensely, and the probability of a reversal is relatively large. Judging the uptrend or downtrend of the first candlestick and taking counter operations is the core idea of this strategy.  

Specifically, after the opening of a new day, the strategy will record the opening price, closing price and price change of the first candlestick. If the opening price is higher than the closing price (green yin line), it means the bears have won and we should long; if the opening price is lower than the closing price (red yang line), it means the bulls have won and we should short. By taking such counter operations, the strategy attempts to capture reversal opportunities after opening.

Meanwhile, the strategy also sets up stop loss and take profit mechanisms, including long stop loss price, long take profit price, short stop loss price and short take profit price, to control risks and profits of long and short positions, avoiding excessive losses or premature profit taking.

## Advantage Analysis
The Reverse Opening Engulfing Strategy has the following advantages:

1. The logic is simple and clear, easy to understand and implement.  
2. It utilizes the high predictive value of the opening segment to capture reversal opportunities.
3. The stop loss and take profit settings can effectively control risks. 
4. The strategy idea has universality and is suitable for most stocks.
5. The participation cost is relatively low and capital control is easy.

## Risk Analysis  
The Reverse Opening Engulfing Strategy also has some risks, mainly including:  

1. Probability of opening reversal failure. A failed reversal signal of the first candlestick may cause huge losses.
2. Inability to effectively filter low-quality stocks. The strategy lacks sufficient fundamental analysis and may pick some stocks with poor fundamentals.  
3. Inability to effectively control systemic risks from black swan events, such as the impact of significantly negative news.  
4. Improper stop loss and take profit settings may lead to magnified losses or narrowed profits.

## Optimization Directions
The Reverse Opening Engulfing Strategy can be optimized in the following aspects:

1. Increase the validity test of opening reversal signals to avoid invalid signals, for example, combine volume analysis.  
2. Select stock pools by integrating fundamental and technical analysis to filter low-quality stocks.
3. Add monitoring modules for major events and news to control systemic risks.  
4. Use genetic algorithms, machine learning and other methods to dynamically optimize stop loss and take profit settings.   

## Summary  
The Reverse Opening Engulfing Strategy attempts to capture reversal opportunities after opening by judging the direction of the first candlestick and taking counter operations. The strategy idea is simple with low participation costs, and has some practical value. But we should also be soberly aware of the risks, and constantly improve and optimize the strategy in practice to make it more robust and reliable.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0915-1455|Market session|
|v_input_2|true|Long Take Profit (%)|
|v_input_3|true|Short Take Profit (%)|
|v_input_4|0.5|Long Stop Loss (%)|
|v_input_5|0.5|Short Stop Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-22 00:00:00
end: 2023-11-21 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © vikris
//@version=4
strategy("[VJ]First Candle Strategy", overlay = true,calc_on_every_tick = true,default_qty_type=strategy.percent_of_equity,default_qty_value=100,initial_capital=750,commission_type=strategy.commission.percent, 
     commission_value=0.02)


// ********** Strategy inputs - Start **********

// Used for intraday handling
// Session value should be from market start to the time you want to square-off 
// your intraday strategy
// Important: The end time should be at least 2 minutes before the intraday
// square-off time set by your broker
var i_marketSession = input(title="Market session", type=input.session, 
     defval="0915-1455", confirm=true)

// Make inputs that set the take profit % (optional)
longProfitPerc = input(title="Long Take Profit (%)",
     type=input.float, minval=0.0, step=0.1, defval=1) * 0.01

shortProfitPerc = input(title="Short Take Profit (%)",
     type=input.float, minval=0.0, step=0.1, defval=1) * 0.01
     
// Set stop loss level with input options (optional)
longLossPerc = input(title="Long Stop Loss (%)",
     type=input.float, minval=0.0, step=0.1, defval=0.5) * 0.01

shortLossPerc = input(title="Short Stop Loss (%)",
     type=input.float, minval=0.0, step=0.1, defval=0.5) * 0.01    


// ********** Strategy inputs - End **********


// ********** Supporting functions - Start **********

// A function to check whether the bar or period is in intraday session
barInSession(sess) => time(timeframe.period, sess) != 0



// Figure out take profit price
longExitPrice  = strategy.position_avg_price * (1 + longProfitPerc)
shortExitPrice = strategy.position_avg_price * (1 - shortProfitPerc)

// Determine stop loss price
longStopPrice  = strategy.position_avg_price * (1 - longLossPerc)
shortStopPrice = strategy.position_avg_price * (1 + shortLossPerc)


// ********** Supporting functions - End **********


// ********** Strategy - Start **********
// See if intraday session is active
bool intradaySession = barInSession(i_marketSession)

// Trade only if intraday session is active

//=================Strategy logic goes in here===========================
 
// If start of the daily session changed, then it's first bar of the new session
isNewDay = time("D") != time("D")[1]
var firstBarCloseValue = close
var firstBarOpenValue = open
if isNewDay
    firstBarCloseValue := close
    firstBarOpenValue := open


greenCandle = firstBarOpenValue < firstBarCloseValue
redCandle = firstBarOpenValue > firstBarCloseValue

buy = redCandle
sell = greenCandle


// plot(firstBarCloseValue)
// plot(firstBarOpenValue)



//Final Long/Short Condition
longCondition = buy
shortCondition =sell
 
//Long Strategy - buy condition and exits with Take profit and SL
if (longCondition and intradaySession)
    stop_level = longStopPrice
    profit_level = longExitPrice
    strategy.entry("My Long Entry Id", strategy.long)
    strategy.exit("TP/SL", "My Long Entry Id", stop=stop_level, limit=profit_level)


//Short Strategy - sell condition and exits with Take profit and SL
if (shortCondition and intradaySession)
    stop_level = shortStopPrice
    profit_level = shortExitPrice
    strategy.entry("My Short Entry Id", strategy.short)
    strategy.exit("TP/SL", "My Short Entry Id", stop=stop_level, limit=profit_level)
 
 
// Square-off position (when session is over and position is open)
squareOff = (not intradaySession) and (strategy.position_size != 0)
strategy.close_all(when = squareOff, comment = "Square-off")

// ********** Strategy - End **********
```

> Detail

https://www.fmz.com/strategy/432901

> Last Modified

2023-11-22 16:05:24
