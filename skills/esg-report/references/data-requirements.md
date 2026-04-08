# Data Requirements — 데이터 입력 스키마 및 대화형 질문 설계

## 1. 파일 기반 입력 (CSV/JSON)

### 1.1 CSV 스키마

#### company_profile.csv
```csv
field,value
company_name_kr,삼성전자
company_name_en,Samsung Electronics
industry_gics,4520 (Technology Hardware)
stock_exchange,KRX KOSPI
listing_status,상장
total_assets_krw,426000000000000
revenue_krw,258935000000000
reporting_year,2025
reporting_boundary,연결
fiscal_year_end,12
headquarter_country,대한민국
headquarter_city,수원시
employee_count,267800
major_subsidiaries,"삼성디스플레이,삼성SDI,삼성전기"
previous_esg_reports,Y
esg_rating_kcgs,A+
esg_committee,Y
sbti_committed,Y
re100_committed,Y
```

#### environmental_data.csv
```csv
metric,unit,year_current,year_prev,year_prev2,methodology,scope,verified
ghg_scope1,tCO2e,5200000,5500000,5800000,GHG Protocol,Global,Y
ghg_scope2_location,tCO2e,8100000,8500000,8900000,GHG Protocol,Global,Y
ghg_scope2_market,tCO2e,7800000,8200000,8700000,GHG Protocol,Global,Y
ghg_scope3_total,tCO2e,15000000,14500000,14000000,GHG Protocol,Global,N
ghg_scope3_cat1,tCO2e,8000000,7500000,7000000,Spend-based,Global,N
ghg_scope3_cat4,tCO2e,2000000,1900000,1800000,Distance-based,Global,N
ghg_scope3_cat6,tCO2e,50000,55000,58000,Distance-based,Global,N
ghg_scope3_cat7,tCO2e,120000,125000,130000,Distance-based,Global,N
ghg_scope3_cat11,tCO2e,4800000,4900000,5000000,Product use,Global,N
energy_total,TJ,95000,98000,102000,Direct measurement,Global,Y
energy_renewable,TJ,12000,9000,7000,Direct measurement,Global,Y
energy_renewable_ratio,%,12.6,9.2,6.9,Calculated,Global,N
water_withdrawal,m3,150000000,155000000,160000000,Direct measurement,Global,Y
water_recycled,m3,45000000,40000000,38000000,Direct measurement,Global,Y
water_recycling_rate,%,30.0,25.8,23.8,Calculated,Global,N
waste_total,ton,800000,850000,900000,Direct measurement,Global,Y
waste_hazardous,ton,120000,130000,140000,Classified,Global,Y
waste_recycled,ton,600000,620000,640000,Direct measurement,Global,Y
waste_recycling_rate,%,75.0,72.9,71.1,Calculated,Global,N
nox_emissions,ton,3500,3800,4000,Measurement,Domestic,Y
sox_emissions,ton,1200,1300,1400,Measurement,Domestic,Y
env_investment,million_krw,250000,220000,200000,Financial records,Global,N
env_violations,count,0,1,0,Records,Global,N
env_fines,million_krw,0,50,0,Records,Global,N
eco_certified_products,count,45,38,30,Records,Global,N
```

#### social_data.csv
```csv
metric,unit,year_current,year_prev,year_prev2,breakdown
total_employees,persons,267800,270000,275000,
female_employees,persons,67000,65000,63000,
female_ratio,%,25.0,24.1,22.9,
female_managers,persons,4500,4200,3800,
female_manager_ratio,%,18.5,17.8,16.5,
non_regular_ratio,%,8.2,9.0,9.5,
new_hires,persons,15000,12000,18000,
turnover_rate,%,6.5,7.2,6.8,voluntary only
parental_leave_return_rate,%,95.0,93.0,91.0,
disabled_employment_rate,%,3.2,3.0,2.8,
gender_pay_ratio,ratio,0.82,0.80,0.78,female/male
training_hours_per_employee,hours,75,70,65,
training_investment,million_krw,350000,320000,300000,
ltifr,rate,0.42,0.48,0.55,per 1M hours
oifr,rate,0.05,0.06,0.07,per 200K hours
fatalities_employee,count,0,0,1,
fatalities_contractor,count,1,0,0,
supplier_esg_assessment_rate,%,85,78,70,of Tier 1 suppliers
local_procurement_rate,%,72,70,68,
social_contribution,million_krw,150000,140000,130000,
volunteer_hours,hours,250000,230000,220000,total
data_breaches,count,0,0,1,
customer_satisfaction,score,88.5,87.2,86.0,out of 100
```

