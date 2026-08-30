
> Name

EMA-Trading-Strategy

> Author

ChaoZhang

> Strategy Description


[trans]
EMA trading strategy
This strategy is judged based on the EMA moving average. The specific trading rules are as follows:
- If the closing price of the previous day is higher than the EMA, enter long at the opening of the next day.
- If the current K-line closing price is lower than the EMA moving average, close the long order.
The advantages of this strategy are:
- Use EMA to determine trend direction
- The rules are simple, clear and easy to implement
- Customizable EMA period for optimization
But there are also some problems with this strategy:
- Easily generate false signals during consolidation
- The entry time is late and it is easy to get trapped
- There is no stop loss setting, and there is a risk of loss
- Failure to consider trading frequency and money management
Generally speaking, the EMA strategy is more suitable for trending markets, but it needs to be used with caution. Stop loss and filter conditions should be added to optimize the strategy.
||EMA Trading Strategy 

This strategy trades based on EMA analysis, with the following rules:

- Enter long if previous day's close is above EMA

- Exit long if current candle closes below EMA

Advantages of this strategy:

- Uses EMA to determine trend direction
- Simple and clear rules, easy to implement  
- Customizable EMA period for optimization

Potential issues:

- Prone to false signals during range-bound markets
- Late entry, risks being caught in whipsaws
- No stop loss, risks uncontrolled losses
- No trade frequency or position sizing rules 

Overall, the EMA strategy works better in trending markets but should be used cautiously. Adding stops and filters would help optimize the strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|Length|
|v_input_2|2000|Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ericdwyang

//@version=5
strategy("EMA Strat", overlay=true, margin_long=100, margin_short=100)

// EMA Variables
emaInput = input(21, "Length")
ema = ta.ema(close, emaInput)

// Variable Declaration
p = 0

start = false

// Start Date
yearInput = input(2000, "Year")
if (time >= timestamp(2000,01,01,01,01))
    start := true


// Check first candle relative to EMA
if (close > ema and start == true)
    p += 1
    strategy.entry("Long", strategy.long, comment = "Entry")
    

// Candle close above EMA (p + 1, count reset to 0)
above = close[1] > ema[1]
if (above)
    p += 1



// Candle close below EMA (reset p to 0, count -1)
below = close < ema
if (below)
    p := 0
    strategy.close("Long", comment = "Flat")

// // Exit Position
// if (redCount == -2)
//     strategy.close("Long", comment = "Flat")
    
// goLong = p[1] == 0 and p == 1
// flatten = p == 0
    
// // Restablish long    
// if (goLong and start == true)
//     strategy.entry("Long", strategy.long, comment = "Entry")
    

plot(p)
plot(ema)

    
```

> Detail

https://www.fmz.com/strategy/426338

> Last Modified

2023-09-11 12:02:56
