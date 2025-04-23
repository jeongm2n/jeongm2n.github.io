---
layout: post
categories: 개발일지
title: "세 번째 개발일지, Github Blog에 이미지 추가하기"
---

<br>

# 세 번째 개발일지, Github Blog에 이미지 추가하기

<br>
<br>

## 문제 발생

<br>

<p>
평소처럼 백준 알고리즘 문제를 풀이한 후 깃허브 블로그에 포스팅을 하고 있었다.<br>
문제 설명, 입력, 출력, 예제입출력 등을 캡쳐해서 이미지로 업로드하는 방법을 사용 중이었는데 저번부터 Github Issue에서 따온 이미지 링크가 먹히질 않았다.<br>

<br>

그래서 이유를 찾아보니 Github 보안 정책 강화 때문에 Github Issue에서 이미지 링크를 따오는 게 불가능해졌다는 말이 있었다.(정확하진 않음..)<br>
어쨌든 github issue에서 따오는 방법으로 했을 때 이미지에서 계속 엑박이 떴기 때문에 다른 방법을 찾아봤다.
</p>

<br>
<br>

## 방법: 이미지만 저장하는 레파지토리를 생성

<br>

<p>
그래서 발견한 방법은 이미지만 저장해서 따로 관리하는 저장소를 생성하는 것이다.<br>

<br>

1. Github에서 new repository로 이미지만 저장하는 저장소를 생성한다.
2. 본인 컴퓨터에 Git과 클론할 위치로 터미널에서 이동한다.
3. git clone [본인 레파지토리 url] 명령어를 실행한다.
4. 블로그에 업로드 할 이미지들을 저장소에 옮긴 후 저장소에 push 한다.

<br>
<br>

Github 사이트에서 이미지 레파지토리로 이동한 후, 업로드하길 원하는 사진을 클릭한다.

<br>

<img width="100%" alt="Image" src="https://raw.githubusercontent.com/jeongm2n/blog-images/refs/heads/main/2025%3A04%3A23/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202025-04-23%20%EC%98%A4%ED%9B%84%204.08.11.png?token=GHSAT0AAAAAADCV3OWQ2OW4OZ2VAZ37D6UI2AISMFA" />

<br>

위 그림처럼 원하는 사진을 클릭한 후 해당 이미지를 마우스 우클릭하면 새 탭에서 이미지 열기를 클릭한다.

<br>
<br>

<img width="100%" alt="Image" src="https://raw.githubusercontent.com/jeongm2n/blog-images/refs/heads/main/2025%3A04%3A23/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202025-04-23%20%EC%98%A4%ED%9B%84%204.09.05.png?token=GHSAT0AAAAAADCV3OWQ5FHLU5WQUIO63XNK2AISNYA" />

<br>

이미지를 새 탭에서 연 후 링크창에 있는 URL 주소를 복사해서 img src에 입력하면 업로드 완료! <br>

<br>
<br>

Github Issue에서 이미지 링크를 따올 때와 달리 조금 귀찮아졌지만 뭐,, 어쩌겠나 이제 Github Issue에서 따오는게 안된다는데 ㅠㅠ

</p>

