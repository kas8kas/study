# 가상 함수(함수 오버라이딩 virtaul)
```c++
class CObj
{
public:
	virtual void Obj_Render()
	{
		cout << "부모의 Render" << endl; 
	}
};

class CPlayer : public CObj 
{
public:
	 void Obj_Render()
	{
		cout << "override 자식의 Render" << endl; 
	}
	void Player_Render()
	{
		cout << "Player Render" << endl; 
	}
};

void main()
{

}
```
- 클래스 문법. 부모에 함수가 정의되어 있는 상태에서 그 부모의 함수 아예 똑같이 재정의 하는 문법. 
- 만약 부모의 객체 포인터에서 실제 객체를 기준으로 오버라이딩된 함수를 호출하고 싶다면!!! virtual 키워드를 추가.
- 가상함수는 동적바인딩으로 포인터 변수를 더 잡기 때문에 일반 함수보다 느리다.
***
### 가상 소멸자
```c++
class Base {
public:
	~Base() {
		cout << "Base destructor!" << endl;
	}
};

class Derived : public Base {
public:
	char* largeBuffer;
	Derived(): largeBuffer(new char[3000])
	{
	}

	~Derived() {
		cout << "Derived destructor!" << endl;
		delete[] largeBuffer;
	}
};

int main()
{
	Base* der2 = new Derived();
	delete der2;

    return 0;
}
```
- 가상 소멸자를 사용하는 이유는 객체 포인터 타입이 부모형식이며 실 객체의 타입이 자식인 경우
- 자식의 소멸자가 호출되지 않는 문제가 발생. 
- 부모에만 명시를 해도 무관하긴 하지만 가독성이 많이 떨어진다. -> 자식들도 해당 키워드를 붙혀주자.
***
### 순수 가상 함수
```c++
	virtual void Render() = 0;
```
- 자식클래스에서 반드시 재정의(오버라이딩)하게끔 유도하는 문법.
- 만약 순수 가상함수를 상속받고도 자식에서 정의하지 않는다면 ! 컴파일 에러를 유발한다.
- 만약 순수 가상함수를 하나라도 들고 있다라면 그 클래스는 더이상 객체화 할 수 없다.
- 그러한 클래스를 가르켜 추상클래스라 부른다. (추상클래스는 객체 포인터 형식으로는 사용할수 있지만 객체화 불가능.)
