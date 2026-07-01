Football Analytics: Home Advantage & The Possession Myth (2000 - 2025)

Project Overview
This project explores a massive global football dataset spanning 25 years and containing over 50,000 unique match records. By engineering a unified data pipeline out of fragmented match logs and structural game statistics, this analysis uncovers historical truths behind **Home Ground Advantage** and challenges popular beliefs surrounding "Ball Possession Efficiency".

---

Core Discoveries & Insights

1. The Home Advantage is Measurable
Across 50,262 analyzed matches, home teams consistently outperform away teams in both scoring volume and field dominance:
* **Average Home Goals:** 1.47 per match
* **Average Away Goals:** 1.13 per match
* **Average Home Possession:** 51.02%

2. The "Tiki-Taka" Possession Myth Exposed
A deep dive using data distributions reveals that high ball possession does **not** equal more clinical finishing. When grouping teams by possession scales, shooting accuracy stays remarkably flat:
* **Low Possession (<45%):** ~29.6% shooting accuracy
* **Medium Possession (45-55%):** ~29.8% shooting accuracy
* **High Possession (>55%):** ~30.1% shooting accuracy

"Conclusion:" Defensive, counter-attacking teams are mathematically just as precise with their shots on goal as teams utilizing heavy possession styles.

---

Tech Stack & Data Pipelines
* **Language:** Python
* **Libraries:** Pandas (Data Engineering), Matplotlib & Seaborn (Data Visualization)
* **Key Tasks Completed:**
  * Handled data fragmentation by horizontally joining separate match logs and match statistic CSV structures.
  * Extracted and converted text data types (clearing `%` string symbols into mathematical `floats`).
  * Eliminated row duplication multiplying errors by filtering on composite key elements.

---

Technical Snippet: Data Cleaning Pipeline
```python
# Strip possession text markers and scale columns into numerical metrics safely
df_final['Ball_Possession_Home'] = df_final['Ball_Possession_Home'].astype(str).str.rstrip('%')
df_final['Ball_Possession_Home'] = pd.to_numeric(df_final['Ball_Possession_Home'], errors='coerce')

# Segmenting possession into analytical tracking categories
def possession_bracket(pos):
    if pos < 45: return 'Low Possession (<45%)'
    elif pos <= 55: return 'Medium Possession (45-55%)'
    else: return 'High Possession (>55%)'

df_final['Possession_Bracket'] = df_final['Ball_Possession_Home'].apply(possession_bracket)
