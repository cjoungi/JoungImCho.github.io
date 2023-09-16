---
title: "[DB] docker 사용해서 오라클-xe-11g 설치하기"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - DB
tags:
  - [oracle, docker, db, colima]

permalink: /db/docker 사용해서 오라클-xe-11g 설치하기/


date: 2023-09-16
last_modified_at: 2022-07-24
---
<br><br><br>
현재 **맥북 프로 M2 칩**을 사용하고 있다.<br><br>
Apple Silicon(M1, M2 등)을 사용하는 맥에서는, 전통적인 방식으로의 Oracle Database 설치가 지원되지 않는다.<br><br>
따라서, <span class="color">Docker</span>를 사용하여 Oracle Database를 설치하고 운영하는 것이 현재로서는 최선의 방법이다!<br><br><br><br>

<code>Docker</code>는 가상화 플랫폼으로, 어플리케이션과 그 의존성들을 '컨테이너'라고 불리는 표준화된 유닛에 패키징하여 소프트웨어를 보다 쉽게 생성, 배포, 실행할 수 있게 해준다.<br><br>
Docker를 사용하면, 여러 종류의 환경에서 같은 방식으로 데이터베이스를 실행할 수 있어, 호환성 문제를 피할 수 있다.<br><br><br><br>

아래의 블로그를 따라해보자.<br><br>
참고로 도커 설치 할 때, Docker Desktop의 <code>Apple Silicon 버전</code>을 받아야 한다!!<br><br>

👉 <a class="underline" src="https://steemit.com/it/@jihyunj/mac-docker-oracle-11g">블로그 바로가기</a>
<br><br><br><br>

---

참고링크 |<br>
- [Mac(맥)에서 docker(도커)를 이용해 Oracle(오라클)11g 설치하기](https://steemit.com/it/@jihyunj/mac-docker-oracle-11g)
<br><br><br><br>