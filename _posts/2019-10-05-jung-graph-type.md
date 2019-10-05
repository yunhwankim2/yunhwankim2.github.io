---
layout: post
title: "[JUNG] 그래프 타입"
date: 2019-10-05 17:04
categories: 프로그래밍
tags: 
  - java
  - jung
  - graph
  - network
---

JUNG (Java Universal Network/Graph Framework)는 이름 그대로 네트워크와 그래프와 관련된 작업을 수행하기 위한 프레임워크이다. Java 에서 네트워크/그래프 관련된 더 좋은 라이브러리나 프레임워크가 있는지 모르겠지만, 일단 검색해보니 JUNG 이 대표적인 프레임워크 중 하나인 것 같아서, 또 이게 Repast Simphony 에서도 사용되는 것 같아서, 이걸 먼저 공부해보기로 했다.

일단은 네트워크를 표현하는 기본적인 자료형이 있어야 할 것이다. 이 자료형들은 jung-api 프로젝트에 구현되어 있다.

\1. 기본적으로 Graph 인터페이스가 있는데, 이것은 Hypergraph 인터페이스를 상속받은 것이다. 이 Hypergraph 안에 웬만한 메쏘드들은 대부분 구현이 되어 있는 듯 하다.

1-1. 이 Graph 인터페이스를 상속받은 것이 DirectedGraph 와 UndirectedGraph 이다. 이 중에서 DirectedGraph 를 상속한 Forest 인터페이스가 있는데, 이건 collection of rooted directed acyclic graphs 라고 설명되어 있다. 또 이 Forest 를 상속받은 Tree 인터페이스가 있다. 

1-2. Graph 인터페이스를 구현한 또다른 것이 GraphDecorator 인데, 설명에는 An implementation of Graph that delegates its method calls to a constructor-specified Graph instance.  This is useful for adding additional behavior (such as synchronization or unmodifiability) to an existing instance. 라고 되어 있다. 

1-3. Graph 인터페이스를 상속받은 또 다른 인터페이스로 KPartiteGraph 가 있다. 설명이 An interface for graphs whose vertices are each members of one of 2 or more disjoint sets (partitions), and whose edges connect only vertices in distinct partitions. 라고 되어 있다. 

1-4. 또 이 GraphDecorator 를 상속받은 클래스가 ObservableGraph 라는 것이 있다. 이건 설명에는 A decorator class for graphs which generates events 라고 되어 있다. 

\2. 그리고 별도로 Multigraph 인터페이스가 있다. 이것은 이름 그대로 parallel edge 가 허용되는 그래프 유형이고, Graph 인터페이스를 상속하거나 구현하지 않고 별도로 마련되어 있다. 

