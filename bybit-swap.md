
> Name

bybit-swap Permanent Position Adding Strategy
> Author

gulishiduan_high frequency sorting
> Strategy Description

//Recently, some friends have reported that there are small bugs. Please go to the test network first. Parameters can be adjusted freely as needed. The essence of the strategy is to track the discount price of the K-line to determine the long and short positions. Simply put, it is to detect signals in real time through the turning point of the moving average.
//Register a new account, welcome to use my registration link: https://www.bytick.com/zh-CN/register/?affiliate_id=7586&language=en&group_id=0&group_type=2
//This link provides many strategies for connecting the three parties. /
//Basic principle: If the K-line continues to rise, continue to increase the position until the maximum position. /
//If long: It is not suitable for short market, but it will not continue to increase long positions during the decline. /
//If short: It is not suitable for the long market, but it will not continue to increase positions during the rise.
//Note the important point, long and short accounts can also be opened at the same time.
//For other strategies, please consult:weixin:ying5737
//You need to connect to the exchange yourself./Test with a demo account first. Please note that you are at your own risk.

// Daily level, or weekly level, we take the daily level as an example,
// Detect ma5ma10, the closing price of the k-line is above ma5, ma10, and ma5 is upward (it is judged that the closing price of yesterday's k-line > the closing price of the fifth k-line from the previous one), then open an order every day or directly buy 500u, continue to rise, and continue to increase positions.
// To increase the position, if there are two consecutive negative lines during the rise, buy 500u to increase the position on the third day. Each two consecutive negative statistics are counted separately.
// Sell, the K line has risen three times in a row to reduce the position by 1000u. (or the K-line has risen for four consecutive times to reduce the position by 2000u)
// Keep looping.
// The strategy runs for 13 days (or 21 days), automatically stops, closes or clears positions and orders.
// If the maximum position is 5000u, the position will only be reduced if it is larger than this position.
Above:
https://wx1.sinaimg.cn/mw1024/c5775633ly1gbsjvtrgnhj20m80dmmxy.jpg
https://wx1.sinaimg.cn/mw1024/c5775633ly1gbsjvty48uj21hc0u077o.jpg
https://wx2.sinaimg.cn/mw1024/c5775633ly1gbsjvu4iipj20lr0h775f.jpg

