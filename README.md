# brazil_austrlia_trade

Bilateral trade between **Brazil and Australia in 2025**, read straight from Brazilian
customs records and turned into self-contained HTML dashboards.

The headline: in 2025 Brazil ran a **~US$261M trade deficit** with Australia — it shipped
out **US$777.4M** (mostly manufactured goods and green coffee) and took back **US$1,038.2M**
(mostly Australian coking coal feeding Brazilian steelmaking).

| Direction | 2025 FOB value | Leading cargo |
|-----------|---------------:|---------------|
| Brazil → Australia (exports) | **$777.4M** | Green coffee, heavy machinery, transport equipment |
| Australia → Brazil (imports) | **$1,038.2M** | Coking coal & coke (~$771M), medical devices, beef |
| **Trade balance** | **−$260.8M** | Deficit for Brazil |
| Total turnover | $1.82B | — |

---

## Dashboards

Both are single-file HTML dashboards (Chart.js via CDN) — open in any browser, no build step.

### `aussie_br_dashboard_v2.html` — current
Bidirectional trade ledger, in **English**. Shows both flows side by side across five sections:

1. **The two lanes** — monthly exports vs imports, plus a monthly surplus/deficit chart.
2. **What crosses each way** — export and import mix by ISIC industry section.
3. **Manifest — top cargo** — ranked top-10 products in each direction.
4. **Logistics & ballast** — transport mode, freight cost, and value-per-kg asymmetry
   (Australia ships ~26× the tonnage; Brazil's cargo carries ~19× the value per kg).
5. **Brazilian ports of call** — origin states for exports, destination states for imports.

### `aussie_br_dashboard.html` — v1 (legacy)
Original single-direction view (Australia → Brazil imports only), in Portuguese —
kept for reference.

---

## Dataset

**`BRL_AUD_IMPORT_EXPORT_DATA.xlsx`** — 17,590 line items, all of 2025, Australia only
(country code `69`). Source: **Comex Stat** (SECEX / Ministério do Desenvolvimento,
Indústria, Comércio e Serviços).

Key columns:

| Column | Meaning |
|--------|---------|
| `CO_ANO`, `CO_MES` | Year, month |
| `TIPO` | `EXPORT` (BR→AU) or `IMPORT` (AU→BR) |
| `CO_NCM`, `NO_NCM_POR` | Product code and description (Portuguese) |
| `VL_FOB` | FOB value in current USD |
| `KG_LIQUIDO`, `QT_ESTAT` | Net weight (kg) and statistical quantity |
| `VL_FRETE`, `VL_SEGURO` | Freight and insurance (import/CIF side only) |
| `CO_VIA` | Transport mode (`1` = sea, `4` = air, …) |
| `SG_UF_NCM` | Brazilian state of origin/destination |
| `NO_ISIC_*_ING` | ISIC industry classification (English) |

**Notes**
- All values are **FOB in current US dollars**.
- Product labels in the v2 dashboard are translated from the official NCM descriptions.
- Freight and insurance are recorded on the **import (CIF) side only** — Brazil reports
  exports FOB, so outbound freight is not in the dataset.

---

## Data source

Comex Stat — <https://comexstat.mdic.gov.br/>
