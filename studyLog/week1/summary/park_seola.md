# 이름
- 변수의 이름만 보고도 무엇을 하는 것인지 짐작할 수 있게 하라.
- 모든 이름은 문자로 시작해서 문자로 끝내야 한다.
    - _(밑줄)로 시작하거나 끝나는 이름은 public 속성이나 전역 변수들을 의미하는데,
    - 프로그램을 제대로 작성했다면 public 속성이나 전역 변수들은 private이여야 한다.
    - $(달러) 기호는 코드 생성기나 트랜스파일러, 매크로 처리기에서 사용할 목적으로 추가됨
    - 서수형 변수는 thing_nr(person_one), 기수형 변수는 nr_things(two_persons)
- 모든 이름은 소문자로 시작해야 한다.
    - new를 사용하지 말라(생성자 함수)
- 예약어를 변수의 이름으로 사용하지 말라

# 불타입
- 불 타입은 두개의 값, true/false만 가질 수 있다.
- NaN은 ===와 !==이 기대한 대로 동작하지 않기 때문에 NaN인지 확인하려면 반드시 **Number.isNaN(x)**를 써야한다.
- === 연산자는 안전한 정수 범위 안에 있을 경우에 사용하고, ===보다 ≥ 연산자가 더 안전하다.
- == 와 !=는 강제로 형변환을 하기 때문에 절대 사용해서는 안된다.

### 불인 척 하기

| falsy한 값 | truty한 값 |
| --- | --- |
| false, null, undefined, “”, 0, NaN | 다른 모든 값 |
- 조건문은 true나 false여야 한다.(불인 척 하는 값x)

  ### 논리 연산자(!, &&, ||)

- 논리 연산자는 복잡해 질 수 있으니 단순화 해서 사용하자.
- `!!p === p` 인 경우 `p`가 불 값일 경우에만 정확함
- 비교 연산자의 경우

```jsx
!(a === b) === a !== b 
!(a <=  b) === a  >  b
!(a >   b) === a <=  b
!(a >=  b) === a <   b
```

- 드모르간 법칙 사용

```jsx
!(p && q) === !p || !q
!(p || q) === !p && !q
```

### 요약

‘불인 척 하는 값’을 피하고 진짜 불 값을 사용하라

# 배열
- **자바스크립트의 배열은 진짜 객체이다.**
- 배열과 객체의 차이점
    - 배열의 length 속성은 가장 큰 색인보다 1 큰 값을 나타낸다.
    - 배열은 Object.prototype보다 더 좋은 메서드를 가지고 있는 Array.prototype을 상속한다.
    - 배열 리터럴을 사용해 만들어진다.
    - JSON은 배열과 객체를 다르게 취급하지만 자바스크립트는 둘을 비슷하게 처리한다.
- 배열이 배열인지 확인하려면 `Array.isArray(value)`를 사용해야 한다.
### 배열의 원점

- 원점이 무엇인지 확실히 해야 한다. ([0]인 경우 0번째라는 말을 사용)

### 초기화

- 배열 리터럴
- new Array
- 실제로 같은 배열인 경우에만 같다고 봄 `[1,2] !== [1,2]`

### 스택과 큐

- pop, push - 스택
- shift, unshift - 큐 (속도가 pop과 push에 비해 많이 느림)

### 검색

- indexOf, lastIndexOf 모두 찾는 값이 없으면 **-1**을 반환하므로 반환 값이 -1인지 검사해야한다.
- includes는 true, false 반환

### 축약

- reduce 메서드는 배열을 하나의 값으로 축약한다.
    - reduce 메서드의 설계 방식
        1. 전달한 함수를 배열의 모든 요소에 대해 호출하는 법 (초기 값 필수)
            - 덧셈인 경우 초기 값이 0, 곱셈인 경우 1, Math.max인 경우 -Infinity
        2. 전달되는 함수가 한 번 덜 호출되는 법 (0번째 요소가 초기 값)
    - reduceRight 함수는 배열의 끝에서 시작
### 반복

- forEach의 세 가지 인자, element, index, array 중 array는 처리되는 동안 배열을 수정하기 때문에 절대 해서는 안된다.
- reduce 이외의 반복 메서드는 반대 방향으로 처리하는 방법이 없는데, for 구문이 사라지는 것을 막기위해 뺀 건 아닐까 생각한다고 함🤔
- 반복 메서드의 반환 값
    
    
    | 메서드 | 반환 값 | 중간 종료 여부 |
    | --- | --- | --- |
    | every | 반환 값이 false면 처리 중단 및 false 반환, true면 계속 진행, 배열의 끝에 도달하면 true 반환 | o |
    | some | 반환 값이 true면 처리 중단 및 true 반환, false면 계속 진행, 배열 끝에 도달하면 false 반환 | o |
    | find | 처리 중인 배열 요소의 값을 반환 | o |
    | findIndex | 배열 요소의 index 반환 | o |
    | filter | 항상 배열의 끝까지 처리하며 반환 값이 true인 배열 요소의 목록을 배열로 반환함 | x |
    | map | 인자로 전달된 함수의 모든 반환 값을 모아서 새로운 배열로 반환 | x |

### 정렬

