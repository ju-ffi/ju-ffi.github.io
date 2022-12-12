---
layout: post
author: Ju Heesong
tags: [restfulapi, project, portfolio]
---

# Restful API를 활용한 디지털 라이브러리 프로그램

본 프로그램은 실험을 통해 수집한 데이터를 서버에 저장하고 모니터링하며 데이터 관리 기능을 수행하는 web기반의 디지털라이브러리 프로그램으로 Flutter를 활용하여 구현하였다.

## 주요기능


- 실험데이터 DB관리 기능
- 각 실험 물질별 데이터 특징 및 구조도 명시
- 데이터별로 그래프 시각화

사용방법:

1. 서버에서 동작하고 있으며, web 주소로 접근 가능
2. 첫 web 실행 화면에 각 실험 물질이 카드형식으로 나타남
3. 물질 카드를 클릭하면 해당 물질에 대한 상세 내용 확인 가능
4. Data Info는 해당 물질의 화학적 특성으로 서버에서 get한 데이터이며, 오른쪽 상단의 연필모양 아이콘으로 수정 가능
5. Data File은 서버에 업로드된 데이터 목록을 나타내며, 오른쪽 상단 + 아이콘을 클릭하여 서버에 파일을 추가 업로드 및 쓰레기통 아이콘으로 서버에서 삭제 가능
6. Ion Mobility Spectrometry는 각 물질 데이터를 그래프로 시각화한 것으로 Data File에서 원하는 파일을 클릭했을 때 실시간으로 확인 가능


## 구현 및 코드 설명

![theme logo](http://ju-ffi.github.io/assets/images/favicon/P1실행화면.PNG)

Now some code:

```
const ultimateTruth = 'follow middlepath';
console.log(ultimateTruth);
```

And here is some `inline code`!

