
> Name

Support-and-Resistance-Strategy-with-Volume-Breakout-and-Trailing-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/177c5bdb71e581a2b8a.png)
[trans]

## Overview
The main idea of ​​this strategy is to determine the entry timing by combining support and resistance levels and breakthroughs in trading volume, and use the ATR indicator to dynamically adjust the stop-loss tracking price after making profits, thereby obtaining more potential profits.
## Strategy Principle
This strategy mainly consists of the following parts of logic:
1. Use the ta.pivothigh and ta.pivotlow functions to calculate the highest price of the L_Bars K-line and the lowest price of the R_Bars K-line as resistance and support lines.
2. When the closing price crosses the resistance line and the trading volume breaks through the volumeRange threshold, go long; when the closing price goes below the support line and the trading volume breaks through the volumeRange threshold, go short.
3. After going long, use close-ATR_LO as the long stop loss; after going short, use close+ATR_SH as the short stop loss to dynamically adjust the trailing stop loss.
4. During the trading hours (0915-1445), make the first trading signal every day. No new orders will be opened after the profit or loss reaches the risk limit.
## Strategic Advantages
1. Use support and resistance theory, combined with trading volume indicators, to make entry timing more precise.
2. Use the ATR indicator to track the stop loss, which can flexibly adjust the stop loss position according to the degree of market fluctuations and reduce the possibility of profit taking after making a profit.
3. Appropriately controlling the number of transactions in a single day and the risk of a single transaction can help grasp the trend and avoid excessive stop losses.
## Strategy Risk
1. Support and resistance may fail and fail to provide effective entry signals.
2. If the ATR indicator is set too large, the stop loss distance may be too far, increasing the risk of loss.
3. If the trading volume indicator is set too small, it may lead to missed opportunities; if it is set too large, it may lead to misjudgment of signals.
**Solution:**
- Adjust support and resistance parameters according to the characteristics of different varieties
- Optimize ATR multiple and volume threshold parameters
- Combine with other indicators to determine the timing of entry
## Strategy optimization direction
1. Combine with other indicators to determine the timing of entry, such as moving averages, etc.
2. Optimize ATR multiple and trading volume threshold parameters
3. Combined with machine learning algorithms to achieve dynamic parameter optimization
4. Expand to other varieties and find parameter patterns
## Summarize
This strategy integrates a variety of analysis tools and achieves better results in the backtesting stage through the use of support, resistance, trading volume and stop loss methods. However, there may be more uncertainties in the real offer, and it is necessary to further enhance the performance of the real offer through parameter optimization and the introduction of other judgment indicators. Overall, the strategy is clear and easy to understand, and provides a good reference case for quantitative trading strategies.
||

## Overview

The main idea of this strategy is to combine support/resistance levels and volume breakouts to determine entry signals, and use the ATR indicator to dynamically adjust stop loss for profit taking, in order to capture more potential profits.

## Strategy Logic

The strategy consists of the following main logics:

1. Use ta.pivothigh and ta.pivotlow to calculate the highest price of previous L_Bars candles and the lowest price of previous R_Bars candles, as resistance and support levels.  

2. When close price crosses above resistance level and volume breaks above the volumeRange threshold, go long. When close price crosses below support level and volume breaks above the volumeRange threshold, go short.

3. After long entry, set stop loss at close-ATR_LO. After short entry, set stop loss at close+ATR_SH. This realizes dynamic trailing stop loss adjustment.

4. Only take the first signal within trading hours (0915-1445) each day. No new orders after reaching the daily risk limit defined by risk input.

## Advantage Analysis

1. Use support/resistance theory combined with volume indicator to improve entry accuracy. 

2. Trailing stop loss based on ATR can flexibly adjust stop level based on market volatility, lowering the chance of profit retracement.  

3. Appropriate control over daily trade times and per trade risk helps to catch the trend and avoid excessive stop loss.

## Risk Analysis

1. Support/resistance levels may fail and unable to provide effective entry signals.  

2. ATR multiplier set too high may lead to stop loss being too far away, increasing loss risk.

3. Volume threshold set too low may miss opportunities, too high may cause false signals.

**Solutions:**

- Adjust support/resistance parameters based on different products’ characteristics. 

- Optimize ATR multiplier and volume threshold parameters.

- Add other indicators to confirm entry signals.

## Optimization Directions

1. Add other indicators like moving averages to assist in determining entry signals.

2. Optimize parameters like ATR multiplier and volume threshold.  

3. Use machine learning algorithms to realize dynamic parameter optimization.

4. Expand strategy to other products to find parameter patterns.

## Summary  

The strategy integrates various analytical tools, applying support/resistance, volume, and stop loss methods, and achieved good backtest results. But more uncertainties may exist in live trading, requiring further enhancements like parameter optimization and additional entry confirmation indicators to improve real-world performance. Overall, the strategy has clear logic and easy understanding, providing a good reference case for quantitative trading strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|10|L_Bars|
|v_input_int_2|15|R_Bars|
|v_input_int_3|20|Volume Break [threshold]|
|v_input_int_4|150|PRICE CROSS EMA|
|v_input_float_1|3.2|_ATR LONG|
|v_input_float_2|3.2|_ATR SHORT|
|v_input_float_3|200|RISK|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-03 00:00:00
end: 2024-01-10 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//   ____________                _________                      _____________
//  |____________|             ||________|                      ||__________|
//       ||            ____    ||        ||                     ||                    ______ ________    _____ ________
//       ||    |   || ||       ||________|| |   || ||    ||     ||     |   ||   /\\   |   // |______| || ||    |______|
//       ||    |===|| |===     ||__________ |   || ||    ||     ||     |===||  /__\\  |===      ||    ||   \\     ||
//       ||    |   || ||___    ||        || |___|| ||___ ||___  ||     |   || /    \\ |   \\    ||    || ___||    ||
//       ||                    ||________||                     ||__________
//       ||                    ||________|                      ||__________|
  
