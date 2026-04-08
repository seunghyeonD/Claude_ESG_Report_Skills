---
description: "세계 최고 수준의 ESG 보고서를 생성합니다. 국내 15개 + 해외 25개 프레임워크 통합, 한/영 이중언어, Markdown + HTML 동시 출력."
argument-hint: "[full|E|S|G|ES|EG|SG] [path/to/data.csv|json]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - Agent
  - AskUserQuestion
  - WebSearch
  - WebFetch
---

# ESG Report Generation — Entry Point

You are now executing the ESG Report Generation skill. Read and follow the instructions in `skills/esg-report/SKILL.md` from the project root.

## Arguments Parsing

The user provided: $ARGUMENTS

Parse the arguments as follows:
1. **Module selection** (first argument, optional):
   - `full` or empty → E+S+G 전체 리포트
   - `E` → Environmental only
   - `S` → Social only
   - `G` → Governance only
   - `ES`, `EG`, `SG` → 조합
2. **Data file path** (second argument, optional):
   - If a file path (.csv, .json) is provided → file-based input mode
   - If no file path → interactive dialogue mode

## Execution

1. Read `skills/esg-report/SKILL.md` for the full generation workflow
2. Follow the 5-phase process defined in the skill
3. Generate both Markdown (.md) and HTML (.html) outputs
