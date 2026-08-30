
> Name

Bit-Maker-Spot USDT equal amount monitoring
> Author

AutoBitMaker-ABM

> Strategy Description

**AutoBitMaker** now officially launches risk-free arbitrage strategy.
The principle of the strategy is spot and contract hedging, and this process can also be completed manually.
But compared to manual operation, BOT will capture the profit margins of all trading pairs in the market and conduct hundreds of transactions every day. Free up your hands and reduce market risks.
The current code is only for account monitoring, and the source code is published for everyone to check or use.
Monitor spot USDT value.
We are **AutoBitMaker**, referred to as **ABM Capital**. Please carefully identify the team name and WeChat ID to identify the authenticity.
We currently only communicate with domestic customers through WeChat and Email contact methods, and do not use other methods such as QQ.
**ABM Team** currently provides 3 types of strategies
* Contract trading
* Spot trading
* Arbitrage trade
The self-learning grid is based on the traditional grid strategy idea, but after long-term real trading + backtest data, dozens of parameter configurations such as position opening logic, position addition timing, take-profit position, position ratio, and grid spacing have been optimized. The intelligent dynamic position addition model and take-profit position are implemented, which can avoid the high risks that traditional grids need to bear when encountering unilateral situations, and use extremely low positions to achieve a good profit drawdown ratio.
The strategy configuration parameters are extremely rich. The team will assign dedicated personnel to customize a unique parameter combination for your account based on customer risk and return needs, and have around-the-clock manual + automated market monitoring.
We have self-developed unique index trading collections. Each index trading collection contains a variety of high-quality single trading pairs, and each trading pair has a unique weight ratio. The robot runs a self-learning grid strategy on the index set to avoid the unilateral risk of a single trading pair.
In addition to the built-in static index, we define dynamic indexes of multiple currency selection models for the index set, and select leading currencies in each sector to form an index level, further reducing risks.
A single account can be configured to run multiple single-currency trading pairs and index trading pairs at the same time, which can not only share risks, but also help you make profits in various complex market conditions.
At present, the team's strategy server cluster has reached 80, and there are more than 50 support servers. The stop-loss conditions of the account are checked at an average speed of 2 times per second, allowing for quick exit when risks come.
Using the heterogeneous hybrid cloud architecture of Alibaba Cloud, Amazon Cloud, and Microsoft Cloud, management and execution nodes are separated, clusters are formed between multiple nodes to ensure redundancy, and the smooth operation of business and financial security are safely and effectively realized.
About the trial:
Depending on your capital size, we provide a trial run of about 2 weeks. During the trial period, we do not charge commission.
After Bot takes over your account, please do not do any operations on your own. When any other manual positions are detected, all Bots will exit immediately.
About commission:
This depends on the amount of funds you have. We can talk more about it after the trial run. If you create an account using our referral link, we will receive a low commission.
Contact information:
1. Interviews are available nationwide
2. WeChat: DuQi_SEC/autobitmaker/autobitmaker_001/Shawn_gb2312/ABM_DD
3. Email: liuhongyu.louie@autobitmaker.com/autobitmaker_master@autobitmaker.com
* Special reminder (WeChat ID autobitmaker001 is not us!! We are not called makebit either!! WeChat ID autobitmaker_001 is us)
Submit trial application for WeChat mini program:
![WeChat Mini Program Code](https://www.fmz.cn![IMG](https://www.fmz.com/upload/asset/1281e73989f891ac26aa9.jpg))
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|baseOriginalBalance|10000|baseOriginalBalance|


> Source (javascript)

``` javascript
//exchanges[0] is spot

var chart = {
    __isStock: false,
    extension: {
        layout: 'single',
        col: 8,
        height: '300px'
    },
    tooltip: {
        xDateFormat: '%Y-%m-%d %H:%M:%S, %A'
    },
    title: {
        text: 'Account_Balance_Detail'
    },
    xAxis: {
        type: 'datetime'
    },
    yAxis: {
        title: {
            text: 'USDT'
        },
        opposite: false
    },
    series: []
};

function initChart() {
    chart.series.push({
        name: "Account_" + (Number(0)) + "_Detail",
        id: "Account_" + (Number(0)) + "_Detail",
        data: []
    });
}

function getChartPosition(avaliableMargin) {
    return {
        __isStock: false,
        extension: {
            layout: 'single',
            col: 4,
            height: '300px'
        },
        title: {
            text: '保证金占比(%)'
        },
        series: [{
            type: 'pie',
            name: 'one',
            data: [{
                name: '可用保证金(%)',
                y: avaliableMargin,
                color: '#dff0d8',
                sliced: true,
                selected: true
            }, {
                name: '保证金占用(%)',
                y: 100 - avaliableMargin,
                color: 'rgb(217, 237, 247)',
                sliced: true,
                selected: true
            }]
        }]
    };
}

function updateAccountDetailChart(ObjChart, totalBalance) {
    var nowTime = new Date().getTime();
    var account = exchanges[0].GetAccount();
    try {
        if (account !== null && account.Info !== null && totalBalance > 0) {
            ObjChart.add([0, [nowTime, Number(totalBalance)]]);
        }
    } catch (err) {
        Log('ERROR ' + account + ',' + err)
    }
}

function getSpotBalanceInUSDT() {
    var ticker = JSON.parse(HttpQuery('https://api.binance.com/api/v1/ticker/24hr'));
    var currentBalance = 0;
    var account = exchanges[0].GetAccount();
    var priceMap = {};
    try {
        if (ticker !== null) {
            for (var index in ticker) {
                priceMap[ticker[index].symbol] = ticker[index].lastPrice;
            }
        }
        if (account !== null && account.Info !== null) {
            for (var index in account.Info.balances) {
                var obj = account.Info.balances[index];
                if (obj.asset !== 'USDT' && priceMap[obj.asset + 'USDT']) {
                    currentBalance += Number(Number(priceMap[obj.asset + 'USDT']) * Number((Number(obj.free) + Number(obj.locked))));
                }
                if (obj.asset === 'USDT') {
                    currentBalance += Number((Number(obj.free) + Number(obj.locked)));
                }
            }
        }
    } catch (err) {
        Log('ERROR ' + account + ',' + err)
    }
    Sleep(666);
    return Number(currentBalance).toFixed(6);
}

function printProfitInfo(currentBalance) {
    var profit = Number((currentBalance) - baseOriginalBalance).toFixed(5);
    var profitRate = Number((((currentBalance) - baseOriginalBalance) / baseOriginalBalance) * 100).toFixed(4);
    LogProfit(Number(profitRate), '&');
    Log('The current balance is ' + currentBalance + ', the profit is ' + profit + ', the profit rate is ' + profitRate + '%');
}

function printPositionInfo(exchangeInnerArray, totalProfitUSDT, totalProfitRate) {
    var totalProfit = 0.0
    var table = {
        type: 'table',
        title: 'POSITIONS',
        cols: ['Symbol', 'Type', 'CurrentPrice', 'Position', 'USDT Value'],
        rows: []
    }
    table.rows.push([{
        body: '本策略是 USDT 本位，低风险现货智能动态参数网格',
        colspan: 5
    }]);
    table.rows.push([{
        body: '所有交易对任选',
        colspan: 5
    }]);
    var ticker = JSON.parse(HttpQuery('https://api.binance.com/api/v1/ticker/24hr'));
    var account = exchanges[0].GetAccount();
    var priceMap = {};
    try {
        if (ticker !== null) {
            for (var index in ticker) {
                priceMap[ticker[index].symbol] = ticker[index].lastPrice;
            }
        }
        if (account !== null && account.Info !== null) {
            for (var index in account.Info.balances) {
                var obj = account.Info.balances[index];
                if (obj.asset !== 'USDT' && priceMap[obj.asset + 'USDT']) {
                    if (Number((Number(obj.free) + Number(obj.locked))) > 0) {
                        table.rows.push([obj.asset, ('LONG #1eda1bab'), Number(priceMap[obj.asset + 'USDT']), Number((Number(obj.free) + Number(obj.locked))), Number(Number(priceMap[obj.asset + 'USDT']) * Number((Number(obj.free) + Number(obj.locked)))).toFixed(4)]);
                    }
                }
            }
        }
    } catch (err) {
        Log('ERROR ' + account + ',' + err)
    }
    Sleep(168);
    table.rows.push([{
        body: 'TOTAL PROFIT OF CURRENT POSITION',
        colspan: 4
    }, totalProfit.toFixed(6) + ' USDT']);
    table.rows.push([{
        body: 'TOTAL PROFIT',
        colspan: 4
    }, totalProfitUSDT + ' USDT']);
    table.rows.push([{
        body: 'TOTAL PROFIT RATE',
        colspan: 4
    }, totalProfitRate + ' %']);
    LogStatus('`' + JSON.stringify(table) + '`');
}

function main() {
    initChart();
    var ObjChart = Chart([chart, getChartPosition(100)]);
    while (true) {
        try {
            var currentSpotBalance = getSpotBalanceInUSDT();
            var totalBalance = Number(currentSpotBalance).toFixed(4);
            printProfitInfo(totalBalance);
            updateAccountDetailChart(ObjChart, totalBalance);
            for (var i = 0; i < 120; i++) {
                try {
                    var avaliableMargin = 100;
                    ObjChart.update([chart, getChartPosition(avaliableMargin)]);
                    var profit = Number((totalBalance) - baseOriginalBalance).toFixed(5);
                    var profitRate = Number((((totalBalance) - baseOriginalBalance) / baseOriginalBalance) * 100).toFixed(4);
                    printPositionInfo(exchanges, profit, profitRate);
                    Sleep(1000 * 120);
                } catch (errInner) {
                    throw errInner;
                }
            }
        } catch (err) {
            throw err;
        }
    }
}
```

> Detail

https://www.fmz.com/strategy/255606

> Last Modified

2021-02-20 11:36:38
