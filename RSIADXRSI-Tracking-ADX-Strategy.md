
> Name

RSI Tracking ADX Strategy RSI-Tracking-ADX-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The RSI tracking ADX strategy is a long-term trend tracking strategy that combines the RSI indicator and the ADX indicator. This strategy uses the RSI indicator to determine whether the market is overbought or oversold, combined with the ADX indicator to determine the strength of the current trend, and implements a long-term position strategy of entering a long position when the trend is upward and not overbought, and closing the position when the trend weakens or is overbought.
## Strategy Principle
This strategy mainly uses a combination of the RSI indicator and the ADX indicator to determine the timing of entry and exit.
Admission conditions:
1. The 20-day SMA rises;
2. ADX increased by more than 0.2 from the previous day, indicating that the trend is strengthening;
3. RSI is less than 85, avoid overbought;
or:
1. The 20-day SMA rises;
2. ADX rises but the amplitude is less than 0.2, indicating a moderate trend;
3. If RSI is less than 50, there is room for rebound.
Exit conditions:
1. RSI is greater than 75, indicating overbought;
2. ADX rose slightly, with a moderate trend;
or:
1. RSI is greater than 75, indicating overbought;
2. ADX rises sharply and the trend is strong;
or:
The SMA turned down on the 20th.
This strategy uses RSI to determine overbought and oversold, combined with ADX to determine the trend, to buy when the trend is upward but not overbought, and to exit when it is overbought or the trend weakens, and overall achieves the effect of tracking the mid- to long-term upward trend.
## Strategic Advantages
This strategy mainly has the following advantages:
1. Combining the two indicators RSI and ADX, you can more accurately judge the trend and overbought and oversold conditions, and make your entry and exit more accurately.
2. Judging the strength of the trend through ADX can reduce the risk of exiting the market due to market shocks.
3. RSI sets loose parameters to track medium and long-term trends and reduce frequent transactions.
4. The strategy is simple to operate and easy to implement, and is suitable for long-term positions.
5. The configurable parameters are flexible and the space for adjustment is large.
## Strategy Risk
This strategy also has certain risks:
1. The ADX indicator lags behind and may miss the trend conversion point, causing losses to expand.
2. When the stock price drops off a cliff, the stop loss may be triggered later, increasing the loss.
3. If the RSI parameter setting is too loose when entering the market, it may lead to overbought positions being held for too long.
4. The ADX parameter settings are too sensitive, which may result in incorrect exits when the trend is weak.
5. When the market is abnormal, individual stocks may also move in the opposite direction.
Corresponding risk management:
1. Appropriately shorten the ADX parameters to make it more sensitive.
2. Set a stricter stop loss line to avoid expanding losses.
3. Appropriately tighten the RSI parameters to prevent overbought positions from being held for too long.
4. Do not set the ADX parameters too sensitively to prevent errors.
5. When the market turns, pause the strategy appropriately and intervene manually.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Optimize RSI parameter settings and test the impact of different cycle parameters on the strategy effect.
2. Optimize the ADX parameter combination and test the impact of DI and ADX cycle parameters on the strategy's ability to capture trends.
3. Test and add other indicators such as MACD as auxiliary judgment.
4. Test different moving average combinations to optimize entry timing.
5. Test the addition of stop-profit and stop-loss strategies to improve the strategy's profit-risk ratio.
6. Judge the status of the market index and manually pause the strategy when the market turns.
## Summarize
The RSI tracking ADX strategy is overall a relatively simple and practical long-term trend tracking strategy. It combines the advantages of two indicators, RSI and ADX, and is more accurate in judging trends and overbought and oversold. The strategy is simple to operate and easy to implement, and it also has certain room for parameter optimization. But you also need to pay attention to ADX lag issues and stop loss setting issues. Generally speaking, this strategy is very suitable for tracking medium and long-term trends and can bring stable returns to investors.
|| 


## Summary 

The RSI Tracking ADX strategy is a trend following strategy that combines the RSI indicator and the ADX indicator. It uses the RSI indicator to determine overbought and oversold conditions, and the ADX indicator to gauge trend strength, allowing entries during uptrends when not overbought and exits when trends weaken or become overbought.

## Strategy Logic

The strategy mainly utilizes a combination of the RSI indicator and the ADX indicator to determine entries and exits.

Entry conditions:

1. 20-day SMA rising;

2. ADX rising more than 0.2 from previous day, indicating strengthening trend; 

