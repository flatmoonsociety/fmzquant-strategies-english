
> Name

Trend following strategy based on CCI zero CCI-Zero-Crossing-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the zero crossing of the CCI indicator as a signal to enter and exit the market to capture the direction of the trend. Go long when the CCI indicator crosses zero from the negative zone, and go short when it crosses zero from the positive zone to achieve the effect of tracking the trend.
## Strategy Principle
- The length of the CCI indicator used is 20 periods.
- When the CCI indicator crosses 0, enter the market long and the stop loss line is -100.
- When the CCI indicator crosses 0, enter the market short and the stop loss line is 100. 
- The condition for closing the position is that the CCI indicator crosses zero again.
The core logic of this strategy is to capture the zero crossing of the CCI indicator as a signal to determine the price trend. When the CCI indicator enters the positive area from the negative area, it means that the price has left the oversold area and may form an upward trend; when the CCI indicator enters the negative area from the positive area, it means that the price has left the overbought area and may form a downward trend. The strategy enters the market when a crossover occurs and sets a reasonable stop loss distance to control risks.
## Advantage Analysis
- Use the zero crossing of the CCI indicator to determine the trend direction. This is a more classic application method of the CCI indicator.
- Using the CCI indicator with appropriate parameter length can filter out excessive noise trading signals and capture the main trend conversion points.
- The strategy only enters the market once when the trend changes and sets a stop loss, which can reduce unnecessary excessive transactions and concentrate funds to pursue big profits.
- The CCI indicator parameters and stop loss distance have been optimized to make the strategy parameters more universal.
## Risk Analysis
- The CCI indicator may produce false breakthrough zero cross signals, leading to unnecessary losses.
- Improper stop loss distance setting may cause the stop loss to be too loose or too narrow.
- The CCI indicator parameter length setting is unreasonable and may filter out effective trading opportunities in shorter periods.
- There is a certain risk of missing time, that is, the price trend has been formed, but the zero cross signal of the CCI indicator lags behind, resulting in late entry.
Countermeasures:
- Confirm in combination with other indicators to avoid false crosses of the CCI indicator. 
- Dynamically adjust stop loss distance.
- Optimize the CCI parameter length so that it can capture the trend of different cycle lengths.
- Appropriately relax the entry conditions and do not have to stick to the CCI zero cross.
## Optimization direction
This strategy can be further optimized from the following directions:
1. Optimize the parameter length of the CCI indicator and find the best parameter combination. You can find the optimal parameters by traversing parameters of different lengths, testing the rate of return and winning rate.
2. Increase the confirmation of other indicators, such as KDJ, MACD, etc., to avoid unnecessary losses caused by false breakthroughs of the CCI indicator. You can set the price to continue to break through a certain price range, or other indicators simultaneously send signals before entering the market.
3. Dynamically adjust the stop loss distance. The range of the stop loss distance can be automatically adjusted according to the degree of market fluctuations. Lowering the stop loss distance is beneficial to stopping losses in time, but it may also be too sensitive; increasing the stop loss distance is beneficial to continuing the trend, but it may also cause large losses.
4. Optimize entry conditions to reduce misses. You can relax the entry conditions, start entering the market when the CCI indicator is close to zero, and gradually increase the position, instead of entering the market only after crossing zero.
5. Add exiting conditions for trend judgment to maximize profits. When the trend reverses, a new exit signal can be set, such as taking profit when the price retraces to a certain extent.
## Summarize
This strategy uses the zero cross of the CCI indicator to determine the direction of the price trend, enter the market when the cross occurs, and set a reasonable stop loss distance, which can effectively track the trend. After the strategy is optimized, it can become a stable and reliable trend following strategy. Combining other indicator confirmations, optimizing parameter settings, improving entry conditions, adding reversal exit mechanisms, etc. can further enhance the effect of the strategy. Investors can choose appropriate stop loss distance, holding time and other parameters based on their own risk preferences, and use this strategy to make profits.
||

## Overview

