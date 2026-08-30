
> Name

Dual-Moving-Average-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/25d7d6be6734f1806e72fedd854107632c3e8ea6c9e2547190ab9d12de8255fe.png)
[trans]
## Overview
The core idea of ​​this strategy is to use the golden cross of the fast moving average and the slow moving average to judge the market trend and achieve low-risk transactions. When the fast moving average crosses the slow moving average, it means that the market may enter an upward trend, so go long; when the fast moving average crosses below the slow moving average, it means that the market may enter a downward trend, then go short.
## Strategy Principle
This strategy uses an exponential moving average of price. The moving average is a trend analysis indicator that smoothes price data to determine price movements. The fast moving average has smaller parameters and can respond to price changes more quickly; the slow moving average has larger parameters and can respond more slowly to price changes. When the fast moving average crosses the slow moving average, it means that the market may enter a long market, and a long position should be established; when the fast moving average crosses below the slow moving average, it means that the market may enter a short market, and a short position should be established.
Specifically, two exponential moving averages are defined in this strategy, the fast moving average period is 21, and the slow moving average period is 55. The strategy determines entry and exit by judging the golden cross of the two moving averages. When the fast moving average crosses the slow moving average, go long; when the fast moving average crosses below the slow moving average, go short.
In addition, this strategy also uses ATR, a volatility indicator, to set stop loss and take profit. ATR can effectively assess the degree of market volatility. The stop loss is set when the price is 1.5 times away from ATR; the take profit is set when the price is close to 1 times away from ATR.
## Advantage Analysis
This strategy has the following advantages:
1. The ideas are clear and easy to understand and implement.
2. Use moving average indicators to determine price trends and achieve low-risk transactions.
3. The combination of fast moving average and slow moving average can effectively filter market noise and identify price trends.
4. Use the ATR indicator to dynamically set stop loss and take profit, and adjust positions according to the degree of market fluctuations.
5. There is no need to adjust parameters frequently, and the strategy has high stability.
## Risk Analysis
This strategy also has certain risks:
1. When prices fluctuate violently, the moving average can easily send out wrong signals, which may lead to unnecessary losses.
2. This strategy is only based on technical indicators and does not take into account fundamental factors. It may cause large losses in the face of major bad news.
3. The stop loss and take profit set by the ATR indicator may not be suitable for all market environments and may be too loose or too tight.
4. The setting of the moving average period is not the only optimal solution. Different combinations of period parameters will produce different effects.
In view of the above risks, we can optimize from the following aspects:
1. Combine with other indicators such as MACD, RSI, etc. to confirm trading signals and avoid wrong entries.
2. Appropriately reduce the stop loss range to reduce single loss.
3. Dynamically optimize the moving average cycle parameters to make them more suitable for the market environment at different stages.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Use machine learning methods to automatically optimize moving average parameters to make the strategy more adaptive.
2. Add fundamental factors as filtering conditions to avoid blindly going long or short when important bad news arrives. For example, the Federal Reserve interest rate decision, the release of important macro data, etc.
3. Set the upper and lower limits of volatility. When the ATR is too large or too small, suspend trading to avoid losses in extreme market environments.
4. Combined with stock fundamental indicators, such as PE price-earnings ratio, trading volume amplification effect, etc., set dynamic stop-loss and stop-profit ranges.
5. Increase the position management mechanism. When the profit rate reaches a certain level, the position will be gradually reduced; when a large loss occurs, trading will be suspended for a period of time, etc.
## Summarize
The overall operation idea of ​​this strategy is clear and simple. It judges the market trend through the intersection of double moving averages. It is a typical trend following strategy. At the same time, the strategy also controls risks well, using the ATR indicator to dynamically set stop-loss and take-profit levels. Through further optimization, the strategy can be improved in terms of drawdown control and trend trading, thereby achieving more stable investment performance.
||

## Overview

The core idea of this strategy is to use the golden cross and death cross of the fast and slow moving average lines to judge the trend of the market and implement low-risk trading. When the fast moving average line crosses above the slow moving average line, it indicates that the market may be entering an uptrend, so go long; when the fast moving average line crosses below the slow moving average line, it indicates that the market may be entering a downtrend, so go short.

## Strategy Principle  

