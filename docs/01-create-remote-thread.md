# 01 · CreateRemoteThread / LoadLibrary DLL 실습

## 과제 목적
Windows 프로세스의 주소 공간과 DLL 동적 로딩을 이해하고, CreateRemoteThread와 LoadLibrary를 이용하는 원격 모듈 로딩 기법을 분석합니다.

## 사용한 항목
- **개발**: Visual Studio C++, Win32 API
- **실습 파일**: `InjectDll.cpp`, `myhack.cpp`, `InjectDll.exe`, `myhack.dll`
- **관찰 대상**: `notepad.exe`
- **검증 도구**: Process Explorer, DLLTest(로컬 로딩 테스트)

## 실제 진행 기록
1. Visual Studio에서 DLL 및 인젝터 프로젝트를 구성하고 빌드했습니다.
2. 대상 프로세스가 실행된 상태에서 Process Explorer로 DLL 로딩 여부를 조사했습니다.
3. 별도 `DLLTest` 앱에서 `LoadLibrary`로 DLL을 로컬 로딩했습니다.
4. 콘솔의 **`DLL Load Success!`** 메시지를 확인했습니다.
5. 언로드 단계에서 `Run-Time Check Failure #2 - Stack around the variable 'szPath' was corrupted` 오류가 발생했습니다.

## 관찰과 해석
- `DLL Load Success!`는 **테스트 프로그램 안에서** DLL이 로딩됐다는 증거입니다.
- 대상 `notepad.exe`에서 원격 로딩 성공 여부는 당시 자료로 **확정할 수 없습니다**.
- 언로드 시점의 스택 검사 실패는 DLL 내 문자열/버퍼 처리 문제를 강하게 시사합니다. 오류 발생 위치가 DLL 해제 호출 근처라는 이유만으로 FreeLibrary 자체의 결함이라고 단정하지 않습니다.

## 관련 API 학습
| API | 역할 |
|---|---|
| LoadLibrary | 호출한 프로세스에 DLL을 동적으로 로딩 |
| CreateRemoteThread | 별도의 프로세스 주소 공간에서 스레드 생성 |
| GetModuleFileName | 모듈/실행 파일의 경로 조회 |
| DllMain | 프로세스 부착·분리 등에 호출되는 DLL 진입점 |

## 개선해야 할 부분
- 버퍼 길이/널 종료 검증
- 포인터 연산 경계 검사
- 프로세스 아키텍처(x86/x64) 호환성 확인
- 대상 프로세스 DLL 목록과 동작 로그를 분리 기록

**검증 상태: 빌드·로컬 로딩 메시지 확인 / 원격 인젝션 및 정상 언로드 미확인.**
