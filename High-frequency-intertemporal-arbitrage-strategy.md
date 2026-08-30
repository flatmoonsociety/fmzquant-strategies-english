
> Name

High frequency intertemporal arbitrage strategy
> Author

Balala little magic fairy
> Strategy Description

## Strategy Description
Transaction object: Bitcoin (BTC)
Spread data: BTC Perpetual - BTC Quarterly (cointegration test omitted)
Transaction period: 1 minute
Position matching: 1:1
Transaction type: Intertemporal of the same variety
Conditions for opening a long spread position: If the current account has no positions and the spread is < (long-term spread level - threshold), go long the spread. That is: buy BTC perpetually and sell BTC quarterly.
Conditions for opening a short spread position: If the current account has no positions and spread > (long-term spread level + threshold), short the spread. That is: sell BTC perpetually and buy BTC quarterly.
Conditions for closing long spread positions: If the current account holds BTC perpetual long orders and holds BTC quarterly short orders, and the spread > the long-term spread level, the long spread will be closed. That is: sell flat BTC perpetually and buy flat BTC quarterly.
Short spread closing conditions: If the current account holds a BTC perpetual short order and holds a BTC quarterly long order, and the spread is < the long-term spread level, the spread will be closed. That is: buy BTC permanently and sell BTC quarterly.
**For example**, assume that the price difference between BTC perpetual and BTC for the current quarter remains around 35 for a long time. If the spread reaches 50 on a given day, we would expect the spread to return to 35 and below at some point in the future. Then you can sell BTC permanently and buy BTC quarterly to short the price difference. Vice versa, note that the price difference between BTC Perpetual and BTC Quarterly will always return to near 0 (delivery at maturity), so when the price difference is positive, priority is given to shorting the price difference, and when the price difference is negative, priority is given to longing the price difference.
## Contact information
:point_right: If you are interested in this strategy, please +V: Irene11229
(Click on my homepage, I will continue to update more strategies, and you can also get market analysis data of several leading exchanges)




> Source (python)

``` python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import json
import time

from kumex.client import Trade, Market


class Hf(object):

    def __init__(self):
        # read configuration from json file
        with open('config.json', 'r') as file:
            config = json.load(file)

        self.api_key = config['api_key']
        self.api_secret = config['api_secret']
        self.api_passphrase = config['api_passphrase']
        self.sandbox = config['is_sandbox']
        self.symbol_a = config['symbol_a']
        self.symbol_b = config['symbol_b']
        self.spread_mean = float(config['spread_mean'])
        self.leverage = float(config['leverage'])
        self.size = int(config['size'])
        self.num_param = float(config['num_param'])
        self.trade = Trade(self.api_key, self.api_secret, self.api_passphrase, is_sandbox=self.sandbox)
        self.market = Market(self.api_key, self.api_secret, self.api_passphrase, is_sandbox=self.sandbox)

    def get_symbol_price(self, symbol):
        ticker = self.market.get_ticker(symbol)
        return float(ticker['price'])


if __name__ == '__main__':
    hf = Hf()
    while 1:
        # ticker of symbols
        price_af = hf.get_symbol_price(hf.symbol_a)
        price_bf = hf.get_symbol_price(hf.symbol_b)
        # position of symbols
        position_a = hf.trade.get_position_details(hf.symbol_a)
        position_a_qty = int(position_a['currentQty'])
        position_b = hf.trade.get_position_details(hf.symbol_b)
        position_b_qty = int(position_b['currentQty'])
        # interval of price
        new_spread = price_af - price_bf
        print('new_spread =', new_spread)

        if position_a_qty == position_b_qty == 0 and new_spread < (hf.spread_mean - hf.num_param):
            buy_order = hf.trade.create_limit_order(hf.symbol_a, 'buy', hf.leverage, hf.size, price_af + 1)
            print('buy %s,order id =%s' % (hf.symbol_a, buy_order['orderId']))
            sell_order = hf.trade.create_limit_order(hf.symbol_b, 'sell', hf.leverage, hf.size, price_bf - 1)
            print('sell %s,order id =%s' % (hf.symbol_b, sell_order['orderId']))
        elif position_a_qty == position_b_qty == 0 and new_spread > (hf.spread_mean + hf.num_param):
            buy_order = hf.trade.create_limit_order(hf.symbol_a, 'sell', hf.leverage, hf.size, price_af - 1)
            print('sell %s,order id =%s' % (hf.symbol_a, buy_order['orderId']))
            sell_order = hf.trade.create_limit_order(hf.symbol_b, 'buy', hf.leverage, hf.size, price_bf + 1)
            print('buy %s,order id =%s' % (hf.symbol_b, sell_order['orderId']))
        elif position_a_qty > 0 and position_b_qty < 0 and new_spread > hf.spread_mean:
            buy_order = hf.trade.create_limit_order(hf.symbol_a, 'sell', position_a['realLeverage'],
                                                    position_a_qty, price_af + 1)
            print('sell %s,order id =%s' % (hf.symbol_a, buy_order['orderId']))
            sell_order = hf.trade.create_limit_order(hf.symbol_b, 'buy', position_a['realLeverage'],
                                                     position_a_qty, price_bf - 1)
            print('buy %s,order id =%s' % (hf.symbol_b, sell_order['orderId']))
        elif position_a_qty < 0 and position_b_qty > 0 and new_spread < hf.spread_mean:
            buy_order = hf.trade.create_limit_order(hf.symbol_a, 'buy', position_a['realLeverage'],
                                                    position_a_qty, price_af - 1)
            print('buy %s,order id =%s' % (hf.symbol_a, buy_order['orderId']))
            sell_order = hf.trade.create_limit_order(hf.symbol_b, 'sell', position_a['realLeverage'],
                                                     position_a_qty, price_bf + 1)
            print('sell %s,order id =%s' % (hf.symbol_b, sell_order['orderId']))

        time.sleep(60)
```

> Detail

https://www.fmz.com/strategy/207009

> Last Modified

2021-03-04 10:13:06
