---
title:  "트랜잭션"
category: computerScience
typora-root-url: ../
toc: true
toc_sticky: true
---



## <br>트랜잭션(Transaction)

- 하나의 논리적 기능을 수행하기 위한 작업의 단위
- 보통 데이터베이스에서는 데이터베이 스 상태를 변화시키기 위해 수행하는 작업 단위를 의미한다.



### ACID

- Atomic(원자성)
  - All or Nothing, 모든 작업이 실행되거나 혹은 모두 실행되지 않아야 한다.
  - 예시) A 계좌에서 B 계좌로 잔액을 송금할 때
    - 'A계좌 잔액 줄이기' 작업와 'B게좌 잔액 늘리기' 작업은 함께 성공하거나 함께 실패해야 한다.
- Consistency(일관성)
  - 모든 트랜잭션이 종료된 후에는 DB의 제약조건을 모두 지키고 있는 상태가 되어야 한다.
  - 예시) 잔액은 0원 이상이다.
    - 이를 위반하는 트랜잭션은 모두 중단된다.
- Isolation(격리성)
  - 트랜잭션은 다른 트랜잭션과 독립적으로 동작해야 한다.
  - A 트랜잭션이 하는 일을 B  트랜잭션은 모르게 해야한다.
  - 하지만 현실은 ...
    - 성능과 안정성의 트레이드 오프 관계에 있는 부분이다.
    - READ_UNCOMMITTED > READ_COMMITTED > REPEATABLE_READ > SERIALIZABLE 순서로 성능은 떨어지고 격리성(고립성)은 증가한다.
      - 격리성이 낮을 때 일어나는 문제 : Dirty read, Phantom read 등이 발생 가능
    - 일반적으로는 MYSQL InnoDB의 기본 값인 REPEATABLE_READ를 많이 활용한다.
- Durability(지속성)
  - commit을 하게 되면 지속(저장)이 꼭 된다.
  - DB 저장이 실패하더라도 모든 로그를 남겨서 DB에 순차적으로 모두 반영이 되도록 한다.