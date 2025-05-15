# C++ 캐스팅 연산자 정리
내가 정리한걸 gpt로 마크다운으로 한번 더 정리한거라 불펌 금지
## 1. 캐스팅 연산자 개요

| 캐스팅 연산자            | 목적                                 | 타입 안전성         | 런타임 검사 | 권장 여부      |
| ------------------ | ---------------------------------- | -------------- | ------ | ---------- |
| `static_cast`      | 타입 변환 (상속, 기본 타입 변환)               | 중간             | 없음     | 일반적 사용     |
| `dynamic_cast`     | 안전한 다운캐스팅 (RTTI 사용)                | 높음             | 있음     | 다형성 클래스 권장 |
| `const_cast`       | `const`, `volatile` 속성 제거 및 추가     | 낮음 (UB 가능성 있음) | 없음     | 제한적 사용     |
| `reinterpret_cast` | 메모리 비트 재해석 (위험성 높음)                | 매우 낮음          | 없음     | 거의 사용하지 않음 |
| `(C-style)`        | 혼합 변환 (static, reinterpret 혼합 가능성) | 낮음             | 없음     | 사용 지양      |

---

## 2. `static_cast`

* 컴파일 타임에 타입 계층(상속 관계)만 검사
* 실제 객체 타입 무시 → 다운 캐스팅 시 UB 발생 가능
* 다형성(가상함수) 필요 없음

```cpp
// 예시
class A {};
class B : public A {};
A* a = new B();
B* b = static_cast<B*>(a); // OK (런타임 타입 무시)
```

---

## 3. `dynamic_cast`

* RTTI 사용 → vptr → vtable → type\_info로 런타임 타입 체크
* 다형성 클래스에서만 사용 가능 (가상함수 필수)
* 실패 시 포인터는 `nullptr`, 참조는 예외(`std::bad_cast`) 발생

```cpp
// 예시
class A { virtual void f() {} };
class B : public A {};

A* a = new A();
B* b = dynamic_cast<B*>(a); // 실패 시 nullptr
```

---

## 4. `const_cast`

* `const` 또는 `volatile` 속성 제거/추가
* 런타임에서 readonly 영역 접근 시 UB 발생 가능

```cpp
// 예시
const int x = 10;
int* p = const_cast<int*>(&x);
*p = 20; // UB 가능
```

---

## 5. `reinterpret_cast`

* 메모리 비트 수준에서 타입 재해석
* 매우 위험 (UB 발생 가능성 높음)
* 플랫폼 종속적, 사용 제한적 권장

```cpp
// 예시
int n = 0x12345678;
char* p = reinterpret_cast<char*>(&n); // 메모리 직접 접근
```

---

## 6. C++20 `std::bit_cast`

* 메모리 비트를 안전하게 reinterpret
* 타입 크기 동일해야 하며 안전성이 강화됨
* 일반적인 메모리 reinterpret에 권장

```cpp
// 예시
int a = 42;
float f = std::bit_cast<float>(a);
```

---

## 7. 사용 권장 순서

```
std::bit_cast (C++20) > static_cast > dynamic_cast > const_cast > reinterpret_cast
```

---

## 8. 꼬리 물기 질문 예시

* `const_cast`가 실제 const 객체인지 런타임에 구분 가능한가?

  * 불가능 → UB 발생 가능
* `reinterpret_cast`를 권장하지 않는 이유는?

  * 타입 검사 무시, 메모리 UB 가능성, 플랫폼 종속성 때문


