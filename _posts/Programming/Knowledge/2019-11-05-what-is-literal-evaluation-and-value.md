---
layout: post
title: "literal, evaluation and value"
date: 2019-11-05
description: "프로그래밍에서 어떤 값을 literal과 evaluate 결과 생성되는 value로 구분할 수 있다는 것과 그것이 가지는 유용성을 이해합니다."
img:  /knowledge/literal-value-logo.jpg
categories: [Programming, Knowledge]
tags: [literal, evaluation, value]
---

<br id="1">

## 1. literal, evaluation and value

---

### 우리는 수많은 '값'을 사용한다


우리는 현실에서 수많은 `값`을 사용한다. 오늘 사 마신 커피는 _4100_ 원이었고 내가 방금 노트에 적은 글자는 _응용_ 이었다. `값`이라는 것은 어떤 **의미**를 말하는 것 같다. 조금은 철학적이기까지 한데 중요한 것은 우리가 만들고 사용하는 모든 것에는 의미가 있다. 그 의미가 개인적이든, 조직과 사회에 폭넓게 공유되는 것이든. 나는 경영학을 전공했음에도 경영학이라는 학문의 값 또는 의미는 개인적으로 별로 무겁지 않다. 대신 프로그래밍이나 영어 등이 훨씬 무겁고 중요하게 다가온다. 반면 1, 2, 3, ...과 같은 값은 보통 상식을 가진 사람들에게 폭넓게 공유되는 값 또는 의미이다. 우리는 이 추상적인 값의 의미를 공유하며 따라서 한 번의 이혼과 두 번의 이혼의 의미를 구별할 수 있다.

값의 사용은 프로그래밍에서도 매우 빈번하다. 수많은 값을 우리는 변수와 상수에 할당해 사용한다. 변수 할당은 어떤 프로그래밍 언어에서도 지원하는 매우 기본적인 기능이며 나도 오늘도 사용했다. 물론 `값`에는 단순히 숫자뿐 아니라, True와 같은 bool, string과 같은 수많은 종류가 존재한다.

<br>

### 값은 개념을 분해할 수 있다

**값은 보다 구체적으로 자신을 구성하는 개념으로 분해할 수 있다.** 어떻게 분리할 수 있다는 뜻일까? 가령 우리는 100을 100이라고만 생각한다. 사실 당연한 생각인 것은 맞다. 근데 이 _100_ 을 살펴보자. 이때 우리는 이 100이라는 것이 인간에게 익숙한 십진수 표기법을 따른 값이라는 것을 잘 안다. 그렇다면, **우리는 얼마든지 십진수가 아닌 진수로 100에 해당하는 값을 표현 또는 표기할 수 있다.** 100이라는 값은 2진수로는 1100100, 8진수로는 144, 16진수로는 64가 된다. **이들은 형태는 달라도 모두 같은 숫자를 표현한다.**

$$
100 = 1100100_{(2)} = 144_{(8)} = 64_{(16)}
$$

이때 **우리는 어떤 값의 실제 의미를 상황에 맞게 다양한 표기로 표현할 수 있다는 것을 깨달을 수 있다.** 이는 조금만 생각해보면 당연하다. 바로 위의 경우도 그렇고 마찬가지로 현실에서도 같은 의미를 전달하는 서로 다른 표기 또는 단어가 존재하는 것을 알 수 있다. 이를 동의어(synonym)이라고 하며 그 예로는 '가게'와 '상점', '넓이'와 '면적', '음식점'과 '식당'과 같이 쉽게 찾을 수 있다.

