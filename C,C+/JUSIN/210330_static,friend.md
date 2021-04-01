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
- 데이터 영역에 할당. 전역변수, 하지만 접근에 지역적인 제한이 있다.
- 전역 변수는 해당 cpp를 벗어나면 사용 불가. (헤더에 extern 키워드로 해당 전역 변수를 추가하면 사용 가능)
- static은 프로그램 내부에서 사용 가능.
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
- static 멤버함수 내에서는 static 멤서변수와 static 멤버함수의 호출만 가능하다.
