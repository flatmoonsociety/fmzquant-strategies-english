
> Name

Double stacked average combination Stochastic similarity and difference K-line trading strategy Intraday-Stochastic-Oscillator-with-Double-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1efdb30d53ef7b8dbec.png)
[trans]


## Overview
This strategy uses a combination of the Double Stacked Average indicator and the Stochastic indicator to identify opportunities for trend reversal and achieve efficient short-term trading. When the price enters the overbought and oversold area, the strategy chooses to go short; when the price enters the oversold area, the strategy chooses to go long to capture the reversal of the short- and medium-term trend.
## Strategy Principle
This strategy is mainly based on the combined use of double stacked moving averages and the Stochastic indicator.
The double stacked average consists of a fast moving average, a slow moving average and a super slow moving average. When the fast moving average crosses the slow moving average, it is considered a buy signal; when the fast moving average crosses below the slow moving average, it is considered a sell signal. Double stacked moving averages can identify reversal points in short- and medium-term trends.
The Stochastic indicator includes the K value and the D value. The K value represents the position of the current closing price relative to the highest and lowest prices within N days. The D value is the M-day simple moving average of the K value. When the K value and D value both exceed 80, it is an overbought zone, and when it is less than 20, it is an oversold zone. The Stochastic indicator identifies short-term overbought and oversold areas.
This strategy combines the double stacked average line and the Stochastic indicator. When the Stochastic indicator shows an overbought or oversold area, the treeview will see if it is consistent with the double average line signal. If it is consistent, the point will be selected for reversal trading, in order to capture the turning point of the short-term trend.
## Advantage Analysis
This strategy has the following advantages:
1. The combined use of the double stacked average line and the Stochastic indicator can simultaneously identify short-term and medium-term trend turning points.
2. Use the overbought and oversold signals of the Stochastic indicator to select more effective double-stacked average line reversal trading opportunities.
3. The trading strategy rules are clear and easy to implement.
4. Adjustable trading time and month parameters to adapt to different varieties and time periods.
5. Set a stop loss to control risk.
## Risk Analysis
There are also some risks with this strategy:
1. The double superimposed average line may produce false breakthroughs, and the Stochastic indicator may also have invalid similar and different K-line patterns, resulting in incorrect trading signals. Parameters can be adjusted appropriately, or other indicators can be added for combined verification.
2. Based only on technical indicators without considering fundamental factors, it is easy to fail when major economic events occur. Economic event risk control can be added.
3. It is difficult to grasp the precise point of reversal of the moving average, and the stop loss may be too small or too large. Stop loss strategies should be optimized.
4. Improper parameter settings may lead to excessive trading frequency or poor signal effects. Parameter optimization testing should be conducted for different varieties and cycles.
5. Only suitable for short-term trading, not suitable for long-term holding. Position size should be controlled.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test more combinations of indicators, such as KDJ, MACD, etc., to enhance the effectiveness of signals.
2. Add trading volume indicator analysis to avoid false breakthroughs.
3. Optimize the parameters of the double moving average and identify more accurate reversal time points.
4. Optimize the stop loss strategy and reduce the possibility of the stop loss being triggered.
5. Add an economic event risk control module to avoid the impact of major events on transactions.
6. Use machine learning technology to automatically optimize parameters and improve the adaptability of parameters.
7. Conduct backtesting in more varieties and cycles to find the best application direction.
## Summarize
This strategy achieves the purpose of trading at the mid- and short-term trend reversal points through the combined use of double superimposed average lines and Stochastic similarity and difference K-line forms. Compared with using a certain indicator alone, this strategy can improve the profitability of trades, and the strategy rules are clear and easy to operate. However, this strategy also has certain risks, and parameters and stop losses need to be optimized, and more verification indicators and risk control methods need to be added. Overall, this strategy is a reliable, moderate-frequency short-term trading strategy.
||

## Overview

This strategy combines double moving average crossover and Stochastic oscillator to identify trend reversal opportunities for efficient short-term trading. It goes short when price enters the overbought region and goes long when price enters the oversold region, in order to catch the reversal of medium-term trends.

## Strategy Logic

The strategy is based on the combination of double moving average crossover and Stochastic oscillator.

The double moving average crossover consists of a fast moving average, slow moving average and ultraslow moving average. When the fast MA crosses above the slow MA, it is a buy signal. When the fast MA crosses below the slow MA, it is a sell signal. The double MA crossover can identify medium-term trend reversal points.

The Stochastic oscillator contains the %K and %D values. %K shows where the current close is relative to the highest and lowest prices of the past N days. %D is the M-day simple moving average of %K. Values above 80 mean overbought levels and values below 20 mean oversold levels. The Stochastic oscillator can identify short-term overbought/oversold zones. 

This strategy combines the double MA crossover and Stochastic oscillator. It looks for trend reversal signals from the double MA crossover when Stochastic shows overbought/oversold levels. This aims to catch short-term trend reversals.

## Advantage Analysis 

The advantages of this strategy:

1. Combining double MA crossover and Stochastic oscillator to identify both medium-term and short-term trend reversals.

2. Using Stochastic overbought/oversold signals to select more effective double MA crossover reversal trades. 

3. Clear trading rules easy to implement. 

4. Adjustable trading time and month parameters suitable for different products and time periods.

5. Stop loss to control risks.

## Risk Analysis

The risks of this strategy:

1. Double MA may have false breakouts. Stochastic may have invalid bull/bear divergences, leading to wrong trade signals. Fine tune parameters or add other indicators for combo confirmation.

