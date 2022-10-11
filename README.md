# 1. Linux Shell?

- 사용자가 프롬프트에  입력한  명령을  해석해서  운영체제에  전달
- 사용자 명령어 해석기

| 종류 | 의미 |
|----|----|
| Bourne Shell(sh) | Stephen Bourne / Original shell |
| C shell (csh, tcsh) | Bill Joy / C lang / History, alias, job control, vi command editing and completion |
| Korn shell (ksh) | David Korn / Bourne shell + C shell |
| Bourne-Again Shell(bash) | GNU Project / csh, ksh + works with bourne shell / Linux & Mac OS default |


- 사용 가능한 shell 리스트 확인하기
```
$ cat/etc/shells
```

- 현재 작업 shell 확인
```
$ echo $SHELL
```

- 로그인 shell 변경
```
$ cat/etc/passwd
$ [sudo] chsh [username]
```
<br>

# 2. Bash Shell과 변수

- 변수 만들기
```
$ valName=value
```

- 환경변수 선언
```
$ export valname=value
```

- 변수 조회
```
$ echo $valName
$ set [| grep 검색어]
```

- 환경변수 조회
```
$ env
```

- 변수 제거
```
$ unset valName
```

- 기억해야 하는 환경변수

| PATH | 명령어 탐색 경로 |
|---|---|
| HOME | 홈 디렉토리 경로 |
| USER | 로그인 사용자 이름 |
| SHELL | 로그인 shell의 이름 |
<br>

# 3. Bash Shell과 Rules

## 1. Quoting Rule
- Metacharacters
  - shell에서 특별히 의미를 정해 놓은 문자들
  - [₩, ?, $, ..., *, %, {}, [] 등]

```
$ echo *
$ echo a* (a로 시작하는 파일 찾기)
$ echo ??? (3글자로 된 파일 찾기)
$ touch myfile{1..4} (myfile1, myfile2, ..., myfile4 생성)
```

- Quoting Rule: 메타문자의 의미를 제거하고 단순 문자로 변경
  - \ : 바로 뒤의 메타문자 의미 제거
  - "" : 내의 모든 메타문자의 의미 제거 (단, $, ``은 제외)
  - '' : 내의 모든 메타문자의 의미 제거


## 2. Nesting Commands
- Command 안에 또다른 Command
- 괄호 안에 리눅스 Command 넣고 출력
- 또는 `` 이용 가능
```
$ echo "Today is $(date)"
$ echo "Today is `date`"
$ touch report-$(date +%Y%m%d)_v{1..4}
```


## 3. Alias

## 4. Prompt