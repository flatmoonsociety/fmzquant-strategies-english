
> Name

TEMA Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/62a9c81c462193799d7c075025438c51e255280251b03ce018d6001703ef2d58.png)
[trans]
#### Overview
The TEMA double moving average crossover strategy is a quantitative trading strategy based on the crossover signals of two triple exponential moving averages (TEMA) with different periods. This strategy compares the relative positions of the two TEMA lines. When the short-term TEMA line crosses the long-term TEMA line, it opens a long position. When the short-term TEMA line crosses below the long-term TEMA line, it opens a short position. When the opposite cross signal appears, it closes the position. This strategy is suitable for capturing short-term trends in volatile markets.
#### Strategy Principle
The core of the TEMA double moving average crossover strategy is to construct two TEMA lines with different periods. TEMA is an improvement on EMA (Exponential Moving Average). It is calculated by re-doing EMA on EMA. Compared with EMA and SMA (Simple Moving Average), it has less lag, is closer to the price trend, and is more sensitive to short-term trends.
The strategy generates trading signals by comparing the position relationship between the short-term TEMA line and the long-term TEMA line:
1. When the short-term TEMA line crosses the long-term TEMA line, and the short-term TEMA line is above the long-term TEMA line, open a long position.
2. When the short-term TEMA line crosses the long-term TEMA line, and the short-term TEMA line is below the long-term TEMA line, open a short position.
3. When holding a long order, if the short-term TEMA line crosses the long-term TEMA line, close the long order; when holding a short order, if the short-term TEMA line crosses the long-term TEMA line, close the short order.
Opening and closing positions through the cross signals of two TEMA lines of different periods can capture short-term price trends in volatile markets.
#### Strategic Advantages
1. Compared with EMA and SMA, the TEMA indicator has less lag, the signal is more sensitive, and it can better fit the price trend.
2. The intersection of two TEMA lines of different periods generates signals for opening and closing positions. The signals are clear and can effectively grasp the short-term trend.
3. The strategy logic and code implementation are simple and clear, easy to understand and optimize.
4. Suitable for use in volatile markets and can obtain relatively stable returns.
#### Strategy Risk
1. Under unilateral trend conditions, this strategy may result in frequent transactions, which will increase transaction costs and affect returns.
2. The TEMA indicator is more sensitive to price than EMA and SMA, and frequent false signals may appear when the market fluctuates violently.
3. The strategy relies heavily on historical data in parameter selection. If market characteristics change in the future, the performance of the strategy may be affected.
4. The strategy does not set a stop loss and may bear greater risks in extreme market conditions.
#### Strategy optimization direction
1. Strategy performance can be improved by optimizing the parameters of the TEMA indicator, such as using parameter optimization methods to find the best period parameters of the two TEMA lines.
2. When generating trading signals, other technical indicators or market sentiment indicators can be combined as filtering conditions to improve the reliability of the signal and reduce false signals.
3. According to the market fluctuation characteristics, dynamic stop loss and trailing stop loss can be set to control risks.
4. You can consider analyzing the position cycle and transaction frequency, and optimize the timing of opening and closing positions and transaction frequency based on market characteristics and transaction costs.
5. This strategy can be combined with other types of strategies to take advantage of different strategies and improve the robustness of the strategy.
#### Summary
The TEMA double moving average crossover strategy is a simple and easy-to-use quantitative trading strategy that captures short-term price trends through the crossover signals of two TEMA indicators of different periods. This strategy has clear logic and is suitable for use in volatile markets. However, this strategy also has some risks, such as frequent trading, false signals and extreme market risks. The performance of the strategy can be improved and the robustness and practicality of the strategy can be improved by optimizing parameters, adding filter conditions, setting stop losses and combining different strategies.
|| 

#### Overview
The TEMA Dual Moving Average Crossover Strategy is a quantitative trading strategy that generates trading signals based on the crossover of two Triple Exponential Moving Averages (TEMA) with different periods. The strategy compares the relative positions of the two TEMA lines. It opens a long position when the short-term TEMA line crosses above the long-term TEMA line and opens a short position when the short-term TEMA line crosses below the long-term TEMA line. The positions are closed when the opposite crossover signals occur. This strategy is suitable for capturing short-term trends in a ranging market.

#### Strategy Principle
The core of the TEMA Dual Moving Average Crossover Strategy is to construct two TEMA lines with different periods. TEMA is an improvement over the Exponential Moving Average (EMA). It is calculated by applying EMA to the EMA of the EMA, resulting in less lag compared to EMA and Simple Moving Average (SMA). TEMA is more responsive to price movements and more sensitive to short-term trends.

