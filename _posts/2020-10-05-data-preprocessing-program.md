---
layout: post
author: Ju Heesong
tags: [project, data, simulator]
---


# 데이터 검출 시뮬레이터 프로그램


본 프로그램은 실험을 통해 수집한 데이터를 기반으로 이용하고 있는 센서에 특정 물질이 들어왔을 때 이를 감지하고 검출하기 위한 시뮬레이터로, Flutter를 활용하여 구현하였다.

## 주요기능

- 실험데이터를 시간에 따른 그래프로 구현하여 원하는 물질 검출 가능
- 그래프에서 물질 데이터를 찾은 후 경보를 통해 알람
- 물질의 화학적 데이터 확인 가능

사용방법:

1. Windows 프로그램으로 실행 가능
2. 첫 실행화면에서는 원하는 실험 데이터 파일을 선택
3. 플레이버튼을 클릭하여 그래프 재생
4. 데이터에서 특정 물질이 검출될 경우, 경보 알람
5. 값 또는 물질 확인을 위해 그래프 멈춤, 재생 동작 가능

## 구현 및 코드 설명
(본 코드는 프로젝트 유출금지로 일부의 코드만 변형 및 기재하였습니다.)

- Windows 실행화면

화면구성:
- 왼쪽상단에서 사용자 이름 확인 가능
- 오른쪽 상단에서 그래프 파일 추가
- Play 버튼 클릭으로 그래프 재생 및 멈춤 기능
- 파일 패스 및 물질 검출시 경보 알람

![theme logo](http://ju-ffi.github.io/assets/images/favicon/p2실행화면.png)

- 데이터 파일 선택 후 graph play
1.데이터의 frame 주기를 확인하여 설정한 후, 그래프가 시간에 따라 변하도록 Timer 활용.

![theme logo](http://ju-ffi.github.io/assets/images/favicon/p2graphplay.png)

Now some code:

```javascript
Timer.periodic(
          Duration(milliseconds: frameTimeMs), (Timer t) => _drawchart());
```

- 실험 물질 검출 화면
1. 물질의 종류와 함께 경보 알람
2. 기존의 chart 라이브러리에 있는 tooltip이 사용하는 UI와 맞지 않아 직접 paint을 이용해 그려서 생성

![theme logo](http://ju-ffi.github.io/assets/images/favicon/p2peak.png)
Now some code:

```javascript
...
  final Paint paint = Paint()
      ..color = color
      ..strokeWidth = 3.0
      ..style = PaintingStyle.fill;

    final Path mark = Path()
      ..moveTo(size.width / 2, size.height)
      ..lineTo(hw - hth, size.height - th)
      ..lineTo(rw, size.height - th)
 ...
```
