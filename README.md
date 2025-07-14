# Multimessenger Astronomy App (MMA_app)

This application is a unified framework for real-time and distributed analysis of astrophysical events using **multimessenger astronomy** — combining signals from gravitational waves (GW), radio waves, and other messengers to better understand cosmic phenomena. This application enables **end-to-end multimessenger inference** of astrophysical events by integrating data from **gravitational waves (GWs)** and **electromagnetic (radio) observations**. It supports low-latency event detection, AI-driven data parsing, and joint parameter estimation to improve cosmological constraints (e.g., Hubble constant $H_0$).

The app integrates three core modules:

---

## Modules Overview

This meta-repository aggregates the following three core components:

### 1. MMA_GravitationalWave

- **Purpose:** Detects BNS events using strain data from LIGO detectors in a **federated fashion** — raw data stays at each site.
- **Key Features:**
  - Distributed inference using deep learning across observatory nodes
  - Kafka-based messaging for event publication (e.g., PotentialMerger events)
  - Real-time classification of GW events
- **Output:** Publishes `PotentialMerger` events to the Octopus event fabric for downstream EM follow-up.

[Repo: MMA_GravitationalWave](https://github.com/parth7stark/MMA_GravitationalWave)

### 2. MMA_RadioWave

- **Purpose:** Handles radio follow-up of GW candidates via GCN alerts.
- **Key Features:**
  - Listens to GCN Kafka stream for LVK alerts and partner circulars
  - AI parser for extracting observation data (flux, time) from radio circulars
  - Federated MCMC fitting of radio light curves while preserving data locality
- **Output:** Posterior samples and fitted light curve parameters for downstream analysis.

[Repo: MMA_GravitationalWave](https://github.com/parth7stark/MMA_RadioWave/tree/main)

### 3. MMA_MultimessengerAnalysis

- **Purpose:** Performs joint inference by overlapping posterior samples from GW and radio observations.
- **Key Features:**
  - Combines $d_L$ and $\theta_{\rm obs}$ posteriors from GW and EM data
  - Produces KDE-based corner plots and credible intervals
  - Improves cosmological parameter estimation (e.g., Hubble constant $H_0$)
- **Output:** Joint plots, metrics, and harmonized posteriors.

[Repo: MMA_GravitationalWave](https://github.com/parth7stark/MMA_MultimessengerAnalysis/tree/main)

---

## 🚀 End-to-End Workflow

1. **GW Detection:**  
   `MMA_GravitationalWave` detects a merger and publishes a `PotentialMerger` event.

2. **GCN Response:**  
   `MMA_RadioWave` listens for GCN alerts, matches to GW events, and parses radio data.

3. **Radio Modeling:**  
   Distributed MCMC is run on radio observations to produce posterior samples.

4. **Joint Inference:**  
   `MMA_MultimessengerAnalysis` combines GW and radio posteriors to constrain cosmological parameters.

---

## Setup & Requirements

Each module contains its own setup instructions and dependencies.
