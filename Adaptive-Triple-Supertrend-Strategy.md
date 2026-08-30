
> Name

Adaptive-Triple-Supertrend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/173bb9ea90d80c37f90.png)
[trans]
## Overview
The Adaptive Triple Supertrend Strategy is a trading method for tracking market trends that brings together the power of three supertrend indicators to identify underlying market trends and profit from them. This strategy focuses on adaptability and precision, with the goal of providing traders with clear entry and exit signals while effectively managing risk. By combining multiple supertrend indicators and their defined parameters, this strategy seeks to capture trends in a variety of market conditions, making it a versatile tool for traders seeking profit opportunities in both traditional and cryptocurrency markets.
## Strategy Principle
The main idea behind the adaptive triple super trend strategy is to combine multiple super trend indicators to identify market trends, enter long when the trend is consistent, and exit the position when the trend reverses.
Specifically, this strategy uses three super trend indicators, which are:
1. Super trend 1: ATR period=12, factor=3
2. Super trend 2: ATR period=10, factor=1
3. Super trend 3: ATR period=11, factor=2
When these three super trend indicators show a long signal (green) at the same time, the strategy will open a long position within a specific date range (January 1, 2023 to October 1, 2023); when any super trend indicator shows a short signal (red), the strategy will close the position and exit the long position. In addition, the strategy also sets a 10% take-profit and 1% stop-loss to lock in profits and manage risks.
Therefore, the specific trading logic of this strategy is:
1. When three super trend indicators show long signals at the same time, open a long position within the date range
2. When holding a long position, monitor the Super Trend Indicator for reversal signals.
3. If any super trend indicator turns short, it will trigger a closing signal and exit the long position.
4. When the take profit reaches 10% or the stop loss reaches 1%, exit the position with take profit or stop loss.
With such trading logic, the strategy aims to capture profits from the bullish trend within a specific date range, while controlling downside risk through stop losses.
## Advantage Analysis
The Adaptive Triple Super Trend Strategy has several key advantages:
1. Combining multiple super trend indicators can more accurately judge market trends and reduce false signals.
2. The super trend itself has the function of filtering noise, which can reduce the impact of shocks on trading.
3. Through parameter settings, you can adapt to different market environments
4. Set up take-profit and stop-loss at the same time, which can stop loss in time when the trend reverses and avoid unnecessary risks of DLayer
5. You can obtain excess returns in a bull market and avoid a sharp decline in a bear market.
Overall, this strategy is very suitable as a core trend following strategy to assist manual trading. It can provide high-quality trading signals, control risks while making profits in the general trend, and is an important tool for quantitative trading.
## Risk Analysis
Although the Adaptive Triple Super Trend Strategy has many advantages, there are also certain risks that need to be noted, mainly including:
1. When the market experiences extreme fluctuations, it may cause the super trend indicator to generate false signals.
2. Improper setting of strategy parameters will also affect strategy performance
3. Stop loss settings that are too small may not be able to effectively control risks.
4. Improper timing of long entry may also lead to losses
These risks can be mitigated by:
1. Combine with other indicators to determine market fluctuations and trends
2. Optimize parameter settings to adapt to different market environments
3. Appropriately enlarge the stop loss range to ensure that the stop loss is effective
4. Use more stable indicators to determine specific entry opportunities
## Optimization direction
As a general trend following strategy, the adaptive triple super trend strategy still has a lot of room for optimization. The main directions are:
1. Dynamically optimize the parameters of the super trend indicator to better adapt to the market
2. Add other auxiliary indicators to judge entry opportunities
3. Further optimize the settings of take profit and stop loss based on the backtest results.
4. Try to use breakthroughs as entry signals and use super trends to determine the trend direction.
5. Encapsulate the strategy into a function to facilitate calling in other strategies
Through these optimizations, the strategy can maintain stable performance in more market environments and obtain higher profitability factors. This is also a future research direction.
## Summarize
The Adaptive Triple Super Trend Strategy is a very valuable quantitative strategy. It combines multiple super trend indicators to determine market trends, and sets stop-profit and stop-loss controls to control risks, aiming to steadily track the market trend and obtain excess returns. Although there are some potential risks, these risks can be well mitigated through parameter optimization and auxiliary indicators. This strategy can be used alone as a core strategy or in combination with other strategies. It also has a lot of room for optimization and is expected to achieve better performance. Therefore, this is a high-quality strategy worthy of continued research and application.
||

## Overview  

The Adaptive Triple Supertrend Strategy is a trend-following trading approach that harnesses the power of three Supertrend indicators to identify potential market trends and capitalize on them. With a focus on adaptability and precision, this strategy aims to provide traders with clear entry and exit signals while managing risk effectively. By combining multiple Supertrend indicators with defined parameters, the strategy seeks to capture trends across various market conditions, making it a versatile tool for traders seeking profitable opportunities in both traditional and cryptocurrency markets.

## Strategy Logic  

The core idea behind the Adaptive Triple Supertrend Strategy is to combine multiple Supertrend indicators to identify market trends, go long when the trends agree, and exit positions when trends reverse.   

Specifically, the strategy utilizes three Supertrend indicators:  

