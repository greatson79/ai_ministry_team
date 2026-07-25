# churchTeam — AI 부교역자 팀 시스템

담임목사의 목회와 사역을 보조하는 **31인 AI 에이전트 팀** 오픈 템플릿입니다.
자기 교회의 목회철학·데이터를 넣으면, 시대통찰 분석부터 연간계획·주간사역·설교 준비·
콘텐츠 제작까지 하나의 오케스트레이션 팀으로 작동하는 "가상 목회자 팀"을 구축할 수 있습니다.

> 이 저장소는 **시스템(에이전트·훅·스킬·커맨드)만** 담은 공개 템플릿입니다.
> 특정 교회의 실데이터(목회철학·교인정보·사역계획)는 포함되어 있지 않으며,
> 사용자가 `pastor/`·`data/` 폴더에 **자기 교회 자료를 직접 업로드**해 사용합니다.

---

## 무엇인가

`AgenticWorkflow` 방법론(품질 우선 · SOT 단일화 · CCP · 4계층 검증 · Adversarial Review)을
상속한 계층형 멀티에이전트 시스템입니다. Claude Code 위에서 동작합니다.

```
Lead Orchestrator (5인)   총괄팀장 · 의도해석 · 작업계획 · 팀라우팅 · 응답종합
미래목회전략팀 (6인)       전략종합 · 신학정렬 · 킹덤비전 · 문화세대분석 · AI사역혁신 · 시나리오
사역기획팀 (3인)           기획팀장 · 주간사역설계관 · 메시지정렬관
사역실행팀 (17인)          실행팀장
   ├─ 말씀·설교팀          말씀팀장 · 설교구조 · 현대적용 · 나눔·묵상
   ├─ 양육·교육팀          교육팀장 · 청소년코칭 · 부모교육 · 성장추적
   ├─ 콘텐츠·소통팀        콘텐츠팀장 · SNS · 스토리텔링 · 이미지프롬프트
   └─ 운영·행정팀          운영팀장 · 문서생성 · 데이터추적 · 행사기획
```

## 안전장치 (훅)

| 훅 | 역할 |
|---|---|
| `theology_filter_dual.py` | 모든 산출물의 신학적 정합성 이중 필터 |
| `pastoral_log_pii_mask.py` | 목회 로그의 개인정보(PII) 마스킹 |
| `self_evolution_gate.py` | 에이전트 정의 자기변조 방지 게이트 |
| `output_internal_id_filter.py` | 산출물의 내부 ID 노출 차단 |
| `setup_init_churchteam.py` | 부트스트랩 인프라 사전 검증 |

## 시작하기

```bash
git clone <this-repo> churchTeam
cd churchTeam
claude
```

1. **목회철학 업로드** — `pastor/philosophy/`에 목회철학·설교철학·핵심가치 문서를 넣습니다.
2. **교회 정보 입력** — `pastor/reference/`, `data/`에 교회 기본정보·절기·설교계획을 넣습니다.
3. **`/팀`** 커맨드로 시작합니다.

### 커맨드

```
/팀              메인 진입점
/팀-전략분석     시대통찰 보고서 발행
/팀-연간계획     연간목회계획 작성
/팀-월간         월간 사역 실행
/팀-분기         분기 점검
/팀-건강         시스템 상태 확인
```

자세한 사용법은 [`USER-MANUAL.md`](USER-MANUAL.md)를 참고하세요.

## 데이터 폴더 (사용자가 채움)

| 폴더 | 용도 |
|---|---|
| `pastor/philosophy/` | 목회철학 (모든 판단의 기준) |
| `pastor/reference/` | 참고자료 |
| `pastor/annual-plans/` | 연간방향·연간기획 |
| `data/` | 교회 절기·설교 계획 |
| `reports/` | 팀이 생성하는 전략·기획·정렬 보고서 |
| `output/` | 실행팀 산출물 |

> `pastor/`·`data/`·`reports/`·`output/`의 **실제 콘텐츠는 `.gitignore`로 제외**됩니다.
> 각 폴더의 `README.md`가 업로드 가이드를 담고 있습니다.

## 선택적 연동

- **부모 게놈** `AgenticWorkflow-Template` — 있으면 `CHURCHTEAM_PARENT_ROOT` 환경변수로 경로 지정.
- **환경스캐닝 시스템** — 있으면 `CHURCHTEAM_ENVSCAN_ROOT`로 지정, 없으면 WebSearch 폴백.
- **weekly-works / church-admin** 하위 시스템 — `.claude/skills/*-bridge.md`에서 경로를 연결.

## 라이선스

[MIT](LICENSE)
