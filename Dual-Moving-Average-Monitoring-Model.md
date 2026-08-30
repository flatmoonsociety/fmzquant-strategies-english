
> Name

Dual-Moving-Average-Monitoring-Model
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fb4b3b16dd02f3b088.png)

[trans]

## Overview
This strategy uses the combined indicator of the double exponential moving average (EMA) and the moving average cross point (MACD) to discover short-term overvalued stocks and conduct short-term shorting to profit from the decline in stock prices. The strategy makes full use of EMA's ability to quickly respond to price changes, combined with MACD's advantage of monitoring momentum and wind direction, to capture short-term profit opportunities at the bull-bear transition point.
## Strategy Principle
1. Calculate the 8-day EMA and the 26-day EMA. When the 8-day EMA crosses the 26-day EMA, it is considered a buy signal.
2. Calculate the 12-day EMA, the 26-day EMA and the 9-day EMA of the difference DEA to form MACD. When MACD crosses DEA, it is considered a buy signal.
3. Buying conditions: 8-day EMA > 26-day EMA and MACD crosses DEA, go long when satisfied.
4. Exit conditions: Set the floating profit stop loss to 3% of the entry price, the trailing stop loss to 1% of the entry price, and close the position when either condition is met.
This strategy also uses the characteristics of EMA to quickly respond to price and MACD to determine the direction of momentum, and determine the direction of operation at key points when bulls turn to bears. The fast EMA reflects the correction of the slower EMA to the short-term intrinsic value, the MACD reflects the prediction of the moving average direction due to changes in trading intensity, and the dual indicators improve the accuracy of determining the trading time point.
## Advantage Analysis
1. The combination of EMA and MACD improves the accuracy of determining buying and selling points. EMA captures the trend of price changes, and MACD determines the direction of momentum changes. The two are combined to identify short-term extremum to avoid losses caused by false breakthroughs.
2. Track and stop losses to control risks, and stop losses and exit in a timely manner. Set a 1% trailing stop after entering the market to avoid losses from expanding.
3. The backtest data is sufficient. The strategy was backtested throughout the bear market in 2022, simulating the actual trading environment.
4. Flexible parameter adjustment. Stop loss ratio and position ratio can be customized to match personal risk preferences.
## Risk Analysis
1. Transactions are frequent and require close tracking. Use a 5-minute cycle, enter and exit frequently, and need enough time to follow up on transactions.
2. The trailing stop may be too densely exited. If the trailing stop loss range is set too small, the trade may be stopped prematurely.
3. It does not work well when the market is in a volatile trend. EMA and MACD are more suitable for more obvious trending markets.
4. Transaction costs need to be considered. Each transaction corresponds to a handling fee, and frequent transactions will lead to increased costs.
## Optimization direction
1. Adjust EMA cycle parameters and optimize trading opportunities. You can test to shorten the fast EMA period, expand the difference between EMAs, and find the best parameter combination.
2. Optimize the stop loss ratio and reduce the risk of premature stop loss. Appropriately relax the trailing stop loss range to avoid being too aggressive with the trailing stop loss.
3. Test different holding times and select the optimal holding period. Evaluate the strategic returns under different holding times and find the optimal holding period.
4. Evaluate and add other technical indicators to filter signals. You can test adding volatility indicators, etc. to improve the effect of trading decisions.
## Summarize
This double EMA moving average and MACD indicator trading strategy aims to capture the opportunity of a short-term drop in stock prices to make short-term profits. It takes full advantage of the rapid response of EMA and changes in MACD judgment strength to improve the accuracy of trading time points under double verification. The space for strategy optimization lies in parameter adjustment, slippage control, position holding time, etc. Careful parameter optimization can lead to better returns.
||

## Overview

This strategy uses a combination of dual exponential moving averages (EMA) and moving average crossover (MACD) indicators to identify overvalued stocks in the short term and take short positions to profit from price declines. The strategy takes full advantage of the EMA's ability to react quickly to price changes and MACD's strength in monitoring momentum direction, capturing short-term profit opportunities at turning points between bulls and bears.

## Strategy Logic

1. Calculate 8-day EMA and 26-day EMA. When 8-day EMA crosses above 26-day EMA, it is considered a buy signal.

2. Calculate MACD with 12-day EMA, 26-day EMA and 9-day EMA of the difference called DEA. When MACD crosses above DEA, it is considered a buy signal.

3. Entry rule: 8-day EMA > 26-day EMA and MACD crosses above DEA, long when both conditions are met.