This strategy uses the zero crossings of the CCI indicator as entry and exit signals to capture the trend direction. It goes long when the CCI breaks above zero from the negative zone, and goes short when the CCI breaks below zero from the positive zone, to follow the trend.

## Strategy Logic

- Use 20 periods for the CCI indicator.
- When CCI crosses above 0, go long with stop loss at -100.
- When CCI crosses below 0, go short with stop loss at 100.
- Exit when CCI crosses zero again.

The core logic is to capture the zero crossings of CCI as signals of trend changes. When CCI goes from negative to positive zone, it indicates prices have moved out of oversold and may start an uptrend. When CCI goes from positive to negative zone, it indicates prices have moved out of overbought and may start a downtrend. The strategy enters on the crossings and sets reasonable stop loss to control risk.

## Advantage Analysis 

- Using CCI zero crossings to determine trend direction is a classical application of the indicator.
- Appropriate CCI length filters out noise and catches major trend change points.
- Only one entry per trend, with stops. Reduces overtrading, concentrates funds for big wins.
- CCI parameters and stop distance are optimized for better universality.

## Risk Analysis

- CCI may give false crossing signals, causing unnecessary losses.
- Improper stop loss distance may be too wide or too narrow. 
- Wrong CCI length may filter out useful shorter period opportunities.
- Time lag risk exists. CCI may lag behind actual trend forming, causing late entry.

Solutions:

- Add other indicators for confirmation, avoid false CCI crossings.
- Dynamically adjust stop distance.
- Optimize CCI length to catch trends across timeframes. 
- Relax entry rules, don't strictly require CCI zero crossings.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Optimize CCI parameter length to find best setting. Test different lengths and evaluate profitability and win rate.

2. Add other indicators like KDJ, MACD for confirmation, avoid false CCI signals. Require persistent breakout of price levels or concurring signals.

3. Dynamically adjust stop loss distance based on market volatility. Tighter stops mean timely stops but may be too sensitive. Wider stops allow holding trends but increase loss if stopped out.

4. Relax entry rules to reduce missed entries. Start scaling in as CCI approaches zero crossing, instead of waiting for exact cross. 

5. Add trend exit rules to maximize profits. New exits when trend reverses, like price pulling back certain percentage.

## Conclusion

This strategy uses CCI zero crossings to determine trend direction and enter on the crossings with reasonable stop loss, effectively following trends. Further optimizations on confirmation, parameter tuning, entry rules, and exits can enhance it into a stable trend following strategy. Traders can adopt appropriate stop distance, holding period based on risk preference, and profit using this strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|CCI Period Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2023-09-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("CCI Level Zero Strategy (by Marcoweb) v1.0", shorttitle="CCI_L_Z_Strat_v1.0", overlay=true)

///////////// CCI
CCIlength = input(20, minval=1, title="CCI Period Length") 
CCIoverSold = -100
CCIoverBought = 100
CCIzeroLine = 0
CCI = cci(hlc3, CCIlength)
price = hlc3
vcci = cci(price, CCIlength)

source = close
buyEntry = crossover(source, CCIzeroLine)
sellEntry = crossunder(source, CCIzeroLine)
plot(CCI, color=black,title="CCI")
p1 = plot(CCIoverSold, color=blue,title="-100")
p2 = plot(CCIoverBought, color=red,title="100")
p3 = plot(CCIzeroLine, color=orange,title="0")


///////////// CCI 0Trend v1.0 Strategy 
if (not na(vcci))

    if (crossover(CCI, CCIzeroLine))
        strategy.entry("CCI_L", strategy.long, stop=CCIoverSold,  comment="CCI_L")
    else
        strategy.cancel(id="CCI_L")
        
    if (crossunder(CCI, CCIzeroLine))
        strategy.entry("CCI_S", strategy.short, stop=CCIoverBought,  comment="CCI_S")
    else
        strategy.cancel(id="CCI_S")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/428098

> Last Modified

2023-09-28 16:00:36
