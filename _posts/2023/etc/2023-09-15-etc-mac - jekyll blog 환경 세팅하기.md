---
title: "[Etc] Mac - jekyll blog 환경 세팅하기"
#excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Etc
tags:
  - [jekyll]

permalink: /etc/mac - jekyll blog 환경 세팅하기/



date: 2023-09-15
#last_modified_at: 2021-10-09
---

## 1. Jekyll blog 환경 세팅
👉 [블로그 바로가기](https://danaing.github.io/etc/2022/03/14/M1-mac-jekyll-setting.html)
<br><br>
위의 블로그를 따라하다보면 jekyll을 설치할 때 오류가 1개 발생한다.<br><br>
<div class="border">
% gem install jekyll<br>
ERROR:  Error installing jekyll:<br>
The last version of sass-embedded (~> 1.54) to support your Ruby & RubyGems was 1.63.6. Try installing it with `gem install sass-embedded -v 1.63.6` and then running the current command again<br>
sass-embedded requires Ruby version >= 3.0.0. The current ruby version is 2.7.5.203.
</div>
<br>
이 오류 메시지는 현재 시스템에서 실행 중인 Ruby 버전이 2.7.5이며, sass-embedded 버전 1.63.6 이상을 설치하려면 Ruby 버전 3.0.0 이상이 필요하다는 것을 나타낸다.
<br><br><br><br>
<div class="border">
rbenv install 3.0.0<br>
rbenv global 3.0.0</div>
<br>
위의 명령어를 사용해 Ruby 3.0.0 버전을 설치하고 아래의 명령어를 사용해 버전을 확인한다.<br><br>
<div class="border">ruby -v</div>
<br><br><br><br>