2. Based solely on technical indicators without considering fundamentals. May fail on major economic events. Add economic event risk control.

3. Hard to pinpoint exact MA reversal timing, may have issues of stops being too tight or too wide. Optimize stop loss strategy. 

4. Improper parameter settings may lead to over-trading or poor signal quality. Optimize parameters for different products and timeframes through backtesting.

5. Only suitable for short-term trading, not long-term holding. Control position sizing.

## Optimization Directions

The strategy can be optimized in several aspects:

1. Test more indicator combos like KDJ, MACD etc to improve signal validity.

2. Add trading volume analysis to avoid false breakouts. 

3. Optimize double MA parameters to identify more accurate reversal points.

4. Optimize stop loss strategy to reduce chance of being stopped out.

5. Add economic event risk control modules to avoid impacts from major events.

6. Use machine learning techniques to auto optimize parameters for better adaptiveness. 

7. Backtest on more products and timeframes to find best applications.

## Conclusion

This strategy trades at medium-term trend reversal points identified by the double MA crossover and Stochastic bull/bear divergences. Compared to using a single indicator, it can improve trade profitability with clear rules. But it also has risks that require parameter and stop loss optimization, and more filters and risk controls. Overall it is a reliable, medium-frequency short-term trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Mode|
|v_input_2|10000|Loss Limit|
|v_input_3|2|Hour Start|
|v_input_4|13|Hour Stop|
|v_input_5|false|Month Selected|
|v_input_6|3|smooth|
|v_input_7|14|K|
|v_input_8|3|D|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-26 00:00:00
end: 2023-10-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="Intraday Stochiastic Strategy", shorttitle="Intraday Stochiastic Strategy", overlay=true, initial_capital = 1000)
//WORKS FOR BTCUSD M30
//OBVERVED GOOD PERFORMANCES FOR SELL MODE M15 : US30USD / UK100GBP / JP225USD / SPX500USD / BCOUSD / EURGBP
//Best Forex Hours are 7-21
//0 is Long Position
//1 is Short Position
//2 No position
mode=input(1, maxval=2, title="Mode")
lossLimit=input(10000, maxval=10000, title="Loss Limit")
hourStart=input(2, maxval=24, title="Hour Start")
hourStop=input(13, maxval=24, title="Hour Stop")

//Month selected for back testing. 0 is maximum number of months
monthSelected = input(0, maxval=12, title="Month Selected")

/////////////////////////////////////////////////

fast = 20, slow = 50, ultraSlow = 200
fastMA = sma(close, fast)
slowMA = sma(close, slow)
ultraSlowMA = sma(close, ultraSlow)

colorFast = red
colorSlow = black
colorUltraSlowMA = purple

if(timeframe.period == "1" or timeframe.period == "3" or timeframe.period == "5" or timeframe.period == "15" or timeframe.period == "30" or timeframe.period == "45" or timeframe.period == "60" or timeframe.period == "120" or timeframe.period == "180" or timeframe.period == "240")
    fastMA := ema(close, fast)
    slowMA := ema(close, slow)
    ultraSlowMA := ema(close, ultraSlow)
    colorFast := orange
    colorSlow := gray
    colorUltraSlowMA := blue

p1 = plot(fastMA, color=colorFast)
p2 = plot(slowMA, color=colorSlow, linewidth=2)  
p3 = plot(ultraSlowMA, color=colorUltraSlowMA, linewidth=3)

fill(p1, p2, color = fastMA > slowMA ? green : red)

////////////////////////////////////////////////

ema150 = 200
ema150MA = ema(close, ema150)

smooth = input(3, minval=1), K = input(14, minval=1), D=input(3,minval=1)
hh=highest(high,K)
ll=lowest(low,K)
k = sma((close-ll)/(hh-ll)*100, smooth)
d = sma(k, 3)
//plot(k, color=blue)
//plot(d, color=red)
//h0 = hline(80)
//h1 = hline(20)
//fill(h0, h1, color=purple, transp=95)


//plot(hour*100, color=red, linewidth=2)

stochiasticHigh = 80
stochiasticLow = 20

data = close < ema150MA and k>stochiasticHigh and d>stochiasticHigh and close>open
plotshape(data, style=shape.triangledown, location=location.belowbar, color=red)

data2 = close > ema150MA and k<stochiasticLow and d<stochiasticLow and close<open
plotshape(data2, style=shape.triangleup, location=location.abovebar, color=green)

isData = 0
isData := isData[1]

    
if(isData == 0)
    if(data)
        if(mode==1 and hour>hourStart and hour<hourStop and (monthSelected==0 or month==monthSelected)) //DOW hours : 2-13
            strategy.entry("SCALP SHORT", strategy.short)  
            isData := 1
else
    if(k<stochiasticLow and d<stochiasticLow)
        if(mode==1)
            strategy.close_all(when = true)
        isData := 0
        
isData2 = 0
isData2 := isData2[1]
    
if(isData2 == 0)
    if(data2)
        if(mode==0 and hour>hourStart and hour<hourStop and (monthSelected==0 or month==monthSelected))
            strategy.entry("SCALP LONG", strategy.long)  
            isData2 := 1
else
    if(k>stochiasticHigh and d>stochiasticHigh)
        if(mode==0)
            strategy.close_all(when = true)
        isData2 := 0

strategy.exit("STOP LOSS", "SCALP LONG", loss=lossLimit)
strategy.exit("STOP LOSS", "SCALP SHORT", loss=lossLimit) 
```

> Detail

https://www.fmz.com/strategy/430384

> Last Modified

2023-10-27 17:00:04
