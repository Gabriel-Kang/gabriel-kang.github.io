---
layout: single
title: 우분투에 NVIDIA DIGITS 4 설치 
category:
 - Deep Learning
tags:
 - DIGITS
 - NVIDIA
 - Deep Learning
 - Caffe
 - Ubuntu
summary: 우분투 14.04에서 NVIDIA DIGITS 설치하기.
---

# 개요

---
Due date이 앞으로 3일 남은 엔비디아코리아 이미지 인식 컨테스트에 참여하기 위해, 무슨 딥러닝 프레임워크를 이용할지 고민을 하다, 가장 빠르고 간편하게 구현이 가능한 NVIDIA DIGITS을 이용하기로 결정했다. DIGITS은 이미 예전에도 여러번 설치한 적이 있으나, 그 동안 버전이 많이 업데이트 되었기에 이번에 새로 설치하면서 기록을 남기고자 한다.

# 설치

- - -

DIGITS은 사실 딥러닝 프레임워크가 아니라, Caffe 또는 Torch를 이용한 학습을 편하게 도와주기 위한 UI를 제공하는 툴이다. 따라서, DIGIT을 설치하기 할 때, Caffe나 Torch도 함께 설치를 해야한다. (Caffe 기준) 단, 이 때 설치되는 Caffe는 DIGITS에 맞게 조금 변현된 버전이라, 만약 기존에 Caffe가 설치되어 있더라도, [NVIDIA/caffe.git](https://github.com/NVIDIA/caffe.git)의 Caffe를 추가로 설치해야한다.

다음은 DIGITS을 설치하기 위한 단계이다.
1. DIGITS Dependencies 설치
1. NVIDIA's Caffe 설치.
1. DIGITS 소스코드 다운로드.
1. 환경설정
1. 실행

## DIGITS Dependencies 설치
먼저 DIGITS 설치를 위해 필요한 패키지를 설치한다.(참고: 이 dependency는 계속해서 변경될 수 있으므로, [공식 DIGITS 깃허브 설치페이지](https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildDigits.md)를 참고한다.)

    sudo apt-get install --no-install-recommends git graphviz gunicorn python-dev python-flask python-flaskext.wtf python-gevent python-h5py python-numpy python-pil python-protobuf python-scipy

## NVIDIA's Caffe 설치
NVIDIA's Caffe를 설치하기 위한 dependencies는 다음과 같다.

    sudo apt-get install --no-install-recommends build-essential cmake git gfortran libatlas-base-dev libboost-all-dev libgflags-dev libgoogle-glog-dev libhdf5-serial-dev libleveldb-dev liblmdb-dev libopencv-dev libprotobuf-dev libsnappy-dev protobuf-compiler python-all-dev python-dev python-h5py python-matplotlib python-numpy python-opencv python-pil python-pip python-protobuf python-scipy python-skimage python-sklearn
    
Caffe를 잘 활용하기 위해서는 최신 CUDA, cuDNN 라이브러리 설치 필요하다. 해당 라이브러리 설치 방법은 본 포스팅에서는 생략한다.

소스코드는 자신이 원하는 path의 하위폴더 NVCaffe(변경가능)에 소스코드를 복사한다.
`git clone https://github.com/NVIDIA/caffe.git NVCaffe`

이후 과정의 편의를 위해 `$CAFFE_HOME` 환경변수를 설정하고, Caffe의 Dependency를 설치한다.
    export CAFFE_HOME=./NVCaffe
    sudo pip install -r $CAFFE_HOME/python/requirements.txt

**만약, PC에 다른 버전의 caffe가 이미 설치되어, `$CAFFE_HOME`이 이미 다른 경로로 설정되어 있다면, DIGITS이 해당 경로의 caffe를 잘못 인식 할 수 있으므로, `$CAFFE_HOME` 환경변수를 현재 다운로드한 소스코드 경로로 변경해준다.**

이제, CMake를 이용하여 caffe를 빌드한다.

    cd $CAFFE_HOME
    mkdir build
    cd build
    cmake ..
    make --jobs=4

## DIGITS 소스코드 다운로드
[DIGITS Github](https://github.com/NVIDIA/DIGITS) 의 소스코드를 원하는 로컬 path에 다음과 같이 복사한다.
`git clone https://github.com/NVIDIA/DIGITS`
현재 path 아래, DIGITS이란 하위 폴더에 깃허브의 소스코드가 다운로드 된다.

다음의 명령으로 필요한 파이썬 패키지들을 설치한다.
`sudo pip install -r $DIGITS_HOME/requirements.txt`

DIGITS은 별도의 빌드가 필요없고, 깁허브에서 다운로드된 바이너리로 실행시킬 수 있다.

## 환경설정

DIGITS을 실해 시키기 전에, `-c` 옵션으로 환경설정을 할 수 있다. 대부분의 옵션은 디폴트(엔터)를 사용하면 되고, 만약 다른 버전의 caffe가 시스템에 설치되어 있을 때, 방금 설치한 NVCaffe를 DIGITS에서 사용할 수 있게 새로 설치한 NVCaffe path를 입력해 준다.

    ./digits-devserver -c
    
    ...other options
    
    ==================================== Caffe =====================================
	Where is caffe installed?

	Suggested values:
	(P*) [PATH/PYTHONPATH] <PATHS>
	>> /home/userid/NVCaffe
	Using "/home/userid/NVCaffe"
    
## 실행

`digits-devserver` 바이너리를 실행하면 DIGITS 웹서버가 로컬호스트의 5000번 포트에서 동작하게된다. 만약 실행할 포트를 바꾸고자 하면 `./digits-devserver -p 1234` 와 같이 포트번호 옵션을 주고 실행시키면 된다.

웹브라이저를 실행시키고 주소창에 `http://localhost:5000` 와 같이 입력하면 아래와 같은 메인 화면에 접속 할 수 있다.

![DIGITS 메인화면]({{ site.url }}/assets/digit_main.JPG)

## 실행 오류

나의 경우에 `./digits-devserver` 를 실행 시켰을 때 protobuf 에서 에러가 발생했다.(에러메시지는 저장을 안해둠.)
인터넷을 찾아보니, caffe에서 필요로하는 버전과 실제 시스템에 설치된 protobuf 버전이 일치하지 않아서였는데, protobuf를 언인스톨 후, caffe 설치시 사용한 패키지 리스트로 다시 재설치 하니 정상 동작하였다.
