
> Name

Eight-Day-Extended-Run-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f84799697d3ba9f989.png)
 [trans]

### Overview
This strategy is inspired by Linda Bradford Raschke and is specifically designed for U.S. Treasury futures (ZN1!). It captures longer-term price trends by tracking the 5-day simple moving average and looking for whether the price can continue to run for more than 8 days after breaking through the average.
### Strategy Principles
The core indicator of this strategy is the 5-day simple moving average (SMA). Linda has proven through extensive testing and research that this indicator is very effective in identifying trends. She found that about 9-10 times a year in each market, prices will have very large abnormal breakthroughs in the direction of the trend. If the trend can continue, these breakthroughs will often trigger a long-term price movement. This is why this strategy uses the 5-day SMA as the core indicator.
Specifically, the strategy logic is as follows:
1. Use the 5-day SMA to determine the price trend direction. When the price is above the 5-day SMA, it is judged to be an uptrend; when the price is below the 5-day SMA, it is judged to be a downtrend.
2. Check whether the price can continue to run for more than 8 days after breaking above the 5-day SMA. If it is an upward trend but the price breaks through the SMA and moves downward for more than 8 days (TriggerBuy variable), then at the end of the first downward period (the price turns upward again), enter the market long (Buy variable). If it is a downward trend but the price breaks through the SMA and moves upward for more than 8 days (TriggerSell variable), then at the end of the first rising period (the price turns downward again), enter the market short (Sell variable).
3. Hold the position for 10 days after entering the market.
Through this design, the strategy attempts to capture longer-term price trends and achieve excess returns.
### Advantage Analysis
This strategy has the following advantages:
1. The proven and effective 5-day SMA indicator is used to determine the trend, which provides a solid theoretical basis for price breakthrough judgment and operation signals.
2. Use the abnormal phenomenon of continuous price breakthroughs in the trend direction to design trading logic. Such breakthroughs often herald a longer price movement. Capturing these runs can lead to high-probability profit opportunities.
3. The entry signal is relatively clear and is a pullback at the end of the first downward/rising price period, which can effectively filter out some false breakthroughs.
4. The holding time of 10 days is longer, which is also conducive to capturing longer price runs.
### Risk Analysis
This strategy also has some risks:
1. The 5-day SMA has a certain lag and may misjudge the price trend. This can lead to incorrect long or short decisions.
2. Even if the price runs for more than 8 days, it may be a false breakout. If the trend reverses soon, you will face the risk of losing money.
3. The 10-day holding period is too long, and the loss may be relatively large.
Countermeasures:
1. You can test and add other indicators to assist in judging trends, such as MACD, etc., to improve the accuracy of judgment.
2. Parameters can be adjusted according to the specific market, such as adjusting the number of days the price runs to 6-7 days.
3. You can experimentally set a trailing stop to control the maximum loss.
### Optimization direction
This strategy can also be optimized from the following aspects:
1. Test and add other indicators to assist in judging trends. For example, MACD, KDJ, etc. This can improve the accuracy of trend judgment.
2. Optimize parameters, such as the minimum number of days for price movement, the number of days of holding positions after entry, etc., to find the optimal parameter combination.
3. Try to set a trailing stop after entering the market to control risks and optimize the stop loss range. This can ensure that you capture the general trend while controlling single losses.
4. Test whether to proactively profit by setting a price target after entering the trade. This can lock in some profits.
5. You can consider closing the strategy in volatile market conditions to avoid being trapped. The implementation method can be to set volatility conditions or market indicator conditions to control the opening of the strategy.

### Summarize
This strategy was inspired by the famous trader Linda Raschke. It judges the price trend by tracking the 5-day SMA indicator, and designs a trading logic based on abnormal price movements to capture the general trend. The strategy has the advantages of solid indicators and theoretical foundation, clear signal generation, and long position time, which is conducive to capturing longer-term price movements. At the same time, there are also certain lag risks and position risks. In the future, optimization testing can be carried out from many aspects to improve the profit factor of the strategy.
||


### Overview

This strategy is inspired by Linda Bradford Raschke and specially designed for the US T-Note futures (ZN1!). It tracks the 5-day simple moving average (SMA) to find price moves that can sustain above or below the average for over 8 days, in order to capture longer-term price trends.  

### Strategy Logic   

The core indicator of this strategy is the 5-day SMA. Through extensive testing and research, Linda proves this indicator to be very effective for trend identification. She finds that in each market, prices tend to have around 9-10 exceptionally large outlier moves per year in the direction of the trend. If the trend persists, these outliers often lead to extended price runs. That's why the 5-day SMA is chosen as the core indicator.