4. Exit rule: Set trailing stop loss at 3% of entry price, trailing stop loss at 1% of entry price, exit when either is touched.

The strategy utilizes both the fast reaction of EMA to price and MACD's judgment on momentum direction, identifying the key turning points from bull to bear. The fast EMA reflects the correction of short-term intrinsic value against the slower EMA, while MACD reflects changes in trading power anticipating the direction of the moving averages, improving accuracy of capturing trading opportunities using dual indicators.

## Advantage Analysis 

1. EMA and MACD combination improves accuracy of capturing trading signals. EMA catches price trends while MACD judges momentum direction changes, combined they identify short-term extremums and avoid losses from false breakouts.

2. Trailing stop loss controls risks and exits timely. The 1% trailing stop set after entry avoids loss enlargement.

3. Solid backtest data. Strategy is backtested through the entire bear market in 2022, simulating real trading environments. 

4. Flexible parameter tuning. Stop loss ratio, position sizing ratio are customizable to match personal risk preference.

## Risk Analysis

1. Frequent trading requires close tracking. The 5-min timeframe means high frequency of entries and exits, requiring sufficient time to follow up the trades.

2. Trailing stop loss may exit prematurely. Overly tight trailing stop loss could lead to premature exits.

3. Poor performance in ranging markets. EMA and MACD work better for trending markets. 

4. Trading costs need consideration. Each trade corresponds to commissions, frequent trading increases costs.

## Optimization Directions

1. Adjust EMA period parameters to optimize entries and exits. Can test shortening fast EMA period, enlarging spread between EMAs to find optimal combinations.

2. Optimize stop loss ratio to lower premature stop risk. Appropriately widening the trailing stop loss avoids overly aggressive stops. 

3. Test different holding periods to find optimum. Evaluate returns for different holding periods to identify best holding duration.

4. Evaluate adding other technical filters. Test adding volatility index etc to improve effectiveness of trading decisions.

## Conclusion

This dual EMA and MACD trading strategy aims to capture short-term pullback opportunities for shorting and profiting. It fully utilizes the fast reaction of EMA and momentum change judgment strength of MACD to improve accuracy in trade timing with dual confirmation. Optimization spaces lie in parameter tuning, slippage control, holding period etc. Careful parameter optimization can lead to good returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_float_1|3|Trail Long Loss (%)|
|v_input_float_2|true|Trail Short Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-16 00:00:00
end: 2023-10-16 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=5
// strategy('Fast EMA above Slow EMA with MACD (by Coinrule)',
//          overlay=true,
//          initial_capital=1000,
//          process_orders_on_close=true,
//          default_qty_type=strategy.percent_of_equity,
//          default_qty_value=30,
//          commission_type=strategy.commission.percent,
//          commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 1, 1, 0, 0)
notInTrade = strategy.position_size <= 0

// EMAs 
fastEMA = ta.ema(close, 8)
slowEMA = ta.ema(close, 26)
plot(fastEMA, color = color.blue)
plot(slowEMA, color = color.green)
//buyCondition1 = ta.crossover(fastEMA, slowEMA)
buyCondition1 = fastEMA > slowEMA


// DMI and MACD inputs and calculations
[macd, macd_signal, macd_histogram] = ta.macd(close, 12, 26, 9)
buyCondition2 = ta.crossover(macd, macd_signal)


// Configure trail stop level with input options
longTrailPerc = input.float(title='Trail Long Loss (%)', minval=0.0, step=0.1, defval=3) * 0.01
shortTrailPerc = input.float(title='Trail Short Loss (%)', minval=0.0, step=0.1, defval=1) * 0.01

// Determine trail stop loss prices
longStopPrice = 0.0
shortStopPrice = 0.0

longStopPrice := if strategy.position_size > 0
    stopValue = close * (1 - longTrailPerc)
    math.max(stopValue, longStopPrice[1])
else
    0

shortStopPrice := if strategy.position_size < 0
    stopValue = close * (1 + shortTrailPerc)
    math.min(stopValue, shortStopPrice[1])
else
    999999
    

if (buyCondition1 and buyCondition2 and notInTrade and timePeriod)
    strategy.entry(id="Long", direction = strategy.long)

strategy.exit(id="Exit", stop = longStopPrice, limit = shortStopPrice)


//if (sellCondition1 and sellCondition2 and notInTrade and timePeriod)
//strategy.close(id="Close", when = sellCondition1 or sellCondition2)
```

> Detail

https://www.fmz.com/strategy/429497

> Last Modified

2023-10-17 16:33:29
