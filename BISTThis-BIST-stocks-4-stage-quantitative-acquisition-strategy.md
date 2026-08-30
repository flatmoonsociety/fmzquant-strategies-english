
> Name

This-BIST-stocks-4-stage-quantitative-acquisition-strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18866ba73b6dadc76fa.png)
 [trans]

## Overview
The four-stage BIST stock quantitative acquisition strategy is a strategy that uses four-stage buying fluctuation tracking to buy in areas where the market is in consolidation and sell in areas where buying is increasing. This strategy is suitable for stocks with large fluctuations and achieves better cost control by buying in batches.
## Strategy Principle
The strategy first calculates resistance and support lines. The resistance line is determined by the intersection of the high price oscillating moving average and the closing price, and the support line is determined by the intersection of the closing price and the low price oscillating moving average.
When the price falls below the support line, if the price is within the set buying range from the resistance line, 25% of the position will be purchased in the first stage. Afterwards, another 25% position is purchased near the first-stage purchase price, and this cycle is repeated 4 times, and finally a 100% position is achieved.
When the stock price exceeds twice the opening cost, all positions will be closed and exited.
## Strategic Advantages
1. Buy in four installments to reduce purchase costs
2. Track stock fluctuations to achieve better entry points
3. Reasonable profit stop points to achieve better returns
## Risks and Solutions
1. The stock price continues to fall and the loss cannot be stopped, which may lead to large losses.
- Set stop loss lines reasonably to effectively control losses
2. Improper parameter setting, multiple buying points are too close to achieve cost dispersion effect
- Reasonably set the price gap between buying phases
3. The stop loss point is set too large and the loss cannot be effectively controlled.
- Set an appropriate stop loss distance based on the real trading environment and psychological endurance
## Strategy optimization direction
1. Adjust parameters according to different types of stocks to make the buying area more consistent with the characteristics of the stock.
2. Add a volatility indicator to buy when volatility increases
3. Optimize the take-profit method and change it to tracking take-profit to achieve higher returns
4. Add a stop loss line setting to stop losses when the price breaks through a certain level downwards
## Summarize
The four-stage BIST stock quantitative acquisition strategy is generally a strategy that is very suitable for popular concept stocks. By opening positions in batches, you can effectively take advantage of the volatility of the stock and obtain better costs when the price falls. At the same time, reasonable take-profit and stop-loss settings also make this strategy perform better in controlling risks. If the parameters are continuously adjusted and optimized according to the real market environment, I believe this strategy can achieve stable Alpha.

|| 

This BIST stocks 4-stage quantitative acquisition strategy is based on a four-stage buying to track the wave movements. It enters the market during post-manipulation and sells when buyer demand increases. This strategy is suitable for stocks with large fluctuations, and achieves better cost control through stage-by-stage purchases.

## Strategy Principles

This strategy first calculates the resistance and support lines. The resistance line is determined by the intersection of the close price and the oscillating moving average of the high price, while the support line is determined by the intersection of the close price and the oscillating moving average of the low price. 

When the price breaks below the support line, if the price is within the set buying range from the resistance line, it will buy in 25% of the position in the first stage. Then it will buy another 25% of the position around the first buy price, and so on for 4 times, eventually holding 100% of the position.

When the stock price exceeds twice the opening cost, it will close out all positions.

## Advantages of the Strategy

1. Lower buying costs through four-stage purchases 
2. Better entry points by tracking stock fluctuations
3. Reasonable take profit point for decent returns

## Risks and Solutions

1. Continued stock decline without stop loss, leading to large losses

    - Set reasonable stop loss to effectively control losses

2. Improper parameter settings make multiple buy points too close to diversify costs

    - Set appropriate price differences between buying stages  

3. Stop loss point too wide to effectively control losses

    - Set suitable stop distance based on actual trading environment and psychological tolerance

## Optimization Directions   

1. Adjust parameters for different types of stocks to better fit their characteristics

2. Add volatility indicators to buy when volatility rises  

3. Optimize take profit by using trailing stop to achieve higher returns  

4. Add stop loss settings to cut losses when price breaks certain levels

## Summary  

The BIST stocks 4-stage quantitative acquisition strategy is well suited for popular concept stocks overall. By staging the purchases, it can effectively utilize the volatility of the stocks to get better costs when prices pull back. Also, the reasonable take profit and stop loss settings allow it to perform well in risk control. With continual parameter adjustments and optimizations based on actual market environments, this strategy can reliably deliver alpha.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|Alım_Üst_Çizgi|
|v_input_2|90|Alım_Alt_Çizgi|
|v_input_3|true|Barcolor|
|v_input_4|true|Bgcolor|
|v_input_5|40|Satım_Üst_Çizgi|
|v_input_6|300|Satım_Alt_Çizgi|
|v_input_7|true|Barcolor2|
|v_input_8|true|Bgcolor2|
|v_input_9|25|Alış Aralığı %|
|v_input_10|45|Satış aralığı %|
|v_input_11|0.12|ALIM YERİ %|
|v_input_12|long entry message|message_long_entry|
|v_input_13|long exit message|message_long_exit|
|v_input_14|2|PROFİT SATIŞ SEVİYESİ|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Cantalk

