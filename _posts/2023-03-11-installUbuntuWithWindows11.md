---
title: "[linux] 윈도우11에 가상머신으로 우분투 설치하기"
excerpt: "윈도우11에 가상머신으로 우분투 설치하기"

categories:
  - linux
tags:
  - [linux]

permalink: /linux/installUbuntuWithWindows11/

toc: true
toc_sticky: true

date: 2023-03-11
last_modified_at: 2023-03-11
---

저는 마리아DB를 사용합니다. 가볍고 빠르고 라이센스에서 자유롭고 등의 이유가 있겠지만 가장 큰 이유는 '로고가 귀여워서'입니다. 마리아DB 로고는 강치(바다 사자의 한 종류)입니다.

리눅스 로고는 펭귄입니다. 이름은 턱스(Tux). 리눅스를 만든 리누스 토르발스 씨가 정했다고 합니다. 토르발스 씨는 리눅스와 git을 만드는 등 컴퓨터 과학에 혁혁한 공을 세웠습니다. 그렇지만 저는 토르발스 씨의 가장 큰 업적은 턱스를 선택한 것이라고 생각합니다. 정말이지 미친듯이 귀엽습니다 ㅠㅠ!

> 빠른 설치를 원하시면 **linux 환경 구축**부터 보시면 됩니다.

![LinuxOnvirtualMachine](/assets/images/posts_img/LinuxOnvirtualMachine.png)

## 리눅스란?

'리눅스'란 '리눅스 커널'만을 의미하는 용어입니다. 커널이란 운영 체제 중심에서 하드웨어를 제어하는 역할을 담당하는 소프트웨어를 말합니다. 사용자가 사용하는 도구나 애플리케이션은 포함되지 않습니다.

일반적으로 "리눅스!"라고 하면 '넓은 의미의 리눅스를 의미합니다. '넓은 의미의 리눅스'란 리눅스 커널과 기본적인 명령어, 애플리케이션을 묶어서 사용자가 바로 사용 할 수 있게 패키징한 것입니다. '리눅스 배포판'이라고도 합니다.

## 리눅스 배포판

리눅스 배포판은 대표적으로 레드 햇(Red Hat)과 데비안(Debian) 계열로 나뉩니다. 우분투는 편의성이 좋아 인기가 매우 많습니다.

| 계열         | 배포판                                   |
| ------------ | ---------------------------------------- |
| Red Hat 계열 | Red Hat Enterprise Linux, CentOS, Fedora |
| Debian 계열  | Denian GNU/Linux, **Ubuntu**             |

---

<br>

## 우분투 환경 구축 전 알아두면 좋은 것들

디스크를 분할하여 우분투를 설치하지 않고, 가상 머신에 우분투 환경을 구축합니다. 오라클이 제공하는 Oracle VM VirtualBox(가상화 소프트웨어)를 사용합니다. 설치에 앞서 간단하게 용어를 알아보겠습니다.

### 호스트 OS

가상화 소프트웨어를 돌리는 OS를 말합니다.

### 게스트 OS

가상화 소프트웨어에 의해 만들어진 OS를 말합니다.

저는 windows에 Oracle VM VirtualBox를 통해 Ubuntu를 설치하겠습니다. 정리하면 아래 표와 같습니다.(macOS에도 동일한 방법으로 설치할 수 있습니다.)

| 역할              | 제품명과 버전        |
| ----------------- | -------------------- |
| 호스트 OS         | Windows11 Home 22H2  |
| 가상화 소프트웨어 | Oracle VM VirtualBox |
| 리눅스 배포판     | Ubuntu 20.04.01      |

---

<br>

## 우분투 환경 구축

### ①VitualBox 다운로드

