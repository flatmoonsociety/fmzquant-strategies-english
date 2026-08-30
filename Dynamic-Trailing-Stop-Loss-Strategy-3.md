
> Name

Dynamic-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1157348bf106fa1d47a.png)
[trans]

## Overview
The dynamic trailing stop strategy is a quantitative trading strategy that utilizes the trailing stop mechanism. This strategy is based on the trend following theory, sets a trailing stop loss line, and realizes stop loss confirmation and trailing stop loss adjustment. It is mainly used to control the stop loss of a single transaction, lock in profits to the maximum extent, and reduce transaction risks.
## Strategy Principle
The core of the dynamic trailing stop strategy is to set three key parameters: initial stop loss distance, trailing stop loss distance and trailing stop loss trigger distance. When the buy signal is triggered, the initial stop loss price is calculated based on the buy price and the set initial stop loss distance. Each K line will then determine whether the trailing stop loss triggering condition is reached, and if so, a new trailing stop loss price will be set. The new trailing stop price will be calculated based on the current closing price and the trailing stop distance. In this way, as long as the price moves in a favorable direction, the trailing stop loss line will continue to rise to lock in profits. A sell signal is issued when price reverses and triggers the trailing stop.
This strategy also has a low stop loss. Regardless of whether the trailing stop is activated or not, if the price falls below the low stop loss, the loss will be stopped directly. Low stop loss is used to prevent unexpected price gaps. Therefore, the dynamic trailing stop loss strategy uses a dynamic stop loss mechanism in the form of upper and lower lines to enable the stop loss line to automatically track favorable trends while preventing excessive losses.
## Strategic Advantages
1. Continuously lock in profits through trailing stop loss to avoid giving too many opportunities to cover.
2. Adopting an upper and lower double-line stop-loss structure not only ensures that the stop-loss line can be followed up in time, but also prevents excessive losses.
3. Use the continuous judgment mechanism to adjust stop loss, which is simple to operate and easy to implement.
4. According to the characteristics of the market and individual stocks, parameters can be adjusted to optimize the stop loss effect.
5. There is no need to predict the market direction, just follow the trend.
## Strategy Risk
1. Improper parameter settings may cause the stop loss to be too loose or too tight. If it is too loose, it will not be able to effectively stop losses; if it is too tight, it will be easily hit by ordinary price fluctuations.
2. When an unexpected event causes the price to jump and fall, the stop loss may be invalid, and other protective measures should be taken.
3. Transaction fees and slippage may have an impact on the actual selling price after the stop loss line is triggered.
4. The adaptability is not strong, and the effect is not good in certain stages, such as the shock range.
Countermeasures:
1. It is recommended to continuously optimize parameters based on backtest and real-time results.
2. You can set a wider low stop loss to prevent gaps.
3. Consider the impact of transaction fees and slippage when calculating the stop loss price. 
4. Can be used in combination with trend and fluctuation judgment indicators.
## Strategy optimization direction
1. Adjust the trailing stop loss line to a percentage change method to better track stock price changes at different price levels.
2. Add a volatility indicator to suspend tracking and stop loss when large fluctuations are determined to avoid stop loss being triggered by ordinary fluctuations.
3. Use machine learning methods to automatically optimize parameters. The training sample selects the return rate of the parameter combination in the most recent period of time.
4. Increase the judgment of opening conditions and combine indicators such as trends, support and resistance to avoid opening positions in volatile markets.

## Summarize
The dynamic trailing stop loss strategy uses a dual-line stop loss mechanism to set trailing stop loss lines to achieve stop loss confirmation and trailing stop loss adjustment. The stop loss distance can be automatically adjusted according to price changes to lock in profits, reduce taking, and control losses. This strategy is simple to operate and easy to implement. It can optimize parameters according to market conditions and has better results when combined with other strategies. However, there are certain limitations. It is recommended to adjust and improve it before putting it into real use.
||

## Overview  

The dynamic trailing stop loss strategy is a quantitative trading strategy that utilizes a trailing stop loss mechanism. It sets a trailing stop loss line based on trend tracking theory to confirm stop loss and adjust trailing stop loss. It is mainly used to control the stop loss of a single trade, maximize profit locking, and reduce trading risks.

## Strategy Logic

The core of the dynamic trailing stop loss strategy lies in setting three key parameters: initial stop loss distance, trailing stop loss distance and trailing stop loss trigger distance. After a buy signal is triggered, the initial stop loss price is calculated based on the entry price and the set initial stop loss distance. Then, every bar will judge whether the trailing stop loss trigger condition is met. If yes, a new trailing stop loss price will be set. The new trailing stop loss price is calculated based on the current closing price and trailing stop loss distance. Thus, as long as the price runs in a favorable direction, the trailing stop loss line will continue to move up to lock in profits. When the price reversal triggers the trailing stop loss line, a sell signal will be generated.

This strategy also has a lower stop loss. No matter whether the trailing stop loss is activated or not, if the price breaks below the lower stop loss, stop loss will be directly triggered. The lower stop loss serves to guard against price gaps caused by sudden events. Therefore, through the dynamic stop loss mechanism in the form of double-line stop loss, the stop loss line can automatically track favorable trends, while preventing excessive losses.

