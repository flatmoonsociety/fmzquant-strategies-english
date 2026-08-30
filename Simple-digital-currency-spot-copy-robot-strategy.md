
> Name

Simple digital currency spot copy robot strategy
> Author

Inventor Quantification-Little Dream
> Strategy Description

## Simple digital currency spot copy robot strategy
Reference article: https://www.fmz.com/bbs-topic/6528
- The test function is a backtest test function that randomly places orders on the reference exchange to trigger the copy test.
- Add exchange objects. The first exchange object is the reference exchange, and the others are copy exchanges.
The strategy only provides design ideas for follow-up strategies. If you have any questions, please leave a message.


> Source (javascript)

``` javascript
function test() { 
    // 测试函数
    var ts = new Date().getTime()    
    if (ts % (1000 * 60 * 60 * 6) > 1000 * 60 * 60 * 5.5) {
        Sleep(1000 * 60 * 10)
        var x = Math.random()
        if (x > 0.5) {
            $.Buy(exchange, x / 10)    
        } else {
            $.Sell(exchange, x / 10)    
        }        
    }
}

function main() {
    LogReset(1)
    if (exchanges.length < 2) {
        throw "没有跟单的交易所"
    }
    var exName = exchange.GetName()
    // 检测参考交易所
    if (exName.includes("Futures_")) {
        throw "仅支持现货跟单"
    }
    Log("开始监控", exName, "交易所", "#FF0000")
    
    // 检测跟单交易所
    for (var i = 1 ; i < exchanges.length ; i++) {
        if (exchanges[i].GetName().includes("Futures_")) {
            throw "不支持期货交易所跟单"
        }
    }
    
    var initAcc = _C(exchange.GetAccount)
    while(1) {
        if(IsVirtual()) {
           // 测试函数
           test()  
        }  
        Sleep(5000)
        
        // 更新参考账户当前的账户信息
        var nowAcc = _C(exchange.GetAccount)
        
        // 参考交易所账户信息
        var refTbl = {
            type : "table", 
            title : "参考交易所",
            cols : ["名称", "币", "冻结币", "钱", "冻结钱"],
            rows : []
        }
        refTbl.rows.push([exName, nowAcc.Stocks, nowAcc.FrozenStocks, nowAcc.Balance, nowAcc.FrozenBalance])
        
        // 跟单交易所账户信息
        var followTbl = {
            type : "table", 
            title : "跟单交易所",
            cols : ["名称", "币", "冻结币", "钱", "冻结钱"],
            rows : []        
        }
        for (var i = 1 ; i < exchanges.length ; i++) {
            var acc = _C(exchanges[i].GetAccount)
            var name = exchanges[i].GetName()
            followTbl.rows.push([name, acc.Stocks, acc.FrozenStocks, acc.Balance, acc.FrozenBalance])
        }
        
        // 状态栏显示
        LogStatus(_D(), "\n`" + JSON.stringify(refTbl) + "`", "\n`" + JSON.stringify(followTbl) + "`")
        
        // 检测跟单
        var amount = (nowAcc.Stocks + nowAcc.FrozenStocks) - (initAcc.Stocks + initAcc.FrozenStocks)
        var func = null 
        if (amount > 0) {
            func = $.Buy
        } else if (amount < 0) {
            func = $.Sell
        } else {
            continue
        }
        
        // 执行跟单
        Log("跟单！数量：", Math.abs(amount), "#FF0000")
        for (var i = 1 ; i < exchanges.length ; i++) {            
            func(exchanges[i], Math.abs(amount))
        }
        
        // 执行跟单之后更新参考交易所账户信息记录
        initAcc = nowAcc
    }
}
```

> Detail

https://www.fmz.com/strategy/255182

> Last Modified

2021-04-08 16:38:12
