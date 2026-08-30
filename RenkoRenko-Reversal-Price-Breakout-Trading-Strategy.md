
> Name

Renko Reversal Price Breakout Trading Strategy Renko-Reversal-Price-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

The name of this strategy is Renko Reversal Price Breakout Trading Strategy. This strategy uses Renko chart pattern analysis to determine the time when the price may reverse, and enters the market when the key price is exceeded.
How the strategy works:
1. Use Renko Bar to display price trends.
2. Analyze the relationship between the closing price and the opening price of the first four K lines of the Renko line.
3. When the closing prices of the first four lines show significant reversal signals, it is judged that the trend may be reversed.
4. When the closing price of the Renko line breaks through the opening price, a trading signal is generated.
Specific trading rules:
1. If the closing prices of the last four Renko lines have increased significantly and the current closing price is lower than the opening price, go short.
2. If the closing prices of the last four Renko lines have fallen significantly, and the current closing price is higher than the opening price, go long.
3. Use a fixed trading volume to trade after entering the market.
Advantages of this strategy:
1. Use Renko lines to reduce market noise and identify reversal opportunities.
2. Rely on multiple K lines to judge and avoid false signals. 
3. The strategy logic is simple, clear and easy to implement.
Risks of this strategy:
1. The Renko line is improperly set, resulting in missed trading opportunities.
2. Fixed transaction volume and no fund management measures.
3. Vulnerable to slippage and transaction fees.
In short, the Renko reversal price breakout trading strategy finds reversal opportunities through the graphical analysis of the Renko line, enters the market at key points, and pursues a higher profit-loss ratio. However, traders need to pay attention to optimizing the Renko line settings and cooperate with reasonable fund management methods to control risks in real transactions.
||

This strategy is called the Renko Reversal Price Breakout Trading Strategy. It identifies potential reversal points through Renko chart pattern analysis and enters trades when prices break critical levels.   

How the strategy works:
1. Use Renko Bars to plot price action. 
2. Analyze the relationship between open and close prices of the last 4 Renko bars.
3. When close prices of last 4 bars show significant reversal signal, a trend reversal may occur.
4. Trade signals are generated when Renko close prices break above/below open prices.

Trading rules:
1. If last 4 Renko bars' close shows significant rise but current close is below open, go short.
2. If last 4 Renko bars' close shows significant fall but current close is above open, go long.
3. Use fixed trade size after entry.

Advantages of this strategy:
1. Renko bars reduce noise and identify reversal opportunities. 
2. Relying on multiple bars prevents false signals.
3. Simple and clear logic, easy to implement.

Risks of this strategy:
1. Improper Renko settings may cause missed trades.  
2. Fixed trade size, no risk management.  
3. Prone to slippage and trading costs.

In summary, the Renko Reversal Price Breakout Trading Strategy identifies reversals through Renko chart analysis and enters at key points, pursuing high risk-reward ratios. But traders need to optimize Renko settings and apply proper risk management for controlling risks in live trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-15 00:00:00
end: 2023-09-14 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title='[STRATEGY][RS]Renko V0', shorttitle='S', overlay=true, pyramiding=0, initial_capital=100000, currency=currency.USD)
trade_size = 1

ro = open
rc = close
buy_entry = rc[4] < ro[4] and rc[3] > ro[3] and rc[2] > ro[2] and rc[1] > ro[1] and rc > ro
sel_entry = rc[4] > ro[4] and rc[3] < ro[3] and rc[2] < ro[2] and rc[1] < ro[1] and rc < ro

strategy.entry('buy', long=strategy.long, qty=trade_size, comment='buy', when=buy_entry)
strategy.entry('sell', long=strategy.short, qty=trade_size, comment='sell', when=sel_entry)
```

> Detail

https://www.fmz.com/strategy/426932

> Last Modified

2023-09-15 16:27:29
