
> Name

Short-term-Trading-Strategy-Based-on-Trend-Following
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy achieves short-term trading with loss control by identifying strong trends and favorable opportunities. The strategy tracks the trend signal when the price breaks through the simple moving average, and promptly stops losses and profits when the RSI deviates from the overbought and oversold zones to capture short-term price rises and falls.
## Strategy Principle
1. Calculate multi-period simple moving average
- Set SMA of 9-day line, 50-day line and 100-day line respectively    
- The short period line crosses the long period line to determine the trend direction
2. RSI indicator determines overbought and oversold
- Set the RSI length to 14 periods    
- RSI above 70 is overbought, below 30 is oversold    
3. Enter when the price breaks through the 9-day moving average
- Go long when the price breaks above the 9-day moving average    
- Go short when the price falls below the 9-day moving average    
4. Stop loss and take profit when RSI divergence THENJournal is formed
- RSI divergence price action stop loss
- Take profit when RSI reaches the set parameter
## Advantage Analysis
- Track short-term trends, suitable for high-frequency trading
- Moving average combination determines the trend direction and avoids wrong transactions
- RSI indicator determines timing and can effectively control risks
- Flexible stop loss and profit, lock in short-term profits
- Combined with indicator signals to improve strategy stability
## Risk Analysis
- The short-term trend judgment may be wrong, chasing highs and selling lows
- RSI generates false signals and expands losses
- Improper setting of stop-loss and take-profit parameters can reduce profits or increase losses.
- Transaction frequency is too high, increasing transaction costs and slippage
- Parameter failure and abnormal market impact strategy effects
- Optimize parameter settings, strictly stop losses, and consider cost control
## Optimization direction
- Test different moving average combinations to optimize the judgment effect
- Consider other indicators such as STOCH to verify RSI signals
- Add machine learning to determine the effectiveness of breakthroughs
- Adjust parameters for different products and trading sessions
- Optimize stop loss and take profit logic to achieve dynamic tracking
- Consider integrating automatic parameter adjustment mechanism
## Summarize
This strategy integrates the advantages of moving average indicators and RSI indicators to achieve a conservative short-term trading strategy. Through parameter optimization, signal verification, risk control, etc., the strategy is more perfect and can adapt to market changes to achieve sustainable results. You can continue to expand the moving average combination, add machine learning and other methods to improve the strategy effect, and become more mature through continuous optimization.
||


## Overview

This strategy identifies strong trends and favorable timing for short-term trading with loss control. It tracks price breakouts of simple moving averages as trend signals and sets stop loss/take profit based on RSI divergences to capture short-term price movements.

## Strategy Logic

1. Calculating multi-period simple moving averages  

    - Setting 9-day, 50-day and 100-day SMAs
    
    - Short SMA crossing long SMA indicates trend direction

2. Judging overbought/oversold levels using RSI

    - RSI length is 14 periods
    
    - RSI above 70 is overbought, below 30 is oversold
    
3. Entering trades when price breaks 9-day SMA

    - Go long when price breaks above 9-day SMA
    
    - Go short when price breaks below 9-day SMA

4. Setting stop loss/take profit based on RSI divergences

    - RSI divergence for stop loss

    - Take profit when RSI reaches preset levels

## Advantage Analysis   

- Captures short-term trends, suitable for high frequency trading

- SMA combos filter trend signals, avoiding bad trades

- RSI helps determine timing, effectively control risks

- Flexible stop loss/take profit locks short-term profits

- Combining indicators improves stability 

## Risk Analysis

- Inaccurate short-term trend judgment causes chasing

- False RSI signals expand losses

- Improper stop loss/take profit settings reduce profit or magnify losses

- High trading frequency increases costs and slippage 

- Ineffective parameters and abnormal markets impact strategy

- Optimize parameters, strict stop loss, manage costs

## Optimization Directions

- Test different SMA combos to improve trend judgment 

- Consider additional indicators like STOCH to verify RSI signals

- Employ machine learning to determine valid breakouts

- Adjust parameters for different products and sessions

- Optimize stop loss/take profit logic for dynamic trailing

- Explore auto parameter tuning mechanisms

## Conclusion

This strategy combines SMA and RSI for a conservative short-term trading approach. Fine-tuning parameters, validating signals, controlling risks makes it more robust and adaptive. There is room for improvement by exploring more SMA combos, adding machine learning models etc. Continuous optimization will lead to further maturity.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|10|From Day|
|v_input_3|2019|From Year|
|v_input_4|true|Thru Month|
|v_input_5|true|Thru Day|
|v_input_6|2112|Thru Year|
|v_input_7|true|Show Date Range|
|v_input_8|9|v_input_8|
|v_input_9|50|v_input_9|
|v_input_10|100|v_input_10|
|v_input_11|70|TP|
|v_input_12|30|SL|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-27 00:00:00
end: 2023-09-26 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=4
strategy(shorttitle='Maximized Scalping On Trend',title='Maximized Scalping On Trend (by Coinrule)', overlay=true, initial_capital = 1000, process_orders_on_close=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 30, commission_type=strategy.commission.percent, commission_value=0.1)

//Backtest dates
fromMonth = input(defval = 1,    title = "From Month",      type = input.integer, minval = 1, maxval = 12)
fromDay   = input(defval = 10,    title = "From Day",        type = input.integer, minval = 1, maxval = 31)
fromYear  = input(defval = 2019, title = "From Year",       type = input.integer, minval = 1970)
thruMonth = input(defval = 1,    title = "Thru Month",      type = input.integer, minval = 1, maxval = 12)
thruDay   = input(defval = 1,    title = "Thru Day",        type = input.integer, minval = 1, maxval = 31)
thruYear  = input(defval = 2112, title = "Thru Year",       type = input.integer, minval = 1970)

showDate  = input(defval = true, title = "Show Date Range", type = input.bool)

start     = timestamp(fromYear, fromMonth, fromDay, 00, 00)        // backtest start window
finish    = timestamp(thruYear, thruMonth, thruDay, 23, 59)        // backtest finish window
window()  => true      // create function "within window of time"

//MA inputs and calculations
movingaverage_fast = sma(close, input(9))
movingaverage_mid= sma(close, input(50))
movingaverage_slow = sma(close, input (100))


//Trend situation
Bullish= cross(close, movingaverage_fast)

Momentum = movingaverage_mid > movingaverage_slow

// RSI inputs and calculations
lengthRSI = 14
RSI = rsi(close, lengthRSI)

//Entry
strategy.entry(id="long", long = true, when = Bullish and Momentum and RSI > 50)

//Exit

TP = input(70)
SL =input(30)
longTakeProfit  = RSI > TP
longStopPrice = RSI < SL

strategy.close("long", when = longStopPrice or longTakeProfit and window())

plot(movingaverage_fast, color=color.black, linewidth=2 )
plot(movingaverage_mid, color=color.orange, linewidth=2)
plot(movingaverage_slow, color=color.purple, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/427996

> Last Modified

2023-09-27 16:56:34
