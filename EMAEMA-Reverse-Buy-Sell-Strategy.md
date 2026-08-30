
> Name

EMA reverse buy and sell strategy EMA-Reverse-Buy-Sell-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/bd6acdeb8fbfc5362b.png)
[trans]

## Overview
This strategy is a trend following strategy based on moving averages. It uses two EMA moving averages with different periods, namely the 21-period and 55-period EMA moving averages. When the short-term EMA line crosses the long-term EMA line, a buy signal is generated; when the short-term EMA line crosses below the long-term EMA line, a sell signal is generated.
In addition, the strategy also combines reverse buying and selling, ATR stop loss and reversal take profit to improve the stability and profitability of the strategy.
## Strategy Principle
1. Use two EMA moving averages of 21 periods and 55 periods. The 21EMA represents the short-term trend, and the 55EMA represents the long-term trend.
2. When the short-term EMA line crosses the long-term EMA line, it means that the short-term trend has converted into an upward trend, generating a buy signal.
3. When the short-term EMA crosses below the long-term EMA, it means that the short-term trend has converted into a downward trend, generating a sell signal.
4. Reverse buying and selling: A buy signal is generated only when the price is less than the opening price, and a sell signal is generated only when the price is greater than the opening price. This is to make a profit by buying during short-term pullbacks and selling during short-term rallies.
5. ATR stop loss: Use N times the ATR indicator to set the stop loss level. This allows for dynamically adjusting stops based on market volatility.
6. Reverse take profit: Use the purchase price minus N times ATR as the take profit level. This is to take profit by taking advantage of the characteristic of support turning into resistance before the price retests.
## Strategic Advantages
1. Use double EMA to determine the main trend direction and capture medium and long-term trends.
2. Reverse trading is suitable for short-term operations on trend pullbacks.
3. ATR stop loss, which can be set according to market volatility.
4. Set the reversal take profit near important technical levels to increase the probability of take profit.
5. The strategy logic is simple and clear, easy to understand and modify.
6. Can be used in markets with high volatility such as digital currencies.
## Risks and Solutions
1. Double EMA moving average has a high probability of generating false signals, so the moving average period can be appropriately extended.
2. It is easy to stop loss in reverse trading, and the adjustable stop loss is relatively loose.
3. There are often false breakthroughs in the market, and other indicators can be added to filter the signals.
4. Take-profit orders are risky, so you can manually remove them in time.
## Strategy optimization suggestions
1. Add indicators such as MACD and KD to determine overbought and oversold areas and filter entry opportunities.
2. Add more moving averages, such as the 120-period EMA, to comprehensively judge the trend.
3. Set slippage points for buying and selling respectively to optimize the entry price.
4. In view of the high volatility characteristics of digital currencies, the stop loss range of ATR can be appropriately relaxed.
5. Optimize the ATR multiple and trailing stop loss plan to obtain maximum profit and minimum retracement.

## Summarize
Overall, this strategy is a relatively simple double EMA moving average strategy. The core idea is to use EMA to determine the trend direction. The advantages of the strategy are simple logic, flexible parameter adjustment, and can be applied to medium and long-term trends and short-term reversals. We also analyzed the possible risks and countermeasures of this strategy, as well as some optimization suggestions for the future. Overall, this strategy has certain practicality and room for expansion, but it needs to adjust parameters according to different markets.
||
## Overview  

This is a trend following strategy based on EMA lines. It uses two EMA lines with different periods, 21 and 55. When the faster EMA line crosses above the slower EMA line, a buy signal is generated. When the faster EMA crosses below the slower one, a sell signal is generated.

In addition, the strategy incorporates reverse trading, ATR stop loss, and reversal take profit to enhance its stability and profitability.  

## Strategy Logic   

1. Use 21 and 55 period EMA lines. 21 EMA represents short-term trend and 55 EMA represents long-term trend.   

