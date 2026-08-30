
> Name

Dual-Timeframe-Supertrend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a dual time frame super trend following strategy. It uses two super-trend indicators of different periods at the same time, one as the main time frame to determine the trend direction, and the other as the auxiliary time frame to filter entry. Only enter the market when the super-trend indicators of the two time frames are in the same direction, so as to capture the trend turning point more accurately.
## Strategy Principle
The core indicator of this strategy is the supertrend indicator. Supertrend indicators determine the direction of price relative to the trend by calculating price dispersion. The strategy uses the supertrend indicator of two time periods to calculate the supertrend lines of the main time frame and the auxiliary time frame respectively.
The specific transaction logic is:
1. Determine the direction of the main time frame above the trend line as the general trend direction.
2. Wait for the auxiliary time frame to cross the trend line and send out a signal in the same direction to enter the market.
3. Set stop loss and take profit points.
4. Close the position when the main time frame exceeds the trend line and turns again.
In this way, by combining two period indicators, some divergence signals can be filtered out, making entry more accurate.
## Advantage Analysis
This strategy has the following advantages:
1. Dual time frame combination can judge the trend more accurately.
2. Super-trend indicators are sensitive to trend changes and can enter the market accurately.
3. Set stop-loss and stop-profit points to control risks.
4. The strategy logic is simple, direct and easy to understand.
5. Parameters can be optimized by oneself to adapt to different varieties.
## Risk Analysis
The main risks of this strategy are:
1. Supertrend indicators may lag behind and may misjudge signals.
2. Improper setting of stop loss and profit may lead to excessive pursuit of gains or deliberate stop loss.
3. The dual time frame combination may miss shorter reversal opportunities.
4. Parameter optimization relies on historical data, and there is a risk of over-fitting.
5. Failure to consider the impact of transaction costs.
Corresponding solutions:
1. Appropriately adjust indicator parameters and introduce other indicator combinations for verification.
2. Dynamically optimize stop loss and take profit positions based on backtest data.
3. Test shorter periods as auxiliary judgment.
4. Expand the scope of data backtesting and verify multi-market backtesting.
5. Add handling fees, slippage and other transaction cost calculations.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Test the combined effect of more indicators and find the optimal combination.
2. Introduce machine learning methods to dynamically optimize parameters.
3. Optimize the stop-loss and take-profit strategy and improve the profit-loss ratio.
4. Try the combination effects of various time periods.
5. Adjust the stop-profit and stop-loss ranges based on the number of transactions.
6. Add calculation logic for handling fees and slippage.
7. Develop graphical parameter optimization tools.
## Summarize
This strategy achieves more accurate trend judgment and entries through dual time frame super trend indicators. Set stop loss and take profit to control risks. The strategy logic is simple and clear, and easy to expand and optimize. In the later period, improvements can be made by introducing more indicators, dynamically optimizing parameters, and adding transaction cost calculations to make the strategy more robust. Overall, this strategy provides a dual-time frame trend tracking idea and has a very good reference value.
||


## Overview

This is a dual timeframe Supertrend tracking strategy. It applies Supertrend indicators in two different time periods, one as the main timeframe to determine the trend direction, and one as the auxiliary timeframe to filter entries. It only enters when the Supertrends in both timeframes are in the same direction, to more accurately capture trend reversal points.

## Strategy Logic

The core indicator of this strategy is Supertrend. Supertrend determines the relative trend direction of prices by calculating price volatility. The strategy uses Supertrend in two time periods, calculating the Supertrend lines for the main and auxiliary timeframes respectively. 

The specific trading logic is:

1. Use the direction of the main timeframe Supertrend as the overall trend direction.

2. Enter when the auxiliary timeframe Supertrend issues a signal in the same direction.

3. Set stop loss and take profit points. 

4. Exit when the main timeframe Supertrend turns again.

By combining two timeframe indicators, some divergences can be filtered for more precise entry.

## Advantage Analysis

The advantages of this strategy include:

1. Dual timeframe combination allows more accurate trend judgment.

2. Supertrend is sensitive to trend changes, with accurate entry.

3. Stop loss and take profit controls risk.

4. Simple and direct strategy logic, easy to understand.

5. Parameters can be customized for different products.

## Risk Analysis

The main risks are:

1. Supertrend lagging may cause misjudged signals.

2. Improper stop loss and take profit may cause over-chasing trends or premature stop loss.

3. Dual timeframe may miss some shorter reversals. 

4. Parameter optimization relies on historical data, risks of overfitting exist.

5. No consideration of transaction costs.

The solutions are:

1. Adjust indicators parameters, add other indicators for combo verification.

2. Dynamically optimize stop loss and take profit based on backtest results.

3. Test shorter timeframes as auxiliary judgement. 

4. Expand backtest data range, multi-market backtest verification. 

5. Add transaction costs like commission and slippage.

## Optimization Directions

The strategy can be further optimized by:

1. Testing more indicator combinations to find optimal combo.

2. Using machine learning to dynamically optimize parameters.

3. Optimizing stop loss and take profit for better risk-reward ratios.

4. Trying combo of more timeframes.

5. Adjusting take profit and stop loss ranges based on number of trades.

6. Adding commission and slippage logic. 

7. Developing graphical parameter optimization tools.

## Conclusion

This strategy achieves relatively accurate trend judgment and entries by using dual timeframe Supertrend indicators. It controls risks by setting stop loss and take profit. The strategy logic is simple and clear, easy to expand and optimize. It can be further improved by introducing more indicators, dynamically optimizing parameters, adding transaction costs etc to make it more robust. Overall, this strategy provides a useful dual timeframe trend tracking idea that holds good reference value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|120|Main SuperTrend Time Frame|
|v_input_2|true|Factor|
|v_input_3|true|Pd|
|v_input_4|500|Take Profit|
|v_input_5|400|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-22 00:00:00
end: 2023-09-21 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Supertrend Strategy by breizh29 using *rajandran.r* Supertrend Indicator

// strategy("Super Trend 2", overlay=true, default_qty_value=100)
TrendUp = 0.0
TrendDown = 0.0
Trend = 0.0
MTrendUp = 0.0
MTrendDown = 0.0
MTrend = 0.0

res = input(title="Main SuperTrend Time Frame",  defval="120")
Factor=input(1, minval=1,maxval = 100)
Pd=input(1, minval=1,maxval = 100)

tp = input(500,title="Take Profit")
sl = input(400,title="Stop Loss")


Up=hl2-(Factor*atr(Pd))
Dn=hl2+(Factor*atr(Pd))
MUp=security(syminfo.tickerid,res,hl2-(Factor*atr(Pd)))
MDn=security(syminfo.tickerid,res,hl2+(Factor*atr(Pd)))

Mclose=security(syminfo.tickerid,res,close)

TrendUp:=close[1]>TrendUp[1]? max(Up,TrendUp[1]) : Up
TrendDown:=close[1]<TrendDown[1]? min(Dn,TrendDown[1]) : Dn

MTrendUp:=Mclose[1]>MTrendUp[1]? max(MUp,MTrendUp[1]) : MUp
MTrendDown:=Mclose[1]<MTrendDown[1]? min(MDn,MTrendDown[1]) : MDn

Trend := close > TrendDown[1] ? 1: close< TrendUp[1]? -1: nz(Trend[1],1)
Tsl = Trend==1? TrendUp: TrendDown

MTrend := Mclose > MTrendDown[1] ? 1: Mclose< MTrendUp[1]? -1: nz(MTrend[1],1)
MTsl = MTrend==1? MTrendUp: MTrendDown

linecolor = Trend == 1 ? green : red
plot(Tsl, color = linecolor , style = line , linewidth = 2,title = "SuperTrend")

Mlinecolor = MTrend == 1 ? blue : orange
plot(MTsl, color = Mlinecolor , style = line , linewidth = 2,title = "Main SuperTrend")

plotshape(cross(close,Tsl) and close>Tsl , "Up Arrow", shape.triangleup,location.belowbar,green,0,0)
plotshape(cross(Tsl,close) and close<Tsl , "Down Arrow", shape.triangledown , location.abovebar, red,0,0)

up = Trend == 1 and Trend[1] == -1 and MTrend == 1 
down = Trend == -1 and Trend[1] == 1 and MTrend == -1 
plotarrow(up ? Trend : na, title="Up Entry Arrow", colorup=lime, maxheight=60, minheight=50, transp=0)
plotarrow(down ? Trend : na, title="Down Entry Arrow", colordown=red, maxheight=60, minheight=50, transp=0)


golong = Trend == 1 and Trend[1] == -1 and MTrend == 1 
goshort = Trend == -1 and Trend[1] == 1 and MTrend == -1 

strategy.entry("Buy", strategy.long,when=golong)
strategy.exit("Close Buy","Buy",profit=tp,loss=sl)
   
   
strategy.entry("Sell", strategy.short,when=goshort)
strategy.exit("Close Sell","Sell",profit=tp,loss=sl)


```

> Detail

https://www.fmz.com/strategy/427591

> Last Modified

2023-09-22 14:27:52
