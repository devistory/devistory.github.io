---
title: TypeScirpt 정리
date: 2025-02-27 00:00:00 +09:00
description: TypeScirpt 내용 정리
categories: [Web, TypeScript]
tags: [Front-End, TypeScript]
hidden: false
image:
  path: /assets/img/logo/typescript_logo.png
  alt: TypeScript
---

## TypeScript란?
`TypeScript`는 `JavaScript`의 슈퍼셋(Superset) 으로, 정적 타입(static type)을 지원하는 프로그래밍 언어입니다. Microsoft에서 개발했으며, JavaScript의 단점을 보완하고 대규모 애플리케이션 개발을 쉽게 하기 위해 만들어졌습니다.


> **참고 사항** <br/>
> \-`슈퍼셋(Superset)` 기존 언어(또는 시스템)를 확장하여 더 많은 기능을 제공하는 것을 의미합니다.<br/>
> \- `서브셋(Subset) `은 기존 언어에서 일부 기능만 포함한 것을 의미 합니다.<br/><br/>
> Example <br/>
>    · `TypeScript`는 `JavaScript`의 Superset (더 많은 기능 제공)<br/>
>    · `JavaScript`는 `TypeScript`의 Subset (TypeScript의 일부 기능만 제공)
{: .prompt-info }

<br/>

---

## 주요 특징
 - **정적 타입(Static Typing) 지원** : `변수(Variable)`, `함수(Function)`, `객체(Object)`에 타입을 명시하여 코드 안정성을 높일 수 있습니다.
 - **객체지향 프로그래밍(OOP) 지원** : `클래스(Class)`, `인터페이스(Interface)`, `제네릭(Generics)` 등을 지원하여 유지보수성을 강화 할 수 있습니다.
 - **ES6+ 문법 지원** : 최신 `JavaScript` 문법을 사용할 수 있으며, 브라우저 호환성을 위해 구버전 JavaScript로 변환할 수도 있습니다.
 - **JavaScript와 100%호환** : 기존 `JavaScript` 코드를 `TypeScript`에서 그대로 사용할 수 있으며, `TypeScript` 코드를 컴파일(transpile) 하면 `JavaScript`로 변환됩니다.

<br/>

---

## TypeScript의 기본 타입 종류
### 기본 타입(Primitive Types)
- JavaSciprt에서 사용되는 원시 타입(Primitive Types)을 그대로 사용할 수 있습니다.

| 타입        | 설명             | 예제           |
| ----------- | ---------------- | -------------- |
| `string`    | 문자열           | `"Hello"`      |
| `number`    | 숫자(정수, 실수) | `42`, `3.14`   |
| `boolean`   | 참/거짓          | `true`,`false` |
| `null`      | 값이 없음        | `null`         |
| `undefined` | 정의되지 않음    | `undefined`    |

```typescript
let firstName: string = "Alice";
let greeting: string = `Hello, ${firstName}!`; // 템플릿 리터럴 사용 가능

let isActive: boolean = true;
let hasPermission: boolean = false;

let empty: null = null;
let notAssigned: undefined = undefined;
```

<br/>

### 배열(Array)
- TypeScript에서는 배열의 요소 타입을 명시할 수 있습니다.

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];
let strings: Array<string> = ["a", "b", "c"];
let mixed: (string | number)[] = [1, "two", 3];
```

<br/>

### 튜플(Tuple)
- 튜플은 고정된 개수의 요소를 가지는 배열로, 각 요소의 타입이 다를 수 있습니다.

```typescript
let person: [string, number, boolean] = ["Alice", 25, true];

// 잘못된 할당 (순서가 맞지 않음)
// person = [25, "Alice", true]; // ❌ 오류 발생
```

<br/>

### 객체(Object)
 - 객체의 속성과 타입을 명확하게 정의할 수 있습니다.
 - 객체 타입이 복잡해지면 interface를 사용하여 구조를 정의할 수 있습니다.

```typescript
let user: { name: string; age: number } = { name: "Alice", age: 25 };

interface User {
  name: string;
  age: number;
}

let user2: User = { name: "Bob", age: 30 };

let user3: { name: string; age: number; isAdmin?: boolean } = { 
  name: "Alice", 
  age: 25 
};

// 선택적 속성 사용
user3.isAdmin = true;
```

> **참고 사항** <br/>
> \- user3 내에 `isAdmin?: bolean`에서 ?는 해당 속성의 사용이 불확실 할 경우 사용<br/>
> \- ?가 없는 속성은 필수로 값이 있어야 하지만 ?를 사용하면 해당 속성을 선택적(optional property)으로 사용 가능
> 
{: .prompt-info }


<br/>

### 열거형(Enum)
- `enum`은 이름이 있는 상수 집합을 정의하는 타입입니다.

```typescript
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}

let move: Direction = Direction.Up;
console.log(move); // 0

// 수동으로 값 지정
enum Status {
  Success = 200,
  NotFound = 404,
  ServerError = 500
}

console.log(Status.Success); // 200

