
> Name

Dynamic-Volatility-Index-VIDYA-with-ATR-Trend-Following-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1321474433722e93ff6.png)

[trans]
#### Overview
This strategy is a trend tracking trading system based on the dynamic volatility indicator (VIDYA), which combines ATR fluctuations to enhance trend identification and risk management capabilities. By dynamically adjusting the response speed to market fluctuations, this strategy can capture market reversal signals in a timely manner while maintaining trend tracking capabilities. The system uses VIDYA as the core indicator and sets dynamic stop loss positions in conjunction with ATR fluctuations, achieving intelligent adaptation to market fluctuations.
#### Strategy Principle
The core of the strategy is to use the dynamic properties of the VIDYA indicator to identify trends. VIDYA dynamically adjusts the weight of the moving average by calculating momentum changes, thereby having different sensitivities in different market environments. Specifically:
1. Use the Chande Momentum Oscillator (CMO) to calculate price momentum
2. Calculate adaptive factor alpha based on momentum
3. Combined with ATR to construct a dynamic fluctuation zone
4. The price breaks through the upper band to generate a long signal, and the price breaks through the lower band to generate a short signal.
5. Use position reversal logic, that is, new signals will close old positions and open new positions at the same time
#### Strategic Advantages
1. Strong dynamic adaptability: VIDYA indicator can automatically adjust parameters according to market fluctuations to avoid the lag problem of traditional moving averages.
2. Improved risk control: Stop loss can be set through the dynamic fluctuation of ATR, which can adapt to different market environments.
3. Clear signals: Using trend reversal logic, trading signals are clear and easy to execute.
4. Good visualization effect: distinguish rising and falling trends through color, and intuitively display the market status
5. Strong parameter adjustability: key parameters can be optimized according to different market characteristics
#### Strategy Risk
1. Volatile market risk: In sideways and volatile markets, false signals are easily generated, leading to frequent trading.
2. Impact of slippage: Due to the reversal strategy, each signal involves two-way transactions and is susceptible to slippage.
3. Fund management risk: Fixed proportion position management may cause large losses during violent fluctuations
4. Parameter sensitivity: The parameter settings of VIDYA and ATR have a greater impact on strategy performance.
5. Dependence on market environment: It performs better in markets with obvious trends, but may perform poorly in other market environments.
#### Strategy optimization direction
1. Add trend filter: Long-term trend judgment can be added to filter out signals that shock the market.
2. Optimize position management: Consider introducing dynamic position management and adjust the position ratio according to market fluctuations
3. Improve entry logic: confirmation of other technical indicators can be added to improve signal reliability
4. Improve the stop loss mechanism: Consider adding a trailing stop or a volatility-based dynamic stop.
5. Add time filtering: strategy parameters can be adjusted according to market characteristics in different time periods
#### Summary
This strategy achieves dynamic tracking of market trends and risk control by combining VIDYA and ATR. Its core advantage lies in its ability to adapt to market fluctuations and capture reversal opportunities in a timely manner while maintaining trend tracking capabilities. Although it may face risks in certain market environments, this strategy still has good practical value through reasonable parameter optimization and risk management measures. It is recommended that investors pay attention to risk control when using real offers, set parameters reasonably, and adjust strategy settings in a timely manner according to market conditions. ||
#### Overview
This strategy is a trend-following trading system based on the Variable Index Dynamic Average (VIDYA), combined with ATR bands to enhance trend identification and risk management capabilities. The strategy dynamically adjusts its response to market volatility while maintaining trend-following capabilities and capturing market reversal signals. The system uses VIDYA as its core indicator and ATR bands for dynamic stop-loss placement.

#### Strategy Principles
The core principle lies in utilizing VIDYA's dynamic characteristics for trend identification. VIDYA adjusts moving average weights through momentum calculations, providing different sensitivities in various market conditions:
1. Uses Chande Momentum Oscillator (CMO) for price momentum calculation
2. Calculates adaptive factor alpha based on momentum
3. Constructs dynamic volatility bands using ATR
4. Generates long signals on upper band breakout and short signals on lower band breakout
5. Employs position reversal logic - new signals close existing positions and open new ones

