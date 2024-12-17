---
layout: post
categories: 개발일지
title: 블로그 개설 후 첫 번째 개발일지
subtitle: 블로그 개설 3일차, 적응하기 위해 작성하는 첫 번째 개발일지
---

# 첫 번째 개발일지 241216

<br>

ruby 언어는 살면서 처음인지라... <br>
계속 블로그를 운영하려면 이 테마의 구조부터 이해해야 할 것 같아서 테마(?)를 공부해봤음.

<br>

일단 네이버 블로그와 벨로그 짬으로 경험해본 결과,<br>
블로그를 가시성있고 깔끔해보이려면 카테고리를 잘 나눠야하기 때문에 개발일지에 맞는 카테고리를 생성하고자 했음.<br>
근데 첫 시작부터 쉽지가 않다.<br>

일단 사이트끼리 주고받는 데이터를 관리하는 코드를 이해해야했다. 
<br>
<br>
<br>

## 공부한 것들

### 1. 변수 할당

{% raw %}
```ruby
{% assign keys = 어쩌구저쩌구 %}
```


어쩌구저쩌구를 변수 keys에 할당하겠다는 뜻이다.

<br>
<br>

### 2. 사이드바 설정

```ruby

{%- if page.sidebar -%}
    {%- assign sidebar = page.sidebar -%}
    {%- elsif site.defaults[page.layout].sidebar -%}
    {%- assign sidebar = site.defaults[page.layout].sidebar -%}
    {%- elsif layout.sidebar -%}
    {%- assign sidebar = layout.sidebar -%}
{%- endif -%}

```

이런 코드가 있는데 세 가지 조건에 의해 페이지마다 사이드바의 내용을 다르게 해서 띄우기 위한 코드로 해석했다.

<br>

#### 2-1. page.sidebar

페이지 자체에 사이드바가 설정되어 있는 경우

```ruby
---
layout: post
sidebar: categories_list 
---
``` 

위와 같이 마크다운 파일 상단에 해당 페이지의 사이드바가 설정되어 있는 경우이다.

<br>

#### 2-2. site.defaults

해당 layout에 연결된 _config.yml에 설정된 전역 기본값을 참조한다.

```ruby
defaults:
  - scope:
      path: ""
      type: "post"
    values:
      sidebar: "default_sidebar"
```

<br>

#### 2-3. layout.sidebar

해당 레이아웃 파일(_layouts/)에 정의된 변수를 의미한다.

```ruby
{% assign layout.sidebar = "layout_sidebar" %}
```

<br>

### 3. Liquid 태그와의 충돌 문제 해결

백틱 내부에서 Liquid태그 ({% ... %}) 를 사용하면 잘릴 수 있음.<br>
잘리지 않도록 파싱하지 않아도 되는 코드의 윗부분에 Liquid 태그에 raw를, 끝나는 부분에 Liquid 태그에 endraw를 붙여주기!!
{% endraw %}
<br>
<hr>
<br>

## 마무리

ruby 이녀석.. 상당히 어렵다.. 블로그 쓸 때만 깔짝대야겠다..ㅎ

깃허브 블로그 첫 번째 글 작성 완료~~ 