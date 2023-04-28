# MCQTSS Subscribe ToolBox Project Api接口文档

## 当前服务器域名:toolboxproject.api.nmsl.life

### 本文档中Python演示代码使用`Python3.9` HTTP请求模块使用`requests`请先前往[Python官网](https://www.python.org/downloads/release/python-3913/)下载Python3.9后执行下面命令安装`requests`

``` python -m pip install requests ```

### 易语言演示代码使用`易语言5.9`并使用了`精易模块`内的部分功能,请先导入`精易模块`([点我前往官网下载](https://ec.125.la/))

## 如何获取ApiKey

### 请在管理端-其他管理中找到ApiKey设置,然后点击生成新ApiKey即可生成一个新的ApiKey

### 注意!请不要将ApiKey泄露给他人以及生成新的ApiKey会删除当前账户之前生成的全部ApiKey

## ApiKey验证

### 此Api用于查看ApiKey状态

### 需提交信息:ApiKey

### 返回:ApiKey是否存在,所属ToolBoxID,所属用户等

### 接口:`/api/open/apikey_verify`

### Python代码:

``` 
import requests

api_url = 'toolboxproject.api.nmsl.life'
ApiKey = '你的ApiKey'
# 推荐请求写法(POST)
resp = requests.post(url='http://{}/api/open/apikey_verify'.format(api_url),
                     data={'apikey': ApiKey})
# 请求方法2(GET)
# resp = requests.get(url='http://{}/api/open/apikey_verify?apikey={}'.format(api_url, ApiKey))
if resp.json()['code'] not in [0, 1]:
    print('访问接口时发送错误\n错误码:{}\n错误信息:{}'.format(resp.json()['code'], resp.json()['message']))
    exit()
if resp.json()['code'] == 0:
    print('ApiKey信息获取成功:\n所属用户名:{}\nToolBoxID:{}'.format(resp.json()['username'], resp.json()['toolbox_id']))
else:
    print('ApiKey不存在')
 ```

### 易语言代码:

```
.版本 2

.子程序 获取ApiKey信息, 文本型
.参数 ApiKey, 文本型
.局部变量 resp, 文本型

resp ＝ 到文本 (网页_访问S (“http://toolboxproject.api.nmsl.life/api/open/apikey_verify”, 1, “apikey=” ＋ ApiKey))
返回 (resp)
 ```

## 获取卡密信息

### 此Api用于查看卡密相关信息

### 需提交信息:ApiKey,卡密

### 返回:过期时间,状态,上次登录时间,激活的时间,版本,卡密时间(比如永久,一个月等),机器码,所属工具箱ID,用户IP信息

### 接口:`api/open/get_card_info`

### Python代码:

```
import requests

api_url = 'toolboxproject.api.nmsl.life'
ApiKey = '你的ApiKey'
card = '你要查询的卡密'
# 推荐请求写法(POST)
resp = requests.post(url='http://{}/api/open/get_card_info'.format(api_url),
                     data={'apikey': ApiKey,
                           'card': card})
# 请求方法2(GET)
# resp = requests.get(url='http://{}/api/open/get_card_info?apikey={}&card={}'.format(api_url, ApiKey,card ))
if resp.json()['code'] not in [0, 1]:
    print('访问接口时发送错误\n错误码:{}\n错误信息:{}'.format(resp.json()['code'], resp.json()['message']))
    exit()
if resp.json()['code'] == 0:
    print(
        '卡密信息获取成功:\n过期时间:{}\n状态:{}\n上次登录时间:{}\n激活时间:{}\n上次登录版本:{}\n卡密时间:{}\n机器码:{}\n所属ToolBoxID:{}\nIP信息:{}'.format(
            resp.json()['info']['exp'], resp.json()['info']['state'], resp.json()['info']['login_time'],
            resp.json()['info']['act_time'], resp.json()['info']['version'],
            resp.json()['info']['card_time'], resp.json()['info']['machine_code'], resp.json()['info']['toolbox_id'],
            resp.json()['info']['ipinfo']))
```

### 易语言代码:

```
.版本 2

.子程序 获取卡密信息, 文本型
.参数 ApiKey, 文本型
.参数 卡密, 文本型
.局部变量 resp, 文本型

resp ＝ 到文本 (网页_访问S (“http://toolboxproject.api.nmsl.life/api/open/get_card_info”, 1, “apikey=” ＋ ApiKey ＋ “&card=” ＋ 卡密))
返回 (resp)
```

## 新增卡密

### 此Api用于新增卡密 注意!卡密时间按秒计算,比如一个月2626560秒,如果要新增永久的卡密卡密时间请填写-1

