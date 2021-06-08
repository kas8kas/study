# 마름모 타일 설치
***
### 타일 객체
- 위치 정보
- 사이즈
- 이미지 정보
- 기타 옵션 정보(통행 가능, 불가능 등등)
- BYTE 자료형: unsigned char -> 가장 작은 자료형으로 사용
```
typedef struct tagTile
{
	D3DXVECTOR3 vPos; 
	D3DXVECTOR3 vSize; 
	BYTE byDrawID; 
	BYTE byOption; 
}TILE;
```
