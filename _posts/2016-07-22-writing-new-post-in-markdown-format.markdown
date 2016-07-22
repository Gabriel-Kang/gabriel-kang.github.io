---
layout: post
title: Markdown 포맷으로 블로그 포스트 작성하고 Jekyll 라이브러리로 변환하기
---

# 개요
---

지난번 포스팅에 이어서 이번에는 본격적으로 Markdown(마크다운) 형식으로 글을 작성하고 게시하는 법에 대한 내용을 포스팅하고자 한다. 사실, Jekyll을 이용한 포스팅 파일 형식은 Markdown, HTML 및 기타 적절한 컨버터가 있는 다양한 포맷을 지원한다.  따라서, 사용자는 단순히 <my_jekyll_path>/_posts 에 새로운 파일을 생성하는 것만으로도 HTML 형식의 웹페이지를 생성할 수 있다. 하지만, 텍스트 파일 형태로만 글을 작성하면 자동으로 HTML 형태로 보기 좋게 만들어주는 마크다운 형식으로 작성하는 것이 대세인듯하다. 따라서 여기서는 마크다운 형식의 문법은 대부분은 매우 간단해서 익히기도 쉽다.(단, 마크다운 오리지날 포맷은 너무 단순해서 사용자가 원하는 여러 기능을 지원하지 않는 것이 많아서, 추후에 각 서비스 업체에서 자신만의 문법을 추가한 버전들이 존재한다. Ex: Github Flavored Markdown, GFM)

# 포스트 파일 만들기
포스트 파일 이름은 다음의 형식을 따라야 한다. 

`YEAR-MONTH-DAY-title.MARKUP`
예) 2016-07-21-building_a_blog_using_Jekyll_Github.md

위 형식에서 MARKUP은 호환되는 파일확장자를 의미한다.
** 주의: 한글로 파일명을 작성하면 인코딩 문제로 빌드 도중 파일명이 깨지거나 에러가 날 소지가 있으니 주의한다. **

# Post 파일 헤더 포맷
---

모든 포스트 파일은 제일 첫머리에 YAML 형식의 Front Matter라는 머리말을 포함하고 있어야 한다. 그러면 Jekyll이 해당 헤더를 읽어서 적절한 형식으로 HTML을 생성해 낸다.
반드시 들어가야 하는 내용만 쓰면 다음과 같다.

\---
layout: post
title: Blogging Like a Hacker
\---

# 마크다운 Syntex
---

구글링을 해보면 마크다운 포맷의 문법에 정리된 글이 매우 많다. 그 중에서도 Github에서 정리해 놓은 문법이 간단하면서도 이해하기 쉽게 정리해 놓은 것같다.

[Writing on GitHub](https://help.github.com/categories/writing-on-github/)

단, 위 문법에서 주의할 점은 오리지날 마크다운에서 Github이 추가한 문법(Github Flavored Markdown, GFM))이 존재한다는 것이다. 따라서, GTM을 지원하지 않는 뷰어에서는 의도한 대로 포스팅이 보이지 않을 수도 있다. 물론, Github에서 블로그 호스팅을 하는 경우는 신경쓰지 않아도 된다.

# 마크다운 포스트 작성 및 Github에 게시하기
---

텍스트 에디터로 _posts 폴더에 "2016-07-21-building_a_blog_using_Jekyll_Github.md" 라는 마크다운 파일을 만들었다. 파일 저장시 주의할 점은 현재 사용환경이 윈도우라면 텍스트 인코딩을 BOM 없는 UTF-8 형식으로 인코딩 설정을 바꿔줘야한다는 점이다. 
생성한 텍스트 파일에 다음과 같은 내용을 입력하고 저장한다.

```
---
layout: post
title: Jekyll + Github로 블로그 만들기 (for Windows 10)
---

개요
여러가지 프로그래밍 작업 및 공부를 하면서, 그 중간 과정(=삽질)에 대한 기록을 해놔야겠다는 필요성 때문에 블로그를 만들어야겠다는 생각을 하게 됐다. 그러던 중, 우연히 회사 동료가 GitHub를 이용해서 무료로 블로그를 만들 수 있는 Jekyll이라는 툴을 쓰는 걸 보고, 깃헙에 블로깅을 하는게 왠지 굉장히 쿨하게 느껴져서 이렇게 만들게 됐다. 

```

위 파일을 Git을 이용해서 내 Github 계정에 push하고, 내 블로그 페이지에 접속하면 다음과 같이 새로운 포스트가 생긴것을 확인 할 수 있다.

![새 포스트의 링크가 추가된 메인 화면]({{ site.url }}/assets/NewPostingMain.png)

해당 포스트의 내용은 다음과 같다.

![새로 포스팅된 내용 화면]({{ site.url }}/assets/NewPostSample.png)


