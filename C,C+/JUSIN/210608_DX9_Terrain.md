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
***
### 타일 생성
- 사각형이 아닌 마름모 특성에 맞게 타일을 배치한다.
```
	for (int i = 0 ; i < TILEY ; ++i)
	{
		for (int j = 0 ;  j < TILEX ; ++j  )
		{
			fX = (j * TILECX) + ((i % 2) * (TILECX >> 1)); 
			fY = i * (TILECY >> 1);
			
			pTile = new TILE; 
			pTile->vPos = { fX, fY, 0.f }; 
			pTile->vSize = { 1.f, 1.f, 0.f }; 
			pTile->byDrawID = 17;
			pTile->byOption = 0; 
			
			m_vecTile.emplace_back(pTile); 
		}
	}
```
***
### 타일 그리기
- 벡터에 저장한 타일객체의 정보를 이용해 타일을 출력한다.
```
	D3DXMATRIX matScale, matTrans, matWorld; 
	DWORD dwSize = m_vecTile.size();
	
	for (size_t i = 0 ; i < dwSize; ++i)
	{
		const TEXINFO* pTexInfo = CTexture_Manager::Get_Instance()->Get_TexInfo_Manager(L"Terrain", L"Tile", m_vecTile[i]->byDrawID);
		if (nullptr == pTexInfo)
			return; 
		float fCenterX = float(pTexInfo->tImageInfo.Width >> 1); 
		float fCenterY = float(pTexInfo->tImageInfo.Height >> 1); 

		D3DXMatrixScaling(&matScale, m_vecTile[i]->vSize.x, m_vecTile[i]->vSize.y, 0.f); 
		D3DXMatrixTranslation(&matTrans, m_vecTile[i]->vPos.x, m_vecTile[i]->vPos.y, 0.f); 
		matWorld = matScale * matTrans; 
		CGraphic_Device::Get_Instance()->Get_Sprite()->SetTransform(&matWorld); 
		
		CGraphic_Device::Get_Instance()->Get_Sprite()->Draw(pTexInfo->pTexture, nullptr, &D3DXVECTOR3(fCenterX, fCenterY, 0.f), nullptr, D3DCOLOR_ARGB(255, 255, 255, 255)); 
	}
```
***
### 타일 삭제
- 동적 할당으로 생성한 타일 객체를 삭제해준다.
```
	for(TILE*& pTile : m_vecTile)
	{
	delete pTile;
	pTile = nullptr;
	}
	m_vecTile.clear();
	m_vecTile.shrink_to_fit();
```
