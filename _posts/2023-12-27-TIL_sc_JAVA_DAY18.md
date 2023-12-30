---
title: 2023.DEC.27(WED) JAVA DAY 18
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, stream, ascend, descend]
---

## ✅ 오름차순, 내림차순

오름차순 `.min((s1, s2)->s1.getScore() - s2.getScore())` <br>
내림차순 `.sorted((s1, s2)-> s2.getScore() - s1.getScore())` <br>
<br>

없으면 n/a출력 <br>
`.orElse("N/A");` <br>
`.orElse(0);` <br>

## ✅ 남학생들 중 가장 낮은 성적을 가진 학생의 이름 출력하기

filter 성별 == 남자 <br>
min 가장 낮은 성적 <br>
map 이름 구하기 <br>
orElse 아니면 이거 출력 <br>

## ✅ 여학생들 중 성적 상위 3명의 평균 성적 구하기

filter 성별 == 여자 <br>
sort 가장 높은 성적으로 내림차순 정렬 <br>
limit 상위 3명만 <br>
mapToInt 점수구하기 <br>
average 평균 <br>
orElse 아니면 이거 출력 <br>
