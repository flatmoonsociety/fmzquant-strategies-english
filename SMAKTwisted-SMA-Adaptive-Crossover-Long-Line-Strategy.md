
> Name

Twisted-SMA-Adaptive-Crossover-Long-Line-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](assets/images/6c7d5fdff4cc5961628086415f5f39dd25a88413b8e7f9485980d2e7aa443ae1.png)
[trans]

## Overview
This strategy uses a combination of three simple moving averages (SMA) with different periods and the Kaufman adaptive moving average to form a long-term entry signal. A buy signal is generated when the short-period SMA crosses above the longer-period SMA. In addition, the strategy also combines the color of the K-line entity to determine the main trend, and only generates buy signals in the bull trend to avoid false breakthroughs.
## Strategy Principle
This strategy uses 3 SMAs with different periods, including SMA 4, SMA 9 and SMA 18. The cross combination of these three SMAs is a classic technical indicator for judging the direction of the trend. When SMA 4 crosses above SMA 9, and SMA 9 crosses above SMA 18, a long-term buy signal is generated.
In order to filter out false breakthroughs, this strategy also introduces the Kaufman adaptive moving average. Only when the closing price is higher than the adaptive moving average, that is, in a bullish trend, the SMA's golden cross signal will take effect to start the long-term trend.
In addition, this strategy also uses the 100-period SMA to determine the main trend. When the price crosses above the 100-period SMA, a bullish trend is confirmed. The strategy generates buy signals only during the main bull trend.
To sum up, the buy signal of this strategy comes from a combination of the following parts:
1. SMA 4 crosses above SMA 9, and SMA 9 crosses above SMA 18, forming a golden cross of short-period SMA.
2. The closing price is higher than the Kaufman adaptive moving average and is in a bullish trend.
3. The price crosses the 100-period SMA, confirming the main bull position
When the above three conditions are met at the same time, a long-term buy signal is generated.
## Advantage Analysis
This strategy has the following advantages:
1. Using 3-fold SMA cross to judge the trend can effectively filter the noise and improve the reliability of the signal.
2. Introduce adaptive moving averages to avoid false breakthroughs when there is no clear trend
3. Combined with the judgment of the main trend, increase the probability of profit and avoid repeatedly opening positions in volatile market conditions
4. The long and short period SMA crosses to form a long-term signal, which is conducive to capturing the larger trend market.
5. Suitable for high cycle timing, such as 4-hour or daily level, the signal is more reliable
## Risk Analysis
This strategy also has some risks:
1. Long-term strategy cannot stop losses in a short period of time, and there is a certain risk of retracement.
2. Entry signals are relatively rare and you may miss part of the gains.
3. Signal errors will occur when short-term, mid-term and long-term trends are inconsistent.
It can be optimized in the following ways:
1. Appropriately shorten the period of medium and long-term SMA to increase entry opportunities
2. Add other auxiliary indicators, such as trading volume indicators, to confirm the reliability of the trend
3. Adopt scientific stop loss and reasonably control drawdowns
## Optimization direction
There is room for further optimization of this strategy:
1. You can test more combinations of SMA cycles and find optimal parameters
2. You can add confirmation of trading volume to avoid false breakthroughs
3. You can add a volatility indicator to filter entry in scenarios where volatility increases.
4. Machine learning algorithms can be introduced to adaptively find optimal parameters.
5. Sentiment indicators can be introduced to avoid opening positions when the market is panic or excited.
## Summarize
This strategy forms long-term signals through multiple SMA crossovers, and combines adaptive moving averages and main trend judgment to obtain greater profits in trending markets. It has stable logic and strong practical effects. But there are also certain risks, and optimization needs to continue to reduce retracement and improve the winning rate. This strategy is a long-term holding strategy and is suitable for investors with patience and risk control capabilities.
|| 

## Overview  

This strategy generates long-term entry signals by combining 3 simple moving averages (SMA) of different periods with the Kaufman adaptive moving average. It produces buy signals when the shorter period SMA crosses over the longer period SMAs. In addition, the strategy also incorporates candlestick color to determine the main trend, generating buy signals only during uptrends to avoid false breakouts.  

## Strategy Logic

The strategy utilizes 3 SMAs of different periods, including SMA 4, SMA 9, and SMA 18. The crossover combinations of these 3 SMAs are classic indicators for judging trend direction. When SMA 4 crosses over SMA 9, and SMA 9 crosses over SMA 18, it produces long entry signals.

To filter out false breakouts, the Kaufman adaptive moving average is also introduced. Only when the close price is higher than the adaptive moving average, i.e. in an uptrend, will the SMA golden cross signals take effect to trigger long positions.  

