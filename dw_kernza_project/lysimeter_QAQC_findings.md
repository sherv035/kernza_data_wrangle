# Lysimeter QA/QC Findings
## Kernza Data Wrangle Project — Christopher Sherve
## April 2026

---

## Overview

This document summarizes all quality assurance and quality control (QA/QC) findings
for the lysimeter nitrate (NO3) dataset from the Kernza/alfalfa intercrop study at
Waseca and Lamberton, MN (2014–2015). Findings are organized by issue type with
supporting evidence and recommended handling for each.

**Bottom line:** The lysimeter data is biologically coherent and analytically useable.
Apparent anomalies are explainable by soil type, agronomic timing, and hydrology.
The data is NOT wonky and tells a consistent story that aligns with the published
literature (Jungers et al. 2017, Agron. J. 109:462–472).

---

## 1. Below Detection Limit (BDL) Readings

### What they are
The laboratory instrument cannot reliably quantify nitrate concentrations below a
threshold value. Readings below this threshold are flagged as BDL.

### Inconsistent reporting between years
The two labs used different conventions for reporting BDL values:

| Year | Lab | BDL Convention | Lab Job Number |
|---|---|---|---|
| 2014 | Agvise Laboratories | Reported as **0** (numeric zero) | Water Job 035 |
| 2015 | Research Analytical Laboratory, UMN | Reported as **< 0.1 mg/L** (text string) | Water Job 074 |

This inconsistency was introduced by the laboratory, not by data cleaning. The two
conventions represent the same biological reality — samples below the detection limit.

### Scope of BDL readings

| Year | Total raw readings | BDL readings | % BDL |
|---|---|---|---|
| 2014 | 160 | 61 | 38.1% |
| 2015 | 270 | 157 | 58.1% |
| **Combined** | **430** | **218** | **50.7%** |

### BDL by treatment (combined years)

| Treatment | Total readings | BDL readings | % BDL | Interpretation |
|---|---|---|---|---|
| 0 kg N (trt 21) | 105 | 53 | 50.5% | Background soil N only; biological catch effective |
| 60 kg N (trt 22) | 109 | 65 | 59.6% | Moderate N input; Waseca retains most above 100cm |
| 120 kg N (trt 23) | 104 | 41 | 39.4% | Highest N input; most detectable leaching — fewest BDL |
| Intercrop 40 kg N (trt 25) | 112 | 59 | 52.7% | Alfalfa adds N but dual-root system enhances retention |

**Key finding:** trt 23 (120 kg N) has the FEWEST BDL readings — consistent with
highest N input producing the most consistently detectable leaching. This is the
expected biological pattern and validates that the detection system was functioning.

### BDL by month and agronomic phase

| Month | Agronomic phase | 2014 %BDL | 2015 %BDL | Biologically expected? |
|---|---|---|---|---|
| May | Post-fertilization | 65.6% | 32.2% | ✅ Yes — urea applied April, N still converting/moving |
| June | Post-fert/Peak demand | 37.5% | 35.6% | ✅ Yes — N moving but crop actively taking up |
| July | Peak crop demand | 18.8% | 64.9% | ✅ Yes — see note below on year difference |
| August | Harvest transition | — (missing) | 80.5% | ✅ Yes — grain removed but perennial roots remain |
| September | Post-harvest | 12.5% | 77.8% | ✅ Yes — microbial immobilization increases |
| October | Late season | 56.2% | 96.3% | ✅ Yes — biological N retention at seasonal peak |

**Note on July difference between years:**
- 2014 July: 18.8% BDL — LOW because Lamberton plots had large NO3 pulses
  (9–17 mg/L) from April urea that had 3 months to travel to 100cm depth
- 2015 July: 64.9% BDL — HIGH because crop demand was at maximum, actively
  suppressing leaching across all plots

Both patterns are biologically expected given the agronomic context.

### Sensitivity analysis
Three BDL substitution values were tested (0.025, 0.05, 0.075 mg/L), applied at
the **raw observation level before averaging** plot-year means:

| Substitution | 2014 ANOVA p | 2015 ANOVA p | Combined ANOVA p |
|---|---|---|---|
| BDL = 0.025 mg/L | 0.089 | 0.247 | 0.124 |
| BDL = 0.050 mg/L | 0.090 | 0.250 | 0.124 |
| BDL = 0.075 mg/L | 0.091 | 0.253 | 0.125 |

**All 9 ANOVAs non-significant.** Treatment effects on NO3 leaching are not
statistically significant regardless of BDL handling assumption.

**Selected value for primary analysis: 0.05 mg/L** (half the detection limit —
standard convention for censored environmental data).

### Handling in combined_clean_final.csv
- `NO3_mean_mgL` — plot-year mean with BDL substituted at 0.05 mg/L before averaging
- `n_raw_readings` — number of raw lysimeter readings per plot-year
- `n_bdl_readings` — number of BDL readings per plot-year
- `pct_bdl_readings` — percentage of readings that were BDL
- `any_bdl` — binary flag: 1 = at least one BDL reading in that plot-year (59/64 rows)
- `majority_bdl` — binary flag: 1 = more than half readings were BDL (28/64 rows)