//@version=5
strategy("SUPPORT RESISTANCE STRATEGY [5MIN TF]",overlay=true )
L_Bars = input.int(defval = 10, minval = 1 , maxval = 50, step =1)
R_Bars = input.int(defval = 15, minval = 1 , maxval = 50, step =1)
volumeRange = input.int(20, title='Volume Break [threshold]', minval = 1)

// ═══════════════════════════ //
// ——————————> INPUT <——————— //
// ═══════════════════════════ //

EMA1 = input.int(title='PRICE CROSS EMA', defval = 150, minval = 10 ,maxval = 400)
factor1 = input.float(title='_ATR LONG',defval = 3.2 , minval = 1 , maxval = 5 , step = 0.1, tooltip = "ATR TRAIL LONG")
factor2 = input.float(title='_ATR SHORT',defval = 3.2 , minval = 1 , maxval = 5 , step = 0.1, tooltip = "ATR TRAIL SHORT")
risk = input.float(title='RISK',defval = 200 , minval = 1 , maxval = 5000 , step = 50, tooltip = "RISK PER TRADE")


var initialCapital = strategy.equity
t = time(timeframe.period, '0915-1445:1234567')
time_cond = not na(t)

// ══════════════════════════════════ //
// ———————————> EMA DATA <——————————— //
// ══════════════════════════════════ //
ema1 = ta.ema(close, EMA1)

plot(ema1, color=color.new(color.yellow, 0), style=plot.style_linebr, title='ema1')

// ══════════════════════════════════ //
// ————————> TRAIL DATA <———————————— //
// ══════════════════════════════════ //
// *******Calculate LONG TRAIL data*****
ATR_LO = ta.atr(14)*factor1

// *******Calculate SHORT TRAIL data*****
ATR_SH = ta.atr(14)*factor2

long_trail = close - ATR_LO
short_trail = close + ATR_SH

// Plot atr data
//plot(longStop, color=color.new(color.green, 0), style=plot.style_linebr, title='Long Trailing Stop')
//plot(shortStop , color=color.new(color.red, 0), style=plot.style_linebr, title='Short Trailing Stop')

// ══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════ //
// ————————————————————————————————————————————————————————> RESISTANCE/SUPPORT LEVELS DATA <————————————————————————————————————————————————————————————————————————————————————————————— //
// ══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════ //

Resistance_pi = fixnan(ta.pivothigh(L_Bars, R_Bars)[1])
Support_pi = fixnan(ta.pivotlow(L_Bars, R_Bars)[1])
r1 = plot(Resistance_pi, color=ta.change(Resistance_pi) ? na : color.red,  offset=-(R_Bars + 1),linewidth=2, title='RESISTANCE')
s1 = plot(Support_pi, color=ta.change(Support_pi) ? na : color.green, offset=-(R_Bars + 1),linewidth=2, title='SUPPORT')

//Volume 
vol_1 = ta.ema(volume, 5)
vol_2 = ta.ema(volume, 10)
osc_vol = 100 * (vol_1 - vol_2) / vol_2

// ══════════════════════════════════//
// ————————> LONG POSITIONS <————————//
// ══════════════════════════════════//
//******barinstate.isconfirmed used to avoid repaint in real time*******

if ( ta.crossover(close, Resistance_pi) and osc_vol > volumeRange and not(open - low > close - open) and strategy.opentrades==0 and barstate.isconfirmed and time_cond and close >= ema1 )
    strategy.entry(id= "Long" ,direction = strategy.long, comment = "BUY")
    
plot(long_trail , color=color.new(color.blue, 0), style=plot.style_linebr, title='long Stop')

if strategy.position_size > 0 
    strategy.exit("long tsl", "Long" , stop = long_trail ,comment='SELL')
 
// ═════════════════════════════════════//
// ————————> SHORT POSITIONS <————————— //
// ═════════════════════════════════════//
if ( ta.crossunder(close, Support_pi) and osc_vol > volumeRange and not(open - close < high - open)  and strategy.opentrades==0 and barstate.isconfirmed and time_cond and close <= ema1 )
    strategy.entry(id = "Short" ,direction = strategy.short,  comment = "SELL") 

if strategy.position_size < 0
    strategy.exit("short tsl", "Short" ,  stop = short_trail ,comment='BUY')

// ════════════════════════════════════════════════//
// ————————> CLOSE ALL POSITIONS BY 3PM <————————— //
// ════════════════════════════════════════════════//
strategy.close_all(when = hour == 14 and minute == 55)

// ════════════════════════════════════════//
// ————————> MAX INTRADAY LOSS  <————————— //
// ════════════════════════════════════════//
// strategy.risk.max_intraday_loss(type = strategy.cash, value = risk)


```

> Detail

https://www.fmz.com/strategy/438379

> Last Modified

2024-01-11 17:58:26
