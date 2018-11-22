---
layout: post
title: '유용한 쉘 함수 소개 Part 1'
date: 2018-11-07
description: "Let me introduce some useful shell commands to you. Part 1."
img:  /shell-programming/shell-logo.png
categories: [Programming, Shell-programming]
tags: [shell, useful_shell_commands]
---

## 들어가며

지난번까지 쉘의 매우 기초적인 기능과 쉘 활용에 필수적인 입출력 재지정, 파이프 연산자에 대해 다뤘다. 이 개념들을 바탕으로 CLI 활용을 GUI 뺨칠 수 있는 수준으로 끌어올려 보자.  

오늘은 쉘의 유용한 기능 몇 개를 다룰 예정이다. 이 기능들은 쉘 활용에 있어 필수적인 기능이라기 보다는 **알고 있으면 쉘의 활용성을 극한으로 끌어올릴 수 있는** 수준의 기능들이다. 사실상 쉘을 쓰는 이유는 이런 다채로운 기능과 입출력 재지정 등을 혼합해서 기상천외한 작업을 할 수 있기 때문이다.  

유용한 기능은 참 많고, 그래서 몇 부로 나눠서 다루려고 한다. **이번 포스트에서는 문자열을 데이터로 보고 전처리하는 데 유용한 기능을 살펴본다.** 지금까지 배운 입출력 전환과 파이프 연산을 통해 본격적으로 재밌는 작업을 예시로 들 수 있을 것 같다. 시작해 볼까?


## less

파일의 내용을 확인해보고 싶을 때가 있다. 이때 우리가 알고 있는 _cat_ 을 써도 내용이 화면에 모두 출력된다. 하지만 **_cat_ 의 단점은 파일의 내용이 길 경우 내용이 모두 한 번에 출력되어 제대로 파악하기 힘들다는 점이다.** 내용이 길 경우, 출력된 결과물을 커서를 한참을 올려가며 내용을 확인해야 할 수도 있다.  

**`less`는 파일의 내용을 한 페이지 단위로 보여주는 프로그램**으로 이런 경우의 활용에 매우 유용하다.  

활용법은 매우 간단한데, `less 파일명'과 같이 사용하면 된다.


```sh
$ less data

...
(some data)
...
```

파일의 내용이 한 페이지 단위로 출력된다. 이때 키를 입력해 페이지를 넘기거나 이전 페이지로 돌아갈 수 있는데 주요 단축키는 다음과 같다.

단축키|실행내용
---|---
PAGE UP or b| 한 페이지 위로
PAGE DOWN or 스페이스바 | 한 페이지 아래로
j | 한 줄 아래로
k | 한 줄 위로
G | 파일의 맨 아래로 이동
g | 파일의 맨 위로 이동
/'문자열'| 파일의 문자열 검색
n | 문자열 검색 사용시 다음으로 넘어가기
q | 프로그램 종료


_less_ 를 한 번 사용해보자. 이 프로그램은 경험상 꽤나 자주 사용하게 된다. 페이지 단위로 오르내리는 키는 꼭 알아둬야 의미 있게 쓸 수 있다.


<br>

파이프 연산자를 통해 _less_ 를 좀더 재밌게 활용해보자.  

**유닉스 시스템에서 '/bin' 디렉토리에는 유닉스 쉘 활용에 필수적인 프로그램들이 저장되어 있다.** 'ls /bin'을 통해 목록을 훑어보길 추천하는데, 'ls', 'rm', 'echo' 등을 포함해 매우 중요한 기능들이 저장되어 있다. 사실, 우리가 빈 쉘에 'ls'을 사용하면 내부적으로 이 디렉토리를 훑어 'ls' 프로그램을 실행시키도록 되어 있다.  

이때, '/bin' 디렉토리의 모든 기능들의 이름을 살펴보고 싶다고 하자. 단순히 'ls' 등을 써도 되지만 이 경로 안의 프로그램 수가 100여개를 훌쩍 넘기 때문에 목록이 잘려 나올 것이다. 이때 _less_ 를 써도 괜찮을 것 같다.  

파이프 연산자를 통해 결과를 확인하는데,

1. 'ls /bin'으로 결과를 출력하고,
2. 그 결과를 'less'의 입력으로 전환하면 모든 프로그램을 확인할 수 있다.


```sh
$ ls /bin | less


