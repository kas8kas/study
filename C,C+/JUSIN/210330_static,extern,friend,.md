# static 정적 변수
```c++
 void Test()
 {
  static int a;
  a++;
 }
 
 void main()
 {
  Test();
  Test();
  Test(); //a == 3
 }
```
- 자동으로 0 초기화가 진행된다. 
- 데이터 영역에 할당. 전역변수와 비슷하지만 접근에 지역적인 제한이 있다.
- 전역변수: 해당 프로그램(실행파일 기준)의 어느 함수, 어느 파일에서도 접근이 가능.
- 정적변수: 변수가 선언된 파일이나 함수내에서만 접근이 가능.
***
### static 멤버 변수 초기화
```c++
 class CMyStatic
 {
 public:
 	static void Render();
 public:
 	static int m_iStatic;
  };
  
  int CMyStatic::m_iStatic = 0;
```
- static 멤버 변수 초기화는 클래스 외부에서 한다.
- static 멤버 변수는 클래스당 하나씩만 생성된다. 따라서 같은 종류의 클래스가 계속 만들어져도 최초에 만을어진 static 멤버 변수를 공유한다.
***
### static 멤버 변수 접근
```c++
 void main()
 {
  cout << CMyStatic::m_iStatic << endl;
  CMyStatic st1;
  cout << st1.m_iStatic << endl;
  CMyStatic st2;
  cout << st2.m_iStatic << endl;
 }
```
- 객체를 생성하지 않고 클래스 이름만으로 호출할 수 있습니다.
- 객체를 생성하지 않으므로, this 포인터를 가지지 않습니다.
- 특정 객체와 결합하지 않으므로, 정적 멤버 변수밖에 사용할 수 없습니다. (static 멤버함수 내에서는 static 멤서변수와 static 멤버함수의 호출만 가능하다.)
***
### extern 키워드
```c++
extern int num1;    // 다른 소스 파일(외부)에 있는 전역 변수 num1을 사용

int main()
{
  cout << num1 << endl;
}
```
- 다른 파일의 전역변수를 사용할 때 사용된다.
- extern 함수도 가능하다. 단 같은 함수명은 사용 불가.
- 헤더 파일에 extern 키워드로 static을 선언하면 파일이 다른 곳에서도 공용으로 사용될 수 있다.
***
### friend 키워드
```c++
class CHuman
{
	friend CBoss;
 int m_iMoney = 1000;
};

class CBoss
{
 int m_iMoney = 1000;
 void GetMoney(CBoss& boss)
 {
  this->m_iMoney += boss.m_iMoney;
  m_iMoney = 0;
 }
};
```
- c++에서 지원하는 기능이다.
- 접근 지정자를 무시하게 만들 수 있다. 무분별한 사용을 지양해야 하는 무서운 키워드... 객체 지향 정보 은닉성을 위배...
- a가 b를 friend로 지정하면, b에서 a를 마음대로 접근할 수 있다.
