
> Name

ATR Adjustable Trailing Stop Loss Strategy ATR-Adjustable-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a11fe258364185305a.png)

[trans]


This strategy uses the ATR indicator to calculate the dynamic stop loss line to achieve the purpose of risk control.
#### Overview
This strategy uses the ATR indicator to calculate the dynamic stop loss line. When the price rises, the stop loss line will be raised as the price rises to lock in profits. When the price falls, the stop loss line remains unchanged to avoid stop loss exit. The ATR indicator can measure market volatility and risk, multiply it by a coefficient to generate a stop loss line, thereby controlling the risk exposure of each order.
#### Principle
This strategy uses a combination of the ATR indicator and the Highest function to calculate the dynamic stop loss line. The specific calculation formula is as follows:
```pine
TS=highest(high-Mult*atr(Atr),Hhv)
```

Among them, Atr represents the ATR period parameter, Hhv represents the Highest function to find the period parameter, and Mult represents the ATR coefficient.
The calculation idea of ​​this formula is to first calculate the value of the ATR indicator, and then multiply it by the coefficient Mult to obtain the range of the stop loss buffer area. Then use the Highest function to find the highest price in the past Hhv period, and then subtract the stop loss cache interval range to obtain the dynamic stop loss line TS.
When the price rises, the highest price will continue to hit new highs, thus driving the stop loss line to move upward and locking in profits. When the price falls, the stop loss line will maintain the previous high point, avoiding stop loss exit.
#### Advantages
1. Dynamic stop loss, lock in profits in time
The stop loss line in this strategy is dynamically adjusted and can track the highest point after the price rises to achieve timely lock-in of profits. It has advantages over fixed stop loss.
2. Avoid unnecessary stop losses
When there is a normal price correction or the stop loss is too dense, the fixed stop loss line can easily be triggered to stop trading. This strategy can keep the stop loss line unchanged when the price drops, avoiding unnecessary stop loss exits.
3. Adjustable stop loss range
By adjusting the ATR cycle parameters and coefficient parameters, you can control the sensitivity of the stop loss line adjustment and achieve different levels of stop loss.
4. Risks are controllable
The range of the stop loss line is dynamically calculated by ATR, which can set a reasonable stop loss range according to market volatility, thereby controlling the risk exposure of each order.
#### Risk
1. Stop loss is too aggressive when the market fluctuates violently.
When the market fluctuates violently, ATR will rise rapidly and the stop loss line will move up quickly, increasing the probability of unnecessary stop loss. At this time, it is necessary to appropriately adjust the ATR cycle parameters to reduce the sensitivity of stop loss line adjustment.
2. Difficult to cope with significant market reversals
This strategy is difficult to cope with a large market reversal. At this time, the stop loss line may be too lagging, and positions should be reduced in time to avoid risks.
3. Parameter optimization is difficult
The ATR period, Highest period and coefficient parameters need to be comprehensively optimized, which is very difficult to optimize. It is recommended to use the step optimization method for multi-combination testing.
#### Optimization ideas
1. Optimize ATR cycle parameters
Appropriately increasing the ATR cycle parameter can reduce the situation of too frequent adjustment of the stop loss line, but it will increase the loss of a single transaction.
2. Optimize Highest cycle parameters
Increasing the Highest period parameter can make the stop loss line more stable, but it needs to be weighed against the tracking speed.
3. Test different ATR coefficients
Choose the appropriate ATR coefficient according to the characteristics of different varieties. Increasing the coefficient will reduce the stop loss range, and decreasing the coefficient will reduce the single loss.
4. Combine trend indicators
Combined with trend indicators to assist decision-making, the probability of the stop loss line being reversed and cleared can be reduced.
#### Summarize
This strategy overall has the advantages of dynamic stop loss and controllable risk, and is suitable for trending markets. However, attention needs to be paid to preventing risks caused by violent market fluctuations, and parameter optimization is difficult. Through reasonable parameter setting and optimization, as well as auxiliary technical analysis, this strategy can be applied to real trading.
||
This strategy uses the ATR indicator to calculate a dynamic stop loss line for risk control.

#### Overview 

