
> Name

DEMA and TEMA Crossover StrategyDual-and-Triple-Exponential-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c956109721342d9a4b.png)
[trans]

### 1. Strategy Overview
The name of this strategy is "Dual Exponential Moving Average and Triple Exponential Moving Average Crossover Strategy". This strategy combines the cross signals of the Double Exponential Moving Average (DEMA) and the Triple Exponential Moving Average (TEMA), and uses the golden cross of DEMA and TEMA to determine entry and exit.
### 2. Strategy Principle
This strategy is mainly based on the intersection of the Double Exponential Moving Average (DEMA) and the Triple Exponential Moving Average (TEMA) to generate trading signals.
The formula for calculating the Double Exponential Moving Average (DEMA) is:
DEMA = 2*EMA1 - EMA2

Among them, EMA1 and EMA2 are Exponential Moving Average with length period N respectively. DEMA combines the smoothness and responsiveness of EMA.
The formula for calculating the Triple Exponential Moving Average (TEMA) is:
TEMA = 3*(EMA1 - EMA2) + EMA3

Among them, EMA1, EMA2 and EMA3 are Exponential Moving Average with length period N respectively. TEMA can filter out false breakthroughs through triple exponential smoothing.
When DEMA crosses above TEMA, a buy signal is generated; when DEMA crosses below TEMA, a sell signal is generated. According to the principle of hyperbola crossover, we can seize the cycle transition and enter and exit the market in a timely manner.
### 3. Strategic advantages
1. DEMA and TEMA are both indicators that optimize the EMA exponential moving average and can improve trading accuracy.  
2. DEMA smoothes price changes, and TEMA filters out false breakthroughs. They can complement each other to form a synergy and improve the strategy's winning rate. 
3. Combined with fast moving average DEMA and slow moving average TEMA, the cross signal is more accurate and reliable.  
4. Through the formation of trading signals based on the hyperbola crossover principle, cycle transitions can be judged in a timely manner and key entry points can be grasped.
### 4. Strategic risks and solutions
1. When market prices fluctuate violently, moving averages cross frequently, which may produce false signals, and parameters need to be adjusted appropriately.  
2. Improper setting of DEMA and TEMA lengths will also affect signal quality and requires parameter optimization.
3. This strategy only forms trading signals based on technical indicators and lacks fundamental verification and may fail. Can be combined with other indicators or model assistance.
### 5. Strategy optimization direction
1. Test and optimize the length parameters of DEMA and TEMA to find the best parameter combination.  
2. Add other technical indicator filters, such as KDJ indicator to determine long and short, to improve the effect.
3. Add machine learning model prediction results to verify the effectiveness of cross signals and reduce false signals.
4. Combine the changes in trading volume or market sentiment indicators to determine true and false crosses.
### 6. Summary
This strategy forms a trading signal through the intersection of the double exponential moving average and the triple exponential moving average. Combined with the response speed of DEMA and the filtering effect of TEMA, it can improve trading accuracy. However, a single indicator combination is susceptible to illusions and still requires the assistance of a variety of verification tools to form a systematic trading system and achieve long-term stable returns.
 ||

### I. Strategy Overview  

This strategy is named "Dual and Triple Exponential Moving Average Crossover Strategy". It combines the crossover signals of Dual Exponential Moving Average (DEMA) and Triple Exponential Moving Average (TEMA) to determine entries and exits.

### II. Strategy Logic  

This strategy mainly uses the crossover of Dual Exponential Moving Average (DEMA) and Triple Exponential Moving Average (TEMA) to generate trading signals.

The formula for DEMA is:  

DEMA = 2*EMA1 - EMA2

Where EMA1 and EMA2 are Exponential Moving Averages with period N. DEMA combines the smoothness of EMA and responsiveness.

The formula for TEMA is:

TEMA = 3*(EMA1 - EMA2) + EMA3  

Where EMA1, EMA2 and EMA3 are Exponential Moving Averages with period N. TEMA filters out fake breakouts by triple smoothing.  

When DEMA crosses above TEMA, a buy signal is generated. When DEMA crosses below TEMA, a sell signal is generated. According to the crossover principle, it can capture cycle conversion timely.  

### III. Advantages  

1. Both DEMA and TEMA optimize EMA, improving trading accuracy.
2. DEMA smooths price change, TEMA filters out fakeouts, forming synergy and improving win rate.  
3. Combining fast DEMA and slow TEMA, crossover signals are more reliable.  
4. Capturing cycle conversion timely based on crossover principle.  

### IV. Risks and Solutions

1. Frequent crossover under volatility causes false signals. Parameter tuning needed.  
2. Inappropriate parameter setting affects signal quality. Parameter optimization required.  
3. Lack of fundamental validation. Other indicators or models can assist.

### V. Optimization  

1. Test and optimize parameters of DEMA and TEMA to find best combination.
2. Add other technical indicators for filtering, e.g. KDJ for trend. 
3. Add machine learning prediction to validate signals and reduce false signals.  
4. Check trading volume or sentiment to judge true or fake crossover.   

### VI. Summary  

This strategy generates trading signals from DEMA and TEMA crossover, combining DEMA's responsiveness and TEMA's filtering capability to improve accuracy. But single indicator combo is prone to illusions. Multi-verification tools are still needed to form systematic trading system for long-term steady profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|10|DEMA Length|
|v_input_1_close|0|DEMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|8|TEMA Length|
|v_input_2_close|0|TEMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-03 00:00:00
end: 2024-01-02 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("DEMA-TEMA Cross Strategy", shorttitle="DEMA-TEMA Cross", overlay=true)

// Input options for Double EMA (DEMA)
dema_length = input.int(10, title="DEMA Length", minval=1)
dema_src = input(close, title="DEMA Source")

// Calculate Double EMA (DEMA)
dema_e1 = ta.ema(dema_src, dema_length)
dema_e2 = ta.ema(dema_e1, dema_length)
dema = 2 * dema_e1 - dema_e2

// Input options for Triple EMA (TEMA)
tema_length = input.int(8, title="TEMA Length", minval=1)
tema_src = input(close, title="TEMA Source")

// Calculate Triple EMA (TEMA)
tema_ema1 = ta.ema(tema_src, tema_length)
tema_ema2 = ta.ema(tema_ema1, tema_length)
tema_ema3 = ta.ema(tema_ema2, tema_length)
tema = 3 * (tema_ema1 - tema_ema2) + tema_ema3

// Crossover signals for long (small green arrow below candle)
crossover_long = ta.crossover(dema, tema)

// Crossunder signals for short (small red arrow above candle)
crossunder_short = ta.crossunder(dema, tema)

plotshape(crossunder_short ? 1 : na, title="Short Entry", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)
plotshape(crossover_long ? -1 : na, title="Long Entry", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)

plot(dema, "DEMA", color=color.green)
plot(tema, "TEMA", color=color.blue)

if (crossover_long)
    strategy.entry("Long", strategy.long)

if (crossunder_short)
    strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/437552

> Last Modified

2024-01-03 16:47:08
