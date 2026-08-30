
> Name

Multi-platform futures funding rate acquisition and monitoring strategy multiple-thread-get-fundings-symbols
> Author

inventor quantification
> Strategy Description

[trans]

# Multi-platform futures funding rate acquisition and monitoring strategy
### Description:
This strategy is used to obtain and monitor funding rates from multiple futures platforms such as OKCoin, Binance, Bitget, etc. Parallel threads are used to poll the perpetual contract market of each exchange and obtain funding rate data, while using a delay mechanism to optimize the request frequency.
### Function:
- **Multi-Platform Support**: Synchronize funding rates for multiple trading platforms and set different request delays for each platform.
- **Specific symbol acquisition**: Supports obtaining the funding rate of specific trading pairs (such as BTC/USDT, ETH/USDT).
- **Optimize for different platforms**: Distinguish between platforms that do not need to query market by market (such as Binance) and platforms that need to traverse all markets (such as OKCoin).
### How to use:
You can adjust the platform list, symbol list and polling interval as needed to meet your specific trading needs.
||

# Multi-Platform Futures Funding Rate Retrieval and Monitoring Strategy

### Description:
This strategy retrieves and monitors funding rates across multiple futures platforms (e.g., OKCoin, Binance, Bitget). It uses parallel threads to poll the perpetual contract markets on various exchanges and retrieve funding rate data, with a delay mechanism to optimize request frequency.

### Features:
- **Multi-Platform Support**: Synchronizes funding rates from several trading platforms, each with customized request delays.
- **Symbol Specific Retrieval**: Allows retrieval of funding rates for specific trading pairs (e.g., BTC/USDT, ETH/USDT).
- **Optimized for Different Platforms**: Distinguishes between platforms that require iteration over individual markets (e.g., OKCoin) and those that do not (e.g., Binance).

### Usage:
You can adjust the platform list, symbol list, and polling intervals to suit your specific trading requirements.

[/trans]



> Source (javascript)

``` javascript

function startFundingWorker() {
    exchanges.forEach((_, pos) => {
        __Thread(function (pos) {
            let e = exchanges[pos]
            let eName = e.GetName()
            let delaySettings = {
                'Futures_OKCoin': 20,
                'Futures_Binance': 500,
            }
            let needInterate = ['Futures_OKCoin', 'Futures_Bitget','Futures_OKX', 'Futures_KuCoin', 'Futures_MEXC', 'Futures_Crypto', 'Futures_Deribit']
            let delay = function () {
                let n = delaySettings[eName]
                if (n) {
                    Sleep(n)
                }
            }
            let epoch = 60000*2;
            let ts = 0;
            let fundings = {}
            while (true) {
                let now = new Date().getTime()
                if (now - ts < epoch) {
                    Sleep(1000)
                    continue
                }
                let markets = e.GetMarkets()
                if (!markets) {
                    Sleep(1000)
                    continue
                }
                if (needInterate.includes(eName)) {
                    for (let symbol in markets) {
                        if (symbol.includes('.swap')) {
                            let ret = e.GetFundings(symbol)
                            if (ret) {
                                for (let r of ret) {
                                    fundings[r.Symbol] = r
                                }
                            }
                            delay();
                        }
                    }
                } else {
                    let zones = []
                    for (let symbol in markets) {
                        if (symbol.includes('.swap') && !zones.includes(markets[symbol].QuoteAsset)) {
                            zones.push(markets[symbol].QuoteAsset)
                            let ret = e.GetFundings(markets[symbol].QuoteAsset + '.swap')
                            if (ret) {
                                for (let r of ret) {
                                    fundings[r.Symbol] = r
                                }
                            }
                            delay();
                        }
                    }
                }
                ts = now
                __threadSetData(0, eName+"_funding", fundings)
            }
        }, pos)
    })
}

function getFundings(eName, symbols) {
    let fundings = __threadGetData(0, eName+"_funding")
    if (!fundings) {
        return null
    }

    if (typeof(symbols) === 'undefined') {
        return fundings
    }

    let ret = {}
    symbols.forEach((s) => {
        if (fundings[s]) {
            ret[s] = fundings[s]
        }
    })
    return ret
}

function main() {
    startFundingWorker()
    while (true) {
        exchanges.forEach((e) => {
            let eName = e.GetName()
            let fundings = getFundings(eName, ['BTC_USDT.swap', 'ETH_USDT.swap'])
            Log(eName, fundings)
        })
        Sleep(5000)
    }
}
```

> Detail

https://www.fmz.com/strategy/470345

> Last Modified

2024-10-24 18:36:42
