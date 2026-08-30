
> Name

Digital currency trading strategy based on Stochastic-RSIStochastic-RSI-Strategy-for-Cryptocurrency-Trading
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/4e1d0ab0b7fd96aa09.png)
 [trans]

## 1. Strategy Overview
The name of this strategy is "Digital Currency Trading Strategy Based on Stochastic RSI". This strategy combines two indicators, the Relative Strength Index (RSI) and the Stochastic RSI, to identify buy and sell signals for digital currencies.
The main idea of ​​the strategy is: first calculate the RSI value, and then build the Stochastic RSI indicator based on RSI, that is, the K value and the D value. When the K value crosses above the D value, a buy signal is generated, and when the K value crosses below the D value, a sell signal is generated. To filter out false signals, the strategy also introduces the Rate of Change Index (RVI) and its smoothed moving average for confirmation.
## 2. Detailed principles of strategy
1. Calculate the RSI value of length 14.
2. Construct a Stochastic RSI indicator with a length of 14 based on RSI, and obtain the K value and D value (D is the 3-period moving average of K).
3. Calculate the RVI of length 5 and its signal line (i.e., the smoothed moving average of RVI).
4. When K crosses D above, if RVI > signal line and RVI in the previous period < signal line, a buy signal is generated; when K crosses below D, if RVI < signal line and RVI in the previous period > signal line, a sell signal is generated.
5. Carry out buy or sell position opening operations according to the generated signal.
## 3. Analysis of strategic advantages
1. Combined with Stochastic RSI and RVI double confirmation, false signals can be effectively filtered.
2. The RVI indicator can reflect overbought and oversold conditions in the short term and avoid opening positions at extreme points.
3. The Stochastic RSI indicator can identify overbought and oversold areas, and use the golden cross pattern of the KDJ indicator to determine the buying and selling points.
4. The backtest results show that this strategy has achieved good results on some digital currency trading pairs (such as FCT/BTC).
## 4. Strategic Risk Analysis
1. Similar to the trailing stop loss strategy, if the stop loss point is not set appropriately, you may get stuck.
2. The frequency of signal generation may be too high, and transaction fees are factors that need to be considered.
3. Both KDJ indicator and RVI indicator may produce false signals, leading to unnecessary losses.
4. Strategy parameters need to be optimized for different trading pairs, and their universality needs to be considered.
## 5. Strategy optimization direction
1. Add a trailing stop to lock in profits. You can refer to ATR to set the stop loss level.
2. Optimize RVI parameters and Stochastic RSI parameters to make the signal clearer.
3. Increase transaction volume control to avoid excessively large single orders.
4. Add a filtering mechanism to avoid opening positions at high positions. The volatility indicator can be introduced to determine whether it is currently in a state of shock.
5. Test different digital currency trading pairs to find the best fit.
## 6. Strategy summary
This strategy first uses the RSI indicator to construct the Stochastic RSI, and then combines the RVI indicator to confirm the signal to discover overbought and oversold phenomena in the short term, thereby opening a position at the reversal point. The advantage is that double confirmation can filter out false signals, but the disadvantage is that there may be a risk of parameter overfitting. Generally speaking, this strategy has achieved good results on some trading pairs, and through further optimization, more stable returns can be obtained.
|| 

## I. Strategy Overview  

This strategy is named "Stochastic RSI Strategy for Cryptocurrency Trading". It combines the Relative Strength Index (RSI) and Stochastic RSI indicators to identify buy and sell signals for cryptocurrencies.  

The main idea behind the strategy is: First calculate the RSI value, then construct the Stochastic RSI indicator based on RSI, namely the K and D values. When the K value crosses above the D value, a buy signal is generated. When the K value crosses below the D value, a sell signal is generated. To filter out false signals, the strategy also introduces the Rate of Change Index (RVI) and its moving average line for confirmation.

## II. Detailed Principles of the Strategy

1. Calculate the 14-period RSI value.  

2. Construct a 14-period Stochastic RSI indicator based on RSI to obtain K and D values (D is the 3-period moving average of K).

