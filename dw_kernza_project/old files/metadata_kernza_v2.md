# Metadata: Kernza Data Wrangle Project
**Dataset:** combined_clean.csv
**Author:** Christopher Sherve
**Date:** April 2026
**Project:** Kernza/Legume Intercrop Data Wrangling — University of Minnesota
**Sites:** Waseca, MN and Lamberton, MN
**Years:** 2014–2015 (Years 3 and 4 of the study)
**Source publications:**
- Jungers et al. 2017. Agronomy Journal 109:462–472. doi:10.2134/agronj2016.07.0438
- Culman et al. 2013. Agronomy Journal 105:735–744. doi:10.2134/agronj2012.0273

---

## Experimental Design

### Overview
A nitrogen fertilizer rate trial was conducted at Waseca and Lamberton, MN comparing
Kernza intermediate wheatgrass (Thinopyrum intermedium, TLI-C2) grown in monoculture
at three N rates versus a Kernza/alfalfa intercrop system. Plots were seeded in fall 2011
following soybean. Data here are from years 3 and 4 of the study (2014 and 2015 only).
The 2013 data year is not included in this dataset.

### Design Structure
The experimental design was a **Randomized Complete Block Design (RCBD)**:
- 2 locations (Waseca, Lamberton)
- 4 treatments per location
- 4 complete blocks (replicates) per location
- 1 plot per treatment per block = 16 plots per location = 32 plots total
- Each plot measured in 2014 and 2015 (repeated measures — same physical plots both years)
- Year is a **repeated measure** on the same experimental units, NOT independent replication
- Kernza is a perennial crop — plots were not replanted between years

### Plot Numbering Key
Plot numbers encode both site and block identity:
- **Thousands digit:** 1xxx = Waseca | 2xxx = Lamberton
- **Hundreds digit:** x1xx = Block 1 | x2xx = Block 2 | x3xx = Block 3 | x4xx = Block 4
- Example: Plot 1303 = Waseca, Block 3 | Plot 2217 = Lamberton, Block 2

### Treatments

| Treatment Code | trt | Crop System | N Fertilizer Rate |
|---|---|---|---|
| I0 | 21 | Kernza monoculture (TLI) | 0 kg N ha⁻¹ |
| I60 | 22 | Kernza monoculture (TLI) | 60 kg N ha⁻¹ |
| I120 | 23 | Kernza monoculture (TLI) | 120 kg N ha⁻¹ |
| IL | 25 | Kernza/alfalfa intercrop (TLI/leg) | 40 kg N ha⁻¹ |

**Treatment code cross-reference confirmed** against Yield.xlsx, Lysimeter.xlsx (2015
sheet), and Soils.xlsx — all files verified as consistent (32 of 32 plots matched).

> Note: Original planned rates were 80 and 160 kg N ha⁻¹ for trt 22 and 23. Rates were
> adjusted in 2014 and 2015 to 60 and 120 kg N ha⁻¹ to avoid extreme lodging (Jungers
> et al. 2017).

---

## Agronomic Calendar

Understanding the timing of field operations is critical for interpreting lysimeter and
soil chemistry data.

| Event | Timing | Notes |
|---|---|---|
| N fertilizer (urea) applied | April each year | ~4–6 weeks before first lysimeter sampling |
| First lysimeter sampling | May each year | ~4–6 weeks post-fertilization |
| Peak crop N demand | June–July | Rapid vegetative growth and grain fill |
| Grain harvest | Mid-August | 0.5 × 1m sample area cut to 10cm height |
| Biomass removal | Post mid-August | All remaining biomass removed from plot |
| August lysimeter gap | 2014 only | No sampling during harvest period — both sites |
| Soils sampled | October 21, 2014 | Agvise Laboratories; fall 2015 exact date unknown |
| Last lysimeter sampling | October each year | Soil cooling, end of growing season |

**Agronomic timing explains key patterns in lysimeter data:**
- July 2014 Lamberton spikes (9–17 mg/L): April urea + June rain events provided
  ~3 months for NO3 to travel to 100cm depth in the freely draining Normania clay loam
- September–October BDL at both sites: Post-harvest Kernza roots remain alive and
  active; microbial immobilization of mineral N increases as harvest residue decomposes
- 2015 values generally lower than 2014: Year 4 root system more established;
  consistent with grain yield declines and increasing plant density reported in
  Jungers et al. 2017

---

## Site Descriptions

### Waseca, MN
- **Coordinates:** 44.068°N, 93.526°W
- **Soil type:** Webster clay loam (poorly drained, high clay content, high CEC)
- **Soil drainage:** Poor — high water holding capacity, strong nitrogen retention
- **Weather station:** nearest NOAA station; data available May–November 2014–2015
- **Growing season precip (May–Oct):** 23.90 in (2014) | 32.11 in (2015) | 56.01 in combined
- **Key characteristic:** Webster clay loam retains nitrogen above 100cm depth; adequate
  soil moisture confirmed (mean VWC 0.248 m³/m³ at 100cm, Sep–Oct 2015) yet low
  lysimeter NO3 — reflects genuine low soil nitrate availability, not equipment failure

