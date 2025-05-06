# 080_Book_Recommender  
# 📘 Recommender Systems Project – Book-Crossing Dataset

## 📌 Objective
The goal of this project was to implement different types of recommender systems using the Book-Crossing dataset, which includes user ratings and metadata for books.

---

## 📂 Dataset Overview
- **Users.csv**: Contains `User-ID`, location, and `Age`
- **Books.csv**: Contains book `ISBN`, `Title`, `Author`, `Year`, and `Publisher`
- **Ratings.csv**: Contains `User-ID`, `ISBN`, and `Book-Rating`

Only explicit ratings (1–10) were kept for collaborative filtering. Implicit ratings (value = 0) were removed.

---

## 🧹 Preprocessing Highlights
- Cleaned invalid or missing values
- Converted `User-ID` safely to integer
- Filtered to include only:
  - Users with at least 10 ratings
  - Books with at least 10 ratings

This reduced matrix size significantly and prevented memory errors.

---

## 🎭 Content-Based Filtering

- Combined book metadata (`Title`, `Author`, `Publisher`) into a single text feature
- Applied **TF-IDF Vectorization**
- Used **Cosine Similarity** to find similar books
- Created a function `get_recommendations(title)` to return top N similar books

**Note**: Due to memory limitations, this was done on a random 30,000 book sample.

---

## 🤝 Collaborative Filtering (Item-Item)

- Built a **pivot table** with `User-ID` × `ISBN`
- Used **Cosine Similarity** on the transposed matrix (books as rows)
- Created `get_similar_books(isbn)` to return similar books based on other users’ ratings

---

## 🧑‍🤝‍🧑 Collaborative Filtering (User-User)

- Calculated similarity between users using **Cosine Similarity**
- For a given user, found top similar users
- Aggregated ratings from similar users to recommend new books
- Created `recommend_books_for_user(user_id)` function

Recommendations exclude books already rated by the user.

---

## ✅ Summary
| Method                    | Description                            | Strengths                             |
|--------------------------|----------------------------------------|----------------------------------------|
| Content-Based Filtering  | Similar books by metadata              | Works without ratings, fast            |
| Item-Item CF             | Similar books based on user ratings    | Accurate when item similarities matter |
| User-User CF             | Recommends based on similar users      | Good personalization                   |
