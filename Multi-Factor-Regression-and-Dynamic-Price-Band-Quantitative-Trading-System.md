
> Name

Multi-Factor-Regression-and-Dynamic-Price-Band-Quantitative-Trading-System
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/45fda41522a7554234cf6c42cdfae5c34fd6e0aeed804b7c7a010ec52e321598.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on multi-factor regression and dynamic price bands. The core logic is to predict price trends through a multi-factor regression model, combined with multiple market factors such as BTC dominance, trading volume, and lagging prices, to construct upper and lower price bands for signal generation. The strategy integrates multiple risk management modules such as outlier filtering, dynamic position management, and trailing stop loss, making it a comprehensive and robust trading system.
#### Strategy Principle
The strategy mainly includes the following core components:
1. Regression prediction module: Use multi-factor linear regression model to predict prices. Factors include BTC dominance, transaction volume, price lag terms, interaction terms, etc. Calculate the beta coefficient of each factor to measure its impact on price.
2. Dynamic price bands: Construct upper and lower price bands based on predicted prices and residual standard deviations to identify overbought and oversold.
3. Signal generation: When the price breaks through the lower track and the RSI is oversold, a long signal is generated; when the price breaks through the upper track and the RSI is overbought, a short signal is generated.
4. Risk management: including multiple protection mechanisms such as outlier filtering (Z score method), stop loss and take profit, ATR trailing stop loss, etc.
5. Dynamic position: Dynamically adjust the opening size based on ATR and preset risk ratio.
#### Strategic Advantages
1. Multi-factor integration: comprehensively consider multiple market factors to provide a comprehensive market perspective.
2. Strong adaptability: the price band will dynamically adjust according to market fluctuations and adapt to different market environments.
3. Perfect risk control: Multi-level risk management ensures the safety of funds.
4. Flexible and configurable: A large number of parameters are adjustable and easy to optimize according to different market characteristics.
5. High signal reliability: multiple filtering mechanisms improve signal quality.
#### Strategy Risk
1. Model risk: Regression models rely on historical data and may fail when the market changes drastically.
2. Parameter sensitivity: Many parameters need to be carefully tuned, and improper parameter settings will affect the strategy performance.
3. Computational complexity: Multi-factor calculation is relatively complex and may affect real-time performance.
4. Market environment dependence: Performance in volatile markets may be better than trending markets.
#### Strategy optimization direction
1. Factor selection optimization: More market factors can be introduced, such as market sentiment indicators, on-chain data, etc.
2. Dynamic parameter adjustment: Develop an adaptive parameter adjustment mechanism to improve strategy adaptability.
3. Machine learning enhancement: Introduce machine learning methods to optimize the prediction model.
4. Signal filtering enhancement: Develop more signal filtering conditions to improve accuracy.
5. Combination strategy integration: Use in combination with other strategies to improve stability.
#### Summary
This strategy is a quantitative trading system with solid theory and perfect design. Predict prices through multi-factor regression models, generate trading signals based on dynamic price bands, and are equipped with a comprehensive risk management mechanism. The strategy is highly adaptable and configurable and suitable for various market environments. Through continuous optimization and improvement, this strategy is expected to achieve stable returns in real trading. ||
#### Overview
This strategy is a quantitative trading system based on multi-factor regression and dynamic price bands. The core logic is to predict price movements through a multi-factor regression model, combining multiple market factors such as BTC dominance, trading volume, and lagged prices to construct price bands for signal generation. The strategy integrates multiple risk management modules including outlier filtering, dynamic position management, and trailing stops, making it a comprehensive and robust trading system.

#### Strategy Principles
The strategy includes the following core components:
1. Regression Prediction Module: Uses multi-factor linear regression to predict prices. Factors include BTC dominance, volume, price lags, and interaction terms. Beta coefficients measure each factor's impact on price.
2. Dynamic Price Bands: Constructs upper and lower price bands based on predicted price and residual standard deviation to identify overbought/oversold conditions.
3. Signal Generation: Generates long signals when price breaks below lower band with oversold RSI; short signals when price breaks above upper band with overbought RSI.
4. Risk Management: Multiple protection mechanisms including outlier filtering (Z-score method), stop-loss/take-profit, and ATR-based trailing stops.
5. Dynamic Positioning: Adjusts position size dynamically based on ATR and preset risk ratio.

