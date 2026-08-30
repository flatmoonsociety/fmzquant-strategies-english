
> Name

Momentum-Breakthrough-EMA-Strategy based on momentum breakout EMA strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fb59654b99268ddf7a.png)
[trans]

## Overview
This strategy is a trend following strategy. It detects changes in price momentum and enters the market when it breaks through the moving average. The goal is to capture the trend of the stock price.
## Strategy Principle
The core logic of this strategy is:
When today's closing price is higher than yesterday's highest price, and yesterday's highest price does not touch the 5-day EMA, a buy position is opened. This is a breakthrough signal, indicating that the stock price is breaking through upward.
After entering the market, set the stop loss to the lowest price of the previous K line and then drop 100 points. Take profit is the entry price multiplied by the set take profit and stop loss ratio (default is 2). If the price continues to rise, you can use a trailing stop to lock in larger profits.
The above is the basic trading logic of this strategy.
## Advantage Analysis
This strategy has the following advantages:
1. Capture the stock price trend and have great profit potential. It is especially suitable for continuous chasing up/down when the stock price enters the stage of accelerating rise or fall.
2. Use EMA filtering to avoid frequent opening of positions during shocks.
3. The breakthrough signal is clear and false breakthroughs are unlikely to occur.
4. Risk control is in place. Stop loss controls a single loss and ensures the safety of funds.
5. The strategy logic is simple and clear, easy to understand and optimize.
## Risk Analysis
There are also some risks with this strategy:
1. The strategy of chasing the rise and killing the fall carries the risk of missing the turning point of the market. It is necessary to pay attention to larger-level trend indicators and control the overall position.
2. If you use breakthroughs to enter the market, there may be a risk of false breakthroughs. This needs to be combined with volume analysis to verify the breakout signal.
3. Improper stop loss setting may cause the stop loss to be too broad or too rigid. This needs to be adjusted based on market volatility and personal risk appetite.
4. If the profit stop point is set too large, it may not be possible to obtain all the profits due to the price drop. This requires the appropriate use of trailing take profit to lock in profits.
## Optimization direction
This strategy can be further optimized from the following perspectives:
1. Optimize the settings of parameters, such as MA cycle, stop loss range, etc., to make them more consistent with different stocks and market environments. Parameter combinations can be tested using stepwise optimization and genetic algorithms.
2. Increase verification of trading volume. Trading volume can verify the validity of breakout signals. Volume breakouts can be set to filter entry signals.
3. Increase the judgment of large-level trends. Make sure to only trade against the larger trend. For example, a short-only strategy in a falling market.
4. Set a dynamic trailing stop. When the price reaches the target, move the stop loss line to lock in profits instead of setting a fixed take profit point. This can maximize trend profits.
5. Add machine learning algorithms and use neural networks or random forests to determine buy and sell signals. It can significantly improve the stability and winning rate of the strategy.
## Summarize
This strategy achieves the capture of stock price trends by detecting price momentum changes and combining EMA filtering and stop loss methods. There are certain advantages and room for improvement in this simple breakout system. We can enhance the strategy through parameter optimization, adding auxiliary indicators, and adjusting stop loss methods. This will make the strategy more robust and efficient in dealing with complex and volatile stock markets.
||

## Overview  

This strategy is a trend-following strategy that enters positions when price momentum changes and breaks through moving averages, aiming to capture trending moves in stock prices.

## Strategy Logic

The core logic of this strategy is:

When today's closing price is higher than yesterday's high price, and yesterday's high price did not touch the 5-day EMA line, go long. This is the breakthrough signal indicating the stock price is breaking out upwards.  

After entering, set the stop loss to the low of the previous bar minus 100 points. Take profit is set to the entry price multiplied by the configured risk-reward ratio (default is 2). If price continues going up, trailing stop can be used to lock in more profit.

The above covers the basic trading logic of this strategy.

## Advantage Analysis

This strategy has the following advantages:

1. Captures trending moves in stock prices with large profit potential. Particularly suitable for riding price momentum during accelerating up or down trends.  

2. Filters out choppy price action using EMA. Avoids over-trading in ranging markets.

3. Breakout signals are clear and robust. Reduces false breakouts.   

4. Good risk control. Stops loss on a per trade basis to protect capital.

5. Simple and clear strategy logic that is easy to understand and optimize.

## Risk Analysis  

There are also some risks to this strategy:

1. Chasing trends runs the risk of missing major market turning points. Needs to monitor higher timeframe trends and manage overall position size.

2. Breakout trading is prone to false breakout risks. Requires checking with volume analysis to confirm valid breakouts. 

3. Inappropriate stop loss placement can cause stops being too wide or too tight. Needs tuning based on market volatility and personal risk preferences.  

4. Profit targets set too high may not be reached if prices reverse. Should consider using trailing stops to lock in profits.

## Optimization Directions

Some ways this strategy can be further optimized:

1. Optimize parameters like MA periods, stop loss size etc. to fit different stocks and market conditions better. Stepwise optimization and genetic algorithms can test combinations of parameters.

2. Add volume confirmation. Volume can validate the authenticity of breakout signals. Can set volume breakouts to filter entry signals.

3. Monitor larger timeframe trends. Ensure trading in alignment with major trends. For example only trade short when in a downward trend. 

4. Use dynamic trailing stops. When price reaches targets, trailing stop moves to lock in profits instead of using fixed take profit points. This maximizes trend following profit.

5. Add machine learning algorithms like neural networks or random forests for trade signal generation. Can significantly improve strategy stability and win rate. 

## Summary  

This strategy captures trending moves by detecting price momentum changes, using EMA filter and stop loss methods. Though simple, this breakout system has advantages and room for improvement. We can make the strategy more robust and efficient by optimizing parameters, adding supporting indicators, adjusting stops etc. to handle complex and ever-changing market conditions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|Length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|false|Offset|
|v_input_2|2|Risk-Reward Ratio|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-29 00:00:00
end: 2024-02-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Custom Strategy", overlay=true)

len = input.int(9, minval=1, title="Length")
src = input(close, title="Source")
offset = input.int(0, title="Offset", minval=-500, maxval=500)

ema5 = ta.ema(src, len)

// Condition for Buy Entry
buy_condition = close > high[1] and high[1] < ema5

// Set Target and Stop Loss
risk_reward_ratio = input(2.0, title="Risk-Reward Ratio")
target_price = close + (high[1] - low[1]) * risk_reward_ratio
stop_loss_price = low[1] - 100

// Execute Buy Order
if (buy_condition)
    strategy.entry("Buy", strategy.long)

// Exit conditions
if (strategy.position_size > 0)
    strategy.exit("Take Profit/Stop Loss", from_entry="Buy", profit=target_price, loss=stop_loss_price)

// Plotting
plot(ema5, title="EMA", color=color.blue, offset=offset)
plotshape(series=buy_condition, title="Buy Entry Signal", color=color.green, style=shape.triangleup, size=size.small, location=location.belowbar)

```

> Detail

https://www.fmz.com/strategy/441086

> Last Modified

2024-02-05 14:51:12
