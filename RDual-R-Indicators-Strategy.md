
> Name

Dual-R-Indicators-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the double R indicator combined with the SMA moving average to achieve trend judgment and trading signal generation for USDJPY. Among them, the double R indicators include Parabolic SAR stop loss indicator and RSI overbought and oversold indicator. This strategy uses the double R indicator to determine market trends and overbought and oversold conditions, and combines the SMA moving average to determine buying and selling points.
## Principle
This strategy mainly uses three technical indicators:
1. Parabolic SAR Stop Loss Indicator: This indicator shows the stop loss point of the current price and can be used to determine the price trend and possible reversal points. In the code, the SAR value is calculated and plotted through parameter settings.
2. RSI overbought and oversold indicator: This indicator determines whether the price is overbought and oversold. The RSI parameters and overbought and oversold thresholds are set in the code, and the RSI curve is calculated and drawn.
3. SMA moving average: Calculate and draw the SMA moving average of the 10-day line and the 20-day line.
Combining the three indicators, the logic for determining buying and selling points is as follows:
When the closing price crosses the 182-day SMA, the 10-day SMA crosses the 20-day SMA, and the RSI indicator breaks through the 30-day oversold line from low to upward, go long;
When the closing price crosses below the 182-day SMA, the 10-day SMA crosses below the 20-day SMA, and the RSI indicator breaks below the 70 overbought line from high, go short.
## Advantages
This strategy has the following advantages:
1. Using the double R indicator to determine the trend direction can effectively confirm trading signals. The RSI indicator determines overbought and oversold conditions, and the SAR stop-loss indicator determines the turning point of the price trend. The combination of the two is more reliable.
2. Combining the SMA moving average for market entry can effectively filter out false breakthroughs. Relying solely on the RSI indicator can easily lead to missed trading opportunities. Adding SMA moving average judgment can reduce this risk.
3. Select the time period of 15 minutes to capture short-term price breakthroughs in a timely manner. Intraday trading is mainly about capturing short-term trends, and you can fully seize opportunities in 15 minutes.
4. The backtest data is sufficient to fully verify the effectiveness of the strategy. Two and a half months of 15-minute data can basically judge the reliability of this strategy.
## Risk
There are also some risks with this strategy:
1. The backtest data time period is too short and cannot fully represent future performance. Only 2 and a half months of data is not enough to fully judge the long-term effectiveness of the strategy.
2. The RSI indicator has a problem of wrong triggering. The RSI indicator itself may deviate from the actual price trend, resulting in false signals.
3. There is a lag problem in the SMA moving average. The SMA moving average responds slowly to price changes and may miss better entry points.
4. Short-term trading within the day is risky. Intraday trading is greatly affected by news events, and there is the risk of overnight positions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Increase the backtest historical data time period to make it longer, such as increasing it to 6 months or 1 year, to more fully verify the strategy effect.
2. Try to use other indicators to replace or combine RSI indicators, such as KDJ, MACD, etc., to make the signal more reliable.
3. Try to optimize the SMA moving average combination, such as changing to a 5-day and 20-day combination, or adding a longer-term moving average to make the breakthrough more reliable.
4. Set up a stop-loss mechanism to control single losses. Such as setting intraday stop loss or trailing stop loss.
5. Optimize the take-profit strategy, such as moving take-profit or batch take-profit, to lock in more profits.
## Summarize
This strategy uses the double R indicator to determine overbought and oversold conditions as a whole, and combines it with SMA moving average filtering to implement the intraday USDJPY trading strategy. This strategy has the advantage of capturing short-term trends in a timely manner, but it also has risks such as insufficient backtest data. In the future, the strategy effect can be further improved by increasing the data time period, optimizing indicator parameters, and setting stop loss and profit.


||


## Overview

