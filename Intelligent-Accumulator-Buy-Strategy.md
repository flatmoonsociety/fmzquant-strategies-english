
> Name

Intelligent-Accumulator-Buy-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/185e0a3fa28ad1a1e7d.png)
[trans]
## Overview
The Smart Accumulation Buy Strategy is a proof-of-concept strategy. It is a combination of a recursive buying strategy and entries and exits based on technical analysis.
This strategy allocates part of the capital and continues to add to the position if the technical analysis conditions are valid. Use technical analysis conditions for exit to define your exit strategy.
You can add positions to losing positions to achieve a lower average price, or you can choose a more aggressive approach that allows you to add positions to profitable positions.
You can choose to exit with all profits, or exit in multiple portions of the same size.
You can also decide whether to allow exit conditions to close the position with a loss, or to require a minimum take profit percentage.
The strategy contains default technical analysis entry and exit conditions, which are only used to demonstrate the idea of ​​​​the strategy, but the ultimate purpose of the script is to delegate entry and exit decisions to external sources.
Internal conditions use an RSI length of 7 to cross 1 times the standard deviation Bollinger Bands below for entry, and above for exit.
The order quantity can be controlled through parameters in the settings:
- Adjust the number of dips
- Adjust the equity percentage used
- Ensure that the number of dips × the percentage of equity used equals 100 to prevent excessive use of equity (unless leverage is used)
This script is intended as an alternative to daily or weekly recursive buying, but it may also be profitable on lower timeframes depending on the accuracy of technical analysis conditions.
This strategy is called "smart" because the most common approach to recursive buying is regardless of the decision: buy in any case with a specified frequency. This strategy still performs recursive buying, but filters out some potentially bad entries that may unnecessarily delay seeing the position move into profit. The second reason is that an exit strategy is set up from the beginning, and recursive buying itself does not provide this function.
## Strategy Principle
This strategy uses the intersection of the RSI indicator and the Bollinger Bands to time entries and exits. Specifically, bearish entries are made when the RSI is below the lower band, and bullish exits are made when the RSI is above the upper band.
In addition, the strategy also provides settings for bargain hunting and exiting in batches. The sum of the number of dips and the equity percentage used each time should equal 100 to prevent excessive use of funds. You can choose to allow additional positions to be added to profitable positions, or to only increase positions to loss-making positions to achieve a decrease in the average price.
When leaving the market, you can choose to exit with all profits, or exit with partial profits in batches according to the set ratio. In addition, you can also set a minimum take-profit percentage, and profits below this percentage will not trigger exit.
Overall, this strategy combines recursive buying and technical analysis indicators to achieve more stable cumulative buying by filtering out some error signals. At the same time, it also sets up a flexible exit mechanism so that parameters can be adjusted according to one's own risk preference.
## Advantage Analysis
Compared with the traditional recursive buying strategy, the biggest advantage of this strategy is that there are technical indicators as a reference for entry and exit, which can filter out some false signals. This is in contrast to daily and weekly buying without decision-making. The specific advantages are as follows:
1. Use RSI and Bollinger Bands to determine the timing of entry and avoid chasing high positions at unfavorable times.
2. The exit conditions are clear, there are take-profit and stop-loss standards, and you will not hold positions aimlessly.
3. Dip buying parameters can be adjusted as needed to achieve more flexible position control.
4. You can choose to only add positions in losing positions or continue to add positions in profitable positions.
5. You can choose to exit with all profits or exit with partial profits in batches
6. Minimum profit percentage setting to avoid premature exit
In general, this strategy achieves the effect of regular position additions of recursive buying, and at the same time increases the technical indicator judgment of entry and exit. You can adjust parameters according to your own preferences, reduce the risk of blindly opening positions, and improve profit efficiency.
## Risk Analysis
Although this strategy sets up technical indicator filtering and a flexible opening and closing mechanism to reduce risks, any strategy inevitably has certain risks. The main risks include:
1. The probability that the indicator sends a wrong signal may miss the best entry or exit opportunity.
2. The number of positions added and the proportion of funds are improperly set, resulting in the risk of excessive positions
3. The market changes drastically in a short period of time, and the indicators fail to respond in time and send signals.
4. Taking profit and leaving the market too early or too late will affect profit efficiency.
The corresponding solutions are as follows:
1. Use multiple indicators in combination to reduce the probability of false signals
2. Carefully test and evaluate parameter settings to avoid the risk of over-positioning
3. Combined with real-time signals of shorter period indicators as auxiliary judgment
4. Test and optimize take-profit and exit parameters to improve stable profitability
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize or replace technical indicators to improve the accuracy of entry and exit. Combinations of different parameters or indicators can be tested to select more reliable signals.
2. Add a stop loss strategy. The current strategy does not set a stop loss. You can set a stop loss level based on retracement or other criteria to control the maximum loss.
3. Dynamically adjust the increase in position. The amount of funds added to each position can be adjusted in real time based on the number of positions or market volatility, and the amount of additional positions can be reduced when volatility is high.
4. Integrate algorithmic trading. The current strategy consists of simple indicators, and it is possible to add algorithm models such as machine learning to judge the market and improve decision-making.
5. Optimize parameter settings. Continuously optimize parameters such as the proportion of funds for each additional position and the percentage of take-profit and exit. The goal is to pursue higher returns while controlling risks.

