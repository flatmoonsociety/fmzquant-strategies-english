
> Name

Kalman filter-based trend tracking strategy Kalman-Filter-Based-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/a951d4af368e79ebce3d9298d5b5c954eaf3853d66bbfda905b89869ff6aacb3.png)
[trans]
## Overview
The core of this strategy is to use Kalman filter technology to smooth the price moving average. By calculating the tangent angle of the smoothed moving average, a trading signal is generated when the tangent angle exceeds a certain threshold within a specified period. This strategy is dedicated to tracking medium and long-term trends and reducing the impact of noise through Kalman filtering technology to obtain clearer and more reliable trend signals.
## Strategy Principle
The core logic of this strategy mainly includes the following steps:
1. Calculate the simple moving average (SMA) of the 1-minute price as the original moving average;
2. Perform Kalman filtering on the original moving average and output the smoothed moving average;
3. Calculate the tangent angle of the smoothed moving average;
4. Define the parameter period and the sum of tangent angles within the statistical period;
5. A buy signal is generated when the sum of tangent angles within the period is greater than 360 degrees; a sell signal is generated when it is less than -360 degrees.
Through this design, when the price shows an upward or downward trend, the tangent angle of the moving average will gradually accumulate. When the accumulation reaches a certain level, a trading signal will be generated, so it can effectively track the medium and long-term trend.
Among them, Kalman filtering is the key to this strategy. Kalman filter is a recursive algorithm that not only predicts the current state, but also predicts the values ​​of process noise and measurement noise, and uses the values ​​of these noises to correct the prediction of the current state, thereby obtaining a more accurate and reliable state estimate.
In this strategy, the SMA of the price can be regarded as a measurement of state. Affected by market noise, the Kalman filter will recursively estimate the true trend of the price, greatly reducing the impact of noise, making subsequent moving average calculations more reliable, and thus producing more stable and accurate trading signals.
## Strategic Advantages
Compared with indicator strategies such as simple moving averages, the biggest advantage of this strategy is that it uses Kalman filtering to reduce the impact of noise, making the trading signals clearer and more reliable. The specific advantages are mainly reflected in the following aspects:
1. Reduce false signals. Kalman filter effectively filters out a large number of false signals caused by random fluctuations by adaptively estimating and eliminating noise, making the generated trading signals more reliable.
2. Better tracking effect. The smoothed moving average shape is smoother and can better reflect the mid- and long-term price trends, thereby achieving better trend tracking effects.
3. Flexible parameter setting. Adjustable parameters include moving average length, Kalman filter parameters and statistical periods, which can be flexibly adapted to different market environments.
4. Risks are controllable. This strategy focuses more on mid- to long-term trends rather than short-term fluctuations, achieving a better risk-reward balance.
5. Simple to implement and easy to expand. The core algorithm of this strategy is relatively simple, easy to implement and test, and also provides room for expansion. For example, machine learning algorithms can be introduced to automatically optimize parameters.
## Strategy Risk
This strategy also has the following main risks:
1. Trend reversal risk. This strategy focuses on trend tracking. Once a drastic trend reversal occurs, large losses will occur. Single transaction losses can be reduced by appropriately shortening the statistical period.
2. Parameter optimization risks. Improper parameter settings may lead to frequent transactions or signal lag, which requires full testing and optimization. Can be combined with machine learning algorithms to automatically optimize.
3. Risk of over-optimization. Over-optimization on historical data may also lead to parameter failure, which needs to be controlled to be effective outside the sample.
4. Implementation complexity increases risks. The introduction of Kalman filter and tangent angle algorithm will increase the code complexity, and it is necessary to ensure correct implementation.
## Strategy optimization direction
Taking into account the above risk factors, the possible optimization directions of this strategy include:
1. Introduce stop loss and position management. Appropriate stop loss can effectively control the risk of single loss; dynamic position management can also adjust the position coverage risk according to market conditions.
2. Automatic parameter optimization. Through machine learning optimization algorithms, automatic optimization of parameters can be achieved to avoid the risk of over-optimization.
3. Integrate other indicators. Some other indicators can be integrated into the strategy to form an indicator combination to improve the stability of the strategy.
4. Add efficiency evaluation. Introduce more risk adjustment indicators to evaluate the efficiency and stability of the strategy to draw more comprehensive and accurate conclusions.
5. Expand multiple varieties. If the results are good, you can consider expanding to more varieties, accumulating richer samples in the medium to long term, and also facilitating cross-variety parameter optimization.
## Summarize
Generally speaking, this strategy is a relatively simple and practical trend following strategy. Compared with the traditional moving average strategy, the introduction of the Kalman filter algorithm is its biggest innovation, which also enables the strategy to generate clearer and more reliable trading signals. In the next step, through further optimization, this strategy is expected to achieve even better results. In general, this strategy provides a new idea for quantitative trading strategies and is worthy of further research and application.
||

