
> Name

Multi-Level-Oversold-Oscillator-Buy-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/167fdf3ee0eff086042.png)
[trans]

#### Overview
The multi-level overbought and oversold swing buying strategy is a long-term trading strategy designed specifically for bull market environments. This strategy uses a combination of the Stochastic and Stochastic RSI to find the best buying opportunities during market corrections. The strategy adopts a three-level pyramid method of adding positions to simulate the effect of dollar cost averaging (DCA), aiming to capture investment opportunities brought about by market corrections.
#### Strategy Principle
The core principle of this strategy is to "buy the dip" by identifying buy signals in oversold areas. Specifically:
1. Use the stochastic indicator (K) and the stochastic RSI indicator (Kr) with a longer period (66).
2. Set upward oversold line (20) and overbought line (99) to adapt to the bull market environment.
3. When K and Kr are below the oversold line (20) at the same time, the strategy begins to look for buying opportunities.
4. When the above conditions are met, once the Kr line crosses the D line, a buy signal is triggered.
5. Adopt a 3-level pyramid method to add positions, investing 20% ​​of the total account value each time.
6. When the Kr line reaches or exceeds the overbought line (99), close all positions and take profits.
The strategy does not set a stop loss, which reflects the firm confidence in the bull market trend.
#### Strategic Advantages
1. Follow the trend: Designed specifically for the bull market and make full use of callback opportunities in the upward trend.
2. Multiple confirmations: Combining two indicators to improve the reliability of entry signals.
3. Flexible position addition: The three-level pyramid method of position increase can not only reduce the average cost, but also control risks.
4. Strong adaptability: By adjusting parameters, it can adapt to different market environments.
5. Simple and intuitive: The strategy logic is clear and easy to understand and execute.
6. Automation-friendly: The code is concise and easy to implement automated transactions.
#### Strategy Risk
1. Risk of false breakthrough: False signals may be triggered frequently in a volatile market.
   Solution: Add additional trend confirmation indicators such as moving averages.
2. Risk of over-positioning: Continuous decline may lead to over-positioning.
   Solution: Set the maximum position limit or dynamically adjust the position increase ratio.
3. Risk of missing a rebound: Strict entry conditions may lead to missing a rapid rebound.
   Solution: Consider adding more sensitive short-term indicators as an aid.
4. Lack of stop-loss mechanism: You may suffer large losses in severe corrections.
   Solution: Introduce a dynamic stop loss mechanism based on volatility.
5. Parameter sensitivity: Strategy performance may be overly dependent on parameter settings.
   Solution: Conduct comprehensive parameter optimization and backtesting.
#### Strategy optimization direction
1. Dynamic parameter adjustment: Automatically adjust the periods of Stochastic and RSI according to market volatility.
   Reason: Improve the adaptability of strategies to different market environments.
2. Introduce trend filter: add long-term moving average as trend confirmation.
   Reason: Reduce false signals in the volatile market and improve the quality of entry.
3. Realize dynamic position addition: adjust the proportion of each position increase based on market volatility and account profit and loss.
   Reason: better control risks and improve capital utilization efficiency.
4. Add a profit-taking mechanism: when Kr reaches the overbought area, reduce positions in batches instead of closing all positions.
   Reason: Avoid missing big trends and improve long-term returns.
5. Integrate market sentiment indicators: such as VIX or capital flow indicators to optimize entry opportunities.
   Reason: Improve the sensitivity of the strategy to the market macro environment.
#### Summarize
The multi-level overbought and oversold shock buying strategy is a well-designed bull market trading system that effectively captures buying opportunities in market adjustments by combining the Stochastic and Stochastic RSI indicators. Its three-level pyramid method of adding positions not only simulates the advantages of the DCA strategy, but also provides more flexible position management. Although the strategy is optimistic in design, through reasonable risk management and continuous optimization, it has the potential to become a stable long-term investment tool. Future optimization directions should focus on improving the adaptability and risk control capabilities of strategies to cope with different market environments. Overall, this is a promising trading strategy that deserves further study and improvement.
|| 

#### Overview

The Multi-Level Oversold Oscillator Buy Strategy is a long-only trading system designed specifically for bullish market environments. This strategy utilizes a combination of the Stochastic Oscillator and the Stochastic Relative Strength Index (Stochastic RSI) to identify optimal buying opportunities during market corrections. The strategy employs a three-level pyramiding approach to emulate the effects of Dollar Cost Averaging (DCA), aiming to capitalize on market pullbacks.

#### Strategy Principles

The core principle of this strategy is to "buy the dips" by identifying buy signals in oversold territory. Specifically:

1. It uses a long-period (66) Stochastic Oscillator (K) and Stochastic RSI (Kr).
2. Sets upwardly biased oversold (20) and overbought (99) lines to suit bullish markets.
3. When both K and Kr fall below the oversold line (20), the strategy starts looking for buying opportunities.
4. Under these conditions, a buy signal is triggered when the Kr line crosses above the D line.
5. Implements a 3-level pyramiding approach, investing 20% of the account value each time.
6. All positions are closed for profit when the Kr line reaches or exceeds the overbought line (99).

