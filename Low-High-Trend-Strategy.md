
> Name

Low-High-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1aafd8bcaf988ccd385.png)
[trans]

## Overview
This strategy is based on the idea of ​​buying when the market is low and selling when it is high. It tracks the highest and lowest prices in a certain period in the past, establishes a long position when the price breaks through the lowest price, and closes the position when the price falls below the highest price or reaches the take-profit condition. At the same time, this strategy adds an optional trend filter, which will only buy when the price is in an upward trend.
## Strategy Principle
### Calculation of lowest price and highest price
- Lowest price (lowcriteria): Call the ta.lowest function to calculate the lowest price in a certain period in the past based on the lookback period set by the user (default 20 K lines), and draw the lowest price line.
- Highcriteria: Call the ta.highest function to calculate the highest price in a certain period in the past based on the lookback period set by the user (default 10 K lines), and draw the highest price line.
### Entry signal
When the current price breaks through the lowest price line, a buy signal is issued and a long position is established.
### Exit signal
Two exit methods are available:
1. Fixed take profit: When the price reaches the set take profit level (for example, it exceeds the entry price by 8%), the position will be closed for arbitrage.
2. Highest price breakthrough: When the price falls below the highest price line, it is judged that the trend is reversed and the position is closed with stop loss.
### Trending Filter
Add the EMA moving average to determine the trend direction, and buy only when the price is higher than the EMA moving average (called an uptrend). This filter can be turned on or off.
## Advantage Analysis
- The strategy of buying when the low point is exceeded and selling when the high point is exceeded is in line with the basic laws of the market.
- Add a trend judgment mechanism to avoid frequent opening of positions when prices fluctuate.
- Provide two exit options, which can either pursue high profit taking or reduce losses.
- Customizable parameters to adapt to a wider market environment.
- There is a large space for strategy optimization, which can be further improved through parameter adjustment, filter design, etc.
## Risk Analysis
- Fixed take-profit cannot be adjusted according to the actual market trend, which may lead to premature take-profit or too small a take-profit range.
- When selling above the highest price, a large loss may have occurred and the loss cannot be effectively controlled.
- EMA trend judgment is only based on a certain historical period and may lag behind the actual trend change.
- Backtest data cannot represent the future, and there is uncertainty in the actual results.
## Optimization direction
- Added take-profit methods: such as moving take-profit, stepped take-profit, etc., so that the take-profit level can be adjusted in real time according to market trends.
- Optimize the exit signal: for example, change the exit signal to batches, or add other indicator judgments.
- Optimize trend judgment: such as adding more indicators or machine learning judgment.
- Optimize parameters: Find the best parameter combination through more extensive backtesting.
- Added stop loss method: making loss control more flexible and effective.
## Summarize
This strategy generally uses the classic principle of buying low and selling high, which can achieve better results under certain conditions. However, the strategy itself still has room for optimization, and more stable returns can be obtained through parameter adjustment, exit optimization, stop-loss improvement, etc. This article conducts a comprehensive and in-depth analysis of the principles, advantages, risks, and optimization directions of the strategy. It aims to provide strategic ideas while also reminding investors to pay attention to risks and treat quantitative transactions with caution.
|| 

## Overview  

This strategy is designed based on the market principle of buying low and selling high. It tracks the highest and lowest prices over a certain period, establishes a long position when the price breaks through the lowest price, and closes the position when the price falls below the highest price or the take profit condition is met. At the same time, this strategy adds an optional trend filter that only allows buying when the price is in an uptrend.

## Strategy Logic  

### Highest and Lowest Price Calculation  

- Lowest price (lowcriteria): Call ta.lowest function to calculate the lowest price over the lookback period set by user (default 20 bars) and plot the lowest price line.  

- Highest price (highcriteria): Call ta.highest function to calculate the highest price over the lookback period set by user (default 10 bars) and plot the highest price line.   

### Entry Signal  

When the current price breaks through the lowest price line, a buy signal is triggered to establish a long position.  

### Exit Signal   

Two exit methods are provided for option:  

1. Fixed take profit: Close the position for profit when the price reaches the preset take profit level (e.g. 8% above entry price).

2. Breakdown of highest price: Close the position to cut losses when the price falls below the highest price line, judging a trend reversal.   

### Trend Filter  

Add an EMA line to determine the trend direction. Allow buying only when the price is above EMA line (an uptrend). This filter can be enabled or disabled.  

