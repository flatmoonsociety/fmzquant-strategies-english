
> Name

Dynamic-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8332281c28b618609007802438fdfb3dd47e5977dabfa1db97951f79bc5e7d0f.png)
[trans]

### Overview
This strategy calculates and draws the 14-day simple moving average (SMA) and the 28-day simple moving average, and goes long when the two generate golden crosses, and goes short when they generate dead crosses to capture changes in market momentum.
### Strategy Principles
The core indicators of this strategy are the 14-day SMA and the 28-day SMA. Among them, the 14-day SMA can respond to price changes quickly, reflecting the recent trend; the 28-day SMA line is relatively stable, reflecting the mid-term trend. When the short-term average crosses the long-term average, it means that the short-term trend is better than the long-term trend, and going long can capture the upward momentum. When the short-term average crosses below the long-term average, it indicates that the long-term trend is weakening, and shorting can capture the downward momentum.
It is a relatively common trading signal to judge the long and short positions through the intersection of SMA lines. Compared with a single SMA indicator, the double SMA crossover combines information from different periods to avoid false signals.
### Advantage Analysis
This strategy has the following advantages:
1. Simple operation and easy to implement.
2. Quickly respond to price changes and capture market turning points.
3. Combined with short-term and medium-term information, the signal is relatively reliable.
4. SMA parameters can be adjusted according to the market and are highly adaptable.
### Risk Analysis
There are also some risks with this strategy:
1. The SMA itself has hysteresis and signal delays may occur.
2. Unable to cope with severe market fluctuations, such as rapid breakthroughs.
3. A large number of double-line crossings will increase transaction frequency and costs.
4. The entry and exit rules are relatively simple and there is room for optimization.
Corresponding risk management and control measures include: appropriately relaxing the stop loss range and focusing on risk control; adjusting SMA cycle parameters according to the market; and filtering signals in combination with other indicators.
### Optimization direction
This strategy can be optimized from the following dimensions:
1. Add filter conditions to avoid false cross signals. The trend can be confirmed by combining trading volume, Stoch indicators, etc.
2. Add a stop loss mechanism. Stop loss can be based on ATR, or combined with breakout stop loss.  
3. Optimize SMA cycle parameters. Adaptive SMA can be used, or parameters can be dynamically optimized through ML methods.
4. Combine with other strategy types, such as retracement control, trend following, etc., to form a combination strategy.
### Summarize
The momentum crossover moving average strategy dynamically captures market trends by calculating double SMA crossover signals. Strategies are easy to implement and respond quickly, but there is also the risk of lag. In the future, we can optimize the confirmation signal, stop loss mechanism, parameter selection, etc., or combine it with other strategies to obtain better performance.
||


### Overview

The strategy calculates and plots the 14-day simple moving average (SMA) and 28-day SMA. It goes long when the two lines have a golden cross and goes short when there is a death cross, in order to capture changes in market momentum.  

### Strategy Logic  

The core indicators of this strategy are the 14-day SMA and 28-day SMA. The 14-day SMA responds quickly to price changes, reflecting short-term trends. The 28-day SMA is more stable, reflecting medium-term trends. When the shorter SMA crosses over the longer SMA, it indicates the short-term trend is stronger than the long-term trend. Going long can capture the upside momentum. When the shorter SMA crosses below the longer SMA, it indicates the long-term trend is weakening. Going short can capture the downside momentum.

Using SMA crosses to determine long/short positions is a common trading signal. Compared to a single SMA indicator, the dual SMA cross combines information from different time horizons and avoids false signals.   

### Advantage Analysis

The advantages of this strategy include:

1. Simple to implement and operate.  
2. Quickly responds to price changes and catches market turns.
3. Combines short-term and medium-term information for relatively reliable signals.  
4. SMA parameters can be adjusted to adapt to different markets.

### Risk Analysis 

There are also some risks:

1. SMA itself has lagging effect, signals may be delayed.  
2. Cannot handle extreme market volatility like flash crashes.
3. More SMA crosses increase trading frequency and costs.  
4. Simple entry/exit rules have room for optimization.

Risk management measures include: allowing wider stops, emphasizing risk control; adjusting SMA periods based on market; combining other filters.

### Optimization Directions

The strategy can be improved in areas like:  

1. Add filters to avoid false crosses. Confirm with volume, Stochastic etc.
2. Add stop loss mechanisms. Such as ATR stops, breakout stops.
3. Optimize SMA periods. Such as adaptive SMA, ML parameter selection.  
4. Combine with other strategy types. Such as drawdown control, trend following to make combo strategies. 

### Conclusion

The momentum SMA cross strategy dynamically captures changing market trends by calculating dual SMA cross signals. It is easy to implement and responds quickly, but also has lagging risk. Future improvements can be made in confirming signals, stop losses, parameter selection etc, or combine with other strategies for better results.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-06 00:00:00
end: 2023-12-06 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Tu Estrategia", overlay=true)

// Variables de estrategia
var bool longCondition = na
var bool shortCondition = na

// Indicador
emaValue = ta.ema(close, 30)
plotColor = close > open ? color.green : color.red
plot(emaValue, color=plotColor, linewidth=2)
value = 10 * open / close
plotColor2 = close == open ? color.orange : color.blue
plot(value, color=plotColor2, linewidth=2)

// Lógica de la estrategia
longCondition := ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
shortCondition := ta.crossunder(ta.sma(close, 14), ta.sma(close, 28))

// Entradas de estrategia
if (longCondition)
    strategy.entry("Long", strategy.long)
if (shortCondition)
    strategy.entry("Short", strategy.short)

plotColor3 = strategy.position_size > 0 ? color.green :
     strategy.position_size < 0 ? color.red :
     color.yellow

plot(ta.sma(close, 10), color=plotColor3)

```

> Detail

https://www.fmz.com/strategy/434556

> Last Modified

2023-12-07 15:26:38
