
> Name

Dual-Momentum-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/bcc5b7dbf7e1665b4bac37c6e2259a29a9b1bf8b45d7aa823f4eb0008a1e80d8.png)

[trans]

## Overview
This strategy is a dual momentum indicator breakout strategy. It uses two momentum indicators with different parameter settings to generate trading signals when both momentum indicators break through the zero axis. This strategy only makes long entries, and short positions are only used to close positions.
## Strategy Principle
The code first sets the strategy attributes, such as delegation mode, fee mode, etc. Then it calculates two momentum indicators:
```pine
// Momentum settings

i_len           = input(defval = 12, title = "Length", minval = 1) 
i_src           = input(defval = close, title = "Source")
i_percent       = input(defval = true, title = "Percent?")
i_mom           = input(defval = "MOM2", title = "MOM Choice", options = ["MOM1", "MOM2"])

// Momentum code

mom0 = momentum(i_src, i_len, i_percent) 
mom1 = momentum(mom0, 1, i_percent)
mom2 = momentum(i_src, 1, i_percent)

momX = mom1 

if i_mom == "MOM2"
    momX := mom2
```

mom0 is the basic momentum indicator, the length is i_len, the data source is i_src, and whether to calculate the percentage is determined by i_percent.
mom1 is a momentum indicator with mom0 as the data source and a length of 1.
mom2 is a momentum indicator with a length of 1 based on the original data i_src.
The final momentum indicator momX defaults to mom1, but you can also choose mom2.
When mom0 and momX exceed the 0 axis at the same time, go long; when mom0 and momX are below the 0 axis at the same time, close the position.
## Strategic Advantages
1. Using double momentum indicators combined with different parameter settings can improve the reliability of trading signals, and double confirmation reduces false signals.
2. Only long entries are used, and short positions are only used to close positions, which can reduce transaction frequency and transaction costs.
3. Momentum indicator parameters can be adjusted to adapt to different market environments.
4. The code structure is clear and easy to understand and modify.
5. Added trading message settings, which can be used in conjunction with automatic trading systems.
## Strategy Risk
1. Although the dual momentum indicator can reduce false signals, it may also miss weaker trend signals.
2. Only doing long transactions may miss short trading opportunities.
3. Improper setting of momentum indicator parameters may lead to too frequent or too slow trading.
4. Insufficient backtest data may lead to parameter overfitting.
5. Although double confirmation can reduce false signals, it cannot be completely avoided. During real trading, you still need to pay attention to the effectiveness of breakthroughs.
## Strategy optimization direction
1. You can test parameter combinations of different lengths and whether to calculate percentages to find the best parameters.
2. You can consider adding short trading signals after the trend is confirmed to capture more trading opportunities.
3. You can test different momentum indicator calculation methods, such as ROC, RSI, etc., to find better results.
4. It can be combined with trend filtering to avoid trading in volatile market conditions.
5. Stop loss strategies can be optimized to maximize profits while controlling risks.
## Summarize
This strategy is a typical double momentum indicator breakout strategy. It uses double confirmation to reduce false signals and only does long entries to reduce trading frequency. The advantage of this strategy is that it is simple, clear and easy to implement, and there is a lot of room for improvement in parameter optimization and risk control. Overall, this strategy is feasible as the basic framework of the momentum breakthrough strategy, but it needs to be optimized and adjusted for specific markets in order to achieve stable profits in the real market.
||
## Overview

This is a dual momentum breakout strategy. It uses two momentum indicators with different parameter settings and generates trading signals when both momentum indicators break through the zero line. The strategy only takes long entries and shorts are only used for exiting positions.

## Strategy Logic

The code first sets strategy properties like order type, commission scheme etc. Then it calculates two momentum indicators:

```pine
// Momentum settings
****
i_len           = input(defval = 12, title = "Length", minval = 1)
i_src           = input(defval = close, title = "Source")  
i_percent       = input(defval = true, title = "Percent?")
i_mom           = input(defval = "MOM2", title = "MOM Choice", options = ["MOM1", "MOM2"])

// Momentum code 

mom0 = momentum(i_src, i_len, i_percent)
mom1 = momentum(mom0, 1, i_percent) 
mom2 = momentum(i_src, 1, i_percent)

momX = mom1   

if i_mom == "MOM2"
    momX := mom2
```

mom0 is the base momentum indicator with length i_len, data source i_src, whether to calculate percentage is decided by i_percent.

mom1 is the momentum indicator with mom0 as data source and length 1.

