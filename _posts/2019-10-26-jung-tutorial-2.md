---
layout: post
title: "[JUNG] 3-2. 튜토리얼(2) 노드와 링크의 추가"
date: 2019-10-17 21:46
categories: 프로그래밍
tags: 
  - java
  - jung
  - graph
  - network
  - node
  - vertex
  - link
  - edge
---

노드와 링크 추가를 위해 일단 그래프를 만든다. 튜토리얼에서는 SparseMultigraph 유형을 사용했지만, 다른 그래프 유형을 사용해도 무방할 것 같다. 그리고 `Graph<V,E>`를 구현하여 새로운 그래프 클래스를 만들어도 된다고 나와 있다. 노드와 링크에는 모든 객체 유형이 다 들어갈 수 있다고 설명되어 있다. 튜토리얼의 일부를 보면, 아래와 같은 식으로 그래프를 만들고 노드와 링크를 추가한다. 

```java
Graph<Integer, String> g = new SparseMultigraph<Integer, String>();

g.addVertex((Integer)1);
g.addVertex((Integer)2);
g.addVertex((Integer)3);

g.addEdge("Edge-A", 1, 2)
g.addEdge("Edge-B", 2, 3);
```

근데 특이한 것은 동일한 노드 혹은 링크가 둘 이상의 그래프에 동시에 속하도록 할 수도 있다고 되어 있다. 위에서 그래프 `g`에 추가한 노드와 링크를 아래의 `g2`에 추가한다.

```java
Graph<Integer, String> g2 = new SparseMultigraph<Integer, String>();

g2.addVertex((Integer)1);
g2.addVertex((Integer)2);
g2.addVertex((Integer)3);

g2.addEdge("Edge-A", 1,3);
g2.addEdge("Edge-B", 2,3, EdgeType.DIRECTED);
g2.addEdge("Edge-C", 3, 2, EdgeType.DIRECTED);
g2.addEdge("Edge-P", 2,3);
```

