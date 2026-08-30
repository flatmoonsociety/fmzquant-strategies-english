
> Name

Native multi-threaded JavaScript and WASM performance comparison
> Author

inventor quantification
> Strategy Description


The inventor quantitatively tried to make Javascript support real multi-threading from the native low-level, and added the WASM function. Below is a DEMO. Download the latest host to try it out.
This function is not a Worker function of Javascript. It can be used to communicate with each other within multiple threads or with the main thread.
C language to wasm can generate tests from this website: https://wasdk.github.io/WasmFiddle/

The C language code compiled into wasm is as follows
```
int fib(int f) {
  if (f < 2) return f;
  return fib(f - 1) + fib(f - 2);
}
```

After compilation, download the wasm file and convert it to a hex string using python
```
python -c "print('data:hex,'+bytes.hex(open('program.wasm','rb').read()))"
```

Just replace the content behind the variable in the code
> __Thread(function, arguments...)

Create a thread and return the thread tid. The functions of the accepted thread body function must complete all function codes within the thread function. References to other closure functions are not supported. All APIs of the platform can be called within the thread, but other user-defined functions cannot be called.
Simple example:
```
let tid = __Thread(function(x, y) {
    return x + y
}, 1, 2)
Log(__threadJoin(tid))
```

Example of multi-threaded request:
```
function main() {
    let threads = [
        "https://www.baidu.com",
        "https://www.163.com"
    ].map(function(url) {
        return __Thread(function(url) {
            Log("GET", url)
            return HttpQuery(url)
        }, url)
    })
    threads.forEach(function(tid) {
        Log(__threadJoin(tid))
    })
}
```

> Thread local storage variables
Supports thread local storage variables. To facilitate data sharing, the data is valid when the thread is not `__threadJoin` waiting for exit success or `__threadTerminate` to terminate
```
__threadGetData(tid, key)
__threadSetData(tid, key, value)
```

If tid is 0, it means the current thread. If value is not specified, it means deleting the key. It supports mutual access of shared variables between threads. The value must be a serializable variable.
> Thread communication
```
__threadPostMessage(tid, msg) // 向指定线程发送消息, tid为0是向主线程即当前主函数发送, 在线程内部调用指向主线程回复消息, 该消息可以被EventLoop捕获
__threadPeekMessage(tid, timeout) // 从指定线程接收消息, 如果不指定timeout(毫秒)就一直等待, tid为0指等待主线程的消息
```

> __threadJoin(tid, timeout)

Wait for the thread to end. Specify timeout (milliseconds) to specify the waiting timeout. You can not specify it, just wait until the thread ends. Successfully returns a structure containing the function return value and recycles resources. The structure is as follows
```
{
    id: tid, // 线程id
    elapsed: 1111, // 线程的运行时间(纳秒)
    terminated: false, // 线程是否被强制结束 
    ret: 123, // 线程函数的返回值
}
```
If timeout returns undefined    
    
> __threadTerminate(tid)

Forcefully end the thread and recycle resources (you can no longer use __threadJoin to wait for the end)    
> Note
The __Thread function does not support referencing variables outside the function (running as an isolated environment). Referring to external variables will cause compilation failure.





> Source (javascript)

``` javascript
function main() {
    let cycle = 100
    let input = 30
    let threads = [
        __Thread(function(cycle, input) {
            function fib(f) {
                if (f < 2) return f
                return fib(f - 1) + fib(f - 2)
            }
            let ret = 0
            for (let i = 0; i < cycle; i++) {
                ret = fib(input);
                Log("javascript progress: ", i)
            }
            return 'javascript fib: ' + ret
        }, cycle, input),
        
        __Thread(function(cycle, input) {
            let data = 'data:hex,0061736d010000000186808080000160017f017f0382808080000100048480808000017000000583808080000100010681808080000007908080800002066d656d6f727902000366696200000aa480808000019e80808000000240200041024e0d0020000f0b2000417f6a10002000417e6a10006a0b'
            let m = wasm.parseModule(data)

            let instance = wasm.buildInstance(m, {
                stack_size: 65 * 1024 * 1024,
            })

            let ret = 0
            for (let i = 0; i < cycle; i++) {
                ret = instance.callFunction('fib', input)
                Log("wasm progress: ", i)
            }

            return 'wasm fib: ' + ret
        }, cycle, input)
    ]

    threads.forEach(function(tid) {
        let info = __threadJoin(tid)
        Log('#'+tid, info.ret, 'elapsed:', info.elapsed / 1e6, "#ff0000")
    })
}
```

> Detail

https://www.fmz.com/strategy/401463

> Last Modified

2023-03-03 03:42:24
