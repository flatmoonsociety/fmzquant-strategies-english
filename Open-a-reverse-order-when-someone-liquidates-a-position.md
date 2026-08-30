
> Name

Open a reverse order when someone liquidates a position
> Author

Exodus[strategy ghostwriting]
> Strategy Description

Someone asked me to write a ghostwriting strategy. After writing it, I didn’t want it anymore, and I didn’t give any money.
I just wrote it in vain and wished him a coupon for buying a coffin.
The strategy does not support backtesting.
This strategy only supports currency standard. After selecting the currency, it will detect the liquidation order of the corresponding currency. If there is a short order and it is liquidated, it will be opened as long. If there are many orders as it is liquidated, it will be opened as a short position. There is no closing logic.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|openDistance|false|Pending order distance (percentage, if it is 0, it is a market order)|
|cancelOrderTime|true|Order cancellation time (how long it took for the pending order to be cancelled, unit: minutes)|
|tickPeriod|15|Detection period (seconds)|
|margin|20|Leverage multiple|
|buyMinute|-1|(for testing) buying time|
|sellMinute|-1|(for testing) selling time|
|contractType|swap|Contract type|
|orderType|0|Order method: fixed number of pieces|Balance percentage|
|orderVolume|3|Order volume (corresponding to the number of pieces ordering method or percentage ordering method)|
|qtyValueSequence|0.4626,|Contract number sequence, how many coins corresponds to one contract|
|xbtApi|false|Use coin-based API|

> Source (javascript)

