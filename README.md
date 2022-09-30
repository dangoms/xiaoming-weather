# Xiaoming-weather
Utility that provides personalized weather data strings for chinese user. Its weather data is captured from http://www.weather.com.cn

[Chinese 中文](README_CN.md)

## Install
pip install xiaoming-weather

## Usage
The utility provides two ways for users who want to get weather data strings of a city by the city code. one is as a external tools running on terminal directly, another is as a packatge in python project. You can get city code in a URL by searching city name on homepage of site http://www.weather.com.cn. For example, Xi'an homepage is http://www.weather.com.cn/weather/101110101.shtml, so its city code is '101110101'.

> Following query on terminal will provide weather data strings of Xi'an.
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
> Using the utility as a package in your python project.
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
## Known issues
> If you see the following warning on a linux host when using the pip install.
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
Sollution:
echo 'export PATH=$HOME/.local/bin:$PATH' >>~/.bashrc
