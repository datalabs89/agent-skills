# REFEREE REPORT / PEER REVIEW REPORT

**Manuscript Title:** *Export Duties, Mineral Downstream Mandates, and Tariff Classification Arbitrage: Evidence from Indonesia’s Gold Export Levies*  
**Author:** Tedy Iskandar (Directorate General of Customs and Excise, Ministry of Finance of Indonesia)  
**Date of Review:** August 2026  
**Review Type:** Blind Peer Review / Academic Evaluation (Target: Field Top/Tier-1 Applied Economics / International Trade / Public Economics Journal, e.g., *Journal of International Economics*, *Journal of Public Economics*, *World Bank Economic Review*, or *Journal of Development Economics*)  
**Recommendation:** **Major Revision (R&R)**

---

## 1. Executive Summary & Overall Appraisal

This paper investigates the empirical impacts and behavioral evasion dynamics stemming from Indonesia’s gold export duty policy enacted under Minister of Finance Regulation (*Peraturan Menteri Keuangan / PMK*) No. 80/2025 (effective December 23, 2025). The regulation introduced a 10%–15% export duty on upstream raw gold (doré bars, granules under HS 7108 and HS 7115) while exempting downstream gold jewelry (HS 7113.19 at 0%). 

Using the universe of Indonesian Customs Export Declarations (BC 3.0) from January 2025 to August 2026 and adopting the state-of-the-art Local Projections Difference-in-Differences (LP-DiD) estimator developed by Dube, Girardi, Jordà, and Taylor (2025), the author documents two principal findings:
1. An immediate and persistent collapse in upstream raw gold exports ($\beta = -13.09$ log points in January 2026, persisting around $-10$ to $-11$ log points throughout 2026).
2. A substantial surge in nominally exempt gold jewelry exports (+2.75 log points in May 2026, +1.96 log points in June 2026), propelled by 43 new market entrants and major mining/trading exporters shifting 100% of their operational volume into jewelry classifications (aggregating >USD 128 million).

### Overall Assessment:
The paper addresses a highly important, timely, and policy-relevant research question at the intersection of international trade policy, mineral downstream mandates (*kebijakan hilirisasi*), and tax evasion/customs fraud. The use of administrative transaction-level customs data with firm identifiers (NPWP) and the adoption of modern LP-DiD methods provide a solid foundation.

However, in its current draft state, the manuscript resembles an extended working paper note rather than a fully developed journal article. There are several **critical methodological contradictions**, **pre-trend validation failures**, **missing price vs. volume decompositions**, and **unexploited forensic mechanisms** that must be rigorously addressed before the manuscript can meet the standards of a leading peer-reviewed journal.

---

## 2. Major Methodological & Econometric Comments

### 2.1. Critical Contradiction in Upstream Control Group Definition
- **The Issue:** In Section 2.1 (lines 25–26), the author states:
  > *"The regulation targeted raw gold, doré bars, and unrefined granules under HS code 7108.12.90 and unworked articles of precious metal under HS 7115.90.10, subjecting them to ad valorem export levies between 10% and 15%."*
  However, in Section 3.2 (line 35), the sample definition states:
  > *"Treated Group: 7 major mining producers under HS 7108.12.90 and Clean Control Group: 11 exporters under HS 7115.90.10."*
- **Why this is critical:** If HS 7115.90.10 was also subjected to the export levy under PMK 80/2025, it is **treated by the policy** and cannot serve as an uncontaminated control group. Using a treated commodity as a control introduces severe attenuation bias and violates the SUTVA (Stable Unit Treatment Value Assumption).
- **Required Remedy:** 
  1. Clarify whether HS 7115.90.10 was exempted, taxed at a different rate, or taxed identically.
  2. If taxed, replace the upstream control group with a truly unaffected precious/base metal category (e.g., refined silver bars HS 7106, copper cathodes HS 7403, or unexposed craft products) or use a synthetic control / cross-country synthetic control approach.

---

### 2.2. Failure of Parallel Pre-Trends in Upstream Regressions (Table 1)
- **The Issue:** In Section 4.1, the author reports dynamic LP-DiD estimates for upstream raw gold (Table 1). However, several pre-treatment coefficients are **statistically significant at the 5% level**:
  - Horizon $h = -10$ (Feb 2025): $\beta = -8.56$ ($p = 0.0179$)
  - Horizon $h = -9$ (Mar 2025): $\beta = -8.14$ ($p = 0.0197$)
  - Horizon $h = -6$ (Jun 2025): $\beta = -8.95$ ($p = 0.0397$)
  - Horizon $h = -2$ (Oct 2025): $\beta = -3.97$ ($p = 0.0383$)
