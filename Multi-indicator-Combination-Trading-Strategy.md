
> Name

Multi-indicator-Combination-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1c0fcffbdd5befe089c.png)

[trans]


### Overview
This strategy uses a combination of three indicators, CCI, ADX, and AO, to achieve long and short judgments and generate trading signals. Among them, CCI is used to determine whether the market is overbought and oversold, ADX is used to determine the trend direction, and AO is used to assist in determining whether the market is volatile. A combination of multiple indicators can improve the stability and efficiency of the trading system.
### Strategy Principles
1. The CCI indicator is used to determine whether the market is overbought or oversold. When the CCI is below -100, it is oversold, and when it is above 100, it is overbought. This strategy goes long when CCI is less than 0.
2. The ADX indicator determines the strength of the trend. DI+ represents the strength of an upward trend, and DI- represents the strength of a downward trend. ADX represents average trend strength. This strategy goes long when DI+ is below 25.
3. The AO indicator determines long and short kinetic energy. AO consists of the fast SMA minus the slow SMA. An increase in AO represents the current strength of bulls, and a decrease in AO represents the strength of shorts. This strategy goes long when AO is below 0.
4. Combining the above multiple indicators, the trading strategy is formed as follows: go long when CCI < 0 and DI+ < 25 and AO < 0; close the position when DI+ > 25.
5. The order quantity is dynamically calculated by dividing the account equity by the close price and rounding to the next round, so that the order quantity can be adjusted as the account equity changes.
6. Use strategy.entry to send a long signal and strategy.close to send a closing signal.
### Advantage Analysis
1. Using CCI to determine overbought and oversold conditions can effectively filter out false signals caused by volatile market conditions.
2. The ADX indicator determines the existence and strength of the trend and can capture strong trend signals.
3. The AO indicator can help determine the heat and momentum of the trend and avoid trading in volatile markets.
4. Multiple indicator combinations can mutually verify signals, enhance signal reliability, and effectively reduce false signals.
5. Dynamically calculate the order quantity and adjust the position size according to changes in account equity, so you have a strong sense of fund management.
6. The strategy logic is clear and simple, easy to understand and track.
### Risk Analysis
1. The CCI indicator has a weak ability to identify vsdk's volatile market and may produce false signals.
2. The ADX indicator has hysteresis and may miss the turning point of the trend.
3. The AO indicator is not effective in judging twists and turns.
4. Although multiple indicator combinations can improve signal reliability, improper indicator settings may also cause excessive filtering and miss trading opportunities.
5. DYNAMICAOR is related to market volatility, and parameters need to be adjusted according to different varieties and market environments.
6. The strategy drawdown may be large, and strict fund management is required to control risks.
### Optimization direction
1. Optimize CCI parameters to identify overbought and oversold areas in different markets.
2. Optimize ADX parameters to capture trend transitions under different varieties and market environments.
3. Adjust AO parameters to identify the real trend under different fluctuation environments.
4. Test different indicator weight combinations to find optimal parameters.
5. Add a stop-loss strategy to control drawdowns.
6. Combine with volume indicators to avoid false breakouts.
7. Adjust fixed positions according to the characteristics of different varieties.
### Summarize
This strategy uses the combination of three indicators, CCI, ADX and AO, to form a more reliable long signal. At the same time, combined with dynamic calculation of order quantity and position management, risks can be effectively controlled. The strategic ideas are simple and clear, easy to understand, and suitable for beginners to follow and learn. However, this strategy has a weak ability to identify volatile market conditions, and there is still a lot of room for optimization. It needs further testing and adjustment to adapt to different varieties and market environments.
||

### Overview

This strategy combines CCI, ADX and AO indicators to generate trading signals for long and short positions. CCI identifies overbought and oversold levels, ADX determines trend strength and direction, and AO assists in oscillating markets. The multi-indicator combination improves the stability and efficiency of the trading system.

### Strategy Logic

1. CCI indicates overbought above 100 and oversold below -100. This strategy goes long when CCI is below 0.

2. ADX measures trend strength. DI+ shows uptrend strength, DI- shows downtrend strength. ADX is the average trend strength. This strategy goes long when DI+ is below 25.

3. AO is fast SMA minus slow SMA. Rising AO represents strengthening bullish momentum, and falling AO represents strengthening bearish momentum. This strategy goes long when AO is below 0.

4. The trading rules are: Go long when CCI < 0 and DI+ < 25 and AO < 0; Close long when DI+ > 25. 

5. Dynamically calculate order size as equity divided by close price and rounded down, to adjust orders as account equity changes.

