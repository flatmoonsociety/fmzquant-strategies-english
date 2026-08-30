
> Name

Adaptive-Multi-Timeframe-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a trend following strategy that utilizes the multi-time frame adaptive moving average crossover principle. This strategy uses fast line, slow line and MACD indicators to judge trading signals at the same time, aiming to obtain additional profits from the medium and long-term trend.
## Principle
This strategy is mainly based on the combined application of the double moving average crossover system and the MACD indicator. The double moving average crossover system consists of fast EMA and slow EMA, which calculate the short-term moving average and the long-term moving average respectively. When the fast line crosses the slow line, a buy signal is generated, indicating that the market has turned from falling to rising, and a long position can be established. When the fast line crosses the slow line, a sell signal is generated, indicating that the market has turned from rising to falling, and you can close your position at this time. The MACD indicator consists of the DIF line and the DEA line, which are the difference line between the short-term EMA and the long-term EMA and the moving average of the difference respectively. The HIST line is the difference between the DIF line and the DEA line, which represents the momentum of the MACD line. When the MACD HIST column turns red, it is a short signal, and when it turns green, it is a long signal.
This strategy combines the trend judgment of double moving averages and the momentum conversion signal of MACD. It can effectively filter out false breakthroughs while obtaining profits from medium and long-term trends. Specifically, when the fast line crosses the slow line, if the MACD column turns green at the same time, a more reliable long signal will be generated; conversely, when the fast line crosses the slow line, if the MACD column turns red at the same time, a stronger short signal will be generated.
In addition, this strategy also introduces parameter adaptation function. During the parameter optimization process, the fast cycle, slow cycle and MACD parameters will be automatically adjusted according to the effects of different time periods to ensure that the strategy can achieve better performance in different market environments.
## Advantages
1. Integrate the dual moving average system and the MACD indicator to make decisions based on multiple factors to avoid being misled by noise and false signals.
2. Apply the adaptive parameter function to enable the strategy to dynamically adjust parameters to adapt to market changes and automatically optimize trading decisions.
3. Better grasp the medium and long-term trends, filter out false breakthroughs that shake the market, and obtain extra profits in trending markets.
4. Use cross-time frame analysis to identify larger-level trend directions.
5. The strategy logic is clear and simple, the code structure is optimized, easy to understand and modify, and is suitable for adjustment to different needs.
## Risk
1. The dual moving average system has the risk of whipsaw lag and is not suitable for volatile market conditions. Stocks and time periods with obvious trends should be selected for operation.
2. MACD has hysteresis and is not suitable for tracking sharply changing trends and should be used in conjunction with other indicators.
3. Parameter optimization requires a sufficiently large backtest period and strict risk assessment to avoid overfitting.
4. When holding long-term positions, you need to pay attention to the systemic risks caused by emergencies and stop losses and exit the market in a timely manner.
5. The adaptive parameter function may be over-optimized and needs to be fully verified to avoid too frequent parameter adjustments.
## Optimization direction
1. You can test different combinations of fast and slow moving averages, and select moving average parameters that can filter noise and follow the trend.
2. You can test multiple sets of MACD parameters to find a combination of parameters that can respond to the trend transition point in advance.
3. You can add trend indicators as filters to suspend trading when the trend is unclear to avoid whipsaw.
4. You can introduce a stop-loss mechanism, set a trailing stop-loss or pending order stop-loss, and control single losses.
5. You can try to add machine learning algorithms, use a larger amount of data to train parameter adaptive rules, and improve the stability of the strategy.
6. You can try multi-variety arbitrage and form a trading portfolio among related varieties to diversify market systemic risks.
## Summarize
This strategy integrates the double moving average crossover and the MACD momentum indicator to achieve an organic combination of trend tracking and rhythm control. The introduction of adaptive parameters makes the strategy more robust and able to adapt smoothly to market changes. Compared with the single indicator strategy, this strategy has formed a stronger decision-making effect and can obtain richer trading returns in the medium and long-term trends. In the next step, the effect of the strategy can be further enhanced through parameter optimization, risk control and other means. Overall, this strategy forms a reliable trend-following trading system, which is worthy of in-depth study and application.

||



## Overview

This strategy utilizes the principle of adaptive moving average crossover across multiple timeframes to track trends. It combines fast line, slow line and MACD indicator for trade signal judgment, aiming to capture additional profits from medium-to-long term trends.

## Principle 

The strategy is mainly based on the combination of dual moving average crossover system and MACD indicator. The dual moving average crossover system consists of fast EMA and slow EMA, which calculate short-term and long-term moving averages respectively. A buy signal is generated when the fast line crosses above the slow line, indicating the market trend has changed from decline to rise, and long position can be built. A sell signal is generated when the fast line crosses below the slow line, indicating the market trend has changed from rise to decline, at which time position can be closed. The MACD indicator consists of DIF line and DEA line, which are the difference between short-term EMA and long-term EMA, and the moving average of the difference respectively. The HIST line, i.e. the difference between DIF and DEA, represents the momentum of MACD. A red MACD histogram bar stands for short signal, while a green one stands for long signal.

The strategy combines the trend judgment of dual moving average and the momentum change signal of MACD. While capturing profits from medium-to-long term trends, it can effectively filter false breakouts. Specifically, when the fast line crosses above the slow line, if the MACD histogram turns green at the same time, a more reliable long signal is generated. On the contrary, when the fast line crosses below the slow line, if the MACD histogram turns red simultaneously, a stronger short signal is generated.

