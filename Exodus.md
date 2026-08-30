
> Name

Three moving average system Exodus
> Author

Exodus[strategy ghostwriting]
> Strategy Description

This system is a two-way contract strategy. When the conditions are met, it is long or short. The order amount is the number of contracts. When using Binance, the order amount is a few BTC. When using Huobi, the order amount unit is Zhang.
【Updated on 7-31】
The parameters of this strategy are suitable for operation at the 1-hour level, but the number of orders opened at the hour-level is too small, so the minute-level is updated. However, parameters need to be modified manually at the minute level.
The following backtest results are for hourly periods
****4-27 to 7-25****
The principal is 300, the order amount is 0.04btc
 ![IMG](https://www.fmz.com/upload/asset/1f4e9984f53d575c506c1.png)
****1-1 to 7-25****
The principal is 300, the order volume is 0.03btc, the order volume of 0.04 is insufficient principal.
If you want to use it yourself, please conduct a backtest to determine your order volume.
 ![IMG](https://www.fmz.com/upload/asset/1f47c59a9ac1f93694193.png) 
If you make money, you might as well support the author
  ![IMG](https://www.fmz.com/upload/asset/1f4c36c1fca8b23e727c7.jpg)  

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|afterEmaCrossTime|4|The operation is only allowed if macd meets the conditions within several k lines after the golden cross or dead cross of the k line|
|buyVolume|0.016|Transaction quantity (0.016BTC)|
|stopLossRate|true|Stop loss rate (leverage not calculated)|
|winLossRate|5|Profit-loss ratio|
|period|60|Period (minutes)|
|EMA1|8|Fastest moving average period|
|EMA2|34|Medium Speed Moving Average Period|
|EMA3|89|Slowest moving average period|
|MACD1|16|MACD parameter 1|
|MACD2|26|MACD parameter 2|
|MACD3|9|MACD parameter 3|

> Source (javascript)

``` javascript
/*backtest
start: 2021-04-27 00:00:00
end: 2021-07-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":300}]
args: [["afterEmaCrossTime",4],["buyVolume",0.04],["winLossRate",5]]
*/

function GetCrossStatus(a, lastA, b, lastB) {
    let lastStatus = lastA < lastB;
    let curStatus = a < b;
    let crosssStaus = 0; //0表示没有交叉，1表示金叉，2表示死叉
    //判断金叉还是死叉,同时判断此刻大于0轴或者小于0轴,因为在此系统中要求金叉时macd>0才有意义，死叉时macd<0才有意义
    if (curStatus != lastStatus) //状态不同时表示金叉或者死叉了
    {
        if (a > b) {
            crosssStaus = 1; //金叉
        }
        if (a < b)
            crosssStaus = 2; //死叉
    }
    return crosssStaus;
}
var lastOpenTime;

function GetCurRecord(records) {
    return records[records.length - 1];
}

function GetCurTime(records) {
    return GetCurRecord(records).Time;
}

function GetCurPrice(records) {
    return GetCurRecord(records).Close;
}

function Open(direction) {
    let pos = exchange.GetPosition()[0];

    if (pos != null) {
        return;
    }
    let amount = buyVolume;
    if (direction == 1) { //做多
        Log("做多", amount);
        exchange.SetDirection("buy");
        exchange.Buy(-1, amount);
    }
    if (direction == 2) { //做空
        Log("做空", amount);
        exchange.SetDirection("sell");
        exchange.Sell(-1, amount);
    }
    
}

function Close(ticker,fastLine,midLine) {
    let pos = exchange.GetPosition()[0];

    if (pos == null) {
        return;
    }
    
    if (pos.Type == PD_LONG) {
        if (ticker.Last < pos.Price*(1- stopLossRate/100) || ticker.Last > pos.Price*(1+(stopLossRate*winLossRate)/100)) {
            Log("平多,开仓价为:",pos.Price,"本次盈利:",pos.Profit);
            exchange.SetDirection("closebuy");
            exchange.Sell(-1, pos.Amount);
            
        }
    }
    if (pos.Type == PD_SHORT) {
        if (ticker.Last > pos.Price*(1+ stopLossRate/100) || ticker.Last < pos.Price*(1-(stopLossRate*winLossRate)/100) ) {
            Log("平空,开仓价为:",pos.Price,"本次盈利:",pos.Profit);
            exchange.SetDirection("closesell");
            exchange.Buy(-1, pos.Amount);
        }
    }
}




var lastEmaCrossTime = 0;
var lastMacdCrossTime = 0;

function NearMacdCross(time) {
    //Log("MACD",time,lastMacdCrossTime,time - lastMacdCrossTime);
    return time - lastMacdCrossTime <= afterEmaCrossTime * 1000 * 3600;
}

function NearEmaCross(time) {
    //Log("EMA",time,lastMacdCrossTime,time - lastMacdCrossTime);
    return time - lastEmaCrossTime <= afterEmaCrossTime * 1000 * 3600;
}


var emaMeet = 0; //0表示不满足，1满足做多条件，2满足做空条件
var macdMeet = 0; //判断macd是否满足条件,0表示不满足，1表示做多条件满足，2表示做空条件满足
function main() {
    exchange.SetContractType("swap");
    while (1) {
        let r = exchange.GetRecords(PERIOD_M1*period);

        //************均线EMA****************
        let emaChart8 = TA.EMA(r, EMA1);
        let emaChart34 = TA.EMA(r, EMA2);
        let emaChart89 = TA.EMA(r, EMA3);

        let ema8 = emaChart8;
        let curEma8 = ema8[emaChart8.length - 1];
        let lastEma8 = ema8[emaChart8.length - 2];

        let ema34 = emaChart34;
        let curEma34 = ema34[emaChart34.length - 1];
        let lastEma34 = ema34[emaChart34.length - 2];

        let ema89 = emaChart89;
        let curEma89 = ema89[emaChart89.length - 1];
        let lastEma89 = ema89[emaChart89.length - 2];

        //判断8均线和34均线的死叉和金叉，当金叉时如果当前实体在ema89均线以上做多，当死叉时如果实体在ema89以下时做空      
        let ticker = exchange.GetTicker();
        let low = ticker.Low;
        let high = ticker.High;
        let close = ticker.Close;

        Close(ticker,curEma8,curEma34);

        let crossStatus1 = GetCrossStatus(curEma8, lastEma8, curEma34, lastEma34);

        if (crossStatus1 != emaMeet) { //状态变化时更新状态
            if (crossStatus1 == 1) {
                emaMeet = 1;
                Log("ema金叉，时间:", GetCurTime(r),talib.LINEARREG_SLOPE(ema8));
                lastEmaCrossTime = r[r.length - 1].Time;
            }
            if (crossStatus1 == 2) {
                emaMeet = 2;
                //Log("ema死叉，时间:", GetCurTime(r));
                lastEmaCrossTime = r[r.length - 1].Time;
                //Log("Ema 2");
            }
        }

        //***************Macd*************
        let macdChart = TA.MACD(r, MACD1, MACD2, MACD3);

        let macd = macdChart[2]; //动能柱
        let curMacd = macd[r.length - 1]; //当前动能柱
        let lastMacd = macd[r.length - 2]; //上一根动能柱，直接根据动能柱的正反来判断macd的金叉和死叉
        //auto lastMacd = macd[r.size() - 2]; //上一根动能柱

        //判断金叉还是死叉
        let dif = macdChart[0];
        let curDif = dif[r.length - 1];
        let lastDif = dif[r.length - 2];


        //判断金叉还是死叉,同时判断此刻大于0轴或者小于0轴,因为在此系统中要求金叉时macd>0才有意义，死叉时macd<0才有意义

        //Macd形成金叉或者死叉的瞬间
        if (curMacd < 0 != lastMacd < 0) {

            if (curMacd > 0) {
                macdMeet = 1;
                //Log("macd金叉", lastMacd, curMacd);
                lastMacdCrossTime = GetCurTime(r);
            }
            if (curMacd < 0) {
                macdMeet = 2;
                //Log("macd死叉", lastMacd, curMacd);
                lastMacdCrossTime = GetCurTime(r);

            }
        }


        let Account = exchange.GetAccount();
        let curBalance = exchange.GetAccount().Balance; //余额
        let curStock = exchange.GetAccount().Stocks; //币量

        //均线系统
        var curTime = GetCurTime(r);
       
        if (NearEmaCross(curTime) && NearMacdCross(curTime)) {
            
            if (emaMeet == 1 && macdMeet == 1 && curDif >= 0) {
                Open(1);
            }
           
            if (emaMeet == 2 && macdMeet == 2 && curDif < 0) {
                Open(2);
            }
        }
        



        var myDate = new Date();
        var myDataM = myDate.getMinutes();
        var myDateS = myDate.getSeconds() * 1000;
        var myDateMs = myDate.getMilliseconds(); //获取到毫秒以减少误差
        Sleep(Math.abs(period - myDataM % period) * 60000 - myDateS - myDateMs);


    }


}
```

> Detail

https://www.fmz.com/strategy/301620

> Last Modified

2021-11-28 07:20:15
