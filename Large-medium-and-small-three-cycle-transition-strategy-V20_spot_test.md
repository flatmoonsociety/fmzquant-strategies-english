
> Name

Large, medium and small three-cycle transition strategy V20_spot_test
> Author

District class quantification
> Strategy Description

Large, medium and small three-cycle transition strategy. In general, the large cycle indicates the market direction, the medium cycle is the current operating cycle, and the small cycle indicates the trend stopping signal. When you enter the market, as long as you refer to the status of the three cycles of large, medium and small, you can, like Zhuge Liang, adopt ever-changing strategies to deal with the complex market. If your operating cycle frequency is several times a day, you can choose the daily line for the large cycle, 4 hours for the medium cycle, and 30 minutes for the small cycle; if your operating cycle frequency is dozens of times a day, you can choose 4 hours for the large cycle, 30 minutes for the medium cycle, and 5 minutes for the small cycle; the previous cycle is always 6 to 8 times different from the next cycle.
Then we list the relationship between the K-line and the Bollinger Band in each cycle. There are 8 states in total. In three cycles, there are 8*8*8=512 states. These 512 states are enough to cope with all possible market conditions. Programmers with strong technical ability can pre-design the best order points and stop-loss points for each state. In order for everyone to have a basis for discussion, the district class leader has also made the strategy public on the inventor platform. Everyone is welcome to improve on this basis.
Then we back-test it, and we can see that the annualized rate is 29, and the retracement is a bit high, reaching 36%. We download the logs and analyze the retracements. This is the advantage of the Inventor Platform.
 ![IMG](https://www.fmz.com/upload/asset/13120536c7fe04832dbcb.png)
  ![IMG](https://www.fmz.com/upload/asset/131192810d7ecb2b1d1ef.png)
  ![IMG](https://www.fmz.com/upload/asset/130ed64aa7da2ceabc187.png)
After analysis, there are mainly the following reasons:
1. Although the structure of large, medium and small cycles is better, the strategy of how small cycles affect medium cycles is difficult to conceive. It can be simplified first and added later;
2. When the market goes short, you should resolutely abandon your position.
3. The directional role of the 5-day moving average is very important and is not reflected in the strategy.
4. If there is a rapid decline outside the Bollinger Bands, you should sell.
5. When the reason for rising falls below, profit and loss should be taken in time
 ![IMG](https://www.fmz.com/upload/asset/1310b2148822a81917ce8.png) ![IMG](https://www.fmz.com/upload/asset/13173d3b37858cf619f9e.png)
After targeted improvements and dozens of iterations, we finally achieved an annualized rate of 210, a retracement of 16.4, and a reduction in the number of transactions.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Interval|10|Polling period (seconds)|

> Source (javascript)

``` javascript
/*backtest
start: 2019-01-01 00:00:00
end: 2019-10-10 00:00:00
period: 1d
exchanges: [{"eid":"OKEX","currency":"ETH_USDT","stocks":0}]
args: [["OpMode",1,10989],["MaxAmount",1,10989],["TradeFee",0.001,10989]]
*/
//注册币乎后https://m.bihu.com/signup?i=1ewtKO&s=4&c=4
//搜索 物联网区块链 可以联系到作者区班主 你也可以给我写邮件tomjava@163.com
var midStatus = 0; //中周期状态
var bigStatus = 0; //大周期状态
var beforeBigStatus = 0; //之前大周期状态
var operPrice;
var markTime=0;

function mySell(rate){
   var account = _C(exchange.GetAccount);
   var ticker = _C(exchange.GetTicker);
   var nowPrice=ticker.Sell;
     
   //以下开始卖出
   var allAmount=account.Balance+account.Stocks*ticker.Sell; //计算出总金额
   var cashRatio=account.Balance*100/allAmount;
   
   if(cashRatio<90){  //现金比率小于10，才可以卖出
      if(rate==1){ //卖出1份
          if(cashRatio<80){
              $.Sell(allAmount*0.1/nowPrice);
              Log("现金比率",cashRatio+10);
          }else{
              $.Sell(allAmount*0.05/nowPrice);
              Log("现金比率",cashRatio+5);
          }
      }else{
          if(cashRatio<75){
              $.Sell(allAmount*0.2/nowPrice);
              Log("现金比率",cashRatio+20);
          }else{
              $.Sell(allAmount*0.1/nowPrice);
              Log("现金比率",cashRatio+10);
          }
      }
   }
}

function myBuy(rate){
   var account = _C(exchange.GetAccount);
   var ticker = _C(exchange.GetTicker);
   var nowPrice=ticker.Sell;
     
   //以下开始买入
   var allAmount=account.Balance+account.Stocks*ticker.Sell; //计算出总金额
   var cashRatio=account.Balance*100/allAmount;
   //Log("需要买入比率",rate);
   if(cashRatio>10){  //现金比率大于10，才可以买入
      if(rate==1){ //买入1份
          if(cashRatio>20){
              $.Buy(allAmount*0.1/nowPrice);
              Log("现金比率",cashRatio-10);
          }else{
              $.Buy(allAmount*0.05/nowPrice);
              Log("现金比率",cashRatio-5);
          }
      }else{
          if(cashRatio>25){
              $.Buy(allAmount*0.2/nowPrice);
              Log("现金比率",cashRatio-20);
          }else{
              $.Buy(allAmount*0.1/nowPrice);
              Log("现金比率",cashRatio-10);
          }
      }
   }
}

function oper(){
    var ticker = _C(exchange.GetTicker);
    var nowPrice=ticker.Sell;
   
    var h1records = exchange.GetRecords(PERIOD_H1);
    var h1boll;var h1upLine;var h1midLine;var h1downLine;
    var h1bw;
    if(h1records && h1records.length > 20) {
        h1boll = TA.BOLL(h1records, 20, 2);
        h1upLine = h1boll[0][h1records.length-1];
        h1midLine = h1boll[1][h1records.length-1];
        h1downLine = h1boll[2][h1records.length-1];
    }
    
    var drecords = exchange.GetRecords(PERIOD_D1);
    var dboll;var dupLine;var dmidLine;var ddownLine;
    var dbw;var beforePrice;
    if(drecords && drecords.length > 20) {
        dboll = TA.BOLL(drecords, 20, 2);
        dupLine = dboll[0][drecords.length-1];
        dmidLine = dboll[1][drecords.length-1];
        ddownLine = dboll[2][drecords.length-1];
        dbw=dupLine-dmidLine;
        beforePrice=(drecords[drecords.length-2].Open+drecords[drecords.length-2].Close)/2;
    }
    
    if(ticker.Time-markTime<15*60*1000){ //只有满足15分钟间隔，才允许判断状态
        return;
    }else{
        markTime=ticker.Time;
    }
    
    if(h1records && h1records.length > 20 && drecords && drecords.length > 20) {
        if(nowPrice>dupLine+dbw*0.1){
            bigStatus=0;
        }else if(nowPrice>dupLine-dbw*0.1){
            bigStatus=1;
        }else if(nowPrice>dmidLine+dbw*0.1){
            bigStatus=2;
        }else if(nowPrice>dmidLine){
            bigStatus=3;
        }else if(nowPrice>dmidLine-dbw*0.1){
            bigStatus=4;
        }else if(nowPrice>ddownLine+dbw*0.1){
            bigStatus=5;
        }else if(nowPrice>ddownLine-dbw*0.1){
            bigStatus=6;
        }else{
            bigStatus=7;
        }
        
        if(beforePrice>dupLine+dbw*0.1){
            beforeBigStatus=0;
        }else if(beforePrice>dupLine-dbw*0.1){
            beforeBigStatus=1;
        }else if(beforePrice>dmidLine+dbw*0.1){
            beforeBigStatus=2;
        }else if(beforePrice>dmidLine){
            beforeBigStatus=3;
        }else if(beforePrice>dmidLine-dbw*0.1){
            beforeBigStatus=4;
        }else if(beforePrice>ddownLine+dbw*0.1){
            beforeBigStatus=5;
        }else if(beforePrice>ddownLine-dbw*0.1){
            beforeBigStatus=6;
        }else{
            beforeBigStatus=7;
        }
        
        if(nowPrice>h1upLine+h1bw*0.1){
            midStatus=0;
        }else if(nowPrice>h1upLine-h1bw*0.1){
            midStatus=1;
        }else if(nowPrice>h1midLine+h1bw*0.1){
            midStatus=2;
        }else if(nowPrice>h1midLine){
            midStatus=3;
        }else if(nowPrice>h1midLine-h1bw*0.1){
            midStatus=4;
        }else if(nowPrice>h1downLine+h1bw*0.1){
            midStatus=5;
        }else if(nowPrice>h1downLine-h1bw*0.1){
            midStatus=6;
        }else{
            midStatus=7;
        }
        
        if(bigStatus-beforeBigStatus>0){ //当前有一个大周期下跌跃迁
            if(midStatus==6||midStatus==7){
                //Log("卖2份 当大",bigStatus,"前大",beforeBigStatus,"中",midStatus);
                //买2份
                mySell(2);
            }else if(midStatus==3||midStatus==4){
                //Log("卖1份 当大",bigStatus,"前大",beforeBigStatus,"中",midStatus);
                //买1份
                mySell(1);
            }else{
                //Log("当大",bigStatus,"前大",beforeBigStatus,"中",midStatus);
            }
        }else if(bigStatus-beforeBigStatus<0){  //当前有一个大周期上涨跃迁
            if(midStatus==6||midStatus==7){
                //Log("买2份 当大",bigStatus,"前大",beforeBigStatus,"中",midStatus);
                //买2份
                myBuy(2);
            }else if(midStatus==3||midStatus==4){
                //Log("买1份 当大",bigStatus,"前大",beforeBigStatus,"中",midStatus);
                //买1份
                myBuy(1);
            }else{
                //Log("当大",bigStatus,"前大",beforeBigStatus,"中",midStatus);
            }
        }else{
            //Log("当大",bigStatus,"前大",beforeBigStatus,"中",midStatus," dup",dupLine," 长度",dboll[0].length);
        }
    }
}

function main() {
    var initAccount = _C(exchange.GetAccount);
    Log(initAccount);
    exchange.SetCurrency("LTC_USDT")
    Log("BTC_USDT的计价币名称：", exchange.GetQuoteCurrency())
  
    while (true) {
        oper();
        Sleep(Interval*1000);
    }
}
```

> Detail

https://www.fmz.com/strategy/177631

> Last Modified

2024-01-28 18:15:48