- **Why this is critical:** While the post-treatment drop is large ($\beta = -13.09$), the presence of significant pre-treatment differences indicates that the parallel trends assumption is violated. The paper cannot claim causal identification under DiD if the treated group was already experiencing divergent trends before PMK 80/2025 was implemented.
- **Required Remedy:**
  - Investigate the cause of pre-policy volatility: Is it driven by anticipation effects (e.g., policy announcements, parliamentary debates), mining quota (*RKAB*) approvals, or seasonality?
  - Re-estimate the model controlling for firm-specific linear trends, or use an alternative matching/synthetic DiD estimator (e.g., Arkhangelsky et al., 2021).
  - Explicitly report an $F$-test / Wald test for joint pre-trend insignificance ($H_0: \beta_h = 0 \quad \forall h < -1$).

---

### 2.3. Handling of Zero Trade Flows and Coefficient Interpretation
- **The Issue:** Table 1 reports point estimates of $-13.09$ log points. In log-transformed linear specifications, $\Delta \log(Y) = -13.09$ implies a reduction of $1 - \exp(-13.09) \approx 99.9998\%$. 
- **Questions for the Author:**
  1. How were observations with zero export volume handled? Trade data at the firm-month or HS-month level frequently feature zeros. Did the author use $\log(Y + 1)$, $\text{arcsinh}(Y)$, or drop zeros?
  2. If zeros were dropped, this creates severe sample selection bias (intensive margin conditioning). If $\log(Y + 1)$ was used, the estimated coefficients are sensitive to scale and units of measurement.
- **Required Remedy:** 
  - Estimate a **Poisson Pseudo-Maximum Likelihood (PPML)** specification (Silva & Tenreyro, 2006; Correia, Guimarães, & Zylkin, 2020) adapted to local projections / DiD to handle zero trade flows naturally on the extensive margin without arbitrary transformations.
  - Decompose the response into:
    - **Extensive margin:** Probability of exporting ($\Pr(\text{Export} > 0)$ via Logit/LPM).
    - **Intensive margin:** Log trade value conditional on positive trade.

---

### 2.4. Price vs. Volume Decomposition and Global Commodity Trends
- **The Issue:** The period 2025–2026 coincided with historic global gold price fluctuations (spot gold reaching record highs on international exchanges like COMEX/LBMA). 
- **Risk:** If export values ($USD$) are used as the dependent variable, price movements could confound policy effects:
  - Did the jewelry surge represent physical volume shifting ($kg$) or higher export valuations due to rising global gold prices?
- **Required Remedy:**
  - Separately estimate LP-DiD models for:
    1. **Physical Quantity** (Net weight in kilograms).
    2. **FOB Value** (in USD).
    3. **Unit Value / Implicit Price** ($\text{USD}/\text{kg}$ or $\text{USD}/\text{gram}$).
  - Control for global gold/silver spot prices ($P_{t}^{\text{Gold}}$, $P_{t}^{\text{Silver}}$) interacting with product exposure.

---

### 2.5. Clustered Standard Errors and Inference
- **The Issue:** Section 3.1 states: *"All standard errors are estimated using Huber-White (HC1) heteroskedasticity-robust covariance estimators."*
- **Critique:** In panel trade regressions with repeated observations across time within firms/commodities, residual errors are heavily autocorrelated. Using HC1 robust standard errors without clustering dramatically inflates $t$-statistics and produces overly narrow confidence intervals (Bertrand, Duflo, & Mullainathan, 2004; Cameron & Miller, 2015).
- **Required Remedy:**
  - Cluster standard errors at the **firm level** (for firm-level panels) or at the **HS-8 digit commodity / exporter level**.
  - Show robustness using wild cluster bootstrap if the number of treated clusters in the upstream sample is small ($N=7$ treated mining producers).

---

## 3. Major Forensic & Mechanism Comments

