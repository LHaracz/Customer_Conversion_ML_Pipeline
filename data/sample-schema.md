# Sample Schema – Customer Conversion (Cleaned Dataset)

This schema describes the **cleaned feature set** used in the Customer Conversion ML pipeline.

- **Raw file:** `digital_marketing_campaign_dataset.csv`
- **Cleaned file:** `digital_marketing_campaign_dataset_cleaned.csv`
- **Rows (cleaned):** ~7.8k
- **Missing values:** None (all rows used for modeling have complete data)
- **Target variable:** `Conversion` (binary: 0/1)

The cleaned dataset:

1. Drops raw metadata columns not used for modeling:
   - `AdvertisingPlatform`
   - `AdvertisingTool`
2. Keeps core customer, campaign, and behavior features.
3. One-hot encodes categorical fields:
   - `Gender` → `is _Male`
   - `CampaignChannel` → `channel _PPC`, `channel _Referral`, `channel _SEO`, `channel _Social Media`  
     (Email is the implicit baseline when all channel dummies are 0.)
   - `CampaignType` → `type _Consideration`, `type _Conversion`, `type _Retention`  
     (Awareness is the implicit baseline.)

---

## Column Dictionary

### ID & Demographics

| Column        | Type    | Example | Description |
|---------------|---------|---------|-------------|
| `CustomerID`  | int     | `12015` | Synthetic customer identifier. Unique per row; no semantic meaning beyond ID. |
| `Age`         | int     | `43`    | Customer age in years (approx. 18–80). |
| `Income`      | int     | `84651` | Annual customer income in currency units (approx. 20k–200k+). |

---

### Campaign & Spend

| Column              | Type    | Example | Description |
|---------------------|---------|---------|-------------|
| `AdSpend`           | float   | `5001.50` | Total advertising spend allocated to this customer/campaign impression window. Roughly 100–10,000. |
| `ClickThroughRate`  | float   | `0.15`  | Click-through rate (% of impressions that resulted in a click), stored as 0–1. |
| `ConversionRate`    | float   | `0.10`  | Conversion rate (% of clicks that converted), stored as 0–1. |

---

### On-Site Behavior

| Column          | Type   | Example | Description |
|-----------------|--------|---------|-------------|
| `WebsiteVisits` | int    | `25`    | Number of website visits in the campaign window (>= 1). |
| `PagesPerVisit` | float  | `5.6`   | Average number of pages viewed per visit (approx. 1–10). |
| `TimeOnSite`    | float  | `7.7`   | Average time spent on site per visit (in minutes, ~0.5–15). |

---

### Engagement & History

| Column              | Type   | Example | Description |
|---------------------|--------|---------|-------------|
| `SocialShares`      | int    | `50`    | Number of social shares associated with this customer’s interactions (0–99). |
| `EmailOpens`       | int    | `10`    | Number of marketing emails opened. |
| `EmailClicks`      | int    | `4`     | Number of clicks from marketing emails. |
| `PreviousPurchases`| int    | `4`     | Count of previous purchases by the customer before this campaign window (0–9). |
| `LoyaltyPoints`    | int    | `2500`  | Loyalty program points accumulated by the customer (0–4999). |

---

### Target

| Column       | Type | Values | Description |
|--------------|------|--------|-------------|
| `Conversion` | int  | {0,1}  | **Target label.** `1` if the customer converted (e.g., made a purchase) during the campaign window, `0` otherwise. |

---

### Encoded Categorical Features

The following binary columns are derived from categorical variables via one-hot encoding (dummy variables). Values are always `0` or `1`.

#### Gender

| Column     | Type | Example | Description |
|------------|------|---------|-------------|
| `is _Male` | int  | `1`     | Gender indicator. `1` = Male, `0` = not male (primarily female in this dataset). |

> Note: There is no explicit `is_Female` column; female is the baseline when `is _Male = 0`.

#### CampaignChannel (baseline: `Email`)

Original values: `Email`, `PPC`, `Referral`, `SEO`, `Social Media`.

| Column               | Type | Example | Description |
|----------------------|------|---------|-------------|
| `channel _PPC`       | int  | `1`     | `1` if campaign channel is **PPC**, else `0`. |
| `channel _Referral`  | int  | `0`     | `1` if campaign channel is **Referral**, else `0`. |
| `channel _SEO`       | int  | `0`     | `1` if campaign channel is **SEO**, else `0`. |
| `channel _Social Media` | int | `0`   | `1` if campaign channel is **Social Media**, else `0`. |

If all channel dummies are `0`, the channel is **Email**.

#### CampaignType (baseline: `Awareness`)

Original values: `Awareness`, `Consideration`, `Conversion`, `Retention`.

| Column              | Type | Example | Description |
|---------------------|------|---------|-------------|
| `type _Consideration` | int | `0`   | `1` if campaign type is **Consideration**, else `0`. |
| `type _Conversion`    | int | `1`   | `1` if campaign type is **Conversion**, else `0`. |
| `type _Retention`     | int | `0`   | `1` if campaign type is **Retention**, else `0`. |

If all type dummies are `0`, the type is **Awareness**.

---

## Raw vs. Cleaned (Summary)

- **Dropped columns (raw only):**
  - `AdvertisingPlatform`
  - `AdvertisingTool`
- **Kept as-is:**
  - `CustomerID`, `Age`, `Gender`, `Income`, `CampaignChannel`, `CampaignType`, `AdSpend`, `ClickThroughRate`, `ConversionRate`, `WebsiteVisits`, `PagesPerVisit`, `TimeOnSite`, `SocialShares`, `EmailOpens`, `EmailClicks`, `PreviousPurchases`, `LoyaltyPoints`, `Conversion`.
- **Engineered in cleaned dataset:**
  - One-hot encodings: `is _Male`, `channel _*`, `type _*`.

This is the schema used throughout the modeling pipeline (EDA, feature engineering, model training, and result visualizations).