#### Strategy Advantages
1. Multi-factor Integration: Provides comprehensive market perspective by considering multiple market factors.
2. Strong Adaptability: Price bands adjust dynamically to market volatility, adapting to different market conditions.
3. Comprehensive Risk Control: Multi-layered risk management ensures capital safety.
4. Flexible Configuration: Numerous adjustable parameters for optimization across different markets.
5. High Signal Reliability: Multiple filtering mechanisms improve signal quality.

#### Strategy Risks
1. Model Risk: Regression model relies on historical data, may fail during dramatic market changes.
2. Parameter Sensitivity: Multiple parameters require careful tuning, improper settings affect strategy performance.
3. Computational Complexity: Multi-factor calculations may impact real-time performance.
4. Market Environment Dependency: May perform better in ranging markets than trending markets.

#### Optimization Directions
1. Factor Selection Optimization: Introduce additional market factors like sentiment indicators and on-chain data.
2. Dynamic Parameter Adjustment: Develop adaptive parameter adjustment mechanisms.
3. Machine Learning Enhancement: Incorporate machine learning methods to optimize prediction model.
4. Signal Filter Enhancement: Develop additional signal filtering conditions to improve accuracy.
5. Strategy Integration: Combine with other strategies to improve stability.

#### Summary
This strategy is a theoretically sound and well-designed quantitative trading system. It predicts prices through a multi-factor regression model, generates trading signals using dynamic price bands, and features comprehensive risk management mechanisms. The strategy demonstrates strong adaptability and configurability, suitable for various market environments. Through continuous optimization and improvement, this strategy shows promise for achieving stable returns in live trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-17 00:00:00
end: 2025-01-16 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/

//@version=5
strategy(  title           = "CorrAlgoX", overlay         = true,pyramiding      = 1, initial_capital = 10000, default_qty_type= strategy.percent_of_equity, default_qty_value=200)

//====================================================================
//=========================== GİRİŞLER ================================
//====================================================================

// --- (1) REGRESYON VE OUTLIER AYARLARI
int   lengthReg         = input.int(300, "Regression Window",   minval=50)
bool  useOutlierFilter  = input.bool(false, "Z-skoru ile Outlier Filtrele")

// --- (2) FİYAT GECİKMELERİ
bool  usePriceLag2      = input.bool(false, "2 Bar Gecikmeli Fiyatı Kullan")

// --- (3) STOP-LOSS & TAKE-PROFIT
float stopLossPerc      = input.float(3.0,  "Stop Loss (%)",   step=0.1)
float takeProfitPerc    = input.float(5.0,  "Take Profit (%)", step=0.1)

// --- (4) REZİDÜEL STD BANTI
int   lengthForStd      = input.int(50, "StdDev Length (residual)", minval=2)
float stdevFactor       = input.float(2.0, "Stdev Factor", step=0.1)

// --- (5) RSI FİLTRESİ
bool  useRsiFilter      = input.bool(true, "RSI Filtresi Kullan")
int   rsiLen            = input.int(14, "RSI Length",   minval=1)
float rsiOB             = input.float(70, "RSI Overbought", step=1)
float rsiOS             = input.float(30, "RSI Oversold",   step=1)

// --- (6) TRAILING STOP
bool  useTrailingStop   = input.bool(false, "ATR Tabanlı Trailing Stop")
int   atrLen            = input.int(14, "ATR Length",   minval=1)
float trailMult         = input.float(1.0, "ATR multiplier", step=0.1)

// --- (7) DİNAMİK POZİSYON BÜYÜKLÜĞÜ (ATR tabanlı)
bool  useDynamicPos     = input.bool(false, "Dinamik Pozisyon Büyüklüğü Kullan")
float capitalRiskedPerc = input.float(1.0, "Sermaye Risk Yüzdesi", step=0.1, tooltip="Her işlemde risk alınacak sermaye yüzdesi")

// --- (8) ETKİLEŞİM VE LOG(HACİM) KULLANIMI
bool  useSynergyTerm    = input.bool(true, "BTC.D * Hacim Etkileşim Terimi")
bool  useLogVolume      = input.bool(true, "Hacmi Logaritmik Kullan")

