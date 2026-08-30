
> Name

Quantitative Trading Strategy Detrended-Price-Oscillator-Quantitative-Trading-Strategy Based on Price Detrended Oscillator
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Overview
The name of this strategy is "Quantitative Trading Strategy Based on Price Detrended Oscillator" (Detrended Price Oscillator Quantitative Trading Strategy). This strategy builds a price detrending oscillator indicator and sends trading signals based on it, which is a typical technical indicator strategy.
## Strategy Principle
The core of this strategy is the Detrended Price Oscillator (DPO) indicator. The DPO indicator is similar to a moving average, which can filter out longer-period trends in prices, making cyclical fluctuations in prices more obvious. Specifically, the DPO indicator compares the price with its N-day simple moving average. When the price is higher than the moving average, DPO is positive; when the price is lower than the moving average, DPO is negative. In this way, an indicator is obtained that oscillates around the 0 axis. We can use the positive and negative of the DPO indicator to judge whether the price rises or falls relative to the trend.
This strategy sets the parameter N to 14 and constructs the 14-day DPO indicator. When the DPO indicator is positive, a long signal is issued; when the DPO indicator is negative, a short signal is issued.
## Strategic Advantages
- The DPO indicator is essentially a filter indicator that can effectively identify short- and medium-term cycles in prices. This is very helpful for discovering more hidden trading opportunities.
- The DPO indicator is simple to construct, easy to understand, and the parameter selection is also relatively flexible.
- Compared with the price itself, the shape of the DPO indicator is relatively standard, easy to judge, and suitable for formulating rules.
## Strategy Risk
- Like most technical indicator strategies, the DPO strategy is prone to generating multiple unnecessary trading signals. This can introduce unnecessary slippage and transaction costs.
- The DPO indicator is very sensitive to parameter N, and different parameter selections will lead to greatly different strategy effects. The optimal parameters must be found through extensive testing.
- In trending market conditions, the holding time of the DPO strategy may be too long, making it impossible to stop losses in time, and there is a certain risk of blood loss.
To reduce risks, the following aspects can be considered for optimization:
1. Add a stop-loss mechanism to control single losses.
2. Adjust the value of parameter N and find the optimal parameters.
3. Combine with trend indicators to avoid trading according to the original strategy despite a clear trend.
## Summarize
This strategy generates trading signals based on the price detrending oscillator indicator. By comparing with the moving average, this indicator filters out long-term trends in prices, making the cyclical characteristics of prices more obvious. This can help uncover some subtle trading opportunities. At the same time, there are also problems such as sensitive parameter selection, stop loss and filtering. Through continuous optimization, there is still much room for improvement in the effectiveness of this strategy.
||

## Strategy Overview

The strategy is named "Detrended Price Oscillator Quantitative Trading Strategy". It generates trading signals based on the Detrended Price Oscillator indicator, which is a typical technical indicator strategy.  

## Strategy Logic

The core of this strategy is the Detrended Price Oscillator (DPO) indicator. DPO is similar to moving average, which can filter out longer-term trends in prices to make cyclical fluctuations more pronounced. Specifically, DPO compares prices with their N-day simple moving average. When the price is above the moving average, DPO is positive; when the price is below the moving average, DPO is negative. This results in an oscillator fluctuating around the 0 axis. We can use the positive/negative of DPO to judge the rise/fall of prices relative to the trend.

This strategy sets the parameter N to 14 and constructs a 14-day DPO indicator. When DPO is positive, a long signal is issued. When DPO is negative, a short signal is issued.

## Advantages

- DPO is essentially a filtering indicator that can effectively identify medium-term cycles in prices. This is very helpful for discovering relatively concealed trading opportunities. 
- DPO has simple construction and is easy to understand. The parameter selection is also relatively flexible.
- Compared to the price itself, the DPO indicator pattern is more standardized and easier to judge, making it suitable for formulating rules.

## Risks

- Like most technical indicator strategies, the DPO strategy tends to generate unnecessary trading signals frequently. This may introduce unnecessary slippage and transaction costs.
- DPO is very sensitive to the parameter N. Different parameter selections can lead to very different strategy efficacy. Extensive testing is needed to find the optimal parameter.
- In trending markets, the holding period of DPO strategies may be too long to stop loss in time, posing some risk of blood loss.

To mitigate risks, optimization can be considered in the following aspects:

1. Add stop loss mechanisms to control single loss.

2. Adjust the value of parameter N to find the optimal parameter. 

3. Incorporate trend indicators to avoid trading against significant trends.

## Conclusion  

This strategy generates trading signals based on the Detrended Price Oscillator indicator. By comparing with moving averages, this indicator filters out long-term trends in prices to make price cyclic characteristics more pronounced. This helps to discover some concealed trading opportunities. At the same time, it also faces problems like parameter sensitivity, filtering, etc. There is still large room for efficacy improvement through continuous optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|close|Price|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-16 00:00:00
end: 2023-11-20 08:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 31/03/2017
// The Detrend Price Osc indicator is similar to a moving average, 
// in that it filters out trends in prices to more easily identify 
// cycles. The indicator is an attempt to define cycles in a trend 
// by drawing a moving average as a horizontal straight line and 
// placing prices along the line according to their relation to a 
// moving average. It provides a means of identifying underlying 
// cycles not apparent when the moving average is viewed within a 
// price chart. Cycles of a longer duration than the Length (number 
// of bars used to calculate the Detrend Price Osc) are effectively 
// filtered or removed by the oscillator.
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="Detrended Price Oscillator", shorttitle="DPO")
Length = input(14, minval=1)
Series = input(title="Price",  defval="close")
reverse = input(false, title="Trade reverse")
hline(0, color=green, linestyle=line)
xPrice = close
xsma = sma(xPrice, Length)
nRes = xPrice - xsma
pos = iff(nRes > 0, 1,
	     iff(nRes < 0, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=red, title="Detrended Price Oscillator")
```

> Detail

https://www.fmz.com/strategy/433079

> Last Modified

2023-11-24 11:22:30
