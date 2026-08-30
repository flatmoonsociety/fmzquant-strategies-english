
> Name

Improved-RSI-Breakout-Strategy-with-Stop-Loss-and-Take-Profit Improved RSI Breakout Strategy with Stop-Loss-and-Take-Profit
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/177ff32b5af0907f550.png)
[trans]

## Overview

The Improved RSI Breakout Strategy is a trend following strategy that uses the Relative Strength Index (RSI) indicator to determine entry and exit points. It builds upon a basic RSI strategy by adding stop loss and take profit orders to manage risk. 

When RSI crosses above 70 (overbought level), the strategy goes long. When RSI crosses below 30 (oversold level), the strategy goes short. This allows it to ride strong trends up and down. Stop loss and take profit orders are then used to lock in profits and limit losses on existing positions.

## How it Works

The core mechanism relies on the RSI indicator crossing its overbought level (default 70) or oversold level (default 30) to trigger entries. 

- When RSI crosses above 70, it indicates the asset is overbought and may reverse, so the strategy opens a long position.  

- When RSI crosses below 30, it indicates the asset is oversold and may bounce, so the strategy opens a short position.

This allows the strategy to capitalize on mean reversion tendencies coming off extreme RSI levels.

The key enhancement is the added risk management through stop loss and take profit orders.

After entering a position, stop loss and take profit orders are placed at fixed percentages away from the entry price (default 2% stop loss, 10% take profit). This locks in a fixed reward to risk ratio on every trade.

If a position moves favorably, the take profit limit order will close it for a gain. If it moves adversely, the stop loss order will close it for a small loss. This maximizes profits in winning trades and minimizes losses from losing trades.

## Advantages

- Rides strong trends by buying dips and selling rallies 
- Take profit targets larger than stop loss targets allow asymmetric risk-reward
- Stop losses minimize losses on trades going the wrong direction
- Simple concept easy to understand and implement
- Added risk management gives it edge over basic RSI strategies

## Risks

- Whipsaws possible if RSI crosses levels multiple times
- Stop loss placement can be optimized 
- Take profit levels need fine tuning for better performance
- Works best in trending markets, range-bound performance weaker

## Enhancements

Some ways the strategy can be improved further:

- Add additional filters before entry trigger, such as a price breakout
- Trail stop loss levels to lock in more profits in winning trades  
- Expand take profit targets for bigger reward potential
- Optimize RSI levels, stop loss %, take profit % for each market
- Adapt to volatility conditions by using ATR for stop loss size

## Conclusion

The Improved RSI Breakout Strategy brings together several positive elements - using RSI to identify potential turning points, trend following entries in direction of momentum, asymmetric risk-reward from take profits > stop loss, and risk mitigation from exit orders.

By combining these aspects it aims to maximize reward while minimizing risk on each trade. Proper optimization and robust position sizing can turn this into a stable system across various market environments. The built-in risk controls give it an edge over basic RSI strategies.

||

## Overview
The Modified RSI Breakout Strategy is a trend following strategy that uses the Relative Strength Index (RSI) indicator to determine entry and exit points. It adds stop-loss and take-profit orders to the basic RSI strategy to manage risk.
This strategy goes long when the RSI crosses 70 (overbought level). This strategy goes short when the RSI crosses below 30 (oversold level). This allows it to go with the flow, go with the flow, go with the flow, and go with the flow. Then use stop loss and take profit orders to lock in profits and limit losses.
## Working principle
The core mechanism of this strategy relies on the RSI indicator crossing its overbought level (default is 70) or oversold level (default is 30) to trigger an entry.
- When RSI crosses 70, it means that the asset is overbought and may reverse, so the strategy is to open a long position.
- When RSI falls below 30, it means that the asset is oversold and may rebound, so the strategy is to open a short position.
This allows the strategy to profit from extreme RSI level reversals.
The key improvement is the addition of risk management through stop-loss and take-profit orders.
After entering the market, set a certain percentage of stop loss and take profit orders above and below the entry price (the default is 2% stop loss and 10% take profit). This locks in a fixed risk-reward ratio for each trade.
If the position moves favorably, a take-profit limit order will close the position at a profit. If the trend is unfavorable, a stop loss order will eliminate the trade with a small loss. This maximizes profits on winning positions and minimizes losses on losing positions.
## Advantages
- Follow the trend, buy low and sell high
- Take profit is greater than stop loss, achieving asymmetric risk-return rate
- Stop loss minimizes losses from trades in the wrong direction
- Concepts are simple and easy to understand and implement
- Added risk management advantages compared to basic RSI strategy
## Risk
- An error signal may occur if the RSI level crosses above and below multiple times
- Stop loss position can be further optimized
- Take profit levels need to be fine-tuned for better performance
- Best performance in trending market, weak performance in range-bound market
## Optimization direction
Some ideas for further improvement of this strategy:
- Add other filters before entering the market, such as price breakouts
- Trailing stop loss to lock in more profits
- Expand your take-profit target for greater profit potential
- Optimize RSI levels, stop loss percentage, take profit percentage for each market
- Set stop loss width based on ATR to adapt to market volatility
## Summarize
The improved RSI breakout strategy brings together several positive factors - using RSI to identify potential turning points, judging direction based on momentum, achieving asymmetric risk-return by taking profit greater than stop loss, and reducing risk through exit orders.
By combining these factors, the aim is to maximize returns and minimize risks on each trade. Properly optimizing the position size can make it operate stably in different market environments. The built-in risk control system gives it an advantage over the basic RSI strategy.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|70|overbought value|
|v_input_2|30|oversold value|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-02-03 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// @version=4
// Improved RSI Simple Strategy
// Added Risk Management System: SL & TP
// © Bitduke
// All scripts: https://www.tradingview.com/u/Bitduke/#published-scripts

strategy("Simple RSI Buy/Sell at a level", shorttitle="Simple RSI Strategy (SL/TP)", overlay=false )
overbought = input(70, title="overbought value")
oversold = input(30, title="oversold value")

lenght = 14
rsi = rsi(close, lenght)
myrsi = rsi > overbought
myrsi2 = rsi < oversold

barcolor(myrsi ? color.black : na)
barcolor(myrsi2 ? color.blue : na)

// Risk Management Sysyem
convert_percent_to_points(percent) =>
    strategy.position_size != 0 ? round(percent / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
    
setup_percent(percent) =>
    convert_percent_to_points(percent)

STOP_LOSS = 2
TAKE_PROFIT = 10

plot(rsi)
plot(overbought, color = color.red)
plot(oversold, color = color.green)

//STRATEGY
if (myrsi)
    strategy.entry("Long", strategy.long)
    
if (myrsi2)
    strategy.entry("Short", strategy.short)

strategy.exit("Exit", qty_percent = 100, profit = setup_percent(STOP_LOSS), loss = setup_percent(TAKE_PROFIT))


```

> Detail

https://www.fmz.com/strategy/440990

> Last Modified

2024-02-04 15:27:50