3. RSI below 85 to avoid overbought state;

Or:

1. 20-day SMA rising;

2. ADX rising but less than 0.2, indicating mild trend;

3. RSI below 50, room for rebound.

Exit conditions:

1. RSI above 75, overbought state;

2. ADX mild rise, weak trend;

Or: 

1. RSI above 75, overbought state;

2. ADX sharp rise, strong trend;

Or:

20-day SMA turning down.

The strategy uses RSI for overbought/oversold and ADX for trend to enter during uptrends when not overbought and exit when overbought or trend weakens. This allows following medium to long term uptrends.

## Advantages

The main advantages of this strategy are:

1. Combining RSI and ADX allows more accurate trend and overbought/oversold readings for better entries and exits.

2. ADX gauges trend strength to avoid whipsaw exits during consolidation.  

3. RSI uses loose parameters to follow medium to long term trends and reduce excessive trading.

4. Simple logic and easy implementation, suitable for long term holdings.

5. Configurable parameters allow flexibility.

## Risks

The main risks are:

1. ADX lag may miss trend turning points leading to larger losses.

2. Stop loss may trigger late during cliff-like price drops, enlarging losses.

3. RSI parameters too loose may cause overbought holdings for too long.

4. ADX parameters too sensitive may wrongly trigger exits during weak trends.  

5. Stocks may behave abnormally during market regime shifts.

Risk management:

1. Use shorter ADX periods for sensitivity.

2. Tighter stop loss to limit losses.

3. Shorten RSI periods to avoid prolonged overbought holdings.

4. Avoid ADX parameters too sensitive.

5. Manually override during significant market shifts.

## Enhancements

The strategy can be optimized by:

1. Testing RSI periods for better parameters.

2. Optimizing ADX periods for trend capturing ability.

3. Adding other indicators like MACD for confirmation.

4. Testing moving average combinations to improve entries. 

5. Adding profit taking and stop losses to enhance risk-reward ratio.

6. Judging market regimes to manually override at turning points.

## Conclusion

The RSI Tracking ADX strategy is an effective yet simple trend following strategy. It synergizes the strengths of RSI and ADX for accurate trend and overbought/oversold analysis. The logic is straightforward and easy to implement with optimization flexibility. Caution is needed against ADX lag and stop loss setting. Overall it is suitable for medium to long term trend tracking and can provide steady profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|ADX Smoothing|
|v_input_2|14|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-03 00:00:00
end: 2023-10-09 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Copyright by Reed Asset Management registered in Shanghai, China
//该策略为上海蘆田资产管理有限公司制
//@version=2
strategy("[蘆田策略]ADX+RSI", overlay=true)

//ADX
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

plot(sig, color=red, title="ADX")

//ADX+RSI Strategy Long Entry
longEntry1 = sma(close, 20) > sma(close, 20)[1] //check if the ADX is rising
longEntry2 = (adx(14, 14) - adx(14, 14)[1]) > 0.2
longEntry3 = rsi(close, 14) < 85
longEntry4 = (adx(14, 14) - adx(14, 14)[1]) > 0
longEntry5 = (adx(14, 14) - adx(14, 14)[1] ) < 0.2
longEntry6 = rsi(close, 14) < 50

longCondition1 = longEntry1 and longEntry2 and longEntry3
longCondition2 = longEntry1 and longEntry4 and longEntry5 and longEntry6
if(longCondition1 or longCondition2)
    strategy.entry("long", strategy.long)

//ADX+RSI Strategy Long Exit
longExit1 = rsi(close, 9) > 75
longExit2 = (adx(14, 14) - adx(14, 14)[1]) > 0
longExit3 = (adx(14, 14) - adx(14, 14)[1] ) < 0.2
longExit4 = (adx(14, 14) - adx(14, 14)[1]) > 0.2
longExit5 = sma(close, 20) < sma(close,20)[1]

longExitCondition1 = longExit1 and longExit2 and longExit3
longExitCondition2 = longExit1 and longExit4
longStop1 = strategy.position_avg_price + 4 * tr
longExitCondition3 = longExit5
longStop2 = sma(close, 20)

strategy.close_all(when = longExitCondition1)
if (longExitCondition2)
    strategy.exit("exit", "long", stop = longStop1)
if (longExitCondition3)
    strategy.exit("exit", "long", stop = longStop2)
    

//Strategy

```

> Detail

https://www.fmz.com/strategy/428853

> Last Modified

2023-10-10 10:32:48
