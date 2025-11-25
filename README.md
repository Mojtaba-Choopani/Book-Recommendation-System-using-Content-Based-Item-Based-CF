# 📚 Book Recommendation System  
### Content-Based Filtering & Item-Based Collaborative Filtering  
Using the Book-Crossing Public Dataset

---

## 📌 Overview
This project implements two classic recommendation system approaches:

1. **Content-Based Filtering (CBF)**  
   Based on book metadata (title, author, publisher) using TF-IDF vectorization and cosine similarity.

2. **Item-Based Collaborative Filtering (CF)**  
   Based on user rating patterns using a user–item matrix and item–item cosine similarity.

The goal is to compare these two models on the Book-Crossing dataset and evaluate their performance.

---

## 📂 Dataset

The project uses the **Book Recommendation Dataset (Book-Crossing)** available on Kaggle:

👉 https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset  

This dataset contains:

- **Books.csv** — ~271K book metadata records  
- **Users.csv** — ~278K user profiles  
- **Ratings.csv** — ~1.1M book ratings  

Ratings include both *implicit feedback* (rating = 0) and *explicit feedback* (1–10).

---

## 🧹 Data Preparation

### 🔹 Content-Based Filtering (CBF)
For the content-based model, the following preprocessing steps were applied:

- Selecting relevant book metadata (ISBN, title, author, publisher, year)
- Cleaning invalid text fields
- Filtering books that appear in `Ratings.csv`
- Removing duplicates and unrealistic publication years
- Keeping books with at least **7 ratings**
- Creating a combined text field per book
- TF-IDF vectorization (1–2 grams, `max_features=30,000`)

The model computes cosine similarity and recommends the Top-10 most similar books.

---

### 🔹 Item-Based Collaborative Filtering (CF)

Steps for building the CF model:

- Keep only **explicit ratings** (`Book-Rating > 0`)
- Filter books with at least **20 ratings**
- Filter users with at least **10 rated books**
- Encode `User-ID` and `ISBN` as category codes
- Build a sparse **user–item matrix (1834 × 2172)**
- Compute item–item cosine similarity
- Predict user ratings using weighted averages of similar items
- Recommend Top-10 unrated books per user

---

## 📊 Evaluation

### Content-Based Filtering
Evaluated using **Precision@10** and **Recall@10**:

| Metric        | Score  |
|--------------|--------|
| Precision@10 | 0.055  |
| Recall@10    | 0.111  |

### Item-Based Collaborative Filtering
Evaluated using **MAE** and **RMSE**:

| Metric | Score  |
|--------|--------|
| MAE    | ~0.70  |
| RMSE   | ~0.94  |

---

## 🛠 Technologies Used
- Python  
- Pandas  
- NumPy  
- Scikit-Learn  
- SciPy  
- Jupyter Notebook  

---

## 📁 Project Structure

```text
├── 01_FrequentPattern and AssociationRules.ipynb
├── 02_Simple Recommender.ipynb
├── 03_Knowledge Recommender.ipynb
├── 04_Content Based Recommenders.ipynb
├── 05_Item-Based Collaborative Filtering.ipynb
├── 06_book-recommendation-system.ipynb
└── Dataset/