In addition, a 100-period SMA is used to determine the main trend. When prices cross above the 100-period SMA, it confirms that an uptrend has begun. The strategy only produces buy signals during main uptrends.

In summary, the long entry signals of this strategy come from the combination of:

1. SMA 4 crosses over SMA 9, and SMA 9 crosses over SMA 18, forming short-term SMA golden crosses

2. Close price is higher than the Kaufman adaptive moving average, in an uptrend  

3. Prices cross above the 100-period SMA, confirming a main uptrend

When all 3 conditions are met at the same time, long entry signals are generated.

## Advantage Analysis 

The main advantages of this strategy include:  

1. Using triple SMA crosses to determine trends can effectively filter out noise and increase signal reliability  

2. Introducing adaptive moving average avoids false breakouts when there is no clear trend

3. Incorporating main trend judgment increases profit probability by avoiding repeatedly opening positions during range-bound movements  

4. Long-term and short-term SMA crosses form long line signals, which captures big trending moves  

5. Suitable for high periodicity timing such as 4-hour or daily levels, with more reliable signals

## Risk Analysis

There are also some risks with this strategy:  

1. As a long-line strategy, unable to realize profits in a timely manner, with certain drawdown risks

2. Relatively few entry signals, may miss some run-ups

3. Conflicting short-term, medium-term and long-term trends may generate erroneous signals

The following optimization methods can be adopted:

1. Appropriately reduce medium and long term SMA periods to increase entry opportunities  

2. Add other auxiliary indicators like volume to confirm trend reliability   

3. Employ prudent stops to reasonably control drawdowns

## Optimization Directions

There is further room for optimizing this strategy:

1. Test more SMA combination periods to find optimum parameters  

2. Incorporate volume confirmation to avoid false breakouts 

3. Add volatility indicators to filter entries during violent swings

4. Introduce machine learning algorithms to adaptively identify optimal parameters  

5. Add sentiment indicators to avoid taking positions during market panic or euphoria

## Conclusion  

This strategy forms long-line signals through multiple SMA crosses, combined with adaptive moving averages and main trend determinations. It can capture significant profits during trending moves with stable logic and strong practical results. But there are also risks that need to be reduced through further optimizations. As a long-term position holding strategy, it suits investors with patience and risk control capabilities. 

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_4|100|  SMA Lenght|
|v_input_int_5|25|    Lenght|
|v_input_bool_1|true|  Self Powered|
|v_input_int_1|4|(?SMA)  1-SMA Lenght|
|v_input_int_2|9|  2-SMA Lenght|
|v_input_int_3|18|  3-SMA Lenght|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-17 00:00:00
end: 2023-11-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Wielkieef


//@version=5
strategy(title='twisted SMA strategy [4h] ', overlay=true, pyramiding=1, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, calc_on_order_fills=false, slippage=0, commission_type=strategy.commission.percent, commission_value=0.03)

src = close

Length1 = input.int(4, title='  1-SMA Lenght', minval=1, group='SMA')
Length2 = input.int(9, title='  2-SMA Lenght', minval=1, group='SMA')
Length3 = input.int(18, title='  3-SMA Lenght', minval=1, group='SMA')
SMA1 = ta.sma(close, Length1)
SMA2 = ta.sma(close, Length2)
SMA3 = ta.sma(close, Length3)

Long_ma = SMA1 > SMA2 and SMA2 > SMA3
Short_ma = SMA1 < SMA2 and SMA2 < SMA3

LengthMainSMA = input.int(100, title='  SMA Lenght', minval=1)

SMAas = ta.sma(src, LengthMainSMA)

//  Powered Kaufman Adaptive Moving Average by alexgrover (modificated by Wielkieef)
lengthas = input.int(25, title='    Lenght')
sp = input.bool(true, title='  Self Powered')

er = math.abs(ta.change(close, lengthas)) / math.sum(math.abs(ta.change(close)), lengthas)
pow = sp ? 1 / er : 2
per = math.pow(math.abs(ta.change(close, lengthas)) / math.sum(math.abs(ta.change(close)), lengthas), pow)
a = 0.
a := per * src + (1 - per) * nz(a[1], src)
mad4h = 0.
a_f = a / a[1] > .999 and a / a[1] < 1.001

///.

Bar_color = close > SMAas ? color.green : Long_ma ? color.blue : Short_ma ? color.maroon : color.gray

barcolor(color=Bar_color)

long_cond = Long_ma and SMAas < close and not a_f
  
long_stop = Short_ma 

if  long_cond
    strategy.entry('BUY', strategy.long)

strategy.close_all(when=long_stop)

//by wielkieef
```

> Detail

https://www.fmz.com/strategy/433101

> Last Modified

2023-11-24 14:26:37