### Lamberton, MN
- **Coordinates:** 44.237°N, 95.302°W
- **Soil type:** Normania clay loam (moderately well drained)
- **Soil drainage:** Moderate to good — more freely draining than Waseca
- **Weather station:** nearest NOAA station; data available May–December 2014–2015
- **Growing season precip (May–Oct):** 20.53 in (2014) | 22.86 in (2015) | 43.39 in combined
- **Key characteristic:** Better drainage facilitates downward water and nitrate flux;
  consistently higher lysimeter NO3 despite receiving 22.5% less precipitation than Waseca

### Site Comparison — Precipitation
Waseca received substantially more precipitation than Lamberton across both growing
seasons (56.01 vs 43.39 inches combined). Both sites experienced comparable large
rain event frequencies and intensities (days >1.0 inch: Was 6/11 vs Lam 5/7 in
2014/2015). Temperature was nearly identical between sites (mean Tmax within 1–2°F;
GDD base 50°F within 55 units). Site differences in lysimeter NO3 are therefore
attributable to soil drainage characteristics, not climate.

---

## Variable Dictionary

### Identifiers

| Variable | Type | Units | Description |
|---|---|---|---|
| `year` | factor | — | Harvest year (2014 or 2015) — repeated measure |
| `location` | factor | — | Field site (Waseca or Lamberton, MN) |
| `plot` | numeric | — | Unique plot ID; encodes site and block (see Plot Numbering Key) |
| `replicate` | numeric | — | Block number (1–4); equivalent to block in RCBD |
| `trt` | factor | — | Treatment code (21, 22, 23, 25 — see Treatments table) |
| `crops` | character | — | Crop system (TLI = Kernza monoculture; TLI/leg = Kernza/alfalfa) |
| `legume_inclusion` | binary | 0/1 | Whether alfalfa was intercropped (1=yes, 0=no) |
| `n_fertilizer` | numeric | kg N ha⁻¹ | Actual N fertilizer rate applied (urea, April) |

---

### Yield Variables
Collected once per year at physiological maturity (mid-August). All biomass removed
from each plot and separated by component.

| Variable | Type | Units | Description |
|---|---|---|---|
| `grain_yield` | numeric | kg ha⁻¹ | Kernza grain yield (de-hulled; lemma/palea fraction subtracted) |
| `iwg_straw_yield` | numeric | kg ha⁻¹ | Kernza vegetative (straw) biomass yield post-grain harvest |
| `legume_biomass` | numeric | kg ha⁻¹ | Alfalfa biomass yield; NA for all monoculture plots (trt 21, 22, 23) |
| `plant_height` | numeric | cm | Mean Kernza plant height at harvest (mean of 3 stems per plot, soil to top of seed head) |
| `lodging_score` | numeric | 0–10 scale | 0 = no lodging (plants upright); 10 = complete lodging (plants horizontal) |

---

### Lysimeter Variables (Nitrate Leaching)
Suction cup lysimeters installed at **100cm depth** in each plot. Sampled approximately
monthly during the growing season. Not all plots produced a sample at every event.
Analyzed for nitrate/nitrite concentration at a commercial laboratory.

#### Critical QA/QC Notes — Lysimeter Data

**Below Detection Limit (BDL) handling:**
Nitrate concentration in soil pore water cannot be truly zero in an agricultural system
due to background nitrogen cycling from organic matter mineralization, even in unfertilized
plots. Values reported as zero (2014) and values reported as `< 0.1 mg/L` (2015)
represent the same biological reality — samples below the instrument detection limit —
reported inconsistently between lab submissions:
- 2014 lab (Water Job 035, Agvise): reported BDL as **0** (numeric zero)
- 2015 lab (Water Job 074, Research Analytical Laboratory, UMN): reported BDL as **< 0.1**

**BDL scope:**
- 2014: 61 of 160 raw readings = 38.1% BDL
- 2015: 157 of 270 raw readings = 58.1% BDL
- Combined: 218 of 430 raw readings = 50.7% BDL

**Sensitivity analysis:**
A sensitivity analysis substituting three BDL values (0.025, 0.05, and 0.075 mg/L)
was conducted at the **raw observation level before averaging** plot-year means.
All 9 ANOVAs (3 substitutions × 3 year groupings) returned non-significant results
(p > 0.05), confirming conclusions are not sensitive to BDL handling assumptions.
Selected substitution: **0.05 mg/L** (half the detection limit — standard convention
for censored environmental data).

