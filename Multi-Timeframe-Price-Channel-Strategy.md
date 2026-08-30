
> Name

Multi-Timeframe-Price-Channel-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the highest price and lowest price EMA of multi-time frame prices to build channels to achieve short-term price reversal trading. It is a typical oscillator strategy.
## Strategy Principle
1. Calculate the EMA of the highest price and lowest price of the last 60 K lines in the 15-minute time frame to depict the upper and lower rails of the price channel.
2. The fast line is the 30-period EMA, and the slow line is the 60-period EMA.
3. When the fast line crosses the slow line, it is deemed that the upper rail of the channel is under pressure, and a bearish signal is sent, so go short.
4. When the fast line crosses the slow line, it is regarded as the lower track support of the channel, sending a bullish signal and going long.
5. After the reversal signal appears, use the characteristics of the short-term price return channel middle to achieve profits.
## Advantage Analysis
1. Multiple time frames can provide more comprehensive price information.
2. EMA smoothes prices and helps determine the general trend.
3. The intersection of fast and slow lines is easy to form a trading signal.
4. Short-term reversals are easy to make profits and reduce time risks.
## Risk Analysis
1. Multiple time frames increase complexity and make parameter optimization difficult.
2. Relying on a single indicator can easily be reversed by a breakthrough.
3. If there is no stop-loss or profit-stop point, there is a greater risk of loss.
4. High transaction frequency increases transaction costs.
## Optimization direction
1. Test different time frame parameter combinations to find the best match.
2. Add trailing stop loss or other indicator filters to control risks.
3. Combine with trading volume indicators to avoid arbitrage and false breakthroughs.
4. Set take-profit and stop-loss points to control risks while making profits.
5. Add opening limits and other money management strategies.
## Summarize
This strategy attempts to use multiple time frames to construct a short-term reversal trading strategy. However, it has problems such as difficulty in optimizing parameters and insufficient risk control. It is necessary to further optimize the signal generation logic and risk management scheme before it can be applied in practice.
|| 

## Overview

This strategy uses EMA of highest and lowest prices from multiple timeframes to build price channels and trade short-term reversals. It belongs to the category of oscillation indicator strategies.

## Strategy Logic

1. Calculate EMA of highest and lowest prices of recent 60 bars on 15m timeframe to plot price channel bands.

2. Fast line is 30-period EMA, slow line is 60-period EMA. 

3. When fast line crosses below slow line, it indicates downward pressure on upper band, giving bearish signal for short entry.

4. When fast line crosses above slow line, it indicates support of lower band, giving bullish signal for long entry.

5. After reversal signals, take profits from prices reverting back to channel middle.

## Advantages

1. Multiple timeframes provide more comprehensive price information.

2. EMA smooths price for determining overall trend.

3. Fast and slow line crossovers easily form trade signals. 

4. Short-term reversals allow quick profits and reduce time risk.

## Risks

1. Multiple timeframes increase complexity in parameter optimization.

2. Reliance on single indicator makes it vulnerable to false breakouts.

3. No stop loss or take profit settings expose to larger loss risks.

4. High trade frequency increases transaction costs.

## Optimization

1. Test different timeframe combinations to find optimal match.

2. Add trailing stop loss or other filters to control risks.

3. Incorporate volume to avoid traps and false breakouts.

4. Set stop loss and take profit points to lock in profits and limit risks.

5. Add position sizing and other capital management strategies. 

## Summary

The strategy attempts to build short-term reversal system using multiple timeframes. But it has issues like difficult parameter optimization and insufficient risk control. Further enhancements are needed in signal logic and risk management for practical application.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-09 00:00:00
end: 2023-09-14 09:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Just_Try_Different_Things", overlay=true)


Sig = security(syminfo.tickerid,'15',open)

H = ema(highest(Sig,60),60)
L = ema(lowest(Sig,60),60)




longCondition = crossunder(sma(H, 30), sma(H, 60))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = crossover(sma(L, 30), sma(L, 60))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
```

> Detail

https://www.fmz.com/strategy/427071

> Last Modified

2023-09-17 18:39:41
