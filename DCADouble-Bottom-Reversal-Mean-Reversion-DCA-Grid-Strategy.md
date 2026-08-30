
> Name

Double-Bottom-Reversal-Mean-Reversion-DCA-Grid-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1435b49f70c6d07d1c0.png)
[trans]
## Overview
The double bottom reversal moving average DCA grid strategy mainly uses moving average price reversal and DCA strategies to realize the gradual establishment of positions on the grid. It identifies reversal opportunities based on double bottom reversal patterns. Once the reversal pattern is triggered, use multiple orders with different prices and combine with DCA to establish a gradual grid position.
## Strategy Principle
This strategy first determines whether the K-line has two consecutive bottoms with equal closing prices, which is called a "double bottom." If a double bottom is detected, a price reversal opportunity is considered possible. At this time, the strategy will set multiple limit orders near the bottom, and the prices of these orders will be calculated based on ATR and volatility to form a grid range. This achieves the effect of DCA, allowing traders to gradually build positions at different price points after the reversal.
Specifically, first calculate the ATR indicator of the last 14 K lines through ta.atr, and then calculate the price volatility based on the last 5 K lines, which is the main parameter used to determine the grid interval. The grid range is divided into 4 price points, which are bottom price + volatility, bottom price + 0.75 times volatility, and so on. When the double bottom condition is triggered, set 4 limit orders at the corresponding price according to this calculation formula, with the quantity of each order being equal. Unfulfilled pending orders will be automatically canceled after the set number of candles.
In addition, the strategy will also set stop loss and take profit levels. The stop-loss price is the lowest price of the double bottom - the minimum tick level, and the take-profit price is the entry price + 5 times the ATR indicator. When the position is not 0, these two prices will be updated in real time.
## Advantage Analysis
This strategy has the following advantages:
1. Using double bottoms to determine the reversal point can effectively avoid false breakthroughs.
2. The DCA grid design allows traders to gradually build positions at different prices, reducing position costs.  
3. ATR and volatility parameters can dynamically adjust the grid and take-profit space to adapt to market changes.
4. The automatic stop-loss mechanism can effectively control single losses.
## Risk Analysis
The main risks are:
1. The price may not reverse and fall directly below the double bottom support level. At this time, the stop loss will be triggered, causing losses. The stop loss distance can be appropriately increased.
2. The DCA grid range is improperly set, and most orders cannot be completed. Different parameters can be tested to ensure the transaction rate.  
3. When the market fluctuates violently, take profit may be triggered frequently. Consider appropriately expanding the take-profit ratio.
## Optimization direction
This strategy can also be optimized from the following directions:
1. Increase trend judgment and only perform reversal operations in bullish trends to avoid missing the big trend.
2. Consider increasing the first order position and gradually reducing the subsequent grid positions to optimize the efficiency of capital use.
3. Test different parameter combinations to find the best parameters. Dynamic parameters can also be designed and adjusted in real time according to the market.
4. Machine learning can be integrated into advanced platforms to achieve automatic optimization of parameters.
## Summarize
The double bottom reversal moving average DCA grid strategy comprehensively uses multiple technical means such as price patterns, moving average indicators, and grid trading. It has the advantages of accurate judgment time, controllable costs, and protected retracements. There is still a lot of room for optimization of this strategy and it deserves in-depth research and application. If the parameters are adjusted properly, good results can be obtained in volatile market conditions.
||

## Overview  

The Double Bottom Reversal Mean Reversion DCA Grid strategy mainly applies the mean reversion price and DCA strategy to implement gradual position building. It determines reversal opportunities based on the double bottom reversal pattern. Once the reversal pattern is triggered, it uses multiple limit orders at different prices combined with DCA to establish gradual grid positions.

## Strategy Logic  

The strategy first checks if there are two consecutive closing prices equal to the bottom on the candlestick chart, which is called a "double bottom". If a double bottom is detected, it considers there may be a price reversal opportunity. At this point, the strategy will set multiple limit orders around the bottom price. The prices of these orders will be calculated based on ATR and volatility, forming a grid zone. This achieves the DCA effect and allows traders to gradually build positions at different prices after the reversal. 

Specifically, the ATR indicator over the recent 14 candlesticks is first obtained through ta.atr. Then the price volatility over the recent 5 candlesticks is calculated. They are the main parameters used to determine the grid zone. The grid contains 4 price levels - bottom price + volatility, bottom price + 0.75 * volatility, and so on. Once the double bottom condition triggers, 4 limit orders with equal size will be placed according to this formula. The unfilled orders will be cancelled after several candlesticks.   

In addition, the strategy also sets a stop loss price and a take profit price. The stop loss price is set to the lowest price of the double bottom minus one tick size, while the take profit price is set to the entry price plus 5 times the ATR. These two prices will update in real-time when the position size is greater than 0.

## Strengths  

The main advantages of this strategy are:

1. Using double bottom to determine reversal improves accuracy and avoids false breaks. 
2. The DCA grid allows traders to gradually build positions at different prices, lowering cost basis.   
3. Dynamic ATR and volatility parameters adjust grid and profit range based on market changes.  
4. Auto stop loss effectively controls per trade loss amount.

## Risk Analysis   

Major risks:  

