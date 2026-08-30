
> Name

RSI Divergence Reversal Strategy RSI-Divergence-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is a reversal strategy based on the RSI indicator. It calculates two RSI curves with different periods, and performs buying or selling operations when a golden cross or dead cross occurs in the two RSI curves.
### Strategy Principles
1. Calculate two RSI curves: a short-period RSI curve and a long-period RSI curve.
2. When the short-period RSI crosses the long-period RSI, it is judged as a bullish signal and goes long.
3. When the short-period RSI falls below the long-period RSI, it is judged as a bearish signal and goes short.
4. When issuing a buy signal, set the stop loss price to the latest price.
5. When issuing a sell signal, set the stop loss price to the latest price.
6. If the price hits the stop loss price, the stop loss will exit the current position.
### Advantage Analysis
1. Using the RSI indicator to determine the trend reversal point has certain reliability.
2. The double RSI curve combination can filter out some noise trading signals.
3. Set a stop loss to control losses on each position.
4. The strategy logic is simple, intuitive and easy to implement.
5. RSI parameters can be customized and suitable for different market environments.
### Risk Analysis
1. The RSI indicator lags behind and may miss the reversal point of a sudden trend.
2. Improper stop loss setting may cause unnecessary losses.
3. The double RSI combination still cannot completely avoid the risks caused by false breakthroughs.
- Risk 1 can be combined with other indicators such as Bollinger Bands to confirm a reversal.
- Risk 2 can use trailing stop loss or pending order stop loss to optimize the stop loss strategy.
- Risk 3 can add trend filter conditions to avoid false breakthroughs.
### Optimization direction
1. Test the effect of RSI cycle combinations of different parameters.
2. Evaluate the combination effect with other indicators such as MACD, KD, etc.
3. Add stop loss strategies such as trailing stop loss and pending order stop loss.
4. Add trend filtering to avoid reverse operations.
5. Evaluate the effect on different varieties and cycles.
### Summarize
This strategy implements simple reversal trades via RSI divergence crossover. Double RSI filtering and stop loss control risk. In the future, the effect can be further improved through multi-indicator combinations, optimized stop loss strategies, etc.
||

### Overview

This strategy is a reversal strategy based on the RSI indicator. It calculates two RSI lines with different lookback periods and enters long or short trades when the two RSI lines cross over.

### Strategy Logic

1. Calculate two RSI lines, one with shorter period and one with longer period.

2. When the shorter period RSI crosses above the longer period RSI, determine a bullish signal for going long.

3. When the shorter period RSI crosses below the longer period RSI, determine a bearish signal for going short.

4. When going long, set stop loss at the latest price.

5. When going short, set stop loss at the latest price. 

6. If price hits stop loss, exit the current position.

### Advantages

1. Using RSI to identify potential reversal points is reasonably reliable.

2. Dual RSI crossover filters out some false signals.

3. Stop loss controls risk for each position.

4. Simple and intuitive logic, easy to implement.

5. Customizable RSI parameters suit different markets.

### Risks

1. RSI lag may miss reversal timing of sudden trend changes. 

2. Improper stop loss setting may cause unnecessary losses.

3. Dual RSI cannot fully avoid false breakout risks.

- Risk 1 can be mitigated by combining indicators like Bollinger Bands.

- Risk 2 can be improved via trailing or pending order stops. 

- Risk 3 can be reduced by adding trend filters.

### Enhancement Opportunities 

1. Test effectiveness of different RSI period combinations.

2. Evaluate combining with indicators like MACD, KD etc.

3. Add stop loss techniques like trailing stops or pending orders.

4. Add trend filter to avoid trading reversals.

5. Assess performance across different products and timeframes.

### Conclusion

This strategy executes simple reversal trades using RSI divergences. Dual RSI and stops control risks. Further improvements can be made through combining indicators, optimizing stops and more.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|length1|
|v_input_2|100|length2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-18 00:00:00
end: 2023-09-17 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("RSI cross Strategy by alireza v1.1.1", overlay=true)
length1 = input( 25 )
length2 = input( 100 )
price = close


vrsi1 = ta.rsi(price, length1)
vrsi2 = ta.rsi(price, length2)

GC = (close > open)
RC = (open > close)

HH = (close > close[2])
LL = (close < close[2])




cu = ta.crossover(vrsi1, vrsi2)
cd = ta.crossunder(vrsi1, vrsi2)



if (not na(vrsi1))
	if (cu) 
	    sll=price
		strategy.entry("BUY", strategy.long )
		strategy.exit("SL" , limit = sll )
	if (cd)
	    sls=price
		strategy.entry("SELL", strategy.short )
		strategy.exit("SL" , limit = sls )


```

> Detail

https://www.fmz.com/strategy/427119

> Last Modified

2023-09-18 13:54:48
