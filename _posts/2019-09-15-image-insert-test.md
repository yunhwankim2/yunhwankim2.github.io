---
layout: post
title: "이미지 넣기 테스트"
date: 2019-09-15 12:04
categories: 테스트
tags: 
  - 테스트
---

이미지 넣기를 테스트하기 위해 만든 포스트입니다.

{% include image.html url='{{"/assets/image/sh1.jpg"| relative_url}}' description='그림 1. 처리전' alt='Image Alt 텍스트' %}

위의 그림은 처리하기 전의 그림입니다.

{% include image.html url='{{"/assets/image/sh2.jpg"| relative_url}}' description='그림 2. 처리후' alt='Image Alt 텍스트' %}

위의 그림은 처리한 후의 그림입니다.
