
> Name

Trend-Breakout-Strategy by calculating price volatility Trend-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/67876b80a4a9182768e6e45adfdae1b3e5d6b2b0d1116113457dbd0d95f0e77b.png)
[trans]

### Overview
The trend breakout strategy is a quantitative strategy that determines market trends and trades by calculating price volatility. This strategy uses the formula of (highest price-lowest price)/closing price to calculate the price volatility of the K-line, and then smoothes it through the moving average to determine whether there is a trend reversal. When volatility is higher than the average level of a recent period, it indicates that a new trend may be emerging, and the strategy will issue a trading signal.
### Strategy Principles
The core indicator of this strategy is (highest price - lowest price)/closing price, which reflects the fluctuation range of the K line. The strategy first calculates this indicator, then takes its absolute value and calculates the simple moving average. If the absolute value of the current K-line fluctuation index is higher than the moving average of a certain period in the past, it indicates that a new trend may be forming.
Specifically, the strategy includes the following steps:
1. Calculate (highest price - lowest price)/closing price as a volatility indicator
2. Take the absolute value of the volatility indicator and calculate the simple moving average
3. Compare the relationship between the current K-line volatility and the moving average of a certain period in the past (user input)
4. If the current volatility is greater than the moving average, a long signal is formed; if the current volatility is less than the moving average, a short signal is formed.
5. Go long or short based on the signal direction
This strategy also includes visual operations such as indicator drawing and K-line color changes, which facilitates intuitive judgment of market trends. In general, the strategy's idea of ​​using price volatility to judge potential trend changes is simple, direct and effective.
### Strategic Advantages
This strategy has the following main advantages:
1. The principle is simple and direct, easy to understand and implement
2. Use price volatility to judge market trend changes, there is no fixed indicator framework
3. Customizable parameters to adjust judgment sensitivity
4. Combined with indicator drawing and K-line color change, the intuitive judgment effect is good
5. It can smooth and remove noise, which is helpful to grasp the medium and long-term trend.
In general, this strategy breaks through the traditional thinking pattern of indicator judgment, only focuses on the volatility of the price itself, and flexibly captures potential trend changes. The parameters are highly adjustable and easy to use, making it a recommended trend strategy.
### Strategy Risk
This strategy also has the following main risks:
1. Too sensitive to market volatility and may generate multiple invalid signals
2. Only consider price volatility and ignore other influencing factors
3. Improper parameter settings may miss trends or make wrong judgments
4. Unable to distinguish between medium and long-term trends and short-term adjustments
These risks are mainly related to the strategy's over-reliance on price volatility to judge market trends. In order to reduce risks, you can consider combining other judgment indicators to judge the effectiveness of trend signals; you can also adjust parameters appropriately to smooth volatility indicators and filter out short-term noise.
### Optimization direction
This strategy can be optimized mainly from the following directions:
1. Determine the validity of the trend based on indicators such as trading volume
2. Add machine learning model to judge signal quality
3. Optimize parameter settings to make the smoothing effect better
4. Distinguish between medium and long-term trends and short-term adjustments
5. Combine with stop loss strategy to control single loss
These optimization measures can reduce the probability of wrong transactions and improve strategy profitability. In particular, increasing indicators and models for judging the validity of signals can significantly reduce invalid signals. In addition, stop-loss strategies are also necessary to control single losses and ensure overall returns.
### Summarize
This trend breakthrough strategy determines market trend changes by calculating price volatility. The principle is simple and direct, and it is flexible to use. The parameters can be customized to adjust the judgment sensitivity. The strategy has the advantage of catching trend changes, but it also has certain risks. We can make improvements by optimizing judgment indicators, establishing filtering models, adjusting parameter settings, etc. to make the strategy more stable and reliable. Overall, this strategy provides new ideas for judging market trend changes and is worthy of further research and optimization.
||
## 

### Overview

The trend breakout strategy is a quantitative strategy that judges market trends and trades by calculating price volatility. The strategy uses the formula (high-low)/close to calculate price volatility of candlestick, and further processes it through moving average to judge whether a trend reversal occurs. When volatility is higher than the average level over a recent period, a new trend may be emerging. Then the strategy will issue trading signals.  

### Strategy Logic

