
Introduce | Development

Jekyll 구조
=========================================================================
_includes
> 부분 파일들이 들어가 있음
> head, footer, page_divider

_layouts
>

_posts
 > 포스팅 파일들이 들어가 있음 
 > 형식 [YYYY-mm-dd-category_name.확장자]

_sass 
 > - css style file 및 static css Value file이 들어가 있음

assets
 > 웹에서 사용하는 리소스를 저장
css 
 > main.scss 에서 _sass의 있는 css를 호출
js

=========================================================================

0. Project 내에 ./
    -index.html
    -posts.html
    -developments.html
    -tags.html 
위 목록에서 클릭시 표시할 html, md를 셋팅 하는 부분은 
---
    layout: page                {development,tags,page,post}.html / (path:_layouts/...)
    title: "Developments"       {{% page.title %}}
    permalink: /developments/   {{% page.url %}}

============================

1. css 사이트의 기본 색을 변경 하고 싶으면 _sass/base/_variables.scss로 가면 된다. 

2. _layouts/archive.html
    {% post in page.posts %}
        ...
    {%%}


3. _layouts/development.html 에 시정한 layout:page는 _layouts/page.html를
    가리키는 것이다. 
    index.html 에서 클릭하고 들어가는 Posting 정보를 뿌려주는  html로 사용됨.

4. developments.html 
    HEAD: menu - Development버튼을 클릭 하고 들어가면 나오게 되는 화면.



============================
error

1. developments.html 
    developments.html 2line error > 
    error.msg: index.html 'fake_tag'

    #### Page build failed: Unknown tag error
    Subject: Page build failed
    The page build failed with the following error:
    The tag `fake_tag` in `index.html` is not a recognized Liquid tag.

    >>>>>> in Source
    소스 내에서 로그 출력이 되는지 확인 하려다가 난 오류 
    이런식 > {% for category in site.categories %} >> {% site.categories %}

    이런식 > % for desc in site.descriptions %}
        {% if desc.cat == cat %} > {%  desc.cat %}