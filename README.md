# Case Studies — GenAI 컨설팅 · 엔지니어링

GenAI 솔루션 델리버리와 사전 검증(PoC)에서 직접 수행한 작업을 정리한 공개 케이스 모음입니다. 고객사 민감 정보·내부 소스는 제외하고, **공개 가능한 사실과 직접 만든 산출물만** 담았습니다.

## 주요 케이스

| 케이스 | 한 줄 요약 |
| --- | --- |
| [A02 — 한국어 TTS 평가 기준 설계](cases/a02-korean-tts-evaluation.md) | 스마트홈 월패드 음성 안내용 한국어 TTS 6종을 "기준 먼저, 측정은 그 다음" 방식으로 실측 비교 → 실제 고객 계약으로 연결 |
| [A07 — Sapie Reco LLM 배치 추천 엔진 델리버리](cases/a07-sapie-reco-batch-recommendation.md) | idus(backpackr) 대상 LLM 기반 야간 배치 상품 추천 엔진 델리버리 총괄 + RAG 코어·PoC 챗봇 직접 구현 (상용 출시) |
| [A08 — public organization 입학상담 챗봇 + 멀티테넌트 RAG 백엔드](cases/a08-yeonsung-admissions-chatbot.md) | FastAPI RAG 백엔드를 단독 설계·구현·운영한 실서비스 ([yeonsung.sapie.ai](https://yeonsung.sapie.ai/)) |

## 보조 기술 증명

리드 케이스를 뒷받침하는 백엔드·델리버리 가드레일 미니 케이스입니다. (단독으로 비즈니스 성과를 주장하지 않습니다.)

| 케이스 | 한 줄 요약 |
| --- | --- |
| [B01 — AI 보조 PoC 델리버리 품질 게이트](cases/b01-ai-poc-quality-gates.md) | AI 보조 개발을 검토·핸드오프 가능하게 가두는 로컬 품질 게이트 워크플로우 |
| [B02 — 프리뷰 우선 AI 코딩 하네스](cases/b02-preview-first-coding-harness.md) | 실행 전 드라이런·사람 검토를 강제하는 AI 보조 구현 핸드오프 패턴 |
| [B03 — 재사용 가능한 인증 메일 워크플로우 API](cases/b03-auth-email-workflow-api.md) | 인증 메일 발송 워크플로우를 Python/FastAPI 서비스·라이브러리로 패키징 |
| [B04 — HWP/HWPX → PDF 문서 워크플로우 API](cases/b04-hwp-to-pdf-workflow-api.md) | 한국 문서 포맷(HWP) 변환 워크플로우를 FastAPI PoC로 패키징 |

## 정직성 · 범위

- **수치를 지어내지 않습니다.** 보유하지 않은 정량 성과(전환율·CTR·상담 건수 등)는 주장하지 않습니다.
- **역할 경계를 명시합니다.** 총괄/리드한 부분과 직접 구현한 부분, 팀 작업을 구분합니다.
- **고객 소스 코드는 비공개입니다.** 공개 근거는 출시 보도자료·운영 URL·본인 보유 공개 레포로 한정합니다.
- 실명 사용(예: idus·public organization·SAPiE)은 공개 승인 범위 안에서만 사용했습니다.

> 언어: 현재 한국어 우선. 영어판은 추후 별도로 정리할 예정입니다. (A02·A07·A08 한국어 / B01–B04 영어 — 통일판은 다음 단계)
