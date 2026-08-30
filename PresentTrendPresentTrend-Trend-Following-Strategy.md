
> Name

PresentTrend Trend Following StrategyPresentTrend-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
PresentTrend strategy is a unique custom trend following strategy. This strategy combines short-term and long-term market trends, making it suitable for different market conditions.
## Strategy Principle
The strategy consists of two parts:
1. Customized RSI or MFI indicator: This indicator calculates the PresentTrend value based on RSI or MFI, and generates buy and sell signals based on the golden cross and dead cross of this value, indicating potential trend reversal.
2. ATR indicator: This is a popular trend following indicator that uses the average true range (ATR).
When the buy and sell signals of both strategies are triggered at the same time, the strategy will open a long or short position. This ensures that trades only occur when short-term and long-term trends are aligned, increasing the reliability of the strategy.
## Strategic Advantages
- Combines short-term and long-term trends, suitable for different market conditions
- Use custom indicators and ATR to improve signal reliability
- You can choose to only do long, only short or two-way trading to adapt to different trading styles
- Default parameters are optimized to balance sensitivity and stability
- Adjust parameters and optimize strategies according to personal preferences
## Strategic risks and solutions
- All trend following strategies have the risk of arbitrage
- Long and short two-way transactions may increase the number of transactions and handling fees
- Improper parameter settings may produce too many error signals
- Can appropriately shorten the trading position cycle and reduce arbitrage risks
- You can choose to only go long or short to reduce the number of transactions
- Parameters should be fully tested and adjusted appropriately to ensure they are reasonable
## Strategy optimization direction
- Add a stop loss mechanism to better control single losses
- Combine with other indicators to filter signals to reduce erroneous transactions
- Test different holding period parameters and find the optimal parameters
- Try to automatically optimize parameters based on machine learning
- Utilize more data sources, such as order flow information, etc.
- Optimize strategy code and improve execution efficiency
## Summarize
The PresentTrend strategy is overall a very effective trend following strategy. It combines both short-term and long-term trend indicators to increase signal reliability while maintaining sensitivity. By adjusting the direction, parameters and adding additional logic, the strategy can be adapted to different market environments and trader needs. While you still need to be aware of the risks inherent in trend following strategies, overall PresentTrend is an option worth considering.
|| 

## Overview

The PresentTrend strategy is a unique custom trend-following strategy. This combination allows the strategy to take advantage of both short-term and long-term market trends, making it suitable for various market conditions. 

## How it Works

The strategy consists of two parts:

1. Custom RSI or MFI indicator: This indicator calculates a PresentTrend value based on RSI or MFI, generating buy and sell signals based on its crossover and crossunder, indicating potential trend reversals.

2. ATR indicator: A popular trend-following indicator using Average True Range (ATR).

The strategy enters a long position when all buy signals from both strategies are true, and a short position when all sell signals are true. This ensures trades are entered only when both short-term and long-term trends align, potentially increasing the strategy's reliability.

## Advantages

- Combines short-term and long-term trends, adaptable to different market conditions
- Uses custom indicator and ATR for increased signal reliability  
- Option for long-only, short-only or dual direction trading suits different trading styles
- Default parameters optimized for balance of sensitivity and stability
- Parameters can be adjusted based on personal preference for optimization

## Risks and Solutions

- Vulnerable to whipsaws like all trend-following strategies
- Dual direction trading can increase number of trades and fees
- Poor parameter tuning may generate excessive false signals
- Can use shorter holding periods to reduce whipsaw risk
- Option for long or short only reduces number of trades  
- Parameters should be thoroughly tested and tuned to ensure viability

## Optimization Directions 

- Add stop loss mechanisms for better loss control
- Filter signals with additional indicators to reduce false trades
- Test different holding period parameters to find optimum  
- Explore machine learning for automated parameter optimization
- Incorporate more data sources like order flow information
- Optimize strategy code for improved execution efficiency

## Conclusion

