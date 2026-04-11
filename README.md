# 🍽️ Yelp Customer Engagement Analysis

An exploratory data analysis project using the **Yelp Open Dataset** to uncover patterns in customer engagement, restaurant performance, and user behavior across the platform.

---

## 📁 Project Structure

```
CUSTOMER_ENGAGEMENT/
├── Yelp JSON/          # Raw Yelp dataset (JSON files)
├── analysis.ipynb      # Main EDA notebook
├── DB_Creation.ipynb   # SQLite database creation from JSON
├── yelp.db             # SQLite database
└── README.md
```

---

## 🗃️ Database Schema

The project uses a SQLite database (`yelp.db`) with 5 tables derived from the Yelp Open Dataset:

| Table | Description |
|---|---|
| `business` | Business info — name, location, stars, review count, categories |
| `review` | User reviews with star ratings, text, and reaction counts (useful/funny/cool) |
| `user` | User profiles including elite status, friends, fans, and compliments |
| `tip` | Short tips left by users for businesses |
| `checkin` | Timestamped check-in records per business |

---

## 🔍 Analysis Overview

The notebook `analysis.ipynb` focuses exclusively on **open restaurants** and answers the following key questions:

1. **Which restaurants have the highest reviews and ratings?**
2. **Do higher-rated restaurants receive more engagement (reviews, tips, check-ins)?**
3. **Is there a correlation between reviews, tips, and check-ins?**
4. **How does engagement differ between high-rated (≥3.5⭐) and low-rated (<3.5⭐) businesses?**
5. **How do restaurants perform across different cities and states?**
6. **Are there seasonal trends in user engagement over time?**
7. **How does review sentiment (useful, funny, cool) correlate with restaurant success?**
8. **Do elite users drive more engagement than non-elite users?**
9. **What are the busiest hours for tips, reviews, and check-ins?**

---

## 📊 Key Conclusions

### 🌟 Rating & Engagement
- **Higher-rated restaurants (≥3.5 stars) consistently attract more reviews, tips, and check-ins** than lower-rated ones, confirming that quality drives sustained customer engagement across all interaction types.
- The correlation heatmap reveals a **strong positive correlation between review count, tip count, and check-in count**, indicating that engagement metrics reinforce each other — a popular restaurant tends to score high on all dimensions simultaneously.

### 🗺️ Geographic Performance
- Restaurant performance varies significantly by city and state. A custom **success score** (computed as `avg_rating × log(review_count + 1)`) was used to compare cities fairly, balancing both volume and quality.
- Top-performing cities cluster in high-density metro areas, showing the importance of market size on overall review volume.

### 📅 Seasonal & Temporal Trends
- Seasonal decomposition of monthly tip and review counts for high-rated businesses reveals **recurring annual patterns**, with engagement generally peaking in warmer months and dipping around the start of the year.
- Review sentiment scores (useful, funny, cool) show only a **modest correlation with success metrics**, suggesting that while positive engagement helps, the volume of interaction matters more than sentiment type alone.

### 👑 Elite vs. Non-Elite Users
- **Elite users represent a small minority of the user base** but contribute a disproportionately large share of total reviews, demonstrating their outsized impact on Yelp's content ecosystem.
- Businesses that attract elite reviewers tend to accumulate more credibility and visibility on the platform.

### ⏰ Peak Engagement Hours
- **Tips and reviews peak in the evening hours** (roughly 6 PM – 9 PM), aligning with typical restaurant dining times.
- **Check-ins show a broader spread** throughout the day but also concentrate in late afternoon and evening, suggesting customers check in at arrival while leaving reviews and tips after the experience.

---

## 🛠️ Tech Stack

- **Python 3.13**
- **pandas** — data manipulation
- **SQLite3** — database querying
- **matplotlib / seaborn** — static visualizations
- **folium** — interactive geospatial map
- **statsmodels** — seasonal decomposition (time series)
- **geopy** — geocoding support
- **numpy** — numerical operations

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas matplotlib seaborn folium geopy statsmodels numpy
```

### Steps
1. Clone the repository.
2. Place the Yelp JSON dataset files inside the `Yelp JSON/` folder.
3. Run `DB_Creation.ipynb` to build the `yelp.db` SQLite database.
4. Open and run `analysis.ipynb` to explore the analysis.

---

## 📦 Dataset

This project uses the [Yelp Open Dataset](https://www.yelp.com/dataset). Download it separately and place the JSON files in the `Yelp JSON/` directory before running `DB_Creation.ipynb`.

---

## 📌 Notes

- Outliers in `review_count`, `useful_count`, `funny_count`, and `cool_count` are removed using the **IQR method** to prevent skewed visualizations.
- The analysis scope is restricted to **open restaurants** (`is_open = 1` and `categories LIKE '%restaurant%'`).
