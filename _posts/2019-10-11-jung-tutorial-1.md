---
layout: post
title: "[JUNG] 3-1. 튜토리얼(1) Graph 인터페이스"
date: 2019-10-11 00:11
categories: 프로그래밍
tags: 
  - java
  - jung
  - graph
  - network
---

JUNG sample 프로젝트를 살펴보든 중, 약간 오래된 버전이긴 하지만 [JUNG tutorial](http://www.grotto-networking.com/JUNG/JUNG2-Tutorial.pdf) 을 찾게 되었다. 간략하긴 하지만, 핵심 기능들이 소개되어 있고 이후 공부해 나갈 수 있는 좋은 출발점이 될 것 같아서 이 튜토리얼 먼저 공부하기로 했다. 

가장 기본이 되는 것은 역시 `Graph<V,E>` 인터페이스이다. 여기에 웬만한 기능들은 다 구현이 되어 있다. 대표적으로 다음과 같다.  
1\) 노드와 링크의 추가와 삭제, 그리고 모든 노드와 모든 링크의 모음 가져오기  
2\) 한 링크의 끝점 구하기  
3\) 노드에 대한 정보 구하기. 대표적으로 degree measure, 그리고 들어오는 링크를 통해 연결된 노드와 나가는 노드를 통해 연결된 노드 등.

사실 이 `Graph<V,E>` 인터페이스는 `Hypergraph<V,E>` 인터페이스를 상속받은 것이다. Hyper-graph 라는 개념이 JUNG 에서 제공되는데, 이건 graph 개념을 일반화시킨 것으로서 두 개 이상의 노드들과 연결되는 링크가 존재할 수 있는 개념이다. (사실 상식적으로는 있을 수 없는 것이지만, 왜 이렇게 만들어놨는지는 모르겠다. 프로그래밍 상의 편의 때문인지...)

`Graph<V,E>` 인터페이스와 연관된 것으로는 `Directed Graph<V,E>`, `Undirected Graph<V,E>`, `Simple Graph<V,E>`가 있다. 앞의 두 가지는 이름에 잘 표현되어 있고, Simple Graph 는 parallel edge 나 self loop 을 허용하지 않는 것을 가리킨다(Multi Graph 의 반대말이 아닌가 싶다). 

그런데 실제로 사용할 때에는 다양한 그래프 중에서 선택할 수 있는데, directed/undirected 의 구분 이외에도 sparse/(unsparse) 의 구분도 있다(unsparse 라는 용어는 없고, sparse 가 붙이 않은 것은 unparse 인 것 같다). Sparse 그래프는 `Sparse means that the implementation is efficient for large graphs with low average connectivity` 라고 설명되어 있다. 정확히 어느 정도 되어야 large 인지는 모르겠지만, 보통 sparse graph 를 많이 사용하는 것 같다. 어쨌든 이러한 구분 기준에 따라 원하는 그래프 유형을 골라서 사용하면 된다. 