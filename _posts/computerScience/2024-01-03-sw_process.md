---
title:  "소프트웨어 개발 프로세스"
category: computerScience
typora-root-url: ../
toc: true
toc_sticky: true
---



## <br>소프트웨어 개발 프로세스



### <br>소프트웨어 개발 관련자

- 요청 고객(Client)
- 사용자(Customer)
- 프로젝트 관리자(Project Manager)
- 개발자(Developer)

### <br>소프트웨어 개발 과정

1. 요구사항(Business Requirements)
   - Cutomer Pain Point + Scope + Benefit
2. 요구명세 + 요구분석(Requirements)
   - 요구사항 유도: 요청자와의 토의를 통해 요구사항을 구체화
   - 요구사항 분석: 요구사항을 상세화해서 명확하게 만드는 작업 
   - 요구사항 기록: 요구사항을 문서화
     - 기능 레벨(Functinal Requirements)
     - 필요 시스템(System Requirements)
     - 테스트 요구사항(Quality Requirements)
     - 외부 시스템과의 연결 요구사항(External Requirements)
     - 제약 사항(Constraints)
3. 설계(Design)
   - 시스템을 구성하는 내부 프로그램이나 모듈 간의 관계와 구조 설계
   - 프로그램 내의 각 모듈에서의 처리 절차나 알고리즘 설계
4. 구현(Implementation)
   - 실제 프로그램을 작성하는 단계
   - 요구사항분석부터 출시까지 전체 관리하기도 함
5. 테스트(Testing)
   - QA: 요구사항 명세를 분석하여 테스트 케이스화 하며 테스트 계획을 만들고 테스트를 진행
6. 공개(Release)
   - Pre-alpha: 핵심 기능이 동작하기 시작한 상태
   - Alpha: 소프트웨어 테스트 단계
   - Beta: 외부에 테스트 단계로 명시 후 오픈해서 내외부 테스트 단계
   - RC(Release Candidate): 정식 Release 후보
   - Official Release: 고객이 사용하는 완벽한 버전
7. 유지보수(Maintenance)
   - 프로그램 유지보수, 추가 요구사항 반영 등



### <br>개발 방법론

- 폭포수 모델(Waterfall Model)
  - 각 단계를 확실히 마무리 지은 후에 다음 단계로 넘어가는 모델
  - 단점
    - 일정을 타이트하게 잡을 수록 개발자의 야근 증가
    - 요구사항 변경이 어려움

- 프로토타입(Prototype Model)
  - 고객이 원하는 핵심기능만 구현 후 고객의 피드백을 반영 후 개발하는 모델
- 나선형 모델(Spiral Model)
  - 개발시 위험을 최소화하기 위해 점진적으로 완벽한 프로그램을 개발해나가는 모델
- 애자일 모델(Agile Model)

  - 개발자는 새로운 기술을 빠르게 익히고 바로 서비스에 적용
    - <u>최소 기능 레벨로 빠르게</u> 개발, 적용, 경험 후 변경
    - 기능 개발시 <u>ABTest 등 고객 반응 확인 후 출시</u>

  - 프로세스
    1. Scrum Team 구성
       - Product Owner(Manager): 제품 책임자(요구사항 담당 등)
       - Scrum Master: 스크럼의 진행자
       - Development team
         - Senior Dev Manager: 시니어 개발자(개발작업 분배 및 관리)
         - Devloper
         - Designer
    2. Sprint(주기) 를 만들어 계획을 세움
    3. Daily Scrum 으로 매일 진척/변경사항 확인 및 공유
    4. Sprint(주기)가 끝나면 그동한 진행한 것을 리뷰



### <br>DevOps

- 개발(Development)과 운영(Operations)의 합성어
- 소프트웨어 개발자와 정보기술 전문가 간의 소통, 협업 및 통합을 강조하는 개발 환경이나 문화를 의미
