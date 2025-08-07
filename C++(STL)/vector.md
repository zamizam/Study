## vector란?

- C++ STL의 시퀀스 컨테이너 중 하나
- **동적 배열 (Dynamic Array)** 구조
- **임의 접근(Random Access)** 지원 → O(1)
- 끝에서의 삽입/삭제는 **상수 시간 O(1)**  
- 중간 삽입/삭제는 **선형 시간 O(n)**  
- 내부 메모리는 **Heap**에 할당됨

---

## vector 주요 함수 정리

### 요소 접근

| 함수 | 설명 |
|------|------|
| `v[i]` | i번째 요소 접근 (범위 검사 X) |
| `v.at(i)` | i번째 요소 접근 (범위 검사 O, 예외 발생) |
| `v.front()` | 첫 번째 요소 참조 |
| `v.back()` | 마지막 요소 참조 |
| `v.begin()` | 첫 요소를 가리키는 iterator |
| `v.end()` | 마지막 다음 요소 (역참조 X) |
| `v.rbegin()` | 역방향 첫 요소 |
| `v.rend()` | 역방향 끝 요소 (역참조 X) |

### 크기 및 메모리 관련

| 함수 | 설명 |
|------|------|
| `v.size()` | 요소 개수 |
| `v.capacity()` | 할당된 용량 |
| `v.resize(n)` | 크기 조정 |
| `v.reserve(n)` | 용량 확보 (재할당 방지) |
| `v.shrink_to_fit()` | 불필요한 capacity 제거 |
| `v.empty()` | 비었는지 확인 |
| `v.clear()` | 모든 요소 제거 (capacity 유지) |

### 삽입 및 삭제

| 함수 | 설명 |
|------|------|
| `v.push_back(val)` | 끝에 요소 추가 |
| `v.emplace_back(args)` | 요소를 직접 생성하여 추가 (생성자 호출 생략) |
| `v.pop_back()` | 마지막 요소 제거 |
| `v.insert(pos, val)` | 지정 위치에 요소 삽입 |
| `v.erase(pos)` | 지정 위치의 요소 제거 |
| `v.swap(other)` | 다른 벡터와 내부 데이터를 교환 |
| `v.assign(n, val)` | n개의 val로 벡터 초기화 |

---

## vector 사용 시 주의할 점

- `v[i]`는 **범위 검사하지 않으므로** 접근 시 주의해야 함 (UB(Undefined Behavior) 발생 가능)
- `v.at(i)`는 **범위를 벗어나면 예외**를 던짐 (`std::out_of_range`)
- `v.end()`는 **실제 요소가 아님** → 역참조하면 안 됨
- `v.reserve()`로 미리 메모리를 확보하면 **재할당 비용**을 줄일 수 있음
- 요소 삭제 후 `iterator`는 무효화됨 (특히 중간 삭제 시)

---

## vector 성능 관련

- 연속된 메모리 덩어리를 사용하여 **캐시 효율이 좋음**
- 요소 개수가 많아질 경우 **capacity가 2배씩 증가**하며 재할당됨
- 재할당 시에는 **모든 요소가 복사 이동됨** → 성능 이슈 주의
- `emplace_back()`은 `push_back()`보다 불필요한 복사/이동이 없어서 빠름

---

## 예시 코드

```cpp
std::vector<int> v;
v.reserve(100);       // 미리 100개 용량 확보
v.push_back(10);      // 요소 추가
v[0] = 20;            // 요소 변경
std::cout << v.at(0); // 예외 안전 접근
```

## 요약 키워드

- `vector` : 동적 배열 / 임의 접근  
- `push_back`, `emplace_back` : 요소 추가  
- `reserve`, `capacity` : 메모리 최적화  
- `at` vs `[]` : 예외 vs 속도  
- `begin`, `end` : iterator 범위  
- `resize`, `shrink_to_fit` : 사이즈 조정 및 메모리 회수  

## 연관 키워드

- [`list`](./list.md) : 연결 리스트 구조로, 중간 삽입/삭제가 vector보다 빠름. 랜덤 접근은 불가  
- [`deque`](./deque.md) : 양쪽 끝 삽입/삭제에 모두 최적화된 시퀀스 컨테이너  
- [`array`](./array.md) : 정적 크기의 배열. 런타임에 크기 변경 불가하지만 매우 빠름  
- [`stack`](./stack.md), [`queue`](./queue.md) : vector 기반의 어댑터 컨테이너. vector의 후방 삽입 성능 활용  
- [`string`](./string.md) : 내부적으로 vector와 유사한 구조를 가지는 동적 문자열 컨테이너  