## Advantage Analysis   

- Adopt the classic strategy of buying low and selling high, aligning with market fundamentals.  

- Add trend judgment to avoid frequent opening during price fluctuations. 

- Provide two exit options for pursuing high profits or reducing losses.  

- Customizable parameters adapt to more market environments.  

- Huge room for strategy optimization via parameter tuning, filter design etc.

## Risk Analysis  

- Fixed take profit level fails to adjust based on actual market moves, resulting in premature profit-taking or insufficient profit target.

- Selling at the breakdown of highest price may already generate huge losses, unable to effectively control losses.  

- EMA trend judgment only looks back a certain period, possibly lagging behind the actual trend change.  

- Backtest results cannot represent the future. Live performance has uncertainties.  

## Optimization Directions   

- Add profit-taking methods like trailing stop, partial exit etc. to dynamically adjust take profit level.  

- Optimize exit signals e.g. partial exits, adding other indicators.

- Enhance trend judgment by incorporating more indicators or machine learning.  

- Optimize parameters by more extensive backtests to find optimum sets.

- Add stop loss methods to better control losses.

## Summary  

This strategy generally applies the classic low buy high sell principle and can perform well under certain conditions. But there is still room for improving via parameter tuning, exit optimization, stop loss mechanisms etc. This article provides an in-depth analysis on the strategy's logic, pros, cons and optimization directions, aiming to share the strategy idea as well as remind investors of the risks and trade cautiously with quantitative strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(01 Jan 2000 05:00 +0000)|Start Time|
|v_input_2|timestamp(01 Jan 2099 00:00 +0000)|End Time|
|v_input_3|20|Lowest Price Lookback|
|v_input_4|10|Highest Price Lookback|
|v_input_5|true|Sell with Take-Profit % intead of highest price cross?|
|v_input_float_1|8|Take Profit %|
|v_input_6|true|Only buy when price is above EMA trend?|
|v_input_7|200|EMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-16 00:00:00
end: 2023-11-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// @version=5
// Author = TradeAutomation


strategy(title="Low-High-Trend Strategy", shorttitle="Low-High-Trend Strategy", process_orders_on_close=true, overlay=true, commission_type=strategy.commission.cash_per_order, commission_value=1, slippage=3, initial_capital = 25000, margin_long=50, margin_short=50, default_qty_type=strategy.percent_of_equity, default_qty_value=110)


// Backtest Date Range Inputs // 
StartTime = input(defval=timestamp('01 Jan 2000 05:00 +0000'), title='Start Time')
EndTime = input(defval=timestamp('01 Jan 2099 00:00 +0000'), title='End Time')
InDateRange = true

// Strategy Calculations //
lowcriteria = ta.lowest(close, input(20, "Lowest Price Lookback", tooltip="The strategy will BUY when the price crosses over the lowest it has been in the last X amount of bars"))[1]
highcriteria = ta.highest(close, input(10, "Highest Price Lookback", tooltip="If Take-Profit is not checked, the strategy will SELL when the price crosses under the highest it has been in the last X amount of bars"))[1]
plot(highcriteria, color=color.green)
plot(lowcriteria, color=color.red)

// Take Profit //
TakeProfitInput = input(true, "Sell with Take-Profit % intead of highest price cross?")
TakeProfit = ta.crossover(close,strategy.position_avg_price*(1+(.01*input.float(8, title="Take Profit %", step=.25))))

// Operational Functions //
TrendFilterInput = input(true, "Only buy when price is above EMA trend?")
ema = ta.ema(close, input(200, "EMA Length"))
TrendisLong = (close>ema)
plot(ema)

// Entry & Exit Functions//
if (InDateRange and TrendFilterInput==true)
    strategy.entry("Long", strategy.long, when = ta.crossover(close, lowcriteria) and TrendisLong)
if (InDateRange and TrendFilterInput==false)
    strategy.entry("Long", strategy.long, when = ta.crossover(close, lowcriteria))
if (InDateRange and TakeProfitInput==true)
    strategy.close("Long", when = TakeProfit)
if (InDateRange and TakeProfitInput==false)
    strategy.close("Long", when = ta.crossunder(close, highcriteria))
if (not InDateRange)
    strategy.close_all()
    
```

> Detail

https://www.fmz.com/strategy/432972

> Last Modified

2023-11-23 11:03:18