#### governance_data.csv
```csv
metric,unit,value,detail
board_total_members,persons,12,
board_independent_members,persons,7,
board_independence_ratio,%,58.3,
board_female_members,persons,3,
board_female_ratio,%,25.0,
board_meetings,count,14,regular 8 + ad hoc 6
board_attendance_rate,%,96.5,
board_avg_tenure,years,3.5,
esg_committee,yn,Y,established 2021
esg_committee_meetings,count,6,
audit_committee_independence,yn,Y,all independent
audit_committee_financial_expert,persons,2,CPA + former CFO
anti_corruption_training_rate,%,98.5,
ethics_violations,count,3,2 confirmed + 1 under investigation
whistleblowing_cases,count,12,
dividend_payout_ratio,%,35.0,
esg_linked_compensation,yn,Y,15% of CEO variable pay
ceo_pay_ratio,ratio,45,CEO/median employee
agm_participation_rate,%,72.0,including proxy votes
```

---

### 1.2 JSON 스키마

```json
{
  "company": {
    "name_kr": "string",
    "name_en": "string",
    "industry_gics": "string",
    "stock_exchange": "string",
    "listing_status": "listed|unlisted",
    "total_assets_krw": "number",
    "revenue_krw": "number",
    "reporting_year": "number",
    "reporting_boundary": "consolidated|separate",
    "headquarter": {"country": "string", "city": "string"},
    "employee_count": "number",
    "major_subsidiaries": ["string"],
    "esg_history": {
      "previous_reports": "boolean",
      "kcgs_rating": "string",
      "esg_committee": "boolean",
      "sbti_committed": "boolean",
      "re100_committed": "boolean"
    }
  },
  "environmental": {
    "ghg": {
      "scope1": {"current": "number", "prev": "number", "prev2": "number", "unit": "tCO2e", "verified": "boolean"},
      "scope2_location": {"current": "number", "prev": "number", "prev2": "number"},
      "scope2_market": {"current": "number", "prev": "number", "prev2": "number"},
      "scope3": {
        "total": {"current": "number", "prev": "number", "prev2": "number"},
        "categories": {
          "cat1": "number", "cat2": "number", "...": "..."
        }
      }
    },
    "energy": {
      "total": {"current": "number", "prev": "number", "prev2": "number", "unit": "TJ"},
      "renewable": {"current": "number", "prev": "number", "prev2": "number"}
    },
    "water": {
      "withdrawal": {"current": "number", "prev": "number", "prev2": "number", "unit": "m3"},
      "recycled": {"current": "number", "prev": "number", "prev2": "number"}
    },
    "waste": {
      "total": {"current": "number", "prev": "number", "prev2": "number", "unit": "ton"},
      "hazardous": {"current": "number", "prev": "number", "prev2": "number"},
      "recycled": {"current": "number", "prev": "number", "prev2": "number"}
    },
    "pollution": {
      "nox": {"current": "number", "unit": "ton"},
      "sox": {"current": "number"},
      "pm": {"current": "number"}
    },
    "management": {
      "env_investment_krw": "number",
      "violations": "number",
      "fines_krw": "number",
      "iso14001_certified_sites": "number",
      "total_sites": "number"
    },
    "taxonomy": {
      "k_taxonomy_eligible_ratio": "number",
      "k_taxonomy_aligned_ratio": "number",
      "green_bond_issued": "boolean",
      "green_bond_amount_krw": "number"
    }
  },
  "social": {
    "employment": {
      "total": "number",
      "female_ratio": "number",
      "female_manager_ratio": "number",
      "non_regular_ratio": "number",
      "new_hires": "number",
      "turnover_rate": "number",
      "gender_pay_ratio": "number"
    },
    "safety": {
      "ltifr": "number",
      "oifr": "number",
      "fatalities_employee": "number",
      "fatalities_contractor": "number",
      "iso45001_certified_sites": "number"
    },
    "training": {
      "hours_per_employee": "number",
      "investment_krw": "number"
    },
    "supply_chain": {
      "esg_assessment_rate": "number",
      "tier1_suppliers": "number",
      "assessed_suppliers": "number"
    },
    "community": {
      "investment_krw": "number",
      "volunteer_hours": "number"
    },
    "privacy": {
      "data_breaches": "number",
      "customer_satisfaction": "number"
    }
  },
  "governance": {
    "board": {
      "total_members": "number",
      "independent_members": "number",
      "female_members": "number",
      "meetings": "number",
      "attendance_rate": "number",
      "avg_tenure_years": "number",
      "skill_matrix": [
        {"name": "string", "type": "inside|outside", "gender": "M|F", "expertise": ["string"]}
      ]
    },
    "committees": {
      "esg_committee": "boolean",
      "audit_independence": "boolean",
      "audit_financial_expert_count": "number"
    },
    "ethics": {
      "anti_corruption_training_rate": "number",
      "violations": "number",
      "whistleblowing_cases": "number"
    },
    "shareholder": {
      "dividend_payout_ratio": "number",
      "agm_participation_rate": "number"
    },
    "compensation": {
      "esg_linked": "boolean",
      "esg_linked_ratio": "number",
      "ceo_pay_ratio": "number"
    }
  },
  "targets": [
    {
      "topic": "string (e.g., 'GHG Reduction')",
      "target": "string (e.g., '2030년까지 Scope 1+2 42% 감축')",
      "base_year": "number",
      "target_year": "number",
      "progress": "number (%)",
      "framework": "string (e.g., 'SBTi')"
    }
  ],
  "certifications": [
    {
      "name": "string",
      "scope": "string",
      "valid_until": "string"
    }
  ]
}
```

