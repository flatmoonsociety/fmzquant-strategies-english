
> Name

Telegram-sending interface-V200-Python
> Author

FawkesPan

> Strategy Description

# Telegram API interface (FMZ.com)
##### This library can currently only send messages through Telegram. More functions will be added in the future.
### Initialization
```
# key 为 Bot key
## 获取 Bot key 可以参考 https://www.ccino.org/create-a-telegram-bot.html
# chat_id 为收信用户Telegram ID
## Telegram ID 可以通过 @dwx_aibot 机器人获取， 连接至此机器人后发送 /getid 即可获得 ChatID
Telegram = ext.Telegram(key=string, chat_id=integer)    # 创建一个新的接口对象
```
### Send message
```
# chat_id 为可选项 默认会使用初始化时设置的ChatID
# message 即为信息内容
Telegram.Send(message=string, chat_id=integer)
```
### Notes
Before you can send a message to yourself, you need to send a /start message to your robot in Telegram, otherwise the robot will not be able to send you a message.
### Contact me
Email i@fawkex.me
Telegram [FawkesPan](https://telegram.me/FawkesPan)
Accept policy customization
### About this library
[Telegram API Documentation](https://core.telegram.org/bots/api)
[Use WTFPL – Do What the Fuck You Want to Public License](http://www.wtfpl.net/)
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|DEBUG|0|DEBUG mode: 0|1|
|KEY||Telegram robot Key|
|CHATID|false|Telegram session ID|

> Source (python)

``` python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
# encoding: utf-8
# 
# Telegram Interface for FMZ.com
#
# Copyright 2018 FawkesPan
# Contact : i@fawkex.me / Telegram@FawkesPan
#
# Do What the Fuck You Want To Public License
#

try:
    import requests
except:
    print('Requests not installed. Try: pip install requests')
    Log('Requests not installed. Try: pip install requests')
    
    raise Exception('Requests not installed. Try: pip install requests')

class Telegram:
    def __init__(self):
        self.key = KEY
        self.chat_id = CHATID
        self.url = 'https://api.telegram.org/bot%s' % self.key
        
    def Send(self, message='', chat_id=None):
        if chat_id is None:
            chat_id = self.chat_id
        PARAM = {}
        PARAM['chat_id'] = chat_id
        PARAM['text'] = message
        PARAM['parse_mode'] = 'markdown'
        URL = self.url + '/sendMessage'
        try:
            res = requests.post(URL, data = PARAM)
            return True
        except IOError as e:
            print(e)
            return False
        

ext.Telegram = Telegram

# 模块功能测试
def main():
    if DEBUG == 1:
        msger = ext.Telegram(KEY, CHATID)
        msger.Send("Hello World!")
    
    return True
```

> Detail

https://www.fmz.com/strategy/116201

> Last Modified

2019-05-16 20:06:03