The core indicator of this strategy is (high-low)/close, which reflects the amplitude of candlestick. The strategy first calculates this indicator, then takes its absolute value and calculates simple moving average. If the current candlestick's volatility indicator absolute value is higher than moving average value over a period, it means a new trend may be forming.

Specifically, the strategy includes following steps:

1. Calculate (high-low)/close as volatility indicator  
2. Take absolute value of volatility indicator and calculate simple moving average
3. Compare current candlestick volatility with moving average over a period (user input) 
4. If current volatility is greater than moving average, form long signal; if lower, form short signal
5. Make long or short positions based on signal directions

The strategy also contains indictor plotting, candlestick color change and other visualizations for intuitive trend judgment. In summary, the idea of using price volatility to judge potential trend change is simple and effective.  

### Advantages

The main advantages of this strategy are:

1. Simple and direct principle, easy to understand and implement
2. Use price volatility to judge market trend change, no fixed indicator framework
3. Customizable parameters to adjust judgment sensitivity  
4. Good intuitive effect combined with indicator plotting and color change
5. Can smooth out noise and catch mid-long term trends

In general, this strategy breaks through the thinking pattern of traditional indicator judgment, and only focuses on price volatility itself to flexibly capture potential trend changes. The strategy is adjustable, easy to use, and worth recommending.

### Risks

The main risks of this strategy include:  

1. Too sensitive to market volatility, may generate multiple invalid signals
2. Only consider price volatility, ignore other factors  
3. Improper parameter settings may miss trends or cause wrong judgements 
4. Unable to distinguish mid-long term trends and short-term adjustments

These risks are mainly related to over reliance of the strategy on price volatility to determine market trends. To reduce risks, we can consider combining other judgment indicators to verify the validity of trend signals, and properly adjust parameters to smooth volatility indicators, filtering out short-term noises.  

### Optimization Directions

The main directions for optimizing this strategy include:

1. Combine trading volume and other indicators to determine trend validity
2. Add machine learning models to judge signal quality
3. Optimize parameter settings for better smoothing effects 
4. Distinguish mid-long term trends and short-term adjustments
5. Combine with stop loss strategies to control per trade loss

These optimization measures can reduce the probability of wrong trades and improve the profitability of the strategy. In particular, adding indicators and models to determine signal validity can greatly reduce invalid signals. In addition, stop loss strategies are also necessary to control single trade loss and ensure overall returns.

### Summary  

This trend breakout strategy judges market trend changes by calculating price volatility. The principle is simple and direct, and the usage is flexible with customizable parameters for sensitivity adjustment. The strategy has the advantage of capturing trend changes, but also has some risks. We can improve it by optimizing judgment indicators, establishing filtering models, adjusting parameter settings and so on, to make the strategy more stable and reliable. In general, this strategy provides a new idea for determining market trend changes and is worth further research and optimization.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|Bar Width|
|v_input_2|true|Look Back|
|v_input_3|false|% change|
|v_input_4|16|SMA Length|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-26 00:00:00
end: 2023-12-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
////////////////////////////////////////////////////////////
//  Copyright by HPotter v2.0 25/10/2017
//
//  This histogram displays (high-low)/close
//  Can be applied to any time frame.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="(H-L)/C Histogram Backtest", precision = 2)
input_barwidth = input(4, title="Bar Width")
input_barsback = input(1, title="Look Back")
input_percentorprice = input(false, title="% change")
input_smalength = input(16, title="SMA Length")
reverse = input(false, title="Trade reverse")
hline(0, color=blue, linestyle=line)
xPrice = (high-low)/close
xPriceHL = (high-low)
xPrice1 = iff(input_percentorprice, xPrice * 100, xPriceHL)
xPrice1SMA = sma(abs(xPrice1), input_smalength)
pos = 0.0
pos := iff(xPrice1SMA[input_barsback] > abs(xPrice1), 1,
	   iff(xPrice1SMA[input_barsback] < abs(xPrice1), -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(abs(xPrice1), color=green, style = histogram, linewidth = input_barwidth, title="Change")
plot(xPrice1SMA[input_barsback], color=red, title="SMA")
```

> Detail

https://www.fmz.com/strategy/436793

> Last Modified

2023-12-27 17:34:31