// 문자열 Enum
enum Role {
  Admin = "ADMIN",
  User = "USER",
  Guest = "GUEST"
}

console.log(Role.Admin); // "ADMIN"
```

<br/>


### 리터럴(Literal)
- `Literal(리터럴)` type을 사용하면 특정 값만 허용할 수 있습니다.

```typescript
let status: "success" | "error" | "loading";
status = "success"; // ✅ 정상
// status = "fail"; // ❌ 오류 발생 (정의되지 않은 값)

function handleResponse(response: "success" | "error") {
  if (response === "success") {
    console.log("요청이 성공했습니다!");
  } else {
    console.log("요청이 실패했습니다!");
  }
}

handleResponse("success"); // ✅ 정상
// handleResponse("pending"); // ❌ 오류 발생
```

<br/>

### 타입 별칭(Type Alias)
 - `Type Alias`를 사용하면 복잡한 타입을 단순하게 정의할 수 있습니다.

#### 기본 사용
```typescript
type UserName = string;
let userName: UserName = "Alice"; // string 타입과 동일
```

#### 객체 타입 Alias
```typescript
type User = {
  name: string;
  age: number;
  isAdmin?: boolean; // 선택적 속성
};

let user1: User = { name: "Alice", age: 25 };
let user2: User = { name: "Bob", age: 30, isAdmin: true };
```

#### 함수 타입 Alias
```typescript
type GreetingFunction = (name: string) => string;

const greet: GreetingFunction = (name) => `Hello, ${name}!`;

console.log(greet("Alice")); // "Hello, Alice!"
```

#### 유니온 타입 Alias
```typescript
type Status = "success" | "error" | "loading";

let responseStatus: Status = "success";
// responseStatus = "failed"; // ❌ 오류 발생
```

#### 여러 타입 조합 Alias
```typescript
type ID = string | number;

let userId: ID = 123;
userId = "abc123"; // ✅ 정상
// userId = true; // ❌ 오류 발생
```

#### 객체와 유니온 타입 조합
```typescript
type SuccessResponse = {
  status: "success";
  data: string;
};

type ErrorResponse = {
  status: "error";
  message: string;
};

type ApiResponse = SuccessResponse | ErrorResponse;

let response1: ApiResponse = { status: "success", data: "Data loaded" };
let response2: ApiResponse = { status: "error", message: "Failed to load data" };
```

### any 
- `any`는 어떤 타입이든 저장할 수 있는 타입으로, `TypeScript`의 타입 검사 기능을 무력화합니다.
- `any` 타입을 많이 사용하면 `TypeScript`의 장점을 잃게 되므로 필요할 때만 사용하는 것이 좋습니다.

```typescript
let value: any = "Hello";
value = 123; // 가능
value = true; // 가능
```


> **주의 사항** <br/>
> `any` 타입을 많이 사용하면 `TypeScript`의 장점을 잃게 되므로 필요할 때만 사용하는 것이 좋습니다.
>
{: .prompt-warning }

<br/>

### unknown
- `unknown`은 `any`와 비슷하지만, 사용하기 전에 타입 검사를 해야 하는 타입입니다.
- `unknown`은 `any`보다 안전하게 동작하며, 타입 검사를 강제하기 때문에 더 권장됩니다.

```typescript
let input: unknown;
input = "Hello"; // 가능
input = 42; // 가능

if (typeof input === "string") {
  console.log(input.toUpperCase()); // 타입이 확인되면 안전하게 사용 가능
}
```

<br/>

### void
- `void`는 값을 반환하지 않는 함수의 반환 타입으로 사용됩니다.

```typescript
function logMessage(message: string): void {
  console.log(message);
}
```

<br/>

### never
- `never`는 절대 반환되지 않는 함수의 반환 타입입니다.
- `never`는 함수가 예외를 던지거나 무한 루프에 빠질 때 사용됩니다.

```typescript
function throwError(message: string): never {
  throw new Error(message);
}
```

<br/>

---

## 인터페이스(Interface)
 - `인터페이스(Interface)` 는 객체의 구조를 정의하는 역할을 합니다.<br/>즉, 어떤 속성과 메서드를 가져야 하는지 명시하는 타입입니다.
 - `인터페이스`는 `type`과 비슷하지만, 주로 객체의 구조를 정의하는 데 사용됩니다.
클래스에서 구현(implements)할 수도 있습니다.
 - 인터페이스를 왜 사용할까?
    - 코드의 일관성 유지
    - 자동 완성 기능 활용 가능 (VS Code에서 유용)
    - 여러 객체에서 공통적인 구조를 정의하여 재사용성 증가

### Interface 기본적인 사용법

```typescript
interface User {
  name: string;
  age: number;
  isAdmin?: boolean; // 선택적 속성
}

const user1: User = {
  name: "Alice",
  age: 25,
};

