---
title:  "(비선형 자료구조) - 트리"
category: algorithm
typora-root-url: ../
toc: true
toc_label: "트리(Tree)"
toc_sticky: true
use_math: true
---

## <br>트리(Tree)

- 노드와 링크로 구성된 자료구조
- 계층적 구조를 나타낼 때 사용합니다.
  - 폴더 구조(디렉토리,서브 디렉토리)
  - 조직도, 가계도 등..



### <br>트리의 구조

<img src="/images/2023-11-19-algorithm-Tree/tree.png" alt="tree" style="zoom:67%;" />

- 노드(Node): 트리 구조의 자료 값을 담고 있는 단위
- 에지(Edge): 노드 간의 연결선 (=link, branch) 
- 루트 노드(Root): 부모가 없는 노드, 가장 위의 노드
- 잎새 노드(Leaf): 자식이 없는 노드 (=단말)
- 내부 노드(Internal): 잎새 노드를 제외한 모든 노드
- 부모(Parent): 연결된 두 노드 중 상위의 노드
- 자식(Child): 연결된 두 노드 중 하위의 노드
- 형제(Sibling): 같은 부모를 가지는 노드
- 깊이(Depth): 루트에서 어떤 노드까지의 간선의 수
- 레벨(Level): 트리의 특정 깊이를 가지는 노드 집합
- 높이(Height): 트리에서 가장 큰 레벨 값(이미지의 높이 : 4)
- 크기(Size): 자신을 포함한 자식 노드의 개수
- 차수(Degree): 각 노드가 지닌 가지의 수(A의 차수: 2 / F의 차수: 1)
- 트리의 차수: 트리의 최대 차수

***



### <br>트리의 특징

- 하나의 노드에서 다른 노드로 이동하는 경로는 유일합니다.
- 노드가 N개인 트리의 Edge수는 n-1개 입니다.
- Acyclic (Cycle - X)
- 모든 노드는 서로 연결되어 있어야합니다.
- 하나의 Edge를 끊으면 2개의 Sub-Tree로 분리됩니다.



### <br>이진 트리(Binary Tree)

- 각 노드는 최대 2개의 자식을 가질 수 있습니다.
- 자식 노드는 좌우를 구분합니다.
  - 왼쪽 자식: 부모 노드의 왼쪽 아래
  - 오른쪽 자식: 부모 노드의 오른쪽 아래



### <br>이진 트리 종류

- 포화 이진 트리(Perfect Binary Tree)
  - 모든 레벨에서  노드들이 꽉 채워져 있는 트리
- 완전 이진 트리(Complete Binary Tree)
  - 마지막 레벨을 제외하고 노드들이 모두 채워져 있는 트리
- 정 이진 트리(Full Binary Tree)
  - 모든 노드가 0개 또는 2개의 자식 노드를 갖는 트리

- 편향 트리(Skewed Binary Tree) = 사향 이진 트리(Degenerate Binary Tree)
  - 한쪽으로 기울어진 트리

- 균형 이진 트리(Balanced Binary Tree)
  - 모든 노드의 좌우 서브 트리 높이가 1이상 차이 나지 않는 트리

![Tree2](/images/2023-11-19-algorithm-Tree/Tree2.webp)

### <br>이진 트리 특징

- 포화 이진 트리의 높이가 h일 때 노드의 수는 2<sup>h+1</sup> - 1개
- 포화(or완전) 이진 트리의 노드가 N개 일 때 높이는 $log_2$N
- 이진 트리의 노드가 N개 일 때 최대 가능 높이는 N