bash
bunzip2
...
```

수많은 프로그램의 목록을 페이지 단위로 끊어볼 수 있으니 간편하게 browse할 수 있다. 


<br>

less 프로그램을 살펴봤다. 그런데 프로그램의 이름인 'less'가 참 재밌다. 'less'는 영어로 '~덜'이라는 뜻으로 'more'의 반대말이다. 영속담 중에 'Less is more'이 있는데 '간결함이 복잡한 것보다 나을 수 있다'는 것을 뜻한다. 정말 재밌게도 'less'라는 프로그램은 정말 그 의미로 이름 지어졌다. 'less' 이전에 'more'이라는 프로그램이 있었는데 같은 기능을 수행하지만 조금 다르다. 'more'을 업그레이드 하면서 프로그램 이름을 속담을 활용해 'less'라고 지은 것이다.

쉘에 'whatis less'을 입력하면 'opposite of more'라고 나오는데, 개발자들은 분명 재미 있는 작자들이다.


## wc

개인적으로 참 좋아하는 프로그램이다. **`wc`는 'word count'의 약자로서 입력 받은 파일의 줄 수, 단어 수, 글자 수를 출력한다.**

바로 예를 확인하자.

```sh
$ echo 'as as as
111 222 333
%%%% @@@@ ####' > data
$ wc data

 3 9 36 data
```

'data' 라는 파일을 새로 만들고 _wc_ 로 결과를 확인했다.  

**결과는 줄 수, 단어 수, 글자 수, 파일의 이름을 차례로 출력한다.**

1. 파일은 3개의 줄로 이루어져 있다.
2. 파일의 단어 수를 출력한다. 이때 단어는 **whitespace을 기준으로 센다.** 예제에는 9개의 단어가 있다.
3. 글자 수를 출력한다. **글자 수는 whitespace를 포함해 다 센다. 파일의 끝에는 EOF(파일의 끝) 문자가 들어가기 때문에 결과는 보여지는 글자 +1이 된다.**  

많은 경우, 파일의 줄 수, 단어 수, 글자 수가 모두 필요하지 않고 한 가지만 필요할 때가 있을 수 있다. 이때는 다음과 같은 인자를 붙여주면 된다.

```sh
-l : line의 약자. 줄 수만 출력된다.
-c : character의 약자. 글자 수만 출력된다.
-w : word의 약자. 단어 수만 출력된다.
```

<br>

글자 수를 셀 때 주의해야 할 사항이 있다. **사실 이 프로그램은 글자를 일일이 센다기보다는 파일이 몇 바이트인지를 센다.** 이게 무엇을 의미하냐면, **영어 소대문자, 공백문자 등은 ASCII 소속으로 1바이트로 표현이 가능한 데 비해, 한글 등의 non-ascii 글자는 최소 2바이트이기 때문에 글자 수가 잘못 세진다는 것이다.**  

```sh
$ echo '가' | wc

1 1 4
```

단 한 글자만 입력했음에도 줄과 단어 수는 정상이지만, 글자 수는 다르다. **utf-8에서는 한글은 한 글자가 3바이트인데다가, 파일의 끝 문자가 붙어 결과가 4가 되었다.** 그래서 ASCII 이상의 문자셋을 사용하는 경우에는 주의를 요한다.

<br>

다른 활용을 해보자. 아까 'ls /bin'의 목록을 살펴봤다. 목록을 살피는 대신, 프로그램의 개수를 알고 싶다면 어떨까? `wc -l`을 쓰면 알 수 있다.

```sh
$ ls /bin | wc -l

