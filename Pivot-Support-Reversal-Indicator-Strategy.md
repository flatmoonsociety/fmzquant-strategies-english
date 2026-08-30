
> Name

Pivot-Support-Reversal-Indicator-Strategy Pivot-Support-Reversal-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
This strategy combines the main axis support reversal indicator with support and resistance levels to achieve trend following and profit-taking retracements.
The specific rules are:
1. When the main axis support reversal indicator generates a buy signal, enter the market long at this point
2. First, make a profit of 25% on the R1 Partial position.
3. Then profit 25% of the position in R2 Partial position
4. Use trailing stop loss, the stop loss line is the 14-period moving average minus 3 times ATR
The main axis support reversal indicator combines CMO, Bollinger Bands, trading volume and other factors to form a strong trend signal. Support and resistance levels serve as profit targets and also have trend tracking functions. The advantage of this strategy lies in the setting of the profit retracement mechanism, which can strictly control risks while ensuring profits.
## Strategic Advantages
- Spindle support indicators combine multiple factors to identify high-probability opportunities
- Support and resistance levels are both profit targets and tracking functions
- Profit in stages combined with trailing stop loss to ensure profits and control risks
## Strategy Risk
- Spindle support index parameters need to be optimized and adjusted
- Support and resistance levels are sometimes breached
- Partial profits will expose you to the risk of remaining positions
## Summarize
This strategy makes full use of the combined signals of the main axis support indicators, and uses support and resistance levels as dynamic profit targets. It locks in profits and strictly controls risks through batch profit and stop losses. It is a pragmatic and feasible trading strategy.
[trans]

||

## Strategy Logic

This strategy combines the Pivot Support Reversal indicator with support/resistance levels to track trends and manage profit/drawdown. 

The rules are:

1. Go long when the PSR indicator generates a buy signal

2. Take 25% partial profit at R1 

3. Take another 25% partial profit at R2

4. Use a moving stop loss below the 14-period moving average minus 3xATR

The PSR indicator synthesizes CMO, Bollinger Bands, volume and more into high-probability signals. Pivot points act as profit targets while having trend-following ability. The strategy's strength lies in its staged profit taking and disciplined stop loss to lock in profits while tightly controlling risk.

## Advantages 

- PSR combines multiple factors for high-quality signals

- Pivots act as profit targets and tracking tools

- Staged profit taking and trailing stop protects profits and manages risk

## Risks

- PSR parameters need optimization 

- Pivots can sometimes be breached

- Risk remains for residual position after partial profits

## Summary

This strategy capitalizes on the PSR indicator's syndicated signals and uses pivots as dynamic profit targets. By taking profits in batches and cutting losses fast, it aims to pragmatically book profits while tightly controlling risk.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-13 00:00:00
period: 3d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ParaBellum68

//@version=4
strategy(title="SOJA PIVOT", shorttitle="SOJA PIVOT")
soja = ((cmo(close,5) > 25) and (cmo(close,5) < 70) and (close> close[1]) and (bbw(close,50,1) < 0.6) and (sum(volume,5)> 250000) and (obv[5]>15))
TP = 2.1 * hlc3[1]- high[1]
TP2 = TP + high[1] - low[1]
SL = avg(close,14) - 3*atr(14)
strategy.entry("buy", true, 1, when = soja == 1)
strategy.close("buy", when = close > TP)
strategy.close("buy", when = close > TP2)
strategy.exit("stop", "exit", when = close < SL)





```

> Detail

https://www.fmz.com/strategy/426785

> Last Modified

2023-09-14 15:49:31