The strategy generates trading signals by comparing the positions of the short-term and long-term TEMA lines:
1. When the short-term TEMA line crosses above the long-term TEMA line and the short-term TEMA line is above the long-term TEMA line, it opens a long position.
2. When the short-term TEMA line crosses below the long-term TEMA line and the short-term TEMA line is below the long-term TEMA line, it opens a short position.
3. When holding a long position, if the short-term TEMA line crosses below the long-term TEMA line, it closes the long position. When holding a short position, if the short-term TEMA line crosses above the long-term TEMA line, it closes the short position.

By using the crossover signals of two TEMA lines with different periods, it can capture short-term price trends in a ranging market.

#### Strategy Advantages
1. TEMA indicator has less lag compared to EMA and SMA, providing more responsive signals and better alignment with price movements.
2. By using the crossover signals of two TEMA lines with different periods to open and close positions, the signals are clear and effective in capturing short-term trends.
3. The strategy logic and code implementation are simple and clear, easy to understand and optimize.
4. Suitable for use in ranging markets, potentially generating stable returns.

#### Strategy Risks
1. In strong trending markets, the strategy may generate frequent trades, leading to increased transaction costs and affecting profitability.
2. TEMA indicator is more sensitive to price compared to EMA and SMA, potentially generating frequent false signals during high market volatility.
3. The strategy's performance depends on parameter selection based on historical data. If future market characteristics change, it may impact the strategy's performance.
4. The strategy does not include stop-loss, potentially incurring significant risks in extreme market conditions.

#### Strategy Optimization Directions
1. Optimize the parameters of the TEMA indicator to improve strategy performance, such as using parameter optimization methods to find the optimal periods for the two TEMA lines.
2. When generating trading signals, incorporate other technical indicators or market sentiment indicators as filters to improve signal reliability and reduce false signals.
3. Set dynamic stop-loss and trailing stop-loss based on market volatility characteristics to control risks.
4. Analyze holding periods and trading frequency, optimize entry and exit timing and trading frequency based on market characteristics and transaction costs.
5. Consider combining this strategy with other types of strategies to leverage the strengths of different strategies and improve overall robustness.

#### Summary
The TEMA Dual Moving Average Crossover Strategy is a simple and easy-to-use quantitative trading strategy that captures short-term price trends using crossover signals of two TEMA indicators with different periods. The strategy has a clear logic and is suitable for use in ranging markets. However, the strategy also has some risks, such as frequent trading, false signals, and extreme market risks. The strategy performance can be improved by optimizing parameters, adding filter conditions, setting stop-losses, and combining with other strategies to enhance its robustness and practicality.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-28 00:00:00
end: 2024-06-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('2 TEMA Cross Strategy', shorttitle='2 TEMA Cross Strat', overlay=true, initial_capital=25000, currency=currency.USD)
//My backtesting showed best results on a 5 min chart
//Create 2 TEMA Input and pre-populate
len1 = input.int(9, minval=1, title='Length 1')
len2 = input.int(26, minval=2, title='Length 2')

//Calculate Tema values for each Input
//Tema 1
ema1 = ta.ema(close, len1)
ema11 = ta.ema(ema1, len1)
ema111 = ta.ema(ema11, len1)
tema1 = 3 * (ema1 - ema11) + ema111

//Tema 2
ema2 = ta.ema(close, len2)
ema22 = ta.ema(ema2, len2)
ema222 = ta.ema(ema22, len2)
tema2 = 3 * (ema2 - ema22) + ema222

//Plot the MAs
plot(tema1, color=color.new(color.black, 20))
plot(tema2, color=color.new(color.maroon, 20))

// Define long/short conditions
long = ta.crossover(tema1, tema2) and tema1 > tema2  
short = ta.crossunder(tema1, tema2) and tema1 < tema2
exitLong = ta.crossunder(tema1, tema2)
exitShort = ta.cross(tema1, tema2)

// Buys when buy condition met
strategy.entry('long', strategy.long, when=long)  
strategy.close('long', when=exitLong)

// Closes position when sell condition met
strategy.entry('short', strategy.short, when=short)  
strategy.close('short', when=exitShort)


```

> Detail

https://www.fmz.com/strategy/453234

> Last Modified

2024-06-03 10:59:42
