
> Name

Leek protection program Tang Anqi channel position balancing strategy
> Author

Go to Boren
> Strategy Description

Applicable to all cash currencies
In fact, what you are eating is the bull market dividend. The function of the strategy is only to reduce the retracement and avoid the plunge.
Latest backtest results: successfully escaped the plunge, and ended up short on 4.22
![](https://www.fmz.com![IMG](https://www.fmz.com/upload/asset/11b300fd2690d0eec7869.png) )
Usage requirements: 1% of your funds must be able to purchase the minimum trading unit of the currency
![](https://www.fmz.com![IMG](https://www.fmz.com/upload/asset/11b032bdb578ffad9a820.png))
The boss who makes money is welcome to reward me with a cup of milk tea.
![](https://www.fmz.com![IMG](https://www.fmz.com/upload/asset/11c58db65dd31bc41a6c5.jpg))



> Source (python)

``` python
'''backtest
start: 2021-04-01 00:00:00
end: 2021-04-30 23:59:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Binance","currency":"ETH_USDT","stocks":0}]
'''

import time
class juncang_strategy():  
    def __init__(self,exchange):
        self.p = 0.5
        self.account = None
        self.cny = 0
        self.btc = 0
        self.exchange =exchange
    
    #K线合成函数
    def k_compose(self,Recordlist,num):
        newRecordlist = []
        for i in range(len(Recordlist)):
            if (i+1)%num == 1:
                tempk = {}
                tempk["Time"]=Recordlist[i]["Time"]
                tempk["Open"]=Recordlist[i]["Open"]
                tempk["High"]=Recordlist[i]["High"]
                tempk["Low"]=Recordlist[i]["Low"]
                tempk["Close"]=Recordlist[i]["Close"]
                tempk["Volume"]=Recordlist[i]["Volume"]
                newRecordlist.append(tempk)
            elif (i+1)%num == 0:
                if Recordlist[i]["High"]>tempk["High"]:
                    tempk["High"] = Recordlist[i]["High"]
                if Recordlist[i]["Low"]<tempk["Low"]:
                    tempk["Low"] = Recordlist[i]["Low"]
                tempk["Time"]=Recordlist[i]["Time"]
                tempk["Close"]=Recordlist[i]["Close"]
                tempk["Volume"]=tempk["Volume"]+Recordlist[i]["Volume"]
                del(newRecordlist[-1])
                newRecordlist.append(tempk)
            else:
                if Recordlist[i]["High"]>tempk["High"]:
                    tempk["High"] = Recordlist[i]["High"]
                if Recordlist[i]["Low"]<tempk["Low"]:
                    tempk["Low"] = Recordlist[i]["Low"]
                del(newRecordlist[-1])
                newRecordlist.append(tempk)
        return newRecordlist

    #唐安奇通道计算，分析出当前什么行情
    def donchian(self):
        exchange.SetMaxBarLen(2000)
        temp_k = _C(self.exchange.GetRecords,PERIOD_D1)
        week_kline = self.k_compose(temp_k,7)
        rt=False
        # Log(len(week_kline),week_kline[-1]["High"],TA.Highest(week_kline, 20, 'High'))
        if len(week_kline)>20:
            if week_kline[-1]["High"]>TA.Highest(week_kline, 20, 'High'):
                rt = '全仓'
            elif week_kline[-1]["High"]<TA.Highest(week_kline, 20, 'High') and week_kline[-1]["Low"]>TA.MA(week_kline, 10)[-1]:
                rt = '均仓'
            elif week_kline[-1]["Low"]<TA.MA(week_kline, 10)[-1]:
                rt = '空仓'
        else:
            rt = '均仓'
        return rt
    def cancelAllOrders(self):
        orders = self.exchange.GetOrders()
        for order in orders:
            self.exchange.CancelOrder(order['Id'], order)
        return True
    #全仓买入函数
    def allin(self):
        kr =  _C(self.exchange.GetRecords,PERIOD_H1)
        account = _C(self.exchange.GetAccount)
        self.cny = account.Balance
        buynum=_N(self.cny*0.99/kr[-1].Close,3)
        if buynum>0:
            Log("全仓allin")
            self.exchange.Buy(kr[-1].Close,buynum)
        
    #全仓卖出函数
    def allout(self):
        kr =  _C(self.exchange.GetRecords,PERIOD_H1)
        account = _C(self.exchange.GetAccount)
        self.btc = _N(account.Stocks,3)
        if self.btc>0:
            Log("空仓allout")
            self.exchange.Sell(kr[-1].Close,self.btc)
    #均仓函数
    def balanceAccount(self):
        kr =  _C(self.exchange.GetRecords,PERIOD_H1)
        account = _C(self.exchange.GetAccount)
        if account is None:
            return

        #赋值
        self.account = account

        #赋值
        self.btc = account.Stocks
        self.cny = account.Balance
        
        accountmoney=self.btc * kr[-1].Close + self.cny
        self.p = self.btc * kr[-1].Close / accountmoney
        tradenum=_N(accountmoney/kr[-1].Close/100,3)
        if tradenum<0.001:
            tradenum=0.001
        #判断self.p的值是否小于0.48
        # Log(self.p)
        if (0.45<self.p < 0.49):
            #调用Log函数并传入参数"开始平衡", self.p
            Log("开始平衡", self.p)

            self.exchange.Buy(kr[-1].Close, tradenum)

            Log("持币数:",self.btc,"现金数:",self.cny)

            #判断self.p的值是否大于0.52
        elif (0.55 > self.p > 0.51):
            #调用Log函数并传入参数"开始平衡", self.p
            Log("开始平衡", self.p)

            #调用Sell函数并传入相应的参数
            self.exchange.Sell(kr[-1].Close, tradenum)

            Log("持币数:",self.btc,"现金数:",self.cny)
        elif (self.p >= 0.55):
            #调用Log函数并传入参数"开始平衡", self.p
            Log("开始平衡,快速平仓", self.p)

            self.exchange.Sell(kr[-1].Close, _N(tradenum*10,3))

            Log("持币数:",self.btc,"现金数:",self.cny)
        elif (self.p <= 0.45):
            #调用Log函数并传入参数"开始平衡", self.p
            Log("开始平衡，快速建仓", self.p)

            self.exchange.Buy(kr[-1].Close, _N(tradenum*10,3))

            Log("持币数:",self.btc,"现金数:",self.cny)
    #交易循环
    def loop(self):
        self.cancelAllOrders()
        rt=self.donchian()
        if rt=='全仓':
            self.allin()
        elif rt=='均仓':
            self.balanceAccount()
        else:
            self.allout()
        Sleep(1000*60)




#函数main
def main():
    #reaper 是构造函数的实例
    reaper = juncang_strategy(exchange)
    while (True):
        reaper.loop()

```

> Detail

https://www.fmz.com/strategy/271523

> Last Modified

2021-07-20 17:27:39
