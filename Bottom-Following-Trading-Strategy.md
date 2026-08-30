
> Name

Bottom-Following-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The bottom following trading strategy is a low risk, low return cryptocurrency trading strategy. It works by identifying when a cryptocurrency is oversold, taking a position and then closing the position at a profit when the price stabilizes. This strategy is suitable for short-term and mid-term trading and can provide stable capital growth.
## Principle
This strategy relies primarily on the fast RSI indicator to determine whether a cryptocurrency is oversold. When the Rapid RSI is below 10, it indicates that the asset is seriously oversold. At this time, if the trading volume is significantly enlarged and the price has bottomed out, it will be a signal to establish a long position.
Once the price stabilizes again and the rapid RSI returns to the neutral zone, the long position can be closed for profit. In order to control risks, you can set a stop loss price in advance.
## Advantages
- This strategy has the ability to accurately judge the bottom and seize the best opportunity for rebound.
- Using the fast RSI indicator, you can quickly determine the oversold and overbought status.
- Only open positions near significant bottoms to effectively control risks.
- Use stop loss to lock in profits and avoid losses from expanding.
- Applicable to most cryptocurrencies and highly flexible.
## Risk
- If you make a wrong judgment and open a position at a position other than the bottom, it may cause large losses.
- Even if you catch the bottom, the market may not rebound enough to make a profit.
- The stop loss setting is too loose and may cause larger losses.
- The stop loss setting is too aggressive and the loss may be stopped prematurely.
- Insufficient trading volume to establish a large enough position in the right position.
## Ways to deal with risks
- Use multiple indicators to confirm the bottom and improve the accuracy of judgment.
- Open positions in batches to reduce the proportion of a single position.
- Set a reasonable stop loss distance according to the fluctuation range.
- Seize the breakthrough of the upward channel or important pressure level as the basis for taking profit.
- Choose trading pairs with sufficient trading volume to ensure sufficient liquidity.
## Summarize
Bottom-following trading strategies allow for lower-risk capital growth by catching oversold bottoms in cryptocurrencies. This strategy uses rapid RSI to determine the time point and cooperates with stop loss to control risks. If optimization and improvements are made, more stable returns are expected. This is a recommended low-risk cryptocurrency trading strategy.
||

## Overview

The bottom following trading strategy is a low-risk, low-return cryptocurrency trading strategy. It establishes long positions when cryptocurrencies are oversold and closes positions when prices recover. This strategy is suitable for short-term and medium-term trading and provides stable capital growth.

## Principles 

This strategy mainly uses the fast RSI indicator to determine if a cryptocurrency is oversold. When the fast RSI is below 10, it indicates the asset is severely oversold. At this point, if trading volume increases significantly and prices start to rebound from the bottom, it signals establishing long positions.

Once prices stabilize and the fast RSI returns to the neutral zone, long positions can be closed for profit. Stop-loss orders can be set beforehand to control risks.

## Advantages

- The strategy accurately identifies bottoms and catches ideal entry points.

- The fast RSI indicator quickly reveals oversold and overbought conditions. 

- Only long positions near significant bottoms, effectively controlling risks.

- Stop-loss locks in profits and avoids expanding losses.

- Applicable to most cryptocurrencies, high flexibility.

## Risks

- Incorrect judgment may lead to large losses if long positions are opened away from bottoms.

- Even with correct bottom picks, rebounds may be insufficient for profits. 

- Stop-loss set too wide may lead to large losses.

- Stop-loss set too tight may be triggered prematurely. 

- Insufficient trading volume prevents building large enough positions.

## Risk Management

- Use multiple indicators to improve accuracy of bottom confirmation.

- Scale in positions to lower allocation per entry.

- Set reasonable stop-loss distance based on volatility.

- Take profit when breaking above channels or resistance.

- Select liquid trading pairs to ensure sufficient liquidity.

## Summary

The bottom following strategy capitalizes on oversold bottoms of cryptocurrencies for low-risk capital growth. It utilizes fast RSI for timing and stop-loss for risk control. Further optimizations may lead to more consistent profits. It is a recommended low-risk crypto trading strategy worth considering.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-16 00:00:00
end: 2023-09-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Noro's CryptoBottom Strategy", shorttitle = "CryptoBottom str", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value=100.0, pyramiding=0)

//Fast RSI
src = close
fastup = rma(max(change(src), 0), 2)
fastdown = rma(-min(change(src), 0), 2)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

mac = sma(close, 10)
len = abs(close - mac)
sma = sma(len, 100)
max = max(open, close)
min = min(open, close)
up = close < open and len > sma * 3 and min < min[1] and fastrsi < 10 ? 1 : 0
//dn = close > open and len > sma * 3 and max > max[1] and fastrsi > 90 ? 1 : 0
plotarrow(up == 1 ? 1 : na, colorup = blue, colordown = blue)
//plotarrow(dn == 1 ? -1 : na, colorup = blue, colordown = blue)

sell = sma(close, 5)
dn = high > sell ? 1 : 0
plot(sell)

longCondition = up == 1
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = dn == 1
if (shortCondition)
    strategy.entry("Exit", strategy.short, 0)
```

> Detail

https://www.fmz.com/strategy/426990

> Last Modified

2023-09-16 18:37:44
