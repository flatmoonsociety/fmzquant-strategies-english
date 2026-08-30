
> Name

Dual-Entry-Position-Averaging-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c0f43fa16c566793398261e694d9dad8c640a4c4a5866a8fed7b8bf2188fa5d0.png)
[trans]

### Overview
This strategy adopts the method of double entry. After entering the first entry point, if the price does not reach the first profit-taking point, it will enter the market again at a higher price to achieve the effect of increasing the position. At the same time, the strategy uses the average price tracking stop loss method, updates the position of the stop loss line in real time, and sets the stop loss line to be above a certain percentage of the average entry price, thereby locking in profits and controlling risks.
### Strategy Principles
The strategy first determines whether the price is below the 200-day simple moving average. If so, it meets the entry conditions. The strategy enters the market between 14:29 and 15:00 every day, forming the first entry point. The strategy then draws the first Take Profit and Stop Loss lines.
If the price rises but does not reach the first take-profit target, enter the market again at a position 5% higher than the entry price at the first entry point to achieve the effect of adding a position. At this time, the strategy will update the position of the stop loss line and set it to 1.15 times the average entry price of the current position. A second take profit line is also drawn.
This strategy can lock in profits through two take-profit targets and trailing stop-loss, and at the same time obtain more profits by adding positions.
### Advantage Analysis
This strategy has several advantages:
1. By using double entry to increase positions, you can obtain higher returns without increasing risks.
2. Update the stop loss line position in real time and adopt the average price tracking stop loss method, which can well control risks and lock in profits.
3. Open a position in a downtrend and have certain ability to operate against the market.
4. Set the entry time and point reasonably to avoid being trapped.
5. The parameters are set reasonably, the take-profit and stop-loss points are tight enough, and the profit-risk ratio is high.
### Risk Analysis
There are also some risks with this strategy:
1. Double entry to increase positions may amplify losses. If both entry points are stopped in the end, the loss will increase.
2. If the stop loss point is set improperly and the risk cannot be effectively controlled, it may lead to losses that exceed the tolerance.
3. If the entry time is chosen improperly, it may lead to head-on entry and the probability of being trapped is greatly increased.
4. If the parameters are set improperly, the profit stop point is too far or the stop loss point is too close, it may lead to a decrease in profits.
These risks can be reduced and avoided through reasonable parameter optimization and strict risk control.
### Optimization direction
This strategy can also be optimized from the following directions:
1. Test different technical indicators as entry conditions to find better entry points.
2. Test and optimize the take-profit and stop-loss points to maximize the profit-risk ratio.
3. Test different methods of adding positions to determine the optimal adding multiple.
4. Add trend judgment rules to avoid entering against the trend.
5. Optimize the selection of entry time period to ensure that you will not enter the market head-on.
### Summarize
This strategy is generally very practical and has strong practical significance. The dual-entry method of adding positions can obtain higher returns while controlling risks. The average price trailing stop loss can lock in profits and control risks. Through reasonable parameter optimization and strict risk control, this strategy can achieve stable and sustained Alpha.
||


### Overview

This strategy adopts a dual entry approach. After the first entry, if the price does not reach the first take profit level, it will enter again at a higher price to achieve the effect of adding positions. At the same time, the strategy adopts a position averaging trailing stop loss method to update the stop loss line in real time and set it to a certain percentage above the average entry price to lock in profits and control risks.

### Strategy Logic  

The strategy first judges if the price is below the 200-day simple moving average. If yes, the entry criteria are met. The strategy enters between 14:29 and 15:00 every day to form the first entry. After that, the strategy will plot the first take profit and stop loss lines.   

If the price rises but does not reach the first take profit target, it will enter again at 5% above the first entry price to add positions. At this point, the strategy will update the stop loss line to 1.15 times the current average holding price. At the same time, the second take profit line will be plotted.

The strategy can lock in profits through two take profit targets and trailing stop loss, while obtaining more profits through adding positions.

### Advantage Analysis 

The strategy has the following advantages:

1. Adopting dual entry add-on method can obtain higher returns without increasing risks.

2. Real-time update of stop loss line position. The position averaging trailing stop loss method can effectively control risks and lock in profits.  

3. Opening positions in a downtrend, it has certain countertrend trading capability.  

4. Reasonable entry time and price levels avoid being trapped.

5. Reasonable parameter settings, tight take profit and stop loss levels mean high risk-reward ratio.

### Risk Analysis   

The strategy also has some risks:

1. The dual entry add-on method may amplify losses. If both entries finally hit stop loss, the loss would be greater.

2. If the stop loss level is set improperly, it may fail to effectively control risks and lead to unacceptable losses.  

