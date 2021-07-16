## pandas 문자열 관련 함수

```python
import pandas as pd
df['column'].str[:2].head()
# 앞 2자리까지만 추출
```



```python
import pandas as pd
df['column'].str[-1].head()
# 마지막 한글자만 추출
```



```python
df['column'].str.split(" ").head()
# 공백 기준으로 분할 

df['column'].str.split(" ",expand = True).head()
# 분할된 개별 리스트를 데이터프레임으로 만들기 
```



```python
df['column'].str.startswith('sth').head()
# 시작글자 인식 (t/f로 반환)


df['column'].str.endswith('sth').head()
# 끝글자 인식 (t/f로 반환)

df['column'].str.contains('sth').head()
# 포함글자 인식 (t/f로 반환)

df['column'].str.extract('( \w*시 )|( \w*군 )|( \w*구 )').dropna(how='all')
# 원하는 문자열 추출 

```

특정 문자열을 포함하는 값을 그룹에 assign

```python
df['new column'].loc[df['column'].str_contains('찾을 문자열')] = '그룹지을 문자열'
```



```python
df = df[['column_name','column_name']]
```

