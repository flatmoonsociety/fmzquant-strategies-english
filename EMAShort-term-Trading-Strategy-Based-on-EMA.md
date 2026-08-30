
> Name

Short-term-Trading-Strategy-Based-on-EMA
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16468e1775ca361bdd4.png)
[trans]
## Overview
This strategy is based on the crossover principle of EMA and designs a short-term trading strategy. When the stock price has a certain degree of correction, appropriate short-term trading can be carried out in order to obtain better returns.
## Strategy Principle
This strategy uses 5 EMA moving averages with different parameters, specifically the 10-day line, the 20-day line, the 50-day line, the 75-day line and the 200-day line. The generation logic of its trading signals is:
1. When the price crosses the 75-day moving average and falls below the 50-day moving average, it is regarded as a short-term correction signal of a certain extent, and short selling can be considered;
2. After shorting, if the 10-day line crosses below the 20-day line, continue to hold short orders; when the 10-day line crosses above the 20-day line again, close the position and buy, ending this round of short-term trading.
Through such a trading logic design, it is possible to capture the large fluctuations in stock prices in the short term and earn the security price difference during the callback phase.
## Strategic Advantages
The biggest advantage of this strategy is that the trading signal generation is simple, clear and easy to implement. Trading decisions can be made simply by relying on the intersection of several moving averages. There is no need for complex models and large amounts of historical data, which reduces the difficulty of implementation.
In addition, the strategy uses multiple sets of EMA moving averages to combine, which can effectively filter market noise and identify the time points for short- and medium-term trend reversals, so as to make accurate trading decisions.
## Strategy Risk
The main risk of this strategy lies in the sharp fluctuations in stock prices in the short term. If the stock price rises or falls rapidly out of control, the stop loss or take profit line will be breached, resulting in larger losses. In addition, if the selected parameters are inappropriate, trading signals may be too frequent, which will also affect the strategic returns.
In order to control risks, the moving average parameters should be appropriately adjusted to maintain the trading frequency at a moderate level; at the same time, reasonable stop loss and stop profit ranges should be set to avoid excessive single losses. When faced with special market conditions, manual intervention is also required to suspend strategic trading.
## Strategy optimization
This strategy mainly optimizes the space in parameter adjustment. You can test more combinations of parameters to find the optimal parameter combination. For example, more average lines can be introduced, such as the 60-day line, the 120-day line, etc., to form a richer trading signal source.
In addition, optimization can also be carried out in dimensions such as stop loss and take profit. Appropriately relaxing the stop loss range may reduce the probability of wrong stop loss; tightening the stop loss range may improve profitability. The adjustment of these parameters requires selecting the optimal parameters based on the backtest results.
## Summarize
This strategy is relatively simple overall. Based on the EMA crossover, a simple and feasible short-term trading strategy is designed. This strategy has clear signals, is easy to implement, and can effectively capture trading opportunities brought about by short- and medium-term trend reversals. Through parameter adjustment and optimization of stop loss and take profit settings, this strategy can achieve better results.
||

## Overview

This strategy is designed with the crossover principles of EMA lines to make appropriate short-term trades and gain decent profits when prices fall back to some extent.

## Strategy Logic  

The strategy adopts 5 EMA lines with different parameters, specifically the 10-day, 20-day, 50-day, 75-day and 200-day lines. The logic for generating trading signals is:

1. When the price crosses above the 75-day line and falls below the 50-day line, it is considered a signal for a proper short-term pullback to take a short position.

2. After going short, if the 10-day line crosses below the 20-day line, continue holding the short position. When the 10-day line crosses back above the 20-day line, close the position to complete this round of short-term trade.

Through this logic design, major fluctuations of prices in the short run can be caught to gain from price spreads during pullbacks.

## Advantages

The biggest advantage of this strategy lies in its simple and clear signals that are easy to implement. Just by the crossover situation of several moving averages, trading decisions can be made smoothly, without complex models and loads of historical data, lowering the difficulty of implementation.

In addition, the combo use of multiple EMA lines helps filter out market noise effectively and spot the timing of mid-to-short term trend reversals precisely to make sensible trading decisions.

## Risks  

The major risk of this strategy comes from violent price swings in the short term. Uncontrolled sharp rises or falls may result in stop loss or take profit lines being broken, causing huge losses. Also, improper parameters may lead to overfrequent trading signals that undermine strategy profitability.

To control risks, parameters of moving averages should be adjusted appropriately to maintain signal frequency at a proper level. Reasonable stop loss and take profit ranges should also be set to avoid oversized losses per trade. Manual intervention is needed as well facing special market conditions, suspending strategy trading.

## Optimization  

The main optimization space lies in parameter tuning. More combinations can be tested to find the optimal parameter portfolio. For instance, more moving averages can be introduced like 60-day and 120-day lines to form a richer signal source.

Optimization can also be done around aspects like stop loss and take profit. Properly loosening the stop loss range may decrease the probability of wrong stops. Tightening take profit range could increase profitability. These parameter adjustments need to be based on backtest results for optima.

## Conclusion

To conclude, this strategy is fairly simple overall. Designed with basic EMA crossover signals, it shapes into a feasible short-term trading tactic. Its advantage lies in clear signals that are easy to carry out, which can effectively seize trading opportunities from mid-to-short term trend reversals. Further improvements can be achieved through parameter tuning and optimizing stop loss, take profit settings.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-13 00:00:00
end: 2024-02-19 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © theswissguy

//@version=5
strategy("Jan 2024 Daily (Short)", initial_capital = 10000, overlay=true, commission_value = 1)

// use closing prices as data source throughout calcs.
ema_source = close
price = close

// set up the EMA curves.
ema10 = ta.ema(ema_source, 10)
ema20 = ta.ema(ema_source, 20)
ema50 = ta.ema(ema_source, 50)
ema75 = ta.ema(ema_source, 75)
ema200 = ta.ema(ta.ema(ema_source, 200), 35)

plot(ema10, color=color.red, title="EMA10")
plot(ema20, color=color.orange, title="EMA20")
plot(ema50, color=color.green, title="EMA50")
plot(ema75, color=color.yellow, title="EMA75")
plot(ema200, color=color.blue, title="EMA200", linewidth = 4)

// if EMA50 <= price <= EMA75 AND EMA10 < EMA20 - sell
dailySellIndicator = ta.crossover(price, ema75) and ta.crossunder(price, ema50) and ta.crossunder(ema10, ema20) 
dailyBuyIndicator = ta.crossover(ema10, ema20)

if(dailySellIndicator)
    strategy.entry("daily", strategy.short)
else if(dailyBuyIndicator)
    strategy.entry("daily", strategy.long)


```

> Detail

https://www.fmz.com/strategy/442225

> Last Modified

2024-02-20 14:06:27
