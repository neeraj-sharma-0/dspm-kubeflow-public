# DSPM for ML Pipelines — Kubeflow Orchestration and Data Governance

## Overview

Implements DSPM lifecycle controls within ML pipelines orchestrated using Kubeflow.

This repository extends vector data governance into the **pipeline layer**, where data flows through ingestion, transformation, training, and inference stages. It focuses on applying **classification, audit, policy enforcement, and controlled deletion** within pipeline execution.

This is a **pipeline governance framework**, not a model performance or training optimization system.

---

## Core Objective

> Apply DSPM controls to ML pipelines to ensure data is classified, audited, governed, and deletable with structured evidence across pipeline stages.

---

## What This Project Does

Within a Kubeflow pipeline, the system:

1. **Ingests data**
   - structured or synthetic datasets

2. **Classifies data**
   - sensitivity levels
   - PII and secrets
   - ownership and source

3. **Processes data through pipeline stages**
   - transformation
   - feature preparation
   - optional training steps

4. **Audits pipeline data**
   - computes risk scores
   - assigns severity levels

5. **Applies policy gate**
   - pass/fail based on critical/high thresholds

6. **Generates evidence artifacts**
   - CSV reports
   - JSON policy outputs
   - SHA256 receipts

7. **Executes destroy phase**
   - deletes pipeline artifacts / outputs
   - records closure with proof-of-absence flag

---

## DSPM Lifecycle Coverage

| Stage    | Implementation                                              |
|----------|-------------------------------------------------------------|
| Discover | Data ingestion and classification                           |
| Classify | Sensitivity, PII, secrets, owner, source                    |
| Audit    | Risk scoring across pipeline data                           |
| Enforce  | Policy gate within pipeline execution                       |
| Destroy  | Artifact deletion with count-based verification             |

---

## Destroy Phase

Pipeline artifacts are deleted and verified using:

- `count_before`
- `count_after`
- `proof_of_absence: true` when `count_after == 0`

> Verification is **count-based only**.  
> Semantic or model-level data persistence validation is not implemented.

---

## Evidence Output

Artifacts are generated per pipeline run:

- `pipeline_input.csv`
- `classification.csv`
- `audit_report.csv`
- `policy_gate.json`
- `pipeline_metadata.json`
- `destroy_closure.json`
- `manifest.json`
- `receipts.json`

Outputs are written to:
