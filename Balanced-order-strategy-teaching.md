
> Name

Balanced order strategy teaching
> Author

Inventor Quantification-Little Dream
> Strategy Description

## The strategy principle is very simple
It is essentially a dynamic balancing strategy, but is designed to place orders in advance. The focus is on strategy teaching. Strategies have not been tested in long-term real trading, so use them with caution.
2020.09.04 OKEX Quantitative Trading Exclusive Conference Zhengzhou Station will explain strategies.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|IsReset|false|Recover data|
|BalanceDistance|500|Balance asset value (price currency)|



|Button|Default|Description|
|----|----|----|
|stop|__button__|Pause|
|continue|__button__|Continue|

> Source (javascript)

``` javascript
var Shannon = {
	// member
    e : exchanges[0],
    arrPlanOrders : [],
    distance : BalanceDistance,
    account : null,
    ticker : null, 
    initAccount : null,
    isAskPending : false,
    isBidPending : false,

    // function 
    CancelAllOrders : function (e) {
        while(true) {
            var orders = _C(e.GetOrders)
            if(orders.length == 0) {
                return 
            }
            Sleep(500)
            for(var i = 0; i < orders.length; i++) {
                e.CancelOrder(orders[i].Id, orders[i])
                Sleep(500)
            }
        }
    },

    Balance : function () {
        if (this.arrPlanOrders.length == 0) {
            this.CancelAllOrders(this.e)
            var acc = _C(this.e.GetAccount)
            this.account = acc
            var askPendingPrice = (this.distance + acc.Balance) / acc.Stocks
            var bidPendingPrice = (acc.Balance - this.distance) / acc.Stocks
            var askPendingAmount = this.distance / 2 / askPendingPrice
            var bidPendingAmount = this.distance / 2 / bidPendingPrice

            this.arrPlanOrders.push({tradeType : "ask", price : askPendingPrice, amount : askPendingAmount}) 
            this.arrPlanOrders.push({tradeType : "bid", price : bidPendingPrice, amount : bidPendingAmount})
        } else if(this.isAskPending == false && this.isBidPending == false) {
            for(var i = 0; i < this.arrPlanOrders.length; i++) {
                var tradeFun = this.arrPlanOrders[i].tradeType == "ask" ? this.e.Sell : this.e.Buy
                var id = tradeFun(this.arrPlanOrders[i].price, this.arrPlanOrders[i].amount)
                if(id) {
                	this.isAskPending = this.arrPlanOrders[i].tradeType == "ask" ? true : this.isAskPending
                	this.isBidPending = this.arrPlanOrders[i].tradeType == "bid" ? true : this.isBidPending
                } else {
                	Log("挂单失败，清理！")
                	this.CancelAllOrders(this.e)
                	return 
                }
            }
        }

        if(this.isBidPending || this.isAskPending) {
            var orders = _C(this.e.GetOrders)
            Sleep(1000)
            var ticker = _C(this.e.GetTicker)
            this.ticker = ticker
            if(this.isAskPending) {
                var isFoundAsk = false 
                for (var i = 0; i < orders.length; i++) {
                    if(orders[i].Type == ORDER_TYPE_SELL) {
                        isFoundAsk = true
                    }
                }
                if(!isFoundAsk) {
                    Log("卖单成交，撤销订单，重置")
                    this.CancelAllOrders(this.e)
                    this.arrPlanOrders = []
                    this.isAskPending = false 
                    this.isBidPending = false 
                    LogProfit(this.CalcProfit(ticker))
                    return 
                }
            }
            if(this.isBidPending) {
                var isFoundBid = false 
                for(var i = 0; i < orders.length; i++) {
                    if(orders[i].Type == ORDER_TYPE_BUY) {
                        isFoundBid = true
                    }
                }
                if(!isFoundBid) {
                    Log("买单成交，撤销订单，重置")
                    this.CancelAllOrders(this.e)
                    this.arrPlanOrders = []
                    this.isAskPending = false 
                    this.isBidPending = false 
                    LogProfit(this.CalcProfit(ticker))
                    return 
                }
            }        
        }
    }, 
    ShowTab : function() {
        var tblPlanOrders = {
            type : "table", 
            title : "计划挂单", 
            cols : ["方向", "价格", "数量"], 
            rows : []
        }
        for(var i = 0; i < this.arrPlanOrders.length; i++) {
            tblPlanOrders.rows.push([this.arrPlanOrders[i].tradeType, this.arrPlanOrders[i].price, this.arrPlanOrders[i].amount])
        }

        var tblAcc = {
            type : "table", 
            title : "账户信息", 
            cols : ["type", "Stocks", "FrozenStocks", "Balance", "FrozenBalance"], 
            rows : []            
        }
        tblAcc.rows.push(["初始", this.initAccount.Stocks, this.initAccount.FrozenStocks, this.initAccount.Balance, this.initAccount.FrozenBalance])
        tblAcc.rows.push(["当前", this.account.Stocks, this.account.FrozenStocks, this.account.Balance, this.account.FrozenBalance])
        
        return "时间：" + _D() + "\n `" + JSON.stringify([tblPlanOrders, tblAcc]) + "`" + "\n" + "ticker:" + JSON.stringify(this.ticker)
    },
    CalcProfit : function(ticker) {
        var acc = _C(this.e.GetAccount)
        this.account = acc
        return (this.account.Balance - this.initAccount.Balance) + (this.account.Stocks - this.initAccount.Stocks) * ticker.Last
    },
    Init : function() {
        this.initAccount = _C(this.e.GetAccount)
        if(IsReset) {
            var acc = _G("account")
            if(acc) {
                this.initAccount = acc 
            } else {
                Log("恢复初始账户信息失败！以初始状态运行！")
                _G("account", this.initAccount)
            }
        } else {
            _G("account", this.initAccount)
            LogReset(1)
            LogProfitReset()
        }
    },
    Exit : function() {
        Log("停止前，取消所有挂单...")
        this.CancelAllOrders(this.e)
    }
}

function main() {
    // 初始化
    Shannon.Init()

    // 主循环
	while(true) {
		Shannon.Balance()		
        LogStatus(Shannon.ShowTab())
        // 交互
        var cmd = GetCommand()
        if(cmd) {
            if(cmd == "stop") {
                while(true) {
                    LogStatus("暂停", Shannon.ShowTab())
                    cmd = GetCommand()
                    if(cmd) {
                        if(cmd == "continue") {
                            break
                        }
                    }
                    Sleep(1000)
                }
            }
        }
		Sleep(5000)
	}
}

function onexit() {
    Shannon.Exit()
}
```

> Detail

https://www.fmz.com/strategy/225746

> Last Modified

2020-09-04 23:17:03
