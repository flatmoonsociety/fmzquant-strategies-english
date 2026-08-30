
> Name

Short-Mid-Term-Trend-Following-Strategy-Based-on-SMA-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/294afc42ad165909a625da2f4f342818e01d5e11ef920beb81127d8c146881eb.png)

[trans]

## Overview
The moving average crossover strategy is a trend following strategy that determines the market trend direction by calculating moving averages of different periods to issue buy and sell signals. This strategy uses the intersection of the 3-day and 50-day moving averages to make judgments. When the short-term moving average crosses the long-term moving average, it is bullish to buy, and when the short-term moving average crosses below the long-term moving average, it is bearish to sell.
## Strategy Principle
This strategy calculates the 3-day and 50-day simple moving averages. When the 3-day SMA crosses above the 50-day SMA, it indicates that the short-term trend has turned bullish and a buy signal is issued; when the 3-day SMA crosses below the 50-day SMA, it indicates that the short-term trend has turned bearish and a sell signal is issued. In order to reduce unnecessary transactions, this strategy also adds a mid-term 40-day SMA. If the 3-day SMA falls below the 40-day SMA, a sell signal will be issued to quickly stop the loss.
The key to this strategy is to use moving averages of different periods to divide different stages of market fluctuations. The 3-day SMA represents the short-term trend, and the 50-day SMA represents the mid-term trend. Their cross represents the conversion of short-term and mid-term trends, which can capture price changes on different time scales. Through this combined analysis of multiple timelines, the turning point of the market can be judged more accurately.
## Advantage Analysis
- The momentum crossover is clear and the signal is relatively clear. The crossover of SMAs of different periods can effectively judge changes in short-term and medium-term trends and avoid being disturbed by small market fluctuations.
- By quickly stopping sma3 and crossing sma40, you can reduce losses and control risks.
- The strategic ideas are simple, clear and easy to implement. Indicators and signal rules are directly operable.
- The parameters of SMA can be flexibly adjusted to adapt to different market conditions and trading varieties.
## Risk Analysis
- In sideways and non-clear trend markets, SMA cross signals are frequent, which may lead to excessive trading and increased transaction costs and slippage losses.
- SMA has hysteresis. When the cross signal is issued, the price has already changed to a certain extent, which can easily cause the strategy to miss the best buying and selling points.
- Fixed SMA parameters are not suitable for all market conditions and need to be used with parameter optimization.
- A single indicator is susceptible to failure, so you can consider adding other technical indicators or fundamental indicators for combined verification.
## Optimization direction
- Optimize SMA cycle parameters and find the best parameter combination
- Add stochastic, MACD and other indicators to verify signals to avoid false signals
- Adjust the opening lot size and stop loss range according to market changes
- Consider adding fundamental indicators, such as financial reports, news, etc. to the combination
- Combined with volume and energy indicators, open positions when high volume breaks out
## Summarize
The moving average crossover strategy determines changes in the short-term and mid-term market trends through the crossover of SMAs of different periods, and adopts trend tracking, which is a relatively simple and direct trend strategy. The advantage of this strategy is that it has clear ideas and is easy to operate. The strategy effect can be improved through parameter optimization and indicator combination verification. However, SMA itself has hysteresis and cannot accurately capture the turning point. It is recommended to use it in combination with other leading indicators to follow the trend and make profits under the general trend.
||

## Overview

The moving average crossover strategy is a trend following strategy that uses the crossover of different period moving averages to determine market trend direction and generate buy and sell signals. This strategy uses the crossover of 3-period and 50-period simple moving averages (SMA) to make judgments. When the short-term SMA crosses above the long-term SMA, it is considered a bullish signal to buy. When the short-term SMA crosses below the long-term SMA, it is considered a bearish signal to sell.

## Strategy Logic

This strategy calculates the 3-period and 50-period simple moving averages. When the 3-day SMA crosses above the 50-day SMA, it indicates the short-term trend has turned bullish and a buy signal is generated. When the 3-day SMA crosses below the 50-day SMA, it indicates the short-term trend has turned bearish and a sell signal is generated. To reduce unnecessary trading, a 40-day median SMA is also added. If the 3-day SMA crosses below the 40-day SMA, a sell signal is also triggered for a quick stop loss.

The key to this strategy is using moving averages of different periods to divide market fluctuations into different stages. The 3-day SMA represents the shortest-term trend, the 50-day SMA represents the medium-term trend, and their crossover represents the conversion of short-term and medium-term trends, which can capture price changes across different time horizons. Through this multi-timeframe analysis, it can judge turning points in the market quite accurately.

## Advantage Analysis 

- Clear momentum crossover and explicit signals. Crossover of different period SMAs can effectively determine changes in short-term and medium-term trends, avoiding interference from minor market fluctuations.

- Quick stop loss by SMA3 crossing below SMA40 reduces losses and controls risks.

- Simple and clear strategy logic, easy to implement. Indicators and signal rules are directly actionable.

- Flexibility to adjust SMA parameters for different market conditions and trading instruments.

- Can incorporate other technical or fundamental indicators for combo validation to avoid false signals.

## Risk Analysis

- Frequent SMA crossover signals may lead to overtrading in sideways or non-trending markets, increasing costs.

- SMA has lagging nature, signals may come after price has already moved substantially from ideal levels.

- Fixed SMA parameters may not suit all market conditions, optimization needed.

- Reliance on single indicator makes strategy vulnerable to failure.

## Improvement Directions

- Optimize SMA periods to find best parameter combinations.

- Add oscillators like stochastic, MACD to validate signals and avoid false signals. 

- Adjust position sizing and stop loss based on changing market conditions.

- Consider adding fundamental indicators like earnings, news.

- Use volume indicators, enter on high volume breakouts.

## Conclusion

The moving average crossover strategy judges changes in short-term and medium-term trends by crossing over different period SMAs, and takes trend following actions. It is a simple and direct trend following strategy. The advantages are its clear logic and ease of implementation. Performance can be enhanced through parameter optimization and combo validation. However, SMAs themselves have lagging nature and cannot precisely catch turns. It is recommended to combine with leading indicators and use for trend following in major trends.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-10 00:00:00
end: 2023-10-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Geduldtrader

//@version=4
strategy("MA Crossover", overlay = true)

start = timestamp(2009,2,1,0,0)

sma50 = sma(close, 50)
sma40 = sma(close, 40)
sma3 =  sma(close, 3)

plot(sma50,title='50', color=#00ffaa, linewidth=2)
plot(sma3,title='3', color=#2196F3, linewidth=2)

long = crossover(sma3,sma50)
neut = crossunder(close,sma50)
short = crossunder(sma3,sma40)

if time >= start
    strategy.entry("Long", strategy.long, 10.0, when=long)


strategy.close("Long", when = short)
strategy.close("Long", when = neut)


plot(close)
```

> Detail

https://www.fmz.com/strategy/429470

> Last Modified

2023-10-17 14:27:10
