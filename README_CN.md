# Xiaoming-weather
从中国天气网http://www.weather.com.cn 爬取天气数据的小工具，提供个性化天气数据字符串。

## 安装
pip install xiaoming-weather

## 用法
工具为用户提供了两种使用方法，可以直接在终端命令行中当作一个外部三方工具使用，也可以在Python项目中当作Package包导入使用。工具在使用时，需要提供城市代码（city-code）作为入参，爬取对应的城市天气数据。想要获取某个城市代码，可以通过在中国天气网主页上搜索相应的城市，然后从城市主页的URL中获得。例如，西安的URL是http://www.weather.com.cn/weather/101110101.shtml，城市代码为'101110101'.

> 在命令行使用，爬取西安的数据：
```
zhangyd@zhangyd-ubuntu:~$ xiaoming-weather -q 101110101
小明天气：今天17℃~24℃，明天阴转多云，比今天凉一点，似乎要降温了。
明天: 阴转多云
温度: 10℃~20℃
风力: 3-4级转<3级
```
```
zhangyd@zhangyd-ubuntu:~$ xiaoming-weather --help
usage: xiaoming-weather [-h] [-q city-code]

XiaoMing Weather

optional arguments:
  -h, --help            show this help message and exit
  -q city-code, --query city-code
                        The specific city code from http://www.weather.com.cn
```
> 作为package使用，导入到Python项目中调用：
```
Python 3.7.9 (tags/v3.7.9:13c94747c7, Aug 17 2020, 18:58:18) [MSC v.1900 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from xiaoming_weather import xiaoming
>>> xaweather = xiaoming.Weather('101040100')
>>> weatherDataTomorow = xaweather.getSepcificDay(2)
>>> weatherDataToday = xaweather.readHistoryTempData()
>>> print (xiaoming.XiaoMingWeather(weatherDataToday, weatherDataTomorow).weatherMsg)
小明天气：今天17℃~24℃，明天阴转多云，比今天凉一点，似乎要降温了。
明天: 阴转多云
温度: 10℃~20℃
风力: 3-4级转<3级
>>>
```
## 已知问题：
> 在一些Linux主机上，pip install xiaoming-weather安装会提示如下WARNING，Windows主机上暂未发现问题。
```
Building wheels for collected packages: xiaoming-weather
  Building wheel for xiaoming-weather (setup.py) ... done
  Created wheel for xiaoming-weather: filename=xiaoming_weather-1.0.1-py3-none-any.whl size=6994 sha256=a381cd2d86a7e66724a132116168b4e58d7d493c247df045d80366a7ba74d4fe
  Stored in directory: /home/zhangyd/.cache/pip/wheels/49/1f/a0/cbae5958f9355fa882c6ce7f367d2fee268401ffe38f442aaa
Successfully built xiaoming-weather
Installing collected packages: chinese_calendar, lxml, xiaoming-weather
  WARNING: The script xiaoming-weather is installed in '/home/zhangyd/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed chinese_calendar-1.7.2 lxml-4.9.1 xiaoming-weather-1.0.1
zhangyd@zhangyd-ubuntu-22:~$
```
解决办法:
echo 'export PATH=$HOME/.local/bin:$PATH' >>~/.bashrc