# Medium frequency unilateral trend strategy
## Monitor variables
1. Fast MA
2. Slow MA
3. Closing price
## Configuration parameters
1. Amount of single order
2. Single position reduction amountCloseAmount
3. Maximum position MaxPosition
## Go long
### Necessary conditions
1. The closing price of the K-line is greater than the fast MA and slow MA
2. The fast MA is rising (it is judged that the closing price of yesterday's K line is greater than the closing price of the fifth K line from the previous one)
### Place an order
1. Three consecutive positives, reduce positions CloseAmount
2. Two consecutive negative periods, increase the position by Amount. That is to say, if there are two consecutive negative events, you will place an order of 2*Amount.
3. Under normal circumstances, place an order for Amount
### Limitations
1. If the maximum position is greater than MaxPosition, no order will be placed.
### Exit
1. Exit after running N K lines
## Short selling
### Necessary conditions
1. The closing price of the K-line is less than the fast MA and slow MA
2. And the fast MA is upward (it is judged that the closing price of yesterday's k line is less than the closing price of the Nth k line from the previous one (fast MA cycle))
### Place an order
1. Three consecutive negative events, reduce positions by CloseAmount
2. Two consecutive positives, increase the position by Amount. That is to say, if there are two consecutive negative events, you will place an order of 2*Amount.
3. Under normal circumstances, place an order for Amount
### Limitations
1. If the maximum position is greater than MaxPosition, no order will be placed.
### Exit
1. Exit after running N K lines
## Notes
1. The program will obtain the position information of the account each time as the position amount of the strategy
2. Please bind fmz WeChat, the program will push WeChat in important places
3.
## Parameters
1. Fast MA cycle
2. Slow MA period
3. Polling interval (ms)
4. Long and short options
5. Leverage size: 0 means full position mode
6. Contract type: Currently fmex only supports swap, and only swap can be filled in. OKEx backtesting can be used during backtesting, which can be set to this_week, this_month, etc.
7. Single position reduction amount. When the conditions for reducing positions are met, the amount of one-time reduction
8. Maximum position (u)
9. API base address. Can be set to https://api.fmex.com，或https://api.testnet.fmex.com
10. Strategy K number exit. How many K lines does the strategy run before exiting normally?
11. Whether to clear positions when the strategy actively exits.
12. Whether interaction is required. The strategy exits normally after meeting the exit conditions. If interaction is required, commands such as manual intervention will be awaited. If it is not needed, the program exits directly.
13. Whether to take the order. If it is checked, the order will be a market order. If it is not checked, it will be a pending order. The buy order is placed on the buy one and the sell order is placed on the sell one.
14. Number of continuous positive (yin) K lines (when going long, continuous positive lines). Signal to reduce position, such as long position, continuous positive line, reduce position
15. The number of continuous Yin (Yang) K lines (when going long, continuous Yin lines). Number of continuous Yin (Yang) K lines (when going long, continuous Yin lines)
16. Is the market volatile? Check the box to indicate a volatile market
## Interaction
**Interaction is only valid when `是否需要交互`**
**Interaction occurs when the policy exits normally**
1. Continue. Continue to reset the strategy and rerun the same parameters
2. Stop. policy stop exit
3. Continue after switching the strategy market. Switch the market to shock or trend and continue running. It is an extension of interaction 1 'continue'.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|fastMaPeriod|5|Fast MA Period|
|slowMaPeriod|10|Slow MA Period|
|interval|1000|Polling interval (ms)|
|direction|0|Long and short options: long|short|
|marginLevel|false|Leverage size|
|contractType|swap|Contract type (default perpetual)|
|amount|500|Amount of single order/position(u)|
|closeAmount|1000|Single position reduction amount (u)|
|maxHoldAmount|5000|Maximum position (u)|
|baseUrl|https://api.bybit.com|API基地址|
|runNBars|13|Strategy K number exit|
|isCleanPosition|true|Whether to clear positions when the strategy actively exits|
|enableCommand|true|Whether interaction is required|
|isTaker|true|Whether to take the order|
|maxSameDirKNum|3|The number of n consecutive positive (yin) K lines (when going long, continuous positive lines will reduce the position)|
|maxOppositeDirKNum|2|Number of consecutive Yin (Yang) K lines (when going long, add positions on continuous Yin lines)|
|isShock|false|Is it a shock market|



|Button|Default|Description|
|----|----|----|
|Continue|__button__|Whether to continue|
|Stop|__button__|Whether to stop|
|Switch strategy market|0|Continue after switching strategy market: shock|trend|

> Source (javascript)

``` javascript

/*联系微信：ying5737(策略讨论，支持付费编写)
# 中频单边趋势策略
## 监测变量
1. 快MA
2. 慢MA
3. 收盘价
## 配置参数
1. 单次下单量Amount
2. 单次减仓量CloseAmount
3. 最大持仓量MaxPosition
## 做多
### 必要条件
1. k线收盘价大于快MA与慢MA
2. 且快MA上行(判断为昨日k线收盘价大于往前数第5根k收盘价)
### 下单
1. 三连阳，减仓CloseAmount
2. 两连阴，加仓Amount。也就是出现两连阴会下单2*Amount
3. 正常情况，开单Amount
### 限制
1. 最大持仓量大于MaxPosition则不开单
### 退出
1. 运行N根K线之后退出

## 做空
### 必要条件
1. k线收盘价小于快MA与慢MA
2. 且快MA下行(判断为昨日k线收盘价小于往前数第N(快MA5周期)根k收盘价)
### 下单
1. 三连阴，减仓CloseAmount
2. 两连阳，加仓Amount。也就是出现两连阴会下单2*Amount
3. 正常情况，开单Amount
### 限制
1. 最大持仓量大于MaxPosition则不开单
### 退出
1. 运行N根K线之后退出
## 注意事项
1. 程序会每次会获取账户的持仓信息做为策略的持仓量
2. 请绑定fmz微信，程序会重要的地方推送微信
## 参数
1. 快MA周期
2. 慢MA周期	
3. 轮询间隔(ms)	
4. 多空选择
5. 杠杆大小: 0表示全仓模式
6. 合约类型: 目前fmex只支持swap，只能填写swap。回测时可用OKEx回测，此处可设置为this_week, this_month等
7. 单次减仓量。达到减仓条件时，一次减仓量
8. 最大持仓(u)
9. API基地址。可设置为https://api.fmex.com，或测试网https://api.testnet.fmex.com
10. 策略K数退出. 策略运行多少个K线后正常退出
11. 策略主动退出时是否清仓。
12. 是否需要交互。策略在满足退出条件后，正常退出时。如果需要交互，则会等待人工干预等命令。如果不需要，则程序直接退出了
13. 是否吃单。勾选，则下单是市价单，不勾选，则是挂单，买单挂在买一，卖单挂在卖一
14. 连续阳(阴)K线数(做多时，连续阳线)。减仓信号，如做多时，连续阳线，减仓
15. 连续阴(阳)K线数(做多时，连续阴线)。连续阴(阳)K线数(做多时，连续阴线)	
16. 是否是震荡行情。勾选是震荡行情
## 交互
**交互只有在`是否需要交互`时有效**
**交互是在策略正常退出时进行交互**
1. 继续。继续是策略复位，重新运行相同的参数
2. 停止。策略停止退出
3. 切换策略行情后继续.切换行情为震荡或趋势后继续运行，是交互1'继续'的一种扩展
*/
////////////////// params ////////////////////////
//var fastMaPeriod = 5
//var slowMaPeriod = 10
//var direction = 做多|做空
//var interval = 1000
//var amount = 500
//var maxHoldAmount = 5000
//var closeAmount = 1000
//var runNBars = 13
//var marginLevel = 0
//var contractType = 'swap'
//var enableCommand = false
//var isTaker = true
//var maxOppositeDirKNum = 2
//var maxSameDirKNum = 3
//var isShock = false
////////////////// variable ////////////////////////

var makeLong = direction == 0 ? true:false
var startTime = null
var holdAmount = 0
var lastBar = null
var yinxianCnt = 0
var yangxianCnt = 0
var lastClose = 0
var last5thClose = 0
var fastMa = []
var slowMa = []
var barCnt = 0
var localIsShock = false
////////////////////////////////////////////////
var PreBarTime = 0
var isFirst = true

function PlotMA_Kline(records){
    $.PlotRecords(records, 'K')
    if(fastMa.length == 0) {
        fastMa = TA.MA(records, fastMaPeriod)
    }
    if(slowMa.length == 0) {
        slowMa = TA.MA(records, slowMaPeriod)
    }
    if(isFirst){
        $.PlotFlag(records[records.length - 1].Time, 'Start', 'STR')
        for(var i = records.length - 1; i >= 0; i--){
            if(fastMa[i] !== null){
                $.PlotLine('ma'+fastMaPeriod, fastMa[i], records[i].Time)
            }
            if(slowMa[i] !== null){
                $.PlotLine('ma'+slowMaPeriod, slowMa[i], records[i].Time)
            }
        }
        PreBarTime = records[records.length - 1].Time
        isFirst = false
    } else {
        if(PreBarTime !== records[records.length - 1].Time){
            $.PlotLine('ma'+fastMaPeriod, fastMa[fastMa.length - 2], records[fastMa.length - 2].Time)
            $.PlotLine('ma'+slowMaPeriod, slowMa[slowMa.length - 2], records[slowMa.length - 2].Time)
            PreBarTime = records[records.length - 1].Time
        }
        $.PlotLine('ma'+fastMaPeriod, fastMa[fastMa.length - 1], records[fastMa.length - 1].Time)
        $.PlotLine('ma'+slowMaPeriod, slowMa[slowMa.length - 1], records[slowMa.length - 1].Time)
}
}

function init () {
    if (fastMaPeriod > slowMaPeriod) {
        throw '快MA周期 > 慢MA周期, 请检查设置'
    }
    Log('快MA周期	    :'  + fastMaPeriod)
    Log('慢MA周期	    :' + slowMaPeriod)
    Log('轮询间隔(ms)   :' + interval)
    Log('是否是震荡策略  :' + (isShock?'是':'否'))
    Log('多空选择	    :' + (direction == 0 ? '多':'空'))
    Log('杠杆大小	    :' + (marginLevel == 0 ? '全仓':marginLevel))
    Log('连续阳(阴)K线数(做多时，连续阳线)数   :' + maxSameDirKNum)
    Log('连续阴(阳)K线数(做多时，连续阴线)   :' + maxOppositeDirKNum)
    Log('运行多少根K后退出   :' + runNBars)
    startTime = new Date()
    localIsShock = isShock
}

function onexit() {
    Log('退出')
}

function onerror() {
    Log('出错退出')
}

function openLong(ex, openAmount) {
    if (holdAmount + openAmount <= maxHoldAmount) {
        Log('已持仓: ' + holdAmount + ', 加仓:' + openAmount)
        ex.SetDirection('buy')
        if(isTaker) {
            ex.Buy(-1, openAmount, '吃单')
            holdAmount += openAmount
        } else {
            var ticker = _C(ex.GetTicker)
            if(ticker == null) {
                return false
            }
            ex.Buy(ticker.Buy, openAmount, '挂单')
        }
        return true
    } else {
        Log('持仓('+holdAmount+') 过多，不加仓')
        return false
    }
}

function closeLong(ex, closeAmount) {
    if (holdAmount >= closeAmount) {
        Log('已持仓: ' + holdAmount + ', 减仓:' + closeAmount)
        ex.SetDirection('closebuy')
        ex.Sell(-1, closeAmount)
        holdAmount -= closeAmount
        return true
    } else {
        Log('持仓('+holdAmount+') 过少，不减仓')
        return false
    }
}

function openShort(ex, openAmount) {
    if (holdAmount + openAmount <= maxHoldAmount) {
        Log('已持仓: ' + holdAmount + ', 加仓:' + openAmount)
        ex.SetDirection('sell')
        if(isTaker) {
            ex.Sell(-1, openAmount, '吃单')
            holdAmount += openAmount
        } else {
            var ticker = _C(ex.GetTicker)
            if(ticker == null) {
                return false
            }
            ex.Sell(ticker.Sell, openAmount, '挂单')
        }
        return true
    } else {
        Log('持仓('+holdAmount+') 过多，不加仓')
        return false
    }
}

function closeShort(ex, closeAmount) {
    if (holdAmount >= closeAmount) {
        Log('已持仓: ' + holdAmount + ', 减仓:' + closeAmount)
        ex.SetDirection('closesell')
        ex.Buy(-1, closeAmount)
        holdAmount -= closeAmount
        return true
    } else {
        Log('持仓('+holdAmount+') 过少，不减仓')
        return false
    }
}

function cancelOrders(ex) {
    Log('取消所有挂单')
    while(true) {
        var orders = _C(ex.GetOrders)
        if (orders.length == 0) {
            break
        }
        for(var i = 0; i < orders.length;i++) {
            ex.CancelOrder(orders[i].Id)
        }
    }
}

function updatePosition(ex) {
    var pos = ex.GetPosition()
    if(typeof(pos) === 'undefined' || pos === null || 
        pos.length == 0 || typeof(pos[0].Type) == 'undefined'  || typeof(pos[0].Amount) == 'undefined' ) {
        return
    }
    Log('仓位信息:' + (pos[0].Type == 0?'多仓,   ':'空仓,  ') + JSON.stringify(pos))
    if(pos.length>0){
        holdAmount = pos[0].Amount
        // if(pos[0].Type == 0){ //多仓
        //     ordersInfo.pos = pos[0].Amount
        // }else{
        //     ordersInfo.pos = -pos[0].Amount
        // }
    }
}

function longStrategy(ex, records) {
    var lastSecondBar = records[records.length-2]

    if ((   lastSecondBar.Close > fastMa[fastMa.length - 2] && 
            lastSecondBar.Close > slowMa[slowMa.length - 2] && 
            lastSecondBar.Close > records[records.length - 2 - fastMaPeriod].Close
        ) || localIsShock){
            var openAmount = amount
            if (lastSecondBar.Close < lastSecondBar.Open) {
                yinxianCnt += 1
                yangxianCnt = 0
            } else if (lastSecondBar.Close > lastSecondBar.Open){
                yinxianCnt = 0
                yangxianCnt += 1
            } else {
                yangxianCnt = 0
                yinxianCnt = 0
            }

            if (yinxianCnt >= maxOppositeDirKNum) {
                Log('两连阴')
                openAmount += amount
                yinxianCnt = 0
            }

            if (yangxianCnt >= maxSameDirKNum) {
                Log('三连阳')
                yangxianCnt = 0
                Log('准备减仓')
                if(closeLong(ex, closeAmount)){
                    $.PlotFlag(records[records.length - 1].Time, 'closeLong', 'CL')
                }
            } else {
                Log('准备开仓')
                if(localIsShock) {
                    openAmount -= amount
                }
                if(openLong(ex, openAmount)){
                    $.PlotFlag(records[records.length - 1].Time, 'openLong', 'OL')
                }
            }
    }
}

function shortStrategy(ex, records) {
    var lastSecondBar = records[records.length-2]

    if ((   lastSecondBar.Close < fastMa[fastMa.length - 2] && 
            lastSecondBar.Close < slowMa[slowMa.length - 2] && 
            lastSecondBar.Close < records[records.length - 2 - fastMaPeriod].Close
        ) || localIsShock){
            var openAmount = amount
            if (lastSecondBar.Close < lastSecondBar.Open) {
                yinxianCnt += 1
                yangxianCnt = 0
            } else if (lastSecondBar.Close > lastSecondBar.Open){
                yinxianCnt = 0
                yangxianCnt += 1
            } else {
                yangxianCnt = 0
                yinxianCnt = 0
            }

            if (yangxianCnt >= maxOppositeDirKNum) {
                Log('两连阳')
                yangxianCnt = 0
                openAmount += amount
            } 

            if (yinxianCnt >= maxSameDirKNum) {
                Log('三连阴')
                yinxianCnt = 0
                Log('准备减仓')
                if(closeShort(ex, closeAmount)){
                    $.PlotFlag(records[records.length - 1].Time, 'closeShort', 'CS')
                }
            } else {
                Log('准备开仓')
                if(localIsShock) {
                    openAmount -= amount
                }
                if(openShort(ex, openAmount)){
                    $.PlotFlag(records[records.length - 1].Time, 'openShort', 'OS')
                }
            }
    }
}

function onBar (ex) {
    var records = _C(ex.GetRecords)
    if (records === null || records.length < slowMaPeriod) {
        return 
    }
    if (lastBar == null) {
        lastBar = records[records.length-1]
    }
    
    if (lastBar.Time == records[records.length-1].Time) {
        return
    }
    lastBar = records[records.length-1]
    updatePosition(ex)
    PlotMA_Kline(records)
    barCnt += 1

    var lastSecondBar = records[records.length-2]
    fastMa = TA.MA(records, fastMaPeriod)
    slowMa = TA.MA(records, slowMaPeriod)
    lastClose = lastSecondBar.Close
    last5thClose = records[records.length - 2 - 5].Close

    Log('收盘价:' +lastSecondBar.Close + 
    ', 前第5个收盘价:' +records[records.length - 2 - 5].Close + 
    ', 快MA:' + _N(fastMa[fastMa.length - 2]) +
    ', 慢MA:' + _N(slowMa[slowMa.length - 2]))
    if (makeLong) {
        longStrategy(ex, records)
    } else {
        shortStrategy(ex, records)
    }
}

function runLife(ex) {
    // var pass = new Date() - startTime
    if (barCnt >= runNBars) {
        if(isCleanPosition) {
            Log('已运行'+barCnt+'K周期,结束，取消订单，清仓#ff0000@')
            cancelOrders(ex)
            updatePosition(ex)
            $.PlotFlag(lastBar.Time, 'Exit', 'EXT')
            
            if (makeLong) {
                closeLong(ex, holdAmount)
            } else {
                closeShort(ex, holdAmount)
            }    
        } else {
            Log('已运行'+barCnt+'K周期,结束，不取消订单，不清仓#ff0000@')
            updatePosition(ex)
            $.PlotFlag(lastBar.Time, 'Exit', 'EXT')
        }
        return true
    } else {
        return false
    }
}

function status() {
    var table = {
        type: 'table',
        title: '信息',
        cols: [
            '运行K数',
            '持仓量',
            '阳线',
            '阴线',
            '收盘价',
            '前第5个收盘价',
            'MA'+fastMaPeriod,
            'MA'+slowMaPeriod,
        ],
        rows: []
      }
      table.rows.push([
            barCnt,
            holdAmount,
            yangxianCnt,
            yinxianCnt,
            lastClose,
            last5thClose,
            fastMa.length == 0 ? 0 : _N(fastMa[fastMa.length - 2]),
            slowMa.length == 0 ? 0 : _N(slowMa[slowMa.length - 2])
      ])
    LogStatus(
        '现在时间:' +_D() +
        '\n启动时间:' +startTime +
        '\n`' +
        JSON.stringify(table)+
        '`\n' +
        '\n托管者版本:' +Version() +
        '\n联系Wechat:ying5737#00ff00' +
        '\nWechat: ying5737info#ff000f'
      )

}