The strategy does not employ a stop-loss, reflecting strong confidence in the bullish trend.

#### Strategy Advantages

1. Trend-following: Designed for bull markets, effectively utilizing pullbacks in uptrends.
2. Multiple confirmations: Combines two indicators to increase the reliability of entry signals.
3. Flexible position sizing: Three-level pyramiding approach lowers average cost while controlling risk.
4. High adaptability: Can be adjusted to different market conditions through parameter tuning.
5. Simplicity and clarity: Clear strategy logic that is easy to understand and execute.
6. Automation-friendly: Concise code, easily implementable for automated trading.

#### Strategy Risks

1. False breakout risk: May trigger frequent false signals in choppy markets.
   Solution: Incorporate additional trend confirmation indicators, such as moving averages.

2. Over-leveraging risk: Continuous declines may lead to excessive positions.
   Solution: Set maximum position limits or dynamically adjust the pyramiding ratio.

3. Missing rebound risk: Strict entry conditions may cause missing quick rebounds.
   Solution: Consider adding more sensitive short-term indicators as supplements.

4. Lack of stop-loss mechanism: May incur significant losses during severe corrections.
   Solution: Introduce a volatility-based dynamic stop-loss mechanism.

5. Parameter sensitivity: Strategy performance may overly depend on parameter settings.
   Solution: Conduct comprehensive parameter optimization and backtesting.

#### Strategy Optimization Directions

1. Dynamic parameter adjustment: Automatically adjust Stochastic and RSI periods based on market volatility.
   Reason: Enhance strategy adaptability to different market environments.

2. Introduce trend filters: Add long-term moving averages for trend confirmation.
   Reason: Reduce false signals in choppy markets and improve entry quality.

3. Implement dynamic position sizing: Adjust each pyramiding ratio based on market volatility and account performance.
   Reason: Better risk control and improved capital efficiency.

4. Enhance profit-taking mechanism: Implement partial position reduction when Kr reaches overbought territory instead of full closure.
   Reason: Avoid missing extended trends and improve long-term returns.

5. Integrate market sentiment indicators: Such as VIX or fund flow indicators to optimize entry timing.
   Reason: Increase strategy sensitivity to macro market environments.

#### Conclusion

The Multi-Level Oversold Oscillator Buy Strategy is an ingeniously designed bull market trading system that effectively captures buying opportunities during market corrections by combining Stochastic and Stochastic RSI indicators. Its three-level pyramiding approach not only emulates the advantages of DCA strategy but also provides more flexible position management. While the strategy design leans towards optimism, it has the potential to become a robust long-term investment tool with proper risk management and continuous optimization. Future optimization should focus on enhancing the strategy's adaptability and risk control capabilities to cope with various market environments. Overall, this is a promising trading strategy worthy of further research and improvement.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-06-29 00:00:00
end: 2024-07-29 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © aeperalta
 
//@version=5
strategy("Buy The Dips [aep]", overlay=false, pyramiding = 3)

//-------  strategy details ------------ {
// The strategy is to buy the dips by entering the market in the territory of oversold
// When both Stochastic (K) and Stochastic RSI (Kr) are below OS line is time to look for 
// crossovers in the Stochastic RSI indicator and buy @ market
// Take profit will happend when Kr is way up near the 100% as Overbought territory
// Since we are buy dips of during bullmarkets, there is no stoploss
//}

 
// ------stochastics --------{
periodK = input.int(66, title="%K Length", minval=1)
smoothK = input.int(3, title="%K Smoothing", minval=1)
periodD = input.int(3, title="%D Smoothing", minval=1)

// classic stochastic
k = ta.sma(ta.stoch(close, high, low, periodK), smoothK)


// stochastic rsi
periodRSI = input(14)
rsi = ta.rsi(close,periodRSI)
kr = ta.sma(ta.stoch(rsi, rsi, rsi, periodK), smoothK)
d = ta.sma(kr, periodD) 
 
// plots
OB = input.int(99, "Overbought")
OS = input.int(20, 'Oversold')

plot(k,'stochastic',color.white,2)
plot(kr, 'stochastic rsi', color.blue, 1)
plot(d, '%rsi D',color.maroon, 1 )

hline(OS, color = color.rgb(39, 230, 18), linestyle= hline.style_dashed)
hline(OB, color = color.rgb(229, 28, 18), linestyle= hline.style_dashed)
hline(100, color = color.red, linestyle= hline.style_dotted)
hline(0, color = color.green, linestyle= hline.style_dotted)

//}
// -------------- strategy excecution --------------- {

if  ta.crossover(kr, d) and kr < OS and k < OS
	strategy.entry("by the dip",strategy.long)
if kr >= OB
	strategy.close_all()

//}
```

> Detail

https://www.fmz.com/strategy/458170

> Last Modified

2024-07-30 15:45:44
