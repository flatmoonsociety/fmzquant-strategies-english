
> Name

Movement Indicator and Detrended Price Oscillator Combination Strategy DMI-DPO-Guard-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9930ed2835efb90441.png)

[trans]

## Overview
This strategy combines two powerful indicators built into the trading view - the Movement Index (DMI) and the Detrended Price Oscillator (DPO) - to form a reliable basis for trading decisions. The core logic of the strategy is to determine whether the value of the DPO indicator is greater than 0 when the DMI indicator appears as a golden cross. If it is greater than 0, a long signal is generated; if the DMI indicator appears as a dead cross, it is determined whether the value of the DPO indicator is less than 0. If it is less than 0, a short signal is generated. This can effectively filter out a large number of false signals generated in the range-bound market, thereby only generating trading signals when the trend is forming, and avoiding repeated stop losses during the shock.
## Strategy Principle
This strategy mainly uses the DMI indicator to determine the direction and strength of the trend. The DMI indicator consists of three curves: +DI, -DI and ADX. +DI represents bull power, -DI represents short power, and their intersection can determine the current trend direction; ADX represents the strength of the trend, and the higher the value, the more obvious the trend. However, ADX does not have a good identification effect on low shocks. This strategy removes the judgment of ADX and only uses the intersection of +DI and -DI to determine the trend direction.
In order to filter out false signals generated during range oscillations, the strategy introduces the DPO indicator to assist in judgment. The DPO indicator represents the degree of deviation of the price from the mid-range. When the price is above the mid-range, DPO is positive, and when the price is below the mid-range, the DPO is negative. This strategy uses the positive and negative of the DPO indicator to determine whether it is currently in a trend. If the DMI indicator crosses but the DPO indicator is close to the 0 level, it is judged to be a shock and no trading signal is generated.
Specifically, the judgment logic is:
1. When +DI crosses -DI, ​​it is a golden cross and is judged to be a long market. At this time, if the DPO indicator is greater than 0, it is confirmed that it is currently in an upward trend, and a long signal is generated.
2. When -DI crosses +DI, it is a dead cross and it is judged to be a short market. At this time, if the DPO indicator is less than 0, it is confirmed that it is currently in a downward trend, and a short signal is generated.
3. If +DI/-DI crosses but the DPO indicator is close to 0, it is judged as a shock and no signal is generated.
## Advantage Analysis
The biggest advantage of this combination strategy is that it is highly accurate in identifying trends. Trading signals will only be generated when a real trend reversal occurs, thus avoiding repeated losses in the volatile range. Its main advantages are:
1. Using the DMI indicator to judge the direction and intensity of the trend is a mature and reliable technical indicator.
2. Use the DPO indicator to filter out false signals of range oscillations and only generate signals when a trend is formed to avoid losses.
3. Combining multiple indicators can verify each other and improve the reliability of the signal.
4. The strategy logic is simple and clear, easy to understand and implement, and is suitable for automatic or manual trading.
5. Because you only trade in trends, you can get a larger risk-reward ratio.
## Risk Analysis
Although this is a more reliable strategy, there are still risks to be aware of:
1. Unexpected events lead to huge unilateral market movements, and this trend opportunity may be missed. This risk can be reduced by lowering the DPO parameters.
2. The DMI indicator itself may also produce false signals, and this risk cannot be completely avoided. Stop losses can be set to control losses.
3. Improper setting of DPO indicator parameters may also lead to misjudgment. Optimum parameters should be determined through repeated backtesting.
4. Transaction costs will have a certain impact on profits, and transaction frequency should be controlled. Invalid transactions can be reduced by optimizing parameters.
## Optimization direction
There is still room for further optimization of this strategy:
1. Different parameter combinations can be tested to find the best parameters to reduce signal delay and improve profitability.
2. Can be combined with other indicators such as KDJ, MACD, etc. for verification to improve signal accuracy.
3. Adaptability parameters can be set according to different varieties, cycles, etc. to make the strategy more adaptable.
4. Dynamic stop loss can be set to control single losses. You can also set different stop loss ranges according to the trend stage.
5. The timing of entry and exit can be optimized through machine learning and other methods in order to obtain higher returns.
## Summarize
This strategy comprehensively uses the advantages of the two indicators DMI and DPO. It has high accuracy in judging trend reversal and can reliably identify the generation of the trend. At the same time, the DPO indicator is used to effectively filter the noise caused by range oscillations and avoid invalid transactions. This makes it a highly effective strategy suitable for automated trading as well as manual adoption. Of course, there are still many details that can be further optimized to obtain better strategy performance. However, this idea of ​​combining indicators has important reference significance for the design of quantitative trading strategies.
||

## Overview

This strategy combines two powerful built-in indicators in TradingView - the Directional Movement Index (DMI) and the Detrended Price Oscillator (DPO) to form a reliable basis for trading decisions. The core logic of the strategy is to determine if the DPO value is greater than 0 when a DMI golden cross occurs, and generate a long signal if so; or to determine if the DPO value is less than 0 when a DMI dead cross occurs, and generate a short signal if so. This can effectively filter out a lot of false signals generated during range-bound oscillations in the market, thereby only generating trading signals when a trend is formed, avoiding repeated stop losses during oscillations.

## Principle  