## Overview

The core of this strategy is to use Kalman filter technology to smooth the price moving average, and generate trading signals when the tangent angle of the smoothed moving average exceeds a certain threshold within a specified period. The strategy aims to track medium and long term trends by using Kalman filter technology to reduce the impact of noise, so as to obtain clearer and more reliable trend signals.

## Strategy Principle  

The core logic of this strategy mainly includes the following steps:

1. Calculate the simple moving average (SMA) of the 1-minute price as the original moving average;

2. Kalman filter the original moving average to output a smoothed moving average;

3. Calculate the tangent angle of the smoothed moving average;  

4. Define the parameter period and statistically sum the tangent angles within the period;

5. Generate a buy signal when the sum of tangent angles within the period is greater than 360 degrees; generate a sell signal when less than -360 degrees.

With this design, when the price shows an upward or downward trend, the tangent angle of the moving average will gradually accumulate. When it accumulates to a certain extent, trading signals will be generated. Therefore, it can effectively track medium and long term trends.

Among them, the Kalman filter is the key. The Kalman filter is a recursive algorithm that predicts the value of process noise and measurement noise while predicting the current state, and uses these noise values to correct the prediction of the current state to obtain a more accurate and reliable state estimation.

In this strategy, the SMA of the price can be seen as the measurement of the state. Affected by market noise, the Kalman filter will recursively estimate the true trend of prices, greatly reduce the impact of noise, make the subsequent moving average calculation more reliable, and thus produce more stable and accurate trading signals.

## Advantage Analysis  

Compared with simple moving average and other technical indicator strategies, the biggest advantage of this strategy is that it uses Kalman filter to reduce the impact of noise, making trading signals clearer and more reliable. The specific advantages are mainly reflected in the following aspects:

1. Reduce false signals. Kalman filtering effectively filters out a lot of false signals caused by random fluctuations by adaptively estimating and eliminating noise, making the trading signals generated more reliable.

2. Better tracking effect. The smoothed moving average shape is smoother and better reflects the medium and long term trend of prices, thus achieving better trend tracking effect.  

3. Flexible adjustable parameters. Adjustable parameters include the length of moving average, parameters of Kalman filter and statistical cycle, which can flexibly adapt to different market environments.

4. Controllable risk. This strategy focuses more on medium and long term trends rather than short term fluctuations, achieving good risk-return balance.  

5. Easy to implement and expand. The core algorithm of this strategy is quite concise and easy to implement and test. It also provides room for expansion, such as introducing machine learning algorithms to automatically optimize parameters.

## Risk Analysis

The main risks of this strategy also include:

1. Trend reversal risk. This strategy focuses on trend tracking. In case of a sharp trend reversal, it will lead to greater losses. This can be mitigated by appropriately shortening the statistical cycle to reduce per trade loss.  

2. Parameter optimization risk. Inappropriate parameter settings may lead to frequent trading or signal lagging. It requires sufficient testing and optimization. It can be combined with machine learning algorithms for automatic optimization.

