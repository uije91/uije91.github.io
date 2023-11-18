---
title:  "(비선형 자료구조) - 힙"
category: algorithm
typora-root-url: ../
toc: true
toc_label: "힙(Heap)"
toc_sticky: true
use_math: true
---

## <br>힙(Heap)

- 완전 이진 트리 형태

  - 중복 값 허용

  - 반 정렬 상태

- 최소값 또는 최대값을 빠르게 찾아내는데 유용한 자료 구조

  - 최대 힙(Max Heap) : 부모 노드의 키가 자식 노드의 키보다 크거나 같은 형태 

  - 최소 힙(Min Heap) : 부모 노드의 키가 자식노드의 키보다 작거나 같은 형태

    


<img src="/images/2023-11-31-algorithm-Heap/heap-1700280061890-3.png" alt="heap" style="zoom:35%;" />

### <br>힙 삽입

- 트리의 가장 끝 위치에 데이터 삽입
- 부모 노드와 키 비교한 후 작을 경우 부모자리와 교체(반복)



<img src="/images/2023-11-31-algorithm-Heap/heap insert.png" alt="heap insert" style="zoom:60%;" />

### <br>힙 삭제

- 최상위 노드 반환 및 삭제
- 가장 마지막 위치의 노드를 최상위 노드로 위치 시킴
- 자식 노드 중 작은 값과 비교 후 부모 노드가 더 크면 자리 교체(반복)



<img src="/images/2023-11-31-algorithm-Heap/heap delete.png" alt="heap delete" style="zoom:60%;" />
