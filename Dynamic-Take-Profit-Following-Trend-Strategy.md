
> Name

Dynamic-Take-Profit-Following-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/15fb6e38fec57213081.png)

[trans]

## Overview
The dynamic stop-profit trend-following strategy achieves the purpose of buying low, selling high, and pursuing the upward trend by detecting long-term trends and short-term corrections. This strategy also uses volatility units to detect profit and loss size, making it applicable to all currencies without worrying about percentage changes.
## Strategy Principle
The buying logic of this strategy is: when there is a long-term upward trend (the 200-day EMA rises and the 200-day RSI is greater than 51) and a short-term downward correction (the closing prices of the last two K lines fall), buy and open a position.
The logic of selling is: take profit when the price rises by more than 1 fluctuation unit; stop loss when the price falls by more than 2 fluctuation units.
The calculation of the fluctuation unit is: 2 times the standard deviation of the closing price within 50 days is used as the basic fluctuation unit. In this way, the fluctuations of different currencies can be detected without manually setting percentages.
## Advantage Analysis
The biggest advantage of this strategy is that it can dynamically detect the fluctuations of different currencies and set take-profit and stop-loss units according to the fluctuations of the currency itself. This avoids the problem of fixed percentage take-profit settings and can automatically adapt to more currencies.
Another advantage is that it can effectively filter out false breakthroughs by combining long- and short-term judgments. Using long-term trends to determine which coins may rise in the future, combined with short-term callback signals, can effectively avoid false signals such as Bollinger Bands squeeze.
## Risk Analysis
The biggest risk of this strategy lies in the setting of take-profit and stop-loss units. If the fluctuation is too large, the stop-profit distance may be too close and it will be impossible to continue to chase the increase; if the fluctuation is too small, the stop-loss may be too fast. This needs to be assisted by longer period EMA to avoid errors in judgment of fluctuating units.
Another risk is the strategy's reliance on short-term trend judgment. If there is a long-term rise but no short-term correction, the entry opportunity will be missed. This may require the addition of other auxiliary judgment indicators.
## Optimization direction
This strategy can be optimized from the following directions:
1. Add longer period EMA judgment to avoid errors in fluctuating units
2. Increase trading volume and other indicators to determine trends and reduce reliance on short-term K-lines
3. Optimize the opening and closing conditions and set stricter entry rules
4. Combine with machine learning algorithms to determine the trend direction and achieve a higher winning rate
## Summarize
The overall idea of ​​the dynamic stop-profit trend chasing strategy is clear, and the core lies in the setting of dynamic fluctuation units. This strategy can automatically adapt to different currencies to set profit and loss units, without the need to manually set percentages. At the same time, combined with long-term and short-term dual judgments, false signals can be effectively filtered out. With further optimization, this strategy can become a highly efficient trend following strategy.
||

## Overview

The Dynamic Take Profit Following Trend strategy detects long-term trends and short-term pullbacks to achieve buying low and selling high, with the goal of chasing uptrends. The strategy also uses volatility units to detect the size of wins and losses so that it can be applied to all coins without worrying about percentage changes.

## Strategy Logic

The buying logic of this strategy is: when a long-term uptrend appears (200-day EMA goes up, 200-day RSI greater than 51) and a short-term pullback happens (last 2 candlesticks show decreased closing prices), long positions are opened.

The selling logic is: take profit when price increases more than 1 volatility unit; stop loss when price decreases more than 2 volatility units. 

The volatility unit is calculated as: 2 times the standard deviation of closing prices in the last 50 days. This can detect volatility conditions of different coins automatically without needing manual percentage settings.

## Advantage Analysis 

The biggest advantage of this strategy is that it can dynamically detect volatility sizes of different coins and set stop loss/take profit levels accordingly. This avoids the problem of fixed percentage settings and can automatically adapt to more coins.

Another advantage is combining long-term and short-term judgments can effectively filter out false breakouts. Using the long-term trend to judge potentially uptrending coins and combining it with short-term pullback signals can avoid false signals like Bollinger squeezes.  

## Risk Analysis

The biggest risk of this strategy is the stop loss/take profit unit settings. If volatility is too high, take profit distances may be too close to keep chasing the uptrend; if volatility is too low, stop loss may trigger too fast. This needs longer period EMAs as an assist to avoid errors in volatility unit judgments.  

Another risk is the strategy's reliance on short-term trends. If there is a long-term uptrend without a short-term pullback, the entry timing would be missed. This may need additional assist indicators.

## Optimization Directions  

The strategy can be optimized in the following directions:

1. Add longer-period EMA judgments to avoid volatility unit errors 

2. Add indicators like trading volumes to judge trends, reduce reliance on short-term candlesticks

3. Optimize entry and exit conditions, set stricter entry rules  

4. Combine machine learning algorithms to determine trend direction, achieve higher win rate

## Conclusion  

The Dynamic Take Profit Following Trend Strategy has clear logic at its core—dynamically setting stop loss/take profit units. This strategy can automatically adapt settings across coins without needing manual percentage inputs. Meanwhile, combining double confirmation of long-term and short-term trends can effectively filter out false signals. With further optimizations, this strategy can become a highly efficient trend chasing strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-22 00:00:00
end: 2023-12-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// @version=4
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © BHD_Trade_Bot

strategy(shorttitle='Take Profit On Trend',
 title='Take Profit On Trend (by BHD_Trade_Bot)',
 overlay=true,
 initial_capital = 15,
 default_qty_type = strategy.cash,
 default_qty_value = 15,
 commission_type=strategy.commission.percent,
 commission_value=0.1)



//Backtest Time
start_day = 1
start_month = 1
start_year = 2021
end_day = 1
end_month = 1
end_year = 2050
start_time = timestamp(start_year, start_month, start_day, 00, 00)
end_time = timestamp(end_year, end_month, end_day, 23, 59)
is_back_test_time() =>
    time >= start_time and time <= end_time ? true : false

// Last bar
h1_last_bar = (timenow - time)/1000/60/60 < 2



// EMA
ema50 = ema(close, 50)
ema200 = ema(close, 200)

// RSI length 200
rsi200 = rsi(close, 200)

// Bollinger Bands length 50
bb50 = 2 * stdev(close, 50)

// BHD Unit
bhd_unit = sma(bb50, 100)
bb50_upper = ema50 + bhd_unit
bb50_lower = ema50 - bhd_unit



// All n candles is going down
all_body_decrease(n) =>
    isValid = true
    for i = 0 to (n - 1)
        if (close[i] > close[i + 1])
            isValid := false
            break
    isValid



// ENTRY

// Long-term uptrend
entry_condition1 = rsi200 > 51 

// Short-term downtrend
entry_condition2 = all_body_decrease(2) 

ENTRY_CONDITION = entry_condition1 and entry_condition2

if (ENTRY_CONDITION and is_back_test_time())
    strategy.entry("entry", strategy.long)



// CLOSE CONDITIONS

// Price increase 1 BHD unit
TAKE_PROFIT = close > strategy.position_avg_price + bhd_unit

// Price decrease 2 BHD unit
STOP_LOSS = close < strategy.position_avg_price - bhd_unit * 2

CLOSE_CONDITION = TAKE_PROFIT or STOP_LOSS

if (CLOSE_CONDITION or h1_last_bar)
    strategy.close("entry")



// Draw
plot(ema50)
plot(ema200, color=color.yellow)
plot(bb50_upper)
plot(bb50_lower)

```

> Detail

https://www.fmz.com/strategy/437022

> Last Modified

2023-12-29 16:06:54