2. When 21 EMA crosses above 55 EMA, it indicates the short-term trend changes to upward, generating a buy signal.  

3. When 21 EMA crosses below 55 EMA, it indicates the short-term trend turns downward, generating a sell signal.   

4. Reverse trading: only buy when price is below open price, and only sell when price is above open price. This aims to buy on short-term pullbacks and sell on rebounds.  

5. ATR stop loss: use N times ATR to set stop loss price. This dynamically adjusts stop loss based on market volatility.  

6. Reversal take profit: use entry price minus N times ATR as profit target. This takes advantage of price retesting previous support-turned-resistance area.  

## Advantages of the Strategy  

1. Captures mid- to long-term trends using dual EMA.  

2. Reverse trading suits short-term pullback trades of trends.   

3. ATR stop adapts to market volatility.  

4. Reversal take profit sits near important technical levels with higher probability.   

5. Simple and clear logic, easy to understand and modify.  

6. Applicable for high volatile markets like cryptocurrencies.  

## Risks and Solutions   

1. Dual EMA may generate false signals. Can lengthen EMA periods.  

2. Reverse trades prone to stop loss. Can loosen stop loss a bit.

3. Fake breakouts happen frequently. Add other filters.  

4. High risk on take profit. Manually remove take profit orders in time.  

## Optimization Suggestions    

1. Add indicators like MACD, KD to filter signals in overbought/oversold zones.   

2. Add more EMA like 120 period EMA to judge trend comprehensively.  

3. Set different slippage for longs and shorts to better entry price.  

4. Loosen ATR stop loss for highly volatile crypto trading.  

5. Optimize ATR multiplier and trailing stop mechanisms for maximum profit and minimum drawdown.

## Conclusion  

In conclusion, this is a relatively simple dual EMA trend following strategy. Its strength lies in clean logic, flexible parameters, applicability in mid- to long-term trends and short-term reversals. We also analyzed its potential weaknesses and solutions, along with several recommendations for future improvements. Overall speaking, this strategy is practical to some extent and has room to evolve, but its parameters need adjustments for different markets.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|ATR Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TheHulkTrading

// Simple EMA strategy, based on ema55+ema21 and ATR(Average True Range) and it enters a deal from ema55 when the other entry conditions are met


//@version=4
strategy("Simple Ema_ATR Strategy HulkTrading", overlay=true)

atr_multiplier = input(2, minval=1, title="ATR Multiplier") // ATR Multiplier. Recommended values between 1..4


emaFast=ema(close,21)
emaSlow=ema(close,55)

//Basically long and short conditions

//If long: 
// 1) close must be less than open (because we are searching for a pullback)
// 2) emaFast(21) must be bigger than emaSlow(55) - for a trend detection
// 3) Difference between emaFast and emaSlow must be greater than ATR(14) - for excluding flat
longCond = close < open and emaFast > emaSlow and abs(emaSlow-emaFast) > atr(14)  

//For short conditions are opposite
shortCond = close > open and emaFast < emaSlow and abs(emaSlow-emaFast) > atr(14) 

//Stop levels and take profits, based on ATR multiplier

stop_level_long = strategy.position_avg_price - atr_multiplier*atr(14)
take_level_long = strategy.position_avg_price + atr_multiplier*atr(14)
stop_level_short = strategy.position_avg_price + atr_multiplier*atr(14)
take_level_short = strategy.position_avg_price - atr_multiplier*atr(14)


//Entries and exits 
strategy.entry("Long", strategy.long, when=longCond, limit = emaSlow)
strategy.exit("Stop Loss/TP","Long", stop=stop_level_long, limit = take_level_long)
strategy.entry("Short", strategy.short, when=shortCond, limit = emaSlow)
strategy.exit("Stop Loss/TP","Short", stop=stop_level_short, limit = take_level_short)


```

> Detail

https://www.fmz.com/strategy/433587

> Last Modified

2023-11-28 16:54:14
