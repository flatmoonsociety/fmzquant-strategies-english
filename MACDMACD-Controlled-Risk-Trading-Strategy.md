
> Name

Stop loss strategy based on MACD indicator MACD-Controlled-Risk-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/10a96e539a0c30d06e273f017448d4656cfeba03bb001576a2a31d44baae800a.png)

[trans]


## Overview
This strategy is based on the MACD indicator to design a long-term trading strategy that can control the risk of each transaction. Compared with the traditional long-short flip strategy, this strategy pays more attention to the risk control of each transaction. The strategy calculates the target stop loss price and take profit price, sets a reasonable position size, and limits the maximum loss that may be caused by each transaction. This can effectively control retracements and obtain long-term stable returns.
## Principle
This strategy first calculates the macd line and signal line of the MACD indicator. When the macd line breaks through the signal line from bottom to top, it is judged as a buy signal. In order to filter out false breakthroughs, the strategy requires barssince(crossover(macd_line, signal_line)) <= 5, that is, the breakthrough occurs within the last 5 K lines. At the same time, both the macd line and signal line are required to be below 0, indicating that it is currently oversold, and the closing price is higher than the wma moving average, indicating an upward trend. When the above conditions are met, a buy position is opened.
For each trade, the strategy calculates a reasonable stop loss price and take profit price. The stop loss price is set to the lowest price of the last three K lines. The take profit price is set as the purchase price plus 4 times the distance from the stop loss price to the purchase price.
Crucially, the strategy calculates the specific position for each trade based on the acceptable risk. Set the maximum tolerable loss for each transaction as a percentage of the total funds through the parameter capital_risk. The position size in USD is then calculated based on the stop loss width. Then convert it into the number of contracts for buying and opening a position.
The risk of each transaction is controlled within 1% of the total funds, which can effectively control drawdowns. At the same time, if the take-profit position is larger, higher profits can be obtained.
## Advantages
- Risk control comes first, and the risk of each transaction is controllable
- Optimize position size and maximize the use of funds
- Stop loss strategy can effectively control retracement
- Reasonable profit taking and high profit potential
## Risks and improvements
- The MACD indicator lags and may miss rapidly changing trends
- Improper setting of stop loss or take profit positions may reduce profits or increase risks.
- Transaction frequency may be too high and transaction costs may increase
Consider:
- Integrate other indicators to determine trends and avoid MACD lagging issues
- Optimize the stop loss and take profit algorithm to make it more flexible
- Appropriately relax transaction frequency and reduce transaction costs
## Summarize
This strategy determines the trend direction based on the MACD indicator, takes risk control as the guide, and calculates reasonable positions for trading. The key lies in risk control and position optimization to obtain long-term stable returns. However, the MACD indicator has certain flaws, and the stop-loss and stop-profit mechanism also needs to be further optimized. If you further optimize the use of indicators, stop loss and profit settings, and reduce the frequency of transactions, the strategy will be more powerful.
||


## Overview

This strategy designs a long-term trading strategy that controls the risk of each trade based on the MACD indicator. Compared with traditional long-short flipping strategies, this strategy focuses more on controlling the risk of each trade. By calculating reasonable stop loss and take profit levels and setting appropriate position sizes, it limits the maximum loss for each trade. This can effectively control drawdowns and achieve steady profits in the long run.

## Principles 

The strategy first calculates the MACD line and signal line of the MACD indicator. When the MACD line crosses above the signal line, it is determined as a buy signal. To filter out false breakouts, the strategy requires barssince(crossover(macd_line, signal_line)) <= 5, meaning the breakout happened within the most recent 5 bars. It also requires both the MACD and signal lines to be below 0, indicating an oversold condition, and the close to be above the WMA line, indicating an upwards trend. When the above conditions are met, a long position is opened.

For each trade, the strategy calculates reasonable stop loss and take profit levels. The stop loss is set to the lowest low of the most recent 3 bars. The take profit is set to the entry price plus 4 times the distance between the stop loss and entry price. 

The key is that the strategy calculates the specific position size based on the maximum affordable risk. The parameter capital_risk sets the percentage of total capital that can be lost for each trade. The position size in USD is then calculated based on the stop loss range. It is then converted to contracts for execution.

The risk of each trade is controlled within 1% of total capital, which can effectively control drawdowns. At the same time, the large profit target allows for higher returns.

## Advantages

- Risk control takes precedence, risk per trade is controllable
- Position sizing optimized to maximize capital usage  
- Stop loss strategy effectively controls drawdowns
- Reasonable take profit allows high profit potential

## Risks and Improvements

- MACD has lag, may miss fast trend changes
- Improper stop loss or take profit settings may reduce profits or increase risk 
- High trading frequency may increase transaction costs

Possible improvements:

- Incorporate other indicators to determine trend, avoid MACD lag
- Optimize stop loss and take profit algorithms to be more flexible
- Relax trading frequency to reduce transaction costs

## Summary

This strategy determines trend direction using the MACD, and takes risk control as the priority to trade with optimized position sizing. The keys are risk control and position sizing, which can achieve steady profits long-term. But MACD has some flaws, and the stop loss/take profit mechanisms need further optimization. Further optimizing indicator usage, stop loss/take profit settings, and reducing trading frequency can make the strategy even more powerful.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|% capital risk per trade|
|v_input_2|4|Take Profit in 'R'|
|v_input_3|150|WMA Bias Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-19 00:00:00
end: 2023-10-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy( "McDonalds ", shorttitle="Ur Lovin' It", initial_capital=10000, default_qty_type=strategy.cash, currency=currency.USD )

capital_risk    = input( 1.0, "% capital risk per trade" ) / 100
r_exit          = input( 4.0, "Take Profit in 'R'" )
wma_length      = input( 150, 'WMA Bias Length' )

[macd_line, signal_line, hist ] = macd(close, 12, 26, 9)

w_line = wma( close, wma_length )

golong = barssince(crossover(macd_line, signal_line)) <= 5 and ( macd_line < 0 and signal_line < 0 ) and ( close > w_line ) and strategy.opentrades == 0

float stop = na
float tp = na

// For a stop, use a recent low 
stop := golong ? lowest(low, 3)[1] : stop[1]
range = abs(close - stop)
tp := golong ? close + (r_exit * range) : tp[1]


// This is the bit that calculates how much size to use so we only lose 1% of the `strategy.equity`
how_much_willing_to_lose = strategy.equity * capital_risk
// Spread the risk across the stop range 
position_size_in_usd = how_much_willing_to_lose / (range / close)
// Sized specified in base contract
position_size_in_contracts = position_size_in_usd / close

// Enter the position
if golong
    strategy.entry("long", strategy.long, qty=position_size_in_contracts)
    strategy.exit("long exit","long", stop=stop, limit=tp)

// experimental exit strategy
// hist_strength = hist >= 0 ? ( hist[1] < hist ? 'strong' : 'weak') : ( hist[1] < hist ? 'weak' : 'strong' )
// if hist < 0 and hist_strength == 'strong' and falling( hist, 8 )
//     strategy.close("long")


plot( strategy.equity,  color=strategy.equity > 10000 ? color.green : color.red, linewidth=2 )
```

> Detail

https://www.fmz.com/strategy/430254

> Last Modified

2023-10-26 15:51:34
