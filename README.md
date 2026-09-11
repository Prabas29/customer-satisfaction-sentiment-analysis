# Customer Satisfaction & Sentiment Analysis — Ticket System Review

Analysis of customer survey data for six help desk / ticketing systems (Zendesk, Zoho Desk, Freshdesk, Jira Service Management, ServiceNow, and otrs). The goal is to measure customer satisfaction using standard metrics, run sentiment analysis on written reviews, and present the findings in an interactive dashboard.

This project was completed as part of the Data Analyst & Business Intelligence Bootcamp (DABI 23) at Dibimbing.id.

## Objectives

- Measure customer satisfaction with CSAT, CES, and NPS
- Classify review text into positive, neutral, and negative sentiment
- Build an interactive Power BI dashboard to communicate the results
- Turn the findings into clear, data-driven business recommendations

## Tools

- **Python** (pandas, numpy, VADER) on Google Colab for data cleaning and analysis
- **Power BI** for the interactive dashboard
- **Google Slides** for the final presentation

## Dataset

The dataset contains 1,462 survey rows, of which 787 are valid responses (a survey is considered valid only when every rating and the review text are filled in). Key fields:

| Column | Description |
|---|---|
| `overall_rating` | overall satisfaction, scale 1 to 5 |
| `customer_service`, `features`, `value_for_money`, `ease_of_use` | per-aspect ratings, 1 to 5 |
| `likelihood_to_recommend` | basis for NPS, scale 1 to 10 |
| `overall_text` | free-text review, used for sentiment analysis |
| `ticket_system` | the product being reviewed |
| `date_of_survey` | survey date |

## Method

**Preprocessing**
- Converted the date column to datetime
- Found invalid `-1` values in some rating columns and treated them as missing values so they would not distort the scores
- Filtered down to the 787 valid respondents before computing any metric

**Satisfaction metrics**
- CSAT = total satisfaction score / (number of respondents × max rating)
- CES uses the `ease_of_use` score with the same formula
- NPS = (Promoters − Detractors) / total respondents, after grouping `likelihood_to_recommend` into Promoter (9–10), Passive (7–8), and Detractor (below 7)

**Sentiment analysis**
- Cleaned the review text (removed URLs, usernames, and double spaces)
- Used VADER (a lexicon-based model) to score each review and label it Positive, Neutral, or Negative

## Key Results

| Metric | Result | Category |
|---|---|---|
| Response Rate | 53.83% | — |
| CSAT (overall) | 91.18% | Excellent |
| CSAT (customer service) | 67.40% | Fair |
| CES | 89.48% | — |
| NPS | 11.94 | Average |
| Positive sentiment | 85.6% | — |

**Main insights**
- Overall CSAT is very high (91%), but customer service is the weakest aspect at only 67%, while features and value for money both sit around 88%.
- NPS is low (12) because most customers are Passive (379 of them). They are satisfied but not yet promoting the product.
- 85.6% of reviews are positive; the most frequent words include easy, great, support, helpful, and recommend.
- Average ratings across all six products are similar (4.5 to 4.6), so the market is competitive.

**Recommendations**
- Prioritize improving customer service, since it is the lowest-scoring aspect and has the highest impact on overall satisfaction.
- Convert Passive customers into Promoters through loyalty programs or follow-ups to lift the NPS.
- Improve the survey response rate so the data is more representative.
- Use positive reviews as testimonials and follow up on negative ones to reduce churn.

## Repository Structure

```
.
├── README.md
├── notebook/      # Google Colab notebook (cleaning, metrics, sentiment)
├── data/          # source dataset
├── dashboard/     # Power BI screenshot and export
└── slides/        # final presentation (PDF)
```

## Author

**Prabaswara Trirespati** — DABI 23, Dibimbing.id Data Analyst Bootcamp
