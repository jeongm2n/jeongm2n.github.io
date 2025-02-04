---
layout: post
categories: 개발일지
title: "두 번째 개발일지, 깃허브 블로그에 댓글 기능 추가하기"
---

<br>

# 깃허브 블로그에 댓글 기능 추가하기

<br>
<br>

<p> 깃허브 블로그를 개설하고 글을 작성하다 보니 뭔가 허전한 느낌이 들었다. <br>
바로 블로그에 필수인 댓글 기능이 빠진 것!! <br>
그래서 바~로 추가해버렸다. 과정이 쉬운 것 같으면서도 쉽지 않았다.. 휴;
</p>

<br>
<br>

> ## Github Apps에서 Utterances 다운받기
> <a href="https://github.com/apps/utterances" target="_blank">Utterances 다운</a>
> <img width="100%" alt="Image" src="https://github.com/user-attachments/assets/0b13a9fb-bc1f-4762-9f43-8682a10da57e" />

install 클릭하기

<br>

> ## 설치할 Repository 선택하기
> Install 후에는 아래 사진과 같은 화면이 나온다.
> <img width="100%" alt="Image" src="https://github.com/user-attachments/assets/bad7c7cf-0040-46c0-822d-5d68e36679c3" />

깃허브 블로그에서만 사용하면 되기 때문에 Only Select repositories에서 깃허브 블로그 레파지토리를 선택한다. <br>
❗️ 여기서 혹시나 github.io 레파지토리가 Private이면 Public으로 바꾸거나 댓글만 관리할 Public 레파지토리를 따로 생성해서 써야한다.

<br>

> ## Repository명 입력하기
> <img width="100%" alt="Image" src="https://github.com/user-attachments/assets/a04c4887-2535-4819-bc66-13cfb25ccd0e" />

owner/ repo 칸에 <span style="background-color: skyblue; color: white">**[본인 깃허브 계정 이름]/[레파지토리 이름]**</span> 을 적어줘야 한다.

<br>

> ## Comments 관리 설정하기
> <img width="100%" alt="Image" src="https://github.com/user-attachments/assets/5c452ae2-de11-46f4-8ef0-8bb323999c06" />

가장 위에 있는 것은 게시글 파일명에 따라 댓글 관리하기 라는 뜻인 것 같은데 어차피 글 제목이 바뀔 순 있어도 게시글 파일명은 잘 안바꾸기 때문에 이걸로 선택했다.<br>
이거는 각자 취향대로 하시면 될 듯 합니다.

<br>

> ## Comments Label 설정하기
> <img width="692" alt="Image" src="https://github.com/user-attachments/assets/1e2e9e80-343d-43a5-9588-3b26aa4688bc" />

Comments 기능이 레파지토리의 Issue로 관리되기 때문에 Issue에서 Comment들에 이름붙이는? 뭐 그런 느낌이라고 생각하면 된다.<br>
나는 그냥 알아보기 쉽게 comments로 했다.

<br>

> ## Utterances script 복사하기
> <img width="100%" alt="Image" src="https://github.com/user-attachments/assets/666abd09-0837-425b-8d85-ba1f158c3d50" />

위 과정을 다 거치면 위 사진처럼 내가 설정한 요소에 따른 script 코드가 뜨는데 이걸 복사한다.

<br>

복사한 script 코드를 _layouts.post.html의 comments 관련 부분에 붙여넣기 한다.

<br>

<span style="color: red"> ⬆️ 근데 이거는 사용하는 깃허브 블로그 테마에 따라 좀 다를 수도 있습니다. <br>
제가 사용하는 테마의 경우는 post.html에서 include 태그를 통해 extensions/comments/utterances.html에 script를 붙여넣기해야 했어요. <span>

<br>
<br>

그러나.. 내가 이런 과정이 쉽게 될리가 없다..

<br>

모든 과정이 끝나고 서버를 다시 실행하고 쿠키 삭제도 해봤지만 댓글 기능이 생기지 않았다.
그래서 찾아보니 _config.yml에 몇 가지 수정해야 하는 부분이 좀 있었다.

<br>

```YAML
utterances: 
  repo: "jeongm2n/jeongm2n.github.io"
  issue_term: "pathname"
  label: "comments"
  theme: "github-light"
  follow_site_theme: true
```

위 코드를 추가해줘야 했다.

<br>

그리고 YAML 코드는 공백이나 들여쓰기를 잘 맞춰줘야 한다는 것을 새롭게 알았다. <br>
이거 무시했다가 세 번의 에러를 맛보게 됨 ;;

<br>

utterances: 뒤에 공백이 하나 이상 있어야 하고 들여쓰기 하는 요소들에는 앞에 공백이 두 개 있어야 한다. <br>
허허....