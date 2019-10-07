---
layout: post
title: "[JUNG] 1-2. 그래프 이벤트"
date: 2019-10-06 16:35
categories: 프로그래밍
tags: 
  - java
  - jung
  - graph
  - network
  - event
---

 jung-api 프로젝트 안에는 jung.graph 패키지 외에도 jung.graph.event 라는 패키지도 있다. 이 안에는 우선 GraphEvent 클래스가 있다. 이 안에는 Type 이라는 열거형(enum) 안에 네 가지의 그래프 이벤트가 있는데, VERTEX_ADDED, VERTEX_REMOVED, EDGE_ADDED, EDGE_REMOVED 인 걸 보니, 아마도 그래프에 일어난 사건들을 탐지하기 위해 만든 것이 아닌가 싶다. 물론 실제 탐지 기능은 다른 클래스로 위임한 것 같고.

 그렇게 위임 받은 것이 아마도 GraphEventListener 인터페이스인 것 같다. 이후에 이 인터페이스를 구현한 클래스를 만들어서 실제 이벤트 탐지 작업을 하게 될 것 같다. 특이한 것은 java.util.EventListener 클래스를 상속받는다는 점이다. 이 EventListener 인터페이스는, 이벤트가 발생했을 때 그것을 탐지하고 그에 따라 어떤 액션을 취하는 방식의 클래스들이 모두 이 인터페이스를 구현해야 한다고 되어 있는 걸 보니, 매우 기본적인 액션을 정의해놓은 인터페이스인 것 같다. 

 