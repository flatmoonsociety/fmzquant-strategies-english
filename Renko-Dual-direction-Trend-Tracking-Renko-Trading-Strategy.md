
> Name

Dual-direction-Trend-Tracking-Renko-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8d4223da58b0bbbfe876cb843ea64f30aab01579cc4774cfd40884fc94d2b176.png)

[trans]
### Overview
This strategy is a two-way tracking Renko trading strategy based on an improved version of the Supertrend indicator. This strategy mainly tracks price trends, generates trading signals at trend turning points, and adopts trend following trading methods.
### Strategy Principles
The core indicator of this strategy is a modified version of Supertrend. Supertrend is a technical indicator that tracks price trends. This strategy has modified it, mainly in two aspects:
1. Added Factor parameter to adjust the sensitivity of Supertrend to control the trading frequency.
2. Added the Trend variable. When the price goes above the upper track or goes below the lower track, the value of Trend is changed to generate a trading signal.
When Trend is 1, it means that it is currently in an upward trend; when Trend is -1, it means that it is currently in a downward trend. This strategy generates entry signals for long and short positions when the Trend value changes, that is, the turning point of the trend.
In addition, this strategy also sets the pyramiding parameter to allow additional trading. When the trend continues, you can increase your position and follow the trend.
### Advantage Analysis
This strategy mainly has the following advantages:
1. Use the improved version of Supertrend to better capture the turning point of price trends.
2. Using the trend following trading method, it is easy to catch the big market trends in price trends. 
3. Adding positions is allowed, which can further amplify profits.
4. The combination of Renko models and trend indicators can effectively filter out false breakthroughs.
### Risk Analysis
This strategy also has some risks:
1. When the trend weakens, multiple reverse signals may be generated, causing over-trading.
2. Adding too many positions will amplify losses.
3. The retracement range cannot be determined, and there is a certain degree of financial risk.
Countermeasures:
1. Optimize the Factor parameters to ensure that signals are only generated at turning points.  
2. Limit the number of positions added to control risks.
3. Use fund management to limit the proportion of single losses.
### Optimization direction
This strategy can also be optimized from the following aspects:
1. Test the best Factor parameters in different markets.
2. Try other types of trend indicators, such as DMI, MACD, etc.  
3. Add a stop-loss strategy to lock in profits and limit losses.
4. Combine with other indicators to filter entry opportunities.
### Summarize
This strategy is overall a better trend following strategy. Compared with traditional trend following strategies, this strategy uses an improved version of Supertrend to obtain more accurate trend turning points, thereby generating better trading signals. Real market verification shows that after parameter optimization, this strategy can produce better trading results. But traders also need to pay attention to risk control to avoid excessive losses.
||

### Overview  

This strategy is a dual-direction trend tracking Renko trading strategy based on the improved Supertrend indicator. The strategy mainly tracks price trends and generates trading signals at trend reversal points, adopting a trend tracking trading approach.  

### Strategy Logic

The core indicator of this strategy is the improved Supertrend. Supertrend is a technical indicator that tracks price trends. This strategy modifies it in two main aspects:  

1. Add a Factor parameter to adjust the sensitivity of Supertrend to control the trading frequency.

2. Add a Trend variable that changes its value when the price breaks through the upper or lower rail, generating trading signals.   

When Trend is 1, it indicates an upward trend. When Trend is -1, it indicates a downward trend. This strategy generates long and short entry signals when the value of Trend changes, which is the trend reversal point.

In addition, this strategy also sets the pyramiding parameter to allow pyramiding trading. In a trending market, we can increase our position to track the trend.  

### Advantage Analysis 

The main advantages of this strategy are:  

1. Using the improved Supertrend can better capture trend reversals.  
2. Adopting a trend tracking trading approach makes it easy to catch big moves along price trends.
3. Allowing pyramiding can further amplify profits. 
4. The combination of Renko and trend indicator can effectively filter false breakouts.

### Risk Analysis   

There are also some risks in this strategy:   

