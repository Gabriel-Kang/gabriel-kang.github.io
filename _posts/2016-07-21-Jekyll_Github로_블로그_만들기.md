---
layout: post
title: Jekyll + Github로 블로그 만들기 (for Windows 10)
---

#개요
여러가지 프로그래밍 작업 및 공부를 하면서, 그 중간 과정(=삽질)에 대한 기록을 해놔야겠다는 필요성 때문에 블로그를 만들어야겠다는 생각을 하게 됐다.
그러던 중, 우연히 회사 동료가 GitHub를 이용해서 무료로 블로그를 만들 수 있는 Jekyll이라는 툴을 쓰는 걸 보고, 깃헙에 블로깅을 하는게 왠지 굉장히 쿨하게 느껴져서 이렇게 만들게 됐다.
간단히 Jekyll과 GitHub으로 블로그를 만들면 좋은 점에 대해 기술하자면 다음과 같다.
* 블로그에 올릴 글들을 로컬에서 작성 및 편집 한 후 원할 때 블로그에 게시 할 수 있다.
* 블로그 글들을 로컬에 저장하여 관리 할 수 있다. 이 것은 추후 마이그레이션 등을 할 때 큰 이점이 된다.
* Git을 이용하여 블로그 글들의 버전 관리가 가능하다.
예상되는 단점은.. 
* 블로그 방문자와의 소통이 가능한지..(댓글 등의 기능이 지원하는지 잘 모르겠다.)
* 블로그 글이나 사진 파일들의 정리를 직접 해야 된다.
* 검색, 태그, 꾸미기 등의 기능 지원

아마도 예상되는 단점에 대한 것은 찾아보면 다 편한 방법이 있을 것 같다. 일단 설치 후 써보면서 하나하나 기능을 알아가보자.

#환경
Jekyll을 설치하기 위한 현재 상태는 다음과 같다.
* Ubuntu 14.04 && Windows 10 (주로 사용하는 PC 와 Laptop에 모두 설치)
* GitHub 계정 없음
* 로컬에서 생성된 블로그 관련 파일들을 GitHub에 싱크하기 위한 git : 없음.

#GitHub 계정 만들기
GitHub은 블로그를 무료로 온라인 상에 게시해 주는 호스팅 서비스의 역할을 하게된다. GitHub에서 코드를 다운로드 받은 적은 있지만 아직 내 계정은 생성 한 적이 없으므로 GitHub에 가입을 하여 계정을 만들었다.
GitHub에 블로그를 위한 Repository를 새로 만든다.
이 때 Repo 이름은 <github계정명>.github.io 의 형식으로 생성한다. 반드시 이름 뒤에 .github.io를 붙이는 것을 명심하자.

#Git 클라이언트 설치 - Window
로컬에서 작성한 문서를 온라인에 게시하기 위해서는 git을 이용한다. 윈도우에서는 Tortoise Git 클라이언트 프로그램을 많이 쓰므로, 해당 툴을 다운로드 하여 설치한다.
https://tortoisegit.org/download/

추가: Tortoise Git에는 실제 Git 프로그램이 포함되어 있지 않다. Tortoise Git은 단지 Git을 위한 GUI를 제공해 줄 뿐이다. 따라서, git for windows를 https://git-for-windows.github.io/ 에서 다운받아 설치해야 한다.

Tortoise Git이 설치가 되면, GitHub에 생성한 repository를 로컬로 연결시킨다.
윈도우 탐색기에서 블로그 파일을 보관할 폴더에 우클릭을 하여 Git clone 항목을 클릭하면 다음과 같은 윈도우가 뜬다.



OK 버튼을 누르면 해당 폴더가 내 Github 계정의 repository가 로컬에 복사된다. 하지만 지금은 아무 내용이 없이 비어 있을 것이다.


#Jekyll 설치
##Ubuntu 14.04
우분투에서 Jekyll의 설치는 다음 한 줄이면 끝난다. 다른 블로그 글들을 찾아보면 Ruby, NodeJS 등의 여러가지 dependency가 있는 걸로 나오는데.. 내 컴에는 이미 모두 설치가 되어 있는지 아니면 다음 명령에서 알아서 처리 하는지(적어도 다음 명령을 실행하는 RubyGems 라는 라이브러리는 설치되어 있는듯 하다.) 간단히 설치를 할 수 있었다.
gem install jekyll

설치 확인을 위해 다음의 명령으로 버전을 확인해 본다.
'jekyll -v'
출력: Jekyll 0.11.2

##Windows 10
윈도우 환경에서 Jekyll을 설치하는 과정은 다음의 블로그를 참고했다.
http://jekyll-windows.juthilo.com/

