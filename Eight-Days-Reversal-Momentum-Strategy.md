
> Name

Eight-Days-Reversal-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/dc004000dc448841b4.png)

[trans]
## Overview
This strategy mainly uses the characteristics of price reversal after being above or below the 5-day simple moving average for 8 consecutive days to capture the momentum effect in the short and medium term. When the price is below the 5-day line for 8 consecutive days, the closing price on the first day crosses the 5-day line again, go long; when the price is above the 5-day line for 8 consecutive days, when the closing price on the first day falls below the 5-day line again, go short.
## Strategy Principle
1. Calculate the 5-day simple moving average SMA.
2. Define the long trend TrendUp as the closing price is greater than or equal to the SMA, and the short trend TrendDown as the closing price is less than or equal to the SMA.
3. Conditions for confirming trend reversal: After the closing price is lower than the SMA for 8 consecutive days, a buy signal is triggered when the closing price of the next day turns long (crosses the SMA); after the closing price is higher than the SMA for 8 consecutive days, a sell signal is triggered when the closing price of the next day turns short (crosses the SMA below).
4. Entry: The buying condition Buy is to go long when the buy signal TriggerBuy was triggered on the previous day and the current trend is short; the selling condition Sell is to go short when the sell signal TriggerSell was triggered on the previous day and the current trend is bullish.
5. Exit: The long stop loss is to close the position when the closing price crosses below the SMA; the short stop loss is to close the position when the closing price is above the SMA.
## Advantage Analysis
1. Taking advantage of the characteristics of price reversal, it is suitable for capturing short- and medium-term momentum.
2. There are many cases of breaking through SMA for 8 consecutive days to form a trend, which increases trading opportunities.
3. The 5-day line parameters are better to avoid being fooled by too many false breakthroughs.
4. The risk is controllable and there is a clear stop loss point.
## Risk Analysis
1. Stop loss points may be triggered frequently when the market fluctuates.
2. If the number of days for breakthrough operation is set too long, the best entry opportunity may be missed.
3. If the market moves unilaterally for a long time, it will be difficult for this strategy to make a profit.
The parameters of SMA can be appropriately adjusted; entry conditions can be optimized to prevent false breakthroughs; and trend judgment indicators can be combined to enhance the effect.
## Optimization direction
1. Parameter optimization: You can test SMA parameters of different periods to find better parameters.
2. Optimize market entry: add trading volume indicators to avoid false breakthroughs; or add positive and negative line judgments to avoid shocks. 
3. Exit optimization: You can test the closing price to fall back to a certain extent and then stop the loss, and increase the stop loss BUFFER.
4. Risk control optimization: You can set the number of daily stop losses to avoid excessive losses.
5. Combined with other indicators: RSI, MACD and other trend indicators can be added to identify the trend.
## Summarize
This strategy determines the price movement status and captures the process of short- and medium-term prices from breakthrough to reversal, thereby achieving a trading strategy that avoids shocks and follows the trend. The key is to be rigorous in parameter setting and entry judgment to prevent being misled by noise; at the same time, the exit stop loss must be reasonable to prevent excessive losses. If supplemented by trend judgment indicators, better results can be obtained. The logic of this strategy is clear and easy to understand, and the code is concise. It is worthy of in-depth study and optimization.
||

## Overview

This strategy mainly utilizes the reversal feature of prices after continuously closing above or below the 5-day simple moving average for 8 days to capture the momentum effect in medium and short term. It goes long when the closing price crosses above the 5-day line again after continuously closing below the 5-day line for 8 days; it goes short when the closing price crosses below the 5-day line again after continuously closing above the 5-day line for 8 days.

## Strategy Logic  

1. Calculate the 5-day simple moving average SMA.
2. Define the uptrend TrendUp as close greater than or equal to SMA, downtrend TrendDown as close less than or equal to SMA.
3. Confirm the condition for trend reversal: trigger buy signal when closing price closes below SMA for consecutive 8 days and turns to uptrend (crosses above SMA) the next day; trigger sell signal when closing price closes above SMA for consecutive 8 days and turns to downtrend (crosses below SMA) the next day.  
4. Entry: long when the buy condition Buy is triggered yesterday and the current trend is downtrend; short when the sell condition Sell is triggered yesterday and the current trend is uptrend.
5. Exit: close long position when closing price crosses below SMA; close short position when closing price crosses above SMA.

## Advantage Analysis  

1. Captures momentum by utilizing price reversal features, suitable for medium and short term trading.
2. High trading opportunities as continuous SMA breakout for 8 days happens frequently.  
3. 5-day SMA parameter performs well, avoids too many false breakouts. 
4. Controllable risk with clear stop loss point.

## Risk Analysis

1. Stop loss may be triggered frequently during market consolidation.  
2. May miss the best entry point if the breakout days are set too long.
3. Hard to profit if there is a prolonged trend.

Can optimize SMA parameters, improve entry criteria to prevent false breakout, combine with trend indicators to strengthen the strategy.  

## Optimization Directions

1. Parameter optimization: test different periods of SMA to find better parameters.  
2. Entry optimization: add volume indicators to avoid false breakouts; or judge bull/bear candles to avoid whipsaws.
3. Exit optimization: test fixed percentage trailing stop loss to give more room.   
4. Risk control: set maximum daily stop loss times to limit losses.
5. Combine indicators: add RSI, MACD to determine trend to identify market conditions.

## Conclusion  

The strategy captures the price movement from breakout to pullback by judging the momentum, implements the trading logic of avoiding whipsaws and trend following. The keys are strict parameter settings and robust entry criteria to prevent noise; reasonable stop loss to limit losses. Combining with trend indicators can achieve better results. The strategy logic is simple and clean. It is worthwhile to explore further optimization.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-04 00:00:00
end: 2023-12-04 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Marcuscor

//@version=5

// Inpsired by Linda Bradford Raschke: a strategy for trading momentum in futures markets

strategy("8D Run", initial_capital = 50000, commission_value = 0.0004) 


SMA = ta.sma(close,5)

TrendUp = close >= SMA

TrendDown = close <= SMA


//logic to long

TriggerBuy = ta.barssince(close < SMA) >= 8

Buy = TriggerBuy[1] and TrendDown 

strategy.entry("EL", strategy.long, when = Buy)
strategy.close(id = "EL", when = close > SMA)

// 1) color background when "run" begins and 2) change color when buy signal occurs
bgcolor(TriggerBuy? color.green : na, transp = 90)
bgcolor(Buy ? color.green : na, transp = 70)


// logic to short 

TriggerSell = ta.barssince(close > SMA) >= 8

Sell = TriggerSell[1] and TrendUp

strategy.entry("ES", strategy.short, when = Sell)
strategy.close(id = "ES", when = close < SMA)

// 1) color background when "run" begins and 2) change color when sell signal occurs
bgcolor(TriggerSell ? color.red : na, transp = 90)
bgcolor(Sell ? color.red : na, transp = 70) 






```

> Detail

https://www.fmz.com/strategy/434294

> Last Modified

2023-12-05 10:56:37