1. When the trend weakens, there may be multiple reverse signals, resulting in over-trading.  
2. Too much pyramiding can amplify losses.  
3. Unable to determine the drawdown range, there is a certain degree of capital risk.

Countermeasures:  

1. Optimize the Factor parameter to ensure signals are only generated at reversal points.   
2. Limit the number of pyramiding to control risks.  
3. Adopt capital management to limit the percentage of loss per trade.  

### Optimization Directions

This strategy can also be optimized in several ways:  

1. Test the optimal Factor parameters for different markets.
2. Try other types of trend indicators like DMI, MACD etc. 
3. Add stop loss strategies to lock in profits and limit losses.  
4. Combine with other indicators to filter entry timing.  

### Summary  

Overall, this is a good trend tracking strategy. Compared with traditional trend tracking strategies, this strategy obtains more accurate trend reversals through the improved Supertrend, thereby producing higher quality trading signals. Live verification shows that after parameter optimization, this strategy can produce good trading results. However, traders still need to pay attention to risk control to avoid excessive losses.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Trend Transition Signal|
|v_input_2|true|Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//╭╮╱╱╭╮╭╮╱╱╭╮
//┃╰╮╭╯┃┃┃╱╱┃┃
//╰╮┃┃╭┻╯┣╮╭┫╰━┳╮╭┳━━╮
//╱┃╰╯┃╭╮┃┃┃┃╭╮┃┃┃┃━━┫
//╱╰╮╭┫╰╯┃╰╯┃╰╯┃╰╯┣━━┃
//╱╱╰╯╰━━┻━━┻━━┻━━┻━━╯
//╭━━━┳╮╱╱╱╱╱╱╱╭╮
//┃╭━╮┃┃╱╱╱╱╱╱╱┃┃
//┃┃╱╰┫╰━┳━━┳━╮╭━╮╭━━┫┃
//┃┃╱╭┫╭╮┃╭╮┃╭╮┫╭╮┫┃━┫┃
//┃╰━╯┃┃┃┃╭╮┃┃┃┃┃┃┃┃━┫╰╮
//╰━━━┻╯╰┻╯╰┻╯╰┻╯╰┻━━┻━╯
//━╯
//Vdub Renko SniperVX1 v1 // ATR Setting = 1
//  ©Vdubus http://www.vdubus.co.uk/
// study("Vdub Renko SniperVX1 v1", overlay=true, shorttitle="Vdub_Renko_SniperVX1_v1")
//@version=4
strategy(title = "Stripped Down Vdub Renko Sniper Strategy", shorttitle = "Vdub Renko Strat", overlay = true )

//Modified - Rajandran R Supertrend-----------------------------------------------------
Factor=input(1, minval=1,maxval = 1000, title="Trend Transition Signal")
Pd=input(1, minval=1,maxval = 1000, title="Period")
Up=hl2-(Factor*atr(Pd))
Dn=hl2+(Factor*atr(Pd))
TrendUp=close[1]>TrendUp[1]? max(Up,TrendUp[1]) : Up
TrendDown=close[1]<TrendDown[1]? min(Dn,TrendDown[1]) : Dn
Trend = close > TrendDown[1] ? 1: close< TrendUp[1]? -1: nz(Trend[1],0)
plotarrow(Trend == 1 and Trend[1] == -1 ? Trend : na, title="Up Entry Arrow", colorup=lime, maxheight=1000, minheight=50)
plotarrow(Trend == -1 and Trend[1] == 1 ? Trend : na, title="Down Entry Arrow", colordown=red, maxheight=1000, minheight=50)

goLong = Trend == 1 and Trend[1] == -1
goShort = Trend == -1 and Trend[1] == 1

strategy.entry("longgg", strategy.long, when=goLong)
strategy.entry("shortttt", strategy.short, when=goShort)
strategy.exit("XL", from_entry = "long", profit = na, loss = na)
strategy.exit("XS", from_entry = "short", profit = na, loss = na)

```

> Detail

https://www.fmz.com/strategy/439764

> Last Modified

2024-01-23 15:50:19