## Advantages

1. Continuously lock in profits through trailing stop loss, avoiding giving too much retracement room.

2. Adopt a double-line stop loss structure to ensure the stop loss line can promptly follow up, while preventing excessive losses.

3. Use a continuous judgment mechanism for stop loss adjustment with simple operation and easy implementation.  

4. Parameters can be optimized according to market and stock characteristics to improve stop loss efficacy.

5. No need to predict market trends, just follow the trend.

## Risks

1. Improper parameter settings may result in either too loose or too tight stop loss. Too loose would make stop loss ineffective, while too tight tends to get stopped out by normal price fluctuations.

2. In case of price gaps caused by sudden events, it may fail to stop loss. Other protective measures should be taken accordingly.

3. Trading costs and slippage may affect the actual selling price after the stop loss line is triggered.  

4. Adaptability is not strong. It does not work well in certain stages, such as range-bound movements.

Countermeasures:
1. It is recommended to continuously optimize parameters based on backtest and live results.
2. Set a wider lower stop loss to guard against price gaps.  
3. Take trading costs and slippage into account when calculating stop loss price.
4. Use in combination with trend and volatility indicators.


## Directions for Optimization

1. Adjust the trailing stop loss line in percentage change, which can better track price movements across different price levels.

2. Add volatility metrics to suspend trailing stop loss when facing high volatility, avoiding normal fluctuations from triggering stop loss.   

3. Automatically optimize parameters via machine learning. Choose return of different parameter combinations in recent period as training samples.  

4. Add open position criteria with consideration of indicators like trend, support & resistance to avoid opening positions in ranging markets.

## Conclusion  

The dynamic trailing stop loss strategy sets trailing stop loss lines through a double-line stop loss mechanism to confirm stop loss and adjust trailing stop loss based on price changes. It can automatically adjust stop loss distance to lock in profits, reduce pullbacks and control losses. With simple operation and easy implementation, this strategy can be further optimized based on market conditions and used together with other strategies for better performance. But it also has some limitations. It is advisable to improve and test it sufficiently before applying it in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|0.035|(?Sell Settings)Stop Loss Loss: 1% = .01|
|v_input_float_2|0.0065|Trailing Stop Arm: 1%=.01|
|v_input_float_3|0.003|Trailing Stop Trigger: 1%=.01 |
|v_input_int_1|14|(?Trend Line Settings) ema 1 Length|
|v_input_1_close|0|ema 1 Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|22| ema 2 Length|
|v_input_2_close|0|ema 2 Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_3|200| ema 3 Length|
|v_input_3_close|0|ema 2 Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-28 00:00:00
end: 2023-12-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Thumpyr
//@version=5

/////////////////////////////////////////////////////////////////////////////////////////////
// Comment out Strategy Line and remove // from Indicator line to turn into Indicator  //////
// Do same for alertConidction at bottom                                               //////
/////////////////////////////////////////////////////////////////////////////////////////////
strategy("PCT Trailing Stoploss-Strategy", shorttitle="PCT Trailing Stoploss- Strategy", overlay=true)
//indicator(title="PCT Trailing Stoploss- Indicator", shorttitle="PCT Trailing Stoploss - Indicator", timeframe="", timeframe_gaps=true, overlay=true)//

sellLow=input.float(.035, minval=0, title="Stop Loss Loss: 1% = .01", group="Sell Settings")
trailStopArm=input.float(.0065, minval=0, title="Trailing Stop Arm: 1%=.01", group="Sell Settings")
trailStopPct=input.float(.003, minval=0, title="Trailing Stop Trigger: 1%=.01 ", group="Sell Settings")

/////////////////////////////////////////////////
//               Indicators                    //
/////////////////////////////////////////////////
ema1Len = input.int(14, minval=1, title=" ema 1 Length", group="Trend Line Settings")
ema1Src = input(close, title="ema 1 Source", group="Trend Line Settings")
ema1 = ta.ema(ema1Src, ema1Len)
plot(ema1, title="EMA", color=color.blue)

ema2Len = input.int(22, minval=1, title=" ema 2 Length", group="Trend Line Settings")
ema2Src = input(close, title="ema 2 Source", group="Trend Line Settings")
ema2 = ta.ema(ema2Src, ema2Len)
plot(ema2, title="EMA", color=color.orange)

ema3Len = input.int(200, minval=1, title=" ema 3 Length", group="Trend Line Settings")
ema3Src = input(close, title="ema 2 Source", group="Trend Line Settings")
ema3 = ta.ema(ema3Src, ema3Len)
plot(ema3, title="EMA", color=color.gray)


/////////////////////////////
////   Buy Conditions    ////
/////////////////////////////

alertBuy = ta.crossover(ema1,ema2) and close>ema3

////////////////////////////////////////////////////////////////////
////   Filter redundant Buy Signals if Sell has not happened    ////
////////////////////////////////////////////////////////////////////
var lastsignal = 0
showAlertBuy = 0
if(alertBuy and lastsignal !=1)
    showAlertBuy  := 1
    lastsignal      := 1
