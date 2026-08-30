
> Name

Moving-Average-Envelopes-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/cf7ccd8c88904d00cd512bc2ced2ba2a269749fd8462a45c0026e53bdb44c165.png)
[trans]

## Overview
The Momentum Moving Average Envelope Trading Strategy is a trend following strategy. It sets the moving average and the upper and lower percentage ranges as buy and sell signals. Trading signals are generated when price breaks out of an upward or downward range. This strategy can be used both for trend following and for identifying overbought and oversold market conditions.
## Strategy Principle
The strategy is based on a simple moving average of length 14. The upward percentage interval is calculated as: moving average + moving average × entered percentage value. The downward percentage range is calculated as: Moving Average - Moving Average × the entered percentage value. This forms an upper and lower parallel trading range.
When the closing price is greater than the upward range, go long; when the closing price is less than the downward range, go short. Otherwise keep the short position. Input parameter "reverse" can achieve reverse operation.
This strategy uses 3 indicators:
1. xSMA - a 14-period simple moving average, representing the midline.
2. xHighBand - Upward percentage range.
3. xLowBand - Downward percentage band.
## Strategic Advantages
This strategy has the following advantages:
1. The rules are clear and easy to understand and implement.
2. Can be used for trend tracking and identification of overbought and oversold. Avoid losing direction in volatile market conditions.
3. By adjusting the percentage interval parameters, the trading frequency can be controlled. Reduce transaction risk.
4. The moving average period can be flexibly selected, suitable for different periods and market varieties.
5. Reverse input parameters increase strategy flexibility. You can operate with the trend or against the trend.
## Risks and Solutions
There are also some risks with this strategy:
1. In a strong trend, there may be a deep rise or fall beyond the range. Resulting in missing out on some profits. Risk can be controlled by reducing the percentage range.
2. In volatile market conditions, frequent erroneous trading signals may occur. The signal can be filtered by increasing the moving average period.
3. When the range is small, the price may frequently touch the upper and lower ranges. Excessive trading frequency increases transaction costs and slippage losses. The range can be appropriately expanded.
4. Rapidly changing emergencies may cause strategy losses. It is recommended to combine stop loss to manage risk.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Test moving averages with periods of different lengths and select the period parameters that produce the best signal.
2. Optimize the upper and lower percentage interval parameters to find the combination parameters that maximize profits and control risks.
3. Add other technical indicators as filters to avoid false signals in volatile and complex markets. For example, MACD, KD, etc.
4. Improve entry timing by combining trend judgment indicators. For example ADX, interrupt, etc.
5. Test the effectiveness of parameters of different varieties. Adjust parameters to suit different trading varieties.
6. Combine with stop-loss strategy to limit the risk of single loss.
## Summarize
The momentum moving average envelope trading strategy is generally a typical trend following strategy. Its parameters are simple to set, easy to understand and backtest. It can also be used to determine complex market conditions of overbought and oversold. Through parameter optimization and indicator combination, the actual effect of the strategy can be greatly improved. This strategy deserves further research and application.
||

## Overview  

The Moving Average Envelopes trading strategy is a trend following strategy. It sets up percentage envelopes above and below a moving average line as trading signals when price breaks out the envelopes. The strategy can be used for both trend following and identifying overbought/oversold market conditions.

## Strategy Logic

The strategy is based on a 14-period simple moving average (SMA). The upper envelope is calculated as: SMA + SMA × input percentage. The lower envelope is calculated as: SMA - SMA × input percentage. This forms up and down trading bands parallel to the SMA. 

When close price goes above the upper band, a long position is taken. When close price goes below the lower band, a short position is taken. Otherwise, maintain a flat position. The input parameter "reverse" allows reverse trading.

The strategy uses 3 indicators:  

1. xSMA - 14-period simple moving average, the midline.  

2. xHighBand - Upper percentage envelope.

3. xLowBand - Lower percentage envelope.

## Advantages  

The advantages of this strategy include:

1. Simple logic, easy to understand and implement.  

2. Can be used for both trend following and identifying overbought/oversold levels. Avoids missing trends in rangy markets.

3. Trade frequency can be controlled by adjusting the percentage envelopes parameters. Lowers trading risk.  

4. Flexibility in choosing moving average periods for different timeframes and instruments.

5. The reverse input parameter adds flexibility. Can trade with or against the trend.

## Risks and Solutions

There are some risks to the strategy:

1. Deep pullbacks beyond the envelope range can happen in strong trends, missing some profits. Can lower percentage parameters to control risk.

2. Frequent false signals may occur in choppy/ranging markets. Can increase moving average period to filter signals. 

3. Too narrow envelopes may trigger excessive whipsaws. Can wisely widen envelope range.

4. Sudden volatility from news events can cause losses. Using stop loss helps manage risk.

## Optimization  

The strategy can be optimized:  

1. Test moving averages of different periods and find optimal parameters with best signals.

2. Optimize percentage envelopes for maximum profitability and controllable risk.  

3. Adding filters like MACD and KD to avoid bad signals in choppy/complex market conditions.

4. Combine with trend strength indicators like ADX to improve entry timing. 

5. Test effectiveness across different instruments. Customize parameters per product.

6. Incorporate stop loss strategy to limit downside risk per trade.

## Conclusion  

Overall this is a typical trend following strategy with easy backtesting parameters. It can also identify overbought/oversold levels. Further parameter optimization and combination with other indicators can significantly improve its practical effectiveness for trading. This is a valuable strategy worthy of further research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|PercentShift|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-25 00:00:00
end: 2023-12-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 04/03/2018
// Moving Average Envelopes are percentage-based envelopes set above and 
// below a moving average. The moving average, which forms the base for 
// this indicator, can be a simple or exponential moving average. Each 
// envelope is then set the same percentage above or below the moving average. 
// This creates parallel bands that follow price action. With a moving average 
// as the base, Moving Average Envelopes can be used as a trend following indicator. 
// However, this indicator is not limited to just trend following. The envelopes 
// can also be used to identify overbought and oversold levels when the trend is 
// relatively flat. 
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Moving Average Envelopes", overlay = true)
Length = input(14, minval=1)
PercentShift = input(1, minval = 0.01, step = 0.01)
reverse = input(false, title="Trade reverse")
xSMA = sma(close, Length)
xHighBand = xSMA + (xSMA * PercentShift / 100)
xLowBand = xSMA - (xSMA * PercentShift / 100)
pos = iff(close > xHighBand, 1,
       iff(close <xLowBand, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(xSMA, color=blue, title="SMA")
plot(xHighBand, color=red, title="High Band")
plot(xLowBand, color=red, title="Low Band")
```

> Detail

https://www.fmz.com/strategy/436647

> Last Modified

2023-12-26 15:55:43
