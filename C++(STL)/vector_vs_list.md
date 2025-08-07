## vector vs list : 정렬과 내부 구현 차이

### 1. sort 사용 방식

| 컨테이너 | 정렬 방식 | 설명 |
|----------|------------|------|
| `vector` | `std::sort(v.begin(), v.end())` | random access iterator 필요 |
| `list` | `l.sort()` | 멤버 함수. 내부 정렬 알고리즘 사용 |

- `std::sort`는 `RandomAccessIterator`만 지원 → `list`에는 사용 불가
- `list.sort()`는 자체 구현된 병합 정렬(merge sort) 기반 알고리즘 사용

---

### 2. 정렬 알고리즘 차이

| 항목 | `vector` (`std::sort`) | `list` (`list.sort()`) |
|------|------------------------|-------------------------|
| 기본 정렬 | Introsort (퀵+힙+삽입 정렬 혼합) | 병합 정렬 (stable) |
| 정렬 안정성 | 불안정 (값이 같을 경우 순서 바뀔 수 있음) | 안정 정렬 (값 같을 경우 순서 유지) |
| 복잡도 | 평균 O(n log n) | O(n log n) |
| 데이터 이동 | 값 복사 (move/copy) | 포인터(노드 연결)만 이동 → 대용량 구조체에 유리 |
| 조건부 정렬 | `std::sort(..., comp)` | `list.sort(comp)` 사용 가능 |

---

### 3. 내부 구현 관점에서의 차이

#### `vector` 정렬 시
- 요소가 연속된 메모리에 존재하므로 `std::sort`는 내부에서 `swap`, `move`, `copy`를 직접 수행
- 포인터나 구조체처럼 무거운 타입이면 이동 비용이 큼
- 포인터를 멤버로 갖는 객체일 경우 shallow copy(얕은 복사) 문제가 발생할 수도 있음

#### `list` 정렬 시
- 요소 자체는 노드에 존재하고, 노드는 포인터로 연결되어 있음
- `list.sort()`는 **실제 값은 이동하지 않고, 포인터(노드 간 연결)** 만 재정렬
- 따라서 `값 이동 비용이 큰 구조체` 정렬에는 `list`가 훨씬 효율적일 수 있음

---

### 4. 실무적 선택 기준

- 단순한 자료형(int, float 등) + 빠른 접근 → `vector + std::sort`
- 객체 크기가 크거나 복사가 비싼 경우 → `list + list.sort()`
- 정렬 안정성이 중요한 경우 → `list.sort()` 권장

---

### 5. 예제 코드

```cpp
// vector 정렬
std::vector<int> v = {3, 1, 4};
std::sort(v.begin(), v.end());

// list 정렬
std::list<int> l = {3, 1, 4};
l.sort(); // 내부적으로 병합 정렬 수행
```
