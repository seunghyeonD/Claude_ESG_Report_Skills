# Claude Report Skills — ESG Report Generator

## Project Overview
세계 최고 수준의 ESG 전문가가 국내(15개) + 해외(25개) 프레임워크를 통합하여 이중언어(한/영) ESG 보고서를 생성하는 Claude Code 스킬 프로젝트.

## Skill Structure
- `/esg-report` 슬래시 커맨드로 실행
- `skills/esg-report/SKILL.md` — 메인 오케스트레이션
- `skills/esg-report/references/` — 프레임워크, 지표, 용어 등 참조 데이터 (필요 시에만 로드)
- `skills/esg-report/assets/` — HTML 템플릿

## Key Conventions
- SKILL.md는 2,500 words 이내 유지 (Progressive Disclosure)
- 프레임워크 상세는 references/ 파일에 분리
- HTML 출력은 외부 의존성 없이 self-contained (CSS 임베디드)
- 이중언어: 한국어 primary, 영어 secondary
- 프레임워크 명칭은 영문 원문 사용, 한국어 번역 괄호 병기

## Output
- `{company}_ESG_Report_{year}.md` — Markdown 보고서
- `{company}_ESG_Report_{year}.html` — HTML 보고서 (브라우저/PDF 출력용)
