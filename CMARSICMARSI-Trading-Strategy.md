
> Name

CMARSI Trading StrategyCMARSI-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The CMARSI trading strategy is a trend following strategy that combines the RSI indicator and moving averages. It uses the improved RSI indicator to identify trends and uses the moving average as a signal to determine entry and exit. This strategy is suitable for medium and long-term trading, and can achieve better profits by following the trend.
## Principle analysis
The CMARSI strategy uses a modified RSI indicator called Connors RSI. Connors RSI combines three indicators: classic RSI, RSI long and short moving average, and price rate of change (ROC). Its calculation formula is:
Connors RSI = (RSI + RSI long and short moving average + ROC percentile) / 3
Among them, the RSI uses a 3-day calculation period, the RSI long and short moving average uses a 2-day calculation period, and the ROC percentile uses a 100-day calculation period.
The advantage of Connors RSI is that it can more accurately identify changes in trends by combining multiple indicators. When the Connors RSI crosses above the 40 boundary, it is a bullish signal, and when it crosses below the 70 boundary, it is a bearish signal.
The CMARSI strategy is based on Connors RSI and introduces an additional moving average factor. This strategy calculates the 2-day moving average and uses the golden cross between the Connors RSI and the moving average as a trading signal. The specific trading rules are:
1. When the Connors RSI crosses the 40 boundary and golden crosses the 2-day moving average, enter the market long.
2. When the Connors RSI falls below the 70 boundary and crosses the 2-day moving average, close the position and exit.
By using moving average filtering, some false signals appearing in Connors RSI can be avoided, thereby improving the stability of the strategy.
## Advantage Analysis
The biggest advantage of the CMARSI strategy is to integrate multiple indicators to identify trends and avoid the limitations of a single RSI indicator. Specifically, this strategy has the following advantages:
1. Connors RSI indicator is more stable than the classic RSI indicator and can accurately identify trend turning points.
2. The introduction of moving averages effectively filters out some noise and avoids chasing highs and selling lows.
3. A combination of multiple indicators can increase the winning rate and make profits by following the trend.
4. The trading rules are simple, clear and easy to implement.
5. As a trend following strategy, it can fully capture the profits of medium and long-term trends.
## Risk Analysis
The main risks of the CMARSI strategy come from incorrect trend judgment and stop loss position setting. Specific risks include:
1. The Connors RSI indicator sends wrong signals, leading to unnecessary entries. Parameters can be adjusted appropriately, or confirmation of the autres indicator can be added.
2. The stop loss position is set unreasonably, and the stop loss may be stopped too early or the stop loss range may be too large. Stop loss positions should be optimized for different varieties and market environments.
3. Under volatile market conditions, the moving average filtering effect may be poor, and the strategy parameters should be optimized.
4. Long-term operation may lead to over-optimization, so you should backtest regularly and adjust parameters according to the market environment.
## Optimization direction
The CMARSI strategy can be optimized from the following aspects:
1. Optimize the parameters of Connors RSI to adapt to different cycles and varieties.
2. Try different types of moving averages to further improve the filtering effect.
3. Add other indicators, such as MACD, Bollinger Bands, etc. to confirm trading signals.
4. Optimize the stop loss strategy and set a reasonable trailing stop loss or step stop loss.
5. Filter trading varieties to make the strategy more suitable for specific varieties.
6. Use the Walk Forward Analysis method to regularly optimize parameters to avoid over-optimization.
## Summarize
The CMARSI strategy comprehensively uses Connors RSI and moving average indicators to conduct medium and long-term trading by following the trend. This strategy is stable, easy to implement, and can effectively track trends and make profits. We should continuously optimize the strategy parameters according to the market environment and conduct risk management, and then we can obtain better profit returns. Overall, CMARSI is a recommended trend trading strategy.
||


## Overview

The CMARSI trading strategy is a trend-following strategy that combines the RSI indicator and moving averages. It uses an improved RSI indicator to identify trends and moving averages as signals for entries and exits. This strategy is suitable for medium-to-long term trading and aims to profit by following the trend. 

## Principle Analysis

The CMARSI strategy uses an enhanced RSI indicator called Connors RSI. Connors RSI incorporates three indicators - classical RSI, RSI Up/Down lines, and ROC percentile. Its calculation formula is:

