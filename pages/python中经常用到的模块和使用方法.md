---
title: python中经常用到的模块和使用方法
---

## datetime
### 导入方法
#### from date_time import datetime, timedelta
### 获取昨天的日期，格式化为20201101这种:
#### `    default_yesterday_date_id = (datetime.now() - timedelta(1)).strftime('%Y%m%d') `