## Summarize
The intelligent cumulative buying strategy retains the advantages of regular position additions of the recursive buying strategy through technical indicator filtering, and at the same time sets a clear stop-profit, stop-loss and exit mechanism to avoid the disadvantages of blindly building positions and holding positions without goals. The strategy can highly customize the opening and exit parameters according to personal risk preferences, which has great advantages for long-term position holders.
Of course, the strategy also has a certain probability of signal errors and the risk of improper setting of PARAMETERSNTTTT, which needs to be solved by continuing to optimize indicators and parameters as well as auxiliary stop loss means. Overall, this strategy has formed an important evolution from recursive buying to intelligent cumulative buying, providing investors with a relatively complete and controllable long-term position plan.
||

## Overview

The Intelligent Accumulator Buy Strategy is a proof of concept strategy. It combines recurring buy-in with technical analysis-based entries and exits.

The strategy will allocate a portion of the funds and continue to increase positions as long as the technical analysis condition is valid. Use the exit technical analysis condition to define your exit strategy.

You can add to losing positions to average down, or choose a more aggressive approach that allows adding to winning positions.

You can choose to take full profit or distribute your exits into multiple take profits of the same size.

You can also decide whether to allow your exit conditions to close your position at a loss or require a minimum take profit percentage.

The strategy contains default technical analysis entry and exit conditions just to showcase the idea, but the final intent of this script is to delegate entries and exits to external sources.

The internal conditions use RSI length 7 crossing below the 1 standard deviation Bollinger Bands for entries and above for exits.

To control the number of orders, adjust the parameters in Settings:
- Adjust pyramiding
- Adjust percentage of equity
- Make sure pyramiding *% equity equals 100 to prevent overuse of equity (unless using leverage)

The script is designed as an alternative to daily or weekly recurring purchases, but depending on the accuracy of your technical analysis conditions, it may also prove profitable at lower timeframes.

The reason the script is called Intelligent is because the most common recurring buy does not involve any decision making: buy no matter what with a certain frequency. This strategy still performs recurring purchases but filters out some potential bad entries that can unnecessarily delay seeing the position profitable. The second reason is also having an exit strategy in place from the start, which no recurring buy option offers out of the box.

## Strategy Principles 

The strategy determines entries and exits based on the crossover of the RSI indicator with the Bollinger Bands. Specifically, when the RSI is below the lower rail, look for short entries, and when the RSI is above the upper rail, look for long exits.

In addition, the strategy provides settings for pyramiding and batched exits. The sum of the number of pyramiding and the percentage of equity used each time should equal 100 to prevent overuse of funds. You can choose to allow continued pyramiding on winning positions or only pyramiding on losing positions to achieve average down.

When exiting, you can choose to take full profit or exit in batches according to the set percentage. In addition, the minimum profit percentage can be set to avoid exits if the profit is lower than that percentage.

Overall, the strategy combines recurring purchases and technical analysis indicators to achieve more stable pyramiding by filtering out some wrong signals, while setting up flexible exit mechanisms that can be adjusted according to one's own risk appetite.

## Advantage Analysis

Compared with traditional recurring purchase strategies, the biggest advantage of this strategy is that both entries and exits have technical indicators as references, which can filter out some wrong signals, in contrast to the daily and weekly purchases without any decision making. The specific advantages are:

1. Use RSI and Bollinger Bands to determine entry timing to avoid chasing highs  
2. Clear exit conditions with profit taking and stop loss standards instead of holding positions indefinitely  
3. Pyramiding parameters can be adjusted as needed for more flexible position sizing  
4. Option to only add to losing positions or pyramid winners as well
5. Take full profit or scale out in batches  
6. Minimum profit percent avoids premature exits

