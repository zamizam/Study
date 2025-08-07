## queue란?

- C++ STL의 **컨테이너 어댑터 (Container Adapter)** 중 하나  
- 기본적으로 **FIFO (First-In-First-Out, 선입선출)** 구조  
- 내부적으로는 `deque`(또는 `list`)를 이용해 구현됨  
- **가장 먼저 들어온 데이터가 가장 먼저 나감**  
- **랜덤 접근 불가**, front/back 접근만 가능

---

## queue 주요 함수 정리

### 요소 접근

| 함수 | 설명 |
|------|------|
| `q.front()` | 첫 번째 요소 참조 |
| `q.back()` | 마지막 요소 참조 |

### 삽입 및 삭제

| 함수 | 설명 |
|------|------|
| `q.push(val)` | 뒤에 요소 추가 |
| `q.emplace(args)` | 요소를 직접 생성하여 추가 |
| `q.pop()` | 앞에서 요소 제거 |

### 크기 및 상태

| 함수 | 설명 |
|------|------|
| `q.size()` | 요소 개수 |
| `q.empty()` | 비었는지 확인 |

---

## queue 사용 시 주의할 점

- `queue`는 **인덱스 접근이 불가** (`q[i]`처럼 사용할 수 없음)
- **중간 삽입/삭제 불가**, 오직 front와 back만 조작 가능
- `pop()`은 반환값이 없음 → `q.front()`로 먼저 확인 후 `pop()`

---

## queue 성능 관련

- 내부적으로 `deque` 기반 → 양 끝 삽입/삭제에 강함  
- `list` 기반으로도 구현 가능하지만, 일반적으로 `deque`가 더 빠름  
- 큐 크기가 커질 경우에도 요소 간 이동 없음 (단, 메모리 재할당 가능성은 있음)

---

## 예시 코드

```cpp
#include <queue>
#include <iostream>

int main() {
    std::queue<int> q;
    q.push(1);
    q.push(2);
    q.push(3);

    std::cout << q.front() << "\n"; // 1
    q.pop();
    std::cout << q.front() << "\n"; // 2
}
```
## 요약 키워드

- `queue` : 선입선출 구조 (FIFO)
- `push`, `pop` : 뒤에 추가, 앞에서 제거
- `front`, `back` : 양 끝 요소 참조
- `empty`, `size` : 상태 확인
- 내부는 `deque` 기반, 중간 접근 불가

---

## 연관 키워드

- [`deque`](./deque.md) : queue의 내부 구조로 사용. 양쪽 삽입/삭제 모두 지원  
- [`list`](./list.md) : queue 구현에 사용할 수 있는 양방향 연결 리스트  
- [`stack`](./stack.md) : LIFO 구조의 컨테이너 어댑터  
- [`priority_queue`](./priority_queue.md) : 우선순위 기반의 큐  
- [`vector`](./vector.md) : queue와 달리 랜덤 접근이 가능한 동적 배열  
