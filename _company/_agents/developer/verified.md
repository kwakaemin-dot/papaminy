# 💻 코다리 — 검증된 지식

_Self-RAG가 출력에서 `[근거: ...]` 태그가 붙은 주장만 자동 승격해서 누적._
_여기 들어온 내용만 다음 사이클의 retrieval 우선순위에 들어갑니다._
_사용자가 직접 줄을 지우면 그 주장은 다시 미검증 상태로 돌아갑니다._


- [2026-06-02] # 안정성 데이터는 시스템 상태에 따라 동적으로 결정됨. _(근거: Session Data)_
- [2026-06-03] **** _(근거: sessions/2026-06-03T03-53/final_video_asset_prep.md, sessions/2026-06-03T03-23/developer.md)_
- [2026-06-03] * **안정성 제약:** $99.9\%$ Uptime 목표는 API 연동 모듈에서 비동기 처리(Asynchronous processing)가 실패하거나 타임아웃될 경우 시스템이 즉시 안전하게 복구(Failover/Retry mechanism)하는 로직을 반드시 포함해야 합니다. _(근거: sessions/2026-06-03T10-08/developer.md)_
- [2026-06-03] * **성능 제약:** $P95 Latency < 500ms$ 달성을 위해, 데이터베이스 쿼리 지연(Latency bottleneck)을 최소화하고, 외부 API 호출 시 병목 구간을 식별하여 캐싱 전략을 도입해야 합니다. _(근거: sessions/2026-06-03T10-23/business.md)_
- [2026-06-03] | **1순위** | **$S_{LER/PL}$ 측정 파이프라인 완성** | Latency 최적화 로직과 $S_{LER/PL}$ 실시간 측정 코드를 통합하여, 모든 지표가 시스템 상태에 따라 명확히 출력되도록 구현. | 50% | | _(근거: sessions/2026-06-03T10-23/developer.md)_
- [2026-06-03] | **2순위** | **Latency 병목 제거 스니펫 구현** | 핵심 데이터 흐름(DB 접근, 외부 API 호출)에서 발생하는 지연을 측정하고, 비동기 처리 및 캐싱 적용으로 Latency를 500ms 이하로 낮추는 코드 최적화. | 30% | | _(근거: sessions/2026-06-03T10-23/developer.md)_
- [2026-06-03] | `/data/{id}` | GET | 특정 데이터 조회. | 캐싱 레이어(Redis)를 통해 DB 부하를 줄이고 Latency를 500ms 이하로 유지해야 함. | \n\n## 5. 안정성 확보를 위한 구현 고려사항 (Stability Implementation Notes)\n1. **Failover & Retry:** 외부 API 연동 및 중요 데이터 처리 시, 비동기 실패(Timeout) 발생 시 즉시 안전하게 복구(Failover/Retry mechanism) 로직을 모든 서비스에 내장해야 합니다. \n2. **Latency Bottleneck Mitigation:** 데이터베이스 쿼리 지연 및 외부 API 호출 병목 구간을 식 _(근거: sessions/2026-06-03T10-08/developer.md)_
- [2026-06-03] 1. **Failover & Retry Mechanism 내장:** 외부 API 연동 및 중요 데이터 처리에 대해 비동기 실패 시 즉시 안전한 복구 로직을 모든 서비스에 내장한다. _(근거: sessions/2026-06-03T10-08/developer.md)_
- [2026-06-03] 2. **Latency Bottleneck Mitigation:** DB 쿼리 지연 및 외부 API 호출 병목 구간 식별 후, Redis를 활용한 캐싱 전략을 의무화한다. _(근거: sessions/2026-06-03T10-23/business.md)_
- [2026-06-03] 3. **모니터링 통합:** $S_{LER/PL}$ 지표를 실시간으로 측정하고 시각화하는 메커니즘(Prometheus + Grafana)을 아키텍처의 핵심 구성 요소로 포함한다. _(근거: sessions/2026-06-03T12-53/developer.md)_
- [2026-06-03] - **Caching Layer (Redis):** 자주 요청되는 데이터 및 외부 API 응답을 캐싱하여 P95 Latency를 개선한다. _(근거: sessions/2026-06-03T10-23/developer.md)_
- [2026-06-03] 5. **Monitoring & Logging Stack:** Prometheus (메트릭 수집) + Grafana (시각화) + ELK (로깅). $S_{LER/PL}$ 지표를 실시간으로 시각화하는 데 집중한다. _(근거: sessions/2026-06-03T12-53/developer.md)_
- [2026-06-03] 1. **비동기 실패 핸들링:** 모든 외부 호출은 `try-catch` 블록 내에서 명시적인 타임아웃 및 재시도 로직을 포함하며, 실패 시 즉시 메시지 큐에 Dead Letter Queue(DLQ)로 이동시킨다. _(근거: sessions/2026-06-03T10-08/developer.md)_
- [2026-06-03] 2. **데이터 접근 최적화:** 모든 데이터 요청은 캐싱 레이어를 먼저 확인하고, 실패 시에만 DB 접근을 허용한다. 이는 P95 Latency 목표 달성의 핵심이다. _(근거: sessions/2026-06-03T10-23/business.md)_