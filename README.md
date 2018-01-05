# 12306Python
py12306 是一个 Python 3.x 版的12306.cn订票程序。

## 功能介绍
```
唯一需要手动操作的是：等待浏览器页面跳出后输入验证码点击登录
目前支持的功能：
    1、支持配置出发地、目的地、乘车日
    2、支持配置车次类型（动车、高铁等）
    3、支持配置出发时间
    4、需要手动输入登录验证码
    5、支持配置预定车次的选择顺序（order字段，暂时只支持配置成0，车次选择算法待优化）
    6、预定、购票自动完成	
   
还不支持的功能：
    1、chromedriver不支持可配置
    2、不支持车次选择
    3、不支持席别选择
```

## Usage
### 1、修改config配置
```
参照Config说明
```
### 2、驱动路径配置
```
__init__方法：修改self.executable_path=r'C:\Users\xxx\Downloads\chromedriver.exe' 为自身的chromedriver.exe地址（后续做成可配置）；
readConfig方法：修改path = r"D:\worspace-afw\12306Python\config.ini"为自身的config.ini路径
```
### 3、运行
```
直接运行:
python 12306Python.py
```
### 3、输入验证码
```
等待跳出浏览器页面，输入验证码，点击登录
```
### 4、完成支付
```
等待自动完成选票、提交订单，支付订单
```

## 环境说明
### Python版本 3.X
### 依赖包
```
pip install splinter
pip install configparser
```
### chromedriver
```
下载chromedrive驱动，修改配置（）
```

## Config说明

最简单的方法是修改 config.ini， 然后填写自己的乘车信息， 这些配置都可以在运行期间进行修改。

```
; config.ini
; 配置信息：请依照注释修改必选项

## 登陆账号和密码
[login]
### username：12306登录用户名，必选参数
username=xxx@qq.com
### password：12306登录密码，必选参数
password=xxx

## cookie信息，出发站，目的站
## cookies值得自己去找, 下面两个分别是武汉, 襄阳
[cookieInfo]
### starts：对应搜索框出发地，必选参数，通过抓取查询请求获得cookie值
starts=%%u6B66%%u6C49%%2CWHN
### ends：对应搜索框目的地，必选参数，通过抓取查询请求获得cookie值
ends=%%u8944%%u9633%%2CXFN
### dtime：对应搜索框出发日，必选参数，时间格式：年-月-日，例如 2018-01-19
## 时间格式2018-01-19
dtime=2018-01-11

## order：车次，选择第几趟，0则从上至下依次点击，必选参数，有效值如下：
#### 0->从上至下点击
[orderItem]
order=0

## users：乘客姓名，必选参数，中文姓名，支持多个乘客，用英文逗号隔开，例如：张三,李四
[userInfo]
users = xxx

## 车次类型：
[trainInfo]
### train_types：车次类型，可选参数，默认全部车次，支持多个值，用英文逗号隔开，有效值如下：
#### T->特快
#### G->高铁
#### D->动车
#### Z->直达
train_types = D,G

### start_time：发车时间，可选参数，默认值“00:00--24:00”
### 时间格式 "12:00--18:00"（需要带英文格式的双引号），有效值如下：
##### “00:00--24:00”->00:00--24:00
##### “00:00--06:00”->00:00--06:00
##### “06:00--12:00”->06:00--12:00
##### “12:00--18:00”->12:00--18:00
##### “18:00--24:00”->18:00--24:00
start_time = "12:00--18:00"

## 网址，必选参数
## 此部分不需改动
[urlInfo]
ticket_url = https://kyfw.12306.cn/otn/leftTicket/init
login_url = https://kyfw.12306.cn/otn/login/init
initmy_url = https://kyfw.12306.cn/otn/index/initMy12306
buy = https://kyfw.12306.cn/otn/confirmPassenger/initDc
```

## TODO
```
1、支持控制台命令
2、支持邮件提醒
3、支持席别选择
4、转换为可执行文件，去除Python强依赖
5、。。。
```

LICENSE

GNU General Public License, version 2
