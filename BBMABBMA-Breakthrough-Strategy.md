
> Name

BBMA Breakthrough StrategyBBMA-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](https://www.fmz.com/upload/asset/773df181c666570e12.png)

[trans]

### Overview
The BBMA breakout strategy is a strategy that uses a combination of Bollinger Bands and moving averages to generate trading signals. This strategy uses both the upper and lower Bollinger Bands and the crossover between the Fast Moving Average and the Normal Moving Average as entry signals. Go long when the price breaks through the upper line of the Bollinger Bands and the fast moving average crosses the ordinary moving average. Go short when the price falls below the lower line of the Bollinger Bands and the fast moving average crosses the ordinary moving average.
### Strategy Principles
This strategy is mainly based on Bollinger Bands Theory and Moving Average Theory. Bollinger Bands are widely used in quantitative trading, and they consist of a middle track, an upper track, and a lower track. The middle rail is a simple moving average of the closing price within a certain period, and the upper and lower rails are the distance of one standard deviation univ from the middle rail. If the price is close to the upper band, it means the market may be overbought, and if the price is close to the lower band, it means the market may be oversold.
The moving average is also a commonly used technical indicator, mainly used to judge the trend and the inflow and outflow of main funds. The fast moving average can capture price changes faster, while the ordinary moving average is more stable. When the fast moving average crosses the ordinary moving average, it is a golden cross, which means that the market may enter an upward trend.
This strategy comprehensively considers the Bollinger Band theory and the moving average theory, and determines the market buying and selling points through the combined signal of the price breaking through the upper and lower Bollinger Bands and the specific intersection of the fast and slow moving averages, and serves as an entry signal to guide the trading direction.
### Strategic Advantages
1. Using Bollinger Band theory to determine market buying and selling points is helpful in seizing price reversal opportunities.
2. Comprehensively consider the cross signals of the fast moving average and the ordinary moving average to avoid false breakthroughs.
3. Establishing stop-loss and stop-profit points is conducive to strict risk control.
4. The backtest data is sufficient, the yield is high, and the winning rate is good.
### Strategy Risk
1. Improper setting of Bollinger Band parameters may lead to incorrect trading signals.
2. Lagging in the fast and slow moving average crossover signals may lead to unnecessary losses.
3. The stop loss point setting is too loose and cannot effectively control a single loss.
4. The market may experience extreme conditions, causing the stop loss point to be breached.
### Strategy optimization direction
1. Optimize Bollinger Band parameters and find the best combination.
2. Evaluate whether to introduce other auxiliary indicators to filter signals.
3. Test and optimize the trailing stop loss strategy to further control risks.
4. Evaluate whether to use time or price breakout methods to stop losses.
### Summarize
The BBMA breakthrough strategy integrates the use of Bollinger Bands and moving average theory to determine trading signals. This strategy has better stability, higher returns, and controllable risk levels. Through parameter optimization and risk control methods, the strategy winning rate and return rate can be further improved. This strategy is suitable for medium and long-term position traders.
||
### Overview
The BBMA breakthrough strategy is a strategy that uses a combination of Bollinger Bands and moving averages to generate trading signals. The strategy uses both the upper and lower rails of the Bollinger Bands and the crossovers between the fast moving average and the ordinary moving average as entry signals. Go long when the price breaks through the upper rail of the Bollinger Bands and the fast moving average crosses above the ordinary moving average, and go short when the price breaks through the lower rail of the Bollinger Bands and the fast moving average crosses below the ordinary moving average.

### Strategy Principle  

This strategy is mainly based on the theory of Bollinger Bands and the theory of moving averages. Bollinger Bands are widely used in quantitative trading, consisting of middle rail, upper rail and lower rail. The middle rail is the simple moving average of closing prices over a certain period, and the upper and lower rails are respectively one standard deviation away from the middle rail. If the price is close to the upper rail, it indicates that the market may be overbought. If the price is close to the lower rail, it indicates that the market may be oversold.

The moving average is also a commonly used technical indicator, mainly used to judge the trend and judge the inflow and outflow of main funds. The fast moving average can capture price changes faster, and the ordinary moving average is more stable. When the fast moving average crosses above the ordinary moving average, it is called the golden cross, indicating that the market may enter an upward trend.  

This strategy takes into account both Bollinger Bands theory and moving averages theory. It determines market entry and exit points through the combination signal of price breaking through the upper and lower rails of Bollinger Bands and special crossovers between fast and slow moving averages, and uses it as the entry signal to guide trading direction.

### Advantages of the Strategy

1. Using Bollinger Bands theory to determine market entry and exit points is conducive to capturing price reversal opportunities.  

2. Comprehensively considering the crossover signals of fast and ordinary moving averages avoids false breakouts.

3. Establishing stop loss and take profit points helps to strictly control risks.  

4. Sufficient backtest data, high rate of return, good win rate.

### Risks of the Strategy  

1. Improper parameter settings of Bollinger Bands may cause wrong trading signals.

2. The lag of moving average cross signals may lead to unnecessary losses. 

3. The stop loss point is set too loose to effectively control single losses.

4. Extreme market conditions may break through stop loss points.

### Optimization Directions of the Strategy

1. Optimize Bollinger Bands parameters to find the best combination.  

2. Evaluate whether to introduce other auxiliary indicators to filter signals.

3. Test and optimize moving stop loss strategies to further control risks.  

4. Evaluate whether to use time or price breakthrough methods for stop loss.

### Summary  

The BBMA breakthrough strategy integrates the use of Bollinger Bands and moving average theory to judge trading signals. This strategy has good stability, high returns, and controllable risk levels. Parameters optimization and risk control measures can further improve the win rate and return on investment of the strategy. The strategy is suitable for medium and long term position holders.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|BBMA Length|
|v_input_2|2|Deviation|
|v_input_3|50|EMA Period|
|v_input_4|10|Fast EMA Period|
|v_input_float_1|true|Stop Loss Percentage|
|v_input_float_2|2|Take Profit Percentage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-17 00:00:00
end: 2023-12-24 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("BBMA Strategy", shorttitle="BBMA", overlay=true)

// Input parameters
length = input(20, title="BBMA Length")
deviation = input(2, title="Deviation")
ema_period = input(50, title="EMA Period")
fast_ema_period = input(10, title="Fast EMA Period")
stop_loss_percentage = input.float(1, title="Stop Loss Percentage") / 100
take_profit_percentage = input.float(2, title="Take Profit Percentage") / 100

// Calculate Bollinger Bands and MTF MA
basis = ta.sma(close, length)
dev = deviation * ta.stdev(close, length)
upper_bb = basis + dev
lower_bb = basis - dev
ema = ta.ema(close, ema_period)
fast_ema = ta.ema(close, fast_ema_period)

// Entry conditions
long_condition = ta.crossover(close, upper_bb) and ta.crossover(close, fast_ema) and close > ema
short_condition = ta.crossunder(close, lower_bb) and ta.crossunder(close, fast_ema) and close < ema

// Signals for entry and exit with stop loss and take profit
if (long_condition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", from_entry="Buy", stop=close * (1 + stop_loss_percentage), limit=close * (1 + take_profit_percentage))

if (short_condition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", from_entry="Sell", stop=close * (1 - stop_loss_percentage), limit=close * (1 - take_profit_percentage))
```

> Detail

https://www.fmz.com/strategy/436483

> Last Modified

2023-12-25 11:33:50
