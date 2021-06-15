# Python-mysql

* Pymysql 모듈 설치

  `!pip install pymysql`

* Localhost : 컴퓨터 네트워크에서 현재 실행중인 자신의 컴퓨터의 호스트 네임 

* import 방법

```python
import pymysql
conn = pymysql.connect(host = 'localhost', port = 3306, user = 'guest', passwd = 'guest', db = 'mydata')

cur = conn.cursor()

sql = "SELECT * FROM MYDATA.DATA1"
cur.execute(sql)
result = cur.fetchone()

print(result)

conn.commit()
conn.close()
```

* `cur.fetchone()` : 결과 한개를 보여줌
* `cur.fetchall()` : 모든 결과를 보여줌 
* `cur.execute(sql)` : 하나의 값 반영
* `cur.executemany(sql)` : 여러개의 데이터 값 반영 