###Step 1. Ruby for Windows 설치
위 링크의 블로그에서는 루비의 2.0.0 버전을 설치할 것을 추천하고 있다. 하지만, 나는 최신 버전을 선호 하므로, 가장 최신 stable 버전인 Ruby 2.2.5(x64)를 다운 받아 설치 했다.
설치 패키지 URL: http://rubyinstaller.org/downloads/

###Step 2. Ruby DevKit 설치
Ruby DevKit은 Ruby installer와 동일한 페이지에 있다.  나는 DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe 를 다운 받아 c:\RubyDevKit\에 압축을 풀었다.
그 다음 devkit을 Ruby와 바인딩하고 설치하는 과정은 명령 프로프트를 열어 다음과 같이 진행하면 된다.
'''
cd c:\RubyDevKit
ruby dk.rb init
ruby dk.rb install
'''

###Step 3. jekyll 설치
Ruby를 설치함에 따라서 명령 프로프트에서 gem 명령을 사용할 수 있게 되었다. 우분투와 마찬가지로 다음의 명령으로 jekyll을 설치 한다.
'gem install jekyll'

###Step 4.jekyll으로 블로그용 폴더 생성
명령 프롬프트에서 내 계정의 GitHub repository를 다운 받은 폴더 폴더로 이동한 후 다음 명령을 입력하면 하위 폴더에 블로그를 위한 기본 템플릿 파일들이 생성된다.
'jekyll new .'

생성된 블로그를 확인하기 위해 다음의 명령을 입력한 후, 인터넷 브라우저에서 http://127.0.0.1:4000/ 주소로 접속하면 초기 화면을 확인 할 수 있다.
'jekyll serve -w'

###Step 4. jekyll을 위한 추가 기능 설치(Optional)
* 소스 파일이 변경되면 자동으로 페이지를 생성하기.
	윈도우에서는 이 기능을 위해 wdm이라는 툴을 추가로 설치해주면 된다.
		'gem install wdm'
* Syntax Highlighter 
	작성한 글에 포함된 소스코드들에 자동으로 하이라이트(=이쁘게)를 추가해주는 기능을 위해서는 Pygments라는 툴을 추가로 설치해야 한다. 이 툴은 Python v2.x 가 설치되어 있어야 한다. 아래 사이트에서 윈도우용 가장 최신 버전(v2.7.12) 파이썬을 다운 받아 설치한다.
	https://www.python.org/downloads/
	그다음 파이썬용 라이브러리 다운 명령툴인 pip를 설치한다. 다음 경로의 get-pip.py를 로컬에 다운받고 아래의 명령을 실행한다.
	https://bootstrap.pypa.io/get-pip.py
	'python get-pip.py'
	
	이제 Pygments를 설치할 차례다.
	'python -m pip install Pygments'
	
	내가 만든 블로그에서 Pygments의 기능을 적용하려면 블로그 로컬 폴더의 _config.yml을 문서 편집기에서 열고 다음의 구문을 추가해 준다.
	'highlighter: pygments'
	

#생성한 블로그를 GitHub에 게시하기
Jekyll로 생성한 블로그 폴더 내용은 다음과 같다.



위 내용을 GitHub에 올리기 위해 모든 파일과 폴더를 선택 후 우클릭하여 TortoiseGit의 항목 중 add 버튼을 클릭 한다.


그리고 모든 파일과 폴더를 선택한 후 OK 버튼을 누른다.


이제 윈도우 탐색기에서 우클릭을 하고, "Git commit -> master .." 버튼을 누른 후, message에 "첫번째 업데이트" 등의 기록을 남기고 커밋한다.
마지막으로 다시, 윈도우 탐색기에서 우클릭을 하고 TortoiseGit 메뉴에서 push를 누르면


위와 같이 깃헙 로긴 메뉴가 나타난다.  아이디와 비번을 넣으면, 깃헙에 업로드가 완료된다.
이후, 인터넷 브라우저에서 내 깃헙 계정의 repository(https://github.com/Gabriel-Kang/gabriel-kang.github.io)로 접속해 보면 로컬에 있던 파일이 깃헙에 올라간것을 확인 할 수 있다.


이제 블로그로의 접속은 repository명으로 접근 가능하다.(https://gabriel-kang.github.io/)



로컬에서 보았던 것과 동일한 웹페이지가 이제 인터넷을 통해 접속이 가능해졌다.

이제 모든 설치가 끝났고, 블로그를 꾸미고, 글을 올리기만 하면된다.

#참고 사이트
1. 윈도우에서 Jekyll 설치: http://jekyll-windows.juthilo.com/
2. GitHub과의 연동 http://blog.saltfactory.net/jekyll/upgrade-github-pages-dependency-versions.html
3. Jekyll 한글 설명서: http://jekyllrb-ko.github.io/docs/