---

## 2. 대화형 모드 — 구조화된 질문 설계

### Round 0: 기본 정보 (필수, 모든 모듈)

```
Q1: 기업명을 알려주세요. (한국어 / 영어)
Q2: 어떤 산업에 속하나요? (예: 반도체, 자동차, 금융, IT서비스 등)
Q3: 상장 여부와 거래소를 알려주세요. (예: 코스피 상장, 미상장 등)
Q4: 보고 연도는 몇 년인가요? (예: 2025)
Q5: 총 임직원 수는 몇 명인가요?
Q6: 연결 매출액은 얼마인가요? (원화 기준)
Q7: 이전에 ESG/지속가능경영 보고서를 발행한 적이 있나요?
Q8: 주요 사업장은 어디에 있나요? (국가/도시)
```

### Round 1: ESG 전략 (필수, 모든 모듈)

```
Q9: ESG 전담 조직이 있나요? (위원회, 팀 등)
Q10: 중대성 평가를 실시했나요? 주요 중대 이슈는 무엇인가요?
Q11: ESG 관련 주요 목표나 KPI가 있나요?
Q12: 연계하고 있는 UN SDGs가 있나요?
```

### Round 2: Environmental (E 모듈)

```
[GHG/에너지]
Q13: GHG 배출량을 알고 계신가요? (Scope 1/2/3, tCO2e)
Q14: 에너지 사용량은? (TJ 또는 MWh)
Q15: 재생에너지 사용 비율은?
Q16: 배출권거래제 적용 대상인가요?
Q17: SBTi 감축 목표를 설정했나요?
Q18: 기후 시나리오 분석을 수행했나요? (1.5°C / 2°C)

[수자원/폐기물]
Q19: 용수 사용량은? (m³)
Q20: 폐기물 발생량과 재활용률은?

[기타 환경]
Q21: 환경 투자액은? (원화 기준)
Q22: 환경 법규 위반 건수는?
Q23: ISO 14001 인증을 받았나요?
Q24: K-Taxonomy 녹색경제활동 비율을 산정했나요?
```

### Round 3: Social (S 모듈)

```
[인적자본]
Q25: 임직원 성별 구성은? (남/여)
Q26: 여성 관리자 비율은?
Q27: 비정규직 비율은?
Q28: 1인당 교육훈련 시간은?
Q29: 성별 임금 격차는?

[안전보건]
Q30: 산업재해율(LTIFR)은?
Q31: 사망사고가 있었나요? (임직원/협력사)
Q32: ISO 45001 인증을 받았나요?

[공급망/사회]
Q33: 공급사 ESG 평가를 실시하나요? 비율은?
Q34: 개인정보 침해 사고가 있었나요?
Q35: 사회공헌 투자액은?
Q36: 인권 실사(Due Diligence)를 수행하나요?
```

### Round 4: Governance (G 모듈)

```
[이사회]
Q37: 이사회 구성은? (사내/사외, 총 인원)
Q38: 이사회 여성 비율은?
Q39: 이사회 연간 개최 횟수는?
Q40: ESG 위원회가 있나요?

[윤리/컴플라이언스]
Q41: 반부패 교육 이수율은?
Q42: 윤리경영 위반 사례가 있었나요?
Q43: 내부신고(Whistleblowing) 체계가 있나요?

[보수/주주]
Q44: 경영진 보수에 ESG KPI가 연계되어 있나요? 비율은?
Q45: 배당성향은?
```

### 질문 최적화 규칙:
1. 모듈 선택에 따라 해당 Round만 질문
2. 이전 답변에서 유추 가능한 항목은 스킵
3. "모르겠다" / "아직 없다"도 유효한 답변으로 처리 → `[데이터 수집 필요]`
4. 파일 입력 시 누락된 항목만 보충 질문
5. 한 번에 최대 5~7개 질문 (너무 많으면 피로감)

---

## 3. 데이터 검증 규칙

### 정합성 체크:
- GHG Scope 2 Market ≤ GHG Scope 2 Location (일반적)
- 재생에너지 비율 = 재생에너지 / 총 에너지 × 100 (교차 검증)
- 폐기물 재활용률 = 재활용량 / 총 발생량 × 100
- 여성 비율 = 여성 인원 / 전체 인원 × 100
- 사외이사 비율 = 사외이사 / 전체 이사 × 100
- 전년 대비 급격한 변동(±50%) 시 확인 필요 플래그

### 단위 표준화:
- 에너지: TJ (1 MWh = 0.0036 TJ)
- GHG: tCO2e
- 수자원: m³ (1,000m³ = 1 ML)
- 폐기물: 톤
- 금액: 백만원 (million KRW)

### 누락 데이터 처리:
- `null` / 빈 값 → `[데이터 수집 필요 / Data to be collected]`
- 추정치 → `[추정 / Estimated]` 표시 + 산정 근거 기재
- 해당 없음 → `[N/A]` + 사유 기재