### 需提交信息:ApiKey,要新增的卡密,卡密时间

### 返回:是否成功

### 接口:`api/open/add_card`

### Python代码:

```
import requests

api_url = 'toolboxproject.api.nmsl.life'
ApiKey = '你的ApiKey'
card = '你要新增的卡密'
card_time = -1  # 写你自己想写的卡密时间,Int
# 推荐请求写法(POST)
resp = requests.post(url='http://{}/api/open/add_card'.format(api_url),
                     data={'apikey': ApiKey,
                           'card': card,
                           'card_time': card_time})
# 请求方法2(GET)
# resp = requests.get(url='http://{}/api/open/add_card?apikey={}&card={}&card_time={}'.format(api_url, ApiKey, card, card_time))
if resp.json()['code'] not in [0, 1]:
    print('访问接口时发送错误\n错误码:{}\n错误信息:{}'.format(resp.json()['code'], resp.json()['message']))
    exit()
if resp.json()['code'] == 0:
    print(resp.json()['message'])
```

### 易语言代码:

```
.版本 2

.子程序 新增卡密, 文本型
.参数 ApiKey, 文本型
.参数 卡密, 文本型
.参数 卡密时间, 整数型
.局部变量 resp, 文本型

resp ＝ 到文本 (网页_访问S (“http://toolboxproject.api.nmsl.life/api/open/add_card”, 1, “apikey=” ＋ ApiKey ＋ “&card=” ＋ 卡密 ＋ “&card_time=” ＋ 到文本 (卡密时间)))
返回 (resp)
```

## 删除卡密

### 此Api用于删除卡密 注意!删除后不可恢复

### 需提交信息:ApiKey,要删除的卡密

### 返回:是否成功

### 接口:`api/open/del_card`

### Python代码:

```
import requests

api_url = 'toolboxproject.api.nmsl.life'
ApiKey = '你的ApiKey'
card = '你要新增的卡密'
# 推荐请求写法(POST)
resp = requests.post(url='http://{}/api/open/del_card'.format(api_url),
                     data={'apikey': ApiKey,
                           'card': card})
# 请求方法2(GET)
# resp = requests.get(url='http://{}/api/open/del_card?apikey={}&card={}'.format(api_url, ApiKey, card))
if resp.json()['code'] not in [0, 1]:
    print('访问接口时发送错误\n错误码:{}\n错误信息:{}'.format(resp.json()['code'], resp.json()['message']))
    exit()
if resp.json()['code'] == 0:
    print(resp.json()['message'])
```

### 易语言代码:

```
.版本 2

.子程序 删除卡密, 文本型
.参数 ApiKey, 文本型
.参数 卡密, 文本型
.局部变量 resp, 文本型

resp ＝ 到文本 (网页_访问S (“http://toolboxproject.api.nmsl.life/api/open/del_card”, 1, “apikey=” ＋ ApiKey ＋ “&card=” ＋ 卡密))
返回 (resp)
```

## 修改卡密机器码

### 此Api用于修改卡密机器码

### 需提交信息:ApiKey,要修改的卡密,新的机器码

### 返回:是否成功

### 接口:`api/open/modify_machine_code`

### Python代码:

```
import requests

api_url = 'toolboxproject.api.nmsl.life'
ApiKey = '你的ApiKey'
card = '你要新增的卡密'
new_machine_code = '新的机器码'
# 推荐请求写法(POST)
resp = requests.post(url='http://{}/api/open/modify_machine_code'.format(api_url),
                     data={'apikey': ApiKey,
                           'card': card,
                           'new_machine_code': new_machine_code})
# 请求方法2(GET)
# resp = requests.get(url='http://{}/api/open/modify_machine_code?apikey={}&card={}&new_machine_code={}'.
#                    format(api_url, ApiKey, card, new_machine_code))
if resp.json()['code'] not in [0, 1]:
    print('访问接口时发送错误\n错误码:{}\n错误信息:{}'.format(resp.json()['code'], resp.json()['message']))
    exit()
if resp.json()['code'] == 0:
    print(resp.json()['message'])
```

### 易语言代码:

```
.版本 2

.子程序 修改卡密机器码, 文本型
.参数 ApiKey, 文本型
.参数 卡密, 文本型
.参数 新机器码, 文本型
.局部变量 resp, 文本型

resp ＝ 到文本 (网页_访问S (“http://toolboxproject.api.nmsl.life/api/open/modify_machine_code”, 1, “apikey=” ＋ ApiKey ＋ “&card=” ＋ 卡密 ＋ “&new_machine_code=” ＋ 新机器码))
返回 (resp)
```
