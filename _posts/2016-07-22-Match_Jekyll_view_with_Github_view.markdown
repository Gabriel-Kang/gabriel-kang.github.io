---
layout: post
title: Jekyll로 생성된 블로그 페이지와 Github의 페이지 모양 일치시키기
category: 
 - Jekyll

tags:
 - Jekyll
 - Markdown
 - Github 
 - Redcarpet

summary: Jekyll로 생성된 블로그 페이지와 Github의 페이지 스타일을 일치시키기 위한 redcarpet 옵션 설정 하기.
---

같은 마크다운 포맷으로 작성한 포스트라 하더라도 마크다운 렌더러에 따라서 보이는 모양이나 기능이 조금씩 차이가 날 수가 있다. Github에서 포스팅하는 모양과 로컬에서 Jekyll로 빌드한 페이지의 모양을 일치 시키기 위해서는, _config.yml파일의 jekyll의 마크다운 렌더러를 Github과 동일한 redcarpet으로 설정하고, 다음과 같은 extentions 옵션을 추가해 준다.

```language
markdown: redcarpet 
redcarpet:
    extensions: ["no_intra_emphasis", "tables", "autolink", "fenced_code_blocks", "strikethrough"]  #default setting github
```

jekyll에서 지원하는 redcarpet extentions 옵션에 대한 자세한 설명은 다음의 링크를 참조한다.
[Configuring Redcarpet](https://george-hawkins.github.io/basic-gfm-jekyll/redcarpet-extensions.html)

