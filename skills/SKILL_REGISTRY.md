# D5 The SRE Commander — Skill Registry

> **Persona:** D5 The SRE Commander  
> **Version:** 1.0.0  
> **Date:** 2026-07-01  
> **Source Strategy:** `C:\KimiWork Projects\GAI-OBSERVE-DESIGN\skills-hooks-plugins-strategy\STRATEGY.md`  
> **Persona Definition:** `C:\KimiWork Projects\CORPORATE V 0.5\PERSONA_D5_The_SRE_Commander.md`  

---

## 1. Registry Overview

This document defines the skill bindings for D5 The SRE Commander. Skills are **reusable procedural capabilities** that augment the arm's decision-making, evidence production, and artifact generation. Each skill entry includes the trigger condition, input/output contract, execution procedure, quality gates, error handling, evidence requirements, and usage examples.

All skills are pre-installed managed skills under `C:\Users\muamm\AppData\Roaming\kimi-desktop\daimon-share\daimon\skills\`.

---

## 2. Skill Definitions

### 2.1 `observability-engineering` — Observability Stack Design & Implementation

| Field | Value |
|-------|-------|
| **Name** | `observability-engineering` |
| **Description** | End-to-end observability stack design: metrics, logs, traces, dashboards, and alerts. Produces architecture diagrams, YAML configs, Grafana dashboards, and SLO definitions. |
| **Owner** | D5 The SRE Commander (primary), D9 The Forward Engineer (secondary) |
| **Trigger** | New service onboarding; observability gap detected; SLO review cycle; customer request for monitoring |
| **Input** | `{"services": array, "environment": string, "retention_days": int, "slos": array, "alert_channels": array, "existing_stack": object}` |
| **Output** | `{"architecture_diagram": string, "prometheus_config": string, "grafana_dashboards": array, "alert_rules": array, "slo_definitions": array, "coverage_score": float, "implementation_guide": string}` |
| **Procedure** | 1. Inventory all services and their endpoints. 2. Design metric schema (golden signals + custom). 3. Configure log aggregation (Loki/ELK). 4. Enable distributed tracing (Jaeger/Tempo). 5. Generate Grafana dashboards. 6. Define alert rules with severity routing. 7. Validate SLO coverage. 8. Produce implementation guide. |
| **Quality Gates** | Golden signals coverage >= 90%; alert precision >= 0.85; dashboard load time < 2s; SLO definitions measurable; no PII in metrics labels |
| **Error Handling** | `STACK_DEPLOY_FAILURE` → retry with partial deploy; `DASHBOARD_GEN_FAILURE` → fallback to JSON export; `ALERT_RULE_CONFLICT` → flag for review |
| **Evidence** | Architecture diagram + YAML configs + dashboard URLs + SLO definitions + coverage score |
| **Example** | `{"services": [{"name": "billing-service", "port": 8080}], "environment": "prod", "slos": [{"name": "availability", "target": 0.999}]}` → `{"coverage_score": 0.95, "grafana_dashboards": ["db-billing-001"]}` |

### 2.2 `incident-response` — Incident Triage & Runbook Execution

| Field | Value |
|-------|-------|
| **Name** | `incident-response` |
| **Description** | Structured incident response: automated triage, runbook execution, escalation management, and communication coordination. Produces incident timeline, post-mortem, and improvement action items. |
| **Owner** | D5 The SRE Commander (primary), D3 The Delivery Captain (secondary) |
| **Trigger** | Alert threshold breach; on-call page; synthetic test failure; manual incident report |
| **Input** | `{"incident_signal": object, "runbook_id": string, "on_call_rotation": string, "severity": string, "communication_channels": array}` |
| **Output** | `{"incident_id": string, "timeline": array, "runbook_steps_executed": int, "escalation_log": array, "communication_log": array, "mttr_seconds": int, "post_mortem_id": string, "action_items": array}` |
| **Procedure** | 1. Acknowledge incident and create ticket. 2. Execute triage runbook (automated where possible). 3. Correlate with recent deployments and changes. 4. Apply mitigation or rollback. 5. Verify service recovery. 6. Coordinate communication (Slack, status page). 7. Generate post-mortem and action items. 8. Record in P2 ledger. |
| **Quality Gates** | MTTD < 2 min; MTTR < 30 min; all steps logged; communication sent within 5 min; post-mortem within 24h; no blame language |
| **Error Handling** | `RUNBOOK_NOT_FOUND` → search LTM for similar runbook; `ESCALATION_FAILURE` → page via alternative channel; `COMMUNICATION_FAILURE` → fallback to email |
| **Evidence** | Incident ticket + timeline + runbook log + communication log + post-mortem + ledger hash |
| **Example** | `{"incident_signal": {"alert_name": "HighLatency", "service": "auth-service"}, "runbook_id": "rb-auth-001"}` → `{"mttr_seconds": 960, "post_mortem_id": "pm-20260701-001"}` |

### 2.3 `capacity-planning` — Predictive Scaling & Cost Optimization

| Field | Value |
|-------|-------|
| **Name** | `capacity-planning` |
| **Description** | Forward-looking capacity planning with time-series forecasting, auto-scaling policy design, and FinOps cost optimization. Produces capacity plans, scaling recommendations, and cost reports. |
| **Owner** | D5 The SRE Commander (primary), CAPCONDUCTOR (federated) |
| **Trigger** | Utilization > 70% for 3 consecutive days; growth spike detected; monthly planning cycle; budget variance alert |
| **Input** | `{"service_id": string, "forecast_horizon_days": int, "historical_utilization": array, "growth_assumption": float, "current_cost_usd": float, "budget_usd": float}` |
| **Output** | `{"capacity_plan_id": string, "forecast": array, "recommended_scaling": array, "auto_scaling_policy": object, "cost_forecast_usd": float, "optimized_cost_usd": float, "savings_usd": float, "headroom_percentage": float, "confidence": float}` |
| **Procedure** | 1. Ingest historical utilization data. 2. Apply forecasting model (ARIMA/Prophet/ML). 3. Project resource needs. 4. Design auto-scaling policies (HPA/VPA). 5. Analyze cost data for waste. 6. Recommend right-sizing and reserved capacity. 7. Validate against SLOs. 8. Produce capacity plan and cost report. |
| **Quality Gates** | Forecast accuracy >= 0.85; headroom >= 20%; cost reduction >= 10% where possible; auto-scaling policies SLO-safe; all recommendations ledgered |
| **Error Handling** | `FORECAST_FAILURE` → fallback to linear projection; `COST_API_FAILURE` → use cached cost data; `SCALING_POLICY_CONFLICT` → flag for human review |
| **Evidence** | Capacity plan + forecast chart + cost analysis + scaling policy YAML + ledger hash |
| **Example** | `{"service_id": "billing-service", "forecast_horizon_days": 90, "current_cost_usd": 12400}` → `{"optimized_cost_usd": 8900, "savings_usd": 3500, "headroom_percentage": 22}` |

### 2.4 `performance-optimization` — Bottleneck Detection & Optimization

| Field | Value |
|-------|-------|
| **Name** | `performance-optimization` |
| **Description** | Comprehensive performance analysis: latency profiling, throughput tuning, resource utilization, and query optimization. Produces benchmark reports, flame graphs, and optimization recommendations. |
| **Owner** | D5 The SRE Commander (primary), D9 The Forward Engineer (secondary) |
| **Trigger** | p95 latency > SLO; throughput decline; resource saturation; customer complaint about slowness |
| **Input** | `{"service_id": string, "metric_type": "latency" | "throughput" | "cpu" | "memory", "baseline": object, "target": object, "duration": string}` |
| **Output** | `{"service_id": string, "bottlenecks": array, "benchmarks": array, "recommendations": array, "before_after": object, "flame_graph_url": string, "estimated_improvement": float, "confidence": float}` |
| **Procedure** | 1. Collect performance metrics and traces. 2. Identify top 3 bottlenecks. 3. Generate CPU/memory flame graphs. 4. Analyze database query plans. 5. Recommend caching, connection pooling, query optimization. 6. Run before/after benchmarks. 7. Produce optimization report. |
| **Quality Gates** | Benchmarks reproducible; flame graphs readable; recommendations actionable; estimated improvement quantified; no regression in other metrics |
| **Error Handling** | `PROFILER_FAILURE` → fallback to metric-only analysis; `BENCHMARK_FAILURE` → retry with longer duration; `QUERY_PLAN_UNAVAILABLE` → skip DB analysis |
| **Evidence** | Benchmark report + flame graphs + query analysis + optimization recommendations |
| **Example** | `{"service_id": "billing-service", "metric_type": "latency", "baseline": {"p95": 2300}, "target": {"p95": 500}}` → `{"bottlenecks": ["N+1 query", "no connection pooling"], "estimated_improvement": 0.78}` |

### 2.5 `chaos-engineering` — Resilience Testing & Game Days

| Field | Value |
|-------|-------|
| **Name** | `chaos-engineering` |
| **Description** | Designs and executes chaos experiments with hypothesis-driven fault injection, game day orchestration, and disaster recovery drills. Produces resilience reports and compliance certificates. |
| **Owner** | D5 The SRE Commander (primary), D7 The Test Automator (secondary) |
| **Trigger** | Quarterly resilience review; new critical service launch; post-incident resilience gap; compliance audit requirement |
| **Input** | `{"service_id": string, "experiment_type": "pod_kill" | "network_partition" | "latency_injection" | "cpu_stress", "hypothesis": string, "blast_radius": int, "duration_minutes": int, "success_criteria": object}` |
| **Output** | `{"experiment_id": string, "service_id": string, "result": "passed" | "failed" | "aborted", "resilience_metrics": object, "deviation_from_hypothesis": object, "rollback_time_seconds": int, "recommendations": array, "game_day_certificate": string}` |
| **Procedure** | 1. Design experiment with hypothesis and blast radius. 2. Validate safety checks (backups, on-call availability, blackout window). 3. Execute fault injection. 4. Monitor resilience metrics during experiment. 5. Validate success criteria. 6. Auto-rollback if thresholds breached. 7. Generate experiment report. 8. Update resilience scorecard. |
| **Quality Gates** | Safety checks all passed; blast radius controlled; rollback < 2 min; success criteria measurable; no customer-facing outage without consent; report within 24h |
| **Error Handling** | `SAFETY_CHECK_FAILURE` → abort experiment; `FAULT_INJECTION_FAILURE` → trigger rollback; `ROLLBACK_FAILURE` → page on-call immediately |
| **Evidence** | Experiment report + resilience metrics + rollback log + game day certificate |
| **Example** | `{"service_id": "auth-service", "experiment_type": "pod_kill", "hypothesis": "p95 < 2s with 50% pods killed", "blast_radius": 2}` → `{"result": "passed", "resilience_metrics": {"p95": 1800, "error_rate": 0.03}}` |

### 2.6 `alert-management` — Alert Design & Noise Reduction

| Field | Value |
|-------|-------|
| **Name** | `alert-management` |
| **Description** | Designs alert rules, routing trees, and severity policies. Reduces alert fatigue through deduplication, correlation, and dynamic thresholding. |
| **Owner** | D5 The SRE Commander (primary) |
| **Trigger** | Alert fatigue complaint; new service needs alerts; false positive surge; alert precision < 0.80 |
| **Input** | `{"service_id": string, "alert_rules": array, "routing_tree": object, "severity_map": object, "deduplication_window": string, "dynamic_thresholding": boolean}` |
| **Output** | `{"service_id": string, "alert_rules_deployed": int, "routing_tree_valid": boolean, "precision_score": float, "estimated_noise_reduction": float, "silence_policies": array, "runbook_links": array}` |
| **Procedure** | 1. Review existing alert rules for redundancy. 2. Apply golden signal alerting. 3. Configure severity-based routing. 4. Enable deduplication and grouping. 5. Set dynamic thresholds where appropriate. 6. Link alerts to runbooks. 7. Validate routing tree. 8. Measure estimated noise reduction. |
| **Quality Gates** | Precision >= 0.90; recall >= 0.95; every alert has a runbook; routing tree has no dead ends; dynamic thresholds have baselines |
| **Error Handling** | `ROUTING_LOOP` → rebuild tree; `ALERT_RULE_CONFLICT` → flag for review; `THRESHOLD_TOO_SENSITIVE` → suggest relaxed threshold |
| **Evidence** | Alert rules YAML + routing tree + precision score + noise reduction estimate |
| **Example** | `{"service_id": "billing-service", "alert_rules": [{"name": "HighLatency", "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m])) > 0.5"}]}` → `{"precision_score": 0.92, "estimated_noise_reduction": 0.35}` |

### 2.7 `runbook-automation` — Runbook Generation & Execution

| Field | Value |
|-------|-------|
| **Name** | `runbook-automation` |
| **Description** | Generates automated runbooks from incident patterns, SRE best practices, and service architecture. Supports decision trees, conditional branching, and rollback procedures. |
| **Owner** | D5 The SRE Commander (primary), D8 The Doc Architect (secondary) |
| **Trigger** | New incident type encountered; runbook gap identified; quarterly runbook review; post-mortem action item |
| **Input** | `{"incident_type": string, "service_id": string, "symptoms": array, "mitigation_steps": array, "rollback_procedure": string, "escalation_matrix": object}` |
| **Output** | `{"runbook_id": string, "service_id": string, "steps": array, "decision_tree": object, "rollback_procedure": string, "automation_level": float, "test_results": object, "version": string}` |
| **Procedure** | 1. Gather incident data and service architecture. 2. Structure decision tree with branches. 3. Write deterministic steps (kubectl, API calls, checks). 4. Add rollback procedure for each risky step. 5. Define escalation matrix. 6. Test runbook in staging. 7. Version and publish. 8. Link to alert rules. |
| **Quality Gates** | All steps deterministic; rollback defined for each risky step; escalation matrix tested; automation level >= 0.70; reviewed by on-call engineer |
| **Error Handling** | `STEP_NON_DETERMINISTIC` → flag for manual step; `ROLLBACK_UNTESTED` → require staging validation; `ESCALATION_MATRIX_INCOMPLETE` → reject until complete |
| **Evidence** | Runbook Markdown + decision tree + test results + version + linked alert rules |
| **Example** | `{"incident_type": "OOMKill", "service_id": "billing-service", "symptoms": ["memory_usage > 90%"], "mitigation_steps": ["Check pod status", "Scale up", "Rollback if correlated with deployment"]}` → `{"runbook_id": "rb-billing-oom-001", "automation_level": 0.85}` |

### 2.8 `cost-optimization` — FinOps Analysis & Waste Reduction

| Field | Value |
|-------|-------|
| **Name** | `cost-optimization` |
| **Description** | Cloud cost analysis with waste identification, right-sizing recommendations, reserved instance planning, and spot instance opportunity detection. |
| **Owner** | D5 The SRE Commander (primary), CAPCONDUCTOR (federated) |
| **Trigger** | Monthly billing review; budget variance > 10%; cost per request increase; FinOps audit |
| **Input** | `{"cloud_provider": "aws" | "gcp" | "azure", "services": array, "time_range": object, "budget_usd": float, "cost_allocation_tags": array}` |
| **Output** | `{"total_cost_usd": float, "waste_usd": float, "waste_percentage": float, "right_sizing_recommendations": array, "reserved_instance_recommendations": array, "spot_opportunities": array, "potential_savings_usd": float, "cost_per_request": float, "confidence": float}` |
| **Procedure** | 1. Ingest cost and usage data from cloud provider. 2. Identify idle resources and orphaned volumes. 3. Compare requested vs. actual utilization. 4. Recommend right-sizing for over-provisioned workloads. 5. Analyze steady-state for reserved instance opportunities. 6. Identify interruptible workloads for spot. 7. Calculate potential savings. 8. Produce FinOps report. |
| **Quality Gates** | Waste identification >= 0.95 accurate; right-sizing recommendations have utilization data; RI recommendations have 30-day baseline; spot workloads have graceful termination; all numbers ledgered |
| **Error Handling** | `COST_API_FAILURE` → use cached data; `TAGGING_INCOMPLETE` → flag unallocated spend; `RESERVATION_CONFLICT` → suggest alternative instance family |
| **Evidence** | Cost report + waste analysis + right-sizing recommendations + RI plan + spot analysis |
| **Example** | `{"cloud_provider": "aws", "services": ["billing-service", "auth-service"], "budget_usd": 15000}` → `{"waste_usd": 3400, "potential_savings_usd": 3500, "cost_per_request": 0.0008}` |

### 2.9 `dora-metrics` — DORA Metrics Tracking & Benchmarking

| Field | Value |
|-------|-------|
| **Name** | `dora-metrics` |
| **Description** | Tracks and benchmarks DORA metrics (deployment frequency, lead time for changes, MTTR, change failure rate) against industry standards. Produces trend analysis and improvement recommendations. |
| **Owner** | D5 The SRE Commander (primary), D3 The Delivery Captain (secondary) |
| **Trigger** | Monthly engineering review; DORA dashboard refresh; team performance review; customer benchmarking request |
| **Input** | `{"time_range": object, "services": array, "team": string, "benchmark_source": "google" | "custom", "output_format": "dashboard" | "pdf" | "json"}` |
| **Output** | `{"deployment_frequency_per_day": float, "lead_time_for_changes_days": float, "mttr_minutes": float, "change_failure_rate": float, "benchmark_percentile": int, "trend": object, "recommendations": array, "dashboard_url": string, "report_path": string}` |
| **Procedure** | 1. Collect deployment data from CI/CD. 2. Calculate lead time from commit to production. 3. Measure MTTR from incident detection to resolution. 4. Calculate change failure rate from deployment success/failure. 5. Benchmark against Google DORA report or custom baseline. 6. Identify improvement priorities. 7. Generate dashboard or report. |
| **Quality Gates** | All metrics calculable from real data; no estimated metrics without flag; benchmark source cited; trend >= 30 days; recommendations actionable |
| **Error Handling** | `CI_CD_DATA_MISSING` → flag metric as unavailable; `INCIDENT_DATA_INCOMPLETE` → use available subset; `BENCHMARK_SOURCE_STALE` → use last known benchmark |
| **Evidence** | DORA dashboard + trend chart + benchmark comparison + improvement recommendations |
| **Example** | `{"time_range": {"from": "-30d", "to": "now"}, "services": ["billing-service"], "team": "platform"}` → `{"deployment_frequency_per_day": 2.3, "lead_time_for_changes_days": 4.2, "mttr_minutes": 47, "change_failure_rate": 0.23, "benchmark_percentile": 65}` |

### 2.10 `toil-elimination` — Automation & Self-Healing Design

| Field | Value |
|-------|-------|
| **Name** | `toil-elimination` |
| **Description** | Identifies operational toil (repetitive manual tasks) and designs automation, self-healing systems, and runbook automation to eliminate it. |
| **Owner** | D5 The SRE Commander (primary), D9 The Forward Engineer (secondary) |
| **Trigger** | On-call survey; toil hotspot detected; repetitive incident pattern; quarterly SRE review |
| **Input** | `{"service_id": string, "on_call_logs": array, "incident_types": array, "manual_steps_count": int, "automation_target": float}` |
| **Output** | `{"service_id": string, "toil_score": float, "toil_hotspots": array, "automation_opportunities": array, "estimated_hours_saved_per_month": float, "self_healing_recommendations": array, "implementation_priority": array, "confidence": float}` |
| **Procedure** | 1. Analyze on-call logs and incident patterns. 2. Count manual steps per incident type. 3. Calculate toil score (manual hours / total hours). 4. Identify top 3 automation opportunities. 5. Design self-healing triggers (auto-restart, auto-scale, auto-rollback). 6. Estimate hours saved. 7. Prioritize by impact vs. effort. 8. Produce toil elimination plan. |
| **Quality Gates** | Toil score based on real data; automation opportunities have clear triggers; self-healing has rollback; estimated savings quantified; no automation without safety checks |
| **Error Handling** | `ON_CALL_DATA_MISSING` → survey on-call engineers; `AUTOMATION_UNSAFE` → require human approval; `SELF_HEALING_CONFLICT` → flag for architecture review |
| **Evidence** | Toil analysis + automation plan + estimated savings + safety review |
| **Example** | `{"service_id": "billing-service", "on_call_logs": ["inc-001", "inc-002"], "manual_steps_count": 12}` → `{"toil_score": 0.35, "estimated_hours_saved_per_month": 24, "automation_opportunities": ["auto-rollback on deployment error"]}` |

---

## 3. Skill-to-Arm Mapping Matrix

| Skill | arm-d5-01 | arm-d5-02 | arm-d5-03 | arm-d5-04 | Primary Usage |
|-------|-----------|-----------|-----------|-----------|---------------|
| `observability-engineering` | ✅ | — | — | — | Stack design |
| `incident-response` | — | ✅ | — | — | Incident handling |
| `capacity-planning` | — | — | ✅ | — | Forecast & scaling |
| `performance-optimization` | ✅ | — | — | ✅ | Bottleneck analysis |
| `chaos-engineering` | — | — | — | ✅ | Resilience testing |
| `alert-management` | ✅ | ✅ | — | — | Alert design |
| `runbook-automation` | — | ✅ | — | — | Runbook generation |
| `cost-optimization` | — | — | ✅ | — | FinOps |
| `dora-metrics` | ✅ | ✅ | ✅ | ✅ | Cross-cutting metrics |
| `toil-elimination` | — | ✅ | ✅ | ✅ | Automation design |

---

**Document Owner:** GAI-OBSERVE Advisory Architecture Team  
**Classification:** Internal — Skill Registry  
**Next Review:** 2026-08-01