function reset() {
    holdAmount = 0
    lastBar = null
    yinxianCnt = 0
    yangxianCnt = 0
    lastClose = 0
    last5thClose = 0
    fastMa = []
    slowMa = []
    barCnt = 0
}

function main () {
    var ex = exchanges[0]

    Log('开工   '+ex.GetName())
 //   if(ex.GetName() != 'Futures_FMex' && !IsVirtual()) {
  //      throw '仅仅支持FMex'
  //  }
    Log('基地址  ' + baseUrl)
    if(!IsVirtual()){
        ex.IO('base', baseUrl) //切换基地址，方便切换实盘和模拟盘，实盘地址：https://api.fmex.com
    }
    ex.SetTimeout(1000);
    _CDelay(500)
    ex.SetContractType(contractType)
    ex.SetMarginLevel(marginLevel)
    updatePosition(ex)
    while (true) {
        try {
            if(!IsVirtual() && runLife(ex)) {
                if((typeof(GetCommand) == 'function') && enableCommand){
                    Log('等待指令, 继续 | 停止 #ff0000@')
                    while (true) {
                        var cmd = GetCommand()
                        if (cmd) {
                            Log('收到指令: '+cmd)
                            switch(cmd) {
                                case '停止':
                                    Log('停止, 退出!#ff0000@')
                                    return
                                case '继续':
                                    reset()
                                    Log('继续, 复位，开工!#ff0000@')
                                    break
                                case '切换策略行情:0':
                                    reset()
                                    localIsShock = true
                                    Log('切换策略行情为震荡行情继续, 复位，开工!#ff0000@')
                                    break
                                case '切换策略行情:1':
                                    reset()
                                    localIsShock = false
                                    Log('切换策略行情为趋势行情继续, 复位，开工!#ff0000@')
                                    break
                            }
                            if (cmd == '停止'){
                                Log('停止, 退出!#ff0000@')
                                return
                            } else if (cmd == '继续') {
                                reset()
                                Log('继续, 复位，开工!#ff0000@')
                                break
                            }
                        }
                        updatePosition(ex)
                        status()
                        Sleep(1000)
                    }
                } else {
                    Log('停止, 退出!#ff0000@')
                    return
                }
            }
            onBar(ex)
            status()
        } catch(e) {
            Log('出错了:'+e+', 请及时处理#ff0000@')
        }
        Sleep(interval)
    }
}

```

> Detail

https://www.fmz.com/strategy/205469

> Last Modified

2021-01-08 19:20:42
