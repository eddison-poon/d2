# Agent Hub Capacity & Scalability Performance Test Plan

## 1. Objective

Establish the relationship between:

**Concurrent Agents → QPM → Response Time → Infrastructure Capacity**

The test should determine:

- Maximum sustainable QPM within the agreed response-time target.
- Concurrent agents supported at sustainable capacity.
- Capacity of the minimum viable Agent Hub infrastructure.
- Key infrastructure indicator(s) when capacity is approached.
- How capacity changes when infrastructure instances are increased.

---

## 2. Test Prerequisites

Before execution:

- [ ] Define the **SIMPLE-01** low-token, repeatable prompt.
- [ ] Confirm **1 virtual user = 1 active agent** for this test.
- [ ] Agree the **P95 response-time target**.
- [ ] Agree the acceptable **error / timeout / throttling rate**.
- [ ] Confirm the authoritative source for measuring **QPM**.
- [ ] Confirm where **CPU, memory and instance/pod utilisation** will be collected.
- [ ] Record the current Agent Hub infrastructure configuration.

---

## 3. Stage 1 — Capacity Discovery

**Goal:** Find the maximum sustainable QPM and concurrent-agent capacity of the current environment.

### Tasks

- [ ] Run SIMPLE-01 with 1 agent to establish the baseline.
- [ ] Increase concurrent agents progressively, e.g. **1 → 2 → 5 → 10 → 20 → 30 → 50 → ...**.
- [ ] Keep the prompt and workload behaviour unchanged.
- [ ] Record QPM, P95 response time, error rate and infrastructure utilisation at each level.
- [ ] Use smaller load increments when performance degradation becomes visible.
- [ ] Identify the highest load that still meets the agreed target.
- [ ] Continue sufficiently beyond that point to identify approximate saturation.

### Results

| Agents | QPM | P95 | Error % | CPU % | Memory % | Result |
|---:|---:|---:|---:|---:|---:|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |

**Maximum Sustainable QPM:** TBD  
**Concurrent Agents Supported:** TBD  
**Observed Saturation QPM:** TBD

---

## 4. Stage 2 — Minimum Infrastructure Isolation

**Goal:** Determine the capacity of the smallest viable Agent Hub infrastructure configuration.

### Tasks

- [ ] Define and record the minimum viable infrastructure configuration.
- [ ] Repeat the Stage 1 workload using this configuration.
- [ ] Determine maximum sustainable QPM.
- [ ] Determine concurrent agents supported.
- [ ] Record the infrastructure utilisation at sustainable capacity.

### Results

| Measure | Result |
|---|---|
| Minimum Infrastructure Configuration | TBD |
| Sustainable QPM | TBD |
| Concurrent Agents Supported | TBD |
| P95 Response Time | TBD |
| Primary Resource Utilisation | TBD |

This result becomes the initial **Agent Hub Capacity Unit**.

---

## 5. Stage 3 — Infrastructure Sampler

**Goal:** Identify the infrastructure signals associated with increasing load and approaching saturation.

Infrastructure data should be collected during Stages 1, 2 and 4.

### Minimum Metrics

- CPU utilisation
- Memory utilisation
- Active instance/pod count
- QPM
- P95 response time
- Errors / timeouts / throttling

### Tasks

- [ ] Correlate infrastructure metrics with each tested concurrency level.
- [ ] Identify which resource increases materially as QPM increases.
- [ ] Identify the primary indicator when sustainable capacity is approached.
- [ ] Record any downstream dependency or quota that limits capacity.

**Primary Saturation Indicator:** TBD  
**Other Constraint / Dependency:** TBD

---

## 6. Stage 4 — Scaling Validation

**Goal:** Determine whether adding Agent Hub infrastructure provides predictable additional capacity.

Use selected configurations such as **1 → 2 → 4 instances/capacity units**, where practical.

### Tasks

- [ ] Keep SIMPLE-01 and the service-level target unchanged.
- [ ] Determine sustainable QPM for each infrastructure configuration.
- [ ] Record concurrent agents supported.
- [ ] Compare capacity increase against infrastructure increase.
- [ ] Determine whether capacity scales approximately linearly.
- [ ] Record any shared bottleneck preventing further scaling.

### Results

| Capacity Units | Sustainable QPM | Concurrent Agents | P95 | Observation |
|---:|---:|---:|---:|---|
| 1 | | | | |
| 2 | | | | |
| 4 | | | | |

**Scaling Behaviour / Efficiency:** TBD  
**Shared Bottleneck:** TBD

---

## 7. Execution Tracker

| ID | Activity | Status | Result / Evidence |
|---|---|---|---|
| PREP-01 | Define SIMPLE-01 and targets | Not Started | |
| CAP-01 | Stage 1 — Capacity Discovery | Not Started | |
| ISO-01 | Stage 2 — Minimum Infrastructure | Not Started | |
| INF-01 | Stage 3 — Infrastructure Sampler | Not Started | |
| SCALE-01 | Stage 4 — Scaling Validation | Not Started | |
| FINAL-01 | Consolidate Capacity Model | Not Started | |

**Status:** `Not Started` / `In Progress` / `Blocked` / `Completed`

---

## 8. Final Deliverable

At completion, consolidate the evidence into the following capacity statement:

> Under **SIMPLE-01**, Agent Hub supports approximately **X concurrent active agents / Y sustainable QPM** while maintaining **P95 ≤ Z seconds** and the agreed reliability target.
>
> The minimum viable infrastructure configuration supports approximately **A QPM / B concurrent agents**, establishing the initial Agent Hub **Capacity Unit**.
>
> Scaling from **1 → N capacity units** provides approximately **C% scaling efficiency**. The primary observed capacity indicator is **Resource D**.
>
> Future capacity planning should use the measured sustainable capacity, scaling behaviour and appropriate operational headroom rather than the observed saturation limit.

### Final Results

| Capacity Measure | Result |
|---|---|
| Maximum Sustainable QPM | TBD |
| Concurrent Agents Supported | TBD |
| P95 at Sustainable Capacity | TBD |
| Minimum Capacity Unit QPM | TBD |
| Agents per Capacity Unit | TBD |
| Saturation Indicator | TBD |
| Scaling Efficiency | TBD |
