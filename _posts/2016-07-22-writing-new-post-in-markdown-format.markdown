---
layout: post
title: Markdown 포맷으로 블로그 포스트 작성 및 Jekyll 라이브러리로 블로그 꾸미기
---

# 개요
---

지난번 포스팅( [Jekyll + Github로 블로그 만들기 (for Windows 10)]({% post_url 2016-07-21-building_a_blog_using_Jekyll_Github %}) )에 이어서 이번에는 본격적으로 Markdown(마크다운) 형식으로 글을 작성하고 게시하는 법에 대한 내용을 포스팅하고자 한다. 사실, Jekyll을 이용한 포스팅 파일 형식은 Markdown, HTML 및 기타 적절한 컨버터가 있는 다양한 포맷을 지원한다.  따라서, 사용자는 단순히 <my_jekyll_path>/_posts 에 새로운 파일을 생성하는 것만으로도 HTML 형식의 웹페이지를 생성할 수 있다. 하지만, 텍스트 파일 형태로만 글을 작성하면 자동으로 HTML 형태로 보기 좋게 만들어주는 마크다운 형식으로 작성하는 것이 대세인듯하다. 따라서 여기서는 마크다운 형식의 문법은 대부분은 매우 간단해서 익히기도 쉽다.(단, 마크다운 오리지날 포맷은 너무 단순해서 사용자가 원하는 여러 기능을 지원하지 않는 것이 많아서, 추후에 각 서비스 업체에서 자신만의 문법을 추가한 버전들이 존재한다. Ex: Github Flavored Markdown, GFM)

# 포스트 파일 만들기
---

포스트 파일 이름은 다음의 형식을 따라야 한다. 

`YEAR-MONTH-DAY-title.MARKUP`
예) 2016-07-21-building_a_blog_using_Jekyll_Github.md

위 형식에서 MARKUP은 호환되는 파일확장자를 의미한다.
** 주의: 한글로 파일명을 작성하면 인코딩 문제로 빌드 도중 파일명이 깨지거나 에러가 날 소지가 있으니 주의한다. **

# 포스트 파일 헤더 포맷
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

# 잠깐.. Jekyll 빌드는 안해도 되나?
---

그렇다. 위 과정에서 Jekyll로 md 형식 파일을 html로 변환하는 과정이 생략되었다. Jekyll이 하는 역할 중의 하나인 md -> HTML 변환은 사실 Github에서도 자체적으로 해주는 것 같다. 따라서, 포스트만 추가로 게시 할려면 Jekyll로 굳이 빌드를 할 필요가 없다. 하지만, 블로그의 전체 스타일 및 블로그에 여러가지 부가기능을 추가하려면(또는, Github에서는 지원하지 않는 기능들을 추가하려면) Jekyll을 이용해서 로컬에서 생성한 HTML 파일을 푸쉬해서 올리면 된다. 

# 포스트에 태그 및 카테고리 추가하기
---

블로그 내용을 정리/검색하기 위해서는 태그 및 카테고리 기능이 필수적이다. 각 포스트마다 카테고리와 태그를 추가하는 법에 대해 알아보자.

## 포스트에 태그 추가하기

각 포스트별로 태그를 추가하는 법은 간단히, 포스트의 yaml frontmatter 헤더에 다음의 내용과 같이 추가해주면 된다.
(이 내용은 [Tags In Jekyll](http://charliepark.org/tags-in-jekyll/)를 그대로 참고하였다.)

```language
tags:
 - Jekyll
 - Markdown
 - Github 
 - Redcarpet
```
하지만, 저렇게 태그만 추가한다고 블로그 페이지에 짠하고 태그가 표시되지는 않는다.

현재 블로그의 하위 폴더에 `_layouts/tag_index.html` 과 `_plugins/_tag_gen.rb`을 추가해야 한다. `_layouts/tag_index.html`는 태그를 클릭했을 때 해당 태그를 포함한 포스트 목록을 보여주기 위한 레이아웃이고, `_plugins/_tag_gen.rb`는 태그별 폴더를 생성하고, 폴더마다 `index.html`을 생성하여, 앞에서 생성한 레이아웃을 삽입하는 역할을 한다.

\_layouts/tag_index.html

````html
---
layout: default
---
<h2 class="post_title">{{page.title}}</h2>
<ul>
	{% for post in site.posts %}
	{% for tag in post.tags %}
	{% if tag == page.tag %}
	<li class="archive_list">
		<h3 class="archive_list_header"><a class="archive_list_article_link" href='{{post.url}}'>{{post.title}}</a></h3>
		<time class="archive_list_post_date" datetime='{{post.date | date: "%Y-%m-%d"}}'>{{post.date | date: "%m/%e/%y"}}</time>
		<p class="summary">Summary: {{post.summary}}
		<ul class="tag_list">
			{% for tag in post.tags %}
			<li class="inline archive_list"><a class="tag_list_link" href="/tag/{{ tag }}">{{ tag }}</a></li>
			{% endfor %}
		</ul>
	</li>
	{% endif %}
	{% endfor %}
	{% endfor %}
</ul>
````

\_tag_gen.rb

```ruby
module Jekyll

  class TagIndex < Page    
    def initialize(site, base, dir, tag)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'

      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'tag_index.html')
      self.data['tag'] = tag
      #self.data['title'] = "Posts Tagged &ldquo;"+tag+"&rdquo;"
	  self.data['title'] = "["+tag+"]"
    end
  end

  class TagGenerator < Generator
    safe true
    
    def generate(site)
      if site.layouts.key? 'tag_index'
        dir = 'tag'
        site.tags.keys.each do |tag|
          write_tag_index(site, File.join(dir, tag), tag)
        end
      end
    end
  
    def write_tag_index(site, dir, tag)
      index = TagIndex.new(site, site.source, dir, tag)
      index.render(site.layouts, site.site_payload)
      index.write(site.dest)
      site.pages << index
    end
  end

end
```

두 개 파일을 텍스트 에디터로 작성하여 추가하고, 명령 프롬프트에서 `jekyll build; jekyll serve`를 실행하면 다음과 같이 메인 화면 윗부분에 태그 목록이 나타난다.

![태그가 추가된 메인 페이지]({{ site.url }}/assets/main_with_tag.JPG)

태그 중에 아무거나 하나를 클릭하면 해당 태그가 포함된 블로그 리스트가 표시된다.(summary 항목은 yaml frontmatter에 `summary: <내용>` 의 문구가 표시된다.)

![태그 리스트 화면]({{ site.url }}/assets/tag_page.JPG)

하지만, 이것만으로는 각 포스트 화면에서는 해당 포스트의 태그가 표시되지 않는다. 이 것은 `_layout/post.html'의 내용을 변경해야 할 부분인듯하다. 레이아웃을 변경하는 것은 직접 만드는 것보다는 공개된 테마를 다운받아 쓰는 것이 훨씬 깔끔하고 편한 방법이다.

