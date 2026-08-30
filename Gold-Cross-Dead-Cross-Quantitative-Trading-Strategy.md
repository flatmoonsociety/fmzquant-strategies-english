
> Name

Gold-Cross-Dead-Cross-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1768cebdd183dccd1c2.png)
[trans]
### Overview
This strategy calculates the intersection of the 30-day simple moving average (MA30) and the 200-day simple moving average (MA200) of XAUUSD (gold) to achieve quantitative transactions of golden cross buying and dead cross selling. This strategy sets both stop-loss and take-profit prices and can automatically close positions.
### Strategy Principles
The core indicators of this strategy are MA30 and MA200. When MA30 crosses above MA200, a buy signal is generated; when MA30 crosses below MA200, a sell signal is generated. This cross is called the "golden cross" and the "dead cross".
Specifically, the strategy uses the ta library to calculate MA30 and MA200. Then judge their crossover status through the ta.crossover and ta.crossunder functions. When an upward cross (golden cross) occurs, set the longCondition value to true and perform a buying operation; when a downward cross (death cross) occurs, set the shortCondition value to true and perform a selling operation.
In terms of transaction execution, stop-loss and take-profit prices of 40,000 points are set for buy and sell orders respectively. This is equivalent to a price movement of 4000 pips in XAUUSD. When the price triggers stop loss or take profit, orders will be automatically closed.
In addition, the strategy also sets up a hedging mechanism. If you currently hold a long position and a dead cross signal appears subsequently, the position will be closed and reversed directly; if you currently hold a short position and a golden cross signal appears subsequently, the position will be closed and reversed directly. This avoids taking big losses when the trend reverses.
### Strategic Advantages
This is a very simple and intuitive trend following strategy. It has the following advantages:
1. The rules are clear and easy to implement.
2. Can be used in multiple time periods, suitable for intraday and long-term operations.
3. Comply with market cyclicality and capture trend reversals.
4. Set up a stop-loss and take-profit automatic exit mechanism to control single losses.
5. Establish a hedging mechanism to avoid losses caused by trend reversal.
### Risk Analysis
There are also some risks with this strategy:
1. The MA indicator lags behind and may miss the best entry opportunity for short-term trend reversal.
2. If the stop loss price is set unreasonably, the trade may be stopped prematurely.
3. Too much interference from reversal signals increases the number of unnecessary transactions.
4. This strategy also has certain requirements for the size of trading funds and needs to withstand a certain drawdown.
In order to control these risks, parameters can be optimized, stop loss ranges adjusted, reversal signals filtered, etc.
### Strategy optimization
This strategy can be optimized from the following aspects:
1. Optimize MA parameters and use EMA or weighted moving average instead.
2. Add other indicator filters, such as trading volume, shock indicators, etc. 
3. Hedging mechanisms can be enabled only on significant signals.
4. Position size management can be set up to optimize capital utilization efficiency.
5. Can combine machine learning algorithms to dynamically optimize stop loss and profit settings.
Through parameter adjustment, adding filters, position management and other means, the stability of the strategy can be further improved.
### Summarize
This strategy is a simple and practical moving average crossover strategy. It operates in line with the market cycle and controls risks by setting automatic stop-loss, stop-profit, position closing and hedging mechanisms. This strategy is easy to understand and implement, and can be applied to a variety of trading varieties and time periods. Through further optimization, a better risk-return ratio can be obtained, which is a recommended quantitative trading strategy.
||

### Overview

This strategy calculates the 30-day simple moving average (MA30) and 200-day simple moving average (MA200) crossovers of XAUUSD (gold) to implement gold cross buys and dead cross sells quantitative trading. The strategy also sets stop loss and take profit prices for automatic position closing.

### Strategy Principle

The core indicators of this strategy are MA30 and MA200. When MA30 crosses above MA200, a buy signal is generated. When MA30 crosses below MA200, a sell signal is generated. These crosses are called "gold crosses" and "dead crosses".  

Specifically, the strategy uses the ta library to calculate MA30 and MA200. The ta.crossover and ta.crossunder functions then judge if they cross. When an upward crossover (gold cross) occurs, the longCondition value is set to true for buying. When a downward crossover (dead cross) occurs, the shortCondition value is set to true for selling.

For order execution, stop loss and take profit prices of 40,000 points each are set for long and short trades. This corresponds to a 4,000 point price change in XAUUSD. When the price triggers the stop loss or take profit, orders will close positions automatically.  

In addition, a hedging mechanism is established in the strategy. If the current position is long, a subsequent dead cross signal will directly flatten the position and reverse it. If the current position is short, a subsequent gold cross signal will also directly flatten and reverse the position. This avoids large losses during trend reversions.

### Advantages

This is a very simple and intuitive trend following strategy. It has the following advantages:

1. Clear rules that are easy to implement.  
2. Applicable to multiple time frames for day and long term trading.
3. Aligns with market cycles and captures trend reversions. 
4. Sets auto exit mechanism with stop loss/profit to control single trade loss.
5. Establishes hedging to avoid losses from trend reversions.

### Risk Analysis 

There are some risks to this strategy:

1. MA indicators lag and may miss best entry for short term trend reversals.  
2. Improper stop loss setting may prematurely exit trades.
3. Too many reverse signals increase unnecessary trading.
4. The strategy has capital requirements to withstand drawdowns.

These risks can be managed by parameter optimization, adjusting stop loss levels, filtering reverse signals etc.

### Optimization

The strategy can be optimized in several ways:

1. Optimize MA parameters using EMA or weighted moving averages.
2. Add other filters like volume, volatility indicators etc.  
3. Enable hedging mechanism only on significant signals.
4. Set up position sizing for better capital efficiency.
5. Dynamically optimize stops/profits using machine learning algorithms.

Parameter tuning, adding filters, position sizing etc. can further improve strategy stability.  

### Conclusion

This is a simple and practical moving average crossover strategy. It aligns with market cycles, controls risk through automated stop loss/profit exits and hedging mechanisms. Easy to understand and implement, it is applicable for multiple products and time frames. Further optimizations can improve risk/reward profile. Overall an advisable quantitative trading strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estrategia de Cruce de Medias Móviles", overlay=true)

// Medias móviles
ma30 = ta.sma(close, 30)
ma60 = ta.sma(close, 60)
ma200 = ta.sma(close, 200)

// Cruce de medias móviles
crossoverUp = ta.crossover(ma30, ma200)
crossoverDown = ta.crossunder(ma30, ma200)

// Señales de compra y venta
longCondition = crossoverUp
shortCondition = crossoverDown

// Ejecución de órdenes
if (longCondition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Cover", "Buy", stop=close - 40.000, limit=close + 40.000)
if (shortCondition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Cover", "Sell", stop=close + 40.000, limit=close - 40.000)

// Plot de las medias móviles
plot(ma30, color=color.blue, title="MA 30")
plot(ma60, color=color.orange, title="MA 60")
plot(ma200, color=color.green, title="MA 200")

// Condiciones para cerrar la posición contraria
if (strategy.position_size > 0)
    if (crossoverDown)
        strategy.close("Buy")
if (strategy.position_size < 0)
    if (crossoverUp)
        strategy.close("Sell")
```

> Detail

https://www.fmz.com/strategy/440829

> Last Modified

2024-02-02 14:46:11
