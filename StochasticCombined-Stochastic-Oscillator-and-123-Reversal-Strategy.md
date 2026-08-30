
> Name

Combined-Stochastic-Oscillator-and-123-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/277ed2a3df5c22f082bb070106dccffd49dd80e55b30e8ba2749abbe62aeef92.png)

[trans]

### Overview
This strategy combines the 123 bottom reversal and the Stochastic indicator to generate a buy signal when the stock price bottoms out and the Stochastic indicator also bottoms out. This strategy can effectively identify the bottom of stock price reversal, and dual indicator filtering can reduce trading frequency and improve signal accuracy.
### Strategy Principles
1. 123 bottom reversal strategy
- A buy signal is generated if the closing price is higher than the closing price of the previous two days and the fast line of the 9-day Stochastic indicator is below the slow line and the fast line is below 50
- If the closing price is lower than the closing price of the previous two days and the fast line of the 9-day Stochastic indicator is above the slow line and the fast line is above 50, a sell signal is generated
2. Stochastic indicator strategy
- If the Stochastic fast line goes above the rails (default 20), a buy signal is generated
- If the Stochastic fast line crosses the lower rail (default 80), a sell signal is generated
3. Dual signal filtering
Only when the 123 reversal strategy and the Stochastic strategy generate buy signals at the same time will the final buy signal be generated, and the same is true for sell signals. This can effectively filter out some error signals and improve signal quality.
### Strategic Advantages
1. Double indicator confirmation can filter out a lot of noise and improve the accuracy of the signal.
2. The 123 reversal strategy can capture the bottom and top of price reversals. Stochastic indicator confirmation helps avoid false breakouts.
3. The Stochastic indicator can effectively identify overbought and oversold areas and perfectly cooperates with the 123 reversal strategy.
4. There is a large space for parameter optimization, and better strategic effects can be obtained by adjusting parameters.
5. The strategy logic is simple and clear, easy to understand and implement, and is suitable for beginners to learn quantitative trading.
### Strategy Risk
1. Double filtering signals may miss some opportunities and reduce trading frequency.
2. Stochastic indicators are prone to produce false signals, so you need to be cautious in judging the actual trend of the indicators.
3. Parameters need to be optimized. Improper parameter settings will also affect the strategy effect.
4. Only applicable to markets with obvious reversal characteristics, not applicable to markets that continue to rise or fall.
5. It is necessary to strictly abide by the strategic signals and avoid deviations caused by self-judgment.
Risk resolution: Optimize parameter settings, strictly follow strategy signals, and timely adjust the market environment for which the strategy is applicable.
### Strategy optimization direction
1. Optimize the parameters of the Stochastic indicator and improve the stability of the indicator.
2. Add a stop-loss strategy to stop the loss and exit when the loss reaches a certain percentage.
3. Adding filtering conditions, such as confirmation of trading volume, can further improve signal quality.
4. Test the combined effects of different reversal strategies and the Stochastic indicator.
5. Add machine learning algorithms and use historical data to train and optimize parameters.
6. Apply the strategy to different markets and test cross-market stability.
7. Explore the combination of other technical indicators and Stochastic indicators to find better pairing solutions.
### Summarize
This strategy combines dual Stochastic indicators and the 123 reversal pattern to effectively capture bottom reversal opportunities. Compared with a single indicator, a combination of multiple indicators can significantly improve the quality and winning rate of signals. Although there is still some room for improvement, overall the strategy has simple logic and is easy to master, making it very suitable for beginners to practice real-time trading. Through repeated testing and optimization, the strategy parameters can be made more robust, thereby obtaining more sustained positive returns.
|| 


### Overview

This strategy combines the 123 reversal pattern and Stochastic oscillator to generate buy signals when the price shows bottom reversal and the Stochastic oscillator also reversed from the bottom. It can effectively identify bottom reversals and the double confirmation filters can reduce trading frequency and improve signal accuracy.

### Strategy Logic

1. 123 Reversal Strategy

    - Buy signal is generated if the closing price is higher than previous 2 days’ closing price, and 9-day Stochastic fast line is below slow line and below 50.

    - Sell signal is generated if the closing price is lower than previous 2 days’ closing price, and 9-day Stochastic fast line is above slow line and above 50.

