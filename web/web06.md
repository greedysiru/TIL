# [스파르타코딩] 웹개발 종합반 항해 1기 3주차 (2)(2021.2.3 ~ 4)



**상세 내용 [블로그](https://greedysiru.tistory.com/162) 참고**



# 1. mongoDB

* **GUI**를 제공하지 않는다.
* **robo3T**로 DB내부를 살펴볼 수 있다.



## robo3T 세팅하기

* 실행 후 뜨는 창에서 **create** 클릭
* Name, Address 등을 세팅한다.



# 2. DB개괄

## SQL vs. NoSQL

* **RDBMS(SQL)**
  * 행/열의 생김새가 정해진 엑셀에 데이터를 저장하는 것과 유사
  * 열을 추가하는 것과 같은 작업은 어렵다.
  * 정형화 되어있는 만큼 데이터의 일관성/분석에 용이
  * MS-SQL, My-SQL 등
* **No-SQL(Not only SQL)**
  * 딕셔너리 형태로 데이터를 저장하는 DB
  * 자유로운 형태의 데이터 적재에 유리
  * 일관성 부족
  * MongoDB



# 3. pymongo로 DB조작하기

* **pymongo** : mongoDB를 조작할 수 있는 파이썬의 라이브러리
* **insert / find / update / delete** 가능
* DB에 데이터를 저장할 때, 데이터의 종류를 통일해야 관리하기 용이하다.



## pymongo 기본코드

```python
from pymongo import MongoClient         # pymongo를 임포트
client = MongoClient('localhost', 27017) # pymongo는 27017 포트로 돌아간다.
db = client.dbsparta                   # 'dbsparta'라는 이름의 db 생성
```



## insert

### DB연결하기 & 데이터 넣기

```python
# 'users'라는 collection에 아래의 딕셔너리를 삽입
db.users.insert_one({'name':'bobby','age':21})
db.users.insert_one({'name':'kay','age':27})
db.users.insert_one({'name':'john','age':30})
```



## find

### 모든 결과 값을 보기 (find)

```python
# MongoDB에서 데이터 모두 보기
all_users = list(db.users.find({}))

# 참고) MongoDB에서 특정 조건의 데이터 모두 보기
same_ages = list(db.users.find({'age':21},{'_id':False})) # id는 표시하지 않기

print(all_users[0])         # 0번째 결과값을 보기
print(all_users[0]['name']) # 0번째 결과값의 'name'을 보기

for user in all_users:      # 반복문을 돌며 모든 결과값을 보기
    print(user)
```

### 특정 결과 값을 뽑아 보기 (find)

```python
user = db.users.find_one({'name':'bobby'}) # name이 boby인 데이터만 뽑기
print(user)
```



## update

### 수정하기

```python
# 생김새
db.people.update_many(찾을조건,{ '$set': 어떻게바꿀지 })

# 예시
db.users.update_one({'name':'bobby'},{'$set':{'age':19}})
```



## delete

### 삭제하기

```python
db.users.delete_one({'name':'bobby'})
```

* 데이터를 삭제하는 것은 리스크가 클 수 있으므로 주의



## 코드 요약

```python
# 저장 - 예시
doc = {'name':'bobby','age':21}
db.users.insert_one(doc)

# 한 개 찾기 - 예시
user = db.users.find_one({'name':'bobby'})

# 여러개 찾기 - 예시 ( _id 값은 제외하고 출력)
same_ages = list(db.users.find({'age':21},{'_id':False}))

# 바꾸기 - 예시
db.users.update_one({'name':'bobby'},{'$set':{'age':19}})

# 지우기 - 예시
db.users.delete_one({'name':'bobby'})
```



# Reference

**스파르타코딩 - 웹개발 종합반**