---

## 2. Missing Data — August 2014

### What happened
No lysimeter samples were collected in August 2014 at either Waseca or Lamberton.
The 2014 dataset jumps from July directly to September.

### Most likely explanation
Mid-August is the grain harvest period (Jungers et al. 2017). Lysimeter sampling
requires walking into each plot and extracting suction cup samples — a task that
would be logistically impossible or impractical while harvest crews are actively
cutting and removing biomass from the same plots. This was almost certainly a missed
sampling opportunity due to harvest operations, not a deliberate protocol decision.

### Impact assessment

| Impact | Assessment |
|---|---|
| Affects both sites equally | ✅ Yes — not a differential bias |
| Affects all treatments equally | ✅ Yes — no selective exclusion |
| Creates analytical gap | ⚠️ Yes — harvest transition window not captured in 2014 |
| Introduces bias between sites | ❌ No |
| Introduces bias between treatments | ❌ No |

### What 2015 tells us about the missing window
The 2015 dataset includes August sampling (80.5% BDL) and reveals that the Kernza
system maintained strong biological N retention through the harvest transition despite
the drop in crop N demand. The perennial root system and soil microbial community
continued immobilizing N immediately post-harvest. The 2014 gap likely means we
missed a similar biological signal in that year.

### Recommended statement for methods section
*"No lysimeter samples were collected in August 2014 at either site, coinciding with
the grain harvest period (mid-August; Jungers et al. 2017). This gap likely reflects
logistical constraints during harvest operations and affects both sites and all
treatments equally. The 2015 dataset, which includes August sampling, provides
a complete seasonal record of nitrate dynamics through the harvest transition period."*

---

## 3. Extreme Values — July 2014 Lamberton

### What they are
Six Lamberton plots recorded NO3 concentrations of 9–17 mg/L in July 2014 — far
exceeding all other readings in the dataset (next highest: 5.3 mg/L at Lamberton,
June 2015). The EPA drinking water standard for nitrate is 10 mg/L.

### Affected plots

| Plot | Treatment | NO3 (mg/L) | N rate |
|---|---|---|---|
| 2111 | 120 kg N (trt 23) | 9.043 | 120 kg ha⁻¹ |
| 2116 | 60 kg N (trt 22) | 13.755 | 60 kg ha⁻¹ |
| 2203 | 60 kg N (trt 22) | 16.997 | 60 kg ha⁻¹ |
| 2304 | 120 kg N (trt 23) | 10.265 | 120 kg ha⁻¹ |
| 2319 | 60 kg N (trt 22) | 14.108 | 60 kg ha⁻¹ |
| 2422 | 120 kg N (trt 23) | 17.011 | 120 kg ha⁻¹ |

### Explanation — agronomic timing + soil drainage
These values are NOT data errors. They are biologically and hydrologically expected:

1. **Urea applied April 2014** — approximately 3 months before July sampling
2. **Urea conversion timeline:** urea → ammonium (hydrolysis, ~1 week) →
   nitrate (nitrification, 2–4 weeks) → ready to leach ~4–6 weeks post-application
3. **June 2014 was extremely wet at Lamberton** — 7.39 inches total; Lamberton
   received 5.38 inches in just the first two weeks of September driving water flux
4. **Normania clay loam (Lamberton)** drains more freely than Waseca's Webster clay
   loam — allows water and nitrate to move downward to 100cm depth more readily
5. **3 months post-application + heavy spring rain + freely draining soil** =
   perfect conditions for April urea to arrive at the lysimeter depth in July

**Why the same pattern was ABSENT at Waseca:**
Waseca received even MORE June rain (12.96 inches vs 7.39) yet showed no July
spikes. Webster clay loam (Waseca) is a poorly drained soil with high CEC that
retains nitrogen above 100cm. The Kernza root system intercepted the N before
it reached the lysimeter depth.

### Recommended handling
Retain these values because they are real measurements representing genuine leaching
events. Flag in analysis as high-leaching events. Note that they drive the high
within-treatment variance that contributes to non-significant ANOVA results.

---

## 4. Sensor Errors — Plot 1110

### What they are
Plot 1110 (trt 25, Kernza/alfalfa intercrop, Waseca) shows `* * *` error readings
at both 50cm and 100cm soil moisture sensor depths across multiple dates in
September–October 2015.

### Interpretation
`* * *` indicates the EC-5 sensor returned an out-of-range or malfunction reading.
This is a **localized instrument issue at a single plot**, not a site-wide problem.
All other Waseca plots show normal numeric readings during the same period.

### Impact
- Affects only 1 of 16 Waseca plots for soil moisture
- VWC data for plot 1110 in Sept–Oct 2015 should be treated as missing
- Does not affect lysimeter or yield data for this plot
- Does not affect any Lamberton plots

