# 时间格式处理

时间的输出格式

```javascript
new Date().toDateString()
"Fri May 08 2020"

new Date().toISOString()
"2020-05-08T09:40:48.287Z"

new Date().toJSON()
"2020-05-08T09:40:55.058Z"

new Date().toLocaleDateString()
"2020/5/8"

new Date().toLocaleString()
"2020/5/8 下午5:41:11"

new Date().toLocaleTimeString()
"下午5:41:17"

new Date().toString()
"Fri May 08 2020 17:41:23 GMT+0800 (中国标准时间)"

new Date().toISOString().slice(0,10)
"2020-05-08"
```

获取指定时间段的起止时间

```javascript
var date = new Date();
var year = date.getFullYear();
var month = date.getMonth() + 1;
var day = date.getDate();
var weekday = date.getDay();
```

获取本周的第一天和最后一天

{% hint style="warning" %}
国外习惯周日是一周里的第一天，中国习惯周一是一周里的第一天所以计算第一天时要 + 1
{% endhint %}

```javascript
var firstdayOfCurrentWeek = (new Date(year, month, day + (weekday === 0 ? -6 : 1) - weekday + 1 )).toISOString().slice(0, 10);
var lastdayOfCurrentWeek = (new Date(year, month, day  + 7 - weekday + 1 )).toISOString().slice(0, 10);
```

获取本月的第一天和最后一天

```javascript
var firstdayOfCurrentMonth = (new Date(year, month -1, 1)).toLocaleDateString();
var lastdayOfCurrentMonth = (new Date(year,month, 0)).toLocaleDateString();
```

获取上月的第一天和最后一天

```javascript
var firstdayOfLastMonth = (new Date(year, month -2, 1)).toLocaleDateString();
var lastdayOfLastMonth = (new Date(year, month -1, 0)).toLocaleDateString();
```

计算过去某个时间点距离今天是多少天前

```javascript
/* @param: date string */
function daysAgo(date) {
    date= new Date(date.replace(/-/g, '/')).getTime();
    return Math.round((new Date().getTime() - date) / 1000 / 3600 / 24) + '天前';
}
daysAgo(lastdayOfLastMonth); // 9天前
```

使用 [moment.js](http://momentjs.cn/) 发现一切都变得更简单了

```javascript
moment().startOf('week').format('YYYY-MM-DD');
"2020-05-03"

moment().endOf('week').format('YYYY-MM-DD');
"2020-05-09"

moment().startOf('month').format('YYYY-MM-DD');
"2020-05-01"

moment().endOf('month').format('YYYY-MM-DD');
"2020-05-31"

moment().startOf('year').format('YYYY-MM-DD');
"2020-01-01"

moment().endOf('year').format('YYYY-MM-DD');
"2020-12-31"
```