3. Calculate the 5-period RVI and its signal line (the moving average of RVI).   

4. When K crosses above D, if RVI > Signal Line and last period's RVI < Signal Line, a buy signal is generated. When K crosses below D, if RVI < Signal Line and last period's RVI > Signal Line, a sell signal is generated.

5. Open long or short positions based on the generated signals.  

## III. Advantage Analysis  

1. The combination of Stochastic RSI and dual confirmation from RVI can effectively filter out false signals.

2. The RVI indicator can reflect short-term overbought/oversold conditions and avoids opening positions at extreme points.

3. The Stochastic RSI indicator identifies overbought/oversold zones. It uses the golden/dead cross of the KDJ indicator to determine entry points.  

4. Backtest results show this strategy has achieved good performance on some cryptocurrency pairs (such as FCT/BTC).

## IV. Risk Analysis   

1. Improper stop loss placement of similar trailing stop strategies may lead to being stopped out prematurely. 

2. High signal frequency may lead to excessive trading fees that should be taken into consideration.  

3. Both the KDJ and RVI indicators may generate false signals, resulting in unnecessary losses.  

4. The strategy parameters need to be optimized for different trading pairs. General applicability needs to be evaluated.

## V. Optimization Directions  

1. Add a moving stop loss to lock in profits. The ATR can be referenced to set stop loss levels.

2. Optimize RVI Parameters and Stochastic RSI parameters for cleaner signals. 

3. Add trade size control to avoid excessively large single orders.  

4. Add filtering mechanisms to avoid opening positions at unfavorable levels. Volatility indicators can be introduced to determine if the market is currently in a choppy state.

5. Test on different cryptocurrency pairs to find the best fit.

## VI. Strategy Summary

This strategy first constructs a Stochastic RSI based on the RSI indicator, then uses the RVI indicator for confirmation, in order to detect short-term overbought/oversold conditions and open positions at turning points. The advantage is that dual confirmation can filter out false signals. The disadvantage is the risk of overfitting parameters. Overall, this strategy has achieved good results on some trading pairs. Further optimizations can obtain more consistent profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Length|
|v_input_2|3|smoothK|
|v_input_3|3|smoothD|
|v_input_4|14|lengthRSI|
|v_input_5|14|lengthStoch|
|v_input_6_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-08 00:00:00
end: 2023-12-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Stochastic RSI", shorttitle="Stoch RSI", overlay = true)
Per = input(5, title="Length", minval=1)
smoothK = input(3, minval=1)
smoothD = input(3, minval=1)
lengthRSI = input(14, minval=1)
lengthStoch = input(14, minval=1)
src = input(close, title="RSI Source")

rsi1 = rsi(src, lengthRSI)
K = sma(stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK)
D = sma(K, smoothD)


rvi = sum(swma(close-open), Per)/sum(swma(high-low),Per)
sig = swma(rvi)
//plot(rvi, color=green, title="RVI")
//plot(sig, color=red, title="Signal")

//plot(K,  title="K")
//plot(D,  title="D")
Dn = K <= D  and K > 70 and rvi <= sig  and rvi[1] >= sig[1]
Up= K >= D  and K < 30 and rvi >= sig  and rvi[1] <= sig[1]
ARROW =  Up - Dn
plotarrow(ARROW, title="Down Arrow",  colordown=red, transp=0, maxheight=10, minheight=10)
plotarrow(ARROW, title="Up Arrow", colorup=lime,  transp=0, maxheight=10, minheight=10)
long = crossover(Up, Dn)
short = crossunder(Up, Dn)
last_long = long ? time : nz(last_long[1])
last_short = short ? time : nz(last_short[1])
long_signal = crossover(last_long, last_short)
short_signal = crossover(last_short, last_long)

//plot(long_signal, "BUY", color=green)
//plot(short_signal, "SELL", color=red)
strategy.entry("BUY", strategy.long, when=long_signal)
strategy.entry("SELL", strategy.short, when=short_signal)

```

> Detail

https://www.fmz.com/strategy/435463

> Last Modified

2023-12-15 10:08:14
