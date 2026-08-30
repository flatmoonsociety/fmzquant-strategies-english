
> Name

Double-HULL-Moving-Average-Strategy Double-HULL-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Strategy principle:
The Double HULL Moving Average strategy is a trading strategy based on the HULL Moving Average indicator created by Alan HULL. This strategy uses two HULL moving averages, one long-term and one short-term, to determine when to buy and sell. The HULL Moving Average is a modified moving average that reduces lag by taking a weighted average of prices. The intersection of the long-term and short-term lines is used to generate buy and sell signals.
The calculation formula of HULL moving average is as follows:
```
HmaL = wma(2*wma(close, round(PDL/2)) - wma(close, PDL), round(sqrt(PDL)))
HmaS = wma(2*wma(close, round(PDS/2)) - wma(close, PDS), round(sqrt(PDS)))
```

Among them, PDL represents the long-term cycle and PDS represents the short-term cycle. The strategy determines buying and selling conditions by comparing the values ​​of the short-term and long-term lines.
## Advantage analysis:
1. Reduce hysteresis: Compared with traditional moving averages, HULL moving averages have less hysteresis, can respond to changes in price trends faster, and provide more accurate buying and selling signals.
2. Simple and easy to understand: This strategy uses two moving averages for cross judgment. The logic is relatively simple and easy to understand and implement.
3. Highly customizable: The cycle parameters in the strategy can be adjusted according to specific markets and trading varieties, making the strategy more adaptable to different trading environments.
## Risk analysis:
1. Market turbulence: During the market turbulence stage, the moving average may cross frequently, resulting in frequent buying and selling signals, which can easily generate false signals, resulting in frequent transactions and losses.
2. Slippage and delay: The execution of strategies is affected by slippage and delay, especially in high-frequency trading, which may cause the execution price to be inconsistent with the expected price, affecting the trading results.
3. Reliance on a single indicator: This strategy only relies on the HULL moving average indicator, without combining other technical indicators or market intelligence, and may not be able to fully capture market changes and trends.
## Summary:
The double HULL moving average strategy is a trading strategy based on the HULL moving average, which determines the timing of buying and selling by comparing the intersections of the short-term and long-term lines. This strategy has the advantages of reduced lag, simplicity, and high customizability, but it also carries the risks of market volatility, slippage and delays, and reliance on a single indicator. In practical applications, strategies can be adjusted and optimized according to specific circumstances, combined with other technical indicators and risk management methods, to improve the success rate and profitability of transactions.

||


## Strategy Overview:
The Double HULL Moving Average Strategy is a trading strategy based on the HULL Moving Average (HMA) indicator created by Alan HULL. The strategy utilizes two HMA lines, a longer-term line and a shorter-term line, to determine entry and exit points. The HMA is an improved moving average that reduces lag by applying weighted averaging to the price data. The crossover of the shorter-term and longer-term lines is used to generate buy and sell signals.

The calculation formula for the HMA is as follows:
```
HmaL = wma(2 * wma(close, round(PDL/2)) - wma(close, PDL), round(sqrt(PDL)))
HmaS = wma(2 * wma(close, round(PDS/2)) - wma(close, PDS), round(sqrt(PDS)))
```

Here, PDL represents the longer-term period, and PDS represents the shorter-term period. The strategy compares the values of the shorter-term and longer-term lines to determine the conditions for buying and selling.

## Advantages:
1. Reduced lag: The HMA has less lag compared to traditional moving averages, enabling it to respond faster to changes in price trends and provide more accurate signals for buying and selling.
2. Simplicity: The strategy uses two moving average lines for crossover analysis, making it relatively simple to understand and implement.
3. High customization: The strategy's period parameters can be adjusted based on specific markets and trading instruments, making it more adaptable to different market conditions.

## Risks:
1. Market volatility: During periods of market volatility, the moving average lines may cross frequently, resulting in frequent signals that can generate false signals and lead to excessive trading and losses.
2. Slippage and latency: The execution of the strategy is subject to slippage and latency, especially in high-frequency trading, which can cause executed prices to deviate from expected prices and affect trading outcomes.
3. Dependency on a single indicator: The strategy relies solely on the HMA indicator without incorporating other technical indicators or market intelligence, which may limit its ability to capture the full range of market changes and trends.

## Conclusion:
The Double HULL Moving Average Strategy is a trading strategy based on the HULL Moving Average indicator. It utilizes the crossover of shorter-term and longer-term HMA lines to determine entry and exit points. The strategy offers advantages such as reduced lag, simplicity, and high customization. However, it also carries risks related to market volatility, slippage and latency, and reliance on a single indicator. In practical applications, the strategy can be adjusted and optimized based on specific circumstances, incorporating other technical indicators and risk management methods to enhance trading success and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|LongerPeriod|
|v_input_2|8|ShorterPeriod|
|v_input_3|2019|From Year|
|v_input_4|true|From Month|
|v_input_5|true|From Day|
|v_input_6|9999|To Year|
|v_input_7|12|To Month|
|v_input_8|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-09-14 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
// Credit Indicator from KIVANC
// author and idea: KIVANC @fr3762 on twitter
// creator: Alan HULL
// 
strategy("Double HULL Moving Average Strategy", overlay=true)
PDL=input(title="LongerPeriod", defval=21, minval=1,maxval=500)
PDS=input(title="ShorterPeriod",  defval=8, minval=1,maxval=500)

// === INPUT BACKTEST RANGE ===
FromYear  = input(defval = 2019, title = "From Year", minval = 2009)
FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 2009)
ToMonth   = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 31, title = "To Day", minval = 1, maxval = 31)

// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => true // create function "within window of time"

HmaL=wma(2*wma(close,round(PDL/2))-wma(close,PDL),round(sqrt(PDL)))
HmaS=wma(2*wma(close,round(PDS/2))-wma(close,PDS),round(sqrt(PDS)))
plot(HmaL,color=red, linewidth=2)
plot(HmaS,color=blue, linewidth=2)

Buy = HmaS > HmaL
Sell = HmaS < HmaL

strategy.entry("Buy",true,when=window() and Buy)
strategy.close_all(when=window() and Sell)
```

> Detail

https://www.fmz.com/strategy/426933

> Last Modified

2023-09-15 16:43:45
