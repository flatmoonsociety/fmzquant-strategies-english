
> Name

Index moving average closed breakout strategy Dual-EMA-Engulfing-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1eee68568c649a8ace0.png)
[trans]

## Overview
This strategy determines the long and short direction by judging the direction of the exponential moving average. When the positive line generally engulfs the negative line and the trading volume increases, perform long operations. When the direction of the exponential moving average changes or the negative line generally engulfs the positive line, the position closing operation is performed.
## Strategy Principle
1. Use two exponential moving averages with different parameters to determine the market trend direction. When the short-term EMA line is above the long-term EMA line, it is considered a long market, and vice versa is a short market.
2. When the market is in a long state, if the Yang line generally engulfs the previous K line, and the trading volume is 1.2 times greater than the previous K line, a long signal will be generated. This form shows that the bulls are strong and can pursue long positions.
3. When the market trend turns, that is, when the short-term EMA crosses the long-term EMA, it indicates that the strength of the bulls has weakened, and the position should be closed. Or when the negative line generally engulfs the positive line, it shows that short sellers are entering the market in large quantities, and they should also take the initiative to stop losses and close positions.
## Advantage Analysis
1. Using double EMA to determine the market structure can more accurately determine the status of the long and short market.
2. The engulfing pattern shows that unilateral power suddenly enters the market in large quantities, which can capture larger market trends. Combined with the trading volume amplification filter, avoid being delayed by false breakthroughs.
3. There is a stop loss mechanism. By not setting a stop loss position and using market structure changes to stop losses, slippage losses caused by unnecessary stop losses can be reduced.
## Risk Analysis
1. The double EMA judgment of the market structure may also be wrong, thus missing the market or entering long positions randomly. The EMA cycle parameters can be adjusted appropriately.
2. The engulfing pattern is easily misled by the volatile market. You can add more filter conditions to avoid mistaken transactions.
3. Failure to set a stop loss level may lead to greater losses. You can try methods such as break even and stop loss.
## Optimization direction
1. You can combine more indicators to judge long and short, such as MACD, energy tide, etc.
2. You can add a certain range of stop loss levels as appropriate.
3. The EMA cycle parameters can be optimized according to the characteristics of the trading variety.
## Summarize
The overall idea of ​​this strategy is clear and easy to understand. It uses exponential moving averages to determine the structure and engulfing patterns to capture breakthroughs. The advantage is that the judgment logic is simple and the trading signals are clear. But there is also the risk of being stuck. Through further optimization, better returns are expected.
||

## Overview

This strategy determines long/short direction by judging the direction of exponential moving averages (EMA). It goes long when there is a bullish engulfing pattern and enlarged trading volume. It closes position when the direction of EMAs is reversed or a bearish engulfing pattern occurs.

## Strategy Logic

1. Use two EMAs with different parameters to determine market trend. If short EMA is above long EMA, it is a bull market, otherwise it is a bear market.  

2. When the market is bullish, if a bullish engulfing pattern appears and trading volume is 1.2 times greater than previous bar, a long signal is triggered. This pattern shows strong momentum of bulls to follow.

3. When market trend is reversed, i.e. short EMA cross below long EMA, it shows weakening momentum of bulls and existing position should be closed. Also when a bearish engulfing pattern appears, it shows bears are entering with strong momentum, so position should be actively closed with stop loss.

## Advantage Analysis 

1. Using dual EMAs to determine market structure can accurately judge bull/bear status.

2. Engulfing pattern shows one side momentum suddenly increases, which can capture major trends. Combining with enlarged volume filter avoids being misled by fake breakouts.  

3. It has a stop loss mechanism. By not setting stop loss price but using market structure reversal to stop loss, unnecessary slippage can be reduced.

## Risk Analysis

1. Dual EMAs may also incorrectly judge market structure, thus missing trends or wrongly going long. EMA periods can be adjusted.

2. Engulfing patterns can be misled by ranging markets. More filters can be added to avoid false trades.  

3. Not having stop loss price may lead to larger losses. Other stop loss methods like break even can be tested.

## Optimization Direction

1. More indicators like MACD, A/D can be used to determine long/short.

2. Add moderate fixed stop loss price based on need.

3. Optimize EMA periods based on symbol trading characteristics.  

## Conclusion

The strategy's logic is clear and easy to understand, using EMAs to determine structure and engulfing patterns to capture breakout. Its advantages are simple judgment logic and clear trading signals. But risks of being trapped exist. Further optimization can gain better return.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(20 Jan 1990 00:00 +0900)|I_start_date|
|v_input_2|timestamp(20 Dec 2030 00:00 +0900)|I_finish_date|
|v_input_int_1|15|Short EMA|
|v_input_int_2|30|Long EMA|
|v_input_float_1|true|Size of Body|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-06 00:00:00
end: 2023-12-06 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// @version=5
// # ========================================================================= #
// #                   |   STRATEGY  |
// # ========================================================================= #
strategy(
  title                           = "fpemehd Strategy001",
  shorttitle                      = "f_001",
  overlay                         =  true,
  default_qty_type                =  strategy.percent_of_equity, 
  default_qty_value               =  100, 
  initial_capital                 =  10000000, 
  currency                        =  currency.USD, 
  slippage                        =  0, 
  commission_type                 =  strategy.commission.cash_per_order, 
  commission_value                =  0.01, 
  process_orders_on_close         =  true)
// # ========================================================================= #
// #                   |   STRATEGY  |
// # ========================================================================= #


// Inputs
I_start_date = input (defval = timestamp("20 Jan 1990 00:00 +0900"))
I_finish_date = input(defval = timestamp("20 Dec 2030 00:00 +0900"))

I_short_ema = input.int(defval = 15 , title = "Short EMA", minval = 1 , maxval = 300 , step = 1)
I_long_ema = input.int(defval = 30 , title = "Long EMA", minval = 1 , maxval = 300 , step = 1)

I_body = input.float(defval = 1 , title = "Size of Body", minval = 1 , maxval = 5 , step = 0.1)

time_cond = true

// Calculate Engulfing Candles
C_uptrend = false
C_downtrend = false
C_ema_short = ta.ema(source = close, length = I_short_ema) 
C_ema_long = ta.ema(source = close, length = I_long_ema) 
C_uptrend := close > C_ema_short and C_ema_short > C_ema_long
C_downtrend := close < C_ema_short and C_ema_short < C_ema_long

C_pre_body = math.abs(open[1]-close[1])
C_pre_body_ratio = (math.abs(open[1]-close[1])) / (math.abs(high[1]-low[1])) * 100

C_now_body = math.abs(open-close)
C_now_body_ratio = (math.abs(open-close)) / (math.abs(high-low)) * 100

C_bullish_engulfing = (open[1] > close[1] and open <= close) and (low < low[1] and high > high[1])
C_bearish_engulfing = (open[1] < close[1] and open >= close) and (low < low[1] and high > high[1])
C_avoid_doge = (C_pre_body_ratio > I_body and C_now_body_ratio > I_body) ? true : false
C_volume_filter = volume > volume[1] * 1.2

// Signals
long_signal = C_uptrend and C_bullish_engulfing and C_avoid_doge and C_volume_filter
close_signal = C_downtrend or C_bearish_engulfing 


if long_signal and time_cond
    strategy.entry(id = "Long", direction = strategy.long)

if close_signal and time_cond
    strategy.close(id = "Long")


```

> Detail

https://www.fmz.com/strategy/434564

> Last Modified

2023-12-07 15:50:13
