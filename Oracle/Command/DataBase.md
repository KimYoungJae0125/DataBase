# DataBase


## User 생성

```sql
SQL> Create User oracle_test Identified by oracle_test; 
```
```shell
User created.
```

## 계정 권한 할당
```sql
SQL> Grant [권한명] To [계정]
```

## 계정 권한 제거
```sql
SQL> Revoke [권한명] On [테이블명] From [계정];
```

## 계정 권한 종류
```sql
Create User : 데이터 베이스 유저 생성 권한
Select Any Table : 모든 유저의 테이블 조회 권한
Create Any Table : 모든 유저의 테이블 생성 권한
Create Session : 데이터 베이스 접속 권한
Create Table : 테이블 생성 권한
Create View : 뷰 생성 권한
Create Proced User : 프로시저 생성 권한
Create Sequence : 시퀀스 생성 권한
SYSDBA : 데이터베이스를 관리하는 최고 권한
SYSOPER : 데이터베이스를 관리하는 권한
```

