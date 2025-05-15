# STL 시간 복잡도 & 특징
| 자료구조     | STL 컨테이너                             | 접근 (Access)      | 검색 (Find)        | 삽입 (Insert)      | 삭제 (Erase)       | 특징 요약                         |
| -------- | ------------------------------------ | ---------------- | ---------------- | ---------------- | ---------------- | ----------------------------- |
| 배열  | `array`                              | O(1)             | O(n)             | 불가               | 불가               | 고정 크기, 빠른 인덱스 접근              |
| 동적 배열 | `vector`                             | O(1)             | O(n)             | O(1) (Amortized) | O(n)             | 동적 크기, 메모리 연속, 뒤에서만 빠른 삽입/삭제  |
| 덱        | `deque`                              | O(1)             | O(n)             | O(1) (양쪽)        | O(1) (양쪽)        | 양쪽 빠른 삽입/삭제, 메모리 분할 가능        |
| 리스트      | `list`                               | O(n)             | O(n)             | O(1) (Iterator)  | O(1) (Iterator)  | 양방향 리스트, 임의 접근 불가             |
| 스택       | `stack` (vector, deque 기반)           | O(1)             | O(n)             | O(1)             | O(1)             | LIFO, top()/push()/pop() 사용   |
| 큐        | `queue` (deque 기반)                   | O(1)             | O(n)             | O(1)             | O(1)             | FIFO, front()/push()/pop() 사용 |
| 우선순위 큐   | `priority_queue`                     | O(1) (top)       | O(n)             | O(log n)         | O(log n)         | 힙 기반, 최대/최소 요소 빠른 접근          |
| 힙 (이진)   | `make_heap`, `push_heap`, `pop_heap` | O(1) (top)       | O(n)             | O(log n)         | O(log n)         | 직접 힙 조작 가능, 정렬 필요 시 사용        |
| 셋        | `set`                                | O(log n)         | O(log n)         | O(log n)         | O(log n)         | 이진 트리 기반, 자동 정렬, 중복 불가        |
| 멀티셋      | `multiset`                           | O(log n)         | O(log n)         | O(log n)         | O(log n)         | 중복 허용                         |
| 맵        | `map`                                | O(log n)         | O(log n)         | O(log n)         | O(log n)         | Key-Value, 자동 정렬, 중복 키 불가     |
| 멀티맵      | `multimap`                           | O(log n)         | O(log n)         | O(log n)         | O(log n)         | 중복 키 허용                       |
| 언오더드 셋   | `unordered_set`                      | O(1) (Amortized) | O(1) (Amortized) | O(1) (Amortized) | O(1) (Amortized) | 해시 기반, 정렬 없음, 중복 불가           |
| 언오더드 멀티셋 | `unordered_multiset`                 | O(1)             | O(1)             | O(1)             | O(1)             | 해시 기반, 중복 허용                  |
| 언오더드 맵   | `unordered_map`                      | O(1) (Amortized) | O(1) (Amortized) | O(1) (Amortized) | O(1) (Amortized) | Key-Value, 해시 기반, 중복 키 불가     |
| 언오더드 멀티맵 | `unordered_multimap`                 | O(1)             | O(1)             | O(1)             | O(1)             | 해시 기반, 중복 키 허용                |
| 비트셋      | `bitset`                             | O(1)             | O(1)             | O(1)             | O(1)             | 고정 크기 비트 배열, 논리 연산 최적화        |

- unordered_* 컨테이너는 최악의 경우 O(n) 가능 (해시 충돌 발생 시).
- vector는 중간 삽입/삭제가 느림, 대신 메모리 연속성으로 캐시 효율 좋음.
- list는 삽입/삭제 빠르지만, 임의 접근 불가.
- priority_queue는 STL에서는 최대 힙이 기본 (최소 힙은 커스텀 필요).
- bitset은 크기가 컴파일 타임에 고정됨 (dynamic_bitset은 boost 필요).
