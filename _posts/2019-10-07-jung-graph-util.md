---
layout: post
title: "[JUNG] 1-3. 그래프 유틸"
date: 2019-10-07 17:41
categories: 프로그래밍
tags: 
  - java
  - jung
  - graph
  - network
  - util
---

 jung-api 프로젝트에 있는 세 번째 패키지는 jung.graph.util 패키지이다. 


먼저 EdgeIndexFunction 인터페이스가 있다. 주어진 그래프 속에서 특정한 edge 의 index 를 반환하는 기능을 구현하도록 할 클래스를 위한 인터페이스인 것 같다. 어떤 순서로 edge 를 배열할 것인지가 구현 단계에서의 이슈인 것 같다. getIndex(), reset() 이 주요 메쏘드이고, index 는 정수형으로만 만들어야 한다고 설명되어 있다.  
이 인터페이스를 구현한 클래스로, 먼저 IncidentEdgeIndexFunction 클래스가 있다. 제목대로 incident edge 의 index 를 생성하고 유지한다고 설명되어 있다. 내부에 edge_index 라는 HashMap 을 속성으로 갖고, 여기에 index 를 저장하는 구조이다.  
구현한 다른 클래스로, DefaultParallelEdgeIndexFunction 클래스가 있다. Parellel Edge 를 위한 index 를 생성하고 관리하는 클래스라고 되어 있다.  `Parallel edges are defined here to be the collection of edges that are returned by v.findEdgeSet(w) for some v and w.` 라고 되어 있는걸 보니, 여러개의 edge 로 이루어진 edge set 을 위한 도구인 듯 하다.

나머지 클래스들은 서로 상속이나 구현 관계 없이 독립적으로 존재한다. 먼저 Context 클래스가 있다. `A class that is used to link together a graph element and a specific graph.` 라고 설명되어 있다. Repast Simphony 에 나오는 context 랑 유사한 개념이 아닐까 싶다. 

Graphs 클래스는 jung.graph 패키지에 있는 GraphDecorator 의 구현이라고 되어 있는데, 실제로 그것을 상속받거나 하지는 않았다. `Provides specialized implementations of GraphDecorator.` 메쏘드가 엄청 많다.

Pair 클래스는 자바의 Collection, Serializable 인터페이스를 구현한 클래스이다. 제목대로 두 개의 객체를 쌍으로 묶어서 저장한다고 설명되어 있다. 

TreeUtil 클래스는 `Contains static methods for operating on instances of Tree.` 라고 설명되어 있는 걸 보니, jung.graph 패키지에 있는 Tree 타입의 객체를 위한 메쏘드의 모음인 것 같다. 대충 훑어보니, getRoots(), getSubTree() 등 Tree 관련 메쏘드가 보인다. 

EdgeType 이라는 열거형이 있는데, 이 안에는 그냥 DIRECTED, UNDIRECTED 두 개의 요소만 들어 있다. 

다음에는 jung-graph-impl 프로젝트에 들어있는 실제 구현 클래스를 봐야겠다.