3. Over-optimization risk. Excessive optimization on historical data may also lead to ineffective parameters. Out-of-sample validity needs to be controlled.

4. Increased complexity risk. Introducing Kalman filter and tangent angle algorithms increases code complexity. Correct implementation needs to be ensured.

## Optimization Directions

Considering the above risks, the optimization directions of this strategy include:

1. Introduce stop loss and position sizing. Appropriate stop loss can effectively control the risk of single trade loss; dynamic position sizing can also adjust positions to hedge risks according to market conditions.

2. Automatic parameter optimization. Machine learning optimization algorithms can achieve automatic parameter optimization to avoid over-optimization risks.  

3. Integrate other indicators. Some other indicators can be integrated into the strategy to form indicator combinations to enhance strategy stability.

4. Increase efficiency evaluation. Introduce more risk-adjusted metrics to evaluate the efficiency and stability of strategies for a more comprehensive and accurate conclusion.

5. Expand to more products. If effective, it can be considered to expand to more products. In the medium and long term, it accumulates richer samples and facilitates cross-product parameter optimization.

## Conclusion

In general, this strategy is a relatively simple and practical trend tracking strategy. Compared with traditional moving average strategies, the introduction of the Kalman filter algorithm is its biggest innovation point, which also enables the strategy to produce clearer and more reliable trading signals. With further optimization, this strategy is expected to achieve better results. Overall, this strategy provides a new idea for quantitative trading strategies and is worth further research and application.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-17 00:00:00
end: 2024-01-24 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
//@library=math
strategy("策略360°（测试）", overlay=true)

// 定义1分钟均线
ma1 = request.security(syminfo.tickerid, "1", ta.sma(close, 1)) // 在这里使用了 math.sma() 函数
//plot(ma1, color=color.yellow, title="原始均线")

// 定义卡尔曼滤波函数，参考了[1](https://www.tradingview.com/pine-script-docs/en/v5/language/Methods.html)和[2](https://www.tradingview.com/pine-script-docs/en/v5/language/Operators.html)的代码
kalman(x, g) => 
    kf = 0.0 
    dk = x - nz(kf[1], x) // 在这里使用了 nz() 函数
    smooth = nz(kf[1], x) + dk * math.sqrt(g * 2) // 在这里使用了 math.sqrt() 函数
    velo = 0.0 
    velo := nz(velo[1], 0) + g * dk // 在这里使用了 nz() 函数
    kf := smooth + velo 
    kf 

// 定义卡尔曼滤波后的均线
ma2 = kalman(ma1, 0.01) 
plot(ma2, color=color.blue, title="卡尔曼滤波后的均线")

// 定义切线角
angle = math.todegrees(math.atan(ma2 - ma2[1])) // 在这里使用了 math.degrees() 和 math.atan() 函数

// 定义累加的切线角
cum_angle = 0.0
cum_angle := nz(cum_angle[1], 0) + angle // 在这里使用了 nz() 函数

// 定义30分钟周期
period = 30 // 您可以根据您的需要修改这个参数

// 定义周期内的切线角总和
sum_angle = 0.0
sum_angle := math.sum(angle, period) // 在这里使用了 math.sum() 函数，把周期内的切线角总和改成简单地把 5 个切线角相加

// 定义买入和卖出条件
buy = sum_angle > 360// 在这里使用了 math.radians() 函数
sell = sum_angle < -360

// 执行买入和卖出操作
strategy.entry("Long", strategy.long, when=buy)
strategy.close("Short", when=buy)
strategy.entry("Short", strategy.short, when=sell)
strategy.close("Long", when=sell)

// 绘制曲线图
plot(sum_angle, color=color.green, title="周期内的切线角总和")
plot(angle, color=color.red, title="切线角") // 这是我为您添加的代码，用于显示实时计算的切线角

```

> Detail

https://www.fmz.com/strategy/439972

> Last Modified

2024-01-25 14:12:26