다시 프로그래밍으로 넘어와서, **우리는 하나의 `값`은 `표기`와 그것이 갖는 `의미`로 개념을 구분할 수 있다는 것을 알았다. 이때 의미를 전달하는 실제 표기를 영어로는 literal, 그 표기가 전달하는 의미는 value라고 한다.** literal은 프로그래밍을 공부했으면 몇 번씩은 접해봤을 듯 하다. 1, 2, 3과 같이 프로그래밍을 하는 데 필수적인 정수는 interger literal이라고 따로 표현도 하며, 'asdf'와 같은 문자열, True, False와 같은 bool 인스턴스도 literal이다. 심지어는 자료구조를 literal로 표현하기도 한다. 파이썬의 핵심 자료구조라 하면 누구나 알 듯 list, tuple, dict, set인데 이때 `[]`는 빈 list, `{}`는 빈 dict를 표현하는 literal이다. 이중 set은 literal을 사용해 빈 set을 표현할 수 없는데 이는 set과 dict가 같은 `{}`를 생성기호로 사용하기 때문이다. 따라서 빈 set을 생성하기 위해서는 자신의 생성자 함수를 호출하는 것만이 방법이다.(_set()_)

이렇게 어떤 값을 literal과 value로 나눌 수 있다.

<br>

### 하나의 value는 여러 literal을 가질 수 있다

이제 본격적으로 중요한 부분이다. literal과 value를 굳이 구분하는 이유는 무엇일까? 이는 literal과 value가 일련의 관계를 갖기 때문이다. 절의 제목을 그대로 이용해서 하나의 value는 여러 가지 형태의 literal을 가질 수 있다. 앞서 100이라는 하나의 값을 다른 진수로 표현할 수 있음을 확인했다. 이때 **우리가 알고 있는 100이라는 십진수가 전달하는 value는 각종 진법에 따라, 다른 요구에 따라 서로 다른 literal로 표현될 수 있는 것이다.** 일반화하면 `하나의 value는 여러 개의 literal을 보유할 수 있다`

그리고 **literal들의 실제 value를 계산하는 것을 evaluate라고 하는데 이 evaluate 과정은 모든 프로그래밍에서 찾아볼 수 있다.** 가령 100의 2진수 표현과 16진수 표현은 분명 다르게 생겼다. 하지만 이들의 평가값은 같다는 것을 파이썬에서 확인해볼 수 있다.

```python
# bin과 hex는 각각 십진수를 2진수, 16진수 문자열로 반환하는 내장함수
bin_100 = bin(100)
hex_100 = hex(100)

print(bin_100)
print(hex_100)

0b1100100
0x64
```

십진수 100을 각각 2진수와 16진수로 변환했다. bin과 hex는 각각 십진수를 2진수, 16진수 문자열로 반환하는 내장함수로 실제 개발에서 많이 유용하지는 않아서 그런지 많이들 모르기도 한다. 참고로 8진수로 변환하는 _oct_ 내장함수도 있다.

어쨌든 두 가지 literal이 반환됐는데 사실 **파이썬에서는 0b, 0x과 같은 접두사를 쓰면 일반 십진수 literal을 사용하듯이 2진수, 16진수 정수 literal을 만들 수 있다.** 이때 `'` 작은따옴표가 필요하지 않다.


```python
print(0b1100100)
print(0x64)
```

<br>

이때 **서로 다른 진수 표기법이지만 이들을 evaluate하면 이들이 실제 갖는 value를 얻을 수 있다.**

```python
print(100 == 0b1100100)
print(0b1100100 == 0x64)
print(0x64 == 100)


True
True
True

# 따라서 이 세 값은 모두 같은 value를 갖는다!
```

이들은 모두 생김새와 길이가 다른 literal임에도 evaluate 결과 동일한 value를 갖고 있는 것을 알 수 있다. 이때 비교연산자로 `==`를 사용했는데 **적어도 파이썬에서 `==`는 양쪽에 literal을 받아 literal 자체가 아니라 이들을 evaluate한 value값을 비교한다는 것을 여기서 확인할 수 있다.**

재밌는 예로 파이썬에서 `True`라는 bool literal은 사실 정수 1과 같은 평가값을 갖는다. False는 예상했듯이 0이다.

```python
print(True == 1)
print(False == 0)

True
True
```

<br> 

여담으로 value와 literal의 관계를 데이터베이스에서 사용하는 _many-to-one_ 관계로 표현할 수도 있겠다. 하나의 literal은 하나의 value를 갖는다. 반대로 하나의 value는 여러 literal을 '소유'할 수 있다. 이를 ERD로 표현하면 다음과 같다.

