# Sina 模拟登陆框架

**说明：**

1，本框架使用 `selenium` 进行自动化登陆操作，你必须安装好 `python` 环境，并安装 `selenium库` 

2，你需要使用的微博账号为免验证码账号，某宝自行购买，按行放入 `account.txt` ,格式如： `qianxue2d000r@163.com----GBYzlj5gudd` 

3，需要下载对应 `chrome` 版本的 `chromedriver` ，自行搜索下载

4，确保你有一个 `redis数据库` ，本框架基于本地的redis服务，没有设置密码，但使用公网redis服务器，必须设置密码，确保安全

5，可根据实际环境修改代码



**如何运行：**

1,配置好 基本参数：

​	打开config.py

```python
# Redis数据库地址
REDIS_HOST = 'localhost'

# Redis端口
REDIS_PORT = 6379

# Redis密码，请设为空  #如果设置redis密码，则需要自行修改部分代码

#默认设置，无需更改
REDIS_DOMAIN = '*'
REDIS_NAME = '*'

#数据库标号
REDIS_DB=3

#api接口配置
API_HOST='0.0.0.0'
API_PORT=5000

#运行平台
PLATFORM='windwos'

#默认开启cookies进程和api进程
GENERATOR_PROCESS=True
API_PROCESS=True

```

2，导入账号密码 import_account.py

需要在account中写入购买的账号

```python
python3 import_account.py
```

每次新购买的账号 只需写入account.txt 然后运行import_account.py 即可（会自动将新导入redis的账号进行模拟登陆）

3，访问接口，获取cookie

```python
@app.route('/<name>/random')
def random(name,):
    """
    获取随机的Cookie, 访问地址如 /weibo/random
    :return: 随机Cookie
    """
    g = get_conn()
    cookies = getattr(g, name + '_cookies').get_random()
    return cookies
```

访问 `http://localhost:5000/weibo/random` 即可获取随机的cookie值

