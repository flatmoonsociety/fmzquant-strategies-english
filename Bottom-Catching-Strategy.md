
> Name

Bottom-Catching-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/146989f202a618da986.png)

[trans]

### Overview
This strategy utilizes the RSI and EMA indicators to determine entries and exits. It performs well in bear markets and can capture bottom rebound opportunities.
### Strategy Principles
The strategy is based on the following buy and sell conditions:
Buying conditions:
1. RSI < 40
2. RSI dropped 3 points from yesterday
3. The 50-day EMA crosses below the 100-day EMA
Selling conditions:
1. RSI > 65
2. The 9-day EMA crosses the 50-day EMA
In this way, you can buy during the decline, sell at the high during the rebound, and capture the bottom rebound opportunity.
### Advantage Analysis
This strategy has the following advantages:
1. Use RSI to capture oversold opportunities
2. EMA pattern to determine trend change points
3. The backtest results are good, especially in bear markets.
4. Configurable parameter adjustment strategy
### Risk Analysis
This strategy also has the following risks:
1. Improper parameter settings may lead to premature buying or delayed selling.
2. The rebound may not occur in time or be sustainable.
3. Transaction fees and slippage will also affect actual profits
The long-short pattern can be judged by adjusting parameter optimization strategies or combining other indicators.
### Optimization direction
This strategy can be optimized in the following directions:
1. Test parameter combinations according to different currencies
2. Judge the effectiveness of buying and selling signals based on changes in trading volume
3. Increase stop loss points to reduce the risk of single loss
4. Consider dynamically adjusting position size
### Summarize
The overall logic of this bottom-capturing strategy is clear and it can work well in a bear market. There is still plenty of room for parameter adjustment and optimization, and it is expected to obtain better backtest indicators. However, you also need to pay attention to risks during the actual offer process, and losses cannot be completely avoided.
||

### Overview

This strategy utilizes the RSI and EMA indicators to determine entries and exits. It performs well in bear markets and can catch bottom rebound opportunities.

### Strategy Logic  

The strategy is based on the following entry and exit conditions:


Entry conditions:
1. RSI < 40  
2. RSI is 3 points lower than previous day
3. 50-day EMA crosses below 100-day EMA

Exit conditions: 
1. RSI > 65
2. 9-day EMA crosses above 50-day EMA

This allows buying on dips and selling at highs during bounces, catching bottom rebound opportunities.

### Advantage Analysis

The strategy has the following advantages:

1. Utilize RSI to catch oversold opportunities  
2. EMA patterns to spot trend change points
3. Good backtesting results, especially resilience in bear markets
4. Configurable parameters to adjust strategy  

### Risk Analysis  

The strategy also has the following risks:

1. Improper parameter tuning may cause premature entries or delayed exits
2. Rebounds may not materialize or sustain
3. Trading fees and slippage also affect actual profit  

Parameters can be optimized, or other indicators combined to determine market structure.

### Optimization Directions

The strategy can be improved in the following ways:

1. Test parameter combinations separately for different coins  
2. Incorporate volume changes to confirm signals
3. Add stop loss to limit single trade loss 
4. Consider dynamic position sizing  

### Conclusion

The bottom catching strategy has clear logic and works well in bear markets. More parameter tuning and optimizations can lead to better backtest results. But risks need to be monitored in live trading, and losses cannot be entirely avoided.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|14|length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-14 00:00:00
end: 2023-11-21 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=5
strategy("V3 - Catching the Bottom",
         overlay=true)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 4, 1, 0, 0)
notInTrade = strategy.position_size <= 0

//==================================Buy Conditions============================================

//RSI
length = input(14)
vrsi = ta.rsi(close, length)

buyCondition1 = vrsi < 40

//RSI decrease
decrease = 3
buyCondition2 = (vrsi < vrsi[1] - decrease)
//sellCondition1 = request.security(syminfo.tickerid, "15", buyCondition2)

//EMAs 
fastEMA = ta.sma(close, 50)
slowEMA = ta.sma(close, 100)
buyCondition3 = ta.crossunder(fastEMA, slowEMA)
//buyCondition2 = request.security(syminfo.tickerid, "15", buyCondition3)

if(buyCondition1 and buyCondition2 and buyCondition3 and timePeriod)
    strategy.entry(id='Long', direction = strategy.long)

//==================================Sell Conditions============================================

sellCondition1 = vrsi > 65

EMA9 = ta.sma(close, 9)
EMA50 = ta.sma(close, 50)
sellCondition2 = ta.crossover(EMA9, EMA50)

if(sellCondition1 and sellCondition2 and timePeriod)
    strategy.close(id='Long')

//Best on: ETH 5mins (7.59%), BNB 5mins (5.42%), MATIC 30mins (15.61%), XRP 45mins (10.14%) ---> EMA
//Best on: MATIC 2h (16.09%), XRP 15m (5.25%), SOL 15m (4.28%), AVAX 5m (3.19%)

```

> Detail

https://www.fmz.com/strategy/432897

> Last Modified

2023-11-22 15:46:19
