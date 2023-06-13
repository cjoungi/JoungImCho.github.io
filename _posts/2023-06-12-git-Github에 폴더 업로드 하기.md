---
title: "[Git/Github] Github에 폴더 업로드하기"

categories:
  - Git/Github

permalink: /git/Github에 폴더 업로드하기/

date: 2023-06-12
#last_modified_at: 2021-10-0
---
공부를 하면서 만들어진 파일들이 꽤나 쌓였다.<br>이 파일들이 담긴 여러개의 폴더 전체를 Git에 올리면서 그 과정을 기록하려고 한다.<br><br>
## 1. git에 repository를 새로 생성하기

[Github](https://www.github.com/){:target="_blank"}에 접속해서 로그인 후, 프로필에 들어가서 2번째 `Repository`를 누르면 아래사진처럼 초록색 `NEW버튼`이 보인다.<br><br>
![new repo](https://lh3.googleusercontent.com/kMMSLaGWXB17CLu0Z6oGD29-OnKovERYajQruyd-Ig1ugQ87AAwrtWeCUzm3PN50cb0ykoV5PV92pp6sFXFBumomb4Zt1_QfOdKr34jVsQBY4xwj1wtT_I7EazFBH7SQWkAJDdJRG-DtMo8zENZ58bLtbQskCcuKfLPwqXzDKLPq5UIgZLNEGvTzabTJ-HRP0jECEYdbt8cbtdgs2hSbHFcs3GMeDJ9SywS4TbmOrpZKn2VKln5Pll1rO8VCEQ0Y7bFmnjDqJQUtkzqDmqQvKuz629d2sP6Ix4kNyqcxh4_WFvazeWuluQDgebXXWNu7G0LvXXFpm-O4n9yNRRCujAKPxA2d19Wy5XC_BQ544XBsDEokvZ3LqWopxpZL4QRvVMew_v6106RrdKyXK2T7Y9Aze_r5UO_9cnZQ7ZHYhwBN6XiREUILF2eJ0zYl4qiCuR_JOC5HefAeazifQ0s4kDhObqsJzHCL-ga59q4baayusPotDTET2pl84wv5v5_8eEYs4Cw4xZjl8fQkOC8ZGXsbuLui4ZLJiJkpv6GNZVWzRR0NOVPvE4Bm2eDg5bRmkCQsH_1V0FyK5iQ7LbYGHFpE91bT6vNJIEaUxJ7ymT2YikxLX4sELvgc62-CQ2_LiIK_45ifQm78xuN5DrcZmyPQQJitexuVm3dCNePAKsEFnrt9CYYUlpvOfs3h9iKzU5dZzy-0ogwujgOsBzaVPqWv4slRGt951TVpfjo6mUl5oGNxYiF5vvd-FNzY6preSya5kjc95EnNpuTzA01SNJ9fi9SI1sshkz2L8ORmJ6ESfA3YC0QC5AQWqPT1A3EN0uUNKhDD042PBP62_7IQUXjuKbWNHezG9kCHcmYQHYYXIgqS1MGNAaQwepv8APsikcs9lF_WGnYdyYnFI4RErfUOztu_WPFJzunYWh4xazwYdGXI=w1280-h168-s-no?authuser=0)<br><br><br>
`NEW버튼`을 누르면 아래처럼 repository를 생성하는 화면이 나온다.<br><br>
![new repo](https://lh3.googleusercontent.com/6wFkvHyfijqHMl3tKFSr-jPGxpE8LW9es5dxFTl05Kgab4gXDYHwz3ZiRhgRsiez29wDyHxwgGAqf1NrYtqi83WvR4hdj5BOoeu5GjO84kw2E2vZTlUcpct8ouFvUNHdxmJNYVjbfTC25sRIachaeW0xXp0VBriZngfWdd0jMo5nZSx3jQ4cGB2kg0yCYdAMHeRZ6zMxeazKSb22nnfkbJQUeOwYlRzpkvo2vHFDu-Y6WoS_9qoFB_q1VgVQPzX54neAlNP_nyc1VC1Twl_NFAkhoCZr8sOzU-Jw5bNOD89yy6qt5687WQWuvW48ySotVr0ySPcr-MjMmZmYC7V7IZQKN8e86X27in6zEhb_Kqp3wKz0HpO4d0X39IBF2mjTpri1_UserzJMRgwtJkaDK3edhjs9AXHumQ_Vp2GqiKgvLkMu-DtJZU0APKj-VbhTqMQE4CB4GdUDnRXFqoolQF3NMyFUkFVMqHWX0w9fJNKJzX-qMeQcsvW0N3FJTYFBPpJCj-_vHS4agdulOLGkSq8FvdrtxDxUlJZdod8TjsbzwLqB5sZIh4uCk6liq5bHAnDBBCr7Ly_-4EQE5XnMDSeJY2N-tCn-aosfgKNewC6ofhFIw35bdY8wDfcBXeJmSfav7BaIEjkBhu8z64rP8ZsOR1GOVfcQV0L7KNmRLyPva2rrQ02AMFs8TMkAf8NLzATzzhVIZUPtnV_7ZXs5gzVO2g52LXvNT317DGQr8C-6m8qNk6AsuaSGuMLjtGfDY_XdfHC66yTvxnEA4IOZCVDJkTyrEYlZSXixLCeLJ23K5larB4L2M0GzAUKL5lUJf5gAtiQYuvu-vclY8pJsNjx7IU1kwYXR5xksoMR1pmGcF8d4vIlQHUPAb_MfbXm4tzPxwWhlmlBotOvAHrn4YAexhpzWklKi-1APcjfvB1b1-iY3=w948-h943-s-no?authuser=0)<br><br>
 제일 먼저 `Repository name`에 원하는 이름을 적으면 된다.<br>잘못 입력했다거나 나중에 바꾸고 싶으면 setting에 들어가서 언제든지 수정가능하기 때문에 걱정하지 않아도 된다!
 <br><br>
 그 다음, README file을 원하면 `Add a README file`에 체크표시를 하고, 원하지 않으면 바로 `create repository 버튼`을 누르면 된다.
 > `README file`은 지금 생성하는 repository에 대한 정보나 자신이 설명하고 싶은 내용을 글로 적을 수 있는 파일이다.
 
 <br><br>
 그러면 최종적으로  repository가 생성되었다는 아래와 같은 페이지가 보인다.<br>
 ![new repo completed](https://lh3.googleusercontent.com/FVV5OzgznsxX-r57muolbgKysqeFUa5AMdYQBnCfQDGV7Ixep8x49SvxiFBU_F_5b0mCKx4pelCEpK9ofDdeAz1CrWlUg3yir_Ow0wo305AYT3-PnxH5a9iv3emdaLpS773gNqF1Ob1q9mnVmUQ0JJqM8408T0WuiXpjO3yvs1wYyJ-9PZ6Kj7gArZ8Zy3vc0YRyTf9xW5qjponOVmUNP6qf_w2LEUL0qXm9JpUJKOpJidVCheUb3YDEgz2vxgic_XACRJjXGnbObS8eckmT1KoY2OharKaazH4JzZY0iNwGoNRWfnj-9F-4JJVEgrDGRXXZFG7npPy6QvhjkHn_t9Q821UBfsEVJVd4SjYYpKw3u6pHZWzYh3YPBJ-J0sZ7x_PVAyclWfMUmz4AkLgqzSk0aOOhaYRHJhGdrr0hn1YLPGnaipxtr_8UXqEMHQcN8J0wNm09l_QSr8JBNIF9LEPiOEe1jFkZZRixByqk2hvS4RpZ4-YCb878J-GuBPy2CEysGhnNJbgC5UnYQjIMc-bPTLlwzUEkZu-S9XF9scTsjl3Wt3tMJOEXR-EhjDo9tsjOaIBkRyN2LW749TiJgSvedgrJKlKksFaEcb7sB0gBbs7u531MVs7ZSWBNMaoAKnxtPNn8ZLimGNZm0vb9F7yRVlY4zDT0LrcMuu0RsK3R6UlSO14Ggpk2HExTiB0XWJrXiC9IB_edSeShYDd2sXEfArsJLmOVyjBrXn3vmCLIXuTC_Tu1wf8SgWLw2sKk1BahzKOAuoqI1MomaLlmBUgBe78NeoyMVSFhXmBvVkl4nVF7bUE8cQyacRpkbMqQ_mB26VnbevlxuIAraw19p369Z-nw5utig0FIgnOUeiniTcJIogk6IPdi8yRAlgMsp_IjK4jnY-gsiE749TYTHWlXNrixjiMRJjvKntgFrzJgLz_i=w1920-h894-s-no?authuser=0)<br>
 <br>
 HTTPS에서 자신의 repository 주소를 확인할 수 있다.<br>
⇨ ```https://github.com/<github ID>/<repository 이름>.git```<br><br>
 위 사진에서 빨간박스안의 버튼을 누르면 HTTPS 주소가 자동으로 복사된다. <br>버튼을 눌러 주소를 미리 복사해두자.<br>
 <br>그럼 repository 준비는 끝났고 이제 폴더를 올려보자!

 <br><br><br>

 
## 2. Git Bash Here를 이용해서 폴더 올리기
 github에 업로드할 폴더의 상위폴더에서 우클릭을 해서 `Git Bash Here`를 클릭한다.<br><br>
 ** 이때, `Git Bash Here`가 보이지 않는다면 아직 Git이 자신의 컴퓨터에 설치되지 않은 것이다.<br>
 [Git Download](https://git-scm.com/downloads)를 클릭해서 먼저 다운로드를 받고 이어서 진행하면 된다.<br>
 
 <br>
 검정 화면이 나오면  아래의 명령어를 입력하여 정상작동이 되는지 확인부터 해보자.<br>
  
  ```bash
  git init
  ```
  >해당 폴더에 `.git`이라는 파일이 생성된다.<br>
  >(master)라는 표시가 나오면 일단 정상작동이다.

<br>
  
  여기서 오류가 발생한다면 global 체크를 해봐야 한다.
  <br>아래의 코드를 따라해보자.
  
### - Bash 설정하기
 
  ```bash
git config --global user.name "본인의 Git 닉네임"
git config --global user.email "본인의 Git 이메일 주소"
``` 
 > 여기서 `--global`은 전역으로 설정해준다는 뜻으로, 이후에 다른 Repository나  폴더에서 올릴때도 따로 수정할 일이 없으면 손대지 않아도 된다. 

<br><br>


### - branch  변경하기
위에서 말한 (master)라는 표시는 Github의 branch를 의미한다.<br>
그런데 Github의 기본 branch 이름은 `main`이기 때문에, `master를 main으로 변경`하려고 한다.<br>
(만약 branch가 다른곳이라면 main 이름만 바꾸면 되고,  master branch를 그대로 사용하고 싶다면 이 부분을 건너뛰면 된다.)  <br>
```bash
git checkout -b main
```



<br><br>

### - Repository에 push하기
이제 원하는 폴더를 업로드하기 위해 아래의 명령어를 순서대로 입력하자.<br>
> 참고로 Git Bash에서 복사는 `ctrl + insert키`이고
> 붙여넣기는 `shift + insert키`이다.

```bash
git status 
git add 폴더이름 
git commit -m "본인이 원하는 커밋 메시지"
git remote add origin 복사한repository주소
git push origin main
```

마지막줄인 `git push origin main`을 입력했을 때, 오류가 날 경우 아래처럼 입력하면 된다.

```bash
git push origin +main
```

<br><br><br>
이제 본인의 Github 페이지로 가서 확인해보면 폴더가 정상적으로 올라간 것을 확인할 수 있다.



