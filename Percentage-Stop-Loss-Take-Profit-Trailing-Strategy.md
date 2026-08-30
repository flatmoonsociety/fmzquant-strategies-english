
> Name

Percentage-Stop-Loss-Take-Profit-Trailing-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a simple trend following strategy that uses SMA moving average to determine the trend direction and sets a percentage stop loss and take profit to lock in profits and control risks. Belongs to the trailing stop strategy type.
## Strategy Principle
This strategy first calculates the SMA with a length of 200 days. When the price crosses the moving average, it is judged that the trend has started and the market is entered long. After entry, the strategy uses a fixed percentage stop loss point, such as 2% below the entry price; it also sets a fixed percentage stop profit point, such as 1% above the entry price. As soon as the price touches one of these levels, the strategy closes the corresponding position.
Specifically, the strategy uses the intersection of the close price and the 200-day SMA as a trading signal. When the close price crosses the SMA moving average, enter the market long. After entering the market, the strategy records the entry price and calculates the stop loss line = entry price * (1 - stop loss percentage); the take profit line = entry price * (1 + take profit percentage). If the price breaks below the stop loss line or above the take profit line, close the corresponding long order.
In this way, the strategy can achieve profits as long as the price moves in the correct direction; if a loss occurs, it can also be exited through stop loss to limit the amount of loss. By adjusting the stop-loss and take-profit percentages, you can control the return-risk characteristics of the strategy.
## Advantage Analysis
- Simple operation and easy to implement
Using SMA moving average to judge the trend, percentage take profit and stop loss are very simple and direct, with low technical threshold and easy to implement.
- Possibility to limit losses per order
By setting a stop loss point in advance, the loss of each order can be controlled within a predetermined percentage, which is helpful for risk control.
- Trailing stop loss, lock in profit
The take-profit point will move upward as profits increase, which can help the strategy lock in profits instead of stopping losses with reversals.
- Customizable profit and loss characteristics
By adjusting the take-profit and stop-loss percentages, you can freely define the risk-return characteristics of the strategy.
## Risk Analysis
- Easily trapped in volatile markets
In the oscillatory range where the trend is not obvious, the stop loss point may be triggered frequently, causing too many small losses.
- Moving average systems tend to lag
The SMA moving average itself lags behind the price and may miss the best entry point of the trend.
- Transaction costs are not considered
Smaller take profit and stop loss settings will increase the frequency of transactions without taking into account the actual transaction costs.
- Percent stop loss does not take into account fluctuations
Percent stop loss settings are static and do not take into account changes in market volatility. It is easy to be broken through during large fluctuations.
## Optimization direction
- Optimize parameters to adapt to market characteristics
Adjust the moving average parameters, find the best balance point, and test different take profit and stop loss percentages.
- Dynamically adjust stop loss based on volatility indicators
According to the latest market volatility, the stop loss percentage is dynamically adjusted to reduce the probability of the stop loss being breached.
- Backtesting taking into account actual transaction costs
Add costs such as transaction slippage and handling fees for backtesting, and optimize the take-profit settings.
- Multi-time backtesting and optimization
Conduct backtests during periods of high activity and low activity to find the optimal parameters for each period.
## Summarize
This strategy integrates moving average trend judgment and percentage stop-profit and stop-loss management of profit and loss. It is simple and easy to implement, and can freely define the income and risk characteristics. However, there is room for optimization in its trading signals and stop loss settings. It is necessary to consider factors such as volatility adaptive stop loss and transaction costs for optimization and adjustment, and strive to obtain stable returns on a simple basis.
||


## Overview 

This is a simple trend following strategy that uses SMA to determine trend direction and sets percentage-based stop loss and take profit to lock in profits and control risk. It belongs to the moving stop loss strategy category.

## Strategy Logic

The strategy first calculates a 200-day SMA line. When price crosses above the SMA line, it signals an uptrend and goes long. After entering, the strategy uses a fixed percentage stop loss level, such as 2% below entry price, and a fixed percentage take profit level, such as 1% above entry price. It will close the position when either level is touched.

Specifically, the strategy uses close price crossing above the 200-day SMA as the trading signal. When close goes above SMA, it enters long. After entry, the strategy records entry price, and calculates stop loss = entry price * (1 - stop loss %); take profit = entry price * (1 + take profit %). If price drops below stop loss or rises above take profit, it will close the long position.

This way, the strategy can lock in profit as long as price moves in the right direction. If a loss occurs, it will be limited by the stop loss. By adjusting the percentages, profit and risk can be customized.

## Advantage Analysis

- Simple to implement

Using SMA for trend and percentage stop loss/take profit is straightforward and easy to implement.

- Limits loss per trade

The pre-set stop loss keeps the loss below a fixed percentage, helping to control risk.

- Trailing stop locks in profit

Take profit level moves up with profit increase, helping to lock in gains instead of being stopped out.

- Customizable profit/loss characteristics 

The percentages can be adjusted to define profit and risk parameters.

## Risk Analysis

- Whipsaws in ranging market

In choppy range-bound markets, stop loss may be frequently hit leading to small losses.

- SMA lags price

SMA itself lags price, can miss best entry timing.

- Ignores trading costs

Small stop/take profit settings increase frequency, without considering trading costs.

- Static percentage stop loss 

Percentage stop loss does not adapt to volatility changes. Easily taken out during big moves.

## Improvement Directions

- Optimize parameters for market

Adjust SMA parameters, test different stop/take percentages to find optimal balance.

- Dynamic stop based on volatility

Adjust stop percentage based on recent volatility to lower chance of stop out.

- Backtest with real trading costs

Incorporate slippage, commission costs for backtest to optimize take profit.

- Multi-session backtests

Separately backtest on high and low activity sessions to find best parameters.

## Summary

This strategy combines SMA for trend and percentage stop/take for profit management in a simple format while allowing profit/risk tuning. But its signals and stop setting can be improved. Aspects like volatility adaptive stops, trading costs etc should be considered to achieve steady results on a simple basis.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|SMA Lookback Period|
|v_input_2|2|Stop Loss %|
|v_input_3|true|Take Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-25 00:00:00
end: 2023-09-24 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Stop Loss Example: Simple Stoploss", overlay=true)

sma_per = input(200, title='SMA Lookback Period', minval=1)
sl_inp = input(2.0, title='Stop Loss %', type=float)/100
tp_inp = input(1.0, title='Take Profit %', type=float)/100

sma = sma(close, sma_per)

stop_level = strategy.position_avg_price * (1 - sl_inp)
take_level = strategy.position_avg_price * (1 + tp_inp)

strategy.entry("Simple SMA Entry", strategy.long, when=crossover(close, sma))

strategy.exit("Stop Loss/TP","Simple SMA Entry", stop=stop_level, limit=take_level)

plot(sma, color=orange, linewidth=2)
plot(stop_level, color=red, style=linebr, linewidth=2)
plot(take_level, color=green, style=linebr, linewidth=2)
```

> Detail

https://www.fmz.com/strategy/427821

> Last Modified

2023-09-25 18:09:14
