
> Name

Three lines of code implement Argos machine learning’s counter-referential strategy for quickly interpreting industry news
> Author

Zero

> Strategy Description

> Argos
https://www.quantinfo.com/Argus/

> Bragging
Argus (Argus Ἄργος) a hundred-eyed giant in Greek mythology
This system is a project of Quanke Online, a subsidiary of the inventor. After five years of research and development, the entire network monitors price fluctuations and related information in futures, stocks, options, commodities, foreign exchange, etc.
Using the most cutting-edge artificial intelligence neural network, trained hundreds of millions of times
It can predict effective stock order quotations, predict financial asset price changes, predict S&P 500 index volatility, optimize investment portfolios, and predict price fluctuations based on news headlines.
 ![IMG](https://www.fmz.com/upload/asset/18bc0cc19ceb00d6bc9.png) 

> Landing
Although the bullshit is fine, embarrassing facts prove that it is better to counter-invert with Argos, which uses AI technology. If it predicts a rise, we will sell, and if it predicts a fall, we will buy.
If others are crazy, I will be afraid. If others are afraid, I will be crazy, because it predicts the public sentiment. If you want to make money, you have to do the opposite.
> Strategy
With the help of the powerful syntax support of the inventor platform, in order to display the most intuitive effect, the enhanced version of My language is selected. The data source returns a decimal from 0 to 1 to describe the probability of increase. If the user needs to obtain data on other varieties, just modify the variety name in the strategy code URL.
> Effect
 ![IMG](https://www.fmz.com/upload/asset/2440e3472cba14cd778.png) 
 
>Finally
If you want to define your own third-party data source, refer to API https://www.fmz.com/api#exchange.getdata
  This strategy is only used to demonstrate how to call third-party data sources for backtest verification, please do not place a real offer!!!



> Source (MyLanguage)

``` pascal
(*backtest
start: 2019-10-01 00:00:00
end: 2020-04-21 23:59:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Bitfinex","currency":"BTC_USD"}]
*)

预测值:DATA('https://www.quantinfo.com/API/Argus/history?symbol=比特币');
预测值>HV(预测值, 5)&&预测值>0.6,SPK;
预测值<LV(预测值, 10)&&预测值<0.4,BPK;
```

> Detail

https://www.fmz.com/strategy/201665

> Last Modified

2020-04-23 19:50:41
