
> Name

Bitcoin-Volatility-Band-Reversion-Strategy Bitcoin-Volatility-Band-Reversion-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a pullback system designed for highly volatile securities, making Bitcoin a very ideal trade. This strategy can be used on the daily chart or lower time frames (I found good results on the 3 hour time frame but did not test it below the 1 hour).
## Strategy Principle
This strategy calculates volatility by comparing the changes in closing prices of the previous two candlesticks and uses this price change to generate a moving average. A standard deviation band is wrapped around the moving average, with the inner part being 1 standard deviation and the outer part being 2 standard deviations. If the price is above the preset moving average filter, it is determined that we are in an uptrend, so during an uptrend, if there is a pullback that causes the internal standard deviation band to be pierced, a buy signal is issued. But if the price continues to fall and breaks out of the outer standard deviation bands, a buy signal will not be issued as this would indicate that the volatility spike is too large. When the inner band is pierced, a pierce "buy" event with a green background will be displayed on the indicator. For sell/short trades, a signal is sent when the upper inner band breaks below the preset moving average filter, and a red background appears on the indicator.
Users can change the date range they want to test, the moving average period over which volatility is calculated, and the inner and outer band standard deviation. For Bitcoin, I leave the internal and external standard deviation bands at the standard settings, but find that the 3-period volatility tracking is good for 1-day chart trading and the 5-period volatility tracking is good for the 3-hour chart. Since this is not a buy and hold strategy, you may want to stick to the most liquid coins when trading so that you can get in and out of any exchange quickly. If you want to test this strategy on lower volatility markets, changing the internal standard deviation band to about 0.75 may work for various futures markets and possibly stocks as well. Stop loss and take profit levels are based on the trading range of the past 7 candlesticks.
## Strategic Advantages
- Use volatility trading to capture market turning points
- Two-way trading to profit in rising and falling markets
- Standard parameter settings are easy to use
- Easily optimize parameters to suit different targets
- Reasonable stop loss and take profit settings are beneficial to lock in profits
## Strategy Risk
- Highly volatile underlying assets carry the risk of expanding losses
- Frequent switching between long and short, high transaction fees
- For short-term operations, you need to pay close attention to market changes
- It is difficult to stop losses when the underlying liquidity is insufficient
- Improper parameters may lead to over-trading
Risk response methods:
1. Select the appropriate volatile target and control a single position.
2. Optimize parameters and reduce invalid transactions.
3. Adopt stop-profit and stop-loss, and strictly manage funds. 
4. Pay attention to transaction execution efficiency and choose targets with good liquidity.
5. Adjust parameters to adapt to different target characteristics.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the moving average period to better track the volatility of different targets.
2. Adjust the parameters of the volatility band to make it closer to the fluctuation range of the specific target.
3. Add other filtering conditions, such as transaction volume amplification, to further verify trading signals.
4. Use machine learning technology to dynamically optimize parameters to make the strategy more adaptable.
5. Test on higher frequency time frames to capture more trading opportunities.
6. Add stop-profit and stop-loss moving tracking to lock more profits in the account.
7. Combine with other indicators or models to establish a quantitative combination strategy.
## Summarize
The overall strategy is relatively simple and intuitive, using volatility indicators to identify reversal situations to capture market turning points. There is a large space for strategy optimization. By adjusting parameters and combining with other technical indicators, the stability and profitability of the strategy can be continued to be improved. But traders need to be careful to guard against over-optimization and curve-fitting issues. This strategy is more suitable for short-term trading and requires strict fund management to control risks. If mastered correctly, this strategy can be a powerful tool for trading highly volatile digital currencies.
||

## Overview

