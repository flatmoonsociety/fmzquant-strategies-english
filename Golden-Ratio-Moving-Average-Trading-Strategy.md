
> Name

Golden-Ratio-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/90098c6dc90f01d4ef1fd51723fa6a68b509b927f0ae41d54f3dd109024a8da7.png)

[trans]

## Overview
The golden section moving average trading strategy is a quantitative trading strategy that attempts to use the golden cross of long and short-term moving averages as a trading signal. This strategy also combines the RSI indicator to avoid opening positions at local highs to control risks.
## Strategy Principle
This strategy is mainly based on two moving averages: the 200-day moving average as the long-term moving average, and the 10-day moving average as the short-term moving average. When the short-term moving average crosses the long-term moving average, a buy signal is generated; when the short-term moving average crosses below the long-term moving average, a sell signal is generated. This is the famous "golden cross". This strategy also combines the RSI indicator. If the RSI is less than 30, it will trigger the strategy to only open positions in the oversold zone.
Specifically, a long position will be opened if the following conditions are met:
1. The 10-day moving average crosses the 200-day moving average
2. There are currently no positions
3. RSI less than 30
The closing conditions are as follows:
1. Stop loss: stop loss when the price falls below a certain percentage of the opening price (can be set)
2. Take profit: Take profit when the price exceeds a certain ratio (can be set)
## Advantage Analysis
This strategy has the following advantages:
1. The golden cross signal of the moving average is used, which is a classic and effective technical indicator trading signal.
2. Combining RSI to avoid buying at high points can control risks to a certain extent.
3. There are stop loss and take profit settings to lock in profits and avoid risks.
## Risk Analysis
There are also some risks with this strategy:
1. Moving average strategies are prone to false signals and U-turns
2. RSI will fail in some strong market conditions
3. Stop loss settings that are too small may lead to frequent stop losses in ultra-short-term trading.
To reduce these risks, the following optimization measures can be considered:
1. Adjust the moving average parameters, or add more moving averages
2. Combine with other indicators to confirm RSI signal
3. Adjust stop loss and take profit parameter settings
## Optimization direction
There is room for further optimization of this strategy:
1. Add more indicators to filter signals and avoid false signals
2. Optimize moving average parameters
3. Set dynamic stop loss combined with volatility indicators
4. Add machine learning models to determine market status
5. Use algorithms to automatically optimize parameters
## Summarize
The Golden Section Moving Average trading strategy is overall a simple and effective trend following strategy. It uses classic moving average crossover signals to generate trading opportunities, and has stop loss and take profit to control risks. This strategy can be further improved through multi-index combination, parameter optimization, machine learning and other means to obtain better strategy effects.
||

## Overview

The golden ratio moving average trading strategy is a quantitative trading strategy that attempts to use the golden cross of short-term and long-term moving averages as trading signals. The strategy also incorporates the RSI indicator to avoid opening positions at local highs in order to control risks.  

## Strategy Logic  

The strategy is mainly based on two moving averages: the 200-day MA as the long-term MA and the 10-day MA as the short-term MA. A buy signal is generated when the short-term MA crosses over the long-term MA; A sell signal is generated when the short-term MA crosses below the long-term MA. This is the famous "golden cross". The strategy also incorporates the RSI indicator so that the strategy only opens long positions in the oversold area when RSI is less than 30.   

Specifically, a long position will be opened if the following conditions are met:  

1. 10-day MA crosses above 200-day MA
2. Currently no position  
3. RSI less than 30

The closing position conditions are as follows:

1. Stop loss: stop loss when the price falls below a certain percentage (adjustable) of the opening price  
2. Take profit: take profit when the price exceeds a certain percentage (adjustable)

## Advantage Analysis   

The strategy has the following advantages:  

1. It utilizes the golden cross signal of moving averages, which is a classic and effective technical indicator trading signal  
2. Incorporating RSI avoids buying at the highs, which can control risks to some extent
3. With stop loss and take profit settings, it can lock in profits and avoid risks   

## Risk Analysis   

The strategy also has some risks:   

1. Moving average strategies are prone to generating wrong signals and whipsaws  
2. RSI can fail in some strong trending markets  
3. If the stop loss is set too small, it may lead to ultra short-term trading and frequent stop loss activation   

To reduce these risks, the following optimization measures can be considered:  

1. Adjust the MA parameters, or add more MAs  
2. Incorporate other indicators to confirm RSI signals  
3. Adjust stop loss and take profit parameter settings  

## Optimization Directions   

There is room for further optimization of the strategy:  

1. Increase more indicator filters to avoid wrong signals  
2. Optimize moving average parameters   
3. Incorporate volatility indicators to set dynamic stops   
4. Add machine learning models to judge market conditions
5. Use algorithms to automatically optimize parameters  

## Conclusion  

In summary, the golden ratio moving average trading strategy is a simple and effective trend following strategy. It generates trading opportunities using classic MA crossover signals and has stops to control risks. The strategy can be further improved through multi-indicator combinations, parameter optimization, machine learning, etc. to obtain better strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|(?パラメータ) long-term moving average BASE200|
|v_input_int_2|10|Long-term moving average BASE10|
|v_input_int_3|20|Damage cut and cut%|
|v_input_int_4|5|利食いの合合%|
|v_input_1|timestamp(01 Jan 2018 13:30 +0000)|(?Period)バックテストを开める日|
|v_input_2|timestamp(1 Jan 2099 19:30 +0000)|バックテスを久わる日|

> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-29 00:00:00
end: 2024-01-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tsujimoto0403

//@version=5
strategy("聖杯", overlay=true,default_qty_type=strategy.percent_of_equity,
     default_qty_value=100)

//ユーザーインプットの準備
malongperiod=input.int(200,"長期移動平均BASE200",group = "パラメータ")
mashortperiod=input.int(10,"長期移動平均BASE10",group = "パラメータ")
stop=input.int(20,title = "損切の割合％",group = "パラメータ")
profit=input.int(5,title = "利食いの割合％",group = "パラメータ")
startday=input(title="バックテストを始める日", defval=timestamp("01 Jan 2018 13:30 +0000"), group="期間")
endday=input(title="バックテスを終わる日", defval=timestamp("1 Jan 2099 19:30 +0000"), group="期間")

//使う変数
var float stopprice=0
var float takeprofit=0

//とりあえず使うインジケーターをプロット
malong=ta.sma(close,malongperiod)
mashort=ta.sma(close,mashortperiod)


plot(malong,color=color.aqua,linewidth = 2)
plot(mashort,color=color.yellow,linewidth = 2)
bgcolor(ta.rsi(close,3)<30?color.rgb(229, 86, 86, 48):na)

//期間条件
datefilter = true

//エントリー条件
if close>malong and close<mashort and strategy.position_size == 0 and datefilter and ta.rsi(close,3)<30
    strategy.entry(id="long", direction=strategy.long)

if strategy.position_size>0 
    strategy.exit(id="long",stop=(1-0.01*stop)*strategy.position_avg_price)

//売り
if  strategy.position_size > 0 and close>mashort and close<low[1] 
    strategy.close(id ="long")



```

> Detail

https://www.fmz.com/strategy/437774

> Last Modified

2024-01-05 14:21:52
