
> Name

MACD-RSI-Combo-Trend-Strategy MACD-RSI-Combo-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy integrates MACD and RSI indicators to determine the trend direction and overbought and oversold conditions to achieve trend following transactions. When the MACD line crosses the zero axis and the RSI line exceeds the overbought and oversold zone, go long or short.
## Strategy Principle
Main logic:
- Calculation of MACD lines and signal lines (EMA of MACD)
- Delta is the difference between the two, expressing changes in price momentum
- RSI to determine overbought and oversold conditions
- Go long when Delta crosses the zero axis and RSI is overbought (default 70)
- Go short when Delta crosses the zero line and RSI is oversold (default 30)
MACD determines the direction of price momentum, and RSI determines overbought and oversold conditions. The combination of the two can filter out many false signals.
## Strategic Advantages
- Fusion of two indicators to filter signals
- MACD determines price momentum, RSI determines overbought and oversold
- Configurable parameters, suitable for different market environments
- Clear trend trading strategy ideas
## Strategy Risk
- A single indicator combination may have limited effect
- Without stop loss, single loss cannot be controlled
- The size of the open position is not taken into account
Countermeasures:
- Test the combination of other indicators to find the best combination
- Add trailing stop or hard stop
- Set positions based on fund size or volatility
## Strategy optimization direction
- Test MACD combinations with other indicators
- Optimize parameters and improve stability
- According to the trend filtr signal, avoid false breakthroughs
- Use progressive stop loss to protect profits
- Use machine learning to determine signal quality
## Summarize
This strategy integrates MACD and RSI indicators to judge the trend, and the idea is clear and reliable. Stability can be improved through parameter optimization, stop loss strategies, intelligent filtering and other methods. It provides an effective trend trading model that is worthy of further expansion and improvement.
|| 

## Overview

This strategy combines the MACD and RSI indicators to determine trend direction and overbought/oversold levels for trend trading. It goes long/short when MACD crosses zero line and RSI is beyond overbought/oversold thresholds.

## Strategy Logic

Main logic:

- Calculate MACD line and Signal line (EMA of MACD) 

- Delta is their difference, expressing price momentum change

- RSI to gauge overbought/oversold conditions

- Go long when Delta crosses above zero line and RSI overbought (default 70) 

- Go short when Delta crosses below zero line and RSI oversold (default 30)

MACD for momentum direction, RSI for overbought/sold - combo filters many false signals.

## Advantages

- Combines two indicators for filtered signals 

- MACD measures momentum, RSI measures overbought/sold

- Configurable parameters for different markets

- Clear trend trading strategy rationale 

## Risks

- Limited effectiveness from single indicator combo 

- No stop loss, unable to control loss per trade

- Does not consider position sizing 

Mitigations:

- Test other indicators, find optimal combinations

- Add trailing or hard stop loss

- Position size based on account size or volatility 

## Enhancement Opportunities

- Test MACD with other indicator combos

- Optimize parameters for stability 

- Filter signals by trend to avoid false breakouts

- Use trailing stop loss to protect profits

- ML to judge signal quality

## Conclusion

This strategy combines MACD and RSI for solid trend determination. Stability can be improved through parameter optimization, stop loss, intelligent filters etc. It provides an effective trend trading framework for further enhancements.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|fastLength|
|v_input_2|26|slowlength|
|v_input_3|9|MACDLength|
|v_input_4|14|length_rsi|
|v_input_5|30|overSold|
|v_input_6|70|overBought|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 6h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("MACD RSI Strategy", overlay=true)

fastLength = input(12)
slowlength = input(26)
MACDLength = input(9)

MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD

// RSI



length_rsi = input( 14 )
overSold = input( 30 )
overBought = input( 70 )
price = close

vrsi = rsi(price, length_rsi)

//

if (not na(vrsi))
    if (crossover(delta, 0) and crossover(vrsi, overBought ))
        strategy.entry("MacdLE", strategy.long, comment="LE")
    if (crossunder(delta, 0) and crossunder(vrsi, overSold))
        strategy.entry("MacdSE", strategy.short, comment="SE")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)


```

> Detail

https://www.fmz.com/strategy/427483

> Last Modified

2023-09-21 15:40:02
