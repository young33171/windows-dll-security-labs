# Windows DLL Injection & Process Analysis Labs

Windows 10 VM에서 진행한 시스템보안 실습을 **관찰 결과와 검증 한계까지 구분**해 기록한 기술 포트폴리오입니다.

## 실습 현황

| 주제 | 확인된 결과 |
|---|---|
| CreateRemoteThread / LoadLibrary | Visual Studio 빌드 및 로컬 LoadLibrary 성공 메시지 확인. 원격 프로세스 인젝션 성공은 미확인 |
| AppInit_DLLs / LoadAppInit_DLLs | 재부팅 후 Process Explorer에서 SearchProtocolHost.exe의 myhack2.dll 로딩 확인 |
| Process Explorer | myhack2.dll 검색 결과 1건, 대상 프로세스 DLL 목록 내 모듈 확인 |
| FreeLibrary / DLL Ejection | 원리와 과제 요구사항 정리. DLL 해제 성공 캡처 미확보 |

## 환경 및 기술
**Windows 10 VM · C++ · Visual Studio · Win32 API · Windows Registry · Sysinternals Process Explorer · x86 Debug · Unicode**

## 세부 문서
- [01. CreateRemoteThread와 LoadLibrary](docs/01-create-remote-thread.md)
- [02. AppInit DLL 로딩 메커니즘](docs/02-appinit-dlls.md)
- [03. Process Explorer 관찰 및 증거](docs/03-process-explorer.md)
- [04. FreeLibrary와 DLL 해제](docs/04-free-library.md)
- [05. 오류 분석과 해결 기록](docs/05-troubleshooting.md)
- [06. 포트폴리오용 경험 정리](docs/06-portfolio-summary.md)

## 실습에서 얻은 핵심 교훈
1. **빌드 성공 ≠ 원격 주입 성공.** 독립 프로세스의 실제 모듈 목록으로 확인해야 합니다.
2. **로딩 확인 ≠ DLL 기능 실행 확인.** 행위 증거는 별도로 필요합니다.
3. **프로세스 1개에서 확인 ≠ 모든 프로세스에서 확인.** 관찰 범위를 그대로 기술합니다.
4. Win32 API 호출에 쓰이는 문자열 버퍼와 포인터 연산은 런타임 무결성에 직접 영향을 미칩니다.

> 공개 저장소에는 은닉 실행 DLL의 소스, 실행 파일, 시스템 전체 DLL 주입 자동화 코드를 포함하지 않았습니다. 별도 실습 증거 캡처는 개인정보와 내부 경로를 마스킹한 원본만 추가합니다.