The strategy uses the ATR indicator to calculate a dynamic stop loss line. When prices rise, the stop loss line will move up with prices to lock in profits. When prices fall, the stop loss line remains unchanged to avoid being stopped out. The ATR indicator can measure market volatility and risk. Multiplying it by a coefficient generates the stop loss line, thus controlling the risk exposure per trade.

#### Principles

The strategy uses the ATR indicator and Highest function to calculate the dynamic stop loss line. The specific formula is:

```pine
TS=highest(high-Mult*atr(Atr),Hhv) 
```

Where Atr is the ATR period parameter, Hhv is the lookback period parameter of the Highest function, and Mult is the ATR coefficient.

The logic is to first calculate the ATR value, then multiply it by the Mult coefficient to get the range of the stop loss buffer zone. Then use the Highest function to find the highest high in the past Hhv periods, and subtract the stop loss buffer zone to obtain the dynamic stop loss line TS.

When prices rise, the highest high will be constantly updated, driving the stop loss line to move up and locking in profits. When prices fall, the stop loss line will maintain the previous high point to avoid being stopped out.

#### Advantages

1. Dynamic stop loss for timely profit taking

The stop loss line adjusts dynamically to track the highest point after price rises, allowing timely profit taking. This is superior to fixed stop loss.

2. Avoid unnecessary stop loss

Fixed stop loss lines can easily be triggered by normal pullbacks or overtight stops. This strategy keeps the stop loss unchanged during price declines to avoid unnecessary stops.

3. Adjustable stop loss range 

By tuning the ATR period and multiplier parameters, the sensitivity of the stop loss adjustment can be controlled for different degrees of stops.

4. Controllable risk

The ATR dynamically calculates the stop loss range, allowing reasonable stop loss ranges according to market volatility for risk control per trade.

#### Risks

1. Stop loss too aggressive during high volatility

When volatility spikes, ATR rises quickly and drives the stop loss line up rapidly, increasing the chance of unnecessary stops. The ATR period can be adjusted to make the line less sensitive.

2. Difficult to adapt to sharp reversals

The strategy struggles to adapt to sharp reversals. The stop loss line may lag too much and needs timely position reduction.

3. Difficult optimization

Optimizing the ATR period, Highest period and multiplier parameters together can be challenging. Stepped parameter sweep testing is recommended.

#### Optimization

1. Optimize ATR Period

Increase ATR period to reduce overly frequent stop line adjustment, but at the cost of larger loss per stop.

2. Optimize Highest Period

Increase Highest period to make the line more stable, but balance tracking speed.

3. Test different ATR coefficients

Choose proper ATR multipliers according to instrument characteristics. Larger multipliers widen stops, smaller ones decrease loss per stop.

4. Add trend filter

Adding a trend filter reduces the chance of stops being triggered by reversals.

#### Summary

The strategy has the advantage of dynamic stops and controllable risks. It fits trending markets but watch out for volatility spikes and difficult parameter optimization. With proper settings, optimization and additional techniques, it can be applied for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Atr Period|
|v_input_2|10|HHV Period|
|v_input_3|2.5|Multiplier|
|v_input_4|true|Barcolor|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-17 00:00:00
end: 2023-10-24 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ceyhun

//@version=4
strategy("ATR Trailing Stoploss Strategy ",overlay=true)

Atr=input(defval=5,title="Atr Period",minval=1,maxval=500)
Hhv=input(defval=10,title="HHV Period",minval=1,maxval=500)
Mult=input(defval=2.5,title="Multiplier",minval=0.1)
Barcolor=input(true,title="Barcolor")

TS=highest(high-Mult*atr(Atr),Hhv),barssince(close>highest(high-Mult*atr(Atr),Hhv) and close>close)
Color=iff(close>TS,color.green,iff(close<TS,color.red,color.black))
barcolor(Barcolor? Color:na)

plot(TS,color=Color,linewidth=3,title="ATR Trailing Stoploss")

Buy  = crossover(close,TS)
Sell = crossunder(close,TS)

if Buy
    strategy.entry("Buy", strategy.long, comment="Buy")
    
if Sell
    strategy.entry("Sell", strategy.short, comment="Sell")
```

> Detail

https://www.fmz.com/strategy/430150

> Last Modified

2023-10-25 15:08:04
