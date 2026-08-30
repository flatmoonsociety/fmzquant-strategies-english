
> Name

Unilateral long strategy SMA-and-RSI-Long-Only-Strategy based on moving average and RSI
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5713ebba3ed36d9d1c.png)
[trans]

## Overview
This strategy was adapted from an article by Enrico Malverti and primarily uses the Simple Moving Average (SMA) and the Relative Strength Index (RSI) to identify long entry and exit signals. The strategy is only long, not short.
## Strategy Principle
The entry signal is to open a long position when the price closes above the longer period SMA.
There are several types of closing signals:
1. Close the position when the RSI indicator falls below 70 or exceeds 75;
2. Stop loss when the closing price breaks below the shorter period SMA moving average;
3. Take profit when the closing price crosses the shorter period SMA.
At the same time, the SMA moving average for stop loss and the SMA moving average for take profit are drawn.
## Advantage Analysis
This strategy has the following advantages:
1. Uses a simple and easy-to-understand indicator combination, which is easy to understand and implement;
2. Only go long and avoid the additional risks of short selling;
3. There are clear entry rules, stop loss rules and take profit rules, and the risks are controllable;
4. It is relatively easy to optimize and can adjust parameters such as SMA cycle.
## Risk Analysis
There are also some risks with this strategy:
1. It is easy to have the psychological shadow of no longer having the confidence to track signals after multiple losses;
2. Dislocation of SMA moving average may lead to risks;
3. The RSI indicator is prone to divergence, and overbought and oversold signals may be unreliable.
Corresponding method:
1. Establish a fixed tracking mechanism that is not affected by psychological influences;
2. Adjust the parameters of SMA moving average and optimize the cycle;
3. Filter RSI signals in combination with other indicators.
## Optimization direction
This strategy can also be optimized from the following directions:
1. Try SMA settings with different parameters;
2. Add other indicators to filter entry and exit signals;
3. Add trend judgment indicators to distinguish trends and consolidation;
4. Try parameter adaptive optimization.
## Summarize
The overall idea of ​​this strategy is clear and easy to understand, uses basic indicators, is highly controllable, and is suitable for medium and long-term operations. However, parameter settings and indicator filtering require repeated testing and optimization to make the strategy more stable and reliable. Strategies with simple ideas also require a lot of optimization adjustments and rich combinations to form a truly usable trading system.
||

## Overview  

This strategy is adapted from the articles by Enrico Malverti. It mainly uses Simple Moving Average (SMA) and Relative Strength Index (RSI) to identify long entry and exit signals. The strategy only goes long but not short.  

## Strategy Logic   

The entry signal is triggered when closing price crosses over the longer period SMA line.  

Exit signals include:
1. Close long when RSI crosses below 70 or goes above 75;  
2. Stop loss when closing price crosses below the shorter period SMA line;
3. Take profit when closing price crosses below the shorter period SMA line.  

The stop loss SMA line and take profit SMA line are also plotted.

## Advantage Analysis   

The advantages of this strategy:

1. Uses simple and easy-to-understand indicator combination;  
2. Only goes long to avoid short selling risk;
3. Has clear entry, stop loss and take profit rules, controllable risk;  
4. Easy to optimize by adjusting SMA periods etc.

## Risk Analysis   

There are some risks:  

1. Psychological bias of losing confidence after losses;
2. SMA line shift may cause risks;
3. RSI divergence signals may be unreliable.

Solutions:
1. Build fixed trading mechanism following rules;
2. Optimize SMA periods;  
3. Add other filters for RSI signals.

## Optimization Directions  

The strategy can be further optimized:  

1. Test different parameters for SMA;
2. Add other indicators as filters;
3. Add trend identification to distinguish trend and consolidation;  
4. Parameter adaption and optimization.

## Conclusion   

The overall idea is simple and clear. With basic indicators and controllability, it suits medium-long term trading. But parameter tuning and indicator filtering require lots of tests and optimization to make the strategy more solid and reliable. Simple ideas need huge efforts on optimization and combination to form real usable trading systems.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Ma periodo veloce|
|v_input_2|14|Ma periodo lungo|
|v_input_3|7|Ma periodi stop|
|v_input_4|14|RSI period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-11 00:00:00
end: 2023-12-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version= 4
// form the original idea of Enrico Malverti www.enricomalverti.com , trading system 2015  
// https://sauciusfinance.altervista.org
strategy(title="MAs & RSI strategy long only", overlay = true, max_bars_back=500)

///********FROM EMAS TO SIMPLE MA *****
// NON AGGIUNTO SCHAFF INDICATOR, che serve per discriminare quali titoli scegliere dallo screener (segnale già aperto o il primo o, a parità,
//quello più alto) ==> Tolte le bande di Bollinger (che filtrano "poco")

// INPUTS 
emapf = input(14, title ="Ma periodo veloce",  minval=1, step = 1)
emapl = input(14, title ="Ma periodo lungo",  minval=1, step = 1)
emaps = input(7, title ="Ma periodi stop",  minval=1, step = 1)
rsi_period = input(14, title="RSI period", minval = 1, step = 1) 
// CALCULATIONS
maf = sma(close, emapf)
mal = sma(close, emapl)
// rsi
myrsi = rsi(close, rsi_period)
//ema stop long ed ema stop short
//Ema7 messo da "massimo" a "chiusura" come target per posizioni short. Il limite è, in questo caso, sempre ema20 (più restringente - asimmetria)
// in questo t.s., lo short viene soltanto indicato come "rappresentazione grafica", non agito
mass = sma(close, emaps)
masl = sma(low, emaps)
ma200=sma(close,200)
/// Entry
strategy.entry("Long", true, when = crossover(close,mal))

rsi1 = crossunder(myrsi,70)
rsi2 = myrsi > 75
// previously, 80
st_loss_long = crossunder(close,masl)// **chiusura sotto EMA7**
target_long= crossunder(close,maf) //* Chiusura sotto EMA14*
// exits. *RSI**Long: Target if over bandamax, loss if under bandamin. Viceversa, for short
strategy.close("Long", when = rsi1, comment="crossunder RSI")
strategy.close("Long", when = rsi2, comment ="RSI MAX")
strategy.close("Long", when = st_loss_long, comment = "Stop loss")
strategy.close("Long", when = target_long, comment = "target_long" )

plot(masl, title="ma stop long", color=#363A45, linewidth= 1, style=plot.style_cross)
plot(maf, title="MA FAST", color=#FF0000,  linewidth= 1)
plot(mal, title="MA SLOW", color=#0000FF,  linewidth= 2)
plot(mass, title="ma stop short", color=#787B86,linewidth= 1, style=plot.style_cross)
plot(ma200, title="ma200", color=color.black,  linewidth= 1)
```

> Detail

https://www.fmz.com/strategy/435703

> Last Modified

2023-12-18 10:28:10
