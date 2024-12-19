---
layouts: post
categories: programmers
title: '[프로그래머스] SQL 조건별로 분류하여 주문상태 출력하기 문제' 
---

# [프로그래머스] SQL 조건별로 분류하여 주문상태 출력하기 문제

<br>

> ## 문제
> <img width="100%" alt="스크린샷 2024-12-19 오후 2 57 56" src="https://github.com/user-attachments/assets/a76b2844-a040-465e-8d06-0991233df890" />

<br>
<br>

> ## 출력 예시
> <img width="100%" alt="스크린샷 2024-12-19 오후 2 59 08" src="https://github.com/user-attachments/assets/a02fbcc5-f5db-4493-a7e6-74b16602c1ef" />

<br>
<br>

## 문제 풀이

나는 Oracle, MySQL 둘 다 사용해봤지만 가장 최근까지 노트북에 설치되어있고 개발에 사용한 것은 MySQL이기 때문에 편의상 MySQL로 SQL 문제 풀이하는 것을 선호한다.

<br>

### 유의할 점
- OUT_DATE가 'yyyy-mm-dd' 형태로 출력되어야 함
- 2022년 5월 1일을 기준으로 OUT_DATE 컬럼의 값이 이하이면 '출고완료', 초과이면 '출고대기', NULL이면 '출고미정'을 출력해야 함

<br>
<br>

날짜 포맷 함수인 <span style="color:skyblue">**DATE_FORMAT 함수**</span>를 사용한다.

```MySQL
DATE_FORMAT(OUT_DATE, '%Y-%m-%d')
```

위 함수만 알면 쉽게 풀 수 있는 문제이다.

<br>

그리고 출고여부 칼럼의 값은 <span style="color:skyblue">**CASE WHEN절**</span>을 사용해서 값을 다르게 나타내준다.

<br>
<br>

## 정답 코드
```MySQL
SELECT ORDER_ID, PRODUCT_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d') AS OUT_DATE,
CASE WHEN DATE_FORMAT(OUT_DATE, '%Y-%m-%d')<='2022-05-01' THEN '출고완료'
    WHEN OUT_DATE IS NULL THEN '출고미정'
    ELSE '출고대기'
END AS 출고여부
FROM FOOD_ORDER
ORDER BY 1;
```