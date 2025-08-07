
## List란?

- C++ STL의 시퀀스 컨테이너 중 하나
- 이중 연결 리스트(Doubly Linked List) 구조
- 삽입/삭제가 빠른 컨테이너 (중간 지점 포함)
- 각 요소는 메모리 상에서 연속되지 않은 위치에 존재하며 포인터로 연결됨
- 임의 접근(Random Access)이 불가능 → `list[i]` 같은 문법은 지원되지 않음

---

## List 주요 함수 정리

### 요소 접근 (제한적)

| 함수 | 설명 |
|------|------|
| `l.front()` | 첫 번째 요소 참조 |
| `l.back()` | 마지막 요소 참조 |
| `l.begin()` | 첫 요소를 가리키는 iterator |
| `l.end()` | 마지막 다음 요소 (역참조 금지) |
| `l.rbegin()` | 역방향 첫 요소 |
| `l.rend()` | 역방향 끝 요소 (역참조 금지) |

※ 리스트는 `[]`, `at()`을 통한 임의 접근을 지원하지 않음

---

### 삽입 및 삭제

| 함수 | 설명 |
|------|------|
| `l.push_back(val)` | 끝에 요소 추가 |
| `l.push_front(val)` | 앞에 요소 추가 |
| `l.pop_back()` | 끝 요소 제거 |
| `l.pop_front()` | 앞 요소 제거 |
| `l.insert(pos, val)` | pos 위치에 요소 삽입 |
| `l.erase(pos)` | pos 위치의 요소 제거 |
| `l.remove(val)` | 값이 val인 요소 제거 |
| `l.unique()` | 연속된 중복 요소 제거 |
| `l.clear()` | 모든 요소 제거 |
| `l.resize(n)` | 요소 개수 조정 |
| `l.assign(n, val)` | n개의 val로 리스트 초기화 |

---

### 정렬, 병합 등 고유 기능

| 함수 | 설명 |
|------|------|
| `l.sort()` | 요소 정렬 (내부 알고리즘 사용) |
| `l.merge(other)` | 정렬된 두 리스트 병합 |
| `l.reverse()` | 요소 순서 반전 |
| `l.splice(pos, other)` | 다른 리스트의 요소를 특정 위치로 이동 |

※ 리스트는 자체적으로 `sort`, `merge` 등의 알고리즘을 내장하고 있음  
→ 이유: 랜덤 접근 불가 → `std::sort()` 등 일반 알고리즘과 호환되지 않음

---

## List 사용 시 주의할 점

- 임의 접근 불가 → `list[i]`, `at()` 사용 불가
- 모든 요소 접근은 iterator 기반으로만 가능
- 삽입/삭제 후에도 iterator가 무효화되지 않음 → vector보다 안정적
- 각 노드마다 포인터 2개를 저장하므로 메모리 오버헤드가 존재

---

## List 성능 관련

- 중간 삽입/삭제가 빠름 (`O(1)` — iterator를 알고 있는 경우)
- 랜덤 접근은 느림 (`O(n)`)
- 요소 개수가 많고, 삽입/삭제가 빈번한 경우 vector보다 효율적
- sort, merge 등의 내부 알고리즘이 최적화되어 있음

---

## 예시 코드

```cpp
std::list<int> l;
l.push_back(10);
l.push_front(5);
l.sort();
l.remove(5);
```
---

## 요약 키워드

- `list` : 이중 연결 리스트 / 중간 삽입·삭제에 강함  
- `push_front`, `pop_front` : 앞쪽 조작 지원  
- `sort`, `merge`, `splice` : 고유 정렬 및 병합 기능  
- `iterator` 기반 접근 : `[]`, `at()` 불가  
- `vector`와 비교 : 랜덤 접근은 느리지만 구조 수정에 강함  

---

## 연관 키워드

- [`vector`](./vector.md) : 동적 배열 구조. 임의 접근은 빠르지만 삽입·삭제는 느림  
- [`deque`](./deque.md) : 양쪽 삽입·삭제가 가능한 시퀀스 컨테이너  
- [`forward_list`](./forward_list.md) : 단방향 연결 리스트, 메모리 절약 가능  
- [`stack`](./stack.md), [`queue`](./queue.md) : list를 기반으로 구현 가능한 컨테이너 어댑터  

