
> Name

Multi-Technical-Indicator-Momentum-MA-Trend-Following-Strategy based on a combination of momentum and moving average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/158791d2c381c2f1ab7.png)

[trans]
#### Overview
This strategy is a trend following trading system based on multiple technical indicators, which mainly combines MACD indicators, RSI indicators and moving averages (MA) to confirm trading signals. The strategy adopts a conservative money management approach and controls risk by setting stop losses and multiple profit targets. This strategy focuses on capturing the market's upward trend and only executes long trades.
#### Strategy Principle
The core logic of the strategy is based on the collaborative confirmation of three technical indicators:
1. Use the MACD indicator to identify momentum - an initial buy signal is generated when the MACD line crosses the signal line
2. Use the RSI indicator to confirm strength - requires the RSI value to be greater than a set threshold (default 50) to confirm upward momentum
3. Use the moving average system to confirm the trend - MA50 is above MA200 to confirm the overall upward trend
At the same time, the strategy implements a complete fund management mechanism:
- Set risk exposure based on total account funds
- Set fixed percentage stop loss to control single trade risk
- Adopt dual profit targets (TP1 and TP2) to optimize profits
#### Strategic Advantages
1. Cross-validation of multiple technical indicators to improve the reliability of trading signals
2. Complete fund management system to effectively control risks
3. Adjustable strategy parameters and strong adaptability
4. Adopt dual profit goals to protect profits while not missing the big market trend
5. The code structure is clear and easy to maintain and optimize.
#### Strategy Risk
1. May generate too many false signals in volatile markets
2. Multiple indicator confirmations may lead to a slight delay in entry timing
3. Only supports long positions and lacks a hedging mechanism in falling markets.
4. Excessive parameter optimization may lead to overfitting
#### Strategy optimization direction
1. Introduce trading volume indicators as auxiliary confirmation
2. Add market volatility filtering mechanism
3. Optimize the exit mechanism and consider adding a trailing stop loss
4. Introduce an adaptive parameter mechanism and dynamically adjust according to market conditions
5. Add retracement control mechanism
#### Summary
This strategy builds a robust trend tracking system through the synergy of multiple technical indicators. The perfect fund management mechanism and adjustable parameter design make it highly practical and adaptable. In the future, the stability and profitability of the strategy can be further improved by increasing market status recognition and optimizing the exit mechanism.
|| 

#### Overview
This strategy is a trend-following trading system based on multiple technical indicators, combining MACD, RSI, and Moving Averages (MA) for trade signal confirmation. It employs a conservative money management approach with stop-loss and multiple profit targets for risk control. The strategy focuses on capturing upward market trends through long-only positions.

#### Strategy Principle
The core logic is based on triple technical indicator confirmation:
1. MACD for momentum identification - generates initial buy signal when MACD line crosses above signal line
2. RSI for strength confirmation - requires RSI value above set threshold (default 50) to confirm upward momentum
3. Moving Average system for trend confirmation - MA50 above MA200 confirms overall uptrend
Additionally, the strategy implements comprehensive money management:
- Risk exposure based on total account capital
- Fixed percentage stop-loss for individual trade risk control
- Dual profit targets (TP1 and TP2) for optimized returns

#### Strategy Advantages
1. Multiple technical indicator cross-validation increases signal reliability
2. Comprehensive money management system for effective risk control
3. Adjustable strategy parameters for high adaptability
4. Dual profit targets protect profits while capturing larger trends
5. Clear code structure for easy maintenance and optimization

#### Strategy Risks
1. Potential false signals in consolidating markets
2. Multiple indicator confirmation may lead to slightly delayed entries
3. Long-only approach lacks hedging in declining markets
4. Parameter optimization risks overfitting

#### Optimization Directions
1. Incorporate volume indicators for additional confirmation
2. Add market volatility filtering mechanism
3. Enhance exit mechanism with trailing stops
4. Implement adaptive parameter system based on market conditions
5. Add drawdown control mechanism

#### Summary
This strategy builds a robust trend-following system through the synergy of multiple technical indicators. Its comprehensive money management mechanism and adjustable parameter design provide good practicality and adaptability. Future improvements can focus on market state identification and exit mechanism optimization to further enhance strategy stability and profitability.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-29 00:00:00
end: 2025-01-05 00:00:00
period: 15m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Saudi Market Buy-Only Strategy (Customizable)", overlay=true)

// مدخلات المستخدم لتخصيص القيم
// رأس المال وإدارة المخاطر
capital = input.float(10000, title="رأس المال (ريال)", minval=1000)    // رأس المال الافتراضي
riskPercent = input.float(2, title="نسبة المخاطرة (%)", minval=0.1, maxval=10) / 100  // نسبة المخاطرة
buySLPercent = input.float(1, title="وقف الخسارة (%)", minval=0.1, maxval=10) / 100  // وقف الخسارة
tp1Percent = input.float(2, title="الهدف الأول (%)", minval=0.1, maxval=20) / 100   // الهدف الأول
tp2Percent = input.float(3, title="الهدف الثاني (%)", minval=0.1, maxval=30) / 100 // الهدف الثاني

// إعدادات المؤشرات الفنية
macdFastLength = input.int(12, title="MACD - فترة المتوسط السريع", minval=1)
macdSlowLength = input.int(26, title="MACD - فترة المتوسط البطيء", minval=1)
macdSignalLength = input.int(9, title="MACD - فترة الإشارة", minval=1)

rsiLength = input.int(14, title="RSI - فترة المؤشر", minval=1)
rsiThreshold = input.int(50, title="RSI - مستوى الدخول", minval=1, maxval=100)

ma50Length = input.int(50, title="MA50 - فترة المتوسط المتحرك", minval=1)
ma200Length = input.int(200, title="MA200 - فترة المتوسط المتحرك", minval=1)

// حساب إدارة المخاطر
riskAmount = capital * riskPercent  // قيمة المخاطرة

// حساب المؤشرات الفنية
[macdLine, signalLine, _] = ta.macd(close, macdFastLength, macdSlowLength, macdSignalLength)
rsiValue = ta.rsi(close, rsiLength)
ma50 = ta.sma(close, ma50Length)
ma200 = ta.sma(close, ma200Length)

// تعريف الاتجاه العام للسوق باستخدام المتوسطات
isBullishTrend = ma50 > ma200

// شروط الدخول شراء فقط
if ta.crossover(macdLine, signalLine) and rsiValue > rsiThreshold and isBullishTrend
    entryPrice = close
    stopLoss = entryPrice * (1 - buySLPercent)   // وقف الخسارة أسفل نقطة الدخول
    takeProfit1 = entryPrice * (1 + tp1Percent) // الهدف الأول
    takeProfit2 = entryPrice * (1 + tp2Percent) // الهدف الثاني
    strategy.entry("Buy", strategy.long)        // فتح صفقة شراء
    strategy.exit("TP1", "Buy", limit=takeProfit1, stop=stopLoss)
    strategy.exit("TP2", "Buy", limit=takeProfit2)

// رسم خطوط المتوسطات
plot(ma50, color=color.blue, title="MA50")
plot(ma200, color=color.orange, title="MA200")

```

> Detail

https://www.fmz.com/strategy/477612

> Last Modified

2025-01-06 16:56:14