//@version=5
strategy("BİST_100 HİSSELERİ 1_SAAT 4 KADEME ALIM",overlay = true, pyramiding=4, initial_capital=10000, process_orders_on_close=true, commission_type=strategy.commission.percent, commission_value=0.002)



LB2 = input(30, title="Alım_Üst_Çizgi")
LB = input(90, title="Alım_Alt_Çizgi")
Barcolor=input(true,title="Barcolor")
Bgcolor=input(true,title="Bgcolor")
//////////////////////////////////////////////////////////////////////

//////////////////////////////////////////////////////////////////////////////////////
RDirenc = ta.valuewhen(ta.cross(ta.hma(close, LB2), close), ta.highest(high, LB2), 1)
SDestek = ta.valuewhen(ta.cross(close, ta.hma(close, LB)), ta.lowest(low, LB), 1)



//plot(RDirenc,title="Resistance", color=#f7d707fc, linewidth =2)
//plot(SDestek,title="Support", color=#064df4, linewidth = 2)

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

LB22 = input(40, title="Satım_Üst_Çizgi")
LB1 = input(300, title="Satım_Alt_Çizgi")

Barcolor2=input(true,title="Barcolor2")
Bgcolor2=input(true,title="Bgcolor2")
//////////////////////////////////////////////////////////////////////

//////////////////////////////////////////////////////////////////////////////////////
RDirenc2 = ta.valuewhen(ta.cross(ta.hma(close, LB22), close), ta.highest(high, LB22), 1)
SDestek2 = ta.valuewhen(ta.cross(close, ta.hma(close, LB1)), ta.lowest(low, LB1), 1)



//plot(RDirenc2,title="Resistance2", color=#f40a0afc, linewidth =2)
//plot(SDestek2,title="Support2", color=#0eed0e, linewidth = 2)

//colors=if(close>RDirenc, color= #008000,if(SDestek<close,color=#FFFF00,color=#FF0000))

aralik_yuzde_alis = ((RDirenc-SDestek)/SDestek)*100
fark = input(25.0, title="Alış Aralığı %")



aralik_yuzde_satis = ((RDirenc2-SDestek2)/SDestek2)*100
fark2 = input(45.0, title="Satış aralığı %")




buyProcess = input(0.12, "ALIM YERİ %")
//buyProcess2 = input(0.10, "ALIM YERİ-2 %")
//buyProcess3 = input(0.10, "ALIM YERİ-3 %")



buy1 = strategy.position_avg_price - (strategy.position_avg_price * buyProcess)

buy2 = buy1 - (strategy.position_avg_price * buyProcess)

buy3 = buy2 - (strategy.position_avg_price * buyProcess)

buy4 = buy3 - (strategy.position_avg_price * buyProcess)



//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
isLong1 = if ta.crossover(close, SDestek) and aralik_yuzde_alis < fark 
    1
else
    0

    
isLong2 = if ta.crossover(close, SDestek) and (close <=  buy1)
    1
else
    0

isLong3 = if ta.crossover(close, SDestek) and (close <=  buy2) 
    1
else
    0

isLong4 = if ta.crossover(close, SDestek) and (close <= buy3) 
    1
else
    0



message_long_entry  = input("long entry message")
message_long_exit   = input("long exit message")


fullProfit = input(2.00, "PROFİT SATIŞ SEVİYESİ")
profit = strategy.position_avg_price * fullProfit
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

strategy.entry(id = "BUY-1", direction = strategy.long, qty = 25, when = (isLong1 and strategy.position_size == 0), alert_message = message_long_entry)
strategy.entry(id = "BUY-2", direction = strategy.long, qty = 25, when = (isLong2 and strategy.position_size == 25), alert_message = message_long_entry)
strategy.entry(id = "BUY-3", direction = strategy.long, qty = 25, when = (isLong3 and strategy.position_size == 50), alert_message = message_long_entry)
strategy.entry(id = "BUY-4", direction = strategy.long, qty = 25, when = (isLong4 and strategy.position_size == 75), alert_message = message_long_entry)



buyclose1 = if  (close >= (strategy.position_avg_price + profit)) and aralik_yuzde_satis > fark2
    close
    

strategy.exit("EXİT",qty_percent = 100, stop = buyclose1)


aritmeticClose =  strategy.position_avg_price + profit
plot(aritmeticClose, color = color.rgb(248, 5, 240), linewidth = 1, style = plot.style_linebr)
```

> Detail

https://www.fmz.com/strategy/435886

> Last Modified

2023-12-19 15:21:22
