# 03 · Process Explorer로 DLL 로딩 확인

## 도구
Sysinternals **Process Explorer (procexp.exe)**

## 분석 화면 사용법
- `Ctrl + F`: Handle or DLL 문자열 검색
- `Ctrl + D`: 하단 창에 선택한 프로세스의 DLL 모듈 목록 표시
- `Ctrl + L`: 하단 창 표시/숨김

## 실습에서 확보한 관찰
검색어: **`myhack2.dll`**  
검색 결과: **1 matching item**  
프로세스: **`SearchProtocolHost.exe`**  
DLL: **`myhack2.dll`**

검색 결과와 하단 DLL 목록에 동일한 DLL이 표시되었습니다. 화면에는 프로세스의 PID와 디스크 DLL 경로도 표시되었습니다. PID는 프로세스 재시작에 따라 바뀔 수 있으므로 고정 식별자로 사용하지 않습니다.

## 증거 수준
| 주장 | 판정 |
|---|---|
| myhack2.dll 파일이 검색 결과에 나타남 | 확인 |
| SearchProtocolHost.exe에 myhack2.dll이 로딩됨 | 확인 |
| 모든 user32.dll 사용 프로세스에 로딩됨 | 미확인 |
| DLL 내부 기능이 정상 실행됨 | 미확인 |

## 포트폴리오 캡처 기준
- Process Explorer의 프로세스 이름, DLL 이름, 검색 결과 수가 함께 보이도록 캡처
- 원본 캡처 보존, 계정명/컴퓨터 이름/내부 경로 등은 공개용 복사본에서 마스킹
- 관찰하지 않은 항목에 '성공' 표시 금지

추가 캡처를 확보하면 `evidence/` 폴더에 파일을 넣고 이 문서에서 연결합니다.