This strategy mainly uses the DMI indicator to determine the trend direction and strength. The DMI indicator consists of three curves: +DI, -DI and ADX. +DI represents the strength of uptrend, -DI represents the strength of downtrend, and their crossover can determine the current trend direction; ADX represents the strength of the trend, the higher the value, the more obvious the trend. However, ADX is not good at identifying low volatility ranges, so this strategy removes the ADX determination and only uses the +DI and -DI crossovers to determine the trend direction.  

In order to filter out the false signals generated in the range-bound oscillations, the DPO indicator is introduced for auxiliary judgment. The DPO indicator represents the degree of deviation of the price from its middle rail. When the price is above the middle rail, the DPO is positive, and when below, it is negative. This strategy uses the positivity and negativity of the DPO indicator to judge whether it is currently in a trend. If the DMI indicator crosses but the DPO indicator is close to the 0 level, it is determined to be an oscillation and no trading signal is generated.

Specifically, the judgment logic is:  

1. When +DI crosses above -DI, it is a golden cross, indicating a bull market. At this time, if the DPO indicator is greater than 0, it confirms that it is currently in an upward trend, and a long signal is generated.

2. When -DI crosses below +DI, it is a dead cross, indicating a bear market. At this time, if the DPO indicator is less than 0, it confirms that it is currently in a downward trend, and a short signal is generated.  

3. If +DI/-DI crosses but DPO indicator is close to 0, it is determined as oscillation and no signal is generated.

## Advantage Analysis   

The biggest advantage of this combined strategy is its high accuracy in identifying trends, generating trading signals only when real trend reversals occur, thus avoiding repeated losses in oscillating intervals. Its main advantages are:

1. Using the DMI indicator to determine the trend direction and strength, it is a mature and reliable technical indicator.  

2. Filter out false signals in range-bound oscillations with the help of the DPO indicator, generate signals only when a trend is formed, avoiding losses.

3. Combining multiple indicators can serve as mutual verification and improve the reliability of signals. 

4. The strategy logic is simple and easy to understand and implement, suitable for automated or manual trading.

5. Since it only trades in trends, it can obtain a relatively high risk reward ratio.

## Risk Analysis

Although this is a highly reliable strategy, the following risks should be noted:

1. Sudden events may cause huge one-sided moves in the market, possibly missing such trend opportunities. This risk can be reduced by lowering the DPO parameters.

2. The DMI indicator itself may also generate wrong signals, and this risk cannot be completely avoided. Losses can be controlled by setting stops.

3. Improper parameter settings of the DPO indicator can also lead to misjudgments. The optimal parameters should be determined through repeated backtesting.  

4. Trading costs will have a certain impact on profits, so the trading frequency should be controlled. Invalid trades can be reduced by optimizing parameters.

## Optimization

There is still room for further optimization of this strategy:  

1. Different parameter combinations can be tested to find the optimal parameters to reduce signal delay and increase profit rate.

2. Can be combined with other indicators such as KDJ, MACD, etc. for verification to improve signal accuracy. 

3. Adaptive parameters can be set according to different varieties, cycles, etc. to make the strategy more adaptive.  

4. Dynamic stops can be set to control single loss. Different stop loss amplitudes can also be set according to trend stages.

5. Machine learning methods can be used to optimize entry and exit timing for higher returns.

## Summary  

This strategy combines the advantages of the DMI and DPO indicators to have high accuracy in judging trend reversals, and can reliably identify the generation of trends. At the same time, the use of the DPO indicator effectively filters out the noise caused by range-bound oscillations, avoiding ineffective trades. This makes it an efficient strategy suitable for automated trading and manual adoption. Of course, there are still many details that can be further optimized for better strategy performance. But the idea of combining indicators has important reference significance for quantitative trading strategy design.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|34|DI Lookback|
|v_input_2|34|Length|
|v_input_3|false|Centered|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-28 00:00:00
end: 2024-01-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("DMI DPO Guard Strategy", calc_on_order_fills=true, initial_capital=100000, default_qty_type=strategy.percent_of_equity, default_qty_value=10, currency="USD", commission_type=strategy.commission.percent, commission_value=0.25)

///Tradingview's DMI indicator logic///
len = input(34, minval=1, title="DI Lookback")
up = change(high)
down = -change(low)
plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
trur = rma(tr, len)
plus = fixnan(100 * rma(plusDM, len) / trur)
minus = fixnan(100 * rma(minusDM, len) / trur)

plot(plus, color=color.orange, title="+DI")
plot(minus, color=color.aqua, title="-DI")


period_ = input(34, title="Length", minval=1)
isCentered = input(false, title="Centered")
barsback = period_/2 + 1
ma = sma(close, period_)
dpo = isCentered ? close[barsback] - ma : close - ma[barsback]
plot(dpo, offset = isCentered ? -barsback : 0, title="Detrended Price Oscillator", color=#C0C000)
hline(0, title="Zero Line", color = #C0C0C0)

long = crossover(plus, minus) and (dpo > 0)
short = crossunder(plus, minus) and (dpo < 0)

strategy.entry("Long", strategy.long, when=long)
strategy.entry("Short", strategy.short, when=short)



```

> Detail

https://www.fmz.com/strategy/437692

> Last Modified

2024-01-04 17:56:28
