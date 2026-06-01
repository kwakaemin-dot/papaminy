# 주식 MVP 프로토타입(시그널X) 한글화 및 봉차트 구현 계획

제공해주신 주식 분석 MVP 프로토타입의 UI 텍스트를 모두 한국어로 번역하고, 상세 분석 탭의 차트를 캔들스틱(봉차트)으로 변경합니다. 또한, 현재 로컬 PC에 Node.js 및 npm이 설치되어 있지 않은 환경을 감안하여, 더블클릭만으로 브라우저에서 즉시 실행하고 테스트해볼 수 있는 완성형 HTML 파일을 함께 제공하고자 합니다.

## User Review Required

> [!IMPORTANT]
> **로컬 실행 및 테스트 방식**
> - 현재 로컬 환경에 Node.js와 npm이 구성되어 있지 않은 것으로 확인되었습니다.
> - 따라서 바탕화면에 React, Recharts, Tailwind CSS 등의 CDN을 탑재한 **독립 실행형 HTML 파일([시그널X_테스트.html](file:///c:/Users/USER/Desktop/시그널X_테스트.html))**을 생성하여, 더블클릭만으로 언제든 브라우저에서 작동하는 앱을 테스트하실 수 있도록 지원합니다.
> - 이와 함께 원래 파일인 [주식프롬프트_analysis_mvp_prototype.jsx](file:///c:/Users/USER/Desktop/주식프롬프트_analysis_mvp_prototype.jsx) 코드도 지시하신 봉차트와 한글화가 완벽하게 적용된 형태로 업데이트합니다.

> [!TIP]
> **봉차트(Candlestick) 색상 기준**
> - 한국 주식 시장의 표준 직관에 맞추어 **상승(양봉)은 빨간색 계열(#F35F5F)**, **하락(음봉)은 파란색 계열(#4A90E2)**로 시각화하여 정보 전달력을 극대화합니다.

---

## Proposed Changes

### 주식 대시보드 컴포넌트

#### [MODIFY] [주식프롬프트_analysis_mvp_prototype.jsx](file:///c:/Users/USER/Desktop/주식프롬프트_analysis_mvp_prototype.jsx)
- **데이터 구조 개선**: `initialData`, `createRealtimePoint`, `selectStock` 함수를 수정하여 시가(open), 종가(close), 고가(high), 저가(low) 데이터를 생성하도록 변형합니다.
- **봉차트(Candlestick) 커스텀 셰이프 추가**: Recharts `<Bar>` 내에서 동작하는 커스텀 `Candlestick` 렌더링 컴포넌트를 구현합니다.
- **상세 분석 차트 변경**: 기존의 단순 종가 꺾은선그래프(Line)를 봉차트로 변경하고, 거래량(Bar)과 겹쳐서 입체적으로 볼 수 있도록 `ComposedChart`를 재구성합니다.
- **전면 한글화**:
  - 종목 이름 한글화 (Tesla → 테슬라, Apple → 애플, NVIDIA → 엔비디아)
  - 시장명 한글화 (NASDAQ → 나스닥, KOSPI → 코스피)
  - 뉴스 출처 및 UI 텍스트 전면 한글화 (예: ON/OFF → 켜짐/꺼짐, DART → 전자공시, T-11 → 11봉 전 등)

#### [NEW] [시그널X_테스트.html](file:///c:/Users/USER/Desktop/시그널X_테스트.html)
- 바탕화면에 신규 생성되는 단일 HTML 파일입니다.
- React, Tailwind CSS, Recharts, Framer Motion 등을 CDN으로 연동하여 브라우저에서 실행 가능한 형태로 제작합니다.
- 캔들스틱 및 한글화가 적용된 주식 앱이 실제 웹 브라우저에서 완벽히 작동하는지 실시간으로 테스트할 수 있습니다.

---

## Verification Plan

### 수동 검증
1. 바탕화면에 생성된 [시그널X_테스트.html](file:///c:/Users/USER/Desktop/시그널X_테스트.html) 파일을 더블클릭하여 브라우저에서 실행합니다.
2. 각 화면(대시보드, 상세 분석, 뉴스·공시)에 진입하여 UI 텍스트가 모두 올바르게 한글로 표기되는지 점검합니다.
3. **상세 분석** 탭에서 빨강/파랑 색상으로 캔들스틱(봉차트)이 거래량과 함께 잘려나감 없이 올바르게 출력되는지 확인합니다.
4. 종목을 변경하거나 자동 분석이 돌아갈 때 봉차트 및 거래량 데이터가 실시간으로 잘 업데이트되는지 검증합니다.
