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
```

```
$ touch report-$(date +%Y%m%d)_v{1..4}
// (date --help 참조)
```

```
echo "Today is $(date +Y-%m-%d)"
```

## 3. Alias
- shell의 명령에 새로운 이름을 부여
- 명령들을 조합하여 새로운 이름의 명령을 생성

```
$ alias name='command'
$ alias or alias name
$ unalias name
```


## 4. Prompt
- PS1 변수를 이용해 shell의 기본 프롬프트 모양을 설정
- Bash Shell에서만 Prompt 모양에 적용 가능한 특수 문자가 존재

|특수문자|의미|
|---|---|
|\h|호스트 이름|
|\u|사용자 이름|
|\w|작업 디렉토리 - 절대경로|
|\W|작업 디렉토리 - 상대경로|
|\d|오늘 날짜|
|\t|현재 시간|
|\$|$ 또는 # 프롬프트 모양|


alias 및 PS1 변경 내용은 로그인 동안에만 적용된다.
로그인 이후에도 적용하기 위해서는 `.bashrc`(zsh, ...) 파일에 적용해주어야 한다.

## 5. Redirection
> 파일 입출력 방향 전환

- Communication Channels
keyboard -> (stdin) -> Program -> (stdout & stderr) -> Terminal

| Communication channels | Redirection characters | 의미 |
|---|---|---|
|STDIN|`0<` / `0<<`|입력을 키보드가 아닌 파일을 통해 받음|
|STDOUT|`1>` / `1>>`|표준 출력을 터미널이 아닌 파일로 출력|
|STDERR|`2>` / `2>>`|표준 에러 출력을 터미널이 아닌 파일로 출력|

0과 1은 생략가능하다.

## 6. Pipeline
> 여러 개의 명령어 조합하여 사용
> 명령의 실행 결과를 다음 명령의 입력으로 전달
> 기호: command1 | command2 | command3

```
ls -l | ws -l
ls -l | more (한 페이지씩, space 누르면 다음 페이지)
```

```
cat passwd | cut -d: -f 1 | sort | wc -l
alias usercount='cat passwd | cut -d: -f 1 | sort | wc -l'
```


