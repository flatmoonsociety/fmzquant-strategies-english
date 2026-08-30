
> Name

Moving-Average-Strategy-with-Dynamic-Profit-Target
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy determines the trend direction based on the moving average, takes profit with a certain proportion of ATR, and dynamically adjusts positions based on ATR. The goal is to follow trends and make profits while controlling risks.
## Principle
The strategy uses a simple moving average of length N to determine the trend direction. When the short-term SMA crosses above the long-term SMA, go long; when the short-term SMA crosses below the long-term SMA, go short.
After entering the market, the strategy uses a certain multiple of ATR as the take-profit level. For long positions, the take-profit level is Entry Price + ATR * Factor. Take profit when the price exceeds the take profit level.
In addition, the strategy adjusts positions based on the size of ATR. ATR size represents market volatility, and position size is inversely proportional to ATR. The larger the ATR, the smaller the position.
## Advantages
1. Use the moving average to determine the direction of the trend and have a certain ability to track the trend.
2. The ATR stop profit method can make profits while avoiding reversals.
3. Dynamic position adjustment can control risks according to the degree of market fluctuations.
4. Take-profit factors and position parameters can be customized.
5. Incorporate stop losses to further limit risk.
## Risks and Solutions
1. There is a lag in the moving average, which may lead to slow entry. More sensitive parameters can be tested.
2. Changes in ATR size may cause the take profit to be too small or too large. ATR moving average can be added to extract its trend.
3. When the fluctuation is too large, the position may be too small, affecting profits. You can set the lower limit of the position.
4. Failure to set a stop loss leads to the risk of loss expansion. A trailing stop loss strategy can be added.
5. If the target is improperly selected, such as low-volatility assets, the strategy may not be effective. You should choose targets with greater volatility.
## Optimization ideas
1. Test different parameter combinations to find optimal parameters.
2. Optimize the position opening logic, such as adding other indicator filters.
3. Research dynamic take-profit and stop-loss strategies to make take-profit and stop-loss more flexible.
4. Combine volatility indicators for position management.
5. Add a re-entry mechanism to extend the holding time.
## Summarize
This strategy uses moving averages to determine trends, takes profits based on the ATR ratio, and dynamically adjusts positions. The advantage is that it has certain trend tracking capabilities and can control risks through parameter adjustment. However, there are problems such as difficulty in parameter selection and excessive take-profit. It can be further improved through indicator optimization and stop-loss strategies to make the strategy more robust.
|| 

## Overview

This strategy identifies trend using moving averages, takes profit at fixed ATR multiples, and dynamically sizes positions based on ATR. It aims to ride trends for profit while controlling risk.

## Principles

The strategy uses Simple Moving Average of length N to determine trend direction. It goes long when short SMA crosses above long SMA, and goes short when crossing below.

After entry, profit target is set at fixed ATR multiples from entry price, e.g. Profit Target = Entry Price + ATR * Factor for longs. Profit is taken when price hit profit target.

Strategy also sizes positions inversely to ATR, which represents market volatility. Larger ATR means smaller position size.

## Advantages

1. MA identifies trend, allowing trend following.

2. ATR profit taking profits from trends while avoiding reversals.

3. Dynamic position sizing manages risk according to market volatility.

4. Customizable profit factor and sizing parameters.

5. Stop loss can further limit risks.

## Risks and Mitigations

1. MA lag may cause late entry. More sensitive parameters can be tested.

2. ATR fluctuations may result in profit targets too small or large. Can use ATR moving average for trend.

3. Excessive volatility leads to too small positions limiting profits. Can set position size floor.  

4. Lack of stop loss risks uncontrolled loss. Can add moving stop loss.

5. Poor symbol selection, e.g. low volatility assets, may lead to underperformance. Should pick high volatility symbols.

## Enhancement Opportunities

1. Test different parameter combinations for optimal settings.

2. Improve entry logic by adding other indicators as filter. 

3. Research dynamic profit taking and stop loss for flexibility.

4. Manage positions based on volatility indicators. 

5. Add re-entry mechanism to prolong holding period.

## Summary

The strategy identifies trend with moving averages, takes profit at ATR multiples and sizes position by ATR. It has some trend following capacity and risk can be adjusted through parameters. But parameter selection and profit target problems exist. Further improvements can be made via optimization, stop loss to make strategy more robust.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|80|period|
|v_input_2|252|ptper|
|v_input_3|12|ptfactor|
|v_input_4|20|sizeper|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-10 00:00:00
end: 2023-09-17 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © dongyun

//@version=4
strategy("利润目标止损的移动平均线", overlay=true)

period = input(80,'')
ptper = input(252,'')
ptfactor = input(12,'')
sizeper = input(20, '')

trend = 0.0
signal = 0
size = 1.0
investment = 100000
atrange = 0.0
ptrange = 0.0
stoph = 0.0
stopl = 0.0


if sizeper != 0
	atrange := atr(sizeper)

if atrange == 0 or sizeper == 0 
	size := 1
else
	size := investment/atrange * 0.1

trend := sma(close,period)


if signal != 1 and nz(trend[1]) < nz(trend[2]) and trend > nz(trend[1])
	strategy.entry('long',strategy.long, comment='open_long')
	signal := 1
else
    signal := nz(signal[1])
    
if signal != -1 and nz(trend[1]) > nz(trend[2]) and trend < nz(trend[1])
	strategy.entry('short',strategy.short, comment='open_short')
	signal := -1
else
    if signal == 0
        signal := nz(signal[1])

ptrange := atr(ptper)

if strategy.position_size > 0
	strategy.exit("exit_long", "long", qty = strategy.position_size, limit = close + ptfactor*ptrange , comment='trail_long') 
else
	if strategy.position_size < 0
		strategy.exit("exit_short", "short", qty = abs(strategy.position_size), limit = close - ptfactor*ptrange, comment='trail_short')

```

> Detail

https://www.fmz.com/strategy/427187

> Last Modified

2023-09-18 21:46:47
