# Data Dictionary — Munich Spatial Property Insights

**Dataset:** `munich_property_500_clean.csv`  
**Records:** 500 mock residential properties across 20 Munich districts  
**Generated:** June 2026 | **Use:** Power BI portfolio project

---

## Identity & Classification

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `property_id` | String | Unique property identifier. Format: MUC-{number} | `MUC-1042` |
| `district` | String | Munich administrative district name | `Schwabing-West` |
| `zone` | String | Broad location zone. Values: `city_center`, `inner_ring`, `outer_ring`, `suburbs` | `inner_ring` |
| `price_tier` | String | Market segment. Values: `ultra`, `luxury`, `premium`, `mid`, `entry` | `premium` |
| `property_type` | String | Type of residential property. Values: `apartment`, `penthouse`, `studio`, `maisonette`, `loft`, `townhouse` | `apartment` |

---

## Spatial

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `latitude` | Decimal | WGS84 latitude coordinate. Required for map visuals in Power BI | `48.1631` |
| `longitude` | Decimal | WGS84 longitude coordinate. Required for map visuals in Power BI | `11.5681` |

---

## Physical Attributes

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `size_sqm` | Decimal | Total living area in square metres | `78.5` |
| `rooms` | Integer | Number of rooms (excluding bathrooms) | `3` |
| `floor` | Integer | Floor number. 0 = ground floor | `4` |
| `year_built` | Integer | Year of original construction | `1987` |
| `condition` | String | Property condition. Values: `new_build`, `renovated`, `good`, `fair`, `needs_renovation` | `renovated` |

---

## Financial

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `price_eur` | Integer | Asking/sale price in Euros | `780000` |
| `price_band` | String | Price bracket. Values: `<500K`, `500K-750K`, `750K-1M`, `1M+` | `750K-1M` |
| `price_per_sqm` | Integer | Price per square metre in Euros | `7400` |
| `monthly_rent_eur` | Integer | Estimated monthly rent in Euros | `2100` |
| `gross_yield_pct` | Decimal | Annual gross rental yield as a percentage. Formula: (monthly_rent × 12) / price × 100 | `3.23` |

---

## Property Features

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `energy_class` | String | EU energy efficiency rating. Values: `A+`, `A`, `B`, `C`, `D`, `E` | `B` |
| `heating_type` | String | Primary heating system. Values: `district_heating`, `gas_central`, `heat_pump`, `underfloor` | `gas_central` |
| `parking` | String | Parking availability. Values: `underground_garage`, `outdoor_spot`, `none` | `underground_garage` |
| `has_balcony` | Boolean | Property includes a balcony or terrace | `True` |
| `has_elevator` | Boolean | Building has a working elevator | `True` |
| `pets_allowed` | Boolean | Pets permitted by building rules | `False` |

---

## Mobility & Walkability

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `walk_score` | Integer | Walkability index (0–99). Higher = more walkable | `82` |
| `transit_score` | Integer | Public transit accessibility index (0–99) | `78` |
| `bike_score` | Integer | Cycling infrastructure index (0–99) | `74` |
| `dist_ubahn_km` | Decimal | Straight-line distance to the nearest U-Bahn station in kilometres | `0.43` |

---

## Market Status

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `currently_listed` | Boolean | Whether the property is actively listed for sale at time of snapshot | `True` |
| `days_on_market` | Integer | Number of days listed. 0 if not currently listed | `34` |

---

## Notes for Power BI

- Load `latitude` and `longitude` as **Decimal Number** type in Power Query — do not leave as text or the map visual will fail.
- Load `price_eur`, `price_per_sqm`, `monthly_rent_eur` as **Fixed Decimal Number** (currency).
- Load `has_balcony`, `has_elevator`, `pets_allowed`, `currently_listed` as **True/False**.
- `price_band` uses hyphens not en-dashes for compatibility with all locales: `500K-750K` not `500K–750K`.
- `days_on_market` = 0 for unlisted properties — filter to `currently_listed = True` before averaging this column.
