
> Name

Vortex-and-RSI-Stock-Long-only-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the turbine indicator to determine the direction of the market trend and identify long opportunities. It also uses the RSI indicator as a filter, combined with stop-loss and take-profit management, to build a relatively complete long stock trading strategy system. This strategy can effectively identify the rising trend of stocks and can customize parameters for optimization.
## Strategy Principle
1. Calculate the positive indicator VIP and the negative indicator VIM of the turbine indicator.
2. When VIP crosses VIM and the closing price is higher than the previous day's highest price, it is judged as a buy signal.
3. Calculate the RSI indicator value. When the RSI indicator falls below 70, it is judged to be a sell signal.
4. When VIM crosses VIP and the closing price is lower than the previous day's lowest price, it is also judged as a sell signal.
5. Set the stop-loss and stop-profit rules: the stop-loss range is stop_loss% of the initial capital, and the take-profit range is Target_profit% of the initial capital.
The turbine indicator can effectively determine the long and short trends, combine with the RSI indicator to avoid the risk of overheating, and cooperate with stop loss and profit management to make the entire trading system more robust and complete.
## Strategic advantage analysis
1. The turbine indicator accurately determines the trend direction and the signal is clear.
2. The RSI indicator can effectively avoid the risk of overheating and prevent chasing highs.
3. Dynamic stop loss and take profit set a clear risk-reward ratio.
4. The stop-loss and take-profit parameters can be adjusted according to the market, which is highly adaptable.
5. The strategy signal rules are simple, clear and easy to implement.
6. It can be expanded to other indicators and has large room for optimization.
## Risk Analysis
1. There is a lag in the turbine indicator and opportunities may be missed.
2. If the stop loss range is too small, you may be trapped.
3. Excessive take-profit range may limit profits.
4. Over-reliance on RSI can easily lead to a dead cross.
5. The impact of transaction costs is not considered.
6. The warehouse management module is not set up.
## Strategy optimization direction
1. Test and optimize the parameters of turbine indicator and RSI.
2. Try other indicators such as OBV instead of or combined with the turbine indicator.
3. Optimize stop loss and take profit strategies, such as trailing stop loss, shrinking stop loss, etc.
4. Add a position management module to limit single losses.
5. Consider combining more indicators, such as KD, MACD, etc., to determine the timing of entry.
6. Use machine learning algorithms to find better parameters.
7. Increase fundamental factors and improve the strategic winning rate.
## Summarize
This strategy integrates the trend judgment of the turbine indicator and the overheating control of the RSI indicator to form a relatively stable long stock trading strategy. Stop-loss and take-profit settings also make risk and return controllable. By further optimizing parameters and adding new modules, the strategy can be made more robust and suitable for real trading. This strategy has strong trend tracking capabilities and room for expansion, and is suitable for active investors.
|| 

## Overview 

This strategy uses the Vortex indicator to determine market trend direction and identify long opportunities. It adds RSI filter and stop loss/take profit management to build a more complete stock long-only trading system. It can effectively identify uptrends and allows parameter customization.

## Strategy Logic

1. Calculate the positive VIP and negative VIM of Vortex indicator. 

2. When VIP crosses above VIM, and close is higher than previous high, a buy signal is generated.

3. Calculate RSI values. When RSI crosses below 70, a sell signal is generated.

4. When VIM crosses below VIP, and close is lower than previous low, a sell signal is also triggered.

5. Set stop loss at stop_loss% of initial capital, and take profit at Target_profit% of initial capital.

Vortex indicator judges bullish/bearish trends well. Adding RSI prevents overheating risks. Stop loss/take profit adds robustness.

## Advantage Analysis

1. Vortex accurately identifies trends with clear signals.

2. RSI avoids overheating risks and chasing tops.

3. Dynamic stops set predefined risk/reward ratio.

4. Adjustable stops fit different market environments.

5. Simple clear rules, easy to implement.

6. Expandable with other indicators.

## Risk Analysis

1. Vortex has lagging effect, may miss opportunities. 

2. Stop loss too small may cause whipsaws.

3. Take profit too large may limit profits.

4. RSI over-reliance causes failures.

5. Trading costs not considered.

6. No position sizing rules.

## Optimization Directions

1. Test and optimize parameters for Vortex and RSI.

2. Try combining Vortex with OBV etc.

3. Enhance stop loss strategies like trailing stop, chandelier exit etc.

4. Add position sizing module to limit single trade loss.

5. Consider more filters like KD, MACD for entry timing.

6. Utilize machine learning for better parameter optimization. 

7. Add fundamental factors to improve win rate.

## Conclusion

This strategy integrates Vortex for trend and RSI for overheating control into a stable long-only stock system. The stop loss/take profit settings also keep risk manageable. Further improvements in parameter tuning and new modules can make it more robust for live trading. With strong trend following capacity and expandability, this strategy suits active investors well.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|vortex period|
|v_input_2|14|RSI period|
|v_input_3|7|Stop loss %|
|v_input_4|16|Target Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by Sauciusfinance 
////////////////////////////////////////////////////////////
strategy(title="Vortex and RSI ts 2020",calc_on_order_fills=true,calc_on_every_tick =true, initial_capital=20000,commission_value=.25,overlay = true,default_qty_type = strategy.cash, default_qty_value = 20000)
//inputs////////////////////////
n = input(title="vortex period",type=input.integer, defval = 14)
m = input(title = "RSI period", type=input.integer, defval = 14)
// CALCULATIONS *** ///////
VMP = sum( abs( high - low[1]), n )
VMM = sum( abs( low - high[1]), n )
STR = sum( atr(1), n )
VIP = VMP / STR
VIM = VMM / STR
// bring the lines in the panel below, add another panel with RSI
plot(VIP, title="VI +", color=#311B92)
plot(VIM, title="VI -", color=#FF006E)

// RSI on total price, always
totalprice = (high + low+close + open)/4
myrsi = rsi(m, totalprice)
strategy.initial_capital = 50000
//// TRADING SYSTEM CODE //// 
entryl = crossover(VIP, VIM) and close >= high[1] 
strategy.entry("Long", true, when=entryl, comment = "Go!")
exit1 = crossover(VIM, VIP) and close <= low[1]
strategy.close("Long", when=exit1, comment = "Vortex down")
exit2 = crossunder(myrsi, 70)
strategy.close("Long", when=exit2, comment = "RSI down")
//money management
stop_loss=input(7, "Stop loss %", minval = 1, step = 1)
sl = -1*stop_loss/100*strategy.initial_capital
close_Stop = strategy.openprofit < sl
strategy.close("Long", when = close_Stop)
Target_profit=input(16, "Target Profit %", minval = 1, step = 1)
tp = Target_profit/100*strategy.initial_capital
close_Target = strategy.openprofit > tp
strategy.close("Long", when = close_Target)


```

> Detail

https://www.fmz.com/strategy/427311

> Last Modified

2023-09-19 22:01:09