---

## 5. Waseca BDL Interpretation — Is the Data Useable?

### The concern
Waseca shows BDL rates of 45–85% depending on treatment and year — much higher
than Lamberton. This raises the question: are the lysimeters malfunctioning, or
is the soil too dry to produce samples?

### Evidence that Waseca data is valid

| Evidence | Finding | Source |
|---|---|---|
| Soil moisture at 100cm | Mean VWC = 0.248 m³/m³ (Sep–Oct 2015) | Raw moisture data |
| Adequate VWC for lysimeter function | Field capacity for silt loam ~0.30–0.38; 0.248 is moist | Soil science benchmarks |
| Waseca precipitation | 56.01 inches (May–Oct, 2-yr total) vs Lamberton 43.39 | Weather station data |
| Rain event comparison | Both sites had comparable large events (>1.0 in/day) | Weather station data |
| June 2014 extreme event | Waseca 12.96 inches vs Lamberton 7.39 — yet Waseca BDL | Weather station data |
| Treatment 23 pattern | 120 kg N plots show fewer BDL (39.4%) across both sites | Raw lysimeter data |
| Sensor errors | Localized to plot 1110 only — not site-wide | Raw moisture data |

### Conclusion
Low Waseca lysimeter NO3 reflects **genuinely low soil nitrate availability**,
not equipment failure or reduced soil water flux. The mechanism is the combination
of Webster clay loam's high nitrogen retention capacity and the Kernza perennial
root system actively intercepting nitrate before it reaches 100cm depth.

---

## 6. Site Difference Summary

### Why Lamberton consistently shows higher NO3 than Waseca

| Factor | Waseca | Lamberton | Effect on leaching |
|---|---|---|---|
| Soil type | Webster clay loam | Normania clay loam | Lamberton drains more freely |
| Drainage class | Poorly drained | Moderately well drained | Lamberton has more downward flux |
| CEC | High | Moderate | Waseca retains N more strongly |
| 2-yr precip (May–Oct) | 56.01 inches | 43.39 inches | Waseca wetter — NOT less water |
| Rain event frequency | More frequent | Less frequent | Similar event character |
| Mean NO3 (legit readings) | Lower | Higher | Real biological difference |

**The site difference is NOT explained by:** drought, sensor failure, sampling gaps,
or differential data quality. It IS explained by soil drainage characteristics and
nitrogen retention capacity — fundamental soil properties documented in Jungers
et al. 2017 (Table 1: soil types by site).

---

## 7. Summary Table — All Flagged Issues

| Issue | Year(s) | Site(s) | Trt(s) | Severity | Action |
|---|---|---|---|---|---|
| BDL zeros reported as 0 | 2014 | Both | All | Medium | Substitute 0.05 mg/L before averaging ✅ done in combined_clean_final.csv |
| BDL reported as < 0.1 | 2015 | Both | All | Medium | Substitute 0.05 mg/L before averaging ✅ done |
| August sampling gap | 2014 | Both | All | Low | Document; does not bias comparisons |
| Extreme July values | 2014 | Lamberton | 22, 23 | Low | Retain; biologically valid; flag in analysis |
| Sensor errors (* * *) | 2015 | Waseca | 25 | Low | Treat as missing; plot 1110 VWC only |
| High Waseca BDL rate | Both | Waseca | All | Medium | Retain; reflects real soil biology |
| Treatment 21 no moisture | Both | Both | 21 only | Medium | Document; sensors not installed by design |
| Soil depths missing 2014 | 2014 | Both | All | Low | Document; deeper depths only in 2015 |

---

## 8. Agronomic Calendar Reference

| Date/Period | Event | Relevance to lysimeter data |
|---|---|---|
| April (each year) | Urea N fertilizer applied | First leaching signal expected ~4–6 weeks later |
| May (each year) | First lysimeter sampling | ~4–6 weeks post-fertilization; early N movement |
| June–July | Peak vegetative growth and grain fill | Maximum crop N demand suppresses leaching |
| Mid-August | Grain harvest (Jungers et al. 2017) | Crop N demand drops; harvest gap in 2014 |
| Post mid-August | All biomass removed from plots | Kernza roots remain alive (perennial) |
| August (2015 only) | Lysimeter sampling resumed | Captures harvest transition dynamics |
| September | Post-harvest period | Microbial immobilization increases; BDL rises |
| October | Late growing season | Near-complete biological N retention |
| **October 21, 2014** | **Soils sampled (confirmed)** | Captured at seasonal peak of N immobilization |
| Fall 2015 (exact date TBD) | Soils sampled | Same seasonal context as 2014 |

---

*Document prepared: April 2026*
*Based on analysis of: Lysimeter.xlsx, Moisture.xlsx, Yield.xlsx, Soils.xlsx,*
*was_weather_data.csv, lam_weather_data.csv, combined_clean_final.csv*
*Reference: Jungers et al. 2017. Agron. J. 109:462–472*
