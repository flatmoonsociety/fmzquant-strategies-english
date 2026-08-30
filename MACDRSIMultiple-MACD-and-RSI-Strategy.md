
> Name

Multiple-MACD-and-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The multi-MACD and RSI strategy comprehensively uses the signals of the MACD indicator and the RSI indicator. It goes long when the slow line and the fast line are both positive crosses and the RSI does not enter the overbought zone. It goes short when the slow line and the fast line are both dead crosses and the RSI enters the oversold zone to capture the mid- to long-term trend of the price.
## Principle
This strategy uses two MACD indicators to provide signals. The parameters of one MACD indicator are fast line length 10, slow line length 22, and MACD line length 9; the parameters of the other MACD indicator are fast line length 21, slow line length 45, and MACD line length 20. A buy signal is generated when the fast lines of both MACDs cross above the slow lines, and a sell signal is generated when both fast lines of MACD cross below the slow lines.
At the same time, the RSI indicator is combined to determine whether it has entered the overbought and oversold area. The RSI parameter is set to 14, the overbought line is set to 70, and the oversold area is set to 20. You can buy when the RSI is below the overbought area, and sell when the RSI is above the oversold area.
Only when two MACD indicators generate buy signals at the same time and RSI is not overbought, a buy is issued; only when two MACD indicators generate sell signals at the same time and RSI enters the oversold zone, a sell is issued.
## Advantages
The biggest advantage of the multi-MACD and RSI strategy is that it can use the dual MACD indicator to filter out some false signals, and only enter the market when both MACD indicators send signals, which can reduce unnecessary transactions, reduce the frequency of transactions, and increase the probability of profit.
In addition, by combining the RSI indicator to determine overbought and oversold conditions, you can avoid going long or short when the price trend is too strong, and reduce the risk of losses.
The combination of dual MACD filtering and RSI judgment allows the strategy to only trade in trending markets and obtain better mid-trend profits.
## Risk
Multiple MACD and RSI strategies also have certain risks. Double MACD filtering may miss the opportunity when the price starts to reverse, causing losses to expand. When both MACDs are crossing and the RSI is not overbought, going long may have missed the price bottom and resulted in losses.
In addition, the MACD indicator itself is very sensitive to the characteristics of the trading market. Under different trading cycles and market environments, the parameters of MACD need to be adjusted to exert its effectiveness. If the parameters are set improperly, it is easy to generate wrong signals and cause losses.
In addition, the RSI indicator may generate multiple overbought and oversold signals, and entering the market prematurely before waiting for the RSI to completely reverse will also increase losses.
## optimization
This strategy can consider optimizing the following points:
1. Optimize the MACD parameters, change the parameters of the fast line and the slow line, find the best MACD parameter combination under different trading varieties and periods, and improve the effectiveness of the signal.
2. Adjust RSI parameters, appropriately shorten or relax the overbought and oversold range of RSI, and optimize the timing of entry.
3. Add a stop-loss strategy to stop the loss and exit when the loss reaches a certain percentage to avoid further expansion of gaming losses.
4. Consider adding breakthrough points and other auxiliary judgments to further confirm that the trend is established before entering the market.

## Summarize
The multi-MACD and RSI strategy comprehensively uses dual MACD indicators and RSI indicators to improve the effectiveness of signals and obtain better returns in medium and long-term trend markets. However, this strategy also has certain risks. It is necessary to further test and optimize the MACD parameters and RSI parameters, and add auxiliary strategies to control risks before the strategy can be applied to actual transactions.
|| 

## Overview

The Multiple MACD and RSI strategy comprehensively utilizes the signals of the MACD indicator and the RSI indicator. It goes long when both fast and slow lines of the two MACD cross up and RSI is below overbought level, and goes short when both fast and slow lines of the two MACD cross down and RSI enters oversold level, aiming to capture mid-long term trends.

## Principle 

