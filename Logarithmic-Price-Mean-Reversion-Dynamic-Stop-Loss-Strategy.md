
> Name

Logarithmic-Price-Mean-Reversion-Dynamic-Stop-Loss-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d7f2157e0d4167c11c27.png)
![IMG](https://www.fmz.com/upload/asset/2d92cc2b50f875d1ee0b4.png)


[trans]
#### Overview
Logarithmic price mean reversion dynamic stop loss strategy is a quantitative trading strategy based on statistical principles, which mainly uses the characteristics of price fluctuations around its mean value for trading. This strategy converts prices into logarithmic form and then calculates their Z-score (multiple of standard deviations) to measure how much prices deviate from the mean. When the Z-score reaches a certain threshold, the strategy considers the market to be overbought or oversold and trades on the basis of expected price reversion to the mean. The unique feature of this strategy is its dynamic stop-loss mechanism, which can automatically adjust the stop-loss level according to changes in market volatility and improve risk management efficiency.
#### Strategy Principle
The core principles of this strategy are based on the theory of mean reversion and the statistical properties of logarithmic prices. The specific implementation steps are as follows:
1. First, the strategy converts the closing price into logarithmic form (`log_price = math.log(close)`), which helps convert multiplicative changes into additive changes, making price changes more consistent with a normal distribution.
2. Then, based on the set rolling window (default 7 periods), calculate the moving average (`rolling_mean`) and standard deviation (`rolling_std`) of the logarithmic price.
3. Use these statistics to calculate the Z score of the current logarithmic price: `rolling_z_score = (log_price - rolling_mean) / rolling_std`, which represents the standard deviation multiple of the current price from the mean.
4. The entry conditions are set as follows:
   - Open a long position when the Z-score is below the set long entry threshold (default -1.825).
   - Open a short position when the Z-score is higher than the set short entry threshold (default 1.825).
5. The take profit target is set as the exponential form of the moving average of the logarithmic price: `take_profit_price = math.exp(rolling_mean)`, which means that the goal of the strategy is to return the price to its statistical mean.
6. The dynamic stop loss mechanism is the key innovation of this strategy:
   - The initial stop loss is set based on the Z-score and volatility at the time of entry.
   - As market volatility changes, the stop loss level will be dynamically adjusted:
     - When volatility increases, the long stop will be lowered and the short stop will be raised, providing more trading space.
     - When volatility decreases, the long stop will be raised and the short stop will be lowered to protect existing profits.
7. Exit logic includes two situations:
   - The price reaches the take profit level (reversion to the mean).
   - The price hits the dynamically adjusted stop loss level.
#### Strategic Advantages
1. **Statistical Basics**: The strategy is based on solid statistical principles and uses Z-score to measure the degree of price deviation, providing objective entry and exit signals.
2. **Logarithmic price conversion**: Using logarithmic prices instead of original prices for calculation makes price changes more consistent with normal distribution and improves the effectiveness of statistical indicators.
3. **Dynamic Risk Management**: The biggest highlight of the strategy is its dynamic stop loss mechanism, which can automatically adjust the stop loss level according to changes in market volatility, allowing sufficient trading space while protecting funds.
4. **Two-way trading**: The strategy supports both long and short transactions, and can find opportunities in various market environments.
5. **Mean value as target**: Using the statistical mean as the profit-taking target is in line with the theoretical basis of mean reversion and improves the rationality of profit-taking.
6. **Adjustable Parameters**: The strategy provides multiple adjustable parameters, including rolling window, entry Z-score and stop-loss Z-score, allowing traders to adjust according to different markets and personal risk preferences.
#### Strategy Risk
1. **Mean Reversion Assumption Risk**: The core assumption of the strategy is that the price will return to its statistical mean, but in trending markets or structurally changing markets, this assumption may fail, leading to long-term losses. Solution: You can add a trend filter to pause trading in strongly trending markets.
2. **Overly Sensitive Z-Score**: In extremely low-volatility markets, even small fluctuations in price can produce large Z-score changes, triggering unnecessary trading signals. Solution: Set a minimum volatility threshold, or adjust the entry threshold in a low volatility environment.
3. **Window length sensitivity**: Strategy performance is very sensitive to the rolling window length parameter, and improper selection may lead to overtrading or missed opportunities. Solution: You can find the optimal parameters by backtesting different window lengths, or use adaptive window lengths.
4. **Data Missing Risk**: In the early stages of trading, the lack of sufficient historical data to calculate the moving average and standard deviation may lead to unstable signals. Solution: Make sure there is a sufficient warm-up period before calculating the indicator.
5. **Stop-loss adjustment strategy risk**: Although the dynamic stop-loss mechanism is innovative, it may also lead to excessive adjustment of the stop-loss position when volatility changes drastically. Solution: You can set the maximum limit of stop loss adjustment to prevent excessive adjustment.
#### Strategy optimization direction
1. **Adaptive window length**: The current strategy uses a fixed rolling window length (default 7 periods) to calculate statistical indicators. Consider implementing adaptive window lengths to automatically adjust the window size based on cyclical changes in the market. This can better capture mean reversion opportunities at different time scales and improve the adaptability of the strategy.
2. **Trend Filter**: Add a trend judgment mechanism, pause or adjust strategy parameters in strong trending markets, and only apply mean reversion strategies in sideways or reversal markets. This can be achieved by adding a long-term moving average or a trend indicator such as ADX to avoid frequent losses in unilateral trending markets.
3. **Multi-time frame analysis**: Integrate Z-score signals from multiple time frames to form a more comprehensive entry and exit decision. For example, you can identify mean reversion opportunities on a larger time frame, and then find precise entry points on a smaller time frame to improve your win rate and risk-reward ratio.
4. **Take profit optimization**: The current strategy uses a simple average as the take profit target. Consider implementing a dynamic take-profit mechanism, such as setting a take-profit target based on market structure or the risk-reward ratio associated with the stop-loss, or implementing a partial take-profit strategy that gradually locks in profits as the price moves in a favorable direction.
5. **Volatility weighting**: Consider adding a volatility weighting mechanism when calculating the Z score to give higher weight to data in more stable periods. This can reduce the interference of extreme fluctuations on signal generation and improve signal quality.
6. **Machine learning integration**: Consider introducing machine learning algorithms to optimize entry and exit thresholds. Models can be trained based on historical data to predict optimal Z-score thresholds and dynamic stop loss parameters to improve the adaptive ability and overall performance of the strategy.
#### Summarize
The logarithmic price mean reversion dynamic stop loss strategy is a quantitative trading strategy based on statistical principles. It identifies the overbought and oversold status of the market by calculating the Z score of the logarithmic price, and makes profits when the price is expected to return to the mean. The core innovation of this strategy is its dynamic stop-loss mechanism, which can automatically adjust risk parameters according to changes in market volatility and provide better risk management.
Although the strategy is based on a solid statistical foundation, it still faces challenges such as possible failure of mean reversion assumptions, parameter sensitivity, and adaptability to market environments. By incorporating improvements such as trend filters, adaptive window lengths, multi-timeframe analysis, and machine learning optimization, the strategy has the potential to achieve more consistent performance in a variety of market environments.
It is worth noting that any quantitative strategy needs to be fully back-tested and forward-validated, and parameters adjusted according to specific market characteristics and personal risk preferences. The strategy provides a framework that combines statistical principles and dynamic risk management, on which traders can further customize and optimize.
|| 

#### Overview

The Logarithmic Price Mean Reversion Dynamic Stop-Loss Strategy is a quantitative trading approach based on statistical principles, leveraging the tendency of prices to oscillate around their mean. This strategy converts prices into logarithmic form and calculates Z-scores (standard deviation multiples) to measure price deviation from the mean. When the Z-score reaches specific thresholds, the strategy identifies overbought or oversold conditions and executes trades based on the expectation that prices will revert to their mean. What sets this strategy apart is its dynamic stop-loss mechanism, which automatically adjusts stop-loss levels according to changes in market volatility, enhancing risk management efficiency.

#### Strategy Principles

The core principles of this strategy are based on mean reversion theory and the statistical properties of logarithmic prices. The implementation follows these steps:

1. First, the strategy converts closing prices into logarithmic form (`log_price = math.log(close)`), which helps transform multiplicative changes into additive changes, making price movements more normally distributed.

2. Then, based on a defined rolling window (default 7 periods), it calculates the moving average (`rolling_mean`) and standard deviation (`rolling_std`) of the logarithmic prices.

3. Using these statistics, it calculates the current Z-score of the logarithmic price: `rolling_z_score = (log_price - rolling_mean) / rolling_std`, which represents how many standard deviations the current price is away from the mean.

4. Entry conditions are set as follows:
   - When the Z-score falls below the long entry threshold (default -1.825), a long position is opened.
   - When the Z-score rises above the short entry threshold (default 1.825), a short position is opened.

5. The take-profit target is set at the exponential form of the moving average of logarithmic price: `take_profit_price = math.exp(rolling_mean)`, meaning the strategy aims for price to revert to its statistical mean.

6. The dynamic stop-loss mechanism is the key innovation of this strategy:
   - Initial stop-loss positions are set based on the Z-score and volatility at entry.
   - As market volatility changes, stop-loss positions are dynamically adjusted:
     - When volatility increases, long stop-losses decrease and short stop-losses increase, providing more trading room.
     - When volatility decreases, long stop-losses increase and short stop-losses decrease, protecting existing profits.

7. Exit logic includes two scenarios:
   - Price reaches the take-profit level (reverts to the mean).
   - Price hits the dynamically adjusted stop-loss level.

#### Strategy Advantages

1. **Statistical Foundation**: The strategy is based on solid statistical principles, using Z-scores to measure price deviation, providing objective entry and exit signals.

2. **Logarithmic Price Transformation**: Using logarithmic prices instead of raw prices makes price movements more normally distributed, improving the effectiveness of statistical indicators.

3. **Dynamic Risk Management**: The strategy's standout feature is its dynamic stop-loss mechanism, which automatically adjusts stop-loss levels based on changes in market volatility, protecting capital while allowing sufficient trading room.

4. **Bidirectional Trading**: The strategy supports both long and short trades, enabling opportunity seeking in various market environments.

5. **Mean as Target**: Using the statistical mean as a take-profit target aligns with mean reversion theory, enhancing the rationality of profit-taking.

6. **Adjustable Parameters**: The strategy offers multiple adjustable parameters, including rolling window, entry Z-scores, and stop-loss Z-scores, allowing traders to adapt to different markets and personal risk preferences.

#### Strategy Risks

1. **Mean Reversion Assumption Risk**: The core assumption that prices will revert to their statistical mean may fail in trending markets or during structural changes, leading to sustained losses. Solution: Add trend filters to pause trading in strong trend markets.

2. **Overly Sensitive Z-scores**: In extremely low volatility markets, even small price movements can generate large Z-score changes, triggering unnecessary trading signals. Solution: Set minimum volatility thresholds or adjust entry thresholds in low volatility environments.

3. **Window Length Sensitivity**: Strategy performance is highly sensitive to the rolling window length parameter; inappropriate choices may lead to overtrading or missed opportunities. Solution: Find optimal parameters through backtesting different window lengths or use adaptive window lengths.

4. **Data Shortage Risk**: In the early stages of trading, lack of sufficient historical data to calculate moving averages and standard deviations may lead to unstable signals. Solution: Ensure an adequate warm-up period before calculating indicators.

5. **Stop-Loss Adjustment Strategy Risk**: While innovative, the dynamic stop-loss mechanism may lead to excessive stop-loss adjustments during rapid volatility changes. Solution: Set maximum adjustment limits to prevent over-adjustment.

#### Strategy Optimization Directions

1. **Adaptive Window Length**: The current strategy uses a fixed rolling window length (default 7 periods) to calculate statistical indicators. Consider implementing an adaptive window length that automatically adjusts based on market cyclicality. This can better capture mean reversion opportunities at different time scales, improving strategy adaptability.

2. **Trend Filter**: Incorporate trend determination mechanisms to pause or adjust strategy parameters in strong trend markets, applying mean reversion strategy only in ranging or reversal markets. This can be implemented by adding long-term moving averages or trend indicators like ADX, avoiding frequent losses in one-sided trend markets.

3. **Multi-timeframe Analysis**: Integrate Z-score signals from multiple timeframes for more comprehensive entry and exit decisions. For example, confirm mean reversion opportunities in larger timeframes, then seek precise entry points in smaller timeframes, improving win rates and risk-reward ratios.

4. **Take-profit Optimization**: The current strategy uses a simple mean as the take-profit target. Consider implementing dynamic take-profit mechanisms, such as setting targets based on market structure or risk-reward ratios associated with stop-losses, or implementing partial take-profit strategies to progressively lock in profits as price moves favorably.

5. **Volatility Weighting**: Consider incorporating volatility weighting when calculating Z-scores, giving higher weight to data from more stable periods. This can reduce the interference of extreme volatility on signal generation, improving signal quality.

6. **Machine Learning Integration**: Consider introducing machine learning algorithms to optimize entry and exit thresholds. Models can be trained on historical data to predict optimal Z-score thresholds and dynamic stop-loss parameters, enhancing the strategy's adaptability and overall performance.

#### Conclusion

The Logarithmic Price Mean Reversion Dynamic Stop-Loss Strategy is a quantitative trading approach based on statistical principles, identifying market overbought and oversold conditions through logarithmic price Z-scores and profiting when prices are expected to revert to their mean. The core innovation lies in its dynamic stop-loss mechanism, which automatically adjusts risk parameters based on market volatility changes, providing superior risk management.

While based on solid statistical foundations, the strategy still faces challenges such as potential failure of the mean reversion assumption, parameter sensitivity, and market environment adaptability. By incorporating trend filters, adaptive window lengths, multi-timeframe analysis, and machine learning optimizations, the strategy has the potential to achieve more stable performance across various market environments.

It's worth noting that any quantitative strategy requires thorough backtesting and forward validation, with parameter adjustments based on specific market characteristics and personal risk preferences. This strategy provides a framework that integrates statistical principles and dynamic risk management, which traders can further customize and optimize.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-14 00:00:00
end: 2025-03-12 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Mean Reversion Z-Score Strategy with Dynamic SL", overlay=true)

// Input parameters
window = input.int(7, "Rolling Window", minval=1)
z_entry_long = input.float(-1.825, "Z-Score Long Entry", step=0.025)
z_entry_short = input.float(1.825, "Z-Score Short Entry", step=0.025)
z_stop_loss_long = input.float(-2.125, "Z-Score Stop Loss Long", step=0.025)
z_stop_loss_short = input.float(2.125, "Z-Score Stop Loss Short", step=0.025)

// Calculate log price, rolling mean, and rolling standard deviation
log_price = math.log(close)
rolling_mean = ta.sma(log_price, window)
rolling_std = ta.stdev(log_price, window)
rolling_z_score = (log_price - rolling_mean) / rolling_std

// Persistent variables to store entry conditions
var float entry_price = 0.0
var float entry_log_price = 0.0
var float entry_mean = 0.0
var float entry_std = 0.0
var float stop_loss_price = 0.0
var string position = "none"

// Calculate dynamic take-profit
take_profit_price = math.exp(rolling_mean)

// Entry logic
if (rolling_z_score <= z_entry_long and position == "none")
    entry_price := close
    entry_log_price := log_price
    entry_mean := rolling_mean
    entry_std := rolling_std
    stop_loss_price := math.exp(log_price + z_stop_loss_long * rolling_std)
    position := "long"
    strategy.entry("Long", strategy.long)

if (rolling_z_score >= z_entry_short and position == "none")
    entry_price := close
    entry_log_price := log_price
    entry_mean := rolling_mean
    entry_std := rolling_std
    stop_loss_price := math.exp(log_price - z_stop_loss_short * rolling_std)
    position := "short"
    strategy.entry("Short", strategy.short)

// Exit logic with dynamic adjustments
if (position != "none")
    // Calculate new stop-loss based on current volatility
    float new_stop_loss = na
    if (position == "long")
        new_stop_loss := math.exp(log_price + z_stop_loss_long * rolling_std)
        if (rolling_std > entry_std)
            stop_loss_price := math.min(stop_loss_price, new_stop_loss)
        else if (rolling_std < entry_std)
            stop_loss_price := math.max(stop_loss_price, new_stop_loss)
        if (close >= take_profit_price)
            strategy.close("Long", comment="TP")
            position := "none"
        else if (close <= stop_loss_price)
            strategy.close("Long", comment="SL")
            position := "none"
    else if (position == "short")
        new_stop_loss := math.exp(log_price - z_stop_loss_short * rolling_std)
        if (rolling_std > entry_std)
            stop_loss_price := math.max(stop_loss_price, new_stop_loss)
        else if (rolling_std < entry_std)
            stop_loss_price := math.min(stop_loss_price, new_stop_loss)
        if (close <= take_profit_price)
            strategy.close("Short", comment="TP")
            position := "none"
        else if (close >= stop_loss_price)
            strategy.close("Short", comment="SL")
            position := "none"

// Plots
plot(rolling_z_score, title="Z-Score", color=color.blue, linewidth=1)
plot(z_entry_short, title="Z-Score-upper", color=color.rgb(33, 243, 103), linewidth=1)
plot(z_entry_long, title="Z-Score-lower", color=color.rgb(243, 33, 61), linewidth=1)

```

> Detail

https://www.fmz.com/strategy/486567

> Last Modified

2025-03-14 09:39:36
