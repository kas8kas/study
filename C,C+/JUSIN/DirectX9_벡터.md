# 벡터
### 정의와 특징
- '크기'와 '방향'을 가지는 물리량을 의미한다.
- 위치는 벡터의 속성이 아님, 위치가 달라도 같은 크기와 방향을 갖는다면 동일한 벡터로 취급한다.
***
### 자료형 D3DXVECTOR3
- 구조체이다.
- D3DVECTOR 구조체를 상속 받는다. (float x, y, z)
- 연산자 오버로딩이 세팅되어 있다.
***
### 단위 벡터
- 크기 1을 가지는 벡터를 뜻한다.
- 특정 벡터를 정규화하여, 단위 벡터로 만들어 사용 가능
```
  float 목적지x
  float 목적지y

  float 도착지x
  float 도착지y

  float 방향x = 목적지x - 도착지x;
  float 방향y = 목적지y - 도착지y;
  float 벡터 = sqrtf(방향x * 방향x + 방향y * 방향y)
  
  //정규화
  방향x /= 벡터;
  방향y /= 벡터;
```
***
### 단위 벡터 함수 D3DXVec3Normalize(pOut, pV)
- 3D 벡터의 정규화한 벡터를 돌려준다.
- pOut 인자: 결과값을 넣어줄 벡터구조체
- pV 인자: 연산을 진행할 벡터구조체
```
	D3DXVec3Normalize(&m_tInfo.vDir, &m_tInfo.vDir);
```
***
### 벡터의 내적
- 벡터의 곱셈
- 두 벡터가 사이의 각도를 구하는 공식 |a| * |b| * COS@ = a1* b1 + a2 * b2
- 벡터의 내적 결과는 스칼라값이 나온다.
- 하나의 벡터(A)를 또다른 벡터 위에 투영시킨 길이와 또다른 벡터(B)의 길이의 곱셈과 같다. 라고 정의할 수 있다.
```
//단위 벡터화
	float fV = sqrt(vec1.x * vec1.x + vec1.y * vec1.y + vec1.z + vec1.z)
	vec1.x /= fV;
	vec1.y /= fV;
	vec1.z /= fV;
	
	fV = sqrt(vec2.x * vec2.x + vec2.y * vec2.y + vec2.z + vec2.z)
	vec2.x /= fV;
	vec2.y /= fV;
	vec2.z /= fV;
	
	//또는
	//D3DXVec3Normalize(&vec1, &vec1);
	//D3DXVec3Normalize(&vec2, &vec2);
	//float fCos = D3DXVec3Dot(&vec1, &vec2);
//공식 대입
	float fCos = vec1.x * vec2.x + ve1.y * vec2.y; //A, B는 단위 벡터화로 1로 만들었으니 제외	
	float fAngle = acosf(fCos); //0~파이 반환(라디안)
//아크코사인 반대값 처리
	if(vec1.y >= vec2.y)
	fAngle *= -1.f;
//앵글값으로(라디안) 움직이기
	vec1.x += cosf(fAngle) * m_fSpeed;
	vec1.y += sinf(fAngle) * m_fSpeed;
//라디안->각도, D3DXToRadian(fAngle), fAngle * 파이 / 180
```
***
### 회전횡렬 공식
- 회전된 q위칙 주소 공식
- qX = pX * cos@ - pY * sin@
- qY = pX * sin@ + pY * cos@
