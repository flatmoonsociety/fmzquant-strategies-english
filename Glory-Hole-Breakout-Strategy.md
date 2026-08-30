
> Name

Glory-Hole-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d2455a6f68e876331f5fde40e1ec2849004a094f8a67eca148e44f6d264520a5.png)

[trans]

## Overview
The halo breakout strategy is a trend following strategy that combines the moving average and ADX indicators to determine price movement and trend strength, entering the market when the moving average is broken. This strategy is simple and practical, can effectively track trends, and has great profit potential.
## Strategy Principle
This strategy is mainly based on three indicators:
1. SMA moving average: Calculate the simple moving average of the closing price of a certain period to determine the direction of the price trend.
2. ADX average trend index: measures the strength of the trend. The higher the ADX, the more obvious the trend.
3. Halo condition: When the closing price is higher than the opening price and the closing price is close to the lowest price, it is a bullish halo. When the closing price is lower than the opening price and the closing price is close to the highest price, it is a bearish halo.
Strategy logic:
1. Calculate the SMA value of N periods and determine the overall price trend.
2. Calculate the ADX value of M period and judge the trend strength. A trading signal is generated only when ADX is above the set threshold.
3. When the price forms a bullish aura, closes above the SMA, and ADX is above the threshold, go long.
4. When the price forms a bearish aura and closes below the SMA and ADX is above the threshold, go short.
5. Exit the position with stop loss or take profit.
## Strategic Advantages
1. Combined with trend direction and strength indicators, it can effectively track trends.
2. The halo condition filters out most invalid breakthroughs and improves the winning rate of entries.
3. Using SMA instead of EMA is helpful to grasp the medium and long-term trend.
4. The ADX indicator avoids trading when there is no obvious trend and is conducive to grasping high-probability operations.
5. The policy rules are simple, clear and easy to implement.
## Strategy Risk
1. SMA is a lagging indicator, and stops may be triggered due to early entry or late entry. SMA cycle parameters can be appropriately optimized.
2. The function of ADX is to filter out the volatile market, but it may misjudge and cause losses when the trend reverses. Can reduce the risk of ADX conditions forming.
3. Although the halo can filter out false breakthroughs, in actual operations, you still need to pay attention to risk management and appropriately adjust the stop loss position.
4. The strategy does not consider long-short balance factors and requires manual intervention or logic optimization.
## Strategy optimization direction
1. Optimize the parameters of SMA and ADX and find the best parameter combination.
2. Add other indicators to judge trends, such as Bollinger Bands, KDJ, etc., to improve the quality of entries.
3. Add closing conditions, such as trend reversal, retracement ratio, etc., to improve the exit logic.
4. Increase the judgment of the long-short ratio and avoid excessive unilateral trading.
5. Optimize the stop loss strategy and improve the fixed stop loss to trailing stop loss or batch stop loss.
6. Optimize fund management strategies and better control single risk.
## Summarize
The halo breakout strategy integrates the moving average and ADX indicators to determine the direction and strength of the trend, and generates trading signals under the filtering of halo conditions. It is a simple and practical trend following strategy. This strategy has the advantage of grasping trends and filtering noise, but it also has problems such as delayed trend judgment and stop loss risks. We can further improve the efficiency and stability of the strategy by optimizing parameters, improving enter and exit logic, and improving risk management.

|| 


## Overview

The Glory Hole breakout strategy is a trend following strategy that combines moving average and ADX indicators to determine price trend and strength, and enters the market when price breaks through the moving average. This simple and practical strategy can effectively track trends and has high profit potential.

## Strategy Logic

The strategy is mainly based on three indicators:

1. SMA: Simple moving average to determine price trend direction. 

2. ADX: Average directional movement index to measure trend strength. Higher ADX indicates stronger trend.

3. Glory Hole Condition: Bullish when close > open and close near low. Bearish when close < open and close near high.

The trading logic is:

1. Calculate N-period SMA to determine overall trend.

2. Calculate M-period ADX to determine trend strength. Trade only if ADX is above threshold.

3. Go long when bullish glory hole forms, close > SMA and ADX > threshold. 

4. Go short when bearish glory hole forms, close < SMA and ADX > threshold.

5. Exit with stop loss or take profit.

## Advantages

1. Combines trend direction and strength for effective trend following.

2. Glory hole filters out false breakouts and improves entry quality.

3. SMA captures mid to long term trends better than EMA. 

4. ADX avoids trading in no-trend zones, ensuring high probability setups.

5. Simple and clear rules easy to implement.

## Risks

1. SMA lag may cause premature or delayed entries leading to stopped out trades. Optimize SMA Period.

2. ADX may wrongly judge trend reversal as no-trend zone. Lower ADX threshold to manage risk.

3. Despite glory hole, tight risk management needed for real trades. Adjust stop loss properly. 

4. Lack of long/short balance logic. Manual intervention or optimization needed.


## Enhancement Opportunities 

1. Optimize SMA and ADX parameters to find best combination.

2. Add other trend indicators like Bollinger or KDJ to improve entry quality.

3. Add exit logic like trend reversal or drawdown percentage to refine exits.

4. Add long/short ratio judgement to avoid excessive one-sided trades.

5. Optimize stop loss from fixed to trailing or staggered.

6. Optimize risk management for better single trade risk control.

## Summary

The Glory Hole strategy integrates SMA and ADX to determine trend direction and strength. It generates signals on glory hole condition to effectively track trends. The strategy has the advantage of capturing trends and filtering noise, but also lagging trend determination and stop loss risks. Further improvements in parameter optimization, enter/exit logic, and risk management will enhance its efficiency and stability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|SMA|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|30|ADX Tradelevel|
|v_input_4|14|ADX Smoothing|
|v_input_5|14|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-18 00:00:00
end: 2023-10-24 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Glory Hole with SMA + ADX", overlay=true)
len = input(20, minval=1, title="SMA")
src = input(close, title="Source")
ADXlevel = input(30, minval=1, title="ADX Tradelevel")
out = sma(src, len)

//adx
adxlen = input(14, title="ADX Smoothing")
dilen = input(14, title="DI Length")
dirmov(len) =>
	up = change(high)
	down = -change(low)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(up > down and up > 0 ? up : 0, len) / truerange)
	minus = fixnan(100 * rma(down > up and down > 0 ? down : 0, len) / truerange)
	[plus, minus]

adx(dilen, adxlen) => 
	[plus, minus] = dirmov(dilen)
	sum = plus + minus
	adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)

sig = adx(dilen, adxlen)

plot(out, title="SMA", color=blue)

bullish = ((out<close) and (out<open) and (out>low) and (sig>ADXlevel))
bearish = ((out>close) and (out>open) and (out<high) and (sig>ADXlevel))


if (bullish)
    strategy.entry("Buy", strategy.long)

if (bearish)
    strategy.entry("Sell", strategy.short)
```

> Detail

https://www.fmz.com/strategy/430124

> Last Modified

2023-10-25 11:35:36