mom2 is the momentum indicator with original data i_src as source and length 1.

The final momentum indicator momX defaults to mom1, can also choose mom2.

When mom0 and momX both breach above 0 line, go long. When mom0 and momX both breach below 0 line, close position.

## Advantages of the Strategy

1. Using dual momentum indicators with different settings improves signal reliability with double confirmation and fewer false signals.

2. Only taking long entries and using shorts for exits lowers trade frequency and reduces transaction costs.

3. Flexible momentum parameter adjustments suit different market environments. 

4. Clean code structure, easy to understand and modify.

5. Trade messages enabled, integrates well with auto trading systems.

## Risks of the Strategy

1. Dual momentum may miss weaker trend signals while reducing false signals.

2. Missing short trade opportunities with only long entries.

3. Improper momentum parameter settings lead to over-trading or delayed signals.

4. Insufficient backtest data causes parameter overfitting. 

5. Double confirmation reduces but does not eliminate false signals, need to watch for validity in live trading.

## Optimization Directions

1. Test combinations of length and percentage parameters to find optimum.

2. Consider adding short trade signals after trend confirmation to capture more trades.

3. Test different momentum calculations like ROC, RSI etc for better results.

4. Add trend filtering to avoid whipsaw markets.

5. Optimize stop loss for maximum profitability within risk limits.

## Conclusion

This is a typical dual momentum breakout strategy. It uses double confirmation to reduce false signals and only long entries to lower trade frequency. The advantages are simplicity and ease of implementation, with much room for improvements in parameter optimization and risk control. Overall it serves as a reasonable momentum breakout framework but needs market-specific tuning and optimizations for profitable live trading.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(2021-01-02T00:00:00)|Start Date|
|v_input_2|timestamp(2021-12-31T00:00:00)|End Date|
|v_input_3|12|Length|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|true|Percent?|
|v_input_6|0|MOM Choice: MOM2|MOM1|
|v_input_7|{{strategy.order.alert_message}}|Buy message|
|v_input_8|{{strategy.order.alert_message}}|Sell message|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-16 00:00:00
end: 2023-11-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Momentum Long Strategy", overlay = false, precision = 2, initial_capital = 10000, default_qty_value = 10000, default_qty_type = strategy.cash, commission_type = strategy.commission.percent, commission_value = 0, calc_on_every_tick = true)

// There will be no short entries, only exits from long.
strategy.risk.allow_entry_in(strategy.direction.long)

// Calculate start/end date and time condition
startDate  = input(timestamp("2021-01-02T00:00:00"), title = "Start Date", type = input.time)
finishDate = input(timestamp("2021-12-31T00:00:00"), title = "End Date",type = input.time)
 
time_cond  =true

// Momentum settings

i_len           =       input(defval = 12,      title = "Length",       minval = 1)
i_src           =       input(defval = close,   title = "Source")
i_percent       =       input(defval = true,    title = "Percent?")
i_mom           =       input(defval = "MOM2",  title = "MOM Choice",   options = ["MOM1", "MOM2"])

// Messages for buy and sell
message_buy  = input("{{strategy.order.alert_message}}", title="Buy message")
message_sell = input("{{strategy.order.alert_message}}", title="Sell message")

// Momentum code

momentum(seria, length, percent) =>
	_mom        =       percent ? ( (seria / seria[length]) - 1) * 100 : seria - seria[length]
	_mom

mom0        =       momentum(i_src, i_len, i_percent)
mom1        =       momentum(mom0, 1, i_percent)
mom2        =       momentum(i_src, 1, i_percent)

momX        =       mom1

if i_mom == "MOM2"
    momX    :=     mom2
    
// Strategy Alerts    

if (mom0 > 0 and momX > 0 and time_cond)
    strategy.entry("MomLE", strategy.long, stop = high + syminfo.mintick, comment = "MomLE", alert_message = message_buy)
else
	strategy.cancel("MomLE")
if (mom0 < 0 and momX < 0 and time_cond)
	strategy.entry("MomExit", strategy.short, stop = low - syminfo.mintick, comment = "MomSE", alert_message = message_sell)
else
	strategy.cancel("MomExit")
	
// Plotting

plot(0, color = #5d606b, title = "ZERO")
plot(mom0, color = #00bcd4, title = "MOM")
plot(mom1, color = #00FF00, title = "MOM1", display = display.none)
plot(mom2, color = #00FF00, title = "MOM2")
```

> Detail

https://www.fmz.com/strategy/432349

> Last Modified

2023-12-01 14:59:44
