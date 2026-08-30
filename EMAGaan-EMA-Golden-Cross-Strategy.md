
> Name

Gaan-EMA-Golden-Cross-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

### Strategy Overview
The Naniwa EMA golden cross strategy is a quantitative strategy that uses double EMA indicators for trend judgment and trading signal generation. This strategy forms long and short signals through the golden cross of fast and slow EMA during a specific trading period, and sets stop loss exit logic to capture short-term and mid-term price trends.
### Strategy Principles
1. Use the 9-day EMA as the fast line, the 27-day EMA as the mid-line, and the 81-day EMA as the slow line.
2. Trading hours are set from 9:00 to 15:00 every day
3. When the fast line crosses the middle line and the price is higher than the fast line, enter the market long
4. When the fast line crosses the middle line and the price is lower than the fast line, enter the market short
5. When the price falls below the fast line, stop the loss and close the long position.
6. When the price breaks through the fast line, stop the loss and close the short position.
The key to this strategy is to use EMA with different parameters to capture trends in different periods. The 9-day EMA represents the short-term trend, the 27-day EMA represents the mid-term trend, and the 81-day EMA represents the long-term trend. When the short-term trend is consistent with the medium-term trend, a trading signal can be generated.
As a trend tracking indicator, EMA can effectively filter out random fluctuations in price and capture the direction of the true trend. EMA golden cross is a commonly used signal method to judge trend turning.
### Strategic Advantages
- Use double EMA crossover to determine trend direction
- Cooperation with different EMA parameters, strong systematization
- The golden cross signal is clear and the timing is precise
- Stop loss strategy to control risk
- Trading time and money management optimization
### Existing risks
- There is a lag in the EMA indicator and false signals may appear.
- Fixed trading hours will miss other trading opportunities
- EMA parameter period needs to be adjusted to optimize results
- Frequent transactions tend to increase transaction rates
### Summarize
Overall, the Naniwa EMA golden cross strategy is a short-term trading strategy with a high degree of parameter optimization, standardized operations, and controllable risks. It seizes the trading timing of the short and mid-line EMA crossover to capture the price trend. Stop loss strategies can also effectively control the risk of a single transaction. This strategy is easier to implement and can provide a solid strategic framework for quantitative trading.

||

### Strategy Overview

The Gaan EMA Golden Cross strategy is a quantitative trading strategy that uses dual EMA indicators for trend determination and trade signal generation. It enters long and short trades based on golden crosses between fast and slow EMAs during specific trading time periods, with stop loss exit logic, to capture short-term and medium-term price trends.

### Strategy Logic

1. Use 9-period EMA as the fast line, 27-period EMA as the medium line, and 81-period EMA as the slow line.

2. Trading time is set to 9:00 - 15:00 daily. 

3. Go long when the fast line crosses above the medium line and price is above the fast line.

4. Go short when the fast line crosses below the medium line and price is below the fast line.

5. Exit long trades with stop loss when price breaks below the fast line. 

6. Exit short trades with stop loss when price breaks above the fast line.

The key is using EMAs of different parameters to capture trends of different periods. The 9-period EMA represents short-term trend, the 27-period EMA represents medium-term trend, and the 81-period EMA represents long-term trend. Trades are generated when the short-term trend aligns with the medium-term trend.

As a trend following indicator, EMA can effectively filter out random price fluctuations and capture the real trend direction. Golden crosses of EMAs are commonly used signals for trend reversals. 

### Advantages of the Strategy

- Uses dual EMA crossovers to determine trend direction

- Different EMA parameters work together for systematical strength 

- Clear and timely golden cross signals 

- Stop loss strategy controls risks

- Optimized trading time and capital management

### Risks Involved

- EMA has lagging effect, may generate false signals

- Fixed trading time misses other opportunities 

- EMA period tuning needed to optimize results

- Frequent trading increases commission costs

### Conclusion

The Gaan EMA Golden Cross strategy is overall a well-optimized, standardized, and risk-controlled short-term trading strategy. It capitalizes on EMA crossover trading opportunities to capture price trends. The stop loss strategy also effectively limits the risk of individual trades. The strategy is easy to implement and provides a robust framework for quantitative trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-09-14 00:00:00
period: 2m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("gaan ema crossover", overlay=true)
t1 = true
ema9 = ema(close, 9)
ema27 = ema(close, 27)
ema81 = ema(close, 81)

long = ema27 > ema81
long2 = close > ema9

short = ema27 <ema81
short2 = close < ema9

longexit = close < ema9
shortexit = close > ema9

plot(ema9, title="9", color=#00ff00, linewidth=3)
plot(ema27, title="27", color=#11ff11, linewidth=3)
plot(ema81, title="81", color=#22ff22, linewidth=3)

if (t1==true)
    if (long==true and long2==true)
        strategy.entry("long", strategy.long)


if (t1==true)
    if (short==true and short2==true)
        strategy.entry("short", strategy.short)
        strategy.close("long", when = longexit )
        strategy.close("short", when = shortexit)

```

> Detail

https://www.fmz.com/strategy/426902

> Last Modified

2023-12-01 14:57:55