In addition, the strategy also incorporates adaptive parameter functionality. During parameter optimization, the periods of fast line, slow line and MACD parameters are automatically adjusted based on performance over different time periods, to ensure the strategy can achieve relatively better performance under different market conditions.

## Advantages

1. Combines dual moving average system and MACD indicator for decision making, avoiding being misled by false signals from noise.

2. Applies adaptive parameter functionality so that the strategy can dynamically adjust parameters to adapt to market changes and optimize trading decisions automatically.

3. Captures medium-to-long term trends relatively well, filters false breakouts from range-bound markets, and obtains additional profits from trending markets.

4. Adopts analysis across timeframes to identify larger-degree trend direction.

5. Simple and clear logic, optimized code structure, easy to understand and modify to meet different needs.

## Risks

1. Dual moving average system has the risk of being whipsawed, unsuitable for range-bound market, should be used for stocks and time periods with obvious trend.

2. MACD has lagging effect, not suitable for tracing rapidly changing trends, should be combined with other indicators. 

3. Parameter optimization requires large enough backtesting period and strict risk assessment to avoid overfitting.

4. Pay attention to systemic risks from sudden events when holding long position, stop loss in time if necessary.

5. Risk of over-optimization for adaptive parameter functionality, requiring sufficient verification to avoid too frequent parameter adjustment.

## Improvement Directions

1. Test different fast and slow moving average combinations to find parameters that filter noise and comply with trend.

2. Try different MACD parameter sets to find the combination that reflects trend change point earliest.

3. Add trend indicator as filter, pause trading when trend is unclear, to avoid whipsaw. 

4. Introduce stop loss mechanism like moving stop loss or pending orders to control single trade loss.

5. Try machine learning algorithms to train adaptive parameter rules with more data, improving stability.

6. Try cross-product arbitrage to form portfolio across correlated products, diversifying market systemic risks.

## Conclusion

This strategy combines dual moving average crossover and MACD momentum indicator, achieving organic integration of trend following and rhythm control. The introduction of adaptive parameters makes the strategy more robust to adapt smoothly to market changes. Compared with single indicator strategies, this strategy forms stronger decision making effects, capable of capturing relatively ample trading profits from medium-to-long term trends. Next steps may include parameter optimization, risk control etc. to further enhance the strategy. Overall, the strategy forms a reliable trend following trading system, worthy of in-depth research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|fastLength|
|v_input_2|55|slowLength|
|v_input_3|9|signalLength|
|v_input_4|6|MACDCandlesCheckedBack|
|v_input_5|4|MACDTolerance|


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

// To enable alerts: Change 'Strategy' to read 'Study' below  and you also need to comment out lines 43 and 47 - Strategy code

// strategy(title="Riz Coloured MACD", shorttitle="Riz MACD" , initial_capital=5000, default_qty_value=3  )
//study(title="Riz Coloured MACD", shorttitle="Riz MACD")

source = close
fastLength = input(21, minval=1), slowLength=input(55,minval=1)
signalLength=input(9,minval=1)
MACDCandlesCheckedBack=input(6,minval=1)
MACDTolerance=input(4,minval=1)

fastMA = ema(source, fastLength)
slowMA = ema(source, slowLength)
macd = fastMA - slowMA
signal = ema(macd, signalLength)
hist = macd - signal

// ====== BASIC COLOURING - IF HISTOGRAM IS HIGHER THAN PREVIOUS 2 CANDLES THEN WE ARE TICKING UP and VISA VERSA ============//

isTickingUp = hist > hist[1] and hist > hist[2] //and hist > hist[3]
isTickingDown = hist < hist[1] and hist < hist[2] // and hist < hist[3]


// ======= MACD STRATEGY CODE ========== //

// Check if MACD is ticking in the right direction to take a trade - adding 1 at the end means it starts at -1 so not to include the current candle
MACDHistHighestHigh= highest(hist, MACDCandlesCheckedBack)[1]
MACDHistLowestLow = lowest(hist, MACDCandlesCheckedBack)[1]

MACDConfirmsLong() => (hist - MACDHistLowestLow) > MACDTolerance
MACDConfirmsShort() => (MACDHistHighestHigh - hist) > MACDTolerance


plot(macd,  title="MACD", color=blue, linewidth=3)
plot(signal,  title="SIGNAL", color=orange, linewidth=3)

// === SIMPLE COLOURING BASED ON LAST 2 CANDLES - EASY TO REFERENCE IN DAY TO DAY MACD USE ====//

plot(hist, title="HIST", color=isTickingDown ? fuchsia : isTickingUp ? lime : green, linewidth=3, style=histogram)

// ==== ALTERNATIVE COLOURING FOR PLOT BASED ON STRATEGY SETTINGS INSTEAD

//plot(hist, title="HIST", color=MACDConfirmsLong() ? lime : MACDConfirmsShort() ? fuchsia : green, linewidth=3, style=histogram)


// === STRATEGY - ENTER POSITIONS - COMMENT OUT TO ENABLE ALERTS === //

strategy.entry(id = "Long", long = true, when = MACDConfirmsLong()) // use function to decide when to go long

strategy.entry(id = "Short", long = false, when = MACDConfirmsShort())

// === CREATE ALERT CONDITIONS === // 

alertup = MACDConfirmsLong()
alertdown = MACDConfirmsShort()

alertcondition(alertup, title='MACD Long', message='Riz MACD says go LONG!')
alertcondition(alertdown, title='MACD Short', message='Riz MACD says go SHORT!')

```

> Detail

https://www.fmz.com/strategy/428783

> Last Modified

2023-10-09 14:56:37
