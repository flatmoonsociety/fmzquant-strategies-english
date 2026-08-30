
> Name

Ichimoku-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]  

## Strategy Principle
This strategy uses the Ichimoku Kinko Hyo for long trading. It comprehensively considers multiple factors in the balance sheet and goes long when conditions are met.
The specific transaction logic is:
1. Calculate conversion line, baseline line, leading line 1, and leading line 2
2. When the closing price is higher than the cloud layer, the cloud layer is upward, and the conversion line is higher than the baseline, consider going long.
3. Additionally, the delay lines should be above the clouds and price to ensure an upward trend
4. When all the above conditions are met, enter the market long
5. If the confirmation line falls back below the price or below the cloud, close the position
This strategy makes full use of multiple indicators of the Ichimoku Balance Sheet to confirm the trend, and uses the cloud layer as a dynamic stop loss level to effectively control risks.
## Strategic Advantages
- Ichimoku Balance Sheet combines multiple factors to determine trends
- Dynamic stop loss to lock in profits to the greatest extent
- The rules are simple, clear and easy to implement
## Strategy Risk
- Ichimoku balance meter is slow and may miss opportunities
- Need to set parameter period carefully
- Only go long, you may miss good short selling opportunities
## Summarize
This strategy utilizes the multi-indicator nature of the Ichimoku to determine the direction of the trend. Based on optimized parameters, it provides a simple set of long rules. However, its hysteresis and long-only limitations still need to be noted.

||

## Strategy Logic

This LONG-ONLY strategy uses the Ichimoku Kinko Hyo system for trades. It combines multiple Ichimoku factors to go long when criteria are met.

The trading logic is:

1. Calculate conversion, base line, leading spans 1 & 2

2. Consider long when close is above cloud and cloud is rising, with conversion above base line 

3. Additionally, lagging span must be above cloud and price for uptrend confirmation

4. When all criteria met, go long

5. If lagging span falls below price or cloud, close long

The strategy utilizes Ichimoku's indicators to confirm trend, with the cloud as dynamic stops for risk control. 

## Advantages

- Ichimoku synthesizes multiple factors for trend determination

- Dynamic stops to maximize profit locking

- Simple and clear rules for easy implementation

## Risks

- Ichimoku is slow and may miss opportunities 

- Careful optimization of lookback periods needed

- LONG only, so good short chances missed

## Summary

This strategy leverages Ichimoku's synthesis of indicators to define trend direction. With optimized parameters, it provides a simple long-only system. But limitations in lag and being LONG-only require caution.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Conversion Line Length|
|v_input_2|60|Base Line Length|
|v_input_3|120|Leading Span B Length|
|v_input_4|30|Displacement|
|v_input_5|true|Stoploss (% below cloud)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Ichimoku Cloud", shorttitle="Doubled Ichimoku", overlay=true, initial_capital=1000, default_qty_value=100, default_qty_type=strategy.percent_of_equity)
conversionPeriods = input(20, minval=1, title="Conversion Line Length")
basePeriods = input(60, minval=1, title="Base Line Length")
laggingSpan2Periods = input(120, minval=1, title="Leading Span B Length")
displacement = input(30, minval=1, title="Displacement")
Stoploss = input(1, minval=0.1, title="Stoploss (% below cloud)") 
donchian(len) => avg(lowest(len), highest(len))
conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)
plot(conversionLine, color=#2962FF, title="Conversion Line")
plot(baseLine, color=#B71C1C, title="Base Line")
plot(close, offset = -displacement + 1, color=#43A047, title="Lagging Span")

p1 = plot(leadLine1, offset = displacement - 1, color=#A5D6A7,
	 title="Leading Span A")
p2 = plot(leadLine2, offset = displacement - 1, color=#EF9A9A,
	 title="Leading Span B")
fill(p1, p2, color = leadLine1 > leadLine2 ? color.rgb(67, 160, 71, 90) : color.rgb(244, 67, 54, 90))

bool TKcross = conversionLine > baseLine
bool aboveCloud = close > leadLine1 and close > leadLine2
bool greenCloud = leadLine1 > leadLine2
bool lagLong = close > leadLine1[2*displacement+1] and close > leadLine2[2*displacement+1] and close > close[displacement]
bool longCondition = false
bool close_trade = crossover(leadLine1[displacement], close) or crossover (leadLine2[displacement], close) or close < close[displacement] or crossover(baseLine, close)
var position_count = 0 

if (TKcross and aboveCloud and greenCloud and lagLong and position_count==0)
    position_count = 1
    strategy.entry(id="buy", long=true)

if (close_trade)
    strategy.close_all()
   // strategy.entry(id="sell", long=false)
    position_count = 0

    
//if (longCondition)
   
//    strategy.close("long", when=exit_trade)
//    strategy.exit("exit","long",stop=stop_level,limit=profit_level)
```

> Detail

https://www.fmz.com/strategy/426797

> Last Modified

2023-09-14 16:13:33