**August 2014 gap:**
No lysimeter samples were collected in August 2014 at either site — coinciding with
the grain harvest period (mid-August). This affects both sites equally and is likely
an intentional protocol decision to avoid plot disturbance during harvest operations.

**Waseca BDL interpretation:**
High BDL rates at Waseca (45–83% depending on treatment and year) reflect genuinely
low soil nitrate availability rather than equipment malfunction or reduced soil water
flux. Evidence: (1) adequate soil moisture confirmed at 100cm depth (VWC 0.248 m³/m³,
Sep–Oct 2015); (2) Waseca received 22.5% more precipitation than Lamberton; (3) both
sites experienced comparable large rain event frequencies and intensities; (4) Waseca's
Webster clay loam is a poorly drained soil with high nitrogen retention capacity.

**Sensor errors:**
Plot 1110 (trt 25, intercrop, Waseca) shows `* * *` errors at both 50cm and 100cm
depths across multiple dates in September–October 2015. These represent sensor
malfunction or out-of-range readings at this specific plot — not a site-wide issue.

| Variable | Type | Units | Description |
|---|---|---|---|
| `NO3_mean` | numeric | mg L⁻¹ | Mean NO3 concentration across all sampling events for that plot-year (primary analysis variable; BDL substituted at 0.05 mg/L before averaging) |
| `NO3_full_mean` | numeric | mg L⁻¹ | Mean NO3 for full N rate sub-treatment scenario |
| `NO3_half_mean` | numeric | mg L⁻¹ | Mean NO3 for half N rate sub-treatment scenario (identical to NO3_mean in all rows) |
| `NO3_zero_mean` | numeric | mg L⁻¹ | Mean NO3 for zero N rate sub-treatment scenario |

> Note: NO3_half_mean and NO3_mean are identical in all rows. NO3_full_mean and
> NO3_zero_mean differ from NO3_mean only in 2015, where multiple sampling events
> per plot allow scenario-specific averaging. Values differ only in 2015; all four
> columns are identical in 2014 (single sampling event per month per plot).

---

### Soil Moisture Variables
Measured using Decagon EC-5 sensors at two depths. Sensors recorded data every 3–5
days during the growing season. Values in combined_clean.csv are seasonal means for
each plot-year. **Treatment 21 (0 kg N) plots have no moisture data** — sensors were
not installed in these plots (by design, not data loss). This affects 8 plots:
1125, 1217, 1313, 1416 (Waseca) and 2121, 2223, 2324, 2407 (Lamberton).

| Variable | Type | Units | Description |
|---|---|---|---|
| `vwc_50cm` | numeric | m³ m⁻³ | Volumetric water content at 50cm depth (seasonal mean) |
| `vwc_100cm` | numeric | m³ m⁻³ | Volumetric water content at 100cm depth (seasonal mean) |

---

### Soil Chemistry Variables
Soils sampled in fall of each year (confirmed date: October 21, 2014; fall 2015 exact
date unknown). Separated into three depth increments and analyzed for nitrate, ammonium,
and organic matter. **Deeper depth data (6–18" and 18–30") are present only for 2015**
— these depths were not analyzed in 2014.

| Variable | Type | Units | Description |
|---|---|---|---|
| `LOI_OM_pct_0_6` | numeric | % | Soil organic matter (loss on ignition) at 0–6 inch depth |
| `LOI_OM_pct_6_18` | numeric | % | Soil organic matter at 6–18 inch depth (2015 only) |
| `LOI_OM_pct_18_30` | numeric | % | Soil organic matter at 18–30 inch depth (2015 only) |
| `NH4_N_ppm_0_6` | numeric | ppm | Ammonium-nitrogen at 0–6 inch depth |
| `NH4_N_ppm_6_18` | numeric | ppm | Ammonium-nitrogen at 6–18 inch depth (2015 only) |
| `NH4_N_ppm_18_30` | numeric | ppm | Ammonium-nitrogen at 18–30 inch depth (2015 only) |
| `NO3_N_ppm_0_6` | numeric | ppm | Nitrate-nitrogen at 0–6 inch depth |
| `NO3_N_ppm_6_18` | numeric | ppm | Nitrate-nitrogen at 6–18 inch depth (2015 only) |
| `NO3_N_ppm_18_30` | numeric | ppm | Nitrate-nitrogen at 18–30 inch depth (2015 only) |
| `TOC_pct_0_6` | numeric | % | Total organic carbon at 0–6 inch depth (2015 only) |
| `TOC_pct_6_18` | numeric | % | Total organic carbon at 6–18 inch depth (2015 only) |
| `TOC_pct_18_30` | numeric | % | Total organic carbon at 18–30 inch depth (2015 only) |

---

## Missing Values Summary

