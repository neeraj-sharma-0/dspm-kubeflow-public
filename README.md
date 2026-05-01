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
out/evidence/<pipeline_run_id>/


These support:
- audit traceability  
- reproducibility  
- compliance documentation  

---

## Pipeline Execution

The Kubeflow pipeline defines stages for:

- ingestion  
- classification  
- transformation  
- audit  
- policy enforcement  
- evidence generation  
- deletion  

Each stage produces intermediate artifacts tracked across the pipeline lifecycle.

---

## Example Run

- records processed: 100  
- high severity findings: 12  
- policy gate: FAIL  
- pipeline executed: yes  
- destroy phase: completed  
- count_before: 100  
- count_after: 0  
- proof_of_absence: true  

---

## Scope and Limitations

This repository:

- does not evaluate model accuracy or training performance  
- does not validate semantic retrieval persistence  
- does not guarantee deletion across distributed storage layers  

Focus is limited to:
- pipeline-level governance  
- lifecycle control enforcement  
- structured evidence generation  

---

## Why This Matters

ML pipelines are a critical execution layer where:

- sensitive data propagates across stages  
- intermediate artifacts persist  
- governance controls are often inconsistent  

This project demonstrates how DSPM principles can be applied to **pipeline execution environments**, enabling:

- data visibility  
- policy enforcement  
- controlled deletion  
- audit-ready evidence  

---

## One-Line Summary

> DSPM governance framework for Kubeflow pipelines with lifecycle controls, policy enforcement, and verifiable artifact deletion.
