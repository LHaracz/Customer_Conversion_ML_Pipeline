# Dataset Schema – Digital Marketing Campaign Dataset (Raw)

This document describes the structure of the **original, uncleaned dataset**
used in the Digital Marketing Conversion Prediction project.

The purpose of this schema is to document the data as it was received prior to
any preprocessing, column pruning, or modeling decisions.

---

## Dataset Overview

- **Each row represents:** A single user interaction with a digital marketing campaign
- **Prediction Target:** Customer conversion outcome
- **Duplicate Rows:** None detected
- **Missing Values:** None detected

---

## Column Definitions (Raw Dataset)

| Column Name | Type | Description |
|------------|------|-------------|
| `User_ID` | Integer | Unique identifier for each user |
| `Age` | Integer | Age of the user |
| `Gender` | Categorical | Gender of the user |
| `Campaign_Type` | Categorical | Marketing campaign category |
| `Channel` | Categorical | Channel through which the campaign was delivered |
| `Advertising_Platform` | Categorical | Platform used to deliver ads (e.g., Google, Meta) |
| `Advertising_Tool` | Categorical | Tool used to manage advertising |
| `Impressions` | Integer | Number of ad impressions |
| `Clicks` | Integer | Number of ad clicks |
| `CTR` | Numeric | Click-through rate |
| `Session_Duration` | Numeric | Duration of the user session |
| `Pages_Viewed` | Integer | Number of pages viewed during the session |
| `Previous_Purchases` | Integer | Count of prior purchases by the user |
| `Bounce_Rate` | Numeric | Bounce rate associated with the session |
| `Time_On_Site` | Numeric | Total time spent on the site |
| `Conversion` | Binary (0/1) | Target variable indicating whether a conversion occurred |

---

## Data Quality Notes

- No duplicate records were found in the dataset
- No missing values were present across any columns
- Data types were consistent and required minimal coercion
- Dataset was immediately suitable for modeling after column selection

---

## Column Pruning Decisions

The following columns were **intentionally removed during preprocessing**:

| Column Removed | Reason |
|---------------|--------|
| `Advertising_Platform` | Redundant with campaign/channel information |
| `Advertising_Tool` | Operational detail not predictive of user conversion |

These features were excluded to:
- Reduce noise
- Minimize dimensionality
- Avoid overfitting to implementation-specific attributes

---

## Cleaned Dataset

After preprocessing, the cleaned dataset retained only features with
predictive relevance for modeling customer conversion behavior.

All preprocessing logic is implemented and documented in:

- `1_EDA_and_Cleaning.ipynb`

The cleaned dataset is used consistently across all downstream models.