3. If the entry time is chosen poorly, it may result in adverse entry and higher probability of being trapped.

4. Unreasonable parameter settings like take profit being too distant or stop loss being too close may reduce profits.
 
These risks could be reduced and avoided through reasonable parameter optimization and strict risk control.

### Optimization Directions   

The strategy can also be optimized in the following aspects:

1. Test different technical indicators as entry signals to find better entry points. 

2. Test and optimize take profit and stop loss levels to maximize risk-reward ratio.

3. Test different add-on methods to determine the optimal add-on multiples.  

4. Add trend judgment rules to avoid countertrend entries.

5. Optimize the selection of entry time periods to ensure no adverse entries.


### Conclusion  

Overall, this strategy is very practical and has strong practical significance. The dual entry add-on method can obtain higher returns while controlling risks. The position averaging trailing stop loss can lock in profits and control risks effectively. With reasonable parameter optimization and strict risk control, this strategy can achieve steady and consistent Alpha.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|1.15|Total Stop Loss|
|v_input_2|1.05|Enter Second trade @ what higher 5%?|
|v_input_3|0.95|First Trade Profit % Target|
|v_input_4|0.9|Second Trade Profit % Target|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-23 00:00:00
end: 2023-11-28 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//              @version=4
strategy("8 Whittle Down", "8 WD", 1, initial_capital=0)


//              DUAL ENTRIES
//              ADDS ON MORE SHARES IF THE PILOT TRADE DOES NOT REACH PROFIT TARGET
//              RED     LINE        == STOP LOSS LINE
//              GREEN   LINE        == PROFIT TARGET FOR THE 1ST TRADE
//              YELLOW  LINE        == ADD ON SHARES TO THE TRADE
//              WHITE   LINE        == PROFIT TARGET FOR THE 1ST & SECOND TRADE COMBINED


StopLossPerc        = input(1.15, "Total Stop Loss", step=0.01)


T2EntTrgPerc        = input(1.05, "Enter Second trade @ what higher 5%?", step=0.01)    //  BUY STOP LIMIT ONLY WHEN ONE TRADE IS ALREADY OPEN & AIMS TO BUY DOUBLE THE OWNED SHARES AT A HIGHER ENTRY PRICE // YELLOW LINE

T1ProfTrgPerc       = input(0.95, "First Trade Profit % Target", step=0.01)
T2ProfTrgPerc       = input(0.90, "Second Trade Profit % Target", step=0.01)


RiskRange           = close*(StopLossPerc)-1
Shares              = floor(1000*1000/RiskRange) / 3                                    //  SPLITS THE RISK OVER THREE TRADES

F1                  = close < sma(security(syminfo.tickerid, "D", close[2]), 200)       //  HIGH OF OLD DATA -- SO NO REPAINTING
F2                  = strategy.opentrades == 0
buyTime             = time(timeframe.period, "1429-1500")                               //  BUY AT THE END OF THE  DAY
 
 
StopLossLine        = strategy.position_avg_price * StopLossPerc
StopLossCol         = strategy.opentrades != 0 ? #FF0000 : na
plot(StopLossLine,  "StopLossLine", StopLossCol, 2)



strategy.cancel_all()                                                                   //  CANCELS ALL ORDERS: BECAUSE THE SYSTEM WILL ADD A BUY STOP LIMIT ORDER FOR ENTRY TWO



///==============   ENTRY 1   ==============   
if  F1 and buyTime and strategy.opentrades == 0
    strategy.entry("S1", false, qty=Shares)


T1Prof              = strategy.position_avg_price * T1ProfTrgPerc
plot(T1Prof,        "1st Profit Target", strategy.opentrades == 1 ? #00FF00 : na, 2)

strategy.exit("S1 Ex", "S1", limit=T1Prof, stop=StopLossLine )


///==============   ENTRY 2   ==============   
T2EntryTrg          = strategy.position_avg_price * T2EntTrgPerc // enters on higher target than 1st entry
plot(T2EntryTrg,    "ent2EntryTrg", strategy.opentrades == 1 ? color.yellow : na, 2)
    
    
if  strategy.opentrades == 1
    strategy.order("S2", false, stop=T2EntryTrg, limit= T2EntryTrg, qty=Shares * 2)     //  BUYS MORE SHARES

T2Prof              = strategy.position_avg_price * T2ProfTrgPerc
    
T2Col               = strategy.opentrades == 2 ? color.white : na
plot(T2Prof,        "2nd Profit Target", T2Col, 2)
    
    
strategy.exit("S2 Ex", "S2", limit=T2Prof, stop=StopLossLine )


```

> Detail

https://www.fmz.com/strategy/433898

> Last Modified

2023-12-01 13:33:48
