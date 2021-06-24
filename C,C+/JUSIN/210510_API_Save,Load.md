# SAVE FILE
```
void CLine_Manager::SaveData_Line_Manager()
{
	HANDLE hFile = CreateFile(L"../Data/LineData.dat", GENERIC_WRITE, 0, 0, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL, nullptr);

  //실패
	if (INVALID_HANDLE_VALUE == hFile)
	{
		MessageBox(nullptr, L"실패!", L"systemError", MB_OK);
		return; 
	}
  
  //성공
	DWORD dwByte = 0; 
	for (auto& pLine : m_listLine)
		WriteFile(hFile, pLine->Get_LineInfo(), sizeof(LINEINFO), &dwByte, nullptr);

	CloseHandle(hFile); 
	MessageBox(nullptr, L"저장완료!", L"오예!", MB_OK); 
}
```
- CreateFile() 함수로 파일을 생성합니다. (GENERIC_WRITE -> 쓰기 권한 부여 후, CREATE_ALWAYS -> 중복 시 덮어씌우기)
- int MessageBox(HWND hWnd, LPCTSTR lpText, LPCTSTR lpCaption, UINT uType);
- MessageBox(핸들값,출력메세지,출력타이틀,박스옵션) -> 박스옵션으로 여러 버튼을 호출할 수 있음. 그리고 버튼에 따른 리턴값을 가지고 있음.
### WriteFile 함수
```
BOOL WriteFile(
    HANDLE hFile,
    LPVOID lpBuffer,
    DWORD nNumberOfBytesToWrite,
    LPDWORD lpNumberOfBytesWritten,
    LPOVERLAPPED lpOverlapped);
    
hFile
파일이나 I/O 장치의 핸들입니다.
반드시 쓰기 권한이 있어야 합니다.
비동기식 쓰기 작업을 하려면 CreateFile 함수를 사용해서 FILE_FLAG_OVERLAPPED 플래그를 지정하거나 socket 함수나 accept 함수를 사용해서 받아온 핸들이어야 합니다.

lpBuffer
파일이나 장치에 기록할 데이터를 가지고 있는 버퍼의 포인터입니다.

nNumberOfBytesToWrite
기록할 데이터의 길이입니다.

lpNumberOfBytesWritten
기록한 데이터 바이트의 수를 리턴받는 인수입니다.
이 인수는 함수가 호출되었을 때 0으로 초기화됩니다.
lpOverlapped 인수가 NULL 값을 가지지 않으면 이 인수를 NULL로 지정해야 합니다.

lpOverlapped
비동기 입출력을 위한 OVERLAPPED 구조체의 포인터입니다.
만약 파일을 FILE_FLAG_OVERLAPPED 플래그를 지정해 열었다면 OVERLAPPED 구조체를 반드시 지정해야 합니다.
비동기 입출력을 사용하지 않을 경우에는 NULL 값으로 지정해야 합니다.
```
***
# LOAD FILE
```
void CLine_Manager::LoadData_Line_Manager()
{
//파일 개방 성공 여부
	HANDLE hFile = CreateFile(L"../Data/LineData.dat", GENERIC_READ, 0, 0, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, nullptr); 
	if (INVALID_HANDLE_VALUE == hFile)
	{
		MessageBox(nullptr, L"개방실패...", L"ㅠㅠ", MB_OK); 
		return; 
	}
  
  //이전 데이터 삭제
	for (auto& pLine : m_listLine)
		Safe_Delete(pLine); 
	m_listLine.clear(); 
  
	//불러오기 코드. 
	DWORD dwByte = 0; 
	LINEINFO tLineInfo = {}; 
	CLine* pLine = nullptr; 
	while (true)
	{
		ReadFile(hFile, &tLineInfo, sizeof(LINEINFO), &dwByte, nullptr); 
		if (0 == dwByte)
			break; 
		
		pLine = CLine::Create(&tLineInfo); 
		m_listLine.emplace_back(pLine);
	}
	CloseHandle(hFile); 
	MessageBox(nullptr, L"에베베", L"이거 시연회에서 보이면 때릴꺼임", MB_OK);
}
```
