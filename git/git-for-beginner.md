# github for beginner

### `touch < file name > .md ` 

* `touch` 는 create과 같은 의미이다. 
* 깃 명령어가 아닌 기본 탐색 명령어이다.

### `git status` 

```bash
git status

On brance master
Untracked files:
		(use "git add <file>..." to include in what will be 		committed)
```

### `git add < file name > .md` 

### `git commit -m "< Message >"`

### `git push origin master`

# git의 작업흐름



![git_add_commit_push](basic.assets/git_add_commit_push.png)

### add -> commit -> push 

`add` 커밋할 목록에 추가

`commit`  커밋 (create a snapshot) 만들기

`push`  



`git commit -m "message"` 

message : 여기에 메세지 설명

* 뼈대 코드 구성
* 메인 기능 구현 등등



> commit convention 날짜 | 수정한 내용 적기

`.gitignore` 파일 만들고 `git touch .gitignore` 또는 VS code에서 파일만들기  

.gitignore에 파일 이름 올리면 파일 숨겨짐

즉, 깃으로 관리하지 않아도 되는 파일들 이름을 적기

e.g. b.txt --> 파일 숨김

e.g. test/ --> 폴더 숨김



* 근데 하나씩 입력하기 힘드니까  https://www.toptal.com/developers/gitignore 자동으로 만들어줌
* https://git-scm.com/book/en/v2 git 기본서 

![Git Flow timeline by Vincent Driessen, used with permission](basic.assets/gitlab_flow_gitdashflow.png)