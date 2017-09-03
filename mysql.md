### python和mysql交互
- 安装pymysql模块
```
sudo apt-get install python3-pymysql
```
1. mysql查询   

```
import pymysql

try:
    conn = pymysql.connect(host='192.168.0.199',user='zabbix',passwd='zabbix',db='zabbix',port=3306)
    cur = conn.cursor()
    cur.execute('select * from users')

    for record in cur.fetchall():
        print(record)

    cur.close()
    conn.close()

except pymysql.err.OperationalError as reason:
    print('mysql connect error :',reason)

```
