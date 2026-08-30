
> Name

Dual-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The dual momentum strategy uses two momentum indicators, fast and slow, to generate trading signals and exit signals. This is a responsive strategy that is suitable for trending varieties on the daily and 4-hour lines. The implementation of this strategy comes from the QuantCT application.
The operating mode can be set to long-short or long only.
It is also possible to set a fixed stop loss or ignore the stop loss, allowing the strategy to run only on entry and exit signals.
## Strategy Principle
This strategy uses momentum indicators with fast periods (default 5 days) and slow periods (default 10 days).
When slow momentum and fast momentum are both greater than 0, a long signal is generated.
When slow momentum or fast momentum is less than 0, a closing signal is generated.
Similarly, when slow momentum and fast momentum are both less than 0, a short signal is generated. When slow momentum or fast momentum is greater than 0, a closing signal is generated.
Therefore, this strategy uses the intersection of two sets of different cycle momentum to capture changes in trends and achieve trend tracking.
## Advantage Analysis
- Using double momentum indicators can more accurately capture changes in market trends and reduce false signals.
- Fast cycle momentum is sensitive to market changes and can quickly respond to trends; slow cycle momentum filters out market noise to ensure the correct trading direction.
- You can flexibly choose to only do long or two-way transactions to adapt to different trading preferences.
- You can choose whether to use stop loss to control risks.
- This strategy is highly responsive and is particularly suitable for trend trading on daily lines or higher periods, and can achieve excess returns.
## Risk Analysis
- The judgment of the trend by the dual momentum strategy depends on the indicator value being greater or less than 0, and there is a certain lag.
- This strategy relies more on trends and performs poorly in consolidating markets. It is prone to excessive transactions, resulting in increased transaction fees.
- If stop loss is not used, there is a greater risk of single loss.
- Inappropriate suitable varieties and cycles can also lead to poor strategy performance.
In order to control risks, it is recommended to appropriately adjust the momentum cycle parameters and set a reasonable fixed stop loss ratio. At the same time, choose a variety with a clear trend and run this strategy on the daily line or higher.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add other indicator filters, such as MACD or RSI, to avoid wrong transactions at trend turning points.
2. Add an adaptive stop-loss mechanism to dynamically adjust the stop-loss range according to the degree of market fluctuations.
3. Optimize momentum parameters and find more suitable parameter combinations for different varieties. It can be achieved through methods such as step optimization and Walk Forward Analysis.
4. Add a position management mechanism to adjust the size of new positions based on previous returns.
5. Distinguish between long and short markets and adopt asymmetric entry and exit strategies. The short market can be more aggressive, and the long market can be more cautious.
## Summarize
The dual momentum strategy determines the trend direction through the intersection of fast and slow momentum indicators, and uses simple indicators to capture market trend changes. It is suitable for tracking obvious trends within or between days, and can obtain better excess returns. At the same time, this strategy also has certain lag risks, and it needs to be combined with stop loss and other indicators to control risks, as well as optimize varieties and parameters to obtain more stable performance.

||


## Overview

The Dual Momentum strategy uses fast and slow momentum indicators to generate entry and exit signals. It is a fast-reacting strategy well-suited for trending instruments on the daily and 4-hour timeframes. This implementation is based on the QuantCT app.  

The strategy allows configuring long/short or long-only mode. It also allows enabling fixed stop loss or ignoring it so that the strategy acts solely on entry and exit signals.

## Strategy Logic

The strategy uses fast period momentum (default 5 days) and slow period momentum (default 10 days). 

When slow momentum and fast momentum are both above 0, a long entry signal is generated.

When slow momentum or fast momentum goes below 0, an exit signal is generated.

Similarly, when slow momentum and fast momentum are both below 0, a short entry signal is generated. When slow momentum or fast momentum goes above 0, an exit signal is generated.

Thus, the strategy captures trend changes using the crossover of two momentum indicators with different periods.

## Advantage Analysis

- Using dual momentum provides more accurate trend change detection and fewer false signals.

- Fast period momentum reacts quickly to market changes, while slow period filters out noise.

- Flexible long/short or long-only modes suit different trading preferences.

- Optional stop loss controls risk.

- Fast-reacting nature makes it suitable for trend trading on daily or higher timeframes for outsized gains.

## Risk Analysis

- Dual momentum relies on indicator values above/below 0, which has some lag.

- The strategy is more trend-dependent and may underperform in range-bound markets with more whipsaws.

- Not using stop loss risks large losses.

- Wrong choice of symbols or timeframes can lead to poor results.

To control risks, tune the momentum periods, use reasonable fixed stop loss percentage, select strongly trending symbols and run on daily or higher timeframes.

## Enhancement Opportunities

The strategy can be enhanced in several ways:

1. Add filters like MACD or RSI to avoid wrong trades at trend turning points.

2. Add adaptive stop loss to adjust stop distance based on market volatility. 

3. Optimize momentum parameters for different symbols via stepwise optimization, walk forward analysis etc.

4. Add position sizing rules to adjust new position size based on past performance.

5. Differentiate long and short market conditions for asymmetric entries and exits.

## Conclusion

The Dual Momentum strategy captures trend direction using fast and slow momentum crossover. Using simple indicators to detect trend changes, it is suitable for riding intraday or multi-day trends and generating excess returns. Proper risk control via stop loss, symbol/parameter optimization can improve consistency.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Fast Period|
|v_input_2|10|Slow Period|
|v_input_3|false|Long Only|
|v_input_4|5|Stop-loss (%)|
|v_input_5|false|Use Stop-Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-28 00:00:00
end: 2023-09-27 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © QuantCT

//@version=4
strategy("Momentum Strategy Idea",
         shorttitle="Momentum", 
         overlay=false,
         pyramiding=0,     
         default_qty_type=strategy.percent_of_equity, 
         default_qty_value=100, 
         initial_capital=1000,           
         commission_type=strategy.commission.percent, 
         commission_value=0.075)

// ____ Inputs

fast_period = input(title="Fast Period", defval=5) 
slow_period = input(title="Slow Period", defval=10)
long_only = input(title="Long Only", defval=false)
slp = input(title="Stop-loss (%)", minval=1.0, maxval=25.0, defval=5.0)
use_sl = input(title="Use Stop-Loss", defval=false)

// ____ Logic

mom_fast = mom(close, fast_period)
mom_slow = mom(close, slow_period)
    
enter_long = (mom_slow > 0 and mom_fast > 0)
exit_long = (mom_slow < 0 or mom_fast < 0)
enter_short = (mom_slow < 0 and mom_fast < 0)
exit_short = (mom_slow > 0 or mom_fast > 0)

strategy.entry("Long", strategy.long, when=enter_long)
strategy.close("Long", when=exit_long) 
if (not long_only)
    strategy.entry("Short", strategy.short, when=enter_short)
    strategy.close("Short", when=exit_short) 
   
// ____ SL

sl_long = strategy.position_avg_price * (1- (slp/100))
sl_short = strategy.position_avg_price * (1 + (slp/100))
if (use_sl)
    strategy.exit(id="SL", from_entry="Long", stop=sl_long)
    strategy.exit(id="SL", from_entry="Short", stop=sl_short)
    
// ____ Plots

colors = 
 enter_long ? #27D600 :
 enter_short ? #E30202 :
 color.orange

mom_fast_plot = plot(mom_fast, color=colors)
mom_slow_plot = plot(mom_slow, color=colors)
fill(mom_fast_plot, mom_slow_plot, color=colors, transp=50)







```

> Detail

https://www.fmz.com/strategy/428081

> Last Modified

2023-09-28 15:03:57
