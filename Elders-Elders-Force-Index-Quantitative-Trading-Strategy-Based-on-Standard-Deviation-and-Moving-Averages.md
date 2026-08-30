
> Name

Elders-Force-Index-Quantitative-Trading-Strategy-Based-on-Standard-Deviation-and-Moving-Averages
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1aee33db94fa1dd32a3.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on Elder's Strength Index (EFI), which combines standard deviation and moving averages for signal judgment, and uses ATR to dynamically adjust stop loss and profit positions. This strategy implements a complete trading system by calculating fast and slow EFI indicators and standardizing them for cross signal judgment. The strategy adopts dynamic stop loss and trailing take profit mechanisms to effectively control risks while pursuing greater returns.
#### Strategy Principle
The strategy is mainly based on the following core elements:
1. Calculate the fast and slow strength index using the EFI indicator with two different periods (13 and 50)
2. Normalize the standard deviation of the EFI of the two periods to make the signal more statistically significant.
3. When the fast and slow EFI break through the upper standard deviation at the same time, a long signal is triggered
4. When the fast and slow EFI break through the lower standard deviation at the same time, a short signal is triggered
5. Use ATR to dynamically set the stop loss position and adjust the stop loss position as the price changes.
6. Adopt a trailing profit-taking mechanism based on ATR to protect profits while allowing profits to continue to grow.
#### Strategic Advantages
1. The signal system combines momentum and volatility characteristics to improve the reliability of trading.
2. Use standard deviation normalization to make the signal statistically significant and reduce false signals.
3. The dynamic stop loss mechanism can effectively control risks and avoid large retracements.
4. The trailing stop-profit mechanism not only protects existing profits but also allows profits to continue to grow.
5. The strategy logic is clear and the parameters are highly adjustable, making it easy to optimize for different markets.
#### Strategy Risk
1. False signals may be generated in violently volatile markets, requiring additional filtering mechanisms.
2. Overly sensitive parameter selection may lead to excessive trading and increase transaction costs.
3. There may be a lag at the turning point of the trend, which will affect the performance of the strategy.
4. Improper stop-loss setting may lead to premature exit or excessive losses.
5. The impact of transaction costs on strategy returns needs to be considered
#### Strategy optimization direction
1. Add a market environment judgment mechanism and use different parameter settings under different market conditions.
2. Introduce volume filter to improve signal reliability
3. Optimize stop-loss and take-profit parameters to better adapt to market fluctuations
4. Add trend filter to avoid frequent trading in volatile markets
5. Consider adding time filtering to avoid trading during unfavorable time periods
#### Summary
This strategy builds a complete trading system by combining the EFI indicator, standard deviation and ATR. The advantage of the strategy is that the signal system has high reliability and reasonable risk control, but it still needs to be optimized for different market environments. By adding mechanisms such as market environment judgment and trading volume filtering, the stability and profitability of the strategy can be further improved. Overall, this strategy provides a good quantitative trading framework and has good practical value.
|| 

#### Overview
This strategy is a quantitative trading system based on Elder's Force Index (EFI), combining standard deviation and moving averages for signal generation, while using ATR for dynamic stop-loss and take-profit positioning. The strategy calculates fast and slow EFI indicators, normalizes them using standard deviation, and generates trading signals through crossover analysis, creating a complete trading system. It employs dynamic stop-loss and trailing take-profit mechanisms to effectively control risks while pursuing higher returns.

#### Strategy Principle
The strategy is built on several core elements:
1. Uses two different periods (13 and 50) to calculate fast and slow force indices
2. Normalizes both EFI periods using standard deviation to make signals more statistically significant
3. Generates long signals when both fast and slow EFI simultaneously break above the standard deviation threshold
4. Generates short signals when both fast and slow EFI simultaneously break below the standard deviation threshold
5. Uses ATR for dynamic stop-loss positioning that adjusts with price movement
6. Implements ATR-based trailing take-profit mechanism to protect and grow profits

#### Strategy Advantages
1. Signal system combines momentum and volatility characteristics, improving trading reliability
2. Standard deviation normalization makes signals statistically significant, reducing false signals
3. Dynamic stop-loss mechanism effectively controls risk and prevents large drawdowns
4. Trailing take-profit mechanism both protects and allows profits to grow
5. Clear strategy logic with adjustable parameters, suitable for optimization across different markets

#### Strategy Risks
1. May generate false signals in highly volatile markets, requiring additional filtering mechanisms
2. Sensitive parameter selection might lead to overtrading, increasing transaction costs
3. Potential lag at trend reversal points, affecting strategy performance
4. Improper stop-loss positioning might result in premature exits or excessive losses
5. Need to consider the impact of transaction costs on strategy returns

