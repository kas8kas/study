# const 멤버 변수
***
### const 멤버 변수 초기화(이니셜라이져)
```c++

class CConst
{
	CConst():m_iConst2(0),m_iConst3(99),m_iNotConst(10) //1번 방법
	{
		//m_iConst2 = 0; 불가능, 상수의 대입이기 때문에.
	}
private:
  const int m_iConst1 = 0;             //2번 방법
  const int m_iConst2;
  const int m_iConst3;
  int m_iNotConst;
};
```
- 생성자 이름 뒤 __쌍점__\으로 초기화 가능
- __쉼표__\로 초기화 변수 추가 가능
- 일반 멤버 변수도 초기화 가능
- 장점: 대입 초기화 보다 빠르다. 초기화 대상을 명확히 인지 할 수 있다.
- 2번 방법의 초기화는 사용하지 않는 것이 좋다. 초기화 위치가 헤더이니 헷갈림. 옛 버전에서는 불가한 형식이기도 함.
