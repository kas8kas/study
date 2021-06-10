# vector containor
- 자동으로 메모리가 할당되는 배열을 뜻함.
- 중간 데이터의 삽입, 삭제에 비효율적.
- 검색에 비효율적.
- 단, 위치를 알고 있다면 제일 효율적인 접근이 가능. (맨 뒤 주소로도 접근 용이)
***
### 선언
```
  vector<자료형> 변수명;
  vector<지료형> 변수명 (size, element); //생성자 이용
  vector<자료형> 변수명 {};
  vector<자료형> 변수명 = {};
```
***
### size()와 capacity()
- size는 벡터가 실질적으로 원소를 담고 있는 크기를 뜻한다. (사용 중인 공간)
- capacity는 벡터의 수용 공간 크기를 뜻하며, 사이즈에 따라 일정 비율로 증가한다. (사용 할 수 있는 공간)
- capacity > size인 경우 : size만 증가.
- capacity == size인 경우 : 둘 다 증가.
- 동적할당을 매번 진행하게 되면 비효율적이기 때문에, capacity로 한 번에 해두는 것임.
***
### resize()와 reserve()
- .resize() : size를 재할당 하는 함수
- .reserve() : capacity를 재할당 하는 함수
- 만약 벡터의 크기를 특정할 수 있다면, reserve()함수를 통해 size 이상으로 capacity가 추가 할당되지 않도록 하는 것이 좋다.
***
### 원소 추가
- .push_back() : 맨 뒤에 원소 추가
- .emplace_back() : 맨 뒤에 원소 추가, 조금 더 효율적 (요즘은 별 차이 없음.)
- .insert(num1, num2) : num1 위치에 num2을 대입하고 iter를 반환
- .insert(num1, num2, num2) : num1 위치에 num2개의 num3를 대입, 뒤에 놈은 밀림.
***
### 원소 제거
- .clear() : 모든 원소 제거, capacity는 그대로
- .pop_back() : 맨 뒤 원소 제거
- .swap() : 교환해주는 함수, capacity가 0인 임시객체를 생성해 제거용으로 사용 가능.
- .erase(iter) : iter가 가르키는 원소를 제거
- .shrink_to_fit() : capacity를 제거하는 함수
***
### 참조 함수
- .at(idx) : idx번째 원소를 참조, [] 참조보다 느리지만 범위 점검을 하므로 안전.
- [idx] : idx번째 원소를 참조
- front() : 첫 번째 원소 참조
- back() : 마지막 원소 참조
- begin() : 첫 번째 원소를 가르킵니다. iterator와 사용
- end() : 마지막의 '다음'을 가르킵니다. iterator와 사용
***
### 기타 함수
- size() : 원소의 갯수를 반환한다.
- empty() : 비어있으면 true 반환한다. (size 기준)
