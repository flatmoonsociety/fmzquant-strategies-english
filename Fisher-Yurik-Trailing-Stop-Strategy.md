
> Name

Fisher-Yurik-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1c4c656f71fc2e16ad6.png)
[trans]

## Overview
The Fisherman indicator trailing stop strategy is a quantitative trading strategy that combines the Fisherman indicator and the trailing stop mechanism. This strategy uses the Fisherman indicator to generate buy and sell signals, and at the same time sets a trailing stop to lock in profits, protecting profits while striving for greater returns.
## Strategy Principle
1. Enter the date range to limit the time period for backtesting or real trading.
2. Enter the parameters of the fisherman indicator, the default is 2 periods
3. Enter the take-profit and stop-loss ratios. The default is 5% take-profit and 2% stop-loss.
4. Calculate the main line and signal line of the Fisherman indicator
5. A buy signal is generated when the main line crosses the signal line
6. Set a trailing stop loss, and stop loss when the price drops by 2% after entering a long position.
7. Take profit when the price rises by more than 5%
## Advantage Analysis
1. The Fisherman indicator is easy to judge the trend and the buying signal is accurate.
2. The trailing stop loss mechanism can lock in most profits while avoiding exceeding the set stop loss point.
3. Customizable parameters to adapt to different market environments
4. Simple to use, easy to understand and implement
## Risk Analysis
1. Improper parameter settings may lead to overly aggressive trading, so testing should be done with caution
2. Excessively large stop loss points may cause the impact of Outliers, leading to losses beyond expectations.
3. If the profit stop point is too small, profits may be taken out too early, affecting profitability.
4. Appropriate parameters should be determined according to different varieties
You can optimize parameters by adjusting the stop-loss and take-profit ratios and testing different parameter combinations; filter signals in combination with other indicators; and set position management rules to control single risk.
## Optimization direction
1. Optimize the parameters of the fisherman indicator and test the impact of different parameters on the strategy
2. Combine with other indicators, such as MACD, KD, etc. to filter signals to improve signal quality
3. Add condition judgment before opening a position, such as breaking through the upper Bollinger Band, etc.
4. Add a position management module to control the risks caused by a single position
5. Optimize trailing stop methods, such as smooth trailing stop, Chandelier Exit, etc.
## Summarize
The fisherman indicator moving stop strategy integrates trend judgment and stop loss management. Through parameter optimization, indicator combination and stop loss method improvement, it can be adapted to most varieties and obtain better returns while preventing excessive losses. It is worth exploring and practicing.
||

## Overview  

The Fisher Yurik trailing stop strategy is a quantitative trading strategy that integrates the Fisher Yurik indicator and trailing stop mechanisms. It uses the Fisher Yurik indicator to generate buy and sell signals while setting trailing stops to lock in profits, maximizing gains while protecting profits.

## Strategy Logic

1. Input date ranges to define backtest/live trading timeframe
2. Input parameters for Fisher Yurik indicator, default to 2 periods  
3. Input profit taking and stop loss ratios, default to 5% profit and 2% loss
4. Calculate main and signal lines of Fisher Yurik indicator
5. Generate buy signal when main line crosses above signal line
6. Set trailing stop, exit long position when price drops 2% after entry
7. Take profit when price rises above 5% 

## Advantage Analysis  

1. Fisher Yurik indicator easily identifies trends, accurate buy signals
2. Trailing stop locks in most profits while avoiding stops beyond threshold 
3. Customizable parameters suit different market environments
4. Simple and easy to understand implementation

## Risk Analysis

1. Improper parameter tuning may cause over-aggressive trading, require cautious testing
2. Stop loss too wide may lead to losses fromoutliers beyond expectations
3. Take profit too tight may cut wins short, limiting profitability
4. Appropriate parameters should be determined for different products

Risks can be addressed by adjusting stop/profit ratios, testing parameters, using signal filters, position sizing rules.

## Enhancement Opportunities

1. Optimize Fisher Yurik parameters for impact on strategy
2. Add signal filters like MACD, KD to improve signal quality
3. Add entry conditions like breakouts from Bollinger Bands  
4. Incorporate position sizing rules to control per trade risk
5. Enhance trailing stop methods, e.g. smoothed, Chandelier Exits

## Conclusion

The Fisher Yurik trailing stop strategy combines trend identification and risk management. With parameter tuning, indicator combinations, and stop loss enhancements, it can suit most instruments for good profits within acceptable risk tolerances.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2021|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|2|Period|
|v_input_float_1|1.05|profit level |
|v_input_float_2|1.02|after the signal|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-26 00:00:00
end: 2024-02-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Fisher_Yurik Strategy with Trailing Stop", shorttitle="FY Strategy", overlay=true)

// Date Ranges 
from_month = input(defval = 1, title = "From Month")
from_day   = input(defval = 1, title = "From Day")
from_year  = input(defval = 2021, title = "From Year")
to_month   = input(defval = 1, title = "To Month")
to_day     = input(defval = 1, title = "To Day")
to_year    = input(defval = 9999, title = "To Year")
start  = timestamp(from_year, from_month, from_day, 00, 00)  // backtest start window
finish = timestamp(to_year, to_month, to_day, 23, 59)        // backtest finish window
window = true
period = input(2, title='Period')
cost = input.float(1.05, title='profit level ', step=0.01)
dusus = input.float(1.02, title='after the signal', step=0.01)

var float Value = na
var float Fish = na
var float ExtBuffer1 = na
var float ExtBuffer2 = na

price = (high + low) / 2
MaxH = ta.highest(high, period)
MinL = ta.lowest(low, period)

Value := 0.33 * 2 * ((price - MinL) / (MaxH - MinL) - 0.5) + 0.67 * nz(Value[1])
Value := math.max(math.min(Value, 0.999), -0.999)
Fish := 0.5 * math.log((1 + Value) / (1 - Value)) + 0.5 * nz(Fish[1])

up = Fish >= 0

ExtBuffer1 := up ? Fish : na
ExtBuffer2 := up ? na : Fish

var float entryPrice = na
var float stopPrice = na
 
if (ExtBuffer1 > ExtBuffer1[1])
    entryPrice := close*dusus
    stopPrice := close * cost 
 
if (ExtBuffer2 < ExtBuffer2[1])
    entryPrice := close
    stopPrice := close * cost

// Sadece seçilen test döneminde işlem yapma koşulu eklenmiştir
strategy.entry("Buy", strategy.long, when=ExtBuffer1 > ExtBuffer1[1] and window)
strategy.exit("Take Profit/Trailing Stop", from_entry="Buy", when=(close >= entryPrice * cost) or (close < stopPrice), trail_offset=0.08, trail_price=entryPrice * cost)

```

> Detail

https://www.fmz.com/strategy/440833

> Last Modified

2024-02-02 14:57:33
