Below is a consolidated Markdown document that captures the key designs, data structures, and methods from this thread, in a form you can store as a .md file in your repo or knowledge base.
Bihar Waste & Agro‑Residue System – Design & Modeling Notes
Last updated: 2026‑06‑10
1. Context & Objectives
Bihar’s waste and residue landscape is central to designing AGRICIRCLE/PIRV‑style circular bio‑economy infrastructure. The state’s waste sector emitted 8.2 MtCO₂e in 2020, primarily from domestic wastewater and unmanaged solid waste. At the same time, large agricultural residue and livestock waste streams create significant bioenergy and biochar potential.[[downtoearth.org](https://www.downtoearth.org.in/waste/bihar-to-strengthen-waste-management-profile-by-formulating-a-low-carbon-action-plan-94963)]
This document synthesises:
State‑level and district‑ready residue inventories.
Waste‑sector GHG trend and forecasting (2016–2026).
Bihar’s Renewable Energy Policy 2025 and biomass incentives.[[energetica-india](https://www.energetica-india.net/news/bihar-unveils-renewable-energy-policy-2025-targets-24-gw-of-re-and-6-1-gwh-of-ess-by-2030)]
Data models and SQL schemas for Postgres + Metabase.
Designs for interactive dashboards and a pellet plant siting simulator, including basic techno‑economics.
2. Bihar Waste & Residue Overview
2.1 Agricultural residues (state‑scale)
From Biobiz’s Bihar agro residues assessment:[[biobiz](https://biobiz.in/s/bring/in/reg/14/)]
CropResidue partsResidue (MT/year)Example key districts
Rice
Straw, husk
11.75
Rohtas, Aurangabad, East/West Champaran, Madhubani
Sugarcane
Trash, bagasse
4.3
Muzaffarpur, Samastipur, West/East Champaran, Sitamarhi
Wheat
Straw
1.9
Rohtas, Bhojpur, Buxar, Aurangabad, Patna
Maize
Cob, husk
0.75
Purnia, Katihar, Kishanganj, Araria, Khagaria
Total crop residues ~21–22 MT/year for these major crops.[[biobiz](https://biobiz.in/s/bring/in/reg/14/)]
A 2024 analysis on stubble burning reports:
Total crop residue in Bihar: 25.29 MT/year.
Of which 3.19 MT/year is burned in fields.[[sprf](https://sprf.in/wp-content/uploads/2024/12/Stubble-Burning-in-North-India.-Defogging-the-Facts.pdf)]
The National Biomass Atlas indicates Bihar’s surplus biomass residues as ~1.1–2.0 MT/year, which is the portion beyond fodder/soil needs and technically available for energy.[[nibe.res](https://nibe.res.in/english/biomass-atlas.php)]
2.2 Animal waste
Livestock population increased from 26.96 million (2003) to 36.45 million (2019).[[mpra.ub.uni-muenchen](https://mpra.ub.uni-muenchen.de/110630/1/MPRA_paper_110630.pdf)]
Using national dung generation (15 kg/animal/day; 1,655 MT dung/year nationally), Bihar’s dung output is ~30–35 MT/year.[[pib.gov](https://www.pib.gov.in/PressReleasePage.aspx?PRID=1697425)]
Poultry manure nationally ~12 MT/year; Bihar studies indicate constraints in scientific disposal (dumping, direct field application, burial).[[sscgj](https://sscgj.in/wp-content/uploads/2024/02/Rural_Solid-Waste-Management_Sector-Report.pdf)]
2.3 Municipal solid waste (MSW)
~2015–2019: 2,500–3,703 TPD statewide, ≈1.0–1.35 MT/year.[[cseindia](https://www.cseindia.org/centre-for-science-and-environment-urges-bihar-to-segregate-and-ramp-up-waste-collection-and-releases-book-on-solid-waste-management-at-patna--6717)]
2023: ~3,000 MT/day with 5% plastic share.[[vigyanvarta](https://vigyanvarta.in/adminpanel/upload_doc/VV_0524_20-.pdf)]
2024–25 Green Budget:
5,467 TPD collected, 1,385 TPD processed, remainder (~4,082 TPD) landfilled or dumped.[[state.bihar.gov](https://state.bihar.gov.in/cache/12/Budget/Budget/Green%20Budget%20Final%202024-25%20English%2022.02.pdf)]
Patna alone produces ~3,000 TPD MSW with 40–70% organics.[[nswai](https://nswai.org/docs/final%20swm%20in%20patna.pdf)]
2.4 Wastewater & emissions
ICLEI’s Low‑Carbon Action Plan (LCAP) and associated reports provide 2016–2020 GHG estimates for Bihar’s waste sector:[[bspcb.bihar.gov](https://bspcb.bihar.gov.in/Final%20report.pdf)]
Total waste‑sector emissions in 2020: 8.20 MtCO₂e.[[downtoearth.org](https://www.downtoearth.org.in/waste/bihar-to-strengthen-waste-management-profile-by-formulating-a-low-carbon-action-plan-94963)]
Sub‑sectors:
Domestic wastewater: 6.69 MtCO₂e (≈91% of waste‑sector emissions).[[circulars.iclei](https://circulars.iclei.org/wp-content/uploads/2024/05/Bihar-LCAP-Waste-Sector-Report_Combined_low-res.pdf)]
Industrial wastewater: ≈4–5% of cumulative waste‑sector emissions.[[ghgplatform-india](https://www.ghgplatform-india.org/wp-content/uploads/publications/phase-3/GHGPI-PhaseIII-Trend%20Analysis%20State-Bihar-Dec'19.pdf)]
Solid waste disposal & biological treatment: ≈4.6%.[[circulars.iclei](https://circulars.iclei.org/wp-content/uploads/2024/05/Bihar-LCAP-Waste-Sector-Report_Combined_low-res.pdf)]
2.5 Industrial & hazardous waste
144 hazardous‑waste generating units in Bihar.[[bhocmms.nic](https://bhocmms.nic.in/)]
57 grossly polluting industries along the Ganga within Bihar.[[nmcg.nic](https://nmcg.nic.in/writereaddata/fileupload/ngtmpr/0_Bihar%20MPR%20August%202020.pdf)]
Cross‑border industrial effluents arrive via the Sirsiya river from Nepal.[[india.mongabay](https://india.mongabay.com/2026/01/a-river-carries-industrial-waste-and-sewage-from-nepal-to-india/)]
2.6 Other residues
E‑waste: only 6 tonnes/year formally collected & processed in 2024–25, indicating a large informal stream.[[dataful](https://dataful.in/datasets/19388/)]
C&D waste: Bihar present in MoHUA/Dataful C&D dataset; national scale 150–500 MT/year.[[dataful](https://dataful.in/datasets/19394/)]
Market waste: typical large mandis ~10 TPD vegetable waste; replicated across Bihar’s major markets.[[sbmurban](https://sbmurban.org/vegetable-waste-packs-power-punch)]
3. Unified Data Model & CSV
3.1 Core schema
The unified CSV (bihar_waste_streams_biochar_enhanced.csv) has columns:
Identification:
stream_group – Agriculture, Municipal, Industrial, Non‑agricultural.
stream_type – Crop residue, Animal waste, MSW, Domestic wastewater, Industrial wastewater, Hazardous waste, E-waste, C&D waste, Market waste.
subcategory – e.g., “Rice straw + husk”, “Patna city MSW”, “Hazardous waste‑generating units”.
state, district, year.
Quantities:
quantity_value, quantity_unit (MT/year, tons/day, MtCO2e/year, units).
Fates:
fate_primary, fate_secondary.
Energy & carbon:
LHV_MJ_per_kg, C_fraction, energy_potential_MJ, carbon_mass_t.
Biochar metrics:
biochar_yield_fraction (t biochar / t feedstock).
biochar_C_fraction (C fraction of biochar).
tCO2e_durable_per_t_feedstock (durable CDR per t feedstock).
Source traceability:
source_note, source_id (e.g., web:27), source_url.[[indiagarbagecase](https://indiagarbagecase.in/wp-content/uploads/2019/04/BIHAR-2015.01.29.pdf)]
3.2 Default factors
By stream_type:
Crop residue: LHV_MJ_per_kg = 14.0, C_fraction = 0.45, biochar_yield_fraction = 0.30, biochar_C_fraction = 0.7, tCO2e_durable_per_t_feedstock ≈ 0.77.[[cseindia](https://www.cseindia.org/content/downloadreports/10421)]
Animal waste: LHV = 8.0, C_fraction = 0.35, biochar_yield_fraction = 0.35, biochar_C_fraction = 0.6, tCO2e_durable_per_t_feedstock ≈ 0.77.[[sscgj](https://sscgj.in/wp-content/uploads/2024/02/Rural_Solid-Waste-Management_Sector-Report.pdf)]
MSW: LHV = 6.0, C_fraction = 0.3, biochar_yield_fraction = 0.25, biochar_C_fraction = 0.6, tCO2e_durable_per_t_feedstock ≈ 0.6.[[niua](https://niua.in/blogs/india-fourth-biennial-update-report-bur-4-focus-ghg-emissions-solid-waste-management)]
Market waste similar to MSW (organics‑heavy).
4. District‑wise Agro‑Residue Dashboard
4.1 Inputs
Use:
District‑wise crop production data from Bihar e‑Statistics.[[planningonline.bihar.gov](https://planningonline.bihar.gov.in/EStatistics/Dashboard.aspx)]
“District‑wise Cropping Pattern of Bihar” dataset (rice, wheat, maize, pulses, sugarcane, oilseeds, jute).[[data.mendeley](https://data.mendeley.com/datasets/t7hx4gz5bw/1)]
RPRs and surplus fractions from biomass literature and National Biomass Atlas technical notes.[[plantarchives](https://www.plantarchives.org/article/21-%20Indian%20Scenario%20of%20Biomass%20Availability%20and%20its%20Bioenergy%20Conversion%20121-126%20(Sp-09).pdf)]
4.2 Calculations per district × crop × year
Given:
production_tonnes[d,c,t].
RPR[c].
surplus_fraction[c,r] (by crop and region).
Compute:
residue_tonnes[d,c,t] = production_tonnes × RPR.
surplus_residue_tonnes[d,c,t] = residue_tonnes × surplus_fraction.
Energy and CDR:
energy_MJ = surplus_residue_tonnes × 1000 × 14 (for crop residues).[[cseindia](https://www.cseindia.org/content/downloadreports/10421)]
CDR_durable_tCO2e = surplus_residue_tonnes × tCO2e_durable_per_t_feedstock (≈0.77).
4.3 Dashboard features
Filters: district, crop, year, surplus threshold.
Choropleth map: surplus residues (per crop or total) by district.
Ranking tables: Top surplus districts and clusters.
Cluster identification: group neighbouring high‑surplus districts for plant siting.
5. Waste‑Sector GHG Forecast (2016–2026)
5.1 Base data 2016–2020 (ICLEI LCAP)
Waste‑sector emissions (solid waste + domestic & industrial wastewater) 2016–2020.[[southasia.iclei](https://southasia.iclei.org/news/low-carbon-action-plan-for-bihars-waste-sector-will-support-emission-reduction-strategies/)]
2020 total: 8.20 MtCO₂e.[[bspcb.bihar.gov](https://bspcb.bihar.gov.in/Final%20report.pdf)]
Domestic wastewater: 6.69 MtCO₂e in 2020, CAGR 2.6% from 2016.[[downtoearth.org](https://www.downtoearth.org.in/waste/bihar-to-strengthen-waste-management-profile-by-formulating-a-low-carbon-action-plan-94963)]
Industrial wastewater and solid‑waste disposal ~4–5% each of cumulative emissions.[[ghgplatform-india](https://www.ghgplatform-india.org/wp-content/uploads/publications/phase-3/GHGPI-PhaseIII-Trend%20Analysis%20State-Bihar-Dec'19.pdf)]
5.2 Forecast to 2026
Domestic wastewater:
Edw,t=6.69×(1.026)(t−2020) MtCO₂e,  t=2021–2026.E_{\text{dw},t} = 6.69 × (1.026)^{(t-2020)} \text{ MtCO₂e},\; t=2021–2026.Edw,t​=6.69×(1.026)(t−2020) MtCO₂e,t=2021–2026.
Industrial wastewater: apply CAGR ~5–6% inferred from LCAP trend charts.[[circulars.iclei](https://circulars.iclei.org/wp-content/uploads/2024/05/Bihar-LCAP-Waste-Sector-Report_Combined_low-res.pdf)]
Solid waste: scale with growth in MSW generation (NGT/CSE/Green Budget data).[[cseindia](https://www.cseindia.org/centre-for-science-and-environment-urges-bihar-to-segregate-and-ramp-up-waste-collection-and-releases-book-on-solid-waste-management-at-patna--6717)]
Residue burning: assume 3.19 MT burned/year and ~1.4 tCO₂ per tonne residue burned.[[sprf](https://sprf.in/wp-content/uploads/2024/12/Stubble-Burning-in-North-India.-Defogging-the-Facts.pdf)]
5.3 Scenario analysis
BAU, LCAP (using ICLEI’s reduction factors), and a Bioenergy uplift scenario (additional reductions from biomass/WtE projects).
Plot emissions by sub‑sector vs year and overlay RE capacity build‑out.
6. Renewable Energy Policy 2025 & Biomass Incentives
6.1 RE Policy 2025 (Bihar)
Key points:[[appartners](https://www.appartners.in/insights/highlights-of-bihars-new-renewable-energy-policy-2025-romit-dey/)]
Target: 23.97 GW RE and 6.1 GWh storage by 2029–30.[[impactpolicies](https://impactpolicies.org/news/717/bihars-renewable-revolution-policy-meets-progress)]
Eligible technologies: solar, wind, biomass & waste‑to‑energy, hydro, green hydrogen, etc.[[energetica-india](https://www.energetica-india.net/news/bihar-unveils-renewable-energy-policy-2025-targets-24-gw-of-re-and-6-1-gwh-of-ess-by-2030)]
Major incentives:
100% electricity duty exemption for 15 years.[[youtube](https://www.youtube.com/watch?v=e4By6NsVTsQ)][[energetica-india](https://www.energetica-india.net/news/bihar-unveils-renewable-energy-policy-2025-targets-24-gw-of-re-and-6-1-gwh-of-ess-by-2030)]
100% SGST reimbursement on RE project inputs for 5 years.[[energetica-india](https://www.energetica-india.net/news/bihar-unveils-renewable-energy-policy-2025-targets-24-gw-of-re-and-6-1-gwh-of-ess-by-2030)]
100% reimbursement of stamp duty & registration fee.[[appartners](https://www.appartners.in/insights/highlights-of-bihars-new-renewable-energy-policy-2025-romit-dey/)]
100% reimbursement of land conversion fees.[[youtube](https://www.youtube.com/watch?v=e4By6NsVTsQ)][[energetica-india](https://www.energetica-india.net/news/bihar-unveils-renewable-energy-policy-2025-targets-24-gw-of-re-and-6-1-gwh-of-ess-by-2030)]
100% exemption on transmission & wheeling charges for 15 years (20 years with storage).[[appartners](https://www.appartners.in/insights/highlights-of-bihars-new-renewable-energy-policy-2025-romit-dey/)]
25‑year open access, must‑run status, energy banking, carbon credit retention.[[impactpolicies](https://impactpolicies.org/news/717/bihars-renewable-revolution-policy-meets-progress)]
6.2 MNRE Biomass Programme
CFA for pellet/briquette plants: ₹9 lakh per MTPH, capped at ₹45 lakh.[[mnre.gov](https://mnre.gov.in/en/bio-mass/)]
CFA for non‑bagasse biomass cogeneration: ₹40 lakh/MW, capped at ₹5 crore.[[mnre.gov](https://mnre.gov.in/en/bio-mass/)]
These combine with state incentives to significantly improve bioenergy project economics.
7. Postgres Schema for Bihar Waste, Biomass & RE
7.1 Dimension tables
sql
CREATE TABLE dim_district (
  district_id SERIAL PRIMARY KEY,
  district_name TEXT UNIQUE NOT NULL,
  state_name TEXT NOT NULL DEFAULT 'Bihar'
);

CREATE TABLE dim_year (
  year_id SERIAL PRIMARY KEY,
  year INT UNIQUE NOT NULL
);

CREATE TABLE dim_stream_type (
  stream_type_id SERIAL PRIMARY KEY,
  stream_group TEXT,
  stream_type TEXT
);

CREATE TABLE dim_crop (
  crop_id SERIAL PRIMARY KEY,
  crop_name TEXT UNIQUE NOT NULL,
  default_rpr NUMERIC,
  default_surplus_fraction NUMERIC
);

CREATE TABLE dim_tech (
  tech_id SERIAL PRIMARY KEY,
  tech_name TEXT,
  category TEXT
);

CREATE TABLE dim_policy (
  policy_id SERIAL PRIMARY KEY,
  policy_name TEXT,
  start_year INT,
  end_year INT,
  electricity_duty_exemption BOOLEAN,
  sgst_reimbursement BOOLEAN,
  stamp_duty_exemption BOOLEAN,
  land_conversion_fee_exemption BOOLEAN,
  transmission_wheeling_exemption BOOLEAN,
  transmission_exemption_years INT,
  notes TEXT
);
7.2 Fact tables
Biomass / residues
sql
CREATE TABLE fact_biomass_residue (
  id BIGSERIAL PRIMARY KEY,
  district_id INT REFERENCES dim_district,
  year_id INT REFERENCES dim_year,
  crop_name TEXT,
  stream_type_id INT REFERENCES dim_stream_type,

  production_tonnes NUMERIC,
  residue_tonnes NUMERIC,
  surplus_residue_tonnes NUMERIC,

  lhv_mj_per_kg NUMERIC,
  energy_mj NUMERIC,
  c_fraction NUMERIC,
  carbon_mass_t NUMERIC,

  biochar_yield_fraction NUMERIC,
  biochar_c_fraction NUMERIC,
  tco2e_durable_per_t_feedstock NUMERIC,

  source_id TEXT,
  source_url TEXT
);
Waste‑sector GHG
sql
CREATE TABLE fact_waste_ghg (
  id BIGSERIAL PRIMARY KEY,
  year_id INT REFERENCES dim_year,
  sub_sector TEXT,      -- 'solid_waste','domestic_ww','industrial_ww','residue_burning'
  scenario TEXT,        -- 'BAU','LCAP','RE_plus_bioenergy'
  emissions_mtco2e NUMERIC,
  source_id TEXT,
  source_url TEXT
);
Feedstock costs
sql
CREATE TABLE fact_feedstock_cost (
  id BIGSERIAL PRIMARY KEY,
  district_id INT REFERENCES dim_district,
  crop_name TEXT,
  year_id INT REFERENCES dim_year,

  surplus_residue_tonnes NUMERIC,
  farmgate_price_rs_per_t NUMERIC,
  collection_cost_rs_per_t NUMERIC,
  transport_cost_rs_per_t NUMERIC,
  avg_transport_distance_km NUMERIC,

  source_id TEXT,
  source_url TEXT
);
RE projects
sql
CREATE TABLE fact_re_projects (
  id BIGSERIAL PRIMARY KEY,
  district_id INT REFERENCES dim_district,
  year_id INT REFERENCES dim_year,
  tech_id INT REFERENCES dim_tech,

  capacity_mw NUMERIC,
  generation_gwh NUMERIC,
  status TEXT,
  scheme TEXT,
  policy_id INT REFERENCES dim_policy,
  policy_incentives JSONB,

  estimated_ghg_reduction_mtco2e NUMERIC,

  source_id TEXT,
  source_url TEXT
);
8. Pellet Plant Siting & ROI + GHG Calculator (Metabase)
8.1 Inputs
Metabase parameters:
District (district_id)
Year (year)
Plant capacity (capacity_tph)
Operating hours (hours_per_year)
Pellet price (pellet_price_rs_per_t)
Gross capex (capex_gross_rs)
Burn fraction (fraction of feedstock that would otherwise be burned; burn_fraction)
Policy (policy_id, e.g., RE 2025 vs none)
8.2 Core SQL model (simplified)
A single query to return delivered cost, policy‑adjusted capex/ROI basics, and GHG impact:
sql
WITH
params AS (
  SELECT
    {{capacity_tph}}::NUMERIC        AS capacity_tph,
    {{hours_per_year}}::NUMERIC      AS hours_per_year,
    {{pellet_price_rs_per_t}}::NUMERIC AS pellet_price_rs_per_t,
    {{capex_gross_rs}}::NUMERIC      AS capex_gross_rs,
    {{burn_fraction}}::NUMERIC       AS burn_fraction
),

feedstock AS (
  SELECT
    (f.farmgate_price_rs_per_t
     + f.collection_cost_rs_per_t
     + f.transport_cost_rs_per_t) AS delivered_cost_rs_per_t
  FROM fact_feedstock_cost f
  JOIN dim_year y ON y.year_id = f.year_id
  WHERE f.district_id = {{district_id}}
    AND y.year = {{year}}
  LIMIT 1
),

policy AS (
  SELECT
    electricity_duty_exemption,
    sgst_reimbursement,
    stamp_duty_exemption,
    land_conversion_fee_exemption,
    transmission_wheeling_exemption
  FROM dim_policy
  WHERE policy_id = {{policy_id}}
),

capex_net AS (
  SELECT
    p.capex_gross_rs,
    p.capacity_tph,
    LEAST(900000 * p.capacity_tph, 4500000) AS mnre_cfa_rs
  FROM params p
),

financials AS (
  SELECT
    c.capex_gross_rs,
    c.mnre_cfa_rs,
    (c.capex_gross_rs - c.mnre_cfa_rs) AS capex_net_rs,
    p.hours_per_year,
    p.capacity_tph,
    f.delivered_cost_rs_per_t,
    p.pellet_price_rs_per_t
  FROM capex_net c
  JOIN params p ON TRUE
  JOIN feedstock f ON TRUE
),

plant_annual AS (
  SELECT
    capex_net_rs,
    capacity_tph,
    hours_per_year,
    delivered_cost_rs_per_t,
    pellet_price_rs_per_t,
    (capacity_tph * hours_per_year) AS annual_output_t,
    (capacity_tph * hours_per_year) * delivered_cost_rs_per_t AS annual_feedstock_cost_rs,
    2000000::NUMERIC AS annual_other_opex_rs
  FROM financials
),

residue_factors AS (
  SELECT
    COALESCE(AVG(tco2e_durable_per_t_feedstock), 0.77) AS tco2e_durable_per_t,
    1.4::NUMERIC AS tco2e_avoided_burning_per_t
  FROM fact_biomass_residue
  WHERE stream_type_id = (
    SELECT stream_type_id FROM dim_stream_type
    WHERE stream_type = 'Crop residue'
    LIMIT 1
  )
),

ghg AS (
  SELECT
    p.annual_output_t AS annual_feedstock_t,
    rf.tco2e_durable_per_t,
    rf.tco2e_avoided_burning_per_t,
    {{burn_fraction}}::NUMERIC AS burn_fraction,
    (p.annual_output_t * rf.tco2e_durable_per_t) AS cdr_durable_mtco2e,
    (p.annual_output_t * {{burn_fraction}}::NUMERIC * rf.tco2e_avoided_burning_per_t) AS avoided_burning_mtco2e
  FROM plant_annual p
  JOIN residue_factors rf ON TRUE
)

SELECT
  pa.delivered_cost_rs_per_t,
  pa.capex_net_rs,
  pa.annual_output_t,
  pa.annual_feedstock_cost_rs,
  pa.annual_other_opex_rs,
  (pa.annual_output_t * pa.pellet_price_rs_per_t) AS annual_revenue_rs,
  ((pa.annual_output_t * pa.pellet_price_rs_per_t)
   - pa.annual_feedstock_cost_rs
   - pa.annual_other_opex_rs) AS annual_cashflow_rs,
  g.cdr_durable_mtco2e,
  g.avoided_burning_mtco2e,
  (g.cdr_durable_mtco2e + g.avoided_burning_mtco2e) AS total_ghg_impact_mtco2e
FROM plant_annual pa
JOIN ghg g ON TRUE;
This returns:
Delivered feedstock cost (Rs/t).
Capex net of MNRE CFA (and easily extendable with RE 2025 land/levy waivers).
Annual output, revenues, and cashflow.
Durable CDR, avoided burning emissions, and total GHG impact.
This Markdown file should give you a coherent, code‑ready representation of what we designed in the thread, ready to drop into a repo as the “Bihar waste & bioenergy design spec v1”.
