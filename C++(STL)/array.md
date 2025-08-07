## array란?

- **C++11부터 도입된 STL 정적 배열 컨테이너**
- `std::array<T, N>` 형태로 사용 (크기 `N`은 **컴파일 타임 상수**)
- **고정 크기 배열**로, `vector`처럼 크기 변경 불가
- **스택 메모리(stack)**에 할당 → **할당/해제 비용 없음**
- 일반 C 배열보다 **안전하고 STL 알고리즘과 호환됨**

---

## array 주요 함수 정리

### 요소 접근

| 함수 | 설명 |
|------|------|
| `a[i]` | i번째 요소 접근 (범위 검사 X) |
| `a.at(i)` | i번째 요소 접근 (범위 검사 O, 예외 발생) |
| `a.front()` | 첫 번째 요소 참조 |
| `a.back()` | 마지막 요소 참조 |
| `a.data()` | 내부 raw pointer 반환 (C 배열처럼 사용 가능) |

### 반복자

| 함수 | 설명 |
|------|------|
| `a.begin()` | 첫 요소를 가리키는 iterator |
| `a.end()` | 마지막 다음 요소 |
| `a.rbegin()` | 역방향 첫 요소 |
| `a.rend()` | 역방향 끝 요소 |
| `a.cbegin()` | const iterator 시작 |
| `a.cend()` | const iterator 끝 |

### 크기 관련

| 함수 | 설명 |
|------|------|
| `a.size()` | 전체 요소 개수 (항상 N) |
| `a.empty()` | 비었는지 확인 (N이 0이면 true) |
| `a.fill(val)` | 모든 요소를 val로 채움 |
| `a.swap(other)` | 두 array 간 요소 교환

---

## array 사용 시 주의할 점

- `N`은 **컴파일 타임 상수** → 런타임 크기 변경 불가
- **동적 배열이 필요하면 `vector` 사용**
- 내부적으로 `T arr[N]`과 유사하지만, `size()`, `at()`, 반복자 등을 제공
- STL 알고리즘과 잘 연동됨 (`std::sort`, `std::accumulate` 등)

---

## array 성능 관련

- **스택 메모리** 사용 → 매우 빠름
- 힙 할당이 없으므로 메모리 오버헤드가 적고 캐시 효율도 높음
- 반복자 기반 연산에서도 `vector`와 성능 차이 거의 없음
- 크기가 크거나 런타임 크기 조정이 필요하면 부적절

---

## 예시 코드

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};
    arr[0] = 10;
    std::cout << arr.at(0) << std::endl;  // 예외 안전 접근
    arr.fill(0);                          // 모든 요소를 0으로 설정
    return 0;
}
```
## 요약 키워드

- `array` : 정적 배열, 크기 고정  
- `at`, `[]` : 예외 안전 vs 성능  
- `fill`, `swap` : 전체 값 설정, 교환  
- `data` : 내부 포인터 접근  
- STL 알고리즘과 호환되는 C++ 배열  

---

## 연관 키워드

- [`vector`](./vector.md) : 동적 크기 배열, 런타임 확장 가능  
- [`deque`](./deque.md) : 양방향 삽입/삭제, 내부는 비연속적  
- [`list`](./list.md) : 연결 리스트, 중간 삽입/삭제 최적화  
- [`stack`](./stack.md) : LIFO 구조의 컨테이너 어댑터  
- [`queue`](./queue.md) : FIFO 구조의 컨테이너 어댑터  
