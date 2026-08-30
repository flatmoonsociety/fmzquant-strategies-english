
> Name

Long-term-Moving-Average-Crossover-Renko-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f4f21605eea35bc420f9a7e5bf8faea8272ae7fbc5af28dc4490e75fee47b774.png)
 [trans]
### Overview
This strategy is a moving average crossover strategy based on Renko candlesticks. It uses the TEMA indicator to construct crossover signals, combined with long-term moving averages for filtering, and is designed to identify trends on Renko candlesticks and issue buy and sell signals.
### Strategy Principles
The main signal source of this strategy is the golden cross of the short-term TEMA indicator and the SMA indicator. The specific logic is:
When the short-term TEMA goes above the short-term SMA, go long; when the short-term TEMA goes below the short-term SMA, close the position.
In addition, the strategy also sets two optional parameters avg_protection and gain_protection, which are used to adjust entry and stop loss logic:
- When avg_protection>0, the purchase will only be made when the close price is lower than the current average price of the position, which can reduce the cost of holding the position;
- When gain_protection>0, the profit will be taken only when the close price exceeds a certain percentage of the entry price, thereby locking in profits.
Finally, the strategy also uses a long-term SMMA indicator as a trend filter. Only when the close price is lower than the SMMA, a long signal will be issued.
### Advantage Analysis
This strategy mainly has the following advantages:
1. Based on Renko candle chart, it can effectively filter noise and identify trends;
2. Use TEMA indicator to construct signals with high sensitivity and good followability;
3. Rich in adjustable parameters, you can control the entry strategy;
4. Combined with long and short-term moving averages, opportunities can be captured in trends.
### Risk Analysis
There are also some risks with this strategy:
1. Renko’s own timeline is uneven and the interval cannot be controlled;
2. TEMA has high sensitivity and is more likely to produce false signals;
3. Improper parameter settings may lead to leakage.
These risks can be avoided by appropriately adjusting parameters and setting stop loss positions.
### Optimization direction
This strategy can mainly be optimized from the following aspects:
1. Test different parameter combinations and find optimal parameters;
2. Add stop loss strategies, such as trailing stop loss, range stop loss, etc., to reduce DD;
3. Combine with other indicators for signal filtering to reduce false signals;
4. Test the parameter effects of different varieties.
### Summarize
Overall, this strategy is a simple but highly practical moving average crossover strategy. It mainly relies on the excellent denoising effect of the Renko K line and the high sensitivity of the TEMA indicator to generate signals. At the same time, the cooperation of long-term and short-term moving averages also strengthens its trend following ability. Through parameter adjustment and appropriate optimization, this strategy can become an effective choice for quantitative trading.
||

### Overview

This strategy is a moving average crossover strategy based on Renko candlestick charts. It uses the TEMA indicator to construct crossover signals and combines long-term moving averages for filtering, aiming to identify trends on Renko charts and generate buy and sell signals.

### Strategy Logic

The main signal source of this strategy comes from the golden cross and death cross of the short-term TEMA indicator and SMA indicator. Specifically, the logic is:

When the short-term TEMA crosses over the short-term SMA, go long; when the short-term TEMA crosses below the short-term SMA, close positions.

In addition, the strategy also sets two optional parameters avg_protection and gain_protection to adjust the entry and stop loss logic:

- When avg_protection>0, only buy when the close price is lower than the current average holding price, which can reduce the cost basis;

- When gain_protection>0, only sell when the close price exceeds the entry price by a certain percentage to lock in profits.

Finally, the strategy also uses a long-term SMMA indicator as a trend filter. Only when the close price is below SMMA will a long signal be triggered.

### Advantage Analysis 

The main advantages of this strategy are:

1. Based on Renko candlestick charts, it can effectively filter out noise and identify trends;
2. Use the TEMA indicator to construct signals with high sensitivity and tracking ability;
3. The adjustable parameters are rich to control the entry strategy;
4. The combination of long-term and short-term moving averages can capture opportunities in trends.

### Risk Analysis

This strategy also has some risks:
 
1. Renko itself has an uneven timeline that cannot control interval times;
2. The high sensitivity of TEMA also leads to more false signals;
3. Improper parameter settings may lead to missing trades.

To mitigate these risks, proper parameter tuning, setting stop losses etc. can be adopted.

### Optimization Directions

The main optimization directions for this strategy are:

1. Test different parameter combinations to find the optimal parameters;
2. Add stop loss strategies such as trailing stop loss, range stop loss, etc. to reduce DD;
3. Combine other indicators for signal filtering to reduce false signals; 
4. Test parameter effectiveness across different products.

### Conclusion

In general, this is a basic, simple but highly practical moving average crossover strategy. It mainly relies on the excellent noise reduction effect of Renko bars and the high sensitivity of the TEMA indicator to generate signals. Meanwhile, the collaboration between long-term and short-term moving averages also enhances its trend following capability. With parameter tuning and proper optimization, this strategy can become an effective choice for quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|temaLength|
|v_input_2|3|smaLength|
|v_input_3|30|smmaLength|
|v_input_4|2|minGainPercent|
|v_input_5|true|avg_protection|
|v_input_6|true|gain_protection|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-17 00:00:00
end: 2024-01-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("TEMA Cross", overlay = true)

tema(src, len) =>
    3*ema(src, len) - 3*ema(ema(src, len), len) + ema(ema(ema(src, len),len),len)

smma(src, len) =>
    sa = 0.0
    sa := na(sa[1]) ? sma(src, len) : (sa[1] * (len - 1) + src) / len
    sa

temaLength = input(5)
smaLength = input(3)
smmaLength = input(30)
tema1 = tema(close, temaLength)
sma1 = sma(tema1, smaLength)
smma1 = smma(close,smmaLength)


plot(tema1, color = green, title = "TEMA")
plot(sma1, color = orange, title = "SMA")
plot(smma1, color = red, title = "SMMA")
minGainPercent = input(2)
gainMultiplier = minGainPercent * 0.01 + 1

avg_protection = input(1)
gain_protection = input(1)

longCondition = crossover(tema1, sma1) and tema1 < smma1
shortCondition = crossunder(tema1, sma1)

strategy.entry("Buy", strategy.long, when = longCondition and (avg_protection >= 1 ? (na(strategy.position_avg_price) ? true : close <= strategy.position_avg_price) : true))
strategy.close_all(when = shortCondition and (gain_protection >=1 ? (close >= gainMultiplier * strategy.position_avg_price) : true))
```

> Detail

https://www.fmz.com/strategy/439823

> Last Modified

2024-01-24 10:55:57
