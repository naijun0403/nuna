# nuna
(우리의 가상) 누나 언어 v0.4

## 명세
### 변수 (variables)
누나 언어는 하나의 스택을 갖습니다.\
시스템 변수를 제외한 모든 변수는 이 스택에 저장됩니다.\
스택의 아이템은 `스택 번호(index)`와 `값(variable)`로 구성되며
이때 값은 `부호있는 정수형(signed integer)`을 의미합니다.

### 변수 가르키기 (variable pointer)
누나 언어는 `pointer`라는 시스템 변수를 갖습니다.\
이는 현재 가르키고 있는 `스택 번호`를 의미합니다.\
언어를 실행할때 `pointer`값은 `0`으로 초기화됩니다.
이는 아무 `스택 번호`도 가르키지 않음을 의미합니다.\
`pointer`와 `스택 번호`가 같은 아이템을 `현재 값`이라고 합니다.\
`pointer - 1`과 `스택 번호`가 같은 아이템을 `이전 값` 혹은 `앞의 값`이라고 합니다.

### 키워드 (keywards / operations)
#### `눈`, `누`
스택에 `1`을 값으로 하는 아이템을 추가하고
`pointer`값에 1을 더합니다.\
뒤에 `.`이 있을경우 `.`의 개수만큼을 값으로 합니다. [예제](examples.md#눈-누-예제)

#### `난`, `나`
현재 값에 `1`을 곱합니다.\
뒤에 `.`이 있을경우 `.`의 개수만큼을 곱합니다. [예제](examples.md#난-나-예제)

#### `주`
현재 값에 `1`을 뺍니다.\
뒤에 `.`이 있을경우 `.`의 개수만큼을 뺍니다. [예제](examples.md#주-예제)

#### `거`
현재 값에 `1`을 더합니다.\
뒤에 `.`이 있을경우 `.`의 개수만큼을 더합니다. [예제](examples.md#거-예제)

#### `헤`
`POP` 작업을 수행합니다.\
이때 `POP`작업이란 현재 값을 없는것(like `undefined` or `None`)으로 하고
포인터에서 `1`을 빼는 것을 의미합니다.\
이 작업은 스택의 길이를 `1`만큼 줄입니다. [예제](examples.md#헤-예제)

#### `으`
이전 값을 의미합니다.\
`.` 대신 사용할 수 있습니다. [예제](examples.md#으-예제)

#### `응`
이전 값에서 현재 값을 뺍니다.\
이전 값은 없는 것(like `undefined` or `None`)으로 합니다. [예제](examples.md#응-예제)

#### `흐`
현재 값에 `1`을 제곱합니다.\
뒤에 `.`이 있을경우 `.`의 개수만큼을 거듭제곱합니다.\
`흐`로 시작한 문장은 `읏`으로 끝나야 합니다. [예제](examples.md#흐-읏-예제)

#### `읏`
아무런 행동을 하지 않습니다.\
`흐`로 시작한 문장을 끝낼때 사용합니다.

#### `💕`
이전 값에서 현재 값을 더합니다.\
이전 값은 없는 것(like `undefined` or `None`)으로 합니다. [예제](examples.md#-예제)

#### `!`
현재 값을 UTF-8 인코딩 출력합니다.\
대부분의 구현체가 출력으로 stdout을 사용합니다.

#### 그 외
`눈` `누`, `난`, `나`, `주`, `거`, `.`, `헤`, `으`, `응`, `흐`, `읏`, `💕`, `!`가 아닌 다른 문자들은 문법 오류입니다.

`.`와 `으`를 요구하지 않는 키워드에서 `.`와 `으`를 사용할 경우 `.`과 `으`는 무시됩니다. [예제](examples.md#외1-예제)

`.`와 `으`를 요구하는 키워드에서 `.`와 `으`가 사용되지 않은 경우 `1`으로 간주합니다.

이전 값을 요구하는 키워드를 사용할때 이전 값이 없을 경우 `0`으로 간주합니다.  [예제](examples.md#외2-예제)

## 예제
```
눈나..흐.....읏..나주..거....흐...읏...
누..나..나...흐....읏..나주..거....💕
눈나.....나..흐...읏나.....주거...💕
누나..흐..읏나.......주..거......응읏..!

눈나..으흐읏
누으나.....주..흐....읏나....응
누나.....나..주...읏나......응!
```
* @pmh-only님이 제작하셨습니다
* 출력 결과: 누나

## 구현체
2021년 3월 13일 기준 구현체 목록입니다.
* [nunalang/web-nuna](https://github.com/nunalang/web-nuna) - [공식] 웹누나 구현체
* [hui1601/nuna-interpreter](https://github.com/hui1601/nuna-interpreter) - [비공식] C++ NUNA 인터프리터
* [pl-Steve28-lq/PyNuna](https://github.com/pl-Steve28-lq/PyNuna) - [비공식] Nuna Language Interpreter Implemented with Python
* [franknoh/nuna-interpreter](https://github.com/franknoh/nuna-interpreter) - [비공식] nodejs NUNA 인터프리터

### 공식 구현체 만족 조건
다음 조건을 맞춘 구현체는 이슈로 남겨주시면 nunalang레포로 옮겨드립니다.
* 명세를 최대한 따릅니다.
* 구현체 이름에 `누나` 혹은 `Nuna`(대소문자 구분 없음)이 포함되어 있습니다.
* 리드미에 "사용 가능한 정수 범위"와 "신뢰성을 보증하는 정수 범위"를 표기하여야 합니다.
* 리드미에 `!` 키워드 출력 방식을 서술하여야 합니다.
* 한글자로 보기 어려운 `💕` 문자를 어떻게 처리하였는지 서술하여야 합니다.
