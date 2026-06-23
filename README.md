# 📊 Data Analyst Portfolio

안녕하세요, 데이터 파이프라인 구축부터 모델링, 시각화까지 엔드투엔드(End-to-End) 데이터 솔루션을 설계하는 **이석하**입니다.  
데이터를 통해 복잡한 문제를 객관적으로 정의하고, 비즈니스 및 사용자 경험을 개선하는 분석을 지향합니다.

---

## 🚀 메인 프로젝트: AdCheck
> **소셜 미디어 허위·과장 광고 탐지 및 모니터링 AI 서비스 (졸업작품)**
> - **개발 기간:** 2026.03 ~ 2026.06
> - **주요 역할:** 멀티모달 데이터 파이프라인 설계, 데이터 정제, 다단계 분석 모델링(KoBERT & Rule-based Engine), AI 추론 서버 배포 및 UI 시각화 연동
> - **Repository:** [Backend & Analysis AI](https://github.com/Jun0913/AdCheck_analysis) | [Frontend UI](https://github.com/lxxsh/Adcheck_frontend/tree/feature/A)

### 1. 문제 정의 (Problem Statement)
- **배경:** 인스타그램, 유튜브 등 소셜 미디어 내 건강기능식품 및 화장품 중심의 허위·과장 광고 급증으로 인한 소비자 피해 증가
- **목적:** 식약처 가이드라인 및 실제 적발 데이터를 기반으로, 광고의 위험도를 객관적인 점수로 환산하여 소비자에게 판정 근거를 제공하는 서비스 기획

### 2. Tech Stack
- **Data & AI:** Python, Pandas, KoBERT, Scikit-learn, PyTorch, Google Vision OCR
- **Backend & MLOps:** FastAPI, Docker
- **Frontend:** HTML5, CSS3, JavaScript (추론 결과 대시보드 및 시각화 구현)

---

### 3. 핵심 수행 내용 (Key Accomplishments)

#### 🛠️ [Data Engineering] 데이터 파이프라인 및 멀티모달 전처리
- **자동화 스크립트 구현:** 원본 데이터(Raw Data) 수집 후 결측치 처리, 노이즈 제거, 데이터셋 병합을 수행하는 전처리 파이프라인(`merge_clean_sheets.py`) 구축
- **멀티모달 텍스트 추출 (OCR):** 이미지 기반 광고 대응을 위해 `Google Vision OCR`을 메인 엔진으로 채택하고, 예외 처리를 위한 Fallback 구조(`EasyOCR`/`PaddleOCR`)를 설계하여 텍스트 데이터 파싱 성공률 최적화
- **라벨링 체계 수립:** 식약처 적발 사례를 기준으로 데이터셋을 '금지(0)', '허용(1)' 및 '주의/의심' 체계로 다중 라벨링(Multi-labeling)하여 데이터 신뢰도 확보

#### 🧠 [Analytics & Modeling] 비용 효율적인 3단계 AI 아키텍처 설계
모든 문장을 무거운 모델에 연산하는 리소스 낭비를 방지하기 위해 **다단계 파이프라인**을 설계했습니다.
1. **0차 전단 필터 (Pre-filter):** 입력 데이터 중 광고/화장품/식품 등 타겟 도메인에 해당하는 텍스트만 1차 분류
2. **1차 규칙 기반 엔진 (Rule-based Engine):** 축적된 금지 키워드 사전을 기반으로 정규식 패턴 매칭을 통해 명확한 위반 문구 고속 필터링
3. **2차 문맥 분석 모델 (KoBERT Fine-tuning):** 단순 단어 매칭으로 잡기 어려운 은유적 표현 및 문맥적 과장을 탐지하기 위해 `KoBERT` 모델을 미세조정하여 딥러닝 추론 진행
4. **종합 의심도 판정 스코어링:** 각 단계의 가중치를 결합하여 `0.0 ~ 1.0` 사이의 연속형 위험도 점수를 산출하는 스코어링 알고리즘 수립

#### 💻 [Deployment & UI Visualization] 분석 결과의 가치 전달
- **추론 서버 경량화:** `FastAPI` 기반 추론 API를 구축하고, 학습 의존성(`requirements-train.txt`)과 실행 의존성(`requirements-runtime.txt`)을 분리하여 `Docker` 이미지 용량 및 배포 프로세스 최적화
- **사용자 중심 시각화 대시보드:** 소비자가 웹 UI상에서 분석 요청 시, 딥러닝 모델이 판단한 **위험도 점수, 핵심 의심 키워드, 매칭된 식약처 가이드라인 라벨**을 직관적인 통계 통계 그래프와 경고(Warning) 메시지로 시각화하여 정보 전달력 극대화

---

### 4. 성과 및 회고 (Results & Lessons Learned)
- **성과:** 비정형 데이터(텍스트, 이미지) 정제부터 AI 모델링, 추론 결과 시각화 웹 서비스까지 엔드투엔드(End-to-End) 데이터 산출물 구현 완료
- **회고:** 실제 가공되지 않은 소셜 미디어 Raw 데이터를 직접 다루며 데이터 핸들링과 전처리의 중요성을 깨달았으며, 규칙 기반 모델과 딥러닝 모델을 상호보완적으로 설계하여 실무적인 리소스 최적화 관점을 기를 수 있었습니다.
