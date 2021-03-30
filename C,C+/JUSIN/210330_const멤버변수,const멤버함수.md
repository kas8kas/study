# const 멤버 변수
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
- 생성자 이름 뒤 쌍점으로 초기화 가능
- 쉼표로 초기화 변수 추가 가능
- 일반 멤버 변수도 초기화 가능
- 장점: 대입 초기화 보다 빠르다. 초기화 대상을 명확히 인지 할 수 있다.
- 2번 방법은 지양. 초기화 위치가 헤더 파일이면 헷갈림. 옛 버전에서는 불가한 형식이기도 함.
***
# const 멤버 함수
***
### 함수 오버로딩
```c++

class CConst1
{
public:
	void Render()
	{
		cout << m_iA << endl;
	}
	void Render() const // const 키워드로 함수 오버로딩 가능, 근데 헷갈림. 쓰지 말자 딱히
	{
		cout << "ㅇㅇ" << endl;
	}
private:
	int m_iA = 9;
public:
	int m_iP = 0;
};

void ShowConst(const CConst1& rConst1)
{
	rConst1.Render();
	//tConst1.m_iP = 99; //래퍼런스 닉네임 rConst1은 const로 하겠다. 변경 불가. 하지만 main함수에서는 const 안 붙힌 tConst1에서는 가능
}

int main()
{
	CConst1 tConst1;
	tConst1.Render();

	const CConst1 tConst2; //const 함수 오버로딩
	tConst2.Render();

	ShowConst(tConst1); //const 함수 오버로딩
	tConst1.m_iP = 99; //가능. showconst함수 내부에서 파라미터로 받은 래퍼런스 닉네임에서는 불가능
	return 0;
}
```
