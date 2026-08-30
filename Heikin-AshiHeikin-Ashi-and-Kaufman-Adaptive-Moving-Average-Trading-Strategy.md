
> Name

Heikin-Ashi and Kaufman Adaptive Moving Average Trading StrategyHeikin-Ashi-and-Kaufman-Adaptive-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/97ae14f8a44c74a649ce959c31d8e7ce5b05cea05f023dc9c6285cae5b77f0fa.png)

[trans]

## Overview
The Heikin Ashi and Kaufman Adaptive Moving Average trading strategy (HLC3/Kaufman Strategy) is a quantitative trading strategy that combines the Heikin Ashi K-line and the Kaufman Adaptive Moving Average (KAMA). This strategy uses the Heikin Ashi K-line to determine the trading direction, and then uses the Kaufman adaptive moving average as an auxiliary indicator to filter trading signals.
## Strategy Principle
This strategy mainly consists of the following parts:
1. Calculate the opening price and closing price of Heikin Ashi. These prices reflect the middle price of the K-line entity and can filter out some noise.
2. Calculate the Kaufman Adaptive Moving Average (KAMA). KAMA can dynamically adjust its smoothness without causing too much lag when the market suddenly fluctuates significantly.
3. Compare the relationship between Heikin Ashi closing price and KAMA to determine buy and sell signals. When the closing price of Heikin Ashi crosses KAMA, a buy signal is generated; when the closing price of Heikin Ashi crosses KAMA, a sell signal is generated.
4. The ADX indicator can be added to determine the strength of the trend to avoid generating false signals in a volatile market.
## Advantage Analysis
The biggest advantage of this strategy is that it combines the double filtering of Heikin Ashi K-line and KAMA, which can greatly reduce noise trading and false signals. The specific advantages are as follows:
1. The Heikin Ashi K-line itself has a denoising function, thus filtering out some short-term fluctuations.  
2. KAMA is more sensitive than SMA and EMA and can effectively track large-level trend changes.  
3. Combining the dual filtering mechanism of Heikin Ashi and KAMA can reduce errors.  
4. The ADX indicator can be configured to determine the strength of the trend and avoid false signals.  
5. The trading signals are direct and clear, and the operation is simple and flexible.
## Risk Analysis
1. Wrong signals may occur in some volatile markets, and parameters should be adjusted appropriately to avoid this risk.  
2. Overly sensitive parameters will easily lead to chasing highs and falling, so the KAMA parameters should be relaxed appropriately.
3. In the long-term trend market, KAMA may lag behind price changes to a certain extent. This needs to be combined with the ADX indicator to determine trend stability.
## Optimization direction
1. Optimize Heikin Ashi closing price and KAMA parameters to find the best filtering conditions.  
2. Add trend judgment indicators such as ADX to ensure that trading signals are generated only when the trend is stable.   
3. Combine with other auxiliary indicators such as Boll line to set stop loss standards.  
4. Test the stability of parameters of different varieties and find the optimal parameter combination.
## Summarize
The Heikin Ashi and Kaufman adaptive moving average trading strategy is a dual-filtered trend following strategy. It combines the denoising function of Heikin Ashi K-line and KAMA's fast tracking of trend changes, which can effectively filter noise transactions and reduce false signals, and is suitable for tracking medium and long-term trends. This strategy can further enhance stability and profitability through parameter optimization, auxiliary indicator confirmation and other means.
||

## Overview

The Heikin Ashi and Kaufman Adaptive Moving Average Trading Strategy (HLC3/Kaufman Strategy) is a quantitative trading strategy that combines Heikin Ashi candles and Kaufman Adaptive Moving Average (KAMA). It uses Heikin Ashi candles to determine trading direction and KAMA as an auxiliary indicator for trade signal filtering.

## Strategy Logic   

The main components of this strategy are:

1. Calculate Heikin Ashi open and close prices. These prices reflect the middle price of candle bodies and can filter out some noise.

2. Calculate Kaufman Adaptive Moving Average (KAMA). KAMA can dynamically adjust its smoothness and will not lag too much during sharp market fluctuations.  

3. Compare the relationship between Heikin Ashi close and KAMA to determine buy and sell signals. When Heikin Ashi close crosses over KAMA, a buy signal is generated. When Heikin Ashi close crosses below KAMA, a sell signal is generated.