buyAlert= showAlertBuy > 0


//////////////////////////////////////////////////////////////////
////          Track Conditions at buy Signal                  ////
//////////////////////////////////////////////////////////////////

alertBuyValue = ta.valuewhen(buyAlert, close,0)
alertSellValueLow = alertBuyValue - (alertBuyValue*sellLow)

////////////////////////////////////////////////////////////
/////            Trailing Stop                         /////
////////////////////////////////////////////////////////////
var TSLActive=0         //Check to see if TSL has been activated
var TSLTriggerValue=0.0 //Initial and climbing value of TSL
var TSLStop = 0.0       //Sell Trigger
var TSLRunning =0       //Continuously check each bar to raise TSL or not

//  Check if a Buy has been triggered and set initial value for TSL //
if buyAlert
    TSLTriggerValue := alertBuyValue+(alertBuyValue*trailStopArm)
    TSLActive := 0
    TSLRunning :=1
    TSLStop := TSLTriggerValue - (TSLTriggerValue*trailStopPct)
    

//  Check that Buy has triggered and if Close has reached initial TSL//  
//  Keeps from setting Sell Signal before TSL has been armed w/TSLActive//
beginTrail=TSLRunning==1 and TSLActive==0 and close>alertBuyValue+(alertBuyValue*trailStopArm) and ta.crossover(close,TSLTriggerValue)
if beginTrail
    TSLTriggerValue :=close
    TSLActive :=1
    TSLStop :=TSLTriggerValue - (TSLTriggerValue*trailStopPct)
    
//  Continuously check if TSL needs to increase and set new value //    
runTrail= TSLActive==1 and (ta.crossover(close,TSLTriggerValue) or close>=TSLTriggerValue)
if runTrail
    TSLTriggerValue :=close
    TSLStop :=TSLTriggerValue - (TSLTriggerValue*trailStopPct)
    
//  Verify that TSL is active and trigger when close cross below TSL Stop//
TSL=TSLActive==1 and (ta.crossunder(close,TSLStop) or (close[1]>TSLStop and close<TSLStop)) 

// Plot point of inital arming of TSL//
TSLTrigger=TSLActive==1 and TSLActive[1]==0
plotshape(TSLTrigger, title='TSL Armed', location=location.abovebar, color=color.new(color.blue, 0), size=size.small, style=shape.cross, text='TSL Armed')


////////////////////////////////////////////////////////////
// Plots used for troubleshooting and verification of TSL //
////////////////////////////////////////////////////////////
//plot(TSLActive,"Trailing Stop", color=#f48fb1)
//plot(TSLRunning,"Trailing Stop", color=#f48fb1)
//plot(TSLTriggerValue,"Trailing Stop Trigger", color.new(color=#ec407a, transp = TSLRunning==1 ? 0 : 100))
//plot(TSLStop,"Trailing Stop", color.new(color=#f48fb1, transp = TSLRunning==1 ? 0 : 100))//


////////////////////////////////////////////////////////////
/////             Sell Conditions                    ///////
////////////////////////////////////////////////////////////
Sell1 = TSL
Sell2 = ta.crossunder(close,alertSellValueLow)

alertSell= Sell1 or Sell2
////////////////////////////////////////////////////////////

////////////////////////////////////////////////////////////
////        Remove Redundant Signals                    ////
////////////////////////////////////////////////////////////
showAlertSell = 0
if(alertSell and lastsignal != -1)
    showAlertSell := 1
    lastsignal      := -1
sellAlert= showAlertSell > 0

if sellAlert
    TSLActive :=0
    TSLRunning :=0

/////////////////////////////////////////
//  Plot Buy and Sell Shapes on Chart  //
/////////////////////////////////////////
plotshape(buyAlert, title='Buy', location=location.belowbar, color=color.new(color.green, 0), size=size.small, style=shape.triangleup, text='Buy')
plotshape(sellAlert, title='Sell', location=location.abovebar, color=color.new(color.red, 0), size=size.small, style=shape.triangledown, text='Sell')

/////////////////////////////////////////////////////////////////////////////////////////////
//                        Remove // to setup for Indicator                                 //
/////////////////////////////////////////////////////////////////////////////////////////////
//Alerts
//alertcondition(title='Buy Alert', condition=buyAlert, message='Buy Conditions are Met')
//alertcondition(title='Sell Alert', condition=sellAlert, message='Sell Conditions are Met')
/////////////////////////////////////////////////////////////////////////////////////////////


////////////////////////////////////////////////////////////
////  Comment out this section if setup as Indicator    ////
////////////////////////////////////////////////////////////
longCondition = buyAlert
if (longCondition)
    strategy.entry("Buy", strategy.long)
    alert(message='Buy', freq=alert.freq_once_per_bar_close)
    
shortCondition = sellAlert
if (shortCondition)
    strategy.close_all(sellAlert,"Sell")
    alert(message='Sell', freq=alert.freq_once_per_bar_close)
/////////////////////////////////////////////////////////////



```

> Detail

https://www.fmz.com/strategy/436984

> Last Modified

2023-12-29 10:42:27
