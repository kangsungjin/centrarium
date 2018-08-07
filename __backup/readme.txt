
Introduce | Development


1. css 사이트의 기본 색을 변경 하고 싶으면 _sass/base/_variables.scss로 가면 된다. 

2. _layouts/archive.html
    {% post in page.posts %}
        ...
    {%%}


3. _layouts/development.html 
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