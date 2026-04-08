# Claude Report Skills — ESG Report Generator

세계 최고 수준의 ESG 전문가가 국내(15개) + 해외(25개) 프레임워크를 통합하여 이중언어(한/영) ESG 보고서를 자동 생성하는 Claude Code 스킬 프로젝트입니다.

---

## 주요 기능

- **40개 프레임워크 통합**: GRI, ISSB, TCFD, SASB, K-ESG, KSSB, KRX, SBTi, CDP, RE100, TNFD, SDGs 등 국내외 ESG 프레임워크 교차 매핑
- **이중언어 지원**: 한국어/영어 실시간 토글 (KR/EN 버튼)
- **인터랙티브 에디터**: 섹션 추가/삭제/순서 변경 UI
- **PDF 다운로드**: 브라우저 인쇄 기능을 활용한 PDF 출력 (커버 페이지 + 섹션별 페이지 분리)
- **Markdown + HTML 동시 출력**: `.md` 보고서와 `.html` 인터랙티브 보고서 동시 생성
- **프레임워크 색인**: GRI Content Index, ISSB Index, TCFD Index, K-ESG Index 등 부록 자동 생성

---

## 사용 방법

### 1. 슬래시 커맨드 실행

Claude Code에서 아래 명령어를 입력합니다:

```
/esg-report
```

### 2. 모듈 선택 (선택 사항)

| 입력 | 생성 범위 |
|------|---------|
| `/esg-report` 또는 `/esg-report full` | E+S+G 전체 리포트 |
| `/esg-report E` | Environmental만 |
| `/esg-report S` | Social만 |
| `/esg-report G` | Governance만 |
| `/esg-report ES` | Environmental + Social |

### 3. 데이터 입력

두 가지 모드를 지원합니다:

**파일 기반 모드** — CSV 또는 JSON 파일 경로를 제공:
```
/esg-report full ./data/company_data.csv
```

**대화형 모드** — 파일 없이 실행하면 구조화된 질문으로 데이터 수집:
```
/esg-report
```

대화형 모드에서 수집하는 정보:
- 기업명 (한/영), 산업 분류, 상장 여부
- 자산/매출 규모, 임직원 수
- GHG 배출량, 에너지 사용량, 재생에너지 비율
- 인적자본 지표 (다양성, 교육, 안전)
- 이사회 구성, 윤리경영 현황

> 모든 데이터가 없어도 보고서 생성이 가능합니다. 누락 항목은 `[데이터 수집 필요]`로 표시됩니다.

### 4. 산출물

`output/` 디렉토리에 3개 파일이 생성됩니다:

```
output/
├── {company}_ESG_Report_{year}.md        # Markdown 보고서
├── {company}_ESG_Report_{year}.html      # HTML 인터랙티브 보고서
└── {company}_Framework_Index_{year}.md   # 프레임워크 색인
```

---

## HTML 보고서 기능

### 언어 토글
우상단 KR/EN 버튼으로 한국어/영어 전환. 모든 섹션 제목, 테이블 헤더, KPI 라벨, 설명 텍스트, 버튼, 모달까지 전체 전환됩니다.

### 섹션 편집
- **삭제**: 각 섹션 우상단 휴지통 아이콘
- **순서 변경**: 위/아래 화살표 버튼
- **추가**: 섹션 사이의 "+ 섹션 추가" 버튼 클릭 → 모달에서 선택

### 추가 가능 섹션
기본 포함 섹션 외에 아래 섹션을 추가할 수 있습니다 (모두 풀 데이터 포함):

| 섹션 | 필러 | 포함 데이터 |
|------|------|-----------|
| CEO 메시지 | 공통 | ESG 경영 성과 하이라이트 |
| 기후변화 대응 | E | TCFD 4 Pillar, 시나리오 분석, 탄소 가격 |
| 에너지 관리 | E | KPI 카드 4개, 3개년 데이터 테이블, RE100 |
| 수자원 관리 | E | 취수/재이용/원단위 3개년 데이터 |
| 생물다양성 | E | TNFD LEAP, 보호구역, 복원 활동 |
| 인권 | S | 인권 실사(HRDD), 강제노동, 교육 현황 |
| 제품 책임 | S | KPI 카드 4개, 침해건수, 만족도, 인증 |
| DEI / 다양성 | S | 5개 지표 3개년 트렌드 |
| 주주 권리 | G | 배당, 전자투표, 소액주주 권리 |
| 리스크 관리 | G | ERM 4개 유형별 리스크/대응 |
| UN SDGs 연계 | 공통 | 7개 SDG 매핑 + 보고 위치 |

### PDF 다운로드
하단 "PDF 다운로드" 버튼 클릭 → 브라우저 인쇄 다이얼로그 → "PDF로 저장" 선택.

