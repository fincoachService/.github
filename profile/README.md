# FinCoach

**AI 기반 종합 금융 코칭 애플리케이션**

## 🎯 프로젝트 소개

FinCoach는 사용자의 금융 생활을 종합적으로 관리하고 분석하는 React Native 기반 모바일 애플리케이션입니다. 계좌 관리, 카드 관리, 지출 분석, 대출 추천 등 다양한 금융 서비스를 하나의 플랫폼에서 제공합니다.

### ✨ 핵심 가치

- **포괄적인 금융 관리**: 계좌, 카드, 지출을 한 곳에서 통합 관리
- **스마트 분석**: AI 기반 지출 패턴 분석 및 맞춤형 금융 조언
- **강력한 보안**: 생체인증, PIN, 패턴 등 다단계 인증 시스템
- **실시간 연동**: 실제 은행 계좌와의 안전한 연동

## 🚀 주요 기능

### 금융 관리
- **대시보드**: 지출 내역을 시각화한 인터랙티브 차트
- **계좌 관리**: 여러 은행 계좌 통합 관리 및 상세 내역 조회
- **카드 관리**: 신용/체크카드 사용 내역 추적 및 분석
- **지출 분석**: 카테고리별 소비 패턴 분석 및 리포트

### 인증 시스템
- **생체 인증**: Face ID / Touch ID 지원
- **PIN 인증**: 6자리 숫자 PIN 코드
- **패턴 인증**: 3x3 그리드 패턴 락
- **보안 저장소**: iOS Keychain 기반 안전한 데이터 보관

### 은행 연동
- **1원 인증**: 계좌 소유권 확인을 위한 1원 송금 인증
- **인증서 연동**: 은행 인증서 기반 계좌 연결
- **딥링크 통합**: TossNotifier 앱과 연동한 원활한 인증 프로세스

### 분석 및 리포트
- **가디언 리포트**: 월별 금융 건강도 분석
- **대출 추천**: 신용점수 기반 맞춤형 대출 상품 추천
- **연체 위험 분석**: 실시간 연체 위험도 평가 및 알림

## 🛠 기술 스택

### Core
- **React Native** 0.80.1 - 크로스 플랫폼 모바일 개발
- **React** 19.1.0 - UI 라이브러리
- **TypeScript** 5.0.4 - 타입 안정성

### 상태 관리 & 네비게이션
- **Jotai** 2.14.0 - 원자적 상태 관리
- **React Navigation** v7 - 네이티브 스택 네비게이션

### UI & 스타일링
- **styled-components** 6.1.19 - CSS-in-JS 스타일링
- **react-native-gifted-charts** 1.4.64 - 인터랙티브 차트
- **react-native-vector-icons** 10.3.0 - 아이콘 라이브러리

### 보안 & 인증
- **react-native-biometrics** 3.0.1 - 생체 인증
- **react-native-keychain** 10.0.0 - 보안 저장소
- **crypto-js** 4.2.0 - 암호화 (PIN/패턴 해싱)

### 네트워킹 & 데이터
- **Axios** 1.12.2 - HTTP 클라이언트
- **@react-native-async-storage/async-storage** 2.2.0 - 로컬 저장소

### 알림 & 유틸리티
- **@notifee/react-native** 9.1.8 - 로컬 푸시 알림
- **@react-native-community/datetimepicker** 8.4.5 - 날짜/시간 선택기

## 🏁 시작하기

### 필요 조건

- Node.js >= 18
- npm 또는 yarn
- Xcode (iOS 개발)
- Android Studio (Android 개발)
- CocoaPods (iOS 의존성 관리)

### 설치

```bash
# 저장소 클론
git clone https://github.com/yourusername/fincoach.git
cd fincoach

# 의존성 설치
npm install

# iOS 의존성 설치
cd ios
pod install
cd ..
```

### 실행

```bash
# Metro 번들러 시작 (필수)
npm start

# 별도 터미널에서 플랫폼별 실행
npm run android  # Android
npm run ios      # iOS
```

### 개발 명령어

```bash
npm run lint     # ESLint 실행
npm test        # Jest 테스트 실행
```

## 🏗 아키텍처

### 네비게이션 구조

FinCoach는 **계층적 5-스택 네비게이션 시스템**을 사용합니다:

```
RootNavigator
├── Splash (스플래시 화면)
├── Auth (인증 스택)
│   ├── Login / SignUp
│   ├── FindId / FindPassword
│   ├── OneWonVerification (1원 인증)
│   └── CertificateSetup (인증서 설정)
├── Onboarding (온보딩 스택)
│   ├── PreInfo (사전 정보 입력)
│   ├── ImportSources (정보 가져오기)
│   └── AnalysisResult (분석 결과)
├── EasyLogin (간편 로그인)
│   └── Biometric / Pattern / PIN 인증
└── Main (메인 스택)
    ├── Home (대시보드)
    ├── Accounts / Cards (목록 화면)
    ├── AccountDetail / CardDetail (상세 화면)
    ├── GuardianReport (가디언 리포트)
    ├── LoanRecommend (대출 추천)
    └── Settings / Menu
```

### 애플리케이션 플로우

1. **Splash** → **Auth** (로그인/회원가입)
2. **Auth** → **Onboarding** (인증/분석)
3. **Onboarding** → **Main** (앱 기능 사용)
4. **EasyLogin**: 재방문 사용자를 위한 빠른 인증 경로

### 상태 관리

- **Jotai atoms**를 활용한 원자적 상태 관리
- 도메인별로 구조화된 상태 atoms (`src/state/*/atoms.ts`)
- 주요 전역 상태:
  - `isSignedInAtom`: 사용자 인증 상태
  - `certCompletedAtom`: 인증 완료 상태

