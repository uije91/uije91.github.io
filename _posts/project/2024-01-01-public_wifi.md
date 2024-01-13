---
title:  "공공 와이파이 프로젝트"
category: singleProject
typora-root-url: ../
---

# <br>공공 와이파이 프로젝트

- OPEN API를 활용하여 자신의 위치 및 특정 위치에서 주변 와이파이를 찾는 기능 구현
- Github: [바로가기](https://github.com/uije91/Public_Wifi)



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

![PUBLIC_WIFI](/../images/2024-01-01-public_wifi/PUBLIC_WIFI-1704610483298-2.png)



## 프로젝트 구조

- **JAVA**
  - controller
    - dbConn: JDBC
  - dao
    - BookmarkDAO
      - getBookmarkInfo(): id를 이용하여 북마크 정보 가져오기
      - getBookmarkList(): 북마크 목록 출력
      - insertBookmark(): 북마크 추가
      - deleteBookmark(): 북마크 삭제
    - BookmarkGroupDAO
      - getBGInfo(): id를 이용하여 북마크그룹에 정보 조회
      - getBGList(): 북마크그룹 목록 출력
      - insertBG(): 북마크그룹 추가
      - updateBG(): 북마크그룹 수정
      - deleteBG(): 북마크그룹 삭제
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
    - BookmarkDTO: 북마크 DTO
    - BookmarkGroupDTO: 북마크그룹 DTO
    - WifiDTO: 와이파이 DTO
    - HistoryDTO: 와이파이 조회기록 DTO
- **webapp**
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
  
  - history
    - history.jsp: 주변 와이파이 검색시 자동 저장 되는 위치 히스토리 목록 조회 및 삭제
    - history-delete.jsp: 히스토리 삭제 쿼리 실행 페이지
  - bookmark
    - bookmark-list.jsp: 북마크 보기 페이지
    - bookmark-add-submit.jsp: 북마크 추가 쿼리 실행 페이지
    - bookmark-delete.jsp: 북마크 삭제 페이지
    - bookmark-delete-submit.jsp: 북마크 삭제 쿼리 실행 페이지
  - bookmark-group
    - bookmark-group.jsp: 북마크 그룹 관리 페이지
    - bookmark-group-add.jsp: 북마크 그룹 추가 페이지
    - bookmark-group-add-submit.jsp: 북마크 그룹 추가 쿼리 실행 페이지
    - bookmark-group-edit.jsp: 북마크 그룹 수정 페이지
    - bookmark-group-edit-submit.jsp: 북마크 그룹 수정 쿼리 실행 페이지
    - bookmark-group-delete.jsp: 북마크 그룹 삭제 페이지
    - bookmark-group-delete-submit: 북마크 그룹 삭제 쿼리 실행 페이지
  - index.jsp: Home화면
  - load-wifi.jsp: Open API를 통해 DB에 저장 후 출력되는 페이지(중복 제외한 추가 데이터 개수 출력)
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
CREATE TABLE PUBLIC_WIFI
(
    MGR_NO      VARCHAR(20) primary key,
    WRDOFC      VARCHAR(10),
    MAIN_NM     VARCHAR(50),
    ADRES1      VARCHAR(100),
    ADRES2      VARCHAR(100),
    INSTL_FLOOR VARCHAR(20),
    INSTL_TY    VARCHAR(50),
    INSTL_MBY   VARCHAR(20),
    SVC_SE      VARCHAR(20),
    CMCWR       VARCHAR(20),
    CNSTC_YEAR  VARCHAR(10),
    INOUT_DOOR  VARCHAR(10),
    REMARS3     VARCHAR(100),
    LAT         VARCHAR(20),
    LNT         VARCHAR(20),
    WORK_DTTM   VARCHAR(30)
);

CREATE TABLE HISTORY_WIFI
(
    ID          INTEGER AUTO_INCREMENT primary key,
    LAT         VARCHAR(20),
    LNT         VARCHAR(20),
    SEARCH_DTTM varchar(30)
);

CREATE TABLE BOOKMARK
(
    ID       INTEGER AUTO_INCREMENT primary key,
    NAME     VARCHAR(50),
    MGR_NO      VARCHAR(20),
    DISTANCE VARCHAR(20),
    MAIN_NM  VARCHAR(50),
    REG_DTTM VARCHAR(30),
    FOREIGN KEY (MGR_NO) REFERENCES PUBLIC_WIFI(MGR_NO)
);


CREATE TABLE BOOKMARK_GROUP
(
    ID        INTEGER AUTO_INCREMENT primary key,
    NAME      VARCHAR(50),
    BG_ORDER  INTEGER,
    REG_DTTM  VARCHAR(30),
    EDIT_DTTM VARCHAR(30)
);
```



### <br>프로젝트 영상

{% include video id="87FVzyhuf4E" provider="youtube" %}
