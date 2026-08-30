
> Name

Take-profit and stop-loss integrated libraries of three major exchanges
> Author

LiteFly

> Strategy Description

The fmz platform does not have a take-profit and stop-loss function. When you need to set a take-profit and stop-loss, you need to call other functional interfaces of the exchange. The take-profit and stop-loss settings of different exchanges are different, so the following packaging is made.
The function of stop-profit and stop-loss is particularly important. It avoids high handling fees without triggering by market price, and also avoids the possibility of being liquidated in extreme circumstances.
The function takes into account isolated and full positions, as well as the situation of U-standard currency standard.



> Source (python)

``` python
import json

# 对合约进行止盈止损   cangType=0默认逐仓  =1全仓
def zhiyingzhisun(ex, amount, directionStr, zhiying, zhisun, cangType = 0):
    if ex.GetName().find('OK') >= 0 :
        # okex
        return okexSwap(ex, amount, directionStr, zhiying, zhisun)
    elif ex.GetName().find('Huobi') >= 0 :
        # huobi
        return huobiSwap(ex, amount, directionStr, zhiying, zhisun, cangType)
    elif ex.GetName().find('Binance') >= 0 :
        # bian
        return bianSwap(ex, amount, directionStr, zhiying, zhisun)
    else:
        return False

# 发送请求
def AsynIo(ex, paramList):
        if (len(paramList) == 3):
            arrRoutine = ex.Go("IO", paramList[0], paramList[1], paramList[2])
        elif (len(paramList) == 4):
            arrRoutine = ex.Go("IO", paramList[0], paramList[1], paramList[2], paramList[3])
        elif (len(paramList) == 5):
            arrRoutine = ex.Go("IO", paramList[0], paramList[1], paramList[2], paramList[3], paramList[4])
        data, ok = arrRoutine.wait()
        return data
# 火币合约
def huobiSwap(ex, amount, directionStr, zhiying, zhisun, cangType):
    instrument_id = ex.GetCurrency().replace('_',"-")
    # 根据全仓或逐仓 与 U本位或币本位，设置请求url
    if instrument_id.find('USDT') >= 0 :
        if cangType == 0:
            url = "/linear-swap-api/v1/swap_tpsl_order"
        elif cangType == 1:
            url = '/linear-swap-api/v1/swap_cross_tpsl_order'
        else:
            return False
    elif instrument_id.find('USD') >= 0 :
        url = "/swap-api/v1/swap_tpsl_order"
    else:
        return False
    # 发送请求
    data = AsynIo(ex, ['api', 'POST', url, '', json.dumps({
        "contract_code": instrument_id,
        "direction": directionStr,
        "volume" : amount,
        "tp_order_price": zhiying,
        "tp_trigger_price": zhiying,
        "sl_trigger_price": zhisun,
        "sl_order_price": zhisun,
    })])
    if data["status"] == 'ok':
        return True
    else:
        return False

# 币安合约
def bianSwap(ex, amount, directionStr, zhiying, zhisun):
    instrument_id = ex.GetCurrency().replace('_',"")
    # U本位或币本位，设置请求url
    if instrument_id.find('USDT') >= 0 :
        url = "/fapi/v1/order"
    elif instrument_id.find('USD') >= 0 :
        url = '/dapi/v1/order'
    else:
        return False
    # 止损
    zhisunData = AsynIo(ex, ['api', 'POST', url , '', json.dumps({
        "symbol": instrument_id,
        "side": directionStr,
        "type": "STOP",
        "quantity": amount,
        "price": zhisun,
        "stopPrice": zhisun,
        "timestamp": str(int(round(time.time() * 1000)))
    })])
    if int(zhisunData['stopPrice']) != int(zhisun):
        return False
    # 止盈
    zhiyingData = AsynIo(ex, ['api', 'POST', url , '', json.dumps({
        "symbol": instrument_id,
        "side": direction,
        "type": "TAKE_PROFIT",
        "quantity": amount,
        "price": zhiying,
        "stopPrice": zhiying,
        "timestamp": str(int(round(time.time() * 1000)))
    })])
    if int(zhiyingData['stopPrice']) != int(zhiying):
        return False
    return True


# 欧易合约
def okexSwap(ex, amount, directionStr, zhiying, zhisun):
    instrument_id = ex.GetCurrency().replace('_',"-") + '-SWAP'
    # 获取仓位方向
    if directionStr == 'buy':
        direction = '4'
    elif directionStr == 'sell':
        direction = '3'
    else:
        return False
    data =  AsynIo(ex, ['api', 'POST', '/v1/order/orders/place', '', json.dumps({
        "instrument_id": instrument_id,
        "type": direction,
        "order_type": '5',
        "size": amount,
        "tp_trigger_price": zhiying,
        "tp_price": zhiying,
        "sl_trigger_price": zhisun,
        "sl_price": zhisun
    })])
    if data["error_code"] == "0":
        return True
    else:
        return False
    
ext.zhiyingzhisun = zhiyingzhisun
```

> Detail

https://www.fmz.com/strategy/261634

> Last Modified

2021-03-19 10:08:13