| Variable(s) | Pattern | Reason |
|---|---|---|
| `legume_biomass` | NA for trt 21, 22, 23 | No alfalfa in monoculture plots |
| `vwc_50cm`, `vwc_100cm` | NA for trt 21 (8 plots) | Sensors not installed in 0 kg N plots (by design) |
| `LOI_OM_pct_6_18`, `_18_30` | NA for 2014 | Deeper depths only analyzed in 2015 |
| `NH4_N_ppm_6_18`, `_18_30` | NA for 2014 | Same as above |
| `NO3_N_ppm_6_18`, `_18_30` | NA for 2014 | Same as above |
| `TOC_pct_*` | NA for 2014 | TOC only analyzed in 2015 |
| `iwg_straw_yield` | 1 NA present | Missing harvest record (plot 1125, 2015) |
| `NO3_mean` and related | High BDL rate | See Lysimeter QA/QC section above |

---

## Data Source Files

| File | Content | Sheets | Notes |
|---|---|---|---|
| `Yield.xlsx` | Yield, height, lodging | Sheet1 | Definitive source for plot-treatment mapping and replicate structure; row 1 contains units |
| `Lysimeter.xlsx` | Raw lysimeter NO3 | 2014, 2015 | Lab analytical reports; 2014=Agvise, 2015=RAL-UMN; 2015 plot numbers are 3-digit (drop leading site digit) |
| `Moisture.xlsx` | Soil moisture time series | Moisture | 5,232 rows; sensors every 3–5 days; trt 21 absent by design |
| `Soils.xlsx` | Soil chemistry | Soils-2014, Soils-2015 | Different formats per year; 2015 has TOC and deeper depths |
| `combined_clean.csv` | Integrated dataset | — | 64 rows (32 plots × 2 years); primary analysis file |

### 2015 Lysimeter Plot Number Reconstruction
The 2015 lab report uses 3-digit plot codes. Full 4-digit plot numbers reconstructed as:
- Waseca plots: 1000 + 3-digit code (e.g., 105 → 1105)
- Lamberton plots: 2000 + 3-digit code (e.g., 106 → 2106)

Treatment assignment verified by cross-referencing treatment codes (I0, I60, I120, IL)
against Yield.xlsx: 32 of 32 plots verified with zero mismatches.

---

## File Structure

```
kernza_data_wrangle/
└── dw_kernza_project/
    ├── combined_clean.csv              ← primary analysis dataset (64 rows × 31 cols)
    ├── metadata_kernza_v2.md           ← this file
    ├── dw_kernza_project.Rproj
    ├── data/
    │   └── raw/
    │       ├── Yield.xlsx
    │       ├── Lysimeter.xlsx
    │       ├── Moisture.xlsx
    │       └── Soils.xlsx
    ├── scripts/
    │   └── lysimeter_sensitivity_analysis.R
    └── output/
        ├── figures/
        └── lysimeter_NO3_QC_analysis_v2.xlsx
```

---

## Abbreviations

| Abbreviation | Meaning |
|---|---|
| TLI | Thinopyrum intermedium (Kernza intermediate wheatgrass) |
| TLI-C2 | Improved grain-type IWG breeding population (The Land Institute) |
| IWG | Intermediate wheatgrass |
| leg | Legume (alfalfa, Medicago sativa) |
| VWC | Volumetric water content |
| NO3 | Nitrate |
| NH4 | Ammonium |
| OM | Organic matter |
| TOC | Total organic carbon |
| LOI | Loss on ignition (method for measuring OM) |
| ppm | Parts per million (mg kg⁻¹) |
| BDL | Below detection limit |
| RCBD | Randomized complete block design |
| AONR | Agronomically optimum nitrogen rate |
| CEC | Cation exchange capacity |
| GDD | Growing degree days |

---

## Key Analytical Decisions and Justifications

| Decision | Justification |
|---|---|
| BDL substitution = 0.05 mg/L | Half the detection limit; standard convention for censored environmental data; sensitivity analysis confirms conclusions unchanged across 0.025–0.075 range |
| BDL substituted before averaging | Substituting after averaging underestimates correction because zeros were already averaged with real values in original combined_clean.csv |
| Waseca data retained | Evidence confirms lysimeters functional; low NO3 reflects soil biology not equipment failure |
| Year treated as repeated measure | Same physical plots measured both years; Kernza is perennial — plots not replanted |
| Location as fixed effect | Only 2 locations — cannot be treated as random; treat as fixed factor in models |
| NO3_mean as primary leaching variable | Identical to NO3_half_mean; most interpretable as overall plot-year mean; sensitivity analysis confirms robustness |
| Moisture excluded from analyses involving trt 21 | Sensors not installed in 0 kg N plots; absence is by design, cannot substitute |
