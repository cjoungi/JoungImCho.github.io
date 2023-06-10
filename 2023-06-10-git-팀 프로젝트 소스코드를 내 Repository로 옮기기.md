---
title: "[Git/Github] 팀 프로젝트 소스코드를 내 Repository로 옮기기"

categories:
  - Git/Github
tags:
  - [tag1, tag2]

permalink: /git/팀 프로젝트 소스코드를 내 Repository로 옮기기/

date: 2023-06-10
#last_modified_at: 2021-10-09


---
 5주간의 팀 프로젝트가 끝났다.<br>
현재 다른 팀원의  깃허브 Repository에 있는 프로젝트와 관련된 모든 기록(소스코드, commit, branch, tag 등)을 개인 Repository로 옮겨보자!

 가장 먼저 Windows cmd에서 git 명령어를 사용할 수 있도록 설정해야 한다.<br>
 설정이 완료되었다면 절차는 아래와 같다.<br><br>

## 1. 기존 Repository 소스코드를 내 PC(local)로 클론(clone)하기

 이 때, 해당 branch와 tag를 전부 가져오기 위해서는 `command 창`에서 아래의 명령어로 클론을 해주면 된다.
 클론받을 폴더를 미리 만들어 둬야하며, cmd창을 실행시켜 해당 폴더의 상위 폴더로 이동한 후 아래 명령어를 실행한다.
```
 git clone --mirror <오리지널 repo 주소> <내 로컬 폴더>
```
> git clone시 `--mirror`옵션을 주면 **원격 repo의 모든 참조가 그대로 복사**된다.<br>
여기서 `원격 repo`란 내가 복사해 올 오리지널 깃허브 주소를 말한다.

<br>
ex ) 기존 팀 프로젝트의 깃허브 주소 ⇨  https://github.com/aaa<br>
   내 PC의 클론받을 폴더 위치 ⇨ C:\project\repo<br>
cmd창에 입력할 명령어 ⇨ `git clone --mirror https://github.com/aaa repo`
<br><br><br>

## 2.  내 GitHub에 새 Repository 생성하기
내 GitHub에 새 Repository를 생성할 때, Readme, gitignore등이 없는 Repository 생성을 권장한다.
다른 파일이 존재하는 경우 push할 때 conflict이 생길수도 있기 때문에 이를 방지하기 위함인 것 같다.

새 Repository 생성하면 주소는  `https://github.com/<깃허브 ID>/<Repository 이름>`  형태로 구성이 된다.
<br>
다음으로 cmd 창에서 클론받은 폴더로 이동한 후,  아래의 명령어를 입력한다.

`git remote set-url origin https://github.com/<깃허브 ID>/<Repository 이름>.git`<br>
`git push`
>위의 코드는 내가 Github에 생성한 주소를 git remote의 파라메터로 넣어주고, push를 해주는 명령어이다.

>`git remote`는 현재 내 PC에 있는 저장소를 원격 저장소로 연결하겠다는 의미이다.<br>
>여기서 `remote`란, remote repository(원격 저장소)를 지칭하며 내 PC가 아닌 **네트워크 상에 존재하는 저장소**를 말한다. <br>즉, 여러 사람이 공동 작업할 수 있는 오리지널 저장소이다. 

>옵션 `set-url`은 현재 설정된 **원격 저장소의 주소를 변경**한다. 즉, 기존에 다른 사람의 깃허브에 연결되어 있던 것을 내가 원하는(즉, 내가 새롭게 만든) 깃허브 주소로 변경할 수 있는 옵션이다.

>파라메터 `origin`은 내가 저장하는 저장소의 이름을 "origin"으로 정하겠다는 의미이다. 이 부분은 내가 알기쉬운 용어로 변경해도 되지만, 관례적으로 origin으로 사용하기 때문에 **가급적 변경없이** 그대로 가도록 한다.

<br><br>
## 3. 변경된 결과 확인하기
git push 이후 내 깃허브에 들어가서 확인하거나,  cmd창에 `git remote -v`  명령어로 확인하다.

<br><br>
---


참고링크 |<br>
[팀 개발 프로젝트가 끝난 이후에, 해당 소스코드를 내 GitHub로 옮겨와서 이어가는 방법](https://peterdrinker.tistory.com/337)