This strategy uses the exponential moving average of prices. The moving average is a trend analysis indicator that smooths price data to judge price trends. The fast moving average has a smaller parameter and can respond to price changes faster; the slow moving average has a larger parameter and responds to price changes more slowly. When the fast moving average crosses above the slow moving average, it indicates that the market may be entering a bull market, and a long position should be established; when the fast moving average crosses below the slow moving average, it indicates that the market may be entering a bear market, and a short position should be established.

Specifically, this strategy defines two exponential moving averages, with periods of 21 and 55 for the fast and slow moving average respectively. The strategy determines entry and exit based on the golden cross and death cross of the two moving average lines. Go long when the fast moving average crosses above the slow moving average, and go short when the fast moving average crosses below the slow moving average.  

In addition, this strategy also uses the ATR volatility indicator to set stop loss and take profit. ATR can effectively assess the degree of market volatility. The stop loss is set at 1.5 times ATR distance from the price; the take profit is set close to 1 times ATR distance from the price.

## Advantage Analysis

This strategy has the following advantages:

1. The idea is clear and easy to understand and implement.  
2. Use the moving average indicator to determine the price trend and implement low-risk trading.
3. The combination of fast and slow moving averages can effectively filter market noise and identify price trends.  
4. Use the ATR indicator to dynamically set stop loss and take profit based on the degree of market volatility.
5. No frequent parameter adjustment is required and the strategy is highly stable.

## Risk Analysis  

This strategy also has some risks:  

1. When prices fluctuate violently, the moving average may give wrong signals, which may lead to unnecessary losses.
2. This strategy is based solely on technical indicators without considering fundamentals, and may suffer greater losses in the face of major negative news.
3. The stop loss and take profit set by the ATR indicator may not suit all market environments, which may be too loose or too tight.
4. The setting of moving average periods is not the only optimal scheme, and different combinations of period parameters will produce different effects.

To address the above risks, we can optimize from the following aspects:

1. Combine other indicators such as MACD and RSI to confirm trading signals and avoid wrong entry.  
2. Slightly narrow the stop loss range to reduce per trade loss.
3. Dynamically optimize moving average period parameters to adapt them better to different market stages.

## Optimization Directions   

This strategy can be further optimized in the following aspects:

1. Use machine learning methods to automatically optimize moving average parameters for better adaptability.  

2. Add fundamentals as filtering conditions to avoid going long or short blindly when major negative news arrives, such as Fed rate decisions and important macro data releases.

3. Set upper and lower limits for volatility, pause trading when ATR gets too high or too low to avoid losses in extreme market environments.  

4. Incorporate stock fundamentals like P/E ratio and trading volume expansion to set dynamic stop loss and take profit ranges.

5. Add position sizing mechanisms, gradually reducing positions when profit ratio reaches a level, suspending trading for a period when suffering relatively large losses, etc.

## Conclusion  

The overall logic of this strategy is clear and simple, using dual moving average crossovers to determine market trends, a typical trend following strategy. Meanwhile, the strategy also controls risks very well by using the ATR indicator to dynamically set stop loss and take profit. With further optimization, the strategy can be enhanced in terms of drawdown control and trend riding, thus leading to more steady investment performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|ATR Length|
|v_input_2|1.5|SL|
|v_input_3|true|TP1|
|v_input_4|21|fastInput|
|v_input_5|55|slowInput|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="No-Nonsense Strategy Template [WM]", overlay = true)

price = close

//
// ATR stuff
//

atrLength = input(14, "ATR Length")
slMultiplier = input(1.5, "SL")
tpMultiplier = input(1, "TP1")

atr = atr(atrLength)

//
// Strategy under test. MA crossover
// 

fastInput = input(21)
slowInput = input(55)

fast = ema(price, fastInput)
slow = ema(price, slowInput)

plot(fast, color = red)
plot(slow, color = blue)

goLong = crossover(fast, slow)
goShort = crossunder(fast, slow)

if (goLong)
    sl = price - atr * slMultiplier
    tp = price + atr * tpMultiplier
    strategy.entry("Long", strategy.long)
    strategy.exit("Long Exit", "Long", stop = sl, limit = tp)
    
if (goShort)
    sl = price + atr * slMultiplier
    tp = price - atr * tpMultiplier
    strategy.entry("Short", strategy.short)	 
    strategy.exit("Short Exit", "Short", stop = sl, limit = tp)


```

> Detail

https://www.fmz.com/strategy/439877

> Last Modified

2024-01-24 15:24:13
