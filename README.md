# Climate Agreements Simulation

An interactive, browser-based tool for simulating international climate negotiations. Designed for classroom exercises where student teams represent different country groups and negotiate emission reduction commitments and financial transfers.

**Live tool:** Hosted via GitHub Pages at [www.andrewrwaxman.com/climate-agreements-sim-expo/](https://www.andrewrwaxman.com/climate-agreements-sim-expo/)

## Original Author

Jacob Bradt (jacob.bradt@mccombs.utexas.edu)
_Modified by_ Andrew Waxman (awaxman@utexas.edu)

# Climate Agreements Simulation

An interactive, browser-based tool for simulating international climate negotiations. Designed for classroom exercises where students represent individual country delegations and negotiate emission reduction commitments and financial transfers.

**Live tool:** [andrewrwaxman.com/climate-agreements-sim-expo](https://www.andrewrwaxman.com/climate-agreements-sim-expo/)

This version is adapted from Jacob Bradt's original tool for PA 388K/345 Climate Policy, LBJ School of Public Affairs, UT Austin. The original tool is available at [jtbradt.github.io/climate-agreements-sim-expo](https://jtbradt.github.io/climate-agreements-sim-expo/).

---

## Overview

Students set three policy parameters for each of eleven individual country delegations:

1. **Emission reduction start year** (2025–2100)
2. **Annual emission reduction rate** (0–20%)
3. **Net financial transfer** ($B/yr; negative = receiving, positive = paying)

The tool instantly computes and visualizes:
- GHG emission pathways under business-as-usual and negotiated policies
- Global temperature change relative to pre-industrial levels
- Country-specific climate damages (% change in per capita GDP)
- Cumulative abatement costs by country

The United States is not a negotiating party. Its emissions are included in the model as an exogenous background trajectory, controlled by the instructor through a separate shock panel (see Instructor Features below).

---

## Country Delegations

All economic values are in **2024 current (nominal) US dollars**. Base year for all projections is **2024**.

| Country | Group | Pop (M) | GDP/cap ($) | Baseline Temp (°C) | Tconv | Emissions (Gt) | BAU Growth |
|---|---|---|---|---|---|---|---|
| Japan | High Emitters | 124 | 33,138 | 13.99 | 1.170 | 1.05 | −2.5%/yr |
| European Union | High Emitters | 450 | 38,290 | 10.85 | 1.184 | 3.20 | −2.0%/yr |
| Brazil | Emerging Major Emitters | 215 | 10,294 | 22.22 | 1.071 | 1.28 | +0.3%/yr |
| China | Emerging Major Emitters | 1,409 | 13,437 | 14.21 | 1.286 | 15.63 | +0.5%/yr |
| India | Emerging Major Emitters | 1,441 | 2,731 | 25.65 | 1.143 | 4.57 | +3.0%/yr |
| Nigeria | Fossil Fuel Exporters | 224 | 1,596 | 26.84 | 1.109 | 0.27 | +2.5%/yr |
| Norway | Fossil Fuel Exporters | 5.5 | 89,202 | 4.83 | 1.192 | 0.049 | −1.5%/yr |
| Fiji | Climate-Vulnerable States | 0.93 | 5,740 | 23.80 | 0.733 | 0.0022 | +1.0%/yr |
| Marshall Islands | Climate-Vulnerable States | 0.042 | 4,400 | 27.50 | 0.814 | 0.00016 | +0.5%/yr |
| Vietnam | Other Developing | 98 | 4,163 | 24.82 | 1.021 | 0.48 | +4.5%/yr |
| Mexico | Other Developing | 130 | 11,265 | 18.84 | 1.175 | 0.65 | +0.5%/yr |

The eleven countries collectively represent approximately 33 Gt CO₂e (62% of global 2024 emissions of 53.2 Gt). The United States (5.9 Gt) is included as an exogenous background emitter, bringing tool coverage to ~73%.

Marshall Islands baseline temperature is a geographic estimate; it is not present in the Burke et al. dataset.

---

## Instructor Features

### U.S. Exogenous Shock Panel

A collapsible red panel (collapsed by default, not visible to students in normal use) allows the instructor to announce a U.S. policy action between negotiation rounds and update the model immediately. Three modes:

- **BAU (default):** U.S. follows current trajectory (−0.5%/yr, reflecting market-driven decarbonization)
- **Shock A — Re-entry:** New administration announces rejoining UNFCCC + net-zero by 2050 pledge. Cuts begin 2028 at 9.3%/yr. Expected temperature impact: approximately −0.12°C versus BAU.
- **Shock B — Oil Expansion:** U.S. lifts sanctions, expands fossil fuel production (+1.2%/yr). Expected temperature impact: approximately +0.15°C versus BAU.

The U.S. emissions line appears on the emissions chart as a dashed grey line in all modes, making the U.S. background trajectory visible to students without giving them control over it.

### Emissions Leverage Table

A collapsible blue panel provides an instructor-controlled leverage table showing each country's emissions and maximum temperature leverage (the °C reduction achievable if that country cuts aggressively from 2025 at 10%/yr, holding all others at BAU). Three reveal states:

- **Show Emissions Only** — for use after Round 1 model reveal
- **Reveal Full Leverage** — adds the °C column, for use in debrief
- **Add Rest-of-World** — displays a panel showing Russia (~2.8 Gt), Indonesia (~2.5 Gt), Saudi Arabia (~0.9 Gt), and Canada (~0.8 Gt) at BAU, for the final debrief reveal of non-participant emissions impact

### Timer

Preset buttons: 5m / 8m / 12m / 15m. Custom input also available. Audio chime on expiry.

---

## Data Sources

### GDP and Population

**Source:** World Bank World Development Indicators (WDI), 2024.

- **GDP per capita:** Indicator `NY.GDP.PCAP.CD`, 2024 current US dollars. EU uses World Bank EU-27 aggregate (`EUU`).
- **Population:** Indicator `SP.POP.TOTL`, 2024.
- **GDP growth rates:** Calibrated long-run assumptions informed by IMF World Economic Outlook projections and OECD long-term baseline scenarios.

### Baseline Temperature and Temperature Conversion Factors

**Source:** Burke, Hsiang & Miguel (2015) replication package.

> Burke, M., Hsiang, S. M., & Miguel, E. (2015). Global non-linear effect of temperature on economic production. *Nature*, 527(7577), 235–239.

- **Population-weighted mean temperature** — From `UDel_temp_popweight` in `GrowthClimateDataset.csv`, averaged over 1980–2010.
- **Temperature conversion factors (Tconv)** — From `CountryTempChange_RCP85.csv`. Derived from CMIP5 RCP8.5 multi-model ensemble mean. Translates global mean temperature change into country-specific local warming. EU value is a population-weighted average of DE, FR, IT, ES, PL, NL, BE, SE.
- **Damage function coefficients** — Pooled regression (no lags): `growth_effect(T) = 0.0127×T − 0.0005×T²`.

### Emissions Data

**Source:** EDGAR 2025 Report (European Commission Joint Research Centre); IEA Global Energy Review 2025; Climate Action Tracker country assessments.

All emissions are total GHG in **Gt CO₂e/year**, 2024 data. BAU growth rates are calibrated assumptions reflecting current-policy trajectories, informed by EDGAR 2025 trend data and Climate Action Tracker current-policy scenarios.

### Atmospheric CO₂ Concentration

- **Base (2024):** 427.0 ppm, NOAA Global Monitoring Laboratory.
- **Pre-industrial:** 297.06 ppm, Burke et al. (2015).
- **Emissions-to-concentration:** OLS regression on 2000–2024 historical data: `ΔCO₂ = 0.9893 + 0.0245 × total_emissions`. Applied iteratively from 2024 base.

---

## Methodology

### Emission Pathways

Business-as-usual:
```
emissions_BAU(t) = emissions_0 × (1 + g)^(t − 2024)
```

Under reduction policy starting at `reduction_year` with annual rate `r`:
```
emissions(t) = emissions_BAU(reduction_year) × (1 − r)^(t − reduction_year + 1)
```

### Temperature

Global CO₂ concentration accumulated from total emissions across all eleven countries plus U.S. exogenous trajectory. Global mean temperature anomaly:
```
T_global = λ × log₂(CO₂ / CO₂_preindustrial)
```
where `λ = 2.367` (climate sensitivity) and `CO₂_preindustrial = 297.06 ppm`.

### Country-Specific Warming

```
T_local(t) = T_base + (T_global(t) − T_global(2024)) × Tconv
```

### Climate Damages

Burke et al. (2015) quadratic damage function:
```
damage(T) = 0.0127 × T − 0.0005 × T²
```
Peaks at approximately 13°C. Local temperature capped at 30°C following Burke et al. Annual GDP growth under climate change:
```
g_CC(t) = g_base + [damage(T_local(t)) − damage(T_base)]
```

### Abatement Costs

Marginal abatement costs follow a quadratic schedule:
```
MAC(t) = c₁ × A(t) + c₂ × A(t)²
```
where `A(t) = 1 − (1−r)^(years_since_start)` is cumulative abatement fraction.

| Country | c₁ | c₂ |
|---|---|---|
| Japan | 220 | 55 |
| European Union | 200 | 50 |
| Brazil | 80 | 18 |
| China | 100 | 25 |
| India | 80 | 20 |
| Nigeria | 120 | 30 |
| Norway | 150 | 40 |
| Fiji | 60 | 12 |
| Marshall Islands | 70 | 15 |
| Vietnam | 85 | 18 |
| Mexico | 90 | 22 |

These are pedagogical calibrations informed by income level and energy mix, not empirical marginal abatement cost curves.

### Discounting

All NPV calculations use a **3% annual discount rate**, consistent with the US government's central rate for regulatory cost-benefit analysis. The Burke et al. damage function applies to GDP *growth rates*, causing damages to compound over time; discounting substantially reduces cumulative figures but magnitudes remain significant for hot, populous countries.

### Financial Transfers

Each country sets a net annual transfer in $B/yr. The tool displays a running net transfer balance — proposals cannot be entered into the model while the balance is non-zero, enforcing the constraint that transfers must sum to zero across all parties.

### Financial Summary

Two views:

1. **Default** (visible during negotiation): NPV abatement costs, cumulative transfers, and climate damages as % GDP/cap in 2100. The unit mismatch between dollar costs and percentage damages is intentional — it prevents students from trivially computing net benefits during negotiation.

2. **Detailed Breakdown** (instructor toggle): Reveals NPV avoided damages in $B and net benefit (avoided damages − abatement cost − transfers). Designed for post-exercise debrief.

---

## Technical Details

The simulation runs entirely client-side as a single HTML file with no server dependencies. The only external resource is Chart.js, loaded from CDN.

- **Framework:** Vanilla HTML/CSS/JavaScript
- **Charting:** Chart.js v4.4.7
- **Deployment:** GitHub Pages (static hosting)
- **Performance:** All computations complete in <1ms; chart updates are instantaneous on slider interaction

---

## Adaptation Notes

This version modifies Bradt's original in the following ways:

- Six country groups replaced with eleven individual country delegations
- United States removed as a negotiating party; added as instructor-controlled exogenous shock panel with three scenarios (BAU, Re-entry, Oil Expansion)
- Country parameters recalibrated from primary sources (World Bank WDI 2024, EDGAR 2025, Burke et al. replication package extracted directly)
- Instructor leverage table added with three-stage reveal sequence for classroom debrief
- Timer presets updated to 5m/8m/12m/15m
- Header updated to COP31/PA 388K/345 context

---

## References

- Burke, M., Hsiang, S. M., & Miguel, E. (2015). Global non-linear effect of temperature on economic production. *Nature*, 527(7577), 235–239.
- EDGAR (2025). *GHG Emissions of All World Countries*. European Commission, Joint Research Centre.
- IEA (2025). *Global Energy Review: CO₂ Emissions*.
- Climate Action Tracker (2025). Country assessments. https://climateactiontracker.org/
- World Bank (2025). World Development Indicators. https://data.worldbank.org/
- NOAA Global Monitoring Laboratory (2025). Trends in Atmospheric Carbon Dioxide. https://gml.noaa.gov/ccgg/trends/
- Bradt, J. Original climate-agreements-sim-expo. https://github.com/jtbradt/climate-agreements-sim-expo
 