In summary, the strategy realizes the periodic pyramiding effect of recurring purchases while increasing the technical indicator judgment for entries and exits, allows parameters adjustment according to one's own preferences, reduces the risk of blind entries, and improves profit efficiency.

## Risk Analysis

Although the strategy sets technical indicators filtering and flexible pyramiding/exit mechanisms to reduce risks, there are still inevitable risks for any strategy. The main risks include:

1. Probability of wrong signals from the indicators, which may cause missing the best entry or exit timing  
2. Inappropriate setting of pyramiding times and capital allocation leading to oversized position risks  
3. Market fluctuates violently in the short term while indicators fail to respond in time  
4. Premature or belated profit-taking exits impacting profitability   

The corresponding solutions are:

1. Use multiple indicators combination to reduce errors  
2. Carefully test and evaluate parameters to avoid over leveraging  
3. Incorporate real-time signals from shorter-period indicators as auxiliary judgment
4. Test and optimize profit-taking parameters to improve steady profitability

## Optimization Directions   

The strategy can be further optimized in the following aspects:

1. Optimize or replace technical indicators to improve entry/exit accuracy. Different parameters or combinations can be tested to choose more reliable signals.  
2. Add stop loss strategy. Currently no stop loss is configured. Loss standards can be set based on drawdown or other metrics to control maximum loss.
3. Dynamically adjust pyramiding magnitude. The funds added on each pyramid can be adjusted in real time based on the number of positions or market volatility. Reduce pyramiding in high volatility environments.  
4. Integrate algorithmic trading. The current strategy consists of simple indicators. Machine learning models can potentially be incorporated for higher level decision making.
5. Optimize parameter settings. Continuously optimize parameters like pyramiding percentages, profit taking percentages etc. with the goal to pursue higher returns while controlling risks.

## Conclusion  

The Intelligent Accumulator Buy Strategy retains the periodic pyramiding advantage of recurring purchases while filtering entries and exits with technical indicators and setting clear profit taking/stop loss exit mechanisms, avoiding the disadvantages of blind entries and indefinite holdings. The strategy allows high customization of pyramiding and exit parameters based on personal risk preference, thus very advantageous for long-term holders.

Of course, there are still risks of signal errors and inappropriate parameters, which needs to be addressed through continued optimization of indicators and parameters as well as auxiliary stop loss means. Overall, the strategy forms an important evolution from recurring purchases to intelligent accumulators, providing investors a relatively comprehensive and controllable long-term holding solution.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|false|Add while in profit|
|v_input_bool_2|false|extLong|
|v_input_source_1_close|0|entry: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|false|Required profit % to exit|
|v_input_float_2|100|% exit per candle|
|v_input_bool_3|false|extShort|
|v_input_source_2_close|0|exit: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-19 00:00:00
end: 2024-02-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TheTradingParrot

//@version=5
strategy("TTP Intelligent Accumulator", overlay=true)

maxEntries = 0.0

if not na(maxEntries[1])
    maxEntries := maxEntries[1]

rsi = ta.rsi(close, 7)
rsima = ta.sma(rsi, 14)
bbstd = ta.stdev(rsi, 14)

// plot(rsi)
// plot(rsima)
// plot(rsima - bbstd)
// plot(rsima + bbstd)

intEntry = rsi < rsima - bbstd
intExit = rsi > rsima + bbstd

maxEntries := math.max(strategy.opentrades, maxEntries)
plot(maxEntries, "maxEntries")

addWhileInProfit = input.bool(false, "Add while in profit")

extLong = input.bool(false, "", inline = "long")
entry = input.source(close,"entry", inline = "long") == 1

if not extLong
    entry := intEntry
longCondition = entry and (strategy.opentrades == 0 or (not addWhileInProfit or close < strategy.position_avg_price))


if (longCondition)
    strategy.entry("long", strategy.long)

minProfit = input.float(0.0, "Required profit % to exit")
exitPxcandle = input.float(100.0,"% exit per candle")

extShort = input.bool(false, "", inline = "exit")

exit = input.source(close,"exit", inline = "exit") == 1
if not extShort
    exit := intExit

shortCondition = exit
if (shortCondition and strategy.opentrades > 0)
    strategy.close("long", qty_percent = exitPxcandle)

plot(strategy.position_avg_price, "Avg")
```

> Detail

https://www.fmz.com/strategy/442835

> Last Modified

2024-02-26 13:59:57
