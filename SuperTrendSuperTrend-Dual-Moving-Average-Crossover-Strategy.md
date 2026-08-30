
> Name

SuperTrend Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a double moving average crossover strategy based on the SuperTrend indicator. The SuperTrend indicator consists of two moving averages whose crossover serves as a buy and sell signal. The strategy belongs to the trend following type of strategy.
## Strategy Principle
1. Calculate the fast line demaFast, the formula is: 2*ema5 - ema(ema5,5)
2. Calculate the slow line demaSlow, the formula is: 2*ema2 - ema(ema2,2)
3. The fast line is composed of the 5-day EMA, which responds to price changes more quickly; the slow line is composed of the 2-day EMA, which responds to price changes more slowly.
4. When the fast line breaks through the slow line from below, a buy signal is generated; when the fast line breaks through the slow line from above, a sell signal is generated.
5. Using the intersection of two moving averages with different response speeds to judge changes in price trends is a typical trend following strategy.
6. Actual execution of trades based on buy and sell signals.
The core idea of ​​this strategy is simple and clear. It can adapt to markets of different cycles by adjusting the moving average parameters. It is a common trend following strategy.
## Advantage Analysis
1. Using double moving average crossover to determine changes in trend direction is a simple and practical technical indicator.
2. The fast and slow line parameters are adjustable and can be optimized for different cycles.
3. The strategy signals are clear and the transaction execution is simple.
4. The backtest function is complete and can verify the effect of the strategy.
5. The visual interface intuitively displays the intersection situation.
6. The strategic ideas are easy to understand and suitable for novices to learn.
## Risk Analysis
1. Lagging signals or false signals may appear when double moving averages cross. You can adjust parameters appropriately or add filter conditions to improve it.
2. Unable to effectively handle consolidation or market shocks, and easy to stop losses. A trend judgment mechanism can be added for optimization.
3. There is limited room for optimization of backtest parameters, and the actual results need to be verified.
4. Pay attention to the impact of transaction costs on profitability.
## Optimization direction
1. Test parameter combinations with different moving average lengths to find the best match.
2. Add other indicators for signal filtering, such as KDJ indicators, etc.
3. Add a stop-loss mechanism to control single losses.
4. Added position management function, using different transaction percentages for different market conditions.
5. Optimize fund management strategies and set risk indicators such as profit-loss ratio.
6. Consider adding algorithms such as machine learning for parameter optimization or signal judgment.
## Summarize
The SuperTrend double moving average crossover strategy is a simple trend following strategy that adapts to different cycles through parameter adjustment and is highly practical. Combining other technical indicators for optimization, expansion and risk control can further enhance the stability of the strategy. This strategy is easy to learn and has great potential for expansion. It is a very practical quantitative trading strategy idea.
|| 

## Overview

This is a dual moving average crossover strategy based on the SuperTrend indicator. SuperTrend consists of two moving averages, their crossover acts as buy and sell signals. The strategy belongs to the trend following category.

## Strategy Logic 

1. Calculate the fast line demaFast, formula: 2*ema5 - ema(ema5,5)

2. Calculate the slow line demaSlow, formula: 2*ema2 - ema(ema2,2)  

3. The fast line consists of 5-day EMA, more responsive to price changes; the slow line consists of 2-day EMA, lagging in response.

4. When fast line crosses above slow line from below, generate buy signal; when crossing below from above, generate sell signal.

5. Using crossover of two lines with different response speeds to determine trend change is a typical trend following strategy.

6. Execute trades based on buy and sell signals.

The core logic is simple and clear. By adjusting the MA parameters it can adapt to different cycle markets, a common trend following strategy.

## Advantage Analysis

1. Using dual MA crossover to determine trend change is a simple and practical technique.

2. Fast and slow line parameters are adjustable for optimizing different periods.

3. Clear signals and simple execution.

4. Complete backtest functionality to verify strategy. 

5. Intuitive visual interface showing crossover.

6. Easy to understand logic, suitable for beginners.

## Risk Analysis

1. Dual MA crossover may have lagging signals or false signals. Can improve by adjusting parameters or adding filters.

2. Ineffective in range-bound or choppy markets, prone to stop loss. Can add trend mechanism.

3. Limited optimization space in backtest, real trading effect untested.

4. Need to watch transaction cost impact on profitability.

## Optimization Directions

1. Test different MA length combinations to find optimal match.

2. Add other indicators for signal filtering, e.g. KDJ.

3. Add stop loss mechanism to control single trade loss amount. 

4. Add position sizing to use different percentages for different market conditions.

5. Optimize money management, set risk metrics like profit ratio.

6. Consider machine learning algorithms for parameter optimization or signal forecasting.

## Summary
This SuperTrend dual MA strategy is a simple trend following system adaptable to different cycles. Combining with other technical indicators and risk control can further enhance stability. Easy to learn with great potential for expansions, it is a highly practical quant trading strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

strategy(title = "SuperTrend", shorttitle = "BTC")
ema5=ta.ema(close, 5)
ema2=ta.ema(close, 2)
 
demaFast =  request.security(syminfo.tickerid, "30", 2 * ema5 - ta.ema(ema5, 5)  )

plotchar((2 * ema5 - ta.ema(ema5, 5)), "d", "", location = location.top)
plotchar(demaFast, "fast", "", location = location.top)

demaSlow  = request.security(syminfo.tickerid,"30", 2 * ema2 - ta.ema(ema2, 2)  )
plotchar(demaSlow, "slow", "", location = location.top)

buy = ta.crossover(demaSlow, demaFast)
sell = ta.crossunder(demaSlow, demaFast)
strategy.entry("BUY", strategy.long, 1, when = buy)
strategy.entry("SELL", strategy.short, 1, when = sell )
```

> Detail

https://www.fmz.com/strategy/427306

> Last Modified

2023-09-19 21:38:06
