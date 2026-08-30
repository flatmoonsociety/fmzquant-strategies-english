
> Name

MACD Momentum-Entangled-with-DMI-Breakout-Short-Term-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10f9c64555169d84b4b.png)
[trans]


## Overview
This strategy focuses on short-term shorting in bear market conditions, using two strength indicators to provide a signal that jointly confirms that the short-term downward trend has begun - seize the shorting opportunity as soon as possible.
This strategy works especially well for coins that you plan to hold for the long term, while using automated trading bots to execute your trades. It allows you to hedge your investment by allocating a percentage of your holdings to trades without risking your entire position. This mitigates unrealized losses from holding coins as it generates additional cash from profits. You can then choose to hold this cash or reinvest it when the market reaches attractive buying levels.
On the other hand, if you trade contracts in the futures market, you can go short directly without first owning the underlying asset.
## Strategy Principle
This trading system uses the MACD momentum indicator and the DMI trend indicator to identify the best selling opportunities. Combining these two indicators can avoid trading in an uptrend and reduce the likelihood of getting stuck in a low-volatility market.
MACD is a trend-following momentum indicator that identifies short-term trend direction. In this variant, it uses 12 periods as fast and 26 periods as slow length EMA while the signal smoothness is set to 9.
The DMI indicates the trend direction of the price and compares the previous lows and highs, drawing two lines between them - a positive movement line (+DI) and a negative movement line (-DI). Trends can be explained by comparing two lines and which line is larger. When the negative DMI is greater than the positive DMI, the asset is more likely to be in a continued downward trend, and vice versa.
When two conditions are met, the system will enter the transaction:
1. MACD histogram turns bearish.
2. Negative DMI is greater than positive DMI.
This strategy comes with a fixed take profit, combined with a volatility stop, which acts as a trailing stop to suit the strength of the trend. Depending on your long-term confidence in the asset, the fixed take profit can be edited to make it more conservative or aggressive.
Positions are closed when the following conditions are met:
Take Profit Closing: +8% entry price drop.
or
Stop loss and close position: the price breaks through the volatility stop loss.
Overall, this approach is suitable for medium to long-term strategies. The backtest of this strategy starts from April 1, 2022 to July 18, 2022, to prove its effectiveness in a bear market. Further backtesting from early 2022 also produced good returns.
It performs particularly well in combinations such as SOLUSDT with a 45-minute time period, MATICUSDT with a 2-hour time period, and AVAUSDT with a 1-hour time period. Overall, backtesting shows that it works best on the 45 minute/1 hour timeframe for most pair combinations.
Trading fees are also taken into account, aligning with Binance’s base fee of 0.1%.
## Advantage Analysis
This strategy has the following advantages:
- Take advantage of the two indicators MACD and DMI to improve the accuracy of entry signals and avoid false breakthroughs.
- Adopt an exit mechanism that combines fixed take-profit and volatility trailing stop-loss, which not only ensures a high take-profit but also controls risks.
- Suitable for the falling stage of bear market and can obtain higher short-term arbitrage income.
- Can be used to hedge long-term positions and obtain additional income. You can also directly short the contract for arbitrage.
- The backtest performance is excellent, especially in the 1-hour and 45-minute periods, which is suitable for high-frequency trading.
## Risk Analysis
This strategy also has the following risks:
- As tracking indicators, DMI and MACD have a high probability of generating false signals at trend turning points, so you need to pay attention to stop loss.
- Improper setting of fixed take profit may result in the take profit being too small or too large. It is recommended to adjust according to the volatility of different currencies.
- Volatility trailing stop loss may be breached during periods of severe volatility, requiring Combine With Additional Stop Loss.
- Improper selection of the backtest time period may lead to overly optimistic results. It should be backtested for a longer period of time and also test different market stages.
- The effect of the real offer will be affected by factors such as transaction fees, market order slippage, etc., and will be different from the backtest.
## Optimization direction
This strategy can be further optimized from the following aspects:
- Use machine learning methods to automatically optimize the parameter combination of MACD and DMI to adapt to different cycles and currencies.
- Add dynamic take-profit based on volatility, and adjust the take-profit range according to market volatility.
- Add other indicator judgments to form a multi-factor model and improve the filtering effect. Such as BVN and OBV indicators.
- Add a machine learning model to determine trends and assist MACD and DMI in sending signals.
- Use limit orders instead of market orders to reduce the impact of transaction slippage.
- Test different currencies separately to find the optimal combination of cycle parameters.
## Summarize
To sum up, this short-term bear market arbitrage strategy uses the powerful combination of MACD and DMI to determine the timing of shorting and achieves high quantitative returns. It can be used to hedge long-term positions or directly perform short arbitrage on futures contracts. Optimizing stop loss strategies and parameter adjustments can further improve the winning rate. This strategy deserves active use and optimization by bear market traders.
|| 

## Overview

This strategy focuses on shorting during bear market conditions by utilizing two strength-based indicators to provide confluence that the start of a short-term downtrend has occurred - catching the shorting opportunity as soon as possible.

The strategy works well on coins you plan to hodl long-term and performs especially well whilst using an automated trading bot that can execute trades for you. It allows you to hedge your investment by allocating a percentage of your coins to trade with, without risking your entire holding. This mitigates unrealized losses from hodling as it provides additional cash from the profits made. You can then choose to hodl this cash, or use it to reinvest when the market reaches attractive buying levels. 

Alternatively, you can use this when trading contracts on futures markets where there is no need to already own the underlying asset prior to shorting it.

## Strategy Logic

