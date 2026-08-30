
> Name

Long and short automatic trading strategy Supertrend-Tracking-Strategy based on super trend indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1c1d69db1e551d6c2c3.png)
 [trans]
## Overview
This strategy is called "Super Trend Following Strategy". This strategy develops a long-short automatic trading system based on the super-trend indicator, which can automatically identify the trend direction and combine the RSI indicator and the ADX indicator for entry and exit.
## Strategy Principle
This strategy is mainly based on super-trend indicators to determine the current price trend. The super-trend indicator combines moving averages and ATR, which can effectively determine the direction of price trends. When the direction of the supertrend indicator changes, it indicates that the price trend has changed.
Specifically, the strategy first calculates the direction of the supertrend indicator, as well as the RSI indicator and the ADX indicator. When the direction of the super-trend indicator turns downward and the RSI indicator shows that the bullish strength has subsided, enter the market short. When the super-trend indicator turns upward again, execute short closing.
## Advantage Analysis
The biggest advantage of this strategy is that it can automatically identify price trends and conduct entry and exit based on the trend without manual judgment. In addition, filtering by combining the RSI indicator and the ADX indicator can effectively filter out false breakthroughs and increase the probability of profit.
## Risk Analysis
The biggest risk of this strategy is that the accuracy of the super-trend indicator itself in judging the price trend is not high, and wrong signals may appear. In addition, without a stop-loss mechanism, a single loss may be large.
You can optimize and reduce risks by adjusting the parameters of the super-trend indicator and adding a trailing stop loss.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize super-trend indicator parameters and improve judgment accuracy
2. Add a trailing stop loss mechanism to control single losses
3. Combine more indicators for filtering, such as Bollinger Bands, KDJ, etc., to increase the probability of profit
4. Develop similar long entry and exit strategies to make the strategy comprehensive
## Summarize
Generally speaking, this strategy is an automated trading strategy based on super-trend indicators to determine trends. The advantage is that it has a high degree of automation and can automatically determine the trend and enter the market. The disadvantage is that the accuracy of the super trend indicator itself is average and there is no stop loss set up. By optimizing parameters and adding other indicators, the probability of profit can be increased, and adding stop loss can control risks, making the strategy more powerful.
||

## Overview

This strategy is named "Supertrend Tracking Strategy". It develops an automated trading system for both long and short positions based on the Supertrend indicator, which can automatically identify the trend direction and make entries and exits combined with the RSI and ADX indicators.

## Principles 

The core of this strategy is using the Supertrend indicator to determine the current price trend. The Supertrend combines moving averages and ATR, which is effective in judging the direction of price trends. When the direction of the Supertrend makes a reversal, it signals that the price trend is changing.

Specifically, this strategy first calculates the Supertrend direction, RSI and ADX. When the Supertrend turns down, and the RSI shows that the uptrend is fading, it makes short entry. When the Supertrend turns up again, it closes the short position.

## Advantages

The biggest advantage of this strategy is that it can automatically identify price trends and make entries and exits based on the trends, without manual judgment. In addition, using RSI and ADX as filters can effectively avoid false breakouts and improve profitability. 

## Risks

The biggest risk is that the Supertrend itself is not highly accurate in judging price trends, which may generate incorrect signals. Also, no stop loss is set, so the loss per trade can be significant.

Optimization can be made by adjusting Supertrend parameters and adding trailing stop loss to reduce risks.

## Optimization

Several aspects of this strategy can be optimized:

1. Optimize Supertrend parameters to improve accuracy

2. Add trailing stop loss to control per trade loss

3. Add more filters like Bollinger Bands, KDJ to improve profitability 

4. Develop similar long entry and exit rules to make the strategy complete

## Conclusion

In conclusion, this is an automated trading strategy that judges trends based on the Supertrend. The advantage is high degree of automatization and auto trend detection. The disadvantage is the low accuracy of Supertrend itself and no stop loss. Parameter tuning, adding filters, and stop loss can enhance profitability and risk control.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|ATR Length|
|v_input_float_1|3|Factor|
|v_input_2|7|ADX Smoothing|
|v_input_3|7|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-16 00:00:00
end: 2024-01-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Supertrend Strategy", overlay=true)

atrPeriod = input(10, "ATR Length")
factor = input.float(3.0, "Factor", step = 0.01)

[_, direction] = ta.supertrend(factor, atrPeriod)

adxlen = input(7, title="ADX Smoothing")
dilen = input(7, title="DI Length")
dirmov(len) =>
    up = ta.change(high)
    down = -ta.change(low)
    plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
    minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
    truerange = ta.rma(ta.tr, len)
    plus = fixnan(100 * ta.rma(plusDM, len) / truerange)
    minus = fixnan(100 * ta.rma(minusDM, len) / truerange)
    [plus, minus]

adx(dilen, adxlen) =>
    [plus, minus] = dirmov(dilen)
    sum = plus + minus
    adx = 100 * ta.rma(math.abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
    adx

sig = adx(dilen, adxlen)

if ta.change(direction) < 0 and ta.rsi(close, 21) < 66 and ta.rsi(close, 3) > 80 and ta.rsi(close, 28) > 49 and sig > 20
    strategy.entry("My Long Entry Id", strategy.long)

if ta.change(direction) > 0
    strategy.close("My Long Entry Id")

//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)

```

> Detail

https://www.fmz.com/strategy/439762

> Last Modified

2024-01-23 15:36:27
