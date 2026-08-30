
> Name

Supertrend-Moving-Stop-Loss-Take-Profit-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10c72e6112de0438872.png)
[trans]

## Overview
The Beyond Trailing Stop Profit Strategy is a quantitative trading strategy based on exceeding indicators. This strategy implements stop loss and trailing stop profit by constructing entry and exit conditions for long and short positions. The advantage of the strategy is that it can obtain higher profits in a sustained trend, and at the same time, most of the profits can be locked in through moving stop profit. However, this strategy is also more sensitive to breakthrough failures.
## Strategy Principle
This strategy is a trend following strategy based on transcendence indicators. Transcendence indicators can determine the direction of price trends. Buy and sell signals are generated when the exceeding indicator changes direction. Specifically, if the surpassing indicator crosses the 0 axis above, a buy signal is generated; if the surpassing indicator crosses below the 0 axis, a sell signal is generated. The ratio of the closing price to the previous day's closing price determines the moving profit stop point. ATR determines the stop loss point. In this way, a moving stop-profit and stop-loss strategy based on exceeding the indicator to determine the trend direction is constructed.
## Advantage Analysis
The biggest advantage of this strategy is that it combines trend judgment and moving stop profit. The transcendence indicator determines the trend direction by breaking through the 0-axis up and down, and can capture the trend more accurately. A trailing stop-profit can lock in most of the profits while the trend is in progress. Stop loss settings are also helpful in controlling risk. Therefore, in markets with obvious trends, this strategy can achieve higher profits. In addition, the strategy logic is simple and clear, easy to understand and implement, which is also an advantage of the strategy.
## Risk Analysis
The biggest risk with this strategy is sensitivity to failed breakouts. In the consolidation area, exceeding the indicator may produce a false breakout and mistakenly establish a position. It is easy to get trapped at this time. In addition, the mobile stop profit mechanism may also stop profits prematurely and miss the subsequent market. Finally, improperly set stops can also be too loose or too aggressive, increasing risk. So these are the risk points that this strategy needs to guard against.
## Optimization direction
This strategy can be optimized from the following aspects: 1) Reasonably determine the parameters of the exceedance indicator to avoid false signals; 2) Add a mechanism to judge the reliability of the breakthrough, such as increasing the trading volume signal; 3) Optimize the parameters of the mobile stop profit to reduce the possibility of arbitrage as much as possible while ensuring profits; 4) Use dynamic stop loss based on volatility to replace the static stop loss; 5) Add other indicators for combination to improve the stability of the strategy.
## Summarize
The Profit Beyond Trailing Stop strategy is overall a better trend following strategy. It can reasonably judge the trend direction and has a moving take-profit mechanism. However, this strategy is also more sensitive to breakthrough failure, and there are certain risks. By further optimizing parameter settings, judgment rules, stop loss mechanisms, etc., this strategy can be effectively improved and turned into a stable and efficient quantitative trading strategy.
||

## Overview
The Supertrend Moving Stop Loss Take Profit strategy is a quantitative trading strategy based on the Supertrend indicator. The strategy constructs long and short entry and exit conditions to implement stop loss and moving take profit. The advantage of the strategy is that it can achieve higher profits in sustained trends, while locking in most of the profits through moving take profit. However, the strategy is also sensitive to breakout failures.

## Strategy Logic
This strategy is a trend following strategy based on the Supertrend indicator. The Supertrend indicator can determine the direction of the price trend. It generates buy and sell signals when the Supertrend line crosses the 0-line. Specifically, a buy signal is generated when the Supertrend line crosses above the 0-line; a sell signal is generated when the line crosses below the 0-line. The ratio between the closing price and previous day's closing price determines the moving take profit point. ATR determines the stop loss point. Thus, a moving take profit stop loss strategy is constructed based on the Supertrend indicator to determine trend direction.  

## Advantage Analysis 
The biggest advantage of this strategy is the combination of trend identification and moving take profit. The Supertrend indicator can capture trends quite accurately through 0-line crossovers. Moving take profit allows locking in most profits while the trend persists. The stop loss setting also helps to control risks. Thus, the strategy can achieve higher profits in obvious trending markets. In addition, the simple and clear logic is also an advantage of the strategy.

## Risk Analysis
The biggest risk of this strategy is its sensitivity to breakout failures. In range-bound periods, the Supertrend indicator may generate false breakouts resulting in wrongly established positions. This can easily lead to being caught in traps. Also, the moving take profit mechanism may exit positions too early, missing subsequent moves. Finally, improper stop loss settings can also be too loose or too aggressive, heightening risks. Thus, these are areas the strategy needs to guard against.

## Optimization Directions 
The strategy can be optimized from the following aspects: 1) Reasonably determine Supertrend parameters to avoid false signals; 2) Add mechanisms to judge breakout reliability, such as volume signals; 3) Optimize the parameters of moving take profit to reduce whipsaw possibility while ensuring profitability; 4) Use volatility-based dynamic stops instead of static stops; 5) Add other indicators for ensemble strategies to improve robustness.

## Conclusion
Overall, the Supertrend Moving Stop Loss Take Profit strategy is a decent trend following strategy. It can reasonably determine trend direction and has a moving take profit mechanism. But it is also sensitive to invalid breakouts and has some risks. Further optimizing parameters, judgement rules, stop mechanisms etc. can improve the strategy and make it a stable and efficient trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|1500|Stop Loss Amount|
|v_input_2|15000|Profit Amount|
|v_input_3|0.91|Long Trailing Profit Taking|
|v_input_4|1.01|Short Trailing Profit Taking|
|v_input_5|10|ATR Length|
|v_input_float_1|3|Factor|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2024-01-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("ST Michael Moving TP", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=15)

// Stop loss and profit amount
stop_loss = input(1500, title="Stop Loss Amount")
profit = input (15000, title="Profit Amount")
LongTrailProfit = input (0.91, title = "Long Trailing Profit Taking")
ShortTrailProfit = input (1.01, title = "Short Trailing Profit Taking")

atrPeriod = input(10, "ATR Length")
factor = input.float(3.0, "Factor", step = 0.01)

[_, direction] = ta.supertrend(factor, atrPeriod)

long_condition = ta.change(direction) <0
short_condition = ta.change(direction) >0


stop_price_long = ta.valuewhen(long_condition, low[0]-stop_loss,0)
profit_price_long = ta.valuewhen(long_condition, high[0]+profit,0)
stop_price_short = ta.valuewhen(short_condition, high[0]+stop_loss,0)
profit_price_short = ta.valuewhen(short_condition, low[0]-profit,0)

atr=ta.atr(10)

intrade_long = strategy.position_size > 0
intrade_short = strategy.position_size < 0
exitConditionLong = (close < (close[1]*LongTrailProfit)) 
exitConditionShort = (close > (close[1]*ShortTrailProfit))

if (long_condition)
    strategy.entry("Long3", strategy.long)
if (intrade_long and exitConditionLong)
    strategy.close("Long3")

if (short_condition)
    strategy.entry("Short3", strategy.short)
if (intrade_short and exitConditionShort)
    strategy.close ("Short3")

if (strategy.position_size>0)
    strategy.exit("exit_long",from_entry="Long3",limit=profit_price_long,stop=stop_price_long)

if (strategy.position_size<0)
    strategy.exit("exit_short",from_entry="Short3",limit=profit_price_short,stop=stop_price_short)    
```

> Detail

https://www.fmz.com/strategy/438054

> Last Modified

2024-01-08 16:24:03