Connors RSI = (RSI + RSI Up/Down + ROC Percentile) / 3

Where RSI uses a 3-day period, RSI Up/Down uses 2 days, and ROC percentile uses 100 days. 

The advantage of Connors RSI is that it combines multiple indicators and can more accurately identify trend changes. A crossing above 40 is a long signal, while a crossing below 70 is a short signal.

The CMARSI strategy further introduces a moving average factor on top of Connors RSI. It calculates a 2-day moving average and uses crossovers of Connors RSI and the MA as trading signals. The specific rules are:

1. Enter long when Connors RSI crosses above 40 and has a golden cross of 2-day MA. 

2. Exit when Connors RSI crosses below 70 and has a death cross of 2-day MA.

Using the MA filter can avoid some false signals from Connors RSI and improve the stability of the strategy.

## Advantage Analysis 

The biggest advantage of the CMARSI strategy is the combination of multiple indicators to identify trends, avoiding the limitations of single RSI indicators. Specifically, the strategy has the following advantages:

1. Connors RSI is more stable than classical RSI for identifying trend turning points.

2. The introduction of moving averages effectively filters out some noise and prevents chasing highs and selling lows. 

3. The combination of multiple indicators can improve win rate by following trends.

4. The trading rules are simple and easy to implement. 

5. As a trend-following strategy, it can fully capture profits from medium-to-long term trends.

## Risk Analysis

The main risks of the CMARSI strategy come from incorrect trend judgement and stop loss placement. The specific risks are:

1. Connors RSI gives incorrect signals, causing unnecessary entries. Parameters can be adjusted or other indicators added for confirmation.

2. Stop loss placement is unreasonable, which may cause premature stop out or too large of a stop loss. Stop loss should be optimized for different products and market environments.

3. Moving average filters may not work well in ranging markets. Strategy parameters should be optimized accordingly. 

4. Prolonged use may lead to overfitting. Regular backtesting and parameter tuning based on market conditions are necessary.

## Optimization Directions 

The CMARSI strategy can be optimized in the following aspects:

1. Optimize Connors RSI parameters for different periods and products. 

2. Try different types of moving averages to further improve the filtering effect.

3. Add other indicators like MACD, Bollinger Bands for trade confirmation. 

4. Optimize stop loss strategies, such as trailing stop loss or staggered stop loss.

5. Select products that fit the strategy better through screening.

6. Use Walk Forward Analysis to regularly optimize parameters and prevent overfitting.

## Conclusion

The CMARSI strategy combines Connors RSI and moving averages to follow trends for medium-to-long term trading. It is stable, easy to implement, and can effectively capture trend profits. We should continuously optimize parameters based on market conditions, manage risks, and generate good profitability. Overall, CMARSI is a recommended trend trading strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-19 00:00:00
end: 2023-09-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
src = close, lenrsi = 3, lenupdown = 2, lenroc = 100, malengt = 2, low = 40, high = 70, a = 1
updown(s) => 
    isEqual = s == s[1]
    isGrowing = s > s[1]
    ud = 0.0
    ud := isEqual ? 0 : isGrowing ? (nz(ud[1]) <= 0 ? 1 : nz(ud[1])+1) : (nz(ud[1]) >= 0 ? -1 : nz(ud[1])-1)
    ud
rsi = rsi(src, lenrsi)
updownrsi = rsi(updown(src), lenupdown)
percentrank = percentrank(roc(src, 1), lenroc)
crsi = avg(rsi, updownrsi, percentrank)
MA = sma(crsi, malengt)

band1 = 70
band0 = 40

ColorMA = MA>=band0 ? lime : red

p1 = plot(MA, title="BuyNiggers", style=line, linewidth=4, color=ColorMA)

p2 = plot(low, title="idk", style=line, linewidth=2, color=blue)
p3 = plot(high, title="idk2", style=line, linewidth=2, color=orange)

//@version=2
strategy("CMARSI")


if crossover(MA,band0)
    strategy.entry("buy", strategy.long, when=strategy.position_size <= 0)
    
if crossunder(MA,band1)
    strategy.exit("sell", "buy", profit=1000000, stop=10000000)
    
plot(strategy.equity)

    




```

> Detail

https://www.fmz.com/strategy/427929

> Last Modified

2023-09-26 20:44:53