![ERD of value and literal](/assets/img/knowledge/literal-value-erd.png)

ERD는 many-to-one 관계를 표현하고 있는데 저 작대기를 이해하기가 어렵다. 조금 해설하자면 **각 박스(value, literal)는 자신에게 서 멀리 있는 기호를 끌어다 해석하면 된다.** value는 'o'과 새 발 기호, literal은 'o'와 '\|'. 이때 새 발 기호는 '여러 개'를 의미한다. 그러면 '하나의 value는 여러 개의 literal을 가질 수 있다'가 되는데 'o'는 가지지 않을 수도 있다는 추가적인 의미라서 최종적으로 '하나의 value는 여러 개의 literal을 가질 수 있되, 가지지 않을 수도 있다'가 된다. 반대로 literal 측은 '하나의 literal은 하나의 value를 가질 수 있되, 가지지 않을 수도 있다'라는 뜻이 된다.

이때 '가지지 않을 수 있다'라는 것이 개인적으로 흥미롭다. 값이 없는 literal이나, 표기 없는 value도 세상에는 존재할 수 있다. 가령 '뜳똘낈'이라는 literal은 방금 내가 만들었는데 딱히 value가 없다. 그리고 아직 표기되지 않은 value의 표기를 만드는 것은 학자와 예술가들의 위대하고 평범한 취미인 것 같기도 하다. 백남준이 비디오아트라는 표기법을 만들어낸 것처럼...

마지막으로 이런 질문도 할 수 있다. '정말 literal은 하나의 value만 가질 수 있나? 아닐 수도 있을 것 같은데?' 가령 `사자`라는 표기는 다의어로서, 'lion', 'herald', 'dead people' 등의 뜻을 갖는데? 여기서부터는 심히 철학적이라 내게 더는 어렵다. 하지만 **내 생각에 적어도 프로그래밍적으로는 하나의 literal은 하나의 value만을 갖는다.** 하나의 literal이 여러 평가값을 가지면 소스코드 컴파일이 안 된다. 마주친 `|`라는 기호가 가질 수 있는 뜻이 여러 개면 여기서는 어떤 뜻을 적용해야 할지 알 수 없기 때문이다. 이렇게 보면 **literal과 value는 함수 관계에 있다고 할 수도 있겠다. 하나의 literal은 하나의 value에 매핑되며, 이때 함수의 이름은 evaluate이 된다.**

$$
func \text{  } evaluate(literal) \text{  } -> value
$$

<br> 

### 유연함이 주는 자유를 누려라