PDF 최적화:
- 커버 페이지가 한 페이지에 꽉 차게 출력
- 각 섹션(01, 02, 03...)이 새 페이지에서 시작
- KPI 카드 4열 레이아웃 유지
- 테이블/callout 페이지 경계 잘림 방지
- 편집 UI (버튼, 툴바) 자동 숨김

---

## 프로젝트 구조

```
Claude_Report_Skills/
├── CLAUDE.md                          # 프로젝트 지침
├── README.md                          # 이 파일
├── .gitignore                         # output/ 제외
├── .claude/
│   └── commands/
│       └── esg-report.md              # /esg-report 슬래시 커맨드 정의
├── skills/
│   └── esg-report/
│       ├── SKILL.md                   # 메인 오케스트레이션 (5-Phase)
│       ├── assets/
│       │   └── html-template.html     # HTML 인터랙티브 에디터 템플릿
│       └── references/
│           ├── framework-crossmap.md  # 40개 프레임워크 교차 매핑 테이블
│           ├── frameworks-international.md  # 해외 25개 프레임워크 상세
│           ├── frameworks-korean.md   # 국내 15개 프레임워크 상세
│           ├── report-structure.md    # 보고서 전체 목차 및 섹션 가이드
│           ├── metrics-catalog.md     # E/S/G KPI 정의 및 산정 가이드
│           ├── bilingual-glossary.md  # 한영 ESG 용어집 + 표기 규칙
│           ├── data-requirements.md   # 데이터 입력 스키마 (CSV/JSON)
│           └── quality-checklist.md   # 최종 품질 검증 체크리스트
└── output/                            # 생성된 보고서 (gitignore)
```

---

## 보고서 생성 프로세스 (5-Phase)

### Phase 1: Input Assessment
기업 기본 정보 수집 및 모듈 선택. 파일 기반 또는 대화형 모드 결정.

### Phase 2: Framework Mapping
기업 프로필(산업, 상장 여부, 자산 규모, 사업 지역)에 기반하여 적용 프레임워크 자동 매핑.

- 의무 적용: KSSB (자산 2조+), 지배구조보고서, 배출권거래제
- 자율/권고: GRI, ISSB, TCFD, SASB, K-ESG, CDP, SBTi
- 산업별: PCAF/SFDR (금융), TNFD (자원/에너지), ISO 45001 (제조)

### Phase 3: Data Collection
대화형 모드 시 구조화된 질문 (Round 1~4)으로 E/S/G 데이터 수집. 부분 데이터 허용.

### Phase 4: Report Generation
Markdown → HTML 순차 생성. HTML은 인터랙티브 에디터 구조 (`section-wrapper` + 삭제/이동/추가 UI + `availableSections` 배열).

### Phase 5: Quality Assurance
9개 항목 검증: 프레임워크 완전성, 데이터 정합성, 중대성 커버리지, 이중언어 일관성, 보증 적격성, 규제 준수, 구조/형식, HTML 렌더링, 면책 조항.

---

## 지원 프레임워크 (40개)

### 국내 (15개)
KSSB, K-ESG, KRX ESG 가이던스, 기업지배구조보고서, K-Taxonomy, 배출권거래제(K-ETS), 목표관리제, 환경정보공개제도, 스튜어드십 코드, KCGS ESG 평가, 금감원 기후리스크 가이던스, 공공기관 ESG, SV Report, 중대재해처벌법, 녹색채권 가이드라인

### 해외 (25개)
GRI Standards 2021, ISSB (IFRS S1/S2), SASB, TCFD, CDP (Climate/Water/Forests), CSRD/ESRS, EU Taxonomy, TNFD, SBTi, GHG Protocol, UN SDGs, UNGC, PRI, PCAF, SFDR, Equator Principles, ISO 14001, ISO 45001, ISO 26000, IIRC (IR), SROI, UK Corporate Governance Code, UK Stewardship Code, SEC Climate Disclosure Rule, NGFS

---

## 데이터 입력 스키마

CSV 또는 JSON 형식으로 데이터를 제공할 수 있습니다. 상세 스키마는 `skills/esg-report/references/data-requirements.md`를 참조하세요.

### CSV 예시
```csv
field,value
company_name_kr,삼성전자
company_name_en,Samsung Electronics
industry_gics,4520
revenue_krw,258935000000000
reporting_year,2025
```

### JSON 예시
```json
{
  "company": {
    "name_kr": "삼성전자",
    "name_en": "Samsung Electronics",
    "industry_gics": "4520",
    "revenue_krw": 258935000000000,
    "reporting_year": 2025
  },
  "environmental": {
    "ghg": {
      "scope1": { "current": 5200000, "unit": "tCO2e" }
    }
  }
}
```

---

## 라이선스

이 프로젝트는 개인 및 상업적 용도로 자유롭게 사용할 수 있습니다.

> **면책**: AI가 생성한 ESG 보고서는 참고용이며, 최종 데이터 검증 및 보증은 별도로 수행되어야 합니다. 투자 판단의 근거로 사용할 수 없습니다.