Overall, the PresentTrend strategy is a highly effective trend-following system. It combines short-term and long-term trend indicators to be sensitive while improving signal reliability. With adjustable direction, parameters, and additional logic, the strategy can adapt to different market environments and trader needs. While inherent trend-following risks remain, PresentTrend is a compelling option worth considering.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|0|Trade Direction: Both|Short|Long|
|v_input_source_1_hlc3|0|(?PresentTrend)Source: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_int_1|14|Length|
|v_input_float_1|1.618|Multiplier|
|v_input_bool_1|false|Whether to use RSI or MFI|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © PresentTrading

//@version=5

// Define the strategy settings
strategy('PresentTrend - Strategy [presentTrading]' , overlay=true, precision=3, default_qty_type=strategy.cash, 
 commission_value= 0.1, commission_type=strategy.commission.percent, slippage= 1, 
  currency=currency.USD, default_qty_type = strategy.percent_of_equity, default_qty_value = 10, initial_capital= 10000)

// Define the input parameters
priceSource  = input.source(title='Source', defval=hlc3, group='PresentTrend') // The price source to use
lengthParam  = input.int(title='Length', defval=14, group='PresentTrend') // The length of the moving average
multiplier = input.float(title='Multiplier', defval=1.618, step=0.1, group='PresentTrend') // The multiplier for the ATR
indicatorChoice  = input.bool(title='Whether to use RSI or MFI', defval=false, group='PresentTrend') // Whether to use RSI or MFI

// Add a parameter for choosing Long or Short
tradeDirection = input.string(title="Trade Direction", defval="Both", options=["Long", "Short", "Both"])

// Calculate the ATR and the upT and downT values
ATR = ta.sma(ta.tr, lengthParam)
upperThreshold = low - ATR * multiplier 
lowerThreshold  = high + ATR * multiplier 

// Initialize the PresentTrend indicator
PresentTrend = 0.0

// Calculate the PresentTrend indicator
PresentTrend := (indicatorChoice ? ta.rsi(priceSource, lengthParam) >= 50 : ta.mfi(hlc3, lengthParam) >= 50) ? upperThreshold < nz(PresentTrend[1]) ? nz(PresentTrend[1]) : upperThreshold : lowerThreshold > nz(PresentTrend[1]) ? nz(PresentTrend[1]) : lowerThreshold

// Calculate the buy and sell signals
longSignal  = ta.crossover(PresentTrend, PresentTrend[2])
shortSignal  = ta.crossunder(PresentTrend, PresentTrend[2])

// Calculate the number of bars since the last buy and sell signals
barsSinceBuy = ta.barssince(longSignal)
barsSinceSell = ta.barssince(shortSignal)
previousBuy = ta.barssince(longSignal[1])
previousSell = ta.barssince(shortSignal[1])

// Initialize the direction variable
trendDirection = 0

// Calculate the direction of the trend
trendDirection := longSignal and previousBuy > barsSinceSell ? 1 : shortSignal and previousSell > barsSinceBuy ? -1 : trendDirection[1]

// Check the trade direction parameter before entering a trade
if (trendDirection == 1 and (tradeDirection == "Long" or tradeDirection == "Both"))
    strategy.entry("Buy", strategy.long) 
if (trendDirection == -1 and (tradeDirection == "Short" or tradeDirection == "Both"))
    strategy.entry("Sell", strategy.short) 

// Add a stop mechanism when the tradeDirection is one-sided
if (tradeDirection == "Long" and trendDirection == -1)
    strategy.close("Buy")
if (tradeDirection == "Short" and trendDirection == 1)
    strategy.close("Sell")

// Visualization
plot(PresentTrend, color=color.blue, title="PresentTrend")
plotshape(series=longSignal, location=location.belowbar, color=color.green, style=shape.labelup, title="Buy Signal")
plotshape(series=shortSignal, location=location.abovebar, color=color.red, style=shape.labeldown, title="Sell Signal")

```

> Detail

https://www.fmz.com/strategy/427466

> Last Modified

2023-09-21 15:00:08
