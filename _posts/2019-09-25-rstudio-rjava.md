---
layout: post
title: "RStudio 에서 rJava 설치시 오류 해결(macOS)"
date: 2019-09-25 22:46
categories: 프로그래밍
tags: 
  - R
  - RStudio
  - rJava
  - KoNLP
---
며칠 전, 수업 듣는 한 학생이 다른 수업에서 직면한 문제를 해결하는데 도움을 요청해왔다. R 에서 한국어 자연어처리에 많이 쓰이는 KoNLP 라이브러리를 맥 컴퓨터에 설치하려고 하는데 잘 안된다는 것이다. 그 수업의 담당 교수님께서도 아직 해결책을 주지 못하셨고 구글링을 해봐도 잘 모르겠다면서, 혹시 해결책을 알고 있느냐는 질문이었다. 앉은 자리에서 대충 살펴봤지만 쉽게 해결되지 않았다. 집에 돌아와서 이것저것 살펴보고 시도해본 끝에, 간신히 답을 얻었다.

일단, 이 문제는 KoNLP 이전에 설치되어야 하는 rJava 의 설치 과정에서 오는 문제인 것 같다. 

RStudio 로 들어가서 rJava 라이브러리를 설치한 다음,
```R
> library(rJava) 
```
라고 하면, 뭐가 안된다고 길게 오류 메시지가 나온다. 이 오류 메시지로부터 찾아내야 하는 정보들이 있다. 

1. 첫번째 정보는 libjvm.dylib 이라는 파일을 어디서 찾으려고 시도했는가 하는 것이다. 오류 메시지에 '어디어디서 libjvm.dylib 을 찾으려 했지만 없다'라는 식의 메시지가 있을 것이다. 내 경우에는 
`/Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home/lib/server/libjvm.dylib`  
위의 경로에서 찾으려고 했다고 나온다. 아마 중간의 jdk-11.0.1.jdk 의 번호는 jdk 버전에 따라 다를 것이다. 
2. 두번째 정보는, 본인의 /Library/Java/JavaVirtualMachines 에서 위 1번의 libjvm.dylib 파일이 실제로 있는 경로를 찾아내는 것이다. 맥의 파인더를 통해서 저 파일이 있는 곳의 경로를 찾으면 된다. 내 경우에는
`/Library/Java/JavaVirtualMachines/jdk-11.0.4.jdk/Contents/Home/lib/server/libjvm.dylib`  
이 경로에 libjvm.dylib 파일이 있었다.
3. 세번째 정보는, rJava.so 라는 파일로부터 이런 명령이 나온 것인데, 그 rJava.so 의 경로를 찾아내는 것이다. 이것은 오류 메시지를 잘 보면 있다. 내 경우에는 
`/Library/Frameworks/R.framework/Versions/3.6/Resources/library/rJava/libs/rJava.so`  
이라고 오류 메시지에 나온다. 아마 크게 다르지 않을 것이다.

실제 문제 해결은 여기부터이다. 일단 터미널을 열어서 
```bash
$ install_name_tool -change \
   (1에서 얻은 경로) \
   (2에서 얻은 경로) \
   (3에서 얻은 경로)
   ```
이렇게 입력하면 된다. (참고로 RStudio 에서 libary(rJava) 해서 안됐다고 해서 그걸 지우면 안된다.)

내 경우는 아래와 같이 입력했다.
```bash
$ install_name_tool -change \
/Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home/lib/server/libjvm.dylib \
/Library/Java/JavaVirtualMachines/jdk-11.0.4.jdk/Contents/Home/lib/server/libjvm.dylib \
/Library/Frameworks/R.framework/Versions/3.6/Resources/library/rJava/libs/rJava.so
```

이건 지금 R 프로그램이 libjvm.dylib 파일을 찾으려고 시도하고 있는 경로가 1)인데, 그걸 2)로 바꾸라는 의미인 것 같다.

아래 링크를 참고했다.  
<https://github.com/s-u/rJava/issues/151#issuecomment-395070694>