Specifically, the strategy logic is designed as follows:  

1. Use the 5-day SMA to determine the price trend direction. When price is above 5-day SMA, the trend is up. When price is below 5-day SMA, the trend is down.

2. Detect if price can sustain above/below the 5-day SMA for over 8 days after breaking through it. If it's an upward trend but price breaks below the SMA and runs for over 8 days (TriggerBuy variable), go long when price turns back up after the first pullback (Buy variable). If it's a downward trend but price breaks above the SMA and runs for over 8 days (TriggerSell variable), go short when price turns back down after the first pullback (Sell variable). 

3. Hold the position for 10 days after entering.

By doing so, the strategy aims to capture longer-term price trends and achieve excess returns.

### Advantage Analysis

The advantages of this strategy include:

1. It adopts the validated 5-day SMA indicator for trend identification, which provides solid theoretical ground for price breakout judgment and trade signals.

2. The trade logic is designed around the exceptional phenomenon of persistent price breakout against the trend direction. These outliers usually imply an extended price run afterwards. Capturing such runs presents high-probability profit opportunities.

3. Entry signals are clear cut, which is the pullback after the first declining/rising leg. This helps filter out some false breakouts. 

4. The 10-day holding period is comparatively long, which also facilitates capturing longer price runs.

### Risk Analysis   

There are also some risks associated with this strategy:

1. The 5-day SMA has some lagging effect, which may result in incorrect trend judgments, causing wrong long/short decisions.

2. Even if the price run sustains for over 8 days, it could still turn out to be a false breakout. If the trend quickly reverses, it poses the risk of losses.

3. The 10-day holding period is relatively long, leading to larger losses if stopped out.

Counter measures:

1. Test adding other indicators to help determine trends, e.g. MACD, to improve accuracy.

2. Adjust parameters based on specific markets, such as lowering the price run days to 6-7 days.  

3. Experiment with moving stop loss to control maximum losses.

### Optimization Directions   

The strategy can be further optimized in the following aspects:

1. Test adding other indicators to aid trend determination, e.g. MACD, KDJ etc. This can improve trend accuracy.

2. Optimize parameters like minimum price run days, holding days after entry etc, to find the optimal parameter combinations.

3. Try setting up moving stop loss after entry to control risks and optimize the stop loss percentage. This balances capturing big trends and limiting per trade losses.

4. Test setting up price targets after entry for actively taking profits. This allows locking in some profits along the way.  

5. Consider closing the strategy during high volatility regimes to avoid being caught in whipsaws. Can be achieved by setting volatility or market benchmark conditions to control strategy activation.


### Summary   

This strategy is inspired by famous trader Linda Raschke. It tracks the 5-day SMA indicator to determine price trends, and designs trade logic based on exceptional price runs to capture big trends. The advantages like solid indicator basis, clear signal generation, long holding periods etc make it suitable for catching longer-term price moves. Meanwhile, certain risks like lagging effect and holding risks do exist. Further optimizations can be done from multiple dimensions to improve the strategy's profit factor.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-18 00:00:00
end: 2023-12-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Marcuscor

//@version=4

// Inpsired by Linda Bradford Raschke: a strategy  for the T-note futures (ZN1!) that finds 8 day extended runs above/ below the 5sma and buys/ sells the first pullback below/ above the 5sma
// as of 01/10/2021 the t-test score is 4.06

strategy("8DayRun", overlay=true)


SMA = sma(close,5)

TrendUp = close > SMA

TrendDown = close < SMA

//logic to long

TriggerBuy = barssince(close < SMA) > 8

Buy = TriggerBuy[1] and TrendDown

strategy.entry("EL", strategy.long, when = Buy)
strategy.close(id = "EL", when = barssince(Buy) >10)

bgcolor(TriggerBuy ? color.red : na)
bgcolor(Buy ? color.blue : na)

// logic to short 

TriggerSell = barssince(close > SMA) > 8

Sell = TriggerSell[1] and TrendUp

strategy.entry("ES", strategy.short, when = Sell)
strategy.close(id = "ES", when = barssince(Sell) > 10)

bgcolor(TriggerSell ? color.white : na)
bgcolor(Sell ? color.fuchsia : na)




```

> Detail

https://www.fmz.com/strategy/435852

> Last Modified

2023-12-19 12:01:49