#### Optimization Directions
1. Add market condition assessment mechanism to use different parameters in different market states
2. Introduce volume filters to improve signal reliability
3. Optimize stop-loss and take-profit parameters to better adapt to market volatility
4. Add trend filters to avoid frequent trading in ranging markets
5. Consider adding time filters to avoid trading during unfavorable periods

#### Summary
The strategy builds a complete trading system by combining EFI indicators, standard deviation, and ATR. Its strengths lie in high signal reliability and reasonable risk control, though optimization for different market environments is still needed. The strategy's stability and profitability can be further improved by adding market condition assessment, volume filtering, and other mechanisms. Overall, it provides a solid quantitative trading framework with practical value.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Elder's Force Index Strategy with ATR-Based SL and TP", overlay=true)

// Input parameters for fast and long EFI
efi_fast_length = input.int(13, "Fast EFI Length", minval=1)
efi_long_length = input.int(50, "Long EFI Length", minval=1)
stdev_length = input.int(50, "Standard Deviation Length", minval=2, maxval=300)
numdev = input.float(2, "Number of Deviations", minval=1, maxval=20, step=0.1)
atr_length = input.int(14, "ATR Length", minval=1)
atr_multiplier_sl = input.float(1.5, "ATR Multiplier for Stop Loss", step=0.1)
trailing_tp_multiplier = input.float(0.5, "Multiplier for Trailing Take Profit", step=0.1)

// Elder's Force Index Calculation for Fast and Long EFI
efi_fast = ta.ema((close - close[1]) * volume, efi_fast_length)
efi_long = ta.ema((close - close[1]) * volume, efi_long_length)

// Calculate Standard Deviation for Fast EFI
efi_fast_average = ta.sma(efi_fast, stdev_length)
efi_fast_stdev = ta.stdev(efi_fast, stdev_length)
efi_fast_diff = efi_fast - efi_fast_average
efi_fast_result = efi_fast_diff / efi_fast_stdev

// Calculate Standard Deviation for Long EFI
efi_long_average = ta.sma(efi_long, stdev_length)
efi_long_stdev = ta.stdev(efi_long, stdev_length)
efi_long_diff = efi_long - efi_long_average
efi_long_result = efi_long_diff / efi_long_stdev

// Define upper and lower standard deviation levels
upper_sd = numdev
lower_sd = -numdev

// Define entry conditions based on crossing upper and lower standard deviations
long_condition = efi_fast_result > upper_sd and efi_long_result > upper_sd
short_condition = efi_fast_result < lower_sd and efi_long_result < lower_sd

// Check if a position is already open
is_position_open = strategy.position_size != 0

// Calculate ATR for stop loss and take profit
atr = ta.atr(atr_length)

// Initialize stop loss and take profit variables
var float stop_loss = na
var float take_profit = na

// Execute trades based on conditions, ensuring only one trade at a time
if (long_condition and not is_position_open)
    strategy.entry("Long", strategy.long)
    stop_loss := close - atr * atr_multiplier_sl  // Set initial stop loss based on ATR
    take_profit := close + atr * trailing_tp_multiplier  // Set initial take profit based on ATR

if (short_condition and not is_position_open)
    strategy.entry("Short", strategy.short)
    stop_loss := close + atr * atr_multiplier_sl  // Set initial stop loss based on ATR
    take_profit := close - atr * trailing_tp_multiplier  // Set initial take profit based on ATR

// Update exit conditions
if (is_position_open)
    // Update stop loss for trailing
    if (strategy.position_size > 0)  // For long positions
        stop_loss := math.max(stop_loss, close - atr * atr_multiplier_sl)
        
        // Adjust take profit based on price movement
        take_profit := math.max(take_profit, close + atr * trailing_tp_multiplier)

    else if (strategy.position_size < 0)  // For short positions
        stop_loss := math.min(stop_loss, close + atr * atr_multiplier_sl)
        
        // Adjust take profit based on price movement
        take_profit := math.min(take_profit, close - atr * trailing_tp_multiplier)

    // Set exit conditions
    strategy.exit("Long Exit", from_entry="Long", stop=stop_loss, limit=take_profit)
    strategy.exit("Short Exit", from_entry="Short", stop=stop_loss, limit=take_profit)

```

> Detail

https://www.fmz.com/strategy/473264

> Last Modified

2024-11-28 17:08:24