### 3.1. Forensic Unit-Value Pricing Test (The Smoking Gun of Arbitrage)
The author provides an exciting narrative regarding PT Swarnim Murni Mulia shifting USD 128M into jewelry and 43 new entrants. To make this an unassailable academic contribution:
- **Unit Value Test:** Genuine gold jewelry carries substantial craftsmanship markups (artisanal value-add), resulting in a unit value ($\text{USD}/\text{gram}$) significantly above the raw gold spot price. In contrast, "cosmetic jewelry" (doré bars with attached clasps or minimally cast plates) will trade at near-zero markup (unit value $\approx$ LBMA spot gold price).
- **Action Item:** Plot the empirical distribution / kernel density of export unit values ($\text{USD}/\text{gram}$) for HS 7113.19:
  - Pre-policy period (Jan–Nov 2025) vs. Post-policy period (Dec 2025–Aug 2026).
  - Incumbent jewelry manufacturers vs. the 43 new entrants.
  - A clustering of unit values at exactly $1.00 \times \text{LBMA Spot Price}$ among new entrants would provide incontrovertible proof of tariff classification arbitrage.

### 3.2. Destination Market & Mirror Trade Statistics
- **Destination Breakdown:** Where did the reclassified HS 7113.19 jewelry go? Typical gold transit/refining hubs include Singapore, Hong Kong, UAE (Dubai), and Switzerland. Showing that exports shifted predominantly to major refining hubs rather than retail consumer markets (e.g., US, Europe, domestic retail) directly supports the trade arbitrage hypothesis.
- **Mirror Statistics:** Compare Indonesian export declarations (BC 3.0) with partner-country import records (e.g., Singapore Customs / UN Comtrade). If Indonesia records HS 7113.19 (jewelry) but the destination country records HS 7108 (bullion/doré), this provides definitive evidence of classification arbitrage.

---

## 4. Minor & Expositional Improvements

1. **Formal Econometric Equation Notation (Section 3.1):**
   - In Equation (1): $\Delta_h y_i = \alpha_h + \beta_h^{\text{LP-DiD}} D_i + \gamma_h' X_{i, t_0 - 1} + \varepsilon_i^h$
   - Clarify the unit of observation $i$ (is $i$ a firm, a firm-commodity pair, or a transaction?).
   - Include fixed effects explicitly (e.g., destination fixed effects $\delta_j$, firm fixed effects $\mu_i$).
2. **Table Documentation:**
   - Add sample size ($N$), number of distinct firms/clusters, and $R^2$ to Table 1 and Table 2.
3. **Institutional Background Expansion:**
   - Provide a brief timeline of Indonesia’s broader mineral export bans (Law No. 4/2009, Law No. 3/2020 on Mineral and Coal Mining / *UU Minerba*), nickel export bans, and domestic smelting mandates (*Hilirisasi*).
   - Explain why gold was subjected to an export levy (PMK 80/2025) instead of a direct export ban.
   - Detail the domestic refining infrastructure (e.g., PT Antam’s Logam Mulia refinery, PT Amman Mineral smelter, PT Freeport Indonesia Gresik smelter) and whether domestic refining capacity was sufficient to process all domestic doré.
4. **Distinction between Legal Tax Avoidance and Customs Fraud:**
   - Clearly delineate between *tariff engineering* (altering physical products legally to fit a lower tariff bracket) and *customs misclassification / fraudulent declaration* under Indonesian Customs Law (*UU No. 17/2006 tentang Kepabeanan*).

---

## 5. Summary of Required Action Items for Revision

| No. | Category | Required Modification |
| :--- | :--- | :--- |
| **1** | **Control Group** | Resolve the contradiction where HS 7115.90.10 is described as both taxed and the clean control. |
| **2** | **Pre-trends** | Address the significant pre-trends in Table 1 ($h=-10, -9, -6, -2$) with joint $F$-tests and trend adjustments. |
| **3** | **Zeroes & Model** | Re-estimate using PPML / extensive vs. intensive margin decomposition instead of plain log changes. |
| **4** | **Price vs Volume** | Decompose export values into physical kilograms ($kg$) and unit value ($\text{USD}/\text{gram}$) against LBMA spot price. |
| **5** | **Inference** | Replace HC1 standard errors with clustered standard errors at the firm/commodity level. |
| **6** | **Forensic Proof** | Add kernel density plots of unit values (Incumbents vs. 43 New Entrants) and destination hub analysis. |
| **7** | **Institutions** | Expand context on *Hilirisasi*, domestic smelting capacity, and legal definitions of classification arbitrage. |

---

## 6. Final Recommendation

**Decision:** **Major Revision**  
The draft paper has a compelling core empirical idea and access to extraordinary administrative data. If the author rigorously executes the econometrics corrections, addresses pre-trend validity, and adds the forensic unit-value tests, this paper will be a strong contender for publication in a leading international trade or public finance journal.