2. Stochastic Oscillator Strategy 

    - Buy signal is generated if Stochastic %K line crossed above upper band (default 20).

    - Sell signal is generated if Stochastic %K line crossed below lower band (default 80).
    
3. Dual Confirmation

    Buy signal is only generated when both 123 reversal and Stochastic strategies give buy signal. Sell signal is similar. This dual confirmation can filter out false signals and improve accuracy.

### Advantages

1. Dual confirmation filters out noise and improves signal accuracy.

2. 123 reversal catches bottom and top reversals. Stochastic avoids false breakouts.

3. Stochastic identifies overbought and oversold effectively, great match with 123 reversal.

4. High optimization flexibility with parameters tuning.

5. Simple logic, easy to understand, good for beginners.

### Risks

1. Dual confirmation may miss some chances and reduce trading frequency.  

2. Stochastic may generate false signals, needs careful examination.

3. Proper parameter tuning is needed, improper settings affect performance.

4. Only works for markets with reversal pattern, not for persistent trends.

5. Strictly follow strategy signals, avoid biases from own judgement.

Risk Solutions: Optimize parameters, strictly follow signals, adjust applicable market condition.

### Optimization Directions 

1. Optimize Stochastic parameters for more stability.

2. Add stop loss strategy.

3. Add filters like volume confirmation to improve signal quality.

4. Test combinations of different reversal strategies and Stochastic.

5. Utilize machine learning to train and optimize parameters.

6. Apply strategy on different markets to test robustness.

7. Explore combinations with other indicators.

### Conclusion

This strategy combines Stochastic oscillator and 123 reversal pattern, which effectively catches bottom reversal opportunities. Compared to single indicator, the multi-indicator combination significantly improves signal quality and win rate. Although there is still room for improvement, the overall logic is simple and easy to grasp, making it ideal for beginner’s live trading practice. With repeated testing and optimization, the parameters can become more robust for consistent positive results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Stochastic ----|
|v_input_7|7|LengthS|
|v_input_8|3|DLengthS|
|v_input_9|20|UpBand|
|v_input_10|80|DownBand|
|v_input_11|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-25 00:00:00
end: 2023-10-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 07/07/2021
// This is combo strategies for get a cumulative signal. 
//
// First strategy
// This System was created from the Book "How I Tripled My Money In The 
// Futures Market" by Ulf Jensen, Page 183. This is reverse type of strategies.
// The strategy buys at market, if close price is higher than the previous close 
// during 2 days and the meaning of 9-days Stochastic Slow Oscillator is lower than 50. 
// The strategy sells at market, if close price is lower than the previous close price 
// during 2 days and the meaning of 9-days Stochastic Fast Oscillator is higher than 50.
//
// Second strategy
// This back testing strategy generates a long trade at the Open of the following 
// bar when the %K line crosses up UpBand line.
// It generates a short trade at the Open of the following bar when the %K line 
// crosses down DownBand line.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
Reversal123(Length, KSmoothing, DLength, Level) =>
    vFast = sma(stoch(close, high, low, Length), KSmoothing) 
    vSlow = sma(vFast, DLength)
    pos = 0.0
    pos := iff(close[2] < close[1] and close > close[1] and vFast < vSlow and vFast > Level, 1,
	         iff(close[2] > close[1] and close < close[1] and vFast > vSlow and vFast < Level, -1, nz(pos[1], 0))) 
	pos


Stochastic(Length,DLength,UpBand,DownBand) =>
    pos = 0.0
    vFast = stoch(close, high, low, Length)
    vSlow = sma(vFast, DLength)
    pos := iff(vFast > UpBand, 1,
	         iff(vFast < DownBand, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Stochastic", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Stochastic ----")
LengthS = input(7, minval=1)
DLengthS = input(3, minval=1)
UpBand = input(20, minval=1)
DownBand = input(80, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posStochastic = Stochastic(LengthS,DLengthS,UpBand,DownBand)
pos = iff(posReversal123 == 1 and posStochastic == 1 , 1,
	   iff(posReversal123 == -1 and posStochastic == -1, -1, 0)) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1 , 1, pos))	   
if (possig == 1 ) 
    strategy.entry("Long", strategy.long)
if (possig == -1 )
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? #b50404: possig == 1 ? #079605 : #0536b3 )
```

> Detail

https://www.fmz.com/strategy/430269

> Last Modified

2023-10-26 17:00:27
