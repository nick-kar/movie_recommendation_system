# Movie Recommendation System

A Python-based movie recommendation system built with the MovieLens dataset. This project explores user rating behavior, establishes a popularity-based baseline, and evaluates personalized recommendations using item-based collaborative filtering.

## Project Objectives

- Explore user–movie rating data and identify rating patterns.
- Build a popularity-based recommendation baseline.
- Implement item-based collaborative filtering using cosine similarity.
- Evaluate top-10 recommendations using Precision@10, Recall@10, and NDCG@10.
- Compare personalized recommendations against a non-personalized baseline.

## Dataset

This project uses the [MovieLens Latest Small dataset](https://grouplens.org/datasets/movielens/latest/).

The dataset contains:
- **100,836 ratings**
- **610 users**
- **9,742 movies with at least one rating**
- Movie metadata, genres, and user-generated tags

Download and extract the dataset into `data/raw/ml-latest-small/`. The raw dataset is excluded from this repository.

## Methods

### 1. Exploratory Data Analysis

The analysis examines rating distributions, user activity, movie popularity, missing values, and duplicate user–movie ratings.

### 2. Popularity-Based Baseline

Movies are ranked using their number of ratings in the training data. Recommendations exclude movies already rated by each user.

### 3. Item-Based Collaborative Filtering

A user–movie rating matrix is constructed from training data. Cosine similarity between movie rating profiles is used to score candidate movies for each user. Previously rated movies are excluded from recommendations.

### 4. Evaluation Protocol

Ratings are ordered chronologically for each user. The latest 20% are held out for testing, while at least five ratings are retained for training.

A test movie is considered relevant when its rating is at least 4.0. Evaluation is restricted to movies present in the training catalog and to users with at least one relevant held-out movie.

The models are evaluated using:
- **Precision@10:** proportion of the top 10 recommendations that are relevant.
- **Recall@10:** proportion of relevant held-out movies retrieved in the top 10.
- **NDCG@10:** ranking-sensitive measure that rewards relevant movies appearing higher in the list.

## Results

| Metric | Popularity Baseline | Item-Based Collaborative Filtering |
|---|---:|---:|
| Precision@10 | 0.0580 | **0.0728** |
| Recall@10 | 0.0498 | **0.0740** |
| NDCG@10 | 0.0757 | **0.0906** |

Both models were evaluated on the same 591 users.

Compared with the popularity baseline, item-based collaborative filtering achieved:
- **25.4% higher Precision@10**
- **48.6% higher Recall@10**
- **19.6% higher NDCG@10**

These results indicate that personalized recommendations improved top-10 ranking performance under this evaluation setup.

## Repository Structure

```text
movie_recommendation_system/
├── data/
│   └── raw/                       # Download separately; not committed
├── notebooks/
│   ├── 01_exploratory_data_analysis.ipynb
│   └── 02_recommendation_models.ipynb
├── src/
├── .gitignore
├── requirements.txt
└── README.md
```

## Installation

Python 3.9 or compatible environment recommended.

```bash
git clone https://github.com/nick-kar/movie_recommendation_system.git
cd movie_recommendation_system

python -m venv .venv
```

Activate the environment on Windows:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install the dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Download and extract MovieLens Latest Small into `data/raw/ml-latest-small/`, then open the notebooks in Jupyter or VS Code and run their cells in order.

## Limitations and Future Improvements

- The dataset is relatively small and does not represent a live production environment.
- Ratings are explicit feedback, rather than clicks or viewing behavior.
- The current collaborative-filtering implementation uses raw ratings and cosine similarity; alternative similarity measures and rating normalization could be explored.
- Further improvements could include matrix factorization, genre-based recommendations, hyperparameter tuning, and a recommendation API.

## Technologies

Python · pandas · NumPy · scikit-learn · SciPy · Matplotlib · Seaborn · Jupyter Notebook

## Acknowledgements

Dataset provided by [GroupLens Research](https://grouplens.org/datasets/movielens/).