``` javascript
/*backtest
start: 2021-05-07 00:00:00
end: 2021-08-04 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"LTC_USDT","balance":200},{"eid":"Futures_Binance","currency":"BTC_USDT","balance":500},{"eid":"Futures_Binance","currency":"ETH_USDT","balance":200},{"eid":"Futures_Binance","currency":"EOS_USDT","balance":500},{"eid":"Futures_Binance","currency":"BCH_USDT","balance":500}]
args: [["stopProfitRate",100],["cancelOrderTime",15]]
*/

class MyExchange{
    constructor(tExchange,tIndex,tQtyValue){
        this.exchange=tExchange;       
        this.getThis=()=>this;
        this.exchange.SetContractType(contractType);
        this.exchange.SetMarginLevel(margin);
        
        this.currency=this.exchange.GetCurrency();
        let precision = $.GetPrecision(this.exchange);
        this.pricePrecision = $.GetPricePrecision(this.currency);
        this.amountPrecision = $.GetAmountPrecision(this.currency);
        
        this.index=tIndex;
        this.qtyValue=tQtyValue;
        
        //币本位账户资金
        this.walletBalance=0;
        this.unrealizedProfit=0;
        this.marginBalance=0;
        this.availableBalance=0;
        
        this.exchange.SetMaxBarLen(2000);
        
        //注册wss链接
        let eName = this.currency.replace("_", "").toLowerCase();
        let symbol=eName+"t@forceOrder";
        if(xbtApi)
            symbol=eName+"@forceOrder";
        //let symbol=eName+"t@aggTrade";
        let str = "wss://fstream.binance.com/ws/" + symbol + "|reconnect=true";
        this.streamClient=Dial(str);
        Log(this.currency+"wss链接为:"+str);
    }
    
    Open(direction,curPrice,distance){
        let pricePrecision=this.pricePrecision;
        let amountPrecision=this.amountPrecision;
        //Log("价格精度",pricePrecision,"数量精度",amountPrecision);
        if(this.walletBalance==0)
            return;
        let orderAmount = orderVolume;
        if(orderType==1){//百分比
            if(xbt)
                orderAmount=Math.floor(Math.floor(this.walletBalance/this.qtyValue)*0.01*orderVolume);//张数               
        }
        
        if($.GetPosByDirection(PD_LONG,this.exchange)==null && direction==PD_LONG){//同时只开一个多单
            Log(this.exchange.GetCurrency(),"挂多单");
            this.exchange.SetDirection("buy");
            if(xbt)
                this.exchange.Buy(distance==0?-1:_N(curPrice*(1-0.01*distance),pricePrecision),orderAmount);//张
            else
                this.exchange.Buy(distance==0?-1:_N(curPrice*(1-0.01*distance),pricePrecision),_N((buyVolume/curPrice)*margin,amountPrecision));
           
            
        }
         if($.GetPosByDirection(PD_SHORT,this.exchange)==null && direction==PD_SHORT){
            this.exchange.SetDirection("sell");
            Log(this.exchange.GetCurrency(),"挂空单");
            if(xbt)
                this.exchange.Sell(distance==0?-1:_N(curPrice*(1+0.01*distance),pricePrecision),orderAmount); //张
            else
                this.exchange.Sell(distance==0?-1:_N(curPrice*(1+0.01*distance),pricePrecision),_N((buyVolume/curPrice)*margin,amountPrecision));  
           
        }
    }
    
    UpdateBalance(walletBalance,unrealizedProfit,marginBalance,availableBalance){
        this.walletBalance=walletBalance;
        this.unrealizedProfit=unrealizedProfit;
        this.marginBalance=marginBalance;
        this.availableBalance=availableBalance;//同步资金用于开仓方法
    }
    run(){
           let buy=false;
           let sell=false;
       
            let socketRs = null;
           
            try {
                socketRs = JSON.parse(this.streamClient.read(-2));//获取websocket
            } catch (e) {
                socketRs = null;
                //Log('获取价格异常(不影响程序运行)：',e); 
            }
            //Log(socketRs);
            if (socketRs == null || typeof(socketRs) == "undefined") {
                //Log("获取行情信息失败。。。。。。。。。。。。。。。。");        
            } else {
                let o = socketRs.o;
                Log("收到强平信息,socketRs.o为：",o);
                if(o.S=="SELL")
                    buy=true;
                if(o.S=="BUY")
                    sell=true;
            }
        
     
        
        
        //平掉漏开的单
        let orders=_C(this.exchange.GetOrders);
        for(let i=0;i<orders.length;i++){
           
            if(orders[i]!=null && Math.floor(_N((Unix()*1000-orders[i].Info.time)/(PERIOD_M1*1000),1))>=cancelOrderTime){
                Log("发现开仓订单经过"+cancelOrderTime+"分钟后仍未成交");
                Log("撤销开仓订单");                
                this.exchange.CancelOrder(orders[i].Id,orders[i]);
                
            }
             
        }
       
        
        let curMinute=new Date().getMinutes();
        //测试
        if(curMinute==buyMinute)
            buy=true;
        if(curMinute==sellMinute)
            sell=true;
        if(buy){
            Log("买入开始");
            let shortPos=$.GetPosByDirection(PD_SHORT,this.exchange);
            if(shortPos)
                $.CloseAmount(PD_SHORT,shortPos.Amount,shortPos,this.exchange);//平空
            $.CancelAllOrder(this.exchange);//清空所有订单
            let curPrice=_C(this.exchange.GetTicker).Last;
            this.Open(PD_LONG,curPrice,openDistance);//开多
        } 
        if(sell){
            Log("卖出开始");
            let longPos=$.GetPosByDirection(PD_LONG,this.exchange);
            if(longPos)
                $.CloseAmount(PD_LONG,longPos.Amount,longPos,this.exchange);//平多
            $.CancelAllOrder(this.exchange);//清空所有订单
            let curPrice=_C(this.exchange.GetTicker).Last;
            this.Open(PD_SHORT,curPrice,openDistance);
        }
        
        table.rows.push([this.currency,this.walletBalance,this.unrealizedProfit,this.marginBalance,this.availableBalance]);
       
    }
}
function GetAllBalance(exchange){
   
    let account=_C(exchange.GetAccount);
    let info=account.Info;
    let assets=info.assets;
    /*let totalWalletBalance=info.totalWalletBalance;//钱包余额
    let canUseBalance=account.Balance;//可用余额
    let frozenBalance=account.FrozenBalance;
    let frozenStocks=account.FrozenStocks;
    return {totalWalletBalance,canUseBalance,frozenBalance,frozenStocks};*/
    return {account,assets};
}

function FindExchange(currency){
    for(let myE of myExchanges){
        //Log(myE.currency,currency);
        if(myE.currency==currency){
            return myE.getThis();
        }
    }
}


var lastRunSecond = 0;

var myExchanges=new Array();
let qtyValueArray=new Array();
var xbt=true;
function main() {
   
    if(_G("profit")){
        LogProfit(_G("profit"));
    }else{
        _G("profit",0);
        LogProfit(0);
    }
   
    qtyValueArray=qtyValueSequence.split(",");
    for (let i = 0; i < exchanges.length; i++) {

        myExchanges.push(new MyExchange(exchanges[i],i,parseFloat(qtyValueArray[i])));
    }
    
     table = {
            type: "table",
            title: "账户信息",
            cols: ["币种","钱包余额", "未实现盈亏", "保证金余额", "可下单余额"],
            rows: [

            ]
        }
    
    /*if (IsVirtual() == false) {
        var symbols = "";
        for (let i = 0; i < exchanges.length; i++) {
            let e = exchanges[i];
            let eName = e.GetCurrency().replace("_", "").toLowerCase();
            symbols += eName + "@forceOrder" + (i == exchanges.length - 1 ? "" : "/");

        }

        let str = "wss://fstream.binance.com/stream?streams=" + symbols + "|reconnect=true";
        let str1="wss://fstream.binance.com/stream?streams=!forceOrder@arr|reconnect=true"
        Log("websocket请求链接为:" + str1);
        streamClient = Dial(str1);
    }*/
    
    while(true){
        
        let date = new Date();
        let curMinute = date.getMinutes();
        
       
         /*if(useTKTick && Math.abs( curSecond - lastCloseSecond)> basePeriod ){
            //Log("检测价格");
            for(let myE of myExchanges){
                myE.getThis().CloseImmidiate();
                //Log("实时止盈");
            }
            lastCloseSecond=Unix();
        }*/

        if (Unix() - lastRunSecond > tickPeriod ) {
           table.rows.length=0;
            for (let myE of myExchanges) {
                myE.getThis().run();
            }
            lastRunSecond = Unix();
            
            //打印账户信息
            let balance=GetAllBalance(exchange);
            let account=balance.account;
            let assets=balance.assets;
            for(let i=0;i<assets.length;i++){
                let asset=assets[i];
                //table.rows.push([asset.asset+"USD",asset.walletBalance,asset.unrealizedProfit,asset.marginBalance,asset.availableBalance]);
                let e=FindExchange(asset.asset+"_USD");
                if(e!=null)
                    e.UpdateBalance(asset.walletBalance,asset.unrealizedProfit,asset.marginBalance,asset.availableBalance);
                //Log(asset.walletBalance,asset.unrealizedProfit,asset.marginBalance,asset.availableBalance);
            }
            
            LogStatus("`" + JSON.stringify(table) + "`")
        }

        let curMillSecond = date.getMilliseconds();
        Sleep(1000 - curMillSecond);
    }
    
}

function onexit(){    
         Log("撤销所有订单");
         for(let e of exchanges){
            let orders= _C(e.GetOrders);
            for (var i = 0 ; i < orders.length ; i++) {           
                e.CancelOrder(orders[i].Id)
            }
         }
    
}
```

> Detail

https://www.fmz.com/strategy/323894

> Last Modified

2021-10-18 23:05:15
