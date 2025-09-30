# British Airways Review Dashboard

![Dashboard Screenshot](Dashboard%201.png)

[View on Tableau Public](https://public.tableau.com/app/profile/neelam.s.jat/viz/BritishAirwaysReviewDashboard_17577182834360/Dashboard1)

## Project Overview

This project analyzes passenger reviews of British Airways flights using a Tableau dashboard. The goal is to provide actionable insights into customer satisfaction across multiple service dimensions, aircraft types, and global regions.

### Business Questions Answered

1. **What is the overall passenger satisfaction trend over time?**
2. **Which countries have the highest/lowest average ratings for British Airways?**
3. **How do ratings vary by aircraft type?**
4. **Which service aspects (Food, Entertainment, Cabin Staff, Ground Service, Value for Money, Seat Comfort) are most and least appreciated?**
5. **How do traveller type, seat type, and continent affect review scores?**
6. **Are there seasonal patterns or anomalies in passenger ratings?**

## Project Flow

1. **Data Collection**
    - Source: Public British Airways review data from Kaggle ([dataset link](https://www.kaggle.com/))
    - Data includes: review text, rating scores, aircraft type, traveller type, country, date, and service dimensions.

2. **Data Cleaning and Preparation**
    - **SQL**: Used for initial structuring, filtering nulls, and removing duplicates.
    - **Python (pandas)**: Further cleaning, handling outliers, standardizing formats.

3. **Data Analysis and Visualization**
    - Load cleaned data into Tableau.
    - Create interactive dashboard with multiple filters and visualizations:
        - Time series of average ratings
        - World map of country-level ratings
        - Bar chart comparing aircraft ratings
        - Top-level KPI metrics
        - Multiple filters for granular exploration

4. **Dashboard Publishing**
    - Published on Tableau Public for easy access.
    - Users can interact with filters to answer business questions.

5. **Documentation**
    - README, scripts, and Tableau workbook provided for transparency and reproducibility.

## Data Cleaning Scripts

### SQL

```sql
-- Remove duplicates and filter out null ratings
CREATE TABLE clean_reviews AS
SELECT DISTINCT
    review_id,
    date,
    country,
    aircraft_type,
    traveller_type,
    seat_type,
    overall_rating,
    food_rating,
    entertainment_rating,
    ground_service_rating,
    cabin_staff_rating,
    value_for_money_rating,
    seat_comfort_rating
FROM raw_reviews
WHERE overall_rating IS NOT NULL;
```

### Python

```python
import pandas as pd

# Load data
df = pd.read_csv('british_airways_reviews.csv')

# Remove duplicates
df = df.drop_duplicates(subset=['review_id'])

# Filter out rows with missing overall ratings
df = df[df['overall_rating'].notnull()]

# Standardize country names
df['country'] = df['country'].str.strip().str.title()

# Handle outliers in ratings (keep ratings between 1 and 5)
rating_cols = [
    'overall_rating', 'food_rating', 'entertainment_rating', 'ground_service_rating',
    'cabin_staff_rating', 'value_for_money_rating', 'seat_comfort_rating'
]
for col in rating_cols:
    df[col] = df[col].apply(lambda x: x if 1 <= x <= 5 else None)

# Save cleaned dataset
df.to_csv('clean_british_airways_reviews.csv', index=False)
```

## How to View the Dashboard

- **Online:** [Tableau Public Dashboard](https://public.tableau.com/app/profile/neelam.s.jat/viz/BritishAirwaysReviewDashboard_17577182834360/Dashboard1)
- **Locally:** Download the Tableau workbook (.twbx) and open with Tableau Desktop or Tableau Public.

## Screenshot

![Dashboard Screenshot](./dashboard_screenshot.png)

## License

This project is licensed under the MIT License. See [LICENSE](./LICENSE) for details.

## Credits

- **Data Source:** British Airways reviews, published via Kaggle
- **Author:** Neelam S Jat

## Contact

For questions or collaboration, please reach out via [GitHub](https://github.com/Neelam-jat).