가상화 소프트웨어인 Oracle VM VirtualBox를 다운로드 합니다. [다운로드🧷](https://www.virtualbox.org/)

![LinuxOnvirtualMachine1](/assets/images/posts_img/LinuxOnvirtualMachine1.png)

![LinuxOnvirtualMachine2](/assets/images/posts_img/LinuxOnvirtualMachine2.png)

### ②VitualBox 설치

`Next`를 세 번 누르고 `Yes`를 선택합니다. 이후 `Install`과 `Finish`를 누르면 설치가 완료됩니다.

![LinuxOnvirtualMachine3](/assets/images/posts_img/LinuxOnvirtualMachine3.png)

![LinuxOnvirtualMachine4](/assets/images/posts_img/LinuxOnvirtualMachine4.png)

![LinuxOnvirtualMachine5](/assets/images/posts_img/LinuxOnvirtualMachine5.png)

![LinuxOnvirtualMachine6](/assets/images/posts_img/LinuxOnvirtualMachine6.png)

네트워크 어댑터 설치 여부를 물어보는 화면입니다. **Yes**를 선택합니다.

![LinuxOnvirtualMachine7](/assets/images/posts_img/LinuxOnvirtualMachine7.png)

![LinuxOnvirtualMachine8](/assets/images/posts_img/LinuxOnvirtualMachine8.png)

![LinuxOnvirtualMachine9](/assets/images/posts_img/LinuxOnvirtualMachine9.png)

![LinuxOnvirtualMachine10](/assets/images/posts_img/LinuxOnvirtualMachine10.png)

### ③우분투 이미지 파일(ISO) 다운로드

이미지 파일(ISO 파일)은 CD나 DVD 등 디스크를 파일로 만든 것을 말합니다. ~~CD나 DVD를 알고 있다면 최소 90년생..~~ 우분투 공식 홈페이지에서 이미지 파일을 다운로드 합니다. [다운로드🧷](https://ubuntu.com) 저는 20.04 LTS를 다운로드 했습니다.(파일 크기가 크기 때문에 잠시 화장실을 다녀와도 됩니다.)

**저는 22.04 LTS가 `linux-image-5.15.0-52 generic 설치 오류`를 발생시켰습니다. 그래서 저는 20.04.01을 다운받았습니다. [다운로드🧷](http://old-releases.ubuntu.com/releases/20.04.1/)**

![LinuxOnvirtualMachine11](/assets/images/posts_img/LinuxOnvirtualMachine11.png)

![LinuxOnvirtualMachine12](/assets/images/posts_img/LinuxOnvirtualMachine12.png)

### ④Virtual Box에서 가상 머신 만들기

버추얼박스(Oracle VM VirtualBox)를 사용해 가상 머신을 만듭니다. 아래 순서와 스크린샷을 따라서 설치합니다.

1. `New`를 선택합니다.
2. 가상 머신의 이름과 종류, 버전을 선택합니다.
3. 가상 머신에 할당할 메모리를 설정합니다.(최소 1024MB) 정도 할당합니다.
4. `지금 새 가상 하드 디스크 만들기(C)`를 선택하고 `만들기`를 선택합니다.
5. 하드 디스크 파일 종류는 기본값인 `VDI(VirtualBox 디스크 이미지)`를 선택합니다.
6. `동적 할당`을 선택합니다.
7. 파일의 위치 및 크기에서는 10GB 정도 할당합니다.
8. `시작(T)`을 선택하여 가상 머신을 시작합니다.
9. 다운로드한 ISO 파일을 선택하고 시작합니다.

<br>

**New를 선택합니다.**

![LinuxOnvirtualMachine13](/assets/images/posts_img/LinuxOnvirtualMachine13.png)

![LinuxOnvirtualMachine14](/assets/images/posts_img/LinuxOnvirtualMachine14.png)

**가상 머신에 할당할 메모리를 설정합니다. 최소 1024MB 할당해야합니다.**

![LinuxOnvirtualMachine15](/assets/images/posts_img/LinuxOnvirtualMachine15.png)

![LinuxOnvirtualMachine16](/assets/images/posts_img/LinuxOnvirtualMachine16.png)

![LinuxOnvirtualMachine17](/assets/images/posts_img/LinuxOnvirtualMachine17.png)

![LinuxOnvirtualMachine18](/assets/images/posts_img/LinuxOnvirtualMachine18.png)

**파일 크기를 선택합니다. 10GB면 무난합니다.**

![LinuxOnvirtualMachine19](/assets/images/posts_img/LinuxOnvirtualMachine19.png)

**Start를 누릅니다.**

![LinuxOnvirtualMachine20](/assets/images/posts_img/LinuxOnvirtualMachine20.png)

**폴더 모양 아이콘을 선택해 디스크를 검색합니다.**

![LinuxOnvirtualMachine21](/assets/images/posts_img/LinuxOnvirtualMachine21.png)

**Add를 선택합니다.**

![LinuxOnvirtualMachine22](/assets/images/posts_img/LinuxOnvirtualMachine22.png)

![LinuxOnvirtualMachine23](/assets/images/posts_img/LinuxOnvirtualMachine23.png)

**Choose를 선택합니다.**

![LinuxOnvirtualMachine24](/assets/images/posts_img/LinuxOnvirtualMachine24.png)

**Start를 선택합니다.**

![LinuxOnvirtualMachine25](/assets/images/posts_img/LinuxOnvirtualMachine25.png)

### ⑤우분투 설치

④까지 잘 하셨다면 잠시 기다려줍니다. 아래 스크린샷을 따라 설치합니다. 만약 `계속하기`버튼이 보이지 않는다면, 3-1에서 문제를 해결합니다.

1. 언어를 선택합니다.
2. 키보드 레이아웃을 설정합니다.
3. 업데이트 및 기타 소프트웨어를 선택합니다.
   3-1. `계속하기`버튼이 보이지 않는 경우
   3-2. X 표시를 눌러 설치 프로그램을 종료합니다.
   3-3. 바탕화면에서 우클릭하여 Display Setting을 선택합니다.
   3-4. 해상도를 조절하고 적용합니다.
   3-5. 설치프로그램을 다시 실행시킵니다.
4. 설치 형식을 선택합니다.
5. 파티션 포맷 여부를 선택합니다.
6. 거주 지역을 확인합니다.
7. 사용자 계정 정보를 입력합니다.

<br>

**가만히 있어도 다음 화면으로 넘어갑니다.**

![LinuxOnvirtualMachine26](/assets/images/posts_img/LinuxOnvirtualMachine26.png)

![LinuxOnvirtualMachine27](/assets/images/posts_img/LinuxOnvirtualMachine27.png)

![LinuxOnvirtualMachine28](/assets/images/posts_img/LinuxOnvirtualMachine28.png)

![LinuxOnvirtualMachine29](/assets/images/posts_img/LinuxOnvirtualMachine29.png)

![LinuxOnvirtualMachine30](/assets/images/posts_img/LinuxOnvirtualMachine30.png)

![LinuxOnvirtualMachine31](/assets/images/posts_img/LinuxOnvirtualMachine31.png)

> `계속하기` 버튼이 보이지 않습니다. 창을 최대화하고, 설치 소프트웨어를 종료(X 표시)합니다.

![LinuxOnvirtualMachine32](/assets/images/posts_img/LinuxOnvirtualMachine32.png)

![LinuxOnvirtualMachine33](/assets/images/posts_img/LinuxOnvirtualMachine33.png)

> 해상도를 조절하고 다시 설치 프로그램을 시작합니다. `계속하기` 버튼이 생겼습니다!!

![LinuxOnvirtualMachine34](/assets/images/posts_img/LinuxOnvirtualMachine34.png)

![LinuxOnvirtualMachine35](/assets/images/posts_img/LinuxOnvirtualMachine35.png)

![LinuxOnvirtualMachine36](/assets/images/posts_img/LinuxOnvirtualMachine36.png)

![LinuxOnvirtualMachine37](/assets/images/posts_img/LinuxOnvirtualMachine37.png)

우여곡절 끝에 가장 어려운 설치가 끝났습니다! 이제 우분투를 즐길 일만 남았습니다 :)

![LinuxOnvirtualMachine38](/assets/images/posts_img/LinuxOnvirtualMachine38.png)

## 참고문헌

**모두의 리눅스**

미야케 히데아키 , 오스미 유스케 지음ㅣ길벗ㅣ2021ㅣ[**도서 정보**](https://product.kyobobook.co.kr/detail/S000001834763)