#### Strategy Advantages
1. Strong Dynamic Adaptation: VIDYA automatically adjusts parameters based on market volatility
2. Comprehensive Risk Control: Uses ATR dynamic bands for stop-loss adaptation
3. Clear Signals: Employs trend reversal logic with distinct trading signals
4. Excellent Visualization: Distinguishes upward and downward trends through color coding
5. Flexible Parameters: Key parameters can be optimized for different market characteristics

#### Strategy Risks
1. Choppy Market Risk: Prone to false signals in ranging markets
2. Slippage Impact: Dual-direction trades on each signal increase slippage exposure
3. Money Management Risk: Fixed position sizing may lead to significant losses in volatile markets
4. Parameter Sensitivity: Strategy performance heavily depends on VIDYA and ATR parameters
5. Market Environment Dependency: Performs well in trending markets but may struggle in others

#### Optimization Directions
1. Add Trend Filters: Implement long-term trend assessment to filter signals in ranging markets
2. Improve Position Management: Introduce dynamic position sizing based on market volatility
3. Enhance Entry Logic: Add technical indicator confirmation for improved signal reliability
4. Refine Stop-Loss Mechanism: Consider trailing stops or volatility-based dynamic stops
5. Include Time Filters: Adjust strategy parameters based on different time period characteristics

#### Summary
This strategy achieves dynamic trend tracking and risk control by combining VIDYA and ATR. Its core strength lies in adapting to market volatility while maintaining trend-following capabilities and capturing reversal opportunities. Though it may face risks in certain market conditions, the strategy maintains practical value through proper parameter optimization and risk management measures. Investors should focus on risk control, appropriate parameter settings, and timely strategy adjustments based on market conditions in live trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-11 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © PakunFX

//@version=5
strategy("VIDYA Auto-Trading(Reversal Logic)", overlay=true)

// ＩＮＰＵＴＳ ――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
int   vidya_length   = input.int(10, "VIDYA Length")       
int   vidya_momentum = input.int(20, "VIDYA Momentum")    
float band_distance  = input.float(2, "Distance factor for upper/lower bands", step = 0.1)  
float source         = input.source(close, "Source")    
color up_trend_color   = input(#17dfad, "+")  
color down_trend_color = input(#dd326b, "-")  
bool  shadow           = input.bool(true, "Shadow") 

// Define VIDYA (Variable Index Dynamic Average) function
vidya_calc(src, vidya_length, vidya_momentum) =>
    float momentum         = ta.change(src)
    float sum_pos_momentum = math.sum((momentum >= 0) ? momentum : 0.0, vidya_momentum)
    float sum_neg_momentum = math.sum((momentum >= 0) ? 0.0 : -momentum, vidya_momentum)
    float abs_cmo          = math.abs(100 * (sum_pos_momentum - sum_neg_momentum) / (sum_pos_momentum + sum_neg_momentum))
    float alpha            = 2 / (vidya_length + 1)
    var float vidya_value  = 0.0
    vidya_value           := alpha * abs_cmo / 100 * src + (1 - alpha * abs_cmo / 100) * nz(vidya_value[1])

    ta.sma(vidya_value, 15)

// Calculate VIDYA
float vidya_value = vidya_calc(source, vidya_length, vidya_momentum)

// Calculate upper and lower bands
float atr_value = ta.atr(200)
float upper_band = vidya_value + atr_value * band_distance
float lower_band = vidya_value - atr_value * band_distance

// Detect trend direction
bool is_trend_up = na
if ta.crossover(source, upper_band)
    is_trend_up := true
if ta.crossunder(source, lower_band)
    is_trend_up := false

// Smooth the trend line
float smoothed_value = na
if is_trend_up
    smoothed_value := lower_band
if not is_trend_up
    smoothed_value := upper_band

// Detect trend change
bool trend_cross_up = ta.crossover(source, upper_band)
bool trend_cross_down = ta.crossunder(source, lower_band)

// ＥＮＴＲＹ ＆ ＥＸＩＴ ―――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
// Long logic: Enter long when down arrow appears and exit when up arrow appears
if trend_cross_up
    strategy.close("Sell")  // Close short position if any
    strategy.entry("Buy", strategy.long)

if trend_cross_down
    strategy.close("Buy")  // Close long position if any
    strategy.entry("Sell", strategy.short)
```

> Detail

https://www.fmz.com/strategy/474953

> Last Modified

2024-12-13 10:21:14
