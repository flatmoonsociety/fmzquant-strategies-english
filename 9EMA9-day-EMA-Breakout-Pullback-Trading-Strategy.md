
> Name

Breakout and pullback trading strategy based on 9-day EMA9-day-EMA-Breakout-Pullback-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy uses the 9-day EMA as a judgment indicator and determines the market direction based on the price's breakthrough of the EMA. It is a typical trend following strategy. When the price breaks through the EMA, enter the long/short position and wait for the price to pull back before taking profit.
### Strategy Principles
Calculate the 9-day EMA and use it as the dividing line between long and short. When the opening price of the K-line is below the EMA line and above the closing price, it is considered that an upward breakthrough has occurred, and a long entry is made at this time; when the opening price is above the EMA line and below the closing price, a downward breakthrough is considered to have occurred, and a short entry is made at this time.
After entering the market, set a take-profit order, and the take-profit price is set near the highest price or lowest price of the K-line. That is, the take-profit price for an upward breakthrough is the high point of the previous K-line, and the take-profit price for a downward breakthrough is the low point of the previous K-line. Wait for the price to reach the take-profit point before ending the trade.
### Advantage Analysis
This strategy uses the EMA moving average to determine the trend direction and enters the market when the price breaks through the EMA, which can effectively track the trend. The take-profit point is close to the entry point and is suitable for catching short-term corrections. The strategy operation is simple and direct, and it is easy to automate.
The EMA cycle can be customized and has strong adaptability. The take-profit strategy is direct and efficient to avoid holding losing orders for a long time. Backtest data shows that the strategy performs well during periods when the trend is obvious.
### Risk Analysis
This strategy only uses a single EMA indicator, which makes it difficult to identify the trend direction in a volatile market and may generate too many false signals. The take-profit point is close to the entry point, and the position time is too short to fully capture the trend.
The EMA cycle parameters can be adjusted appropriately, and other technical indicators can also be added to assist judgment. Optimizing take-profit strategies, such as moving take-profit, dynamic take-profit, etc., can also improve the stability of the strategy. In terms of fund management, controlling the size of a single position can also reduce risks.
### Optimization direction
1. Test and optimize EMA parameters to find more suitable period parameters.
2. Add judgment rules such as volume energy indicators and volatility indicators.
3. Optimize the take-profit strategy, such as introducing moving take-profit, dynamic take-profit, etc.
4. Combine with more technical indicators to form a strategic combination.
5. Apply machine learning and other methods to determine the market trend direction.
6. Carry out strict fund management and control the size of a single position.
### Summarize
This strategy is a simple EMA breakout and callback trading strategy. The advantage is that the idea is clear and easy to implement, but the effect of relying only on a single EMA indicator is limited. Stability can be improved by introducing a variety of technical indicator optimizations. Overall, it provides a basic strategic idea for quantitative trading.
||


### Overview

This strategy uses the 9-day EMA as the judgement indicator, determining market direction based on price breakouts of the EMA, belonging to a typical trend following strategy. It enters long/short on EMA breakouts, and exits for profit when price pulls back.

### Strategy Logic

The 9-day EMA line is computed for trend judgement. When price opens below and closes above the EMA, an upward breakout is identified for going long. When price opens above and closes below the EMA, a downward breakout is identified for going short.

After entry, take profit stops are set near the high/low of that bar, i.e. take profit for upside breakouts is the high of previous bar, and for downside breakouts is the low of previous bar. Trades are closed when price hits the take profit levels.

### Advantage Analysis  

The strategy uses EMA to determine trends and enters on EMA breakouts, effectively tracking trends. The nearby take profit points aim to capture short-term pullbacks. The strategy logic is simple and direct, easy to automate.

The EMA period is customizable for flexibility. The direct stop profit approach avoids holding losing trades for too long. Backtests show good performance during obvious trending periods.

### Risk Analysis

The reliance on a single EMA indicator makes trend identification difficult during ranging markets, with the risk of excessive false signals. The nearby stop profits also fail to capture adequate trend moves.

Tuning the EMA period, or incorporating additional technical indicators could help improve judgement. Optimizing the stop profit, via trail stops, dynamic exits etc, could also aid stability. Controlling per trade position sizes via capital management would further limit risks.

### Optimization Directions

1. Test and optimize EMA parameters to find more suitable periods.

2. Add volume, volatility or other judgement rules.

3. Optimize stop profit strategies, such as trail stops, dynamic exits. 

4. Combine more technical indicators to form an ensemble system.

5. Apply machine learning for trend direction forecasting.

6. Adopt strict capital management to control per trade position sizing. 

### Summary

The strategy is a simple EMA breakout pullback system, which is clear and easy to implement, but limited relying on single EMA. Incorporating more technical indicators could improve robustness. Overall it provides a basic quant trading strategy idea.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-19 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("larry willians teste2", overlay=true)

//Window of time
start     = timestamp(2019, 00, 00, 00, 00)  // backtest start window
finish    = timestamp(2019, 12, 31, 23, 59)        // backtest finish window
window()  => true // create function "within window of time"  

ema9=ema(close,9) // Ema de 9 periodos

//Condições de compra
c1= (open< ema9 and close > ema9) //abrir abaixo da ema9 e fechar acima da ema9

if(window())
    if(c1)
        strategy.entry("Compra", true, stop = high) // Coloca ordem stopgain no topo anterior
    else
        strategy.cancel("Compra") // Cancela a ordem se o proximo candle não "pegar"
        
//codições de venda
v1= (open> ema9 and close < ema9) // abrir acima da ema9 e fechar abaixo ema9

if(window())
    if (v1)
        strategy.exit("Venda", from_entry = "Compra", stop = low) // Saida da entrada com stop no fundo anterior
    else
        strategy.cancel("Venda") //Cancela a ordem se o proximo candle não "pegar"


```

> Detail

https://www.fmz.com/strategy/427353

> Last Modified

2023-09-20 11:45:21