1. Price may break through support without reversal, triggering stop loss and losses. Widen stop loss distance for protection.   
2. Improper DCA grid setting may lead to low fill rate. Test different parameters to ensure fill rate.
3. Frequent take profit with whipsaws in volatile market. Consider allowing wider take profit multiples. 

## Improvement Areas

Some areas that can be improved:

1. Add trend judgment, only trade reversals along the major trend to avoid losses.  
2. Consider larger size for first entry and smaller sizes for grid entries to optimize capital usage efficiency.   
3. Test different parameter combinations to find optimum parameters. Or design dynamic adjusting logics.
4. Integrate machine learning in advanced platform to achieve auto parameter optimization.  

## Summary   

The Double Bottom Reversal Mean Reversion DCA Grid Strategy consolidates price pattern, indicator techniques and grid trading. It has accurate timing, controllable cost basis and drawdown protection. Still has room for optimization and is worth researching. Properly configured, can achieve good results in range-bound markets. 
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|(?Strategy Settings)ATR length for taking profit|
|v_input_int_2|5|ATR multiplier|
|v_input_int_3|5|Volatility length|
|v_input_float_1|0.5|Volatility multiplier|
|v_input_int_4|4|How many candles to wait after placing orders grid?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-12 00:00:00
end: 2024-02-19 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © cherepanovvsb

//@version=5
strategy("Reversal (only long)", overlay=true, margin_long=1, margin_short=1,initial_capital=1000,commission_type = strategy.commission.percent,commission_value =0.1,currency='USD', process_orders_on_close=true)
plotshape(low == low[1], style=shape.triangleup, location=location.belowbar, color=color.blue, title="1 Setup")
plotshape(low == low[1] and low[1]==low[2], style=shape.triangleup, location=location.belowbar, color=color.red, title="Triple Setup")

ATRlenght   = input.int(title="ATR length for taking profit", defval=14, group="Strategy Settings")
rewardMultiplier= input.int(title="ATR multiplier", defval=5, group="Strategy Settings")
Volatility_length=input.int(title='Volatility length',defval=5,group="Strategy Settings")
Volatility_multiplier=input.float(title='Volatility multiplier',defval=0.5,step=0.1, group="Strategy Settings")
Candles_to_wait=input.int(title='How many candles to wait after placing orders grid?',defval=4,group="Strategy Settings")

// Get ATR
atr1 = ta.atr(ATRlenght)

//Get volatility values (not ATR) 
float result = 0
for i = 0 to Volatility_length
	result+=high[i]-low[i]
volatility=result*Volatility_multiplier/Volatility_length

//Validate entrance points
validlow =  low [2]== low[1] and not na(atr1) 
validlong = validlow and strategy.position_size == 0  and low[1]<low


// Calculate SL/TP
longStopPrice = low[1]-syminfo.mintick
longStopDistance = close - longStopPrice
longTargetPrice = close + (longStopDistance * rewardMultiplier)
strategy.initial_capital = 50000
//Assign all variables
var tradeStopPrice = 0.0
var tradeTargetPrice = 0.0
var point1=0.0
var point2=0.0
var point3=0.0
var point4=0.0
var contracts = int(strategy.initial_capital/close)/4
if validlong 
    tradeStopPrice := longStopPrice
    tradeTargetPrice := longTargetPrice
    point1:=low[1]+volatility
    point2:=low[1]+volatility*0.75
    point3:=low[1]+volatility*0.5
    point4:=low[1]+volatility*0.25

strategy.entry ("Long1", strategy.long,limit=point1,qty=contracts, when=validlong)
strategy.entry ("Long2", strategy.long,limit=point2,qty=contracts, when=validlong)
strategy.entry ("Long3", strategy.long,limit=point3,qty=contracts, when=validlong)
strategy.entry ("Long4", strategy.long,limit=point4,qty=contracts, when=validlong)

stopcondition = ta.barssince(validlong) == Candles_to_wait

strategy.cancel("Long1",when=stopcondition)
strategy.cancel("Long2",when=stopcondition)
strategy.cancel("Long3",when=stopcondition)
strategy.cancel("Long4",when=stopcondition)
    
strategy.exit(id="Long Exit", limit=tradeTargetPrice, stop=tradeStopPrice, when=strategy.position_size > 0)

plot(strategy.position_size != 0 or validlong ? tradeStopPrice : na, title="Trade Stop Price", color=color.red, style=plot.style_linebr, linewidth=3)
plot(strategy.position_size != 0 or validlong ? tradeTargetPrice : na, title="Trade Target Price", color=color.green, style=plot.style_linebr, linewidth=3)

plot(strategy.position_size != 0? point1 : na, title="Long1", color=color.green, style=plot.style_linebr, transp=0)
plot(strategy.position_size != 0? point2 : na, title="Long2", color=color.green, style=plot.style_linebr, transp=0)
plot(strategy.position_size != 0? point3 : na, title="Long3", color=color.green, style=plot.style_linebr, transp=0)
plot(strategy.position_size != 0? point4 : na, title="Long4", color=color.green, style=plot.style_linebr, transp=0)


```

> Detail

https://www.fmz.com/strategy/442205

> Last Modified

2024-02-20 11:09:33
