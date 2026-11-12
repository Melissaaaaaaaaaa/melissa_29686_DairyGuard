# melissa_29686_DairyGuard
Oracle PL/SQL Capstone Project (INSY 8311): Milk Collection Center quality testing, automated spoilage-prevention triggers, cold-chain tank tracking, and farmer payout system.
# DairyGuard: Milk Collection Center Quality Control and Cold-Chain Spoilage Prevention System

**Student Name:** NAHIMANA Melissa  
**Student ID:** 29686  
**Course:** INSY 8311 – Database Development with PL/SQL  
**Instructor:** Eric Maniraguha  
**Academic Year:** 2026–2027 

---

## 1. Problem Statement
Dairy farming is a vital pillar of Rwanda’s agricultural economy, yet Milk Collection Centers (MCCs) and smallholder cooperatives lose up to 15–20% of raw milk daily due to post-harvest spoilage, lack of cold-chain monitoring, and milk adulteration (such as water dilution). Because many local MCCs rely on manual paper ledgers, sub-standard or high-temperature milk is frequently mixed into bulk cooling tanks, contaminating entire batches of good milk and delaying fair farmer payouts.

## 2. Objectives
* **Main Objective:** Design and implement a normalized (3NF) Oracle PL/SQL database system to automate milk quality validation, cold-tank capacity management, and farmer payouts at Milk Collection Centers.
* **Specific Objectives:**
  1. Normalize real-world dairy quality and cooperative collection records into a 3NF relational schema.
  2. Enforce automated quality thresholds (temperature, pH, and lactometer density) using PL/SQL triggers to block contaminated batches from entering bulk cooling tanks.
  3. Automate monthly quality-graded farmer payouts using PL/SQL packages, cursors, and functions.
  4. Connect a live Power BI analytics dashboard to visualize rejected milk batches, tank utilization, and spoilage trends.

## 3. Data Source
* **Primary Dataset:** [Milk Quality Prediction Dataset (Kaggle)](https://www.kaggle.com/datasets/cpluzshrijayan/milkquality) — 1,059 real sensor records of milk pH, temperature, taste, odor, fat, turbidity, and quality grade, licensed for educational use with no personally identifiable information (PII).
* **Contextual Statistics:** National Institute of Statistics of Rwanda (NISR) livestock and dairy production statistics for modeling realistic Rwandan district cooperative volumes and pricing.

## 4. Planned Database Tables (3NF)
1. `DISTRICTS_COOPERATIVES` — Cooperative details, district location, and MCC contact information.
2. `FARMERS` — Registered smallholder dairy farmers and cooperative membership.
3. `COOLING_TANKS` — Bulk chiller tanks at each MCC, maximum capacity (liters), current volume, and target temperature.
4. `MILK_DELIVERIES` — Daily morning and evening milk deliveries linked to farmers and cooling tanks.
5. `QUALITY_TESTS` — Lab measurements per delivery (temperature, pH, density, fat percentage, and assigned quality grade).
6. `FARMER_PAYOUTS` — Monthly payment cycles, accepted liter totals, Grade A quality bonuses, and payment status.
7. `AUDIT_LOG` — Security and compliance trail logging blocked deliveries, manual overrides, and payout updates.

## 5. Planned PL/SQL Features
* **Triggers:**
  * `trg_validate_milk_quality`: Blocks spoiled or adulterated milk (temperature > 7°C or pH outside 6.5–6.8) from being assigned to a bulk cooling tank.
  * `trg_check_tank_capacity`: Prevents milk allocation if a cooling tank's maximum capacity would be exceeded.
  * `trg_audit_payout_changes`: Logs all updates or deletions on `FARMER_PAYOUTS` into `AUDIT_LOG`.
* **Functions & Procedures:**
  * `fn_calculate_quality_grade`: Evaluates lab metrics and returns Grade A, B, or Rejected.
  * `proc_record_delivery`: Validates farmer status, runs quality grading, assigns an available tank, and updates tank volume atomically.
  * `proc_generate_monthly_payouts`: Uses an explicit cursor to compute monthly farmer earnings including Grade A quality bonuses.
* **Packages & Exceptions:**
  * `pkg_dairy_operations`: Encapsulates all collection, grading, and payout subprograms with custom exceptions (`e_contaminated_milk`, `e_tank_full`, `e_inactive_farmer`).

## 6. Innovation
* **Option:** Live Analytics Dashboard
* **Tool:** Microsoft Power BI connected directly to the Oracle Pluggable Database (PDB) via Oracle ODAC/ODBC.
* **Purpose:** Provides MCC managers with real-time KPIs on daily accepted vs. rejected milk volume, cooling tank fill levels, and spoilage trends by district while PL/SQL enforces all validation rules at the database layer.

## 7. Repository Structure
* `docs/research/` — Research log (`research_log.md`) and literature notes
* `docs/proposal/` — Phase 0 project proposal (`.docx` and `.pdf`)
* `docs/presentation/` — Phase 0 and final presentation slides
* `data/` — Raw and cleaned dairy quality datasets
* `scripts/` — Oracle DDL, DML, PL/SQL packages, and triggers (Phases IV–VI)
* `innovation/` — Power BI dashboard files, setup guide, and live screenshots (Phase VII)

## 8. References (APA)
* Food and Agriculture Organization [FAO]. (2023). *Dairy market review: Emerging trends and outlook in East Africa*. FAO.
* chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/https://openknowledge.fao.org/server/api/core/bitstreams/68f7f25d-b3cb-418e-b04d-5708e5bcea1e/content 
* Kanyamibwa, S., & Habimana, J. (2022). Assessment of post-harvest milk losses and quality control along the dairy value chain in Rwanda. *Rwanda Journal of Agricultural Sciences*, 3(1), 45–58.
* National Institute of Statistics of Rwanda [NISR]. (2024). *Seasonal agricultural survey and livestock production report*. NISR.https://statistics.gov.rw/statistical-publications/agriculture-environment/seasonal-agricultural-survey-2024-annual-report-2024
* Patel, A. (2022). *Milk quality prediction dataset* [Data set]. Kaggle. https://www.kaggle.com/datasets/cpluzshrijayan/milkquality
