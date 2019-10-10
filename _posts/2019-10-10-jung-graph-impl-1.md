---
layout: post
title: "[JUNG] 2-1. Add Node & Add Edge"
date: 2019-10-10 15:40
categories: 프로그래밍
tags: 
  - java
  - jung
  - graph
  - network
  - node
---

애초에는 jung-graph-impl 프로젝트에 있는 그래프 구현을 살펴보려고 했는데, 이게 워낙 많기도 하고 복잡해서, 이걸 다 보고 있자면 시간이 너무 많이 걸릴 것 같다. 그래서 jung-samples 프로젝트 안에 있는 여러 샘플들을 살펴보면서, 그때그때 필요한 자료형들을 찾아서 공부하는 것이 낫겠다는 생각을 했다. 

가장 먼저는 당연히 네트워크를 만들고 노드와 링크를 추가하는 것이다. jung-sample 프로젝트의 가장 위에 있는 것이 (이름 때문에 그렇겠지만) AddNodeDemo.java 클래스이다. 

우선 네트워크를 만들어야 할텐데, 사실 여기부터가 선택과 판단이 들어간다. 여러 가지의 그래프 유형 가운데 무엇을 선택할 것인가 하는 문제이다. 샘플에는 이렇게 되어 있다. 

```java
public class AddNodeDemo extends javax.swing.JApplet {
    ...
    private Graph<Number,Number> g = null;
    ...
    public void init() {
      //create a graph
    	Graph<Number,Number> ig = Graphs.<Number,Number>synchronizedDirectedGraph(new DirectedSparseMultigraph<Number,Number>());

      ObservableGraph<Number,Number> og = new ObservableGraph<Number,Number>(ig);
      ...
      this.g = og;
      ...

    }

    Integer v_prev = null;

    public void process() {
      ...
      //add a vertex
      Integer v1 = new Integer(g.getVertexCount());
      ...
      g.addVertex(v1);
      ...
      // wire it to some edges
      if (v_prev != null) {
          g.addEdge(g.getEdgeCount(), v_prev, v1);
          // let's connect to a random vertex, too!
          int rand = (int) (Math.random() * g.getVertexCount());
          g.addEdge(g.getEdgeCount(), v1, rand);
      }

      v_prev = v1;
      ...
    }
...
}
```

먼저 클래스 속성으로 Graph (jung-api 프로젝트의 jung.graph 패키지) 인터페이스의 객체 `g`를 만들어서 null 값을 넣어 놓는다. 그리고 이와 별도로 `ig`라는 이름의 객체를 만드는데, 이를 위해 먼저 `DirectedSparseMultigraph` 클래스의 객체를 하나 만들고, 그것을 Graphs 클래스(jung-api 프로젝트의 jung.graph.util 패키지)의 `synchronizedDirectedGraph()` 함수의 인자로 받는다. 하나씩 보자면,

1\. `DirectedSparseMultigraph` 클래스

설명에는 An implementation of DirectedGraph, suitable for sparse graphs,that permits parallel edges 라고 되어 있다. 이름 그대로, directed 링크를 갖고, 네트워크가 sparse 하며, 노드간 여러 개의 링크를 가질 수 있는 네트워크인 것 같다. 

2\. `synchronizedDirectedGraph()` 함수

함수가 선언되어 있기는 하지만, 그냥 DirectedGraph 를 입력으로 받아서 SynchronizedDirectedGraph 를 반환하는 내용만 있다. 아마도 그래프 사이의 동기화와 관련된 별도의 작업이 있는 모양이다. 추후에 공부해야 할 듯.