//====================================================================
//======================= VERİLERİ AL & HAZIRLA =======================
//====================================================================

// Mevcut enstrüman fiyatı
float realClose = close

// BTC Dominance (aynı TF)
float btcDom    = request.security("SWAP", timeframe.period, close)

// Hacim
float vol       = volume

// Gecikmeli fiyatlar
float priceLag1 = close[1]
float priceLag2 = close[2]  // (isteğe bağlı)

//----------------- Outlier Filtrelemesi (Z-Skoru) ------------------//
float priceMean  = ta.sma(realClose, lengthReg)
float priceStdev = ta.stdev(realClose, lengthReg)

float zScore     = (priceStdev != 0) ? (realClose - priceMean) / priceStdev : 0
bool  isOutlier  = math.abs(zScore) > 3.0

float filteredClose = (useOutlierFilter and isOutlier) ? na : realClose

// Fiyatın stdev'i (filtrelenmiş)
float fCloseStdev = ta.stdev(filteredClose, lengthReg)

//====================================================================
//=============== ORTALAMA, STDEV, KORELASYON HESAPLARI ==============
//====================================================================

// BTC.D
float btcDomMean    = ta.sma(btcDom, lengthReg)
float btcDomStdev   = ta.stdev(btcDom, lengthReg)
float corrBtcDom    = ta.correlation(btcDom, filteredClose, lengthReg)

// Hacim
float volMean       = ta.sma(vol, lengthReg)
float volStdev      = ta.stdev(vol, lengthReg)
float corrVol       = ta.correlation(vol, filteredClose, lengthReg)

// Fiyat Lag1
float plag1Mean     = ta.sma(priceLag1, lengthReg)
float plag1Stdev    = ta.stdev(priceLag1, lengthReg)
float corrPLag1     = ta.correlation(priceLag1, filteredClose, lengthReg)

// Fiyat Lag2 (isteğe bağlı)
float plag2Mean     = ta.sma(priceLag2, lengthReg)
float plag2Stdev    = ta.stdev(priceLag2, lengthReg)
float corrPLag2     = ta.correlation(priceLag2, filteredClose, lengthReg)

// BTC.D * Hacim (synergyTerm)
float synergyTerm   = btcDom * vol
float synergyMean   = ta.sma(synergyTerm, lengthReg)
float synergyStdev  = ta.stdev(synergyTerm, lengthReg)
float corrSynergy   = ta.correlation(synergyTerm, filteredClose, lengthReg)

// Log(Hacim)
float logVolume     = math.log(vol + 1.0)
float logVolMean    = ta.sma(logVolume, lengthReg)
float logVolStdev   = ta.stdev(logVolume, lengthReg)
float corrLogVol    = ta.correlation(logVolume, filteredClose, lengthReg)

//====================================================================
//===================== FONKSIYON: BETA HESAPLAMA =====================
//====================================================================
// Pine Script'te fonksiyonlar şöyle tanımlanır (tip bildirmeyiz):
getBeta(corrVal, stdevX) =>
    (stdevX != 0 and not na(corrVal) and fCloseStdev != 0)? corrVal * (fCloseStdev / stdevX)  : 0.0

//====================================================================
//======================== BETA KATSAYILARI ===========================
//====================================================================

// BTC Dominance
float betaBtcDom  = getBeta(corrBtcDom,  btcDomStdev)
// Hacim
float betaVol     = getBeta(corrVol,     volStdev)
// Fiyat Lag1
float betaPLag1   = getBeta(corrPLag1,   plag1Stdev)
// Fiyat Lag2
float betaPLag2   = getBeta(corrPLag2,   plag2Stdev)
// synergy
float betaSynergy = getBeta(corrSynergy, synergyStdev)
// logVol
float betaLogVol  = getBeta(corrLogVol,  logVolStdev)

//====================================================================
//===================== TAHMİNİ FİYAT OLUŞTURMA ======================
//====================================================================

float alpha  = priceMean
bool canCalc = not na(filteredClose) and not na(priceMean)