const user2: User = {
  name: "Bob",
  age: 30,
  isAdmin: true, // 선택적 속성 포함
};
```
> `isAdmin?: boolean;` 처럼 속성명 뒤에 ?를 붙이면 `선택적 속성(optional property)` 이 됩니다.

<br/>

### 함수 타입 Interfcae
 - 인터페이스를 함수 타입에도 사용할 수 있습니다.

```typescript
interface AddFunction {
  (x: number, y: number): number;
}

const add: AddFunction = (a, b) => a + b;

console.log(add(5, 10)); // 15
```

<br/>

### Interface 상속 (Extends)
 - 하나의 인터페이스를 다른 인터페이스에서 `확장(extends)` 할 수도 있습니다.

```typescript
interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  position: string;
}

const employee: Employee = {
  name: "Charlie",
  age: 28,
  position: "Developer",
};
```

>Employee 인터페이스는 Person을 확장하므로, name과 age 속성도 포함해야 합니다.

<br/>

### 클래스에서 인터페이스 구현하기 (Implements)
- 클래스에서 인터페이스를 구현할 수도 있습니다.

```typescript
interface Animal {
  name: string;
  makeSound(): void;
}

class Dog implements Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound() {
    console.log("Woof! Woof!");
  }
}

const myDog = new Dog("Buddy");
myDog.makeSound(); // "Woof! Woof!"
```
> Dog 클래스는 Animal 인터페이스를 구현했기 때문에 name 속성과 makeSound() 메서드를 반드시 포함해야 합니다.

<br/>

---

## 제네릭 (Generics)
- `제네릭(Generics)`은 다양한 타입에서 재사용할 수 있는 유연한 코드를 작성할 수 있게 해주는 기능입니다. <br/>즉, 타입을 동적으로 지정할 수 있는 도구입니다.
- `제네릭`을 사용하면 같은 로직의 코드에서 다양한 타입을 사용할 수 있습니다.

<br/>

### 제네릭 함수 사용하기
```typescript
function identity<T>(value: T): T {
  return value;
}

console.log(identity<number>(42)); // 42
console.log(identity<string>("Hello")); // "Hello"
```
> <T> : 여기서 T는 제네릭 타입 변수로, 함수가 호출될 때 타입을 지정할 수 있습니다.

<br/>

### 제네릭을 활용한 배열 함수
```typescript
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}

console.log(getFirstElement<number>([1, 2, 3])); // 1
console.log(getFirstElement<string>(["a", "b", "c"])); // "a"
```
> 배열 타입도 제네릭을 활용하면 더 유연하게 사용할 수 있습니다.

<br/>

### 제네릭 인터페이스
```typescript
interface Box<T> {
  value: T;
}

const numberBox: Box<number> = { value: 42 };
const stringBox: Box<string> = { value: "Hello" };
```
> Box<T>를 사용하여 value의 타입을 유동적으로 설정할 수 있습니다.

<br/>

### 제네릭 클래스
```typescript
class Storage<T> {
  private data: T;

  constructor(value: T) {
    this.data = value;
  }

  getData(): T {
    return this.data;
  }
}

const stringStorage = new Storage<string>("Hello");
console.log(stringStorage.getData()); // "Hello"

const numberStorage = new Storage<number>(100);
console.log(numberStorage.getData()); // 100
```
> 제네릭 클래스를 사용하면 다양한 타입을 저장할 수 있습니다.

<br/>

### 제네릭 & extends (제약 조건 추가)
```typescript
function getLength<T extends { length: number }>(item: T): number {
  return item.length;
}

console.log(getLength("Hello")); // 5
console.log(getLength([1, 2, 3])); // 3
// console.log(getLength(100)); // ❌ 오류 발생 (length 속성이 없음)
```
> T extends { length: number }를 사용하면 T는 반드시 length 속성을 가진 타입이어야 합니다.

<br/>

### 제네릭을 사용한 유틸리티 타입 만들기
```typescript
type ApiResponse<T> = {
  status: "success" | "error";
  data: T;
};

const userResponse: ApiResponse<{ name: string; age: number }> = {
  status: "success",
  data: { name: "Alice", age: 25 },
};

console.log(userResponse);
```
> 제네릭을 활용하면 API 응답 타입을 유연하게 만들 수 있습니다.

<br/>

---

## TypeScript를 사용하면 좋은 경우
 - 대규모 프로젝트
 - 협업이 필요한 프로젝트
 - 안정적인 코드가 필요한 경우
 - 최신 JavaScript 기능을 사용하고 싶은 경우

## 마무리

`typescript`에 대해서 정리하였습니다. 해당 내용 이외에도 더 많은 내용이 있기 때문에 필요하시면 `참고 자료`를 참조하시면 됩니다.

<br/>

📑 **참고 자료**
- [Inpa Dev 블로그](https://inpa.tistory.com/entry/TS-📘-타입스크립트-타입-선언-종류-💯-총정리)
- [코딩애플(타입스크립트 쓰는 이유 & 필수 문법 10분 정리)](https://youtu.be/xkpcNolC270?si=_J5kPfvURz4MNaZK)

<br/>


<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>