# 06 · 취업 포트폴리오용 프로젝트 요약

## 프로젝트 이름
**Windows DLL Injection 메커니즘 및 프로세스 모듈 로딩 분석**

## 한 줄 소개
Visual Studio C++ 및 Windows Win32 API 기반 DLL 실습을 수행하고 Sysinternals Process Explorer를 이용하여 실제 프로세스의 모듈 로딩 상태를 검증한 시스템보안 실습 프로젝트.

## 개인 수행 내용
- Windows 10 VM 환경에서 C++ DLL 프로젝트 구성 및 x86 Debug 빌드
- `CreateRemoteThread`, `LoadLibrary`, `FreeLibrary`, `DllMain` 호출 구조 학습
- `AppInit_DLLs` 메커니즘의 동작 및 보안적 위험 이해
- Process Explorer로 프로세스 목록, DLL 검색, 모듈 목록 분석
- `DLL Load Success!` 메시지와 DLL 언로드 시 발생한 스택 손상 런타임 오류 분석
- 실제 확인한 성공 범위와 미검증 범위 구분

## 실제 성과
**확인됨**
1. DLL 빌드 및 로컬 LoadLibrary 성공 메시지.
2. Process Explorer에서 `myhack2.dll` 검색 결과 1건 확인.
3. `SearchProtocolHost.exe`의 모듈 목록에서 `myhack2.dll` 로딩 확인.

**추가 검증 필요**
1. `CreateRemoteThread` 방식으로 `notepad.exe`에 원격 DLL 로딩.
2. `FreeLibrary` 기반 정상적인 DLL 해제.
3. `user32.dll` 의존 전체 프로세스에 대한 로딩 범위.

## 이력서용 기술
**C++/Win32 API 기반 Windows DLL 로딩 구조를 실습하고, Sysinternals Process Explorer를 활용해 실제 프로세스에서 DLL 로딩을 확인했습니다. 또한 로컬 DLL 테스트 과정에서 발생한 스택 메모리 손상 오류를 분석하고, 빌드·로딩·실행 검증을 분리하는 절차를 문서화했습니다.**

> 실행 성공 여부를 과장하지 않고 실제 확인한 증거 중심으로 작성했습니다.