이제 좋다. 우리는 literal과 value를 구별할 수 있고, 하나의 값이 여러 개의 literal을 가질 수 있다는 것도 잘 안다. 그러면 이것이 어떻게 우리에게 도움이 될 수 있을까? 내 생각은, **하나의 value가 여러 개의 literal을 가질 수 있다는 점에서 그 value의 표현형태를 우리가 취사선택할 수 있다는 유연함이 생긴다고 생각한다.** 심지어는 **value에 대한 literal을 요구상황에 맞게 내가 창조해낼 수 있다.** 내 블로그에 그런 예시가 하나 있다. 전에 작성한 [실용적인 비트마스크 활용예제 포스트](https://shoark7.github.io/programming/knowledge/some-useful-bit-tricks-and-usages#4){:target="_blank"}에서 어떤 숫자의 k번째 비트를 끄는 연산을 집합론의 관점에서 구현한 코드가 있다. 이때 가령 어떤 수 n에 대한 표기를 위해 응당 2진수 표기를 쓸 수도 있겠으나 여기서 최선은 아닌 것 같다. 이유는 첫 째, $$1010...$$ 수열에서 정확히 k번째 비트가 어디인지 한눈에 보기 힘들다는 점과, 두 번째로 우리는 집합론의 관점에서 비트를 끄고, 정확히 차집합의 유명한 공식을 그대로 사용해 비트마스킹을 하는데 2진수 표기 자체는 전혀 집합처럼 보이지 않는다는 것이다.

그래서 **내가 포스트에서 고안한 표기는 어떤 수 N을 켜져 있는 비트 자리의 집합으로 표현하는 것이다.** 가령 210이라는 십진수는 2진수로 $$11010010_{(2)}$$인데 이때 1, 4, 6, 7번째 비트가 켜져 있으므로 이 값의 집합적 표기를 다음과 같이 쓴다.

$$
210 = 11010010_{(2)} = \{1, 4, 6, 7\}
$$

**이 표기는 적어도 내가 만든 체제 안에서는 다른 진수 표현들과 평가값이 같다.** 그리고 어떤 십진수 N에 대한 비트 집합 표기는 언제나 유일하기 때문에 문제가 없다.

**이렇게 어떤 정수를 집합적으로 표현하면 특정 비트를 끈다는 표현을 차집합으로 이해하는 것이 훨씬 수월해진다.** 단순히 그 수에서 꺼지는 비트를 담은 집합을 빼는 식으로 이해할 수 있기 때문이다. 가령 이 수에서 6번째 비트를 끈다면 다음과 같을 것이다.

$$
\{1, 4, 6, 7\} - \{6\} = \{1, 4, 6, 7\} \cap \{6\}^\complement = \{1, 4, 7\} = 2^7 + 2^4 + 2^1 = 146
$$

이때 $$2^6$$은 64이기 때문에 146은 210에서 정확히 64를 뺀 값이 된다. 집합론의 그 유명한 차집합 공식을 사용하면 다음과 같이 코드를 짤 수 있을 것이다.

```python
print(210 & ~(1 << 6))


146
```

**210과 $$\{1, 4, 6, 7\}$$은 적어도 내 세계에서는 평가값이 같다.** 따라서 어떤 수에서 비트 끄기를 사용할 때는 편리한 십진수 표기인 210을 그대로 사용하고, 집합 기호에 맞는 비트 연산자를 사용해 비트를 끈다.

이렇게 어떤 값에 대한 표기를 유연하게 확장하고 새로 만들어 우리가 원하는 작업을 하는 데 유용하게 사용했다. 우리는 이처럼 어떤 창의적인 작업을 위해 literal을 다양하게 창조하고 사용할 새로운 가능성을 얻게 됐다. 이것이 기존에 없던 자신의 어떤 독특한 세계나 값을 표현하기 위해 예술가들이 항상 하는 짓이 아닐까?

<br>

### 요약・정리

오늘은 포스트 제목 그대로 value, evaluate, literal을 살펴봤다. value는 실제 어떤 의미 또는 값이다. 이 값 자체는 추상적인 의미로 머리에 새겨진 이미지라고 짧게 설명해볼 수 있다. 그리고 그것의 실제적인 표기를 literal이라고 한다. literal은 프로그래밍 전반에서 매우 많이 쓰이며, 단순히 1, 2, 3과 같은 숫자도 어떤 값을 표기하는 literal이고, 문자열, 심지어는 자료구조를 표현하는 literal도 있다. 이때 literal이 갖는 실제 value를 구하는 것을 evaluate, 즉 '평가한다'고 한다.

literal과 value의 관계는 하나의 value는 여러 개의 literal을 가질 수 있으며, 하나의 literal은 적어도 프로그래밍에서는 현실적인 필요에 의해 하나의 value를 가질 수 있다. 서로 다른 literal은 생김새가 다를지언정 같은 value를 가질 수도 있기 때문에 이들을 비교할 때는 일반적으로 literal 자체가 아니라 이들을 evaluate한 value로 비교한다.

이런 관점은 어떤 값이나 의미를 다른 literal로 표기해 유연하게 바라볼 수 있게 하며 특정 상황에서 다른 literal로는 어려울 수 있는 의미 파악을 더욱 용이하게 할 수 있다.

<br>
<br>

## 2. 자료 출처

---

* [integer literal: wikipedia](https://en.wikipedia.org/wiki/Integer_literal){:target="_blank"}
* [literal: wikipedia](https://en.wikipedia.org/wiki/Literal_(computer_programming)){:target="_blank"}
* [동의어: wikipedia](https://ko.wikipedia.org/wiki/%EB%8F%99%EC%9D%98%EC%96%B4){:target="_blank"}