This strategy is a pullback system designed for securities with high volatility, so naturally Bitcoin is an excellent choice for trading this. This could be used both on a daily chart or on lower timeframes (I found good results on 3hr timeframe but haven't tested it on anything under 1hr).

## Strategy Logic

The strategy calculates volatility by comparing the change in closing price of the previous 2 candles, and uses this change in price to generate a moving average. A band is wrapped around the moving average with a standard deviation of 1 for the inner band and 2 for the outer band. If the price is above a pre-set MA (moving average) filter then it is determined we are in an uptrend so the strategy will issue a buy signal when we are in an uptrend and there is a pullback which causes the lower inner deviation band to be spiked, but if the price continues and falls through the outer deviation band then a buy signal will not issue as this detriments that the volatility spike is to great. You can see a spike "buy" event occur on the indicator where the background is coloured green. For a short/sell then there will be a spike on the upper inner band and we are below the pre-set MA filter, for this it shows with red background on the indicator.

The user can change the date range they wish to test, the moving average period for the volatility tracking and the inner and outer band deviations. On BTC I left the inner deviation and outer deviation bands on standard settings but found the 3 period volatility tracking to be good for trading 1 day chart and the 5 period volatility tracking good for the 3hr chart. Since this is not a buy and hold strategy then for trading you would probably want to stick with the most liquid coins so you can get in and out very fast on any exchange. If you wanted to tray this on less volatile markets then changing the inner deviation band to ~0.75 would work okay in various futures markets likely stocks as well. The take profit and stop loss levels are based on a multiple of the trading range looking back the past 7 candles.

## Advantages of the Strategy

- Utilizes volatility trading to capture market turning points
- Trades both long and short, profiting in up and down markets
- Simple standard parameter settings easy to use
- Parameters can be easily optimized for different underlyings  
- Reasonable stop loss and take profit settings help lock in profits

## Risks of the Strategy

- High volatility underlyings risk larger losses
- Frequent long/short switching incurs higher trading costs
- Short-term operations require close market monitoring
- Difficult to stop loss when low market liquidity
- Poor parameter tuning can lead to over-trading

Risk Mitigation Methods:

1. Choose appropriate volatile underlyings, control position sizing.

2. Optimize parameters to reduce ineffective trades. 

3. Use stop loss and take profit, strict money management.

4. Focus on execution efficiency, choose liquid underlyings.

5. Adjust parameters to suit different underlying characteristics.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize moving average period to better track volatility of different underlyings. 

2. Adjust volatility band parameters to better fit specific underlying's volatility range.

3. Add other filters like volume spike to further validate signals.

4. Use machine learning techniques to dynamically optimize parameters for adaptiveness.

5. Test on higher frequency timeframes to capture more trading opportunities.

6. Add moving stop loss/take profit tracking to lock in profits more.

7. Combine with other indicators or models to build quantitative portfolio strategies.

## Summary 

The strategy overall is rather simple and intuitive, identifying reversals via volatility indicator to capture market turning points. There is large optimization space by adjusting parameters and incorporating other technical indicators to further enhance stability and profitability. However traders need to be aware of overfitting and curve fitting problems. This strategy suits short-term trading more, requiring strict money management to control risks. If mastered properly, it can become a powerful tool for trading high volatility cryptocurrencies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|7| MA Length|
|v_input_2|true|Inner Band|
|v_input_3|2|Outer Band|
|v_input_4|true|From Day|
|v_input_5|true|From Month|
|v_input_6|2000|From Year|
|v_input_7|true|To Day|
|v_input_8|true|To Month|
|v_input_9|2100|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-10-11 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © gary_trades
//This script is designed to be used on volatile securities/tickers so is best suited for day charts on Crypto (particularly good for BTC).
//It takes both long and short trades and the main indicator settings can be changed by the use so they can test for ideal settings for ticker of interest.

//@version=4

strategy("BTC Volatility Band Strategy", shorttitle="Vol Band Strategy", overlay=false, margin_long=100, margin_short=100)

//VOLATILTY
CandleChange = ((close - close[1])/close)*100         //OR CandleChange = ((close[2] - close[1])/close)*100
plot(CandleChange, color=color.red, linewidth = 1)

//VOLATILITY BANDS 
MAlen = input(7, minval=3, maxval=30, title=" MA Length")
MAout = sma(CandleChange, MAlen)
plot(MAout, color=color.black, display=display.none)

InnerBand = input(1.0, minval=0.5, maxval=5, title="Inner Band")
OuterBand = input(2.00, minval=0.5, maxval=10, title="Outer Band")
devInner = InnerBand * stdev(CandleChange, MAlen)
devOuter = OuterBand * stdev(CandleChange, MAlen)

upper1 = MAout + devInner
lower1 = MAout - devInner
b1 = plot(upper1, "Upper Inner", color=color.gray)
b2 = plot(lower1, "Lower Inner", color=color.gray)
upper2 = MAout + devOuter
lower2 = MAout - devOuter
b3 = plot(upper2, "Upper Outer", color=color.gray)
b4 = plot(lower2, "Lower Outer", color=color.gray)
fill(b1, b3, color.rgb(250,145,175,70), title="Background")
fill(b2, b4, color.rgb(250,145,175,70), title="Background")

band1 = hline(25, "Upper Band", color=color.gray, linestyle=hline.style_dotted, linewidth=2)
band0 = hline(-25, "Lower Band", color=color.gray, linestyle=hline.style_dotted, linewidth=2)

//LONG FILTER
VolFilterL = CandleChange <= lower1 and CandleChange > lower2
SMAFilterL = close[1] > sma(close[1], 50)
PriceFilterL = close > lowest(close,7)
LongFilter = VolFilterL and SMAFilterL and PriceFilterL
bgcolor(LongFilter ? color.new(color.green, 80) : na)

//SHORT FILTER
VolFilterS = CandleChange >= upper1 and CandleChange < upper2
SMAFilterS = close[1] < sma(close[1], 50)
PriceFilterS = close < highest(close,7)
ShortFilter = VolFilterS and SMAFilterS and PriceFilterS
bgcolor(ShortFilter ? color.new(color.red, 80) : na)

//SETTING BACK TEST INPUTS
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2000, title = "From Year", minval = 1970)
 
toDay = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2100, title = "To Year", minval = 1970)

startDate = timestamp("America/New_York", fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp("America/New_York", toYear, toMonth, toDay, 00, 00)
time_condition = time >= startDate and time <= finishDate

//ORDER DETAILS
Risk = (high[7] - low[7])/ 7
Profit = Risk*1.15
Loss = Risk*0.65

AlertMSG = "New stategy position" + tostring(strategy.position_size)

if (time_condition) 
    strategy.entry("Long", strategy.long, when = LongFilter, alert_message=AlertMSG)
    if (LongFilter)
        LongStop = strategy.position_avg_price - Loss
        LongProfit = strategy.position_avg_price + Profit 
        strategy.exit("TP/SL", "Long", stop=LongStop, limit=LongProfit)

if (time_condition)
    strategy.entry("Short", strategy.short, when = ShortFilter, alert_message=AlertMSG)
    if (ShortFilter)
        ShortStop = strategy.position_avg_price + Loss
        ShortProfit = strategy.position_avg_price - Profit 
        strategy.exit("TP/SL", "Short", stop=ShortStop, limit=ShortProfit)



```

> Detail

https://www.fmz.com/strategy/429086

> Last Modified

2023-10-12 17:38:39
