
> Name

Logarithmic-Weighted-Moving-Average-Trading-Strategy-Based-on-Cross-Signal-Analysis-Quantitative trading strategy based on log-weighted moving average cross signals
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c30feb4411a822738c.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on logarithmic transformation and weighted moving average (WMA) crossover. It reduces market noise by logarithmically transforming price data and uses the crossover of short-term and long-term WMAs to generate trading signals. The core idea of ​​the strategy is to convert price fluctuations into logarithmic space for smoothing, thereby obtaining a more stable trend judgment.
#### Strategy Principle
The strategy first logarithmically transforms the closing price to reduce the impact of extreme values on price fluctuations. Then calculate the short-term (5-period) and long-term (20-period) weighted moving averages respectively. When the short-term WMA crosses the long-term WMA upward, the system generates a long signal; when the short-term WMA crosses the long-term WMA downward, the system generates a short signal. Trend tracking is achieved by determining the trend transition point by crossing the logarithm-transformed moving average.
#### Strategic Advantages
1. Logarithmic transformation can effectively reduce the impact of extreme values on price fluctuations and make trend judgment more stable.
2. Using a weighted moving average can respond to price changes faster than a simple moving average.
3. The crossover signal of the double moving average is clear, avoiding false signals that may be caused by a single indicator.
4. The system has automatic transaction execution function, which reduces the delay and emotional impact caused by human operations.
5. Real-time warning function ensures that important trading opportunities will not be missed
#### Strategy Risk
1. In a volatile market, more false signals may be generated, leading to frequent transactions and increased costs.
2. Logarithmic transformation may delay signal generation in extreme market conditions
3. Fixed moving average periods may not be suitable for all market environments
It is recommended to manage risks by setting stop loss conditions and position control, and at the same time, it can be combined with other technical indicators for signal confirmation.
#### Strategy optimization direction
1. Introduce adaptive moving average cycles and dynamically adjust parameters according to market volatility
2. Add auxiliary indicators such as trading volume to confirm trading signals
3. Add trend strength filter to avoid trading in weak trend environment
4. Optimize stop-loss and take-profit conditions to improve capital utilization efficiency
5. Consider adding a retracement control mechanism to prevent large losses
#### Summary
This is a trend following strategy that combines a logarithmic transformation with a weighted moving average. Reduce the impact of price fluctuations through logarithmic transformation, and use dual moving average crossovers to capture trend transition points. The strategy logic is clear and has good operability, but attention needs to be paid to risk control in volatile markets. By optimizing parameter settings and adding auxiliary indicators, this strategy is expected to achieve better performance.
|| 

#### Overview
This strategy is a quantitative trading system based on logarithmic transformation and Weighted Moving Average (WMA) crossovers. It reduces market noise by applying logarithmic transformation to price data and generates trading signals through the intersection of short-term and long-term WMAs. The core concept is to smooth price fluctuations in logarithmic space for more stable trend identification.

#### Strategy Principle
The strategy first applies logarithmic transformation to closing prices to minimize the impact of extreme price movements. It then calculates short-term (5-period) and long-term (20-period) weighted moving averages. The system generates long signals when the short-term WMA crosses above the long-term WMA, and short signals when the short-term WMA crosses below the long-term WMA. Trend transition points are identified through moving average crossovers in logarithmic space, enabling effective trend following.

#### Strategy Advantages
1. Logarithmic transformation effectively reduces the impact of extreme price movements, leading to more stable trend identification
2. Weighted moving averages respond more quickly to price changes compared to simple moving averages
3. Dual moving average crossovers provide clear signals, avoiding false signals that might occur with single indicators
4. Automated trading execution reduces delays and emotional impacts from manual operations
5. Real-time alert system ensures no important trading opportunities are missed

#### Strategy Risks
1. May generate excessive false signals in ranging markets, leading to increased trading costs
2. Logarithmic transformation might delay signal generation in extreme market conditions
3. Fixed moving average periods may not be suitable for all market environments
Risk management through stop-loss conditions and position sizing is recommended, along with signal confirmation using additional technical indicators.

#### Strategy Optimization
1. Introduce adaptive moving average periods that dynamically adjust based on market volatility
2. Add volume and other auxiliary indicators for signal confirmation
3. Implement trend strength filters to avoid trading in weak trend environments
4. Optimize stop-loss and take-profit conditions for better capital efficiency
5. Consider adding drawdown control mechanisms to prevent significant losses

#### Summary
This is a trend-following strategy combining logarithmic transformation and weighted moving averages. It reduces price volatility impact through logarithmic transformation and captures trend transition points using dual moving average crossovers. The strategy has clear logic and good operability but requires careful risk management in ranging markets. Through parameter optimization and additional indicator integration, this strategy has potential for improved performance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-02-09 00:00:00
end: 2025-02-06 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Logaritmik WMA Al-Sat Stratejisi", overlay=true)

// Parametreler
shortWMA_length = input.int(5, title="Kısa WMA (5)")
longWMA_length = input.int(20, title="Uzun WMA (20)")

// Logaritmik Fiyat Hesaplaması
log_close = math.log(close)  // Fiyatların logaritmasını alıyoruz

// Logaritmik WMA'ların Hesaplanması
log_shortWMA = ta.wma(log_close, shortWMA_length)  // Kısa WMA (Log)
log_longWMA = ta.wma(log_close, longWMA_length)    // Uzun WMA (Log)

// WMA'ları Normal Ölçeğe Geri Dönüştürme
shortWMA = math.exp(log_shortWMA)  // Logaritmadan geri dönüştürülmüş kısa WMA
longWMA = math.exp(log_longWMA)    // Logaritmadan geri dönüştürülmüş uzun WMA

// Al-Sat Koşulları
longCondition = ta.crossover(shortWMA, longWMA)  // Kısa WMA uzun WMA'yı yukarı keserse
shortCondition = ta.crossunder(shortWMA, longWMA)  // Kısa WMA uzun WMA'yı aşağı keserse

// WMA'ları Çizdirme
plot(shortWMA, color=color.green, title="Kısa WMA (Log)", linewidth=2, style=plot.style_line)
plot(longWMA, color=color.red, title="Uzun WMA (Log)", linewidth=2, style=plot.style_line)

// İşlem Girişleri
if (longCondition)
    strategy.entry("AL", strategy.long)

if (shortCondition)
    strategy.entry("SAT", strategy.short)

// Alarm Fonksiyonu
if (longCondition)
    alert("AL Sinyali: Kısa WMA (Log), Uzun WMA (Log)'yı yukarı kesti.", alert.freq_once_per_bar_close)

if (shortCondition)
    alert("SAT Sinyali: Kısa WMA (Log), Uzun WMA (Log)'yı aşağı kesti.", alert.freq_once_per_bar_close)



```

> Detail

https://www.fmz.com/strategy/481094

> Last Modified

2025-02-08 14:53:53
