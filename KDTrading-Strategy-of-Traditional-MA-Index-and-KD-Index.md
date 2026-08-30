
> Name

Trading-Strategy-of-Traditional-MA-Index-and-KD-Index Trading-Strategy-of-Traditional-MA-Index-and-KD-Index
> Author

Archimedes' bathtub
> Strategy Description

[trans]
- Strategy name: Trading strategy of traditional moving average indicator and KD indicator
- Data cycle: 15M, 30M, etc.
-Support: commodity futures, digital currency
- The indicator uses EMA and KD line, and the KD line uses the default parameters (the indicator parameters are fixed at 3, 3, 9)
- Official website: www.quantinfo.com
![IMG](https://www.fmz.com/upload/asset/f842e44b0b8451cb562b8d5bd888e4c0.png) 

- Main picture
  EMA moving average, formula: MAC^^EMA(C,N);

- Sub-picture
K line in KD line, formula: K:SMA(RSV,M1,1);//moving average of RSV
  D line in KD line, formula: D:SMA(K,M2,1);//K’s moving average
||

- Data Cycle: 15M, 30M, etc.
- Support: Commodity Futures
- Indicators are EMA, KD lines, and KD line use default parameters (index parameters fixed 3, 3, 9)

  ![IMG](https://www.fmz.com/upload/asset/320fafa2ce5d6f68a4260a028783580d.png)  
  ![IMG](https://www.fmz.com/upload/asset/6753142c9c078ad25e9c913e82c0d999.png) 

- Main chart:
  EMA mean, formula: MAC ^^ EMA (C, N);

- Secondary chart:
  K line in KD, formula: K: SMA (RSV, M1, 1); //RSV moving average
  D line in KD, formula: D: SMA (K, M2, 1); //K moving average value

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|SLOSS|2|stop loss percentage|stop loss percentage|
|N|120|EMA parameter|EMA parameter|

> Source (MyLanguage)

``` pascal
(*backtest
start: 2018-04-01 00:00:00
end: 2018-05-15 00:00:00
period: 30m
exchanges: [{"eid":"Futures_BitMEX","currency":"XBT_USD"}]
args: [["TradeAmount",100,126961],["ContractType","XBTUSD",126961]]
*)

MAC^^EMA(C,N);

NKD:=9;
M1:=3;
M2:=3;
RSV:=(CLOSE-LLV(LOW,NKD))/(HHV(HIGH,NKD)-LLV(LOW,NKD))*100;  //收盘价与NKD周期最低值做差，NKD周期最高值与NKD周期最低值做差，两差之间做比值。
// (1)closing price minus the lowest value in NKD cycle, 
// (2)the highest value in NKD cycle minus the lowest value in NKD cycle, then (1) divided by (2).

K:SMA(RSV,M1,1);     // RSV的移动平均值
                     // MA of RSV
                     
D:SMA(K,M2,1);       // K的移动平均值
                     // MA of K

BARPOS>N AND C>MAC AND K<D,BK;
BARPOS>N AND C<MAC AND K>D,SK;
C<=BKPRICE*(1-SLOSS*0.01),SP(BKVOL);
C>=SKPRICE*(1+SLOSS*0.01),BP(SKVOL);
C>=BKPRICE*(1+SLOSS*0.01) AND C<MAC,SP(BKVOL);
C<=SKPRICE*(1-SLOSS*0.01) AND C>MAC,BP(SKVOL);
```

> Detail

https://www.fmz.com/strategy/128249

> Last Modified

2019-08-20 10:30:47