163
```

내 우분투 배포에서는 '/bin'에 163개의 프로그램이 들어있음을 알 수 있다. 사실 ls의 출력에서는 한 프로그램이 하나의 단어이고 한 줄을 차지하기 때문에 'wc -w'도 결과는 같다.


## sort

**`sort`는 파일의 내용을 줄 단위로 구분해서 오름차순 정렬해 출력한다.** 하나의 줄은 문자열인데 줄을 정렬하는 것은 문자열 비교방식을 따른다. 사전식 비교라고 보면 된다.

```sh
$ echo 'c
b
a' > data

$ sort data

a
b
c
```

파일의 내용을 정렬해 출력했다. 내림차순으로 정렬하고 싶다면 '-r' 옵션을 붙이면 된다.


## uniq

**`uniq` 기능은 파일에서 중복된 줄을 지우고 출력하는 기능이다.**

```sh
$ echo 'a
a
a
b
b' > data

$ uniq data

a
b
```

중복된 줄을 지우고 유일하게(unique) 줄을 남겼다. **보통 _uniq_ 는 _sort_ 와 같이 쓰이는데, 그 이유는 _uniq_ 의 중복을 제거하는 알고리즘이 정교하고 복잡하게 짜여진 것이 아니라 단순히 이전 줄과 같은지만 확인해서 중복을 제거하기 때문이다.** 따라서 일반적인 사용시에는 _sort_ 로 정렬을 해야 이전 행과 비교해 중복을 제거할 수 있다.

```sh
$ echo 'a
b
a
b
a
b' > data

$ sort data | uniq

a
b
```

위와 같은 파일에서 _sort_ 없이 _uniq_ 를 썼다면 중복이 제거되지 않았을 것이다. _sort_ 를 먼저 하고 _uniq_ 를 사용한 이후에야 중복이 온전히 제거되었다. 궁금하면 직접 해봐도 좋다.



## head & tail

R이나 파이썬으로 데이터 전처리를 하다보면, 데이터 내용의 상태를 확인해보고 싶을 때가 있다. 그런데 데이터의 크기가 크다면 이를 전체를 보는 것은 비효율적일 것이다. 이때 `head`나 `tail`을 이용하면 유용하다.

**`head`는 파일의 첫 10줄을 출력하고, `tail`은 파일의 마지막 10줄을 출력한다.** 말 그대로이다. _cat_ 이 파일 전체를 출력한다면, 그 반대의 일을 하는 것이다.

```sh
$ echo '1
2
3
4
5
6
7
8
9
10
11
12
13
14
15' > data

$ head data

1
2
3
4
5
6
7
8
9
10
```

**_head_, _tail_ 은 '-n' 인자를 받는데 숫자와 같이 쓰여서 출력물의 줄 수를 10개가 아닌 다른 수로 정할 수 있다.**


```sh
$ tail -n 5 data

11
12
13
14
15
```


## 마치며

쉘 활용에 중요한 기능 몇 가지를 살펴봤다. 이 기능들은 평소에도 자주 쓰이기 때문에 이 정도까지 쓸 수 있으면 일단 GUI 저리가라 할 정도까지는 완성된다. 하지만 **아직 쉘의 꽃을 다루지는 않았는데 그것은 주어진 조건 하에서 파일을 찾는 _find_ 와 파일에서 정규표현식에 맞는 줄만을 추려내는 _grep_ 이다.** 이 기능은 각각 독립적인 포스트에서 다룰 예정이다.  

쉘은 참 재밌다. 이 정도는 별 것 아니지 않나? 쉘을 단순히 '나쁘지 않게 쓰는 유저'를 넘어 shell geek으로 거듭나려면 나부터 공부를 훨씬 더 해야 한다. Windows를 벗어나고 싶다면, 따라오도록 하자.  

이만 포스트를 마친다.