The trading system uses the Momentum Average Convergence Divergence (MACD) indicator and the Directional Movement Index (DMI) indicator to confirm when the best time is for selling. Combining these two indicators prevents trading during uptrends and reduces the likelihood of getting stuck in a market with low volatility.

The MACD is a trend following momentum indicator and provides identification of short-term trend direction. In this variation it utilizes the 12-period as the fast and 26-period as the slow length EMAs, with signal smoothing set at 9.

The DMI indicates what way price is trending and compares prior lows and highs with two lines drawn between each - the positive directional movement line (+DI) and the negative directional movement line (-DI). The trend can be interpreted by comparing the two lines and what line is greater. When the negative DMI is greater than the positive DMI, there are more chances that the asset is trading in a sustained downtrend, and vice versa.

The system will enter trades when two conditions are met:

1) The MACD histogram turns bearish. 

2) When the negative DMI is greater than the positive DMI.

The strategy comes with a fixed take profit combined with a volatility stop, which acts as a trailing stop to adapt to the trend's strength. Depending on your long-term confidence in the asset, you can edit the fixed take profit to be more conservative or aggressive.

The position is closed when:

Take-Profit Exit: +8% price decrease from entry price.

OR

Stop-Loss Exit: Price crosses above the volatility stop.

In general, this approach suits medium to long term strategies. The backtesting for this strategy begins on 1 April 2022 to 18 July 2022 in order to demonstrate its results in a bear market. Back testing it further from the beginning of 2022 onwards further also produces good returns.

Pairs that produce very strong results include SOLUSDT on the 45m timeframe, MATICUSDT on the 2h timeframe, and AVAUSDT on the 1h timeframe. Generally, the back testing suggests that it works best on the 45m/1h timeframe across most pairs. 

A trading fee of 0.1% is also taken into account and is aligned to the base fee applied on Binance.

## Advantage Analysis

The advantages of this strategy include:

- Utilizes the strengths of both MACD and DMI indicators to improve the accuracy of entry signals and avoid false breakouts.

- Employs a combination of fixed take profit and volatility trailing stop exit mechanisms to ensure higher take profits while controlling risk.

- Suitable for bear market downtrends to capture substantial short-term scalping profits. 

- Can be used to hedge long positions to gain additional income. Or directly short futures contracts for scalping.

- Strong backtest results, especially on 1h and 45m timeframes suitable for high frequency trading.

## Risk Analysis

The risks of this strategy include:

- DMI and MACD as lagging indicators have a higher probability of generating erroneous signals around trend turning points, requiring stop loss monitoring.

- Improper fixed take profit settings may result in take profits being too small or too large. Adjustments based on different coin volatility is recommended.

- Volatility trailing stops can be broken during periods of violent swings, requiring combination with additional stop loss. 

- Improper backtest time period selection may lead to overly optimistic results. Longer testing across different market conditions should be done.

- Real-world performance will be impacted by trading fees, market order slippage etc leading to deviations from backtest.

## Optimization Directions

This strategy can be further optimized in the following aspects:

- Utilize machine learning to auto optimize MACD and DMI parameter combinations, adapted to different timeframes and coins.

- Add volatility based dynamic take profits, adjusting take profit range based on market volatility.

- Incorporate additional indicators, forming a multi-factor model to improve filtering. Such as BVN and OBV.

- Add machine learning models to aid MACD and DMI in signaling. 

- Use limit orders instead of market orders to reduce slippage impact.

- Test on individual coins to find optimal timeframe parameters.

## Conclusion

In summary, this short-term bear scalping strategy provides substantial quantitative profits by identifying optimal shorting moments through the powerful MACD and DMI combination. It can be used to hedge long positions and directly short futures contracts. Optimizing stops and tuning parameters can further improve win rate. The strategy merits active application and optimization by bear market traders.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|3|Take_profit|
|v_input_int_1|20|Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|vStop Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-13 00:00:00
end: 2023-11-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Inverse MACD + DMI Scalping with Volatility Stop (Shorting) (By Coinrule)",

         overlay=true,
         initial_capital=10000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=100,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 4, 1, 0, 0)
notInTrade = strategy.position_size <= 0

// DMI and MACD inputs and calculations
[pos_dm, neg_dm, avg_dm] = ta.dmi(14, 14)
[macd, macd_signal, macd_histogram] = ta.macd(close, 12, 26, 9)

Take_profit = input(3) / 100
longTakeProfit = strategy.position_avg_price * (1 + Take_profit)

length = input.int(20, 'Length', minval=2)
src = input(close, 'Source')
factor = input.float(2.0, 'vStop Multiplier', minval=0.25, step=0.25)
volStop(src, atrlen, atrfactor) =>
    var max = src
    var min = src
    var uptrend = true
    var stop = 0.0
    atrM = nz(ta.atr(atrlen) * atrfactor, ta.tr)
    max := math.max(max, src)
    min := math.min(min, src)
    stop := nz(uptrend ? math.max(stop, max - atrM) : math.min(stop, min + atrM), src)
    uptrend := src - stop >= 0.0
    if uptrend != nz(uptrend[1], true)
        max := src
        min := src
        stop := uptrend ? max - atrM : min + atrM
        stop
    [stop, uptrend]
    
[vStop, uptrend] = volStop(src, length, factor)

closeShort = close > longTakeProfit or ta.crossunder(close, vStop)

//Entry
strategy.entry(id='short', direction=strategy.short, when=ta.crossover(macd_signal, macd) and pos_dm < neg_dm and timePeriod)

//Exit
strategy.close('short', when=closeShort and timePeriod)

```

> Detail

https://www.fmz.com/strategy/431968

> Last Modified

2023-11-13 17:42:23
