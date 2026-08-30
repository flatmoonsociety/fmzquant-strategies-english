
> Name

Fixed investment strategy
> Author

Balala little magic fairy
> Strategy Description

## Strategy description
There is a saying in stocks: Novices die from chasing highs, and veterans die from buying lows. What matters is timing. If you are not careful, you will get stuck. Therefore, many strategies will make some trend predictions and adjust positions according to the trend.
As for the fixed investment strategy, that is, the investment strategy with a fixed amount on a regular basis, the fundamental core is - buy low and sell high, and buy more as the price falls, rather than chasing the rise and killing the fall. Therefore, for the fixed investment strategy, you can think that you can buy it at any time.
Formulating an effective fixed investment strategy can greatly increase the income of fixed investment. Before making a fixed investment, we should put our plan on paper, implement it according to the plan, reduce human intervention, stick to it, stop profits and stop losses, so that we can truly appreciate the value of fixed investment.
Here we limit the scope of operations to control risks and formulate the following strategic rules:
Fixed investment of 1 short lot per minute with 20 times leverage.
For unclosed positions, if the loss exceeds 3%, continue to invest. If the profit exceeds 3%, 2 positions will be closed every minute
Among them, in the test script, the fixed investment period, fixed investment quantity, leverage multiple, profit and loss ratio, and position direction are configurable items.

## Contact information
 If you are interested in this strategy, please +V: Irene11229
(Click on my homepage, I will continue to update more strategies, and you can also get market analysis data of several leading exchanges)



> Source (python)

``` python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
import json
import time

from kumex.client import Trade


class Aip(object):

    def __init__(self):
        # read configuration from json file
        with open('config.json', 'r') as file:
            config = json.load(file)

        self.api_key = config['api_key']
        self.api_secret = config['api_secret']
        self.api_passphrase = config['api_passphrase']
        self.sandbox = config['is_sandbox']
        self.symbol = config['symbol']
        self.timer = int(config['timer'])
        self.size = int(config['size'])
        self.side = config['side']
        self.leverage = config['leverage']
        self.rate = float(config['rate'])
        self.trade = Trade(self.api_key, self.api_secret, self.api_passphrase, is_sandbox=self.sandbox)
        if self.side == 'sell':
            self.close = 'buy'
        else:
            self.close = 'sell'

    def get_position_pcnt(self):
        position = self.trade.get_position_details(self.symbol)
        return float(position['unrealisedPnlPcnt'])


if __name__ == '__main__':
    aip = Aip()
    market_order = aip.trade.create_market_order(aip.symbol, aip.side, aip.leverage, type='market', size=aip.size)
    print('create a market %s order, order id = %s' % (aip.side, market_order['orderId']))
    while 1:
        time.sleep(aip.timer * 60)
        pcnt = aip.get_position_pcnt()
        if pcnt < 0 and abs(pcnt) > aip.rate:
            market_order = aip.trade.create_market_order(aip.symbol, aip.side, aip.leverage,
                                                         type='market', size=aip.size)
            print('create a market %s order, order id = %s' % (aip.side, market_order['orderId']))
        elif pcnt > 0 and pcnt > aip.rate:
            market_order = aip.trade.create_market_order(aip.symbol, aip.close, aip.leverage,
                                                         type='market', size=(aip.size*2))
            print('create a market %s order, order id = %s' % (aip.close, market_order['orderId']))

```

> Detail

https://www.fmz.com/strategy/207710

> Last Modified

2021-03-04 10:13:37
