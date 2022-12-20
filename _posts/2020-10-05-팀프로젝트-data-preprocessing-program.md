---
layout: post
author: Ju Heesong
tags: [project, data, preprocessing]
---


# 데이터 전처리 통합 공유 플랫폼 팀 프로젝트


본 프로젝트는 서울시 뉴딜일자리 빅데이터 전문가 양성 과정에서 진행되었던 프로젝트로 <Day Share> 라는 데이터 전처리 통합 공유 플랫폼을 개발하고자 하였다.

## 주요기능

- 회원가입을 통한 회원DB와 얼굴인식 데이터 저장 및 로그인
- 데이터 파일 업로드 및 위치 API저장
- 데이터 결측치 처리 시스템

사용방법:

1. 회원가입을 통해 아이디, 비밀번호, 이름, 얼굴 등록 가능
2. 아이디, 비밀번호를 통해 로그인한 후 얼굴인식으로 데이터 접근
3. 파일 업로드 기능
4. 사용하고자 하는 데이터에서 원하는 결측치 처리 가능

## 구현 및 코드 설명

- 회원가입 화면
 
 1.회원정보를 입력하고 저장

![theme logo](http://ju-ffi.github.io/assets/images/favicon/회원가입.png)

- 저장된 회원데이터를 기반으로 로그인

![theme logo](http://ju-ffi.github.io/assets/images/favicon/로그인.png)

- 데이터 업로드 화면
1. 원하는 데이터 파일을 선택하여 업로드
2. 파일에 접근하려면 얼굴 인식 보안을 통해 접근 가능

![theme logo](http://ju-ffi.github.io/assets/images/favicon/마이페이지 업로드.png)

- 데이터 전처리 화면
1. 원하는 데이터 요약을 확인
2. 결측치, 이상치 여부 확인
          
![theme logo](http://ju-ffi.github.io/assets/images/favicon/결측치처리.png)
          
- 데이터 전처리 결과 확인
          
![theme logo](http://ju-ffi.github.io/assets/images/favicon/결과확인.png)