- sort 메서드는 **배열 자체를 수정**해서 위험하다.
- 문자열로 간주해서 정렬하기 때문에 숫자를 전달할 때 문자열처럼 정렬한다.
    - ex) [11,13,17,2,23,3,5,7]
- 비교함수
    - 0번째 요소가 배열의 앞쪽에 와야 할 경우 음수
    - 1번째 요소가 앞쪽에 와야할 경우 양수
    - 어느 쪽이 앞쪽으로 가야 할 지 알 수 없을 때는0 반환
- sort 함수는 안정성을 보장하지 않는다.
    - ex) 이름으로 정렬하고 성으로 정렬하는 경우 성으로 정렬할 때 이름으로 정렬한 순서가 사라짐

### 그 외의 내용

- concat 메서드는 두 개 이상의 배열을 연결해서 새로운 배열로 만듦
    - [1,2,3].concat([4,5])  → [1,2,3,4,5]
- join 메서드는 문자열 배열과 구분자를 인자로 받아 큰 문자열로 만듦
    - [1,2,3].join(’&’) → “1 & 2 & 3”
- reverse 메서드는 배열의 요소들을 반대 방향으로 뒤집음 (원본 배열 수정)
    - [1,2,3].reverse() → [3,2,1]
- slice 메서드는 배열 일부나 전체를 복사할 수 있음
    - [1,2,3].slice(0,1) → [1]

## 순수함, 그리고 순수하지 않음

| 함수 종류 | 메서드명 |
| --- | --- |
| 순수 함수 | concat, every, filter, find, findIndex, forEach, indexOf, join, lastIndexOf, map, reduce, reduceRight, slice, some |
| 비순수 함수 | fill, pop, push, shift, unshift, splice |
| 순수 함수여야 했던 비순수 함수 | reverse, sort |

# 객체

- 객체에는 undefined를 저장하지 않는 것이 좋다.
- 속성을 찾을 때 쓰는 키 값은 대소문자를 구별한다.
- `Object.assign` 함수로 객체의 속성들을 다른 객체로 복사할 수 있다.

### 상속

- `Object.create(*prototype*)`은 이미 있는 객체를 전달받아 이를 상속받는 새로운 객체를 반환한다.
- 프로토타입의 체인은 짧은 것이 좋다.
- 객체의 속성에 값을 대입하면, 가장 새로운 객체, 프로토타입 체인의 가장 위쪽에 있는 객체만 변경된다.
- 프로토타입을 쓰는 주된 용도는 함수를 저장하는 공간으로 사용하는 것인데, `Object.prototype`의 메서드들은 거의 쓸모가 없다.
- 객체가 상속받은 메서드와 같은 이름의 속성을 가지고 있으면 메서드 대신 객체의 속성이 함수로서 호출된다.
    
    ```jsx
    object.hasOwnProperty = 7; 
    object.hasOwnProperty("bar")  // Exception
    ```
    
- 객체의 속성 확인을 위해 JSON.stringfy를 사용할 수 있다.
    - `object.toString`은 “[object Object]”를 반환해서 쓸모가 없다
- `Object.assign(Object.create({}), prototype)` 보다 `Object.creat(prototype)` 이 메모리를 덜 쓴다.
- Object.create(null)을 쓰면 객체가 아무것도 상속받지 않게 만들 수 있다.

### 키

- `Object.keys(object)`는 객체의 모든 속성의 이름을 문자열의 배열로 반환하는데, 삽입된 순서로 나열된다.

### 동결

- `Object.freeze(objct)` 함수는 객체를 전달받아 최상위 객체를 동결해서 신뢰성을 높여준다.
- `Object.freeze` 는 값에 적용되고 `const` 는 변수에 적용된다. `const` 의 객체는 수정이 가능하지만 일반 변수에 불변 객체를 지정해도 객체를 변경할 수 없다.

### 프로토타입과 동결을 같이 쓰지 마세요.

- Object.create는 새로운 객체를 만드는 시간을 아낄 수 있지만, 프로토타입을 뒤지느라 속성 값을 가져오는 것은 비용이 들 수 있다.
- 객체가 동결되어 있으면 위 방법을 사용할 수 없다.
- 프로토타입 전체를 뒤지는 것은 Object.create(null)을 써서 피할 수 있다.

### WeakMap

- 기존 객체는 객체의 속성 이름이 반드시 문자열이여야 하고, 문자열이 아니면 키 객체를 toString 메서드를 통해 키 문자열로 변환한다.
- WeakMap은 문자열을 제외한 다른 객체를 키로 쓴다.
- 객체에 비밀스럽게 보관되어야 할 속성을 추가할 때 유용하다.

```jsx
const secret_key = new WeakMap();
secret_key.set(object, secret);  // key, value

secret = secret_key.get(object);
```

- 동결된 객체에 효율적으로 비밀스러운 속성을 추가할 수 있다.
- 봉인자(sealer)와 개봉자(unsealer)

```jsx
function sealer_factory() {
	const weakmap = new WeakMap();
	return {
		sealer(object) {
			const box = Object.freeze(Object.create(null));
			weakmap.set(box, object);
			return box;
		},
		unsealer(box) {
			return weakmap.get(box);
		}
	};
}
```

- WeakMap은 키를 갖고 있지 않는 한 값을 볼 수 없다.(검사 허용 x)
- WeakMap은 가비지 컬렉터와 잘 맞는다.
