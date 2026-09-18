# TasteMatch: Restaurant Recommender System

DSA 4060: Recommender Systems - Semester Project

**Student:** Claire Mwarari - 669470

## Project Description

TasteMatch is a restaurant recommender system that helps users discover restaurants matching their cuisine preferences, budget, and rating history, while introducing relevant restaurants they have not yet rated.

Choosing where to eat is harder than it looks. A city has thousands of restaurants with different cuisines, prices, and ratings, while search and delivery apps rank results mainly by popularity, advertising, or distance instead of personal taste. This project builds a system that learns from a user's past ratings and the features of restaurants they liked, then ranks unrated restaurants by predicted relevance.

**Users:** diners looking for personalised restaurant suggestions (students, residents, visitors).

**Items:** restaurants in Philadelphia, filtered from the Yelp Open Dataset.

**Output:** a ranked top-10 list of restaurants with predicted rating, cuisine tags, price level, and a short explanation for each recommendation.

## Dataset

**Source:** [Yelp Open Dataset](https://business.yelp.com/data/resources/open-dataset/) (Yelp Inc.), free for educational use under the Yelp Dataset License.

The license does not allow redistribution, so the raw data is **not** uploaded to this repository. To reproduce the dataset:

1. Download the dataset from the link above (free registration required).
2. Extract the archive (the zip contains `yelp_dataset.tar`, which holds the JSON files).
3. Run `notebooks/Week1_Yelp_Data_Preparation.ipynb` on Google Colab. It filters businesses to restaurants, keeps Philadelphia, loads reviews in memory-safe chunks, filters to active users and restaurants, and saves compact parquet files.

**Dataset figures after preparation:**

| Stage | Users | Restaurants | Ratings |
|---|---|---|---|
| Full Yelp Open Dataset | ~2,000,000 | 150,346 businesses (64,616 restaurants) | 6,990,280 reviews |
| Philadelphia restaurant subset | - | 7,076 | 738,688 |
| Working dataset (restaurants with 20+ reviews, users with 5+ ratings) | 27,771 | 4,495 | 436,931 |

Working dataset matrix density: 0.35%.

**Key files used:**

- `business.json` - restaurant metadata: name, location, stars, review_count, categories (cuisines), attributes (30+ fields: price range, ambience, parking, dietary options)
- `review.json` - user-item interactions: user_id, business_id, 1-5 star rating, timestamp
- `user.json` - user metadata: review_count, average_stars, yelping_since

## Proposed Approaches

- **Baseline:** popularity-based recommendations (weighted rating of stars and review_count)
- **Approach 1:** content-based filtering using cuisine categories and restaurant attributes
- **Approach 2:** collaborative filtering (user-based and item-based kNN) on the rating matrix
- **Approach 3:** matrix factorization (SVD) combined with content-based scores in a hybrid design

## Evaluation Plan

- RMSE and MAE for rating prediction
- Precision@K, Recall@K, and NDCG@K for recommendation relevance and ranking quality
- Catalogue coverage and intra-list cuisine diversity as supporting metrics
- Time-based train/test split per user; every approach is compared against the popularity baseline on identical splits

## Milestones

| Weeks | Main tasks | Expected outputs |
|---|---|---|
| 1-2 | Problem selection, dataset inspection, proposal, GitHub setup | Proposal, repository with README |
| 3-4 | Data cleaning, restaurant/city subset, baseline model, content-based prototype | Clean dataset, baseline + content-based notebook |
| 5-6 | Collaborative filtering (user/item kNN), preliminary evaluation | kNN models, evaluation tables |
| 7 | Mid-semester examination | - |
| 8-10 | Matrix factorization, hybrid design, hyperparameter tuning | SVD + hybrid models, improved metrics |
| 11-13 | Interface, evaluation, documentation, presentation | App, report, demo |

## Tools

Python, Pandas/NumPy, Scikit-learn, Surprise, Google Colab, Streamlit, GitHub.
