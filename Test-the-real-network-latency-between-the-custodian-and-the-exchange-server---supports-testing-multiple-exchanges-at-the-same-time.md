
> Name

Test the real network latency between the custodian and the exchange server - supports testing multiple exchanges at the same time
> Author

Xueqiu Bot

> Strategy Description

Contact: ck@xueqiubot.com / WeChat@stay37
This strategy is to test the real network delay between the host and the server. The test method is: compare the time of sending the request and the time of receiving the result, and average it multiple times. 
Supports simultaneous testing of multiple exchanges, just add different trading platforms, and the numpy module needs to be installed.


> Source (python)

``` python
# Contact : ck@xueqiubot.com / WeChat@stay37

import time
import numpy as np


def test():
    #延迟数据接收器
    delay_list = []
    for i in range(len(exchanges)):
        delay_list.append([])
    while True:
        #延迟数据获取
        for i in range(len(exchanges)):
            send_t = time.time()
            ticker = exchanges[i].GetTicker()
            delay_list[i].append(round((time.time() - send_t) * 1000 , 2))
        #数据输出 
        delay_table = {"type":'table',"title":'延迟数据',"cols": ['账号序号','最近一次延迟','平均延迟','已测试次数'],"rows":[]}
        for i in range(len(delay_list)):
            delay_table['rows'].append([i + 1, str(delay_list[i][-1])+' ms', str(round(np.mean(delay_list[i]) , 2)) + ' ms', len(delay_list[i])])
        LogStatus("输出的延迟为：发送一次get_ticker请求到获取到数据的真实时间" + "\n" + "`" + json.dumps(delay_table) + "`")
        time.sleep(0.05)

                
def main():
    for i in range(len(exchanges)):
        exchanges[i].SetContractType('swap')
    test()
                

```

> Detail

https://www.fmz.com/strategy/236426

> Last Modified

2021-01-10 19:22:52