This strategy uses dual R indicators combined with SMA lines to determine trends and generate trading signals for USDJPY. The dual R indicators include Parabolic SAR trailing stop indicator and RSI overbought-oversold indicator. It judges trends and overbought-oversold situations through dual R indicators, and generates buy and sell signals with SMA lines.

## Principles 

The strategy mainly utilizes the following three technical indicators:

1. Parabolic SAR trailing stop indicator: It shows potential stop loss points and can be used to determine price trends and potential reversal points. The code calculates and plots SAR values based on parameter settings.

2. RSI overbought-oversold indicator: It judges whether prices are overbought or oversold. The code sets RSI parameters and overbought/oversold threshold values, and calculates and plots the RSI curve.

3. SMA lines: It calculates and plots the 10-day and 20-day SMA lines.

Combining the three indicators, the buy and sell point logic is as follows:

Go long when close goes above 182-day SMA line, 10-day SMA crosses above 20-day SMA, and RSI breaks through 30 oversold line from below. 

Go short when close goes below 182-day SMA line, 10-day SMA crosses below 20-day SMA, and RSI breaks through 70 overbought line from above.

## Advantages

The strategy has the following advantages:

1. Using dual R indicators to determine trend direction can effectively confirm trading signals. RSI for overbought-oversold and SAR for trend reversal work together for more reliability.

2. Adding SMA filter helps avoid false breakouts. Relying solely on RSI may miss opportunities, SMA adds confidence. 

3. 15-min timeframe captures short-term breakouts timely. For intraday trading, 15-min is optimal to capitalize on short-term trends.

4. 2.5 months of 15-min backtest data sufficiently validates strategy. 15-min data over 2.5 months can basically determine reliability.

## Risks

There are some risks:

1. Limited backtest data cannot fully represent future performance. 2.5 months is insufficient to determine long-term validity.

2. RSI may give false signals, deviating from actual price moves.

3. SMA has lagging effect. It reacts slower to price changes, missing good entry points.

4. Intraday trading has higher risks. More impacted by news and overnight position risks.

## Optimization

Some ways to optimize the strategy:

1. Expand backtest timeframe to 6 months or 1 year for more sufficient validation.

2. Try other indicators like KDJ, MACD to complement or replace RSI for more reliable signals. 

3. Optimize SMA combinations, like 5-day and 20-day, or adding longer SMAs, for more solid breakouts.

4. Add stop loss mechanisms to control single trade loss, like intraday or trailing stop loss. 

5. Optimize take profit, like trailing stop or partial profits, to lock in more gains.

## Conclusion

The strategy overall uses dual R indicators for overbought-oversold and SMA for filters to implement USDJPY intraday trading. It has advantage of catching short-term trends but also risks like insufficient backtest data. It can be further improved by expanding timeframe, optimizing parameters, adding stop loss/take profit.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|start|
|v_input_2|0.02|increment|
|v_input_3|0.2|maximum|
|v_input_4|6|RSI Period Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-08 00:00:00
end: 2023-10-08 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Chrome", overlay=false, pyramiding = 1, commission_value = 0.01, currency = currency.USD, initial_capital = 1000)

// Parabolic Support And Resistance
start = input(0.02)
increment = input(0.02)
maximum = input(0.20)
sar = sar(start, increment, maximum)

//plot(sar, style = circles, linewidth = 2)

// (v)RSI
RSIlength = input(6,title="RSI Period Length") 
RSIoverSold = 30
RSIoverBought = 70
RSImid = 50
price = close
vrsi = rsi(price, RSIlength)
plot(vrsi)
a = hline(70)
b = hline(30)

strategy.entry("buy", strategy.long,  when = close > sma(close, 182) and sma(close, 10) > sma(close, 20) and crossover(vrsi, RSIoverSold))
strategy.entry("short", strategy.short,  when = close < sma(close, 182)  and sma(close, 10) < sma(close, 20) and crossunder(vrsi, RSIoverBought))














```

> Detail

https://www.fmz.com/strategy/428801

> Last Modified

2023-10-09 15:46:05
