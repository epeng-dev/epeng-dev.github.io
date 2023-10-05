---
title: "우분투에서 한글 zip 파일을 열 때 깨지는 문제 수정 방법"
categories:
  - Ubuntu
tags:
  - Ubuntu
  - Ubuntu 22.04
  - nautilus
  - unzip
  - 한글 깨짐
  - zipinfo
---
평소에 나는 개발환경으로 리눅스를 애용하는 편이다.  
일단 윈도우보다 빠르며 많은 개발 툴이 리눅스 쪽을 지원하고 이 환경이 익숙해서 윈도우로 개발은 생각도 안하고 있다.  
(그래도 Mac OS 쓰고 싶다. 맥 스튜디오 사고 싶다.)

하지만 종종 불편한 사항들이 있기도 한데 그 중에 하나였던 압축 파일 이름 깨짐이 있었다.
기본적으로 반디집 같은 압축 프로그램을 이용하지 않고 윈도우 기본 압축을 하게 되면 CP949로 인코딩 되게 된다.
- 반디집에 경우에는 기본값으로 확장필드에 UTF-8 파일명을 저장하기 때문에 어떤 시스템 언어나 프로그램이라도 거의 정상적으로 보인다.
- 출처: [https://kr.bandisoft.com/bandizip/help/utf8/](https://kr.bandisoft.com/bandizip/help/utf8/)
![마소 또 너야 이이익](/assets/images/2023-10-24-unzip_ecu_kr/hangul_crash.png)


따라서 나는 한국기업에서 한국인들과 같이 일하기 때문에 기본적으로 zip 파일을 CP949로 열려고 한다. 따라서 bashrc에다가 해당 내용을 적용하려고 한다.
- 해당 내용은 .profile이든 .bashrc든 부팅 시 실행시키는 스크립트에다가 넣으면 된다.  

~~~~ bash
export UNZIP="-O cp949"
export ZIPINFO="-O cp949"
~~~~

해당 환경변수는 unzip, zipinfo 유틸리티의 기본값을 지정하는 변수들이다.
- man 페이지에 Environment Options 항목에 나와있다.
- [unzip man page](https://linux.die.net/man/1/unzip)
- [zipinfo man page](https://linux.die.net/man/1/zipinfo)

-O cp949는 Windows의 CP949로 디코딩하게 해준다.
- -O CHARSET  specify a character encoding for DOS, Windows and OS/2 archives

![키야 잘 된다](/assets/images/2023-10-24-unzip_ecu_kr/hangul_success.png)

해당 해결 방법의 출처: [https://daechu.tistory.com/12](https://daechu.tistory.com/12)