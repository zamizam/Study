## deque란?

- **Double-Ended Queue (양방향 큐)**  
- 앞과 뒤 **양쪽 모두 삽입/삭제 O(1)**  
- **랜덤 접근(Random Access)** O(1) 지원  
- 내부적으로 **다중 버퍼 블록**을 사용해 메모리 관리  
- `vector`와 달리 **앞쪽 삽입/삭제가 빠름**

---

## deque 주요 함수 정리

### 요소 접근

| 함수 | 설명 |
|------|------|
| `d[i]` | i번째 요소 접근 (범위 검사 X) |
| `d.at(i)` | i번째 요소 접근 (범위 검사 O, 예외 발생) |
| `d.front()` | 첫 번째 요소 참조 |
| `d.back()` | 마지막 요소 참조 |
| `d.begin()` | 첫 요소를 가리키는 iterator |
| `d.end()` | 마지막 다음 요소 (역참조 X) |
| `d.rbegin()` | 역방향 첫 요소 |
| `d.rend()` | 역방향 끝 요소 (역참조 X) |

### 크기 및 메모리 관련

| 함수 | 설명 |
|------|------|
| `d.size()` | 요소 개수 |
| `d.empty()` | 비었는지 확인 |
| `d.resize(n)` | 크기 조정 |
| `d.clear()` | 모든 요소 제거 |

### 삽입 및 삭제

| 함수 | 설명 |
|------|------|
| `d.push_back(val)` | 뒤에 요소 추가 |
| `d.push_front(val)` | 앞에 요소 추가 |
| `d.pop_back()` | 뒤 요소 제거 |
| `d.pop_front()` | 앞 요소 제거 |
| `d.insert(pos, val)` | 지정 위치에 요소 삽입 |
| `d.erase(pos)` | 지정 위치 요소 제거 |
| `d.swap(other)` | 다른 deque와 내부 데이터 교환 |
| `d.assign(n, val)` | n개의 val로 초기화 |

---

## deque 사용 시 주의할 점

- `vector`처럼 메모리가 연속적이지 않음 → **raw pointer 연동 주의**
- `front/back` 양쪽 삽입이 빈번하면 `deque`가 유리
- 중간 삽입/삭제는 여전히 **선형 시간 O(n)**
- STL 알고리즘 대부분과 호환됨

---

## deque 성능 관련

- **앞뒤 삽입/삭제 모두 빠름 (O(1))**
- `vector`와 달리 **중간 삽입에도 iterator 무효화 덜함**
- `vector`보다 **약간의 메모리 오버헤드** 존재
- 대량 삽입/삭제가 반복될 경우 **`deque`가 더 효율적**

---

## 예시 코드

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> d;
    d.push_front(1);   // 앞에 추가
    d.push_back(2);    // 뒤에 추가
    d.pop_front();     // 앞 요소 제거
    std::cout << d.at(0); // 안전하게 접근
    return 0;
}
```
## 요약 키워드

- `deque` : 양방향 삽입/삭제  
- `push_front`, `push_back` : 양 끝 삽입  
- `pop_front`, `pop_back` : 양 끝 제거  
- `at` vs `[]` : 예외 vs 성능  
- `front`, `back` : 양쪽 끝 참조  

---

## 연관 키워드

- [`vector`](./vector.md) : 연속된 메모리 / 빠른 임의 접근, 앞 삽입/삭제는 느림  
- [`list`](./list.md) : 연결 리스트 구조로 중간 삽입/삭제에 최적화  
- [`queue`](./queue.md) : 기본적으로 deque 기반의 FIFO 컨테이너 어댑터  
- [`stack`](./stack.md) : deque 기반의 LIFO 컨테이너 어댑터  
- [`array`](./array.md) : 정적 배열로 런타임 크기 변경 불가하지만 빠름  