### 보안 아키텍처

#### 서비스 레이어 (`src/services/auth/`)

- `biometricService.ts`: Face ID/Touch ID 인증 및 키 생성
- `pinService.ts`: 6자리 PIN 인증 (SHA-256 해싱, 잠금 시스템)
- `patternService.ts`: 3x3 패턴 인증 (최소 4포인트)
- `easyLoginService.ts`: 통합 간편 로그인 관리
- `secureStorage.ts`: iOS Keychain 래퍼
- `oneWonService.ts`: 1원 인증 뱅킹 연동
- `certificateService.ts`: 은행 인증서 관리

#### 보안 기능

- iOS Keychain을 통한 모든 인증 데이터 보호
- crypto-js SHA-256 + salt 기반 PIN/패턴 해싱
- 5회 실패 시 30분 잠금 (실시간 카운트다운)
- Face ID 사용 목적: "간편하고 안전한 로그인" (Info.plist 설정)
- 실패 시 자동 복구 및 전통적 로그인으로 폴백

## 📁 프로젝트 구조

```
fincoach/
├── src/
│   ├── assets/              # 이미지 및 정적 리소스
│   ├── components/          # 재사용 가능한 컴포넌트
│   │   ├── easyLogin/      # 인증 UI 컴포넌트
│   │   └── modals/         # 모달 다이얼로그
│   ├── navigation/          # 네비게이션 설정
│   │   ├── stacks/         # 스택 네비게이터
│   │   └── types.ts        # 네비게이션 타입 정의
│   ├── screens/            # 화면 컴포넌트
│   │   ├── auth/          # 인증 화면
│   │   ├── easyLogin/     # 간편 로그인 화면
│   │   ├── main/          # 메인 앱 화면
│   │   └── onboarding/    # 온보딩 화면
│   ├── services/           # 비즈니스 로직 서비스
│   │   └── auth/          # 인증 서비스
│   ├── state/             # 전역 상태 관리
│   │   └── auth/          # 인증 상태 atoms
│   ├── styles/            # 테마 및 스타일
│   │   ├── theme.ts       # 중앙 테마 설정
│   │   └── styled.d.ts    # TypeScript 타입 정의
│   └── utils/             # 유틸리티 함수
│       ├── api.ts         # API 엔드포인트
│       ├── axios.ts       # HTTP 클라이언트 설정
│       ├── notifications.ts # 푸시 알림 처리
│       └── secureStorage.ts # 보안 저장소
├── ios/                   # iOS 네이티브 코드
├── android/               # Android 네이티브 코드
└── App.tsx               # 앱 진입점
```

## 💻 개발 가이드

### 코드 스타일

프로젝트는 다음 설정을 따릅니다:

- **ESLint**: `@react-native` 구성 확장
- **Prettier**: 커스텀 규칙
  - `arrowParens: 'avoid'`
  - `singleQuote: true`
  - `trailingComma: 'all'`
- **TypeScript**: `@react-native/typescript-config` 기반

### 테마 시스템

중앙화된 테마 (`src/styles/theme.ts`):

- **Primary Color**: 민트 그린 (#a6e1d8)
- **Spacing Scale**: xs(4px) ~ xxl(24px)
- **Typography**: Font weight 400 ~ 700
- **Shadow System**: 다단계 elevation
- **Chart Colors**: 데이터 시각화 전용 팔레트

### API 통합

- **Axios 클라이언트**: `src/utils/axios.ts`에서 구성
- **API 엔드포인트**: `src/utils/api.ts`에 중앙화
- **인터셉터**: 요청/응답 처리 및 토큰 관리
- **TypeScript 인터페이스**: 모든 엔드포인트에 대한 타입 안정성

### 차트 구현 패턴

```typescript
// 인터랙티브 차트 상태 관리
const [selectedIdx, setSelectedIdx] = useState<number | null>(null);

// 반응형 크기 조절
const onLayout = (event: LayoutChangeEvent) => {
  setChartSize(event.nativeEvent.layout.width);
};

// 커스텀 센터 라벨 컴포넌트
const centerLabel = useMemo(() => {
  return selectedIdx !== null ? 
    <CategoryDetail /> : <TotalAmount />;
}, [selectedIdx]);
```

### 로딩 모달 패턴

```typescript
// 다중 API 호출 조정
const [isLiveAdviceReady, setLiveAdviceReady] = useState(false);
const [isMonthDataReady, setMonthDataReady] = useState(false);

// 모든 비동기 작업 완료 확인
const isLoadingComplete = isLiveAdviceReady && isMonthDataReady;

// 에러 처리 시에도 로딩 상태 완료
catch (error) {
  setLiveAdviceReady(true);
  setMonthDataReady(true);
}
```

## 🔒 보안

### 데이터 보호

- **iOS Keychain**: 모든 민감한 데이터는 디바이스 패스코드로 보호되는 iOS Keychain에 저장
- **암호화**: crypto-js를 사용한 SHA-256 해싱 (Salt 포함)
- **세션 관리**: 안전한 토큰 기반 인증

### 인증 보안

- **잠금 메커니즘**: 5회 실패 후 30분 잠금
- **생체 인증**: 디바이스 기능 감지 및 안전한 키 생성
- **자동 복구**: 간편 로그인 실패 시 전통적 로그인으로 폴백

### 네트워크 보안

- **HTTPS**: 모든 API 통신 암호화
- **토큰 관리**: Axios 인터셉터를 통한 자동 토큰 갱신
- **에러 처리**: 보안 관련 에러의 적절한 처리

