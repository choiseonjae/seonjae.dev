---
title: \[MYSQL] 사용자 권한 확인, 부여, 삭제 (grant, revoke)

categories: 
   - Mysql
   - Command
tags:
   - Mysql
   - grant
   - revoke

author_profile: true #작성자 프로필 출력여부
read_time: true # read_time을 출력할지 여부 1min read 같은것!

toc: true #Table Of Contents 목차 보여줌
toc_label: "My Table of Contents" # toc 이름 정의
toc_icon: "cog" # font Awesome아이콘으로 toc 아이콘 설정 
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차

last_modified_at: 2020-02-17T10:00:00 # 마지막 변경일

---

<!-- intro -->
{% include intro %}

# 쿼리

권한을 부여하기 위해서 먼저 **root 계정**으로 접속하면 된다.  

## 사용자 추가하기

```sql
mysql> create user '사용자'@'localhost(또는 %)' identified by '비밀번호';
```

## 사용자에게 데이터베이스 권한 부여

```sql
grant all privileges on [DB 이름].[테이블 이름] to '[user id]'@'localhost(또는 %)';

grant select on [DB명].[테이블명] to '[user id]'@'localhost(또는 %)';
grant update(컬럼1, 컬럼2) on DB명.테이블명 to '[user id]'@'localhost(또는 %)';
```

**특정 데이터베이스** 권한 혹은 **특정 데이터 베이스의 특정 테이블**에만 권한을 줄 수 있다.  

권한을 줄 때도, all privileges(select, update, delete etc..)나 select 권한 만 줄 수도 있다.

특정 컬럼의 update 권한만 부여할 수 도 있다.

모든 데이터베이스의 권한을 부여하고 싶으면 DB이름에 `*`을 넣으면 되고, 테이블도 모든 권한 부여하고 싶으면  `*`을 넣으면 된다.
ex) *.* : 모든 DB의 모든 테이블 권한

@ 뒤에 localhost 가 붙으면 로컬에서 접속할 경우를 뜻한다.  
@ 뒤에 %가 붙으면 원격, 특정 외부 ip도 지정할 수 있다.

## 사용자 권한 삭제하기
``` sql
revoke all on DB명.테이블명 from '사용자'@'localhost(또는 %)';
```
위와 마찬가지로 응용해서 사용가능하다.

## 사용자 권한 확인하기
``` sql
show grants for '[user id]'@'localhost(또는 %)';
```

# Reference

* [[[MySQL] 사용자 추가, 삭제, 권한 부여](https://sleepyeyes.tistory.com/32)]