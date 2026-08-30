
> Name

Single product commissary strategy V20_annualized 130
> Author

District class quantification
> Strategy Description

According to some statistics, in terms of market trends, 80% of the time it is in a volatile trend. The grid strategy is a strategy to deal with shocks. There are many ways to implement the grid strategy, but the essence is to set a relatively stable position-adding strategy, and execute the position-adding as long as the price fluctuation meets the conditions of the strategy. Let's take an example. For example, every time the price drops by 5%, we will increase the position by 20% of the total funds. In this way, we will fully use the funds after executing up to five positions. Here we can also reduce the position by 20% of the initial capital for every 5% increase, and then we will clear the position after five times. This is the basic idea of ​​the grid strategy.
Today, the district leader introduced a quantitative strategy, which is similar to grid trading, but based on this, some improvements have been made. In some cases, it can achieve an annualized return of 130%. The district leader named it the canteen strategy, imagining that the operator is a canteen operator. He aims at a fair price in the market. Once it is higher than the fair price, he will sell the goods. If it is lower than the fair price, he will buy the goods. In addition, he has a small book that records the last transaction price. Once the price of the product is lower than the last transaction price, he can also buy suddenly, and vice versa. In order to avoid unlimited operations, stop operations when the funds are less than 10% or more than 10%.
Describe the steps in detail:
Step 1: Observe the volatility of the commodity and find a fair price indicator, which can be a moving average (20 periods of the 30-minute line) or the Bollinger Middle Line; buy 50% of the position by default and record the transaction price;
Step 2: If it is 3% lower than the fair price indicator, give a buy instruction; if it is 3% higher than the fair price, give a sell instruction; and record the transaction price;
		    If it is 5% lower than the last transaction price, then give a buy instruction; if it is 5% higher than the last transaction price, then give a sell instruction; and record the transaction price;
Step 3: Based on the current position, decide how to operate when receiving a buy order; the position fluctuates between 10% and 90%. If it exceeds this range, no operation will be performed, but the transaction price can be recorded; each operation only buys 20% or 10% of the position to avoid unlimited operations.
This strategy is called a single-commodity store strategy because the store has only one product. As a future direction for improvement, we hope to increase the rotation of multiple commodities and even back-to-back short hedging.
Let's run a backtest. First, we choose ETH, which has high volatility, as this commodity. The period is from January 1 to October 10, 2019. This range has both sharp rises and sharp falls.
It can be seen that the backtest effect is still good, reaching an annualized rate of 130%, and creating a transaction fee of 1,651 yuan. This result should be a strategy that both exchanges and traders are happy with.
The disadvantage is that the maximum drawdown is still a bit high, reaching about 30%. Major retracements occur during the phase of a sharp decline in the commodity. It’s easy to understand when you think about it, because this strategy is anchored in trading commodities. If the price of commodities falls, then some goods may have been stored at a high level and have not had time to be released to the market. As time goes by, they should be able to make up for it.
After registering on Coinhu https://m.bihu.com/signup?i=1ewtKO&s=4&c=4, search for "Internet of Things Blockchain" to contact the author area leader.
In addition, readers need to be reminded that this strategy is also related to product selection. Try to choose commodities that are highly volatile and will appreciate in value over the long term. From another perspective, if you can adjust parameters based on products, then no matter how small the fluctuation is, as long as it can cover the handling fee, it shouldn't be a problem.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Interval|10|Polling period (seconds)|
|mnum|20|30 minute line period|
|initRatio|0.5|Initial position ratio|

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
//搜索 物联网区块链 可以联系到作者区班主
function main() {
    var isInit = 1; //表示初始态
    var allAmount;
    var cashRatio;
    var initAccount = _C(exchange.GetAccount);
    var lastPrice;
    var wantRatio;
    var wantOper=0;//期待的操作，0不操作，1买入，-1卖出
    Log(initAccount);
    var mhigh;
    var mlow;
    while (true) {
        var mrecords = exchange.GetRecords(PERIOD_M30);
        //一定周期内的高低点
        mhigh=TA.Highest(mrecords, mnum, 'High');
        mlow=TA.Lowest(mrecords, mnum, 'Low');
        
        var midLine = (mhigh+mlow)/2;
        var ticker = _C(exchange.GetTicker);
        var account = _C(exchange.GetAccount);
        var nowPrice=ticker.Sell;
        var obj;
        
        if (isInit == 1) {  //初始化状态为默认仓；     
            //账户现金乘以比例，除以当前价格，保留小数前3位
            obj = $.Buy(_N(account.Balance * initRatio / ticker.Sell, 3));
            if (obj) { //如果购买成功，就标志开仓
                      opAmount = obj.amount;
                      lastPrice = obj.price;
                      isInit=0; //初始化成功
                      account = _C(exchange.GetAccount);
                      Log("初始开仓:购买量", opAmount);
                      Log("目前持币数", account.Stocks);
            }
        }else{ //日常操作检测
            if(nowPrice>midLine*1.03||nowPrice>lastPrice*1.07){
                wantOper=-1;
            }else if(nowPrice<midLine*0.97||nowPrice<lastPrice*0.93){
                wantOper=1;
            }else{
                wantOper=0;
            }
            
            if (wantOper==-1) { //离市平仓
                lastPrice=nowPrice; //不管买没买成功都修改了一下价格
                allAmount=account.Balance+account.Stocks*ticker.Sell; //计算出总金额
                cashRatio=parseFloat((account.Balance/allAmount).toFixed(3));
                
                if(cashRatio>0.9){ //现金比例大于0.9，不做任何操作 
                    wantRatio=0;
                }else if(cashRatio>0.8){ //现金比例超过0.8，可以抛一成仓 
                    wantRatio=0.1;
                }else{ //其他情况都可以抛掉2成仓
                    wantRatio=0.2;
                }
                
                obj = $.Sell(_N(allAmount*wantRatio/ticker.Sell, 3)); 
                if(obj){
                    opAmount = obj.amount;
                    Log("平仓：卖出量",opAmount);
                    nowAccount = _C(exchange.GetAccount);
                    Log("目前现金",nowAccount.Balance,"盈利",allAmount - initAccount.Balance);
                }
            }else if (wantOper==1) { //开仓买入
                lastPrice=nowPrice; //不管买没买成功都修改了一下价格
                allAmount=account.Balance+account.Stocks*ticker.Sell; //计算出总金额
                cashRatio=parseFloat((account.Balance/allAmount).toFixed(3));
                //Log("准备买入",cashRatio);
                if(cashRatio<0.1){ //现金比例小于0.1，已没钱买了
                    wantRatio=0;
                }else if(cashRatio<0.2){ //现金比例超过0.2，可以买一成仓 
                    wantRatio=0.1;
                }else{ //其他情况都可以买2成仓
                    wantRatio=0.2;
                }
                
                obj = $.Buy(_N(allAmount*wantRatio/ticker.Sell, 3)); 
                if(obj){
                    opAmount = obj.amount;
                    Log("买入：买入量",opAmount);
                    nowAccount = _C(exchange.GetAccount);
                    Log("目前现金",nowAccount.Balance,"盈利",allAmount - initAccount.Balance);
                }
            }
        }
        Sleep(Interval*1000);
    }
}
```

> Detail

https://www.fmz.com/strategy/170557

> Last Modified

2019-10-20 15:52:19
