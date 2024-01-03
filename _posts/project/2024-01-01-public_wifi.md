---
title:  "공공 와이파이 프로젝트"
category: singleProject
typora-root-url: ../
---

# <br>공공 와이파이 프로젝트

- OPEN API를 활용하여 자신의 위치 및 특정 위치에서 주변 와이파이를 찾는 기능 구현



## 사용 기술

- Language: JAVA / JSP
- DB: MariaDB
- Server: Tomcat 8.5
- OS: Windows11



## 기능 설명

- OPEN API를 활용하여 공공WIFI 정보를 DB에 저장
- 사용자가 입력한 좌표(또는 현재 위치의 좌표)를 기준으로 주변 20개의 와이파이 정보 출력
- 조회 시점으로 트리거를 이용하여 DB에 저장 및 정보 조회기능 제공
- 주변 WIFI의 상세 정보 제공
- 사용자는 북마크 그룹을 이용할 수 있으며, CRUD기능 제공



## ERD





## 프로젝트 구조

- JAVA
  - controller
    - dbConn: JDBC
  - dao
    - HistoryDAO
      - insertHistory(): WIFI 검색 시 위치 히스토리 자동 저장
      - getHistoryList(): 저장된 History 목록 출력
      - deleteHistory(): 저장된 History 삭제
    - WifiDAO: 와이파이 DAO
      - getNearbyWifiList(): 위도,경도값을 기준으로 근처 20개의 WIFI정보 출력
      - insertWifi(): 파싱된 데이터를 DB에 추가
      - insertAPI(): JSON을 파싱하여 insertWifi() 실행
      - wifiCnt(): OPEN API 갯수 체크
  - dto
    - WifiDTO: 와이파이 DTO
    - HistoryDTO: 와이파이 조회기록 DTO
- webapp
  - crud
    - history-delte.jsp: 위치 히스토리 목록 삭제
  - resources
    - CSS
      - style.css: 사용된css파일
    - JS
      - script.js
        - getLocation(): geolocation을 이용하여 현재 위치 가져오기
        - getnearbyWifiList(): input값을 전달받아서 get방식으로 주소 호출
  - include
    - header.jsp: 전체페이지의 header부분
    - menu.jsp: 메뉴탭 jsp
  - index.jsp: : Home화면
  - load-wifi.jsp: Open API를 통해 DB에 저장 후 출력되는 페이지(중복 제외한 추가 데이터 개수 출력)
  - history.jsp: 주변 와이파이 검색시 자동 저장 되는 위치 히스토리 목록 조회,삭제 
  - detail.jsp: 위치정보로 검색된 WIFI의 상세정보 조회







## SQL 쿼리

```sql
# 데이터베이스 생성
create database PUBLIC_WIFI

# 계정 생성
CREATE USER 'admin'@'localhost' IDENTIFIED BY '1234'
CREATE USER 'admin'@'%' IDENTIFIED BY '1234'

# DB권한 부여
GRANT ALL PRIVILEGES ON PUBLIC_WIFI.* TO 'admin'@'localhost' IDENTIFIED BY '1234'
GRANT ALL PRIVILEGES ON PUBLIC_WIFI.* TO 'admin'@'%' IDENTIFIED BY '1234'

# 테이블 생성
CREATE TABLE PUBLIC_WIFI (
	MGR_NO VARCHAR(20) primary key ,
	WRDOFC VARCHAR(10) NULL,
	MAIN_NM VARCHAR(50) NULL,
	ADRES1 VARCHAR(100) NULL,
	ADRES2 VARCHAR(100) NULL,
	INSTL_FLOOR VARCHAR(20) NULL,
	INSTL_TY VARCHAR(50) NULL,
	INSTL_MBY VARCHAR(20) NULL,
	SVC_SE VARCHAR(20) NULL,
	CMCWR VARCHAR(20) NULL,
	CNSTC_YEAR VARCHAR(10) NULL,
	INOUT_DOOR VARCHAR(10) NULL,
	REMARS3 VARCHAR(100) NULL,
	LAT VARCHAR(20) NULL,
	LNT VARCHAR(20) NULL,
	WORK_DTTM VARCHAR(30) NULL
);

CREATE TABLE HISTORY_WIFI (
	ID INTEGER AUTO_INCREMENT primary key ,
	LAT VARCHAR(20) NULL,
	LNT VARCHAR(20) NULL,
	SEARCH_DTTM varchar(30) NULL
);

# 트리거 생성(PUBLIC_WIFI 조회 시 HISTORY_WIFI에 정보 저장)

```