4. Add ADX indicator to judge the strength of the trend to avoid wrong signals in range-bound markets.

## Advantage Analysis 

The biggest advantage of this strategy is the dual filter of Heikin Ashi candles and KAMA, which can greatly reduce noisy trades and wrong signals. The specific advantages are:

1. Heikin Ashi candles themselves have noise reduction capabilities to filter out some short-term fluctuations.
2. KAMA is more sensitive than SMA and EMA and can effectively track trend changes at major levels.  
3. The combination of Heikin Ashi and KAMA dual filters can reduce errors.
4. ADX indicator can be configured to determine the strength of the trend to avoid wrong signals.   
5. Trading signals are direct and easy to operate flexibly.
  

## Risk Analysis

1. Wrong signals may occur in some ranging markets. Parameters should be adjusted accordingly to avoid this risk.
2. Overly sensitive parameters can easily chase peaks and kill bottoms. KAMA parameters should be relaxed properly.  
3. In long-term trending markets, KAMA may lag behind price changes to some extent. ADX should be combined to determine the stability of the trend.
  
## Optimization Directions   

1. Optimize Heikin Ashi close and KAMA parameters to find the best filtering conditions.
2. Add trend judging indicators such as ADX to ensure trading signals are generated only when the trend is stable.  
3. Combine other auxiliary indicators such as Bollinger Bands to set stop loss standards.
4. Test the stability of parameters on different products to find the optimal parameter combinations.

## Summary

The Heikin Ashi and Kaufman Adaptive Moving Average Trading Strategy is a dual filter trend tracking strategy. It combines the noise reduction capability of Heikin Ashi candles and KAMA's fast tracking of trend changes to effectively filter out noise trades and reduce wrong signals. It is suitable for tracking medium and long term trends. The strategy can be further enhanced in terms of stability and profitability through parameter optimization, confirmation by auxiliary indicators, etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|D|Hlc3 Time Frame|
|v_input_2|true|Hlc3 Shift|
|v_input_3|20|Slow EMA Period|
|v_input_4|5|Length|
|v_input_5_hlc3|0|xPrice: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_6|2.5|Fastend|
|v_input_7|20|Slowend|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
//Heikin/Kaufman   by Marco

strategy("HLC3/Kaufman Strategy ",shorttitle="HLC3/KAU",overlay=true)
res1 = input(title="Hlc3 Time Frame", defval="D")
test = input(1,"Hlc3 Shift")
sloma = input(20,"Slow EMA Period")

//Kaufman MA
Length = input(5, minval=1)
xPrice = input(hlc3)
xvnoise = abs(xPrice - xPrice[1])
Fastend = input(2.5,step=.5)
Slowend = input(20)
nfastend = 2/(Fastend + 1)
nslowend = 2/(Slowend + 1)
nsignal = abs(xPrice - xPrice[Length])
nnoise = sum(xvnoise, Length)
nefratio = iff(nnoise != 0, nsignal / nnoise, 0)
nsmooth = pow(nefratio * (nfastend - nslowend) + nslowend, 2) 
nAMA = nz(nAMA[1]) + nsmooth * (xPrice - nz(nAMA[1]))

//Heikin Ashi Open/Close Price
//ha_t = heikinashi(tickerid)
//ha_close = request.security(ha_t, period, nAMA)
//mha_close = request.security(ha_t, res1, hlc3)
bha_close = request.security(syminfo.ticker, timeframe.period, nAMA)
bmha_close = request.security(syminfo.ticker, res1, hlc3)

//Moving Average
//fma = ema(mha_close[test],1)
//sma = ema(ha_close,sloma)
//plot(fma,title="MA",color=black,linewidth=2,style=line)
//plot(sma,title="SMA",color=red,linewidth=2,style=line)
bfma = ema(bmha_close[test],1)
bsma = ema(bha_close,sloma)
plot(bfma,title="MA",color=black,linewidth=2,style=line)
plot(bsma,title="SMA",color=red,linewidth=2,style=line)
//Strategy
//golong =  crossover(fma,sma) 
//goshort =   crossunder(fma,sma)
golong =  crossover(bfma,bsma) 
goshort =   crossunder(bfma,bsma)
strategy.entry("Buy",strategy.long,when = golong)
strategy.entry("Sell",strategy.short,when = goshort)




```

> Detail

https://www.fmz.com/strategy/435897

> Last Modified

2023-12-19 15:51:30