This strategy employs two MACD indicators to generate signals. One MACD has parameters of fast length 10, slow length 22 and MACD length 9. The other MACD has parameters of fast length 21, slow length 45 and MACD length 20. It generates a buy signal when fast lines of both MACDs cross above their slow lines, and a sell signal when fast lines of both MACDs cross below their slow lines. 

In the meantime, it incorporates the RSI indicator to judge overbought and oversold conditions. The RSI parameter is set to 14, with overbought level at 70 and oversold level at 20. It can buy when RSI is below overbought level and sell when RSI is above oversold level.

Only when both MACDs generate a buy signal and RSI is not overbought, a long entry will be triggered. Only when both MACDs generate a sell signal and RSI enters oversold zone, a short entry will be triggered.

## Advantages

The biggest advantage of this strategy is that it utilizes dual MACD indicators to filter out some false signals and only enters when both MACDs give out signals. This reduces unnecessary trades and trading frequency while improving profitability rate.

Also, incorporating RSI to judge overbought/oversold conditions avoids going long/short when the price is already trending strongly, thus reducing loss risks.

Combining dual MACD filtering and RSI judgment, this strategy only trades in trending markets and can gain decent profits from mid-term trends.

## Risks

This strategy also possesses some risks. The dual MACD filtering may miss the timing of price reversal and lead to enlarged losses. Going long when both MACDs are positive crossing and RSI is not overbought yet may have already missed the bottom and lead to losses.

Moreover, MACD itself is very sensitive to the characteristics of the trading markets. MACD parameters need to be adjusted for different trading cycles and market environments to take effect. If the parameters are not set properly, it is prone to generating false signals and causing losses.

In addition, RSI may produce multiple overbought/oversold signals. Prematurely entering before RSI fully reverses can add to the losses.

## Optimization

Some aspects can be considered to optimize this strategy:

1. Optimize MACD parameters, adjust fast/slow line lengths to find optimal MACD parameter combinations for different products and timeframes, improving signal efficiency. 

2. Fine tune RSI parameters, moderately shorten or widen overbought/oversold levels to optimize entry timing.

3. Add stop loss strategies to cut losses when drawdown reaches a certain level, avoiding further losses.

4. Consider adding auxiliary judgements like breakout points to further confirm the trend before entering.

## Conclusion

The Multiple MACD and RSI strategy combines dual MACD indicators and RSI indicator to improve signal validity, and can gain decent profits from mid-long term trending moves. But it also bears some risks. MACD and RSI parameters need further testing and optimizing, and risk control mechanisms need to be added, before the strategy can be applied to actual trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|fastLength|
|v_input_2|22|slowlength|
|v_input_3|9|MACDLength|
|v_input_4|21|fastLength2|
|v_input_5|45|slowlength2|
|v_input_6|20|MACDLength2|
|v_input_7|14|Length|
|v_input_8|20|Oversold|
|v_input_9|70|Overbought|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-30 00:00:00
end: 2023-10-07 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("MACDbl RSI", overlay=true)

fastLength = input(10)
slowlength = input(22)
MACDLength = input(9)

MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = sma(MACD, MACDLength)
delta = MACD - aMACD

fastLength2 = input(21)
slowlength2 = input(45)
MACDLength2 = input(20)

MACD2 = ema(open, fastLength2) - ema(open, slowlength2)
aMACD2 = sma(MACD2, MACDLength2)
delta2 = MACD2 - aMACD2

Length = input(14, minval=1)
Oversold = input(20, minval=1)
Overbought = input(70, minval=1)
xRSI = rsi(open, Length)


if (delta > 0) and (year>2015) and (delta2 > 0) and (xRSI < Overbought)
    strategy.entry("buy", strategy.long, comment="buy")

if (delta < 0) and (year>2015) and (delta2 < 0) and (xRSI > Oversold)
    strategy.entry("sell", strategy.short, comment="sell")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/428693

> Last Modified

2023-10-08 14:03:47
