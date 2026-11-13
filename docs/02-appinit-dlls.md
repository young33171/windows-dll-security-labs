# 02 · AppInit_DLLs DLL 로딩 메커니즘 분석

## 학습 목적
Windows의 레거시 AppInit DLL 로딩 기능과 `user32.dll` 의존 프로세스의 관계를 이해하고, 실제 모듈 로딩 여부를 분석합니다.

## 환경 및 실습 파일
- Windows 10 가상머신
- Visual Studio C++ `myhack2` DLL 프로젝트
- **x86 / Debug / Unicode**
- `myhack2.dll`

## 진행 및 관찰
1. `myhack2.dll` 프로젝트를 빌드했습니다.
2. Windows 레지스트리의 관련 설정 항목을 확인했습니다.
3. VM을 재부팅한 뒤 Process Explorer를 실행했습니다.
4. **Find → Find Handle or DLL**에서 `myhack2.dll`을 검색했습니다.
5. 검색 결과에 **1 matching item**이 나타났습니다.
6. `SearchProtocolHost.exe` 프로세스의 DLL 목록에서도 `myhack2.dll` 로딩을 확인했습니다.

## 증거의 의미
- **확인한 사실**: `SearchProtocolHost.exe`의 주소 공간에 `myhack2.dll`이 로딩됨
- **확인하지 못한 사실**: `user32.dll`을 사용하는 *모든* 프로세스에 같은 DLL이 로딩됨
- **별도 검증 필요**: DLL이 포함한 기능이 실제 수행되었는지

AppInit DLL 로딩은 Windows 버전, 부팅 및 코드 서명 정책, 프로세스 아키텍처의 영향을 받을 수 있어 단일 검색 결과를 전체 시스템에 일반화하지 않습니다.

## 방어적 분석 포인트
설정값 자체뿐 아니라 실제 프로세스/모듈 조합, 파일 서명, 파일 해시, 생성·로딩 시점을 함께 확인해야 합니다.

> 이 공개 기록은 모듈 관찰과 학습 결과를 다룹니다. 임의 DLL의 시스템 전역 자동 주입 또는 은닉 실행을 위한 구체적인 활성화 절차와 코드는 포함하지 않습니다.