float predictedPrice = na
if canCalc
    // Farklar
    float dBtcDom   = (btcDom - btcDomMean)
    float dVol      = (vol    - volMean)
    float dPLag1    = (priceLag1 - plag1Mean)
    float dPLag2    = (priceLag2 - plag2Mean)
    float dSynergy  = (synergyTerm - synergyMean)
    float dLogVol   = (logVolume   - logVolMean)

    float sumBeta   = 0.0
    sumBeta += betaBtcDom  * dBtcDom
    sumBeta += betaVol     * dVol
    sumBeta += betaPLag1   * dPLag1

    if usePriceLag2
        sumBeta += betaPLag2 * dPLag2

    if useSynergyTerm
        sumBeta += betaSynergy * dSynergy

    if useLogVolume
        sumBeta += betaLogVol * dLogVol

    predictedPrice := alpha + sumBeta

//====================================================================
//======================= REZİDÜEL & BANT ============================
//====================================================================

float residual   = filteredClose - predictedPrice
float residStdev = ta.stdev(residual, lengthForStd)

float upperBand  = predictedPrice + stdevFactor * residStdev
float lowerBand  = predictedPrice - stdevFactor * residStdev

//====================================================================
//========================= SİNYAL ÜRETİMİ ===========================
//====================================================================

bool longSignal  = (realClose < lowerBand)
bool shortSignal = (realClose > upperBand)

//------------------ RSI Filtresi (opsiyonel) -----------------------//
float rsiVal       = ta.rsi(realClose, rsiLen)
bool rsiOversold   = (rsiVal < rsiOS)
bool rsiOverbought = (rsiVal > rsiOB)

if useRsiFilter
    longSignal  := longSignal  and rsiOversold
    shortSignal := shortSignal and rsiOverbought

//====================================================================
//=============== DİNAMİK POZİSYON & GİRİŞ/ÇIKIŞ EMİRLERİ ============
//====================================================================

float myAtr      = ta.atr(atrLen)
float positionSize = na

if useDynamicPos
    float capitalRisked   = strategy.equity * (capitalRiskedPerc / 100.0)
    float riskPerUnit     = (stopLossPerc/100.0) * myAtr
    positionSize          := (riskPerUnit != 0.0) ? (capitalRisked / riskPerUnit) : na

// Long
if longSignal
    if useDynamicPos and not na(positionSize)
        strategy.entry("Long", strategy.long, qty=positionSize)
    else
        strategy.entry("Long", strategy.long)

// Short
if shortSignal
    if useDynamicPos and not na(positionSize)
        strategy.entry("Short", strategy.short, qty=positionSize)
    else
        strategy.entry("Short", strategy.short)

// Stop-Loss & Take-Profit
if strategy.position_size > 0
    strategy.exit( "Long Exit", "Long",stop  = strategy.position_avg_price * (1 - stopLossPerc/100),  limit = strategy.position_avg_price * (1 + takeProfitPerc/100))

if strategy.position_size < 0
    strategy.exit("Short Exit", "Short", stop  = strategy.position_avg_price * (1 + stopLossPerc/100),limit = strategy.position_avg_price * (1 - takeProfitPerc/100))

//------------------ TRAILING STOP (opsiyonel) ----------------------//
if useTrailingStop
    if strategy.position_size > 0
        strategy.exit(  "Long Exit TS", "Long",  trail_points = myAtr * trailMult,  trail_offset = myAtr * trailMult )
    if strategy.position_size < 0
        strategy.exit( "Short Exit TS", "Short", trail_points = myAtr * trailMult, trail_offset = myAtr * trailMult)

//====================================================================
//======================== GRAFİK ÇİZİMLER ===========================
//====================================================================
plot(realClose,      color=color.white,  linewidth=1, title="Fiyat")
plot(predictedPrice, color=color.yellow, linewidth=2, title="PredictedPrice")
plot(upperBand,      color=color.red,    linewidth=1, title="Üst Band")
plot(lowerBand,      color=color.lime,   linewidth=1, title="Alt Band")

plotshape( useOutlierFilter and isOutlier, style=shape.circle, color=color.red, size=size.tiny, location=location.abovebar, title="Outlier", text="Outlier")
```

> Detail

https://www.fmz.com/strategy/478722

> Last Modified

2025-01-17 15:57:53