6. Use strategy.entry for long signals, and strategy.close for exit signals.

### Advantages

1. CCI filters noise from ranging markets, reducing false signals.

2. ADX identifies stronger trends early.

3. AO avoids trading choppy markets. 

4. Multiple indicators verify signals, increasing reliability.

5. Dynamic position sizing manages risk effectively.

6. Simple and clear logic, easy to follow.

### Risks

1. CCI struggles identifying vkosd ranges.

2. ADX has lag in catching trend turns. 

3. AO struggles with choppy consolidation. 

4. Poor indicator settings lead to over-filtering and missed trades.

5. Dynamic sizing dependent on volatility and markets.

6. Potential for large drawdowns, requiring strict risk management.

### Enhancements

1. Optimize CCI parameters for different markets.

2. Optimize ADX parameters to catch trend changes.

3. Adjust AO parameters for volatility environments. 

4. Test combinations to find optimal indicator weighting.

5. Add stop loss for drawdown control.

6. Incorporate volume for false breakout avoidance. 

7. Customize fixed position sizing by instrument.

### Conclusion

This strategy combines CCI, ADX and AO to generate fairly reliable long signals. Dynamic sizing and position management control risk. The logic is simple and clear for beginners to follow. But it struggles in ranging markets, with significant optimization potential required for different markets. Further testing and tuning is needed for robustness across instruments and environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|buywhenadxabove|
|v_input_2|10|buywhendiplusbelow|
|v_input_3|false|buywhenccibelow|
|v_input_4|false|buywhenawesomeoscillatorbelow|
|v_input_5|25|sellwhendiplusabove|
|v_input_6|20|numberofbarsforcci|
|v_input_7|14|ADX Smoothing|
|v_input_8|14|DI Length|
|v_input_9|34|Length Slow|
|v_input_10|5|Length Fast|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-19 00:00:00
end: 2023-10-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Strategy Niel", shorttitle="Strategy Niel", max_bars_back=2000, initial_capital=1000)

//Input variables
buywhenadxabove = input(25)
buywhendiplusbelow = input(10)
buywhenccibelow = input(0)
buywhenawesomeoscillatorbelow = input(0)
sellwhendiplusabove = input(25)

//CCI script
numberofbarsforcci = input(20)
CCI = cci(close,numberofbarsforcci)

//+DI and ADX
adxlen = input(14, title="ADX Smoothing")
dilen = input(14, title="DI Length")
dirmov(len) =>
	up = change(high)
	down = -change(low)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(up > down and up > 0 ? up : 0, len) / truerange)
	minus = fixnan(100 * rma(down > up and down > 0 ? down : 0, len) / truerange)
	[plus, minus]

adx(dilen, adxlen) => 
	[plus, minus] = dirmov(dilen)
	sum = plus + minus
	adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
	[adx, plus, minus]

[sig, up, down] = adx(dilen, adxlen)

//plot(sig, color=red, title="ADX")
//plot(up, color=blue, title="+DI")
//plot(down, color=orange, title="-DI")


//Awesome Oscillator
nLengthSlow = input(34, minval=1, title="Length Slow")
nLengthFast = input(5, minval=1, title="Length Fast")
xSMA1_hl2 = sma(hl2, nLengthFast)
xSMA2_hl2 = sma(hl2, nLengthSlow)
xSMA1_SMA2 = xSMA1_hl2 - xSMA2_hl2
cClr = xSMA1_SMA2 > xSMA1_SMA2[1] ? blue : red
//plot(xSMA1_SMA2, style=histogram, linewidth=1, color=cClr)

buy = sig > buywhenadxabove and up < buywhendiplusbelow  and CCI < buywhenccibelow and xSMA1_SMA2 < buywhenawesomeoscillatorbelow 

ordersize=floor(strategy.equity/close) // Floor returns largest integer, strategy.equity gives total equity remaining - allows to dynamically calculate the order size as the account equity increases or decreases.
strategy.entry("long",strategy.long,ordersize,when= buy) //strategy.entry let's you enter the market variables id ("long"), strategy.long (long position entry), size of the order and when the order should happen
bought = strategy.position_size[0] > strategy.position_size[1]
entry_price = valuewhen(bought, open, 0)
sell = up > sellwhendiplusabove 
strategy.close("long", when=sell ) //strategy.close let's you close your position with variables id ('long') and when this should happen



```

> Detail

https://www.fmz.com/strategy/430245

> Last Modified

2023-10-26 15:22:28
