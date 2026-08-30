
> Name

Coppock-Curve-Based-Quantitative-Trading-Strategy based on Coppock Curve
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d00c72563fbd3d295abd559134ca05311586ba9483dd7744ef4d70a501ffe2c2.png)
[trans]

## Overview
This strategy utilizes the lesser-known Coppock Curve technical indicator to achieve quantitative trading. The Coppock Curve is derived by calculating a weighted moving average of the rate of change of the S&P 500 Index or trading equivalent. A buy signal is generated when the Coppock curve crosses the zero line above, and a sell signal is generated when it crosses the zero line below. Optionally use a trailing stop to lock in profits. This strategy uses the Coppock Curve of $SPY as a proxy signal for buying and selling other ETFs and stocks.
## Principle
This strategy uses the Coppock curve as a technical indicator to generate trading signals. The calculation formula of Coppock curve is:
Coppock curve = 10-period weighted moving average (14-period rate of change ROC + 11-period rate of change ROC)
The calculation formula of the rate of change ROC is: (Current Close - Close N cycles ago) / Close N cycles ago
The strategy calculates its Coppock curve based on the closing price of $SPY. A buy signal is generated when the curve crosses the zero line above, and a sell signal is generated when it crosses the zero line below.
## Advantages
- Use the unique Coppock curve indicator, which is more forward-looking than common indicators such as moving averages.
- Configurable indicator parameters for optimization, such as weighted moving average period, rate of change calculation period, etc.
- Using $SPY as the signal source, it has strong market representativeness
- You can choose trailing stop to lock in profits and reduce drawdowns
## Risk
- The Coppock curve is not a very popular indicator and its validity needs to be verified
- Trading signals may be delayed and parameters need to be optimized
- Stop loss settings that are too loose may miss retracement opportunities
- Relying on a single indicator can easily produce false signals
## Optimization direction
- Test different markets and stocks to optimize the best parameter combination
- Combine with other indicators to filter false signals, such as trading volume
- Dynamically optimized stop loss percentage
- Consider number of trades or price breakouts as entries
## Summarize
This strategy utilizes the unique curve shape characteristics of the Coppock curve to generate trading signals. Compared with common indicators, the Coppock curve is more forward-looking. However, its reliability as an independent indicator still needs to be verified, and it is recommended to be used in combination with other factors to filter out false signals. Through parameter optimization, stop loss optimization, and combination with other indicators, this strategy can become an effective quantitative trading system.
||


## Overview

This strategy utilizes the lesser known Coppock Curve technical indicator to implement quantitative trading. The Coppock Curve is derived by taking a weighted moving average of the rate of change (ROC) of a market index like S&P 500 or a trading equivalent like SPY ETF. Buy signals are generated when the Coppock Curve crosses above zero and sell signals when it crosses below. An optional trailing stop loss is available to lock in profits. The strategy uses $SPY Coppock curve as a proxy to generate trade signals on other ETFs and stocks.

## Principles 

The strategy uses Coppock Curve as the technical indicator for generating trading signals. The Coppock Curve formula is:

Coppock Curve = 10-period WMA (14-period ROC + 11-period ROC)

Where ROC rate of change is calculated as: (Current Close - Close N periods ago) / Close N periods ago

The strategy calculates the Coppock Curve based on the closing price of $SPY. Buy signals are generated when the curve crosses above zero and sell signals when it crosses below.

## Advantages

- Uses unique Coppock Curve indicator which has better predictive power than common indicators like moving averages
- Configurable parameters for optimization like WMA period, ROC period etc. 
- Uses $SPY as signal source which has strong market representativeness
- Optional trailing stop loss to lock in profits and reduce drawdowns

## Risks

- Coppock Curve is not a widely used indicator, its efficacy needs validation
- Signal lag may exist, parameters need to be optimized
- Overly wide stop loss may miss pullback opportunities  
- Reliance on single indicator can produce false signals

## Optimization Directions

- Test optimal parameter combinations across different markets and stocks
- Combine with other indicators to filter out false signals e.g. volume
- Dynamic optimization of stop loss percentage
- Consider other entry signals like number of bars or price breakthroughs

## Conclusion

The strategy utilizes the unique curve shape characteristics of the Coppock Curve to generate trade signals. Compared to common indicators, the Coppock Curve has stronger predictive power. But as a standalone indicator, its reliability needs validation. It's recommended to combine it with other factors to filter false signals. Through parameter optimization, stop loss optimization and combining with other indicators, this strategy can become an effective quantitative trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|100|Trail Long Loss (%)|
|v_input_2|SPY|security|
|v_input_3|10|WMA Length|
|v_input_4|14|Long RoC Length|
|v_input_5|11|Short RoC Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-13 00:00:00
end: 2023-11-12 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © RolandoSantos

//@version=4
strategy(title = "Coppock Curve", shorttitle = "Copp Curve Strat", default_qty_type=strategy.cash, default_qty_value=10000, initial_capital=10000)

///trail stop
longTrailPerc = input(title="Trail Long Loss (%)", minval=0.0, step=0.1, defval=100) * 0.01

// Determine trail stop loss prices
longStopPrice = 0.0

longStopPrice := if (strategy.position_size > 0)
    stopValue = close * (1 - longTrailPerc)
    max(stopValue, longStopPrice[1])
else
    0
//Use SPY for Copp Curve entries and exits//
security = input("SPY")
ticker = security(security, "D", close)

///Copp Curve////
wmaLength = input(title="WMA Length", type=input.integer, defval=10)
longRoCLength = input(title="Long RoC Length", type=input.integer, defval=14)
shortRoCLength = input(title="Short RoC Length", type=input.integer, defval=11)
source = ticker
curve = wma(roc(source, longRoCLength) + roc(source, shortRoCLength), wmaLength)

///Lower Band Plot///
band1 = hline(0)
band0 = hline(100)
band2 = hline(-100)
fill(band1, band0, color=color.green, transp=90)
fill(band2, band1, color=color.red, transp=90)
plot(curve, color=color.white)

///Trade Conditions///
Bull = curve > 0
Bear = curve < 0

///Entries and Exits//
if (Bull)
    strategy.entry("Long", strategy.long, comment = "LE")
    

if (Bear)
    strategy.close("Long", qty_percent=100, comment="close")
    
// Submit exit orders for trail stop loss price
if (strategy.position_size > 0)
    strategy.exit(id="Long Trail Stop", stop=longStopPrice)
    

```

> Detail

https://www.fmz.com/strategy/431926

> Last Modified

2023-11-13 11:44:55