1. Supertrend 1: ATR Period = 12, Factor = 3
2. Supertrend 2: ATR Period = 10, Factor = 1  
3. Supertrend 3: ATR Period = 11, Factor = 2

When all three Supertrend indicators simultaneously show a bullish (green) signal, the strategy will open a long position within a defined date range (Jan 1, 2023 to Oct 1, 2023). When any one of the Supertrend indicators shows a bearish (red) signal, the strategy will exit the long position. In addition, the strategy sets a 10% take profit and 1% stop loss to lock in profits and manage risk.

So the specific trade logic is:  

1. Open long when all three Supertrends show bullish signals within the date range   
2. Monitor Supertrends for reversal signals while in a long position
3. Exit long if any Supertrend turns bearish  
4. Take profit at 10% or stop loss at 1%  

This logic aims to capture profits from bull trends within the date range while controlling downside risk with the stop loss.  

## Advantage Analysis   

The Adaptive Triple Supertrend Strategy has several key advantages:

1. Combining multiple Supertrends gives more accurate trend judgement and reduces false signals  
2. Supertrend itself filters noise, reducing oscillation impacts   
3. Parameters can be tuned to adapt to different market environments  
4. Take profit and stop loss settings lock in profits and cut losses when trends reverse  
5. Can capture outsized gains in bull markets and avoid huge drawdowns in bear markets

In summary, this strategy works excellently as a core trend following strategy to assist manual trading. By providing high quality trade signals to profit from major trends while controlling risk, it is an important tool for quantitative trading.  

## Risk Analysis  

Despite its many strengths, the Adaptive Triple Supertrend Strategy has some key risks to note:  

1. Huge market swings can cause wrong signals  
2. Poor parameter tuning impacts performance   
3. Small stop loss may fail to control risk  
4. Bad long entry timing can lead to losses  

These risks can be mitigated by:

1. Adding other indicators to judge oscillations   
2. Optimizing parameters for different markets
3. Increasing stop loss percentage to ensure effectiveness  
4. Using more stable indicators for entry signals  

## Enhancement Opportunities

As a versatile trend following strategy, the Adaptive Triple Supertrend has much room for enhancement:  

1. Dynamic optimization of Supertrend parameters   
2. Adding other indicators to improve entry timing   
3. Further optimizing take profit and stop loss based on backtests
4. Trying breakout for entry with Supertrend for trend direction  
5. Packaging strategy as function for easy plug-and-play
  
With these optimizations, the strategy can maintain steady performance across more market environments and achieve higher profit factors. This presents exciting research directions going forwards.  

## Conclusion  

The Adaptive Triple Supertrend Strategy is a valuable quantitative strategy. By combining multiple Supertrend indicators to determine trends and setting take profit/stop loss to control risk, it aims to steadily track major trends for outsized gains. Despite some risks, these can be alleviated via parameter optimization and auxiliary indicators. The strategy can be used standalone or combined with others. It also has significant enhancement potential for even better performance. As such, this is a quality strategy worth continual research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|3|Factor 1|
|v_input_1|12|ATR Length 1|
|v_input_float_2|true|Factor 2|
|v_input_2|10|ATR Length 2|
|v_input_float_3|2|Factor 3|
|v_input_3|11|ATR Length 3|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-25 00:00:00
end: 2024-01-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Custom Supertrend Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=15, shorttitle="Supertrend Strategy")

// Define the parameters for Supertrend 1
factor1 = input.float(3.0, "Factor 1", step = 0.01)
atrPeriod1 = input(12, "ATR Length 1")

// Define the parameters for Supertrend 2
factor2 = input.float(1.0, "Factor 2", step = 0.01)
atrPeriod2 = input(10, "ATR Length 2")

// Define the parameters for Supertrend 3
factor3 = input.float(2.0, "Factor 3", step = 0.01)
atrPeriod3 = input(11, "ATR Length 3")

[_, direction1] = ta.supertrend(factor1, atrPeriod1)
[_, direction2] = ta.supertrend(factor2, atrPeriod2)
[_, direction3] = ta.supertrend(factor3, atrPeriod3)

// Define the start and end dates as Unix timestamps (in seconds)
start_date = timestamp("2023-01-01T00:00:00")
end_date = timestamp("2023-10-01T00:00:00")

// Determine Buy and Sell conditions within the specified date range
in_date_range = true
buy_condition = direction1 > 0 and direction2 > 0 and direction3 > 0 and in_date_range
sell_condition = direction1 < 0 or direction2 < 0 or direction3 < 0

// Track the position with a variable
var isLong = false

if buy_condition and not isLong
    strategy.entry("Long Entry", strategy.long)
    isLong := true

if sell_condition and isLong
    // Define take profit and stop loss percentages
    take_profit_percentage = 10 // Increased to 10%
    stop_loss_percentage = 1

    // Calculate take profit and stop loss levels
    take_profit_level = close * (1 + take_profit_percentage / 100)
    stop_loss_level = close * (1 - stop_loss_percentage / 100)

    // Exit the long position with take profit and stop loss
    strategy.exit("Take Profit/Stop Loss", from_entry="Long Entry", limit=take_profit_level, stop=stop_loss_level)
    isLong := false
```

> Detail

https://www.fmz.com/strategy/440109

> Last Modified

2024-01-26 16:33:37
