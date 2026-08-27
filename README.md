# 📚 Books Recommendation System

### A Recommendation System using Popularity-Based and Collaborative Filtering

Finding a good book can be difficult when there are thousands of books available. This project explores how **book information, user information, and user ratings** can be used to build a recommendation system.

The project implements two recommendation approaches:

- 🔥 Popularity-Based Recommendation
- 🤝 Collaborative Filtering

For collaborative filtering, **Cosine Similarity** and **K-Nearest Neighbours (KNN)** are used to identify books with similar user-rating patterns.

---

## ✨ Project Highlights

| Feature | Details |
|---|---|
| 📚 Recommendation Approaches | **2** |
| 📂 Datasets Used | **3** |
| 🔥 Recommendation Type | **Popularity-Based** |
| 🤝 Filtering Technique | **Collaborative Filtering** |
| 📐 Similarity Measure | **Cosine Similarity** |
| 🤖 Neighbourhood Algorithm | **KNN** |
| 📖 Recommendation Output | **Top 5 Similar Books** |
| 📊 Analysis | **EDA & Visualization** |

---

## 🎯 Project Overview

The main objective of this project is to build a book recommendation system that can suggest books based on **popularity and user-rating patterns**.

The project starts with raw book, user, and rating data and processes it through data cleaning, exploratory analysis, popularity analysis, and collaborative filtering.

### Overall Workflow

    Books + Users + Ratings
              ↓
       Data Preprocessing
              ↓
    Exploratory Data Analysis
              ↓
       Recommendation System
          ↙          ↘
    Popularity      Collaborative
    Based           Filtering
                       ↓
               Cosine Similarity
                       ↓
                      KNN
                       ↓
              Book Recommendations

---

## 📂 Dataset

The project uses three main datasets:

| Dataset | Description |
|---|---|
| `Books.csv` | Contains information about books |
| `Users.csv` | Contains information about users |
| `Ratings.csv` | Contains user ratings for books |

### 📚 Books Dataset

The books dataset contains information such as:

- `ISBN`
- `Book-Title`
- `Book-Author`
- `Year-Of-Publication`
- `Publisher`
- `Image-URL-S`
- `Image-URL-M`
- `Image-URL-L`

The `ISBN` field is used to connect book information with the ratings dataset.

### 👤 Users Dataset

The users dataset contains:

- `User-ID`
- `Location`
- `Age`

### ⭐ Ratings Dataset

The ratings dataset contains:

- `User-ID`
- `ISBN`
- `Book-Rating`

The `User-ID` and `ISBN` fields are used to connect users, books, and ratings.

### Dataset Relationship

    Users.csv
        │
        │ User-ID
        ↓
    Ratings.csv
       /    \
      /      \
 User-ID    ISBN
              │
              ↓
          Books.csv

---

## 🧹 Data Preprocessing

Before building the recommendation system, the datasets are explored and cleaned.

The preprocessing includes:

- Checking missing values
- Checking duplicate records
- Handling missing publisher information
- Cleaning user age values
- Removing unrealistic age values
- Processing rating information
- Merging datasets using ISBN
- Filtering users based on rating activity
- Filtering books based on the number of ratings

This step helps prepare the data for exploratory analysis and recommendation.

---

## 📊 Exploratory Data Analysis

Exploratory Data Analysis is performed to understand the dataset before building the recommendation system.

### 📅 Publication Analysis

The number of books published across different years is analyzed.

### ✍️ Author Analysis

The project identifies authors with a large number of books in the dataset.

### 🏢 Publisher Analysis

Publishers are analyzed based on the number of books associated with them.

### 📚 Book Popularity

Books are analyzed based on the number of ratings they received.

### 👤 User Age Distribution

The distribution of users based on age is analyzed.

### ⭐ Rating Distribution

The distribution of book ratings is visualized to understand user rating behaviour.

---

## 🔥 Popularity-Based Recommendation

The first recommendation approach is based on **book popularity**.

The `Books.csv` and `Ratings.csv` datasets are merged using ISBN. The number of ratings and average rating are then calculated for each book.

    Books Dataset
          +
    Ratings Dataset
          ↓
      Merge using ISBN
          ↓
      Count Ratings
          ↓
      Calculate Average Rating
          ↓
      Sort Books
          ↓
      Popular Books

This approach is useful when there is little or no information available about a particular user.

### Example Popular Books

The popularity analysis includes books such as:

- `Wild Animus`
- `The Lovely Bones: A Novel`
- `The Da Vinci Code`
- `The Secret Life of Bees`
- `The Red Tent`

---

## 🤝 Collaborative Filtering

The second recommendation approach is **Collaborative Filtering**.

Instead of relying only on overall popularity, this approach uses **user-rating behaviour** to identify relationships between books.

The data is filtered to focus on users and books with sufficient rating activity before creating the user-book matrix.

    User Ratings
         ↓
    Filter Active Users
         ↓
    Filter Frequently Rated Books
         ↓
    Create User × Book Matrix
         ↓
    Calculate Similarity
         ↓
    Find Similar Books
         ↓
    Generate Recommendations

---

## 📐 Cosine Similarity

Cosine Similarity is used to measure the similarity between books based on their rating patterns.

Each book can be represented as a vector containing ratings from different users.

### Example

    Book A → [5, 4, 0, 3, 0, 5]

    Book B → [5, 3, 0, 4, 0, 5]

                  ↓

           Cosine Similarity

                  ↓

           Similarity Score

The implementation uses Scikit-learn's `cosine_similarity`:

    from sklearn.metrics.pairwise import cosine_similarity

    similarity_score = cosine_similarity(pt)

A higher similarity score indicates that two books have more similar rating patterns.

---

## 🤖 K-Nearest Neighbours

The project also uses **K-Nearest Neighbours (KNN)** to find books that are closest to a selected book.

The user-book matrix is converted into a sparse matrix before applying KNN.

    from scipy.sparse import csr_matrix
    from sklearn.neighbors import NearestNeighbors

    book_sparse = csr_matrix(pt)

    model = NearestNeighbors(algorithm='brute')
    model.fit(book_sparse)

The model searches for the nearest books and returns the most similar results.

    Selected Book
          ↓
       KNN Model
          ↓
    Nearest Neighbours
          ↓
      Similar Books
          ↓
    Top 5 Recommendations

---

## 🔍 Recommendation Function

A recommendation function is used to find books similar to a selected title.

### Example

    recommend_similar_books(
        'A Walk to Remember',
        pt,
        model
    )

The function:

1. Finds the selected book
2. Gets its position in the matrix
3. Finds the nearest neighbours
4. Sorts the results
5. Returns the top five similar books

---

## 📈 Recommendation Workflow

    User selects a book
            │
            ↓
    Check book in data
            │
            ↓
       Find book index
            │
            ↓
       Get rating vector
            │
            ↓
     Calculate similarity
            │
            ↓
    Find nearest neighbours
            │
            ↓
     Sort similar books
            │
            ↓
      Return Top 5 Books

---

## 🏗️ System Architecture

    ┌───────────────┐
    │   Books.csv   │
    └───────┬───────┘
            │
    ┌───────▼───────┐
    │   Users.csv   │
    └───────┬───────┘
            │
    ┌───────▼───────┐
    │  Ratings.csv  │
    └───────┬───────┘
            │
            ▼
    ┌───────────────────┐
    │ Data Preprocessing│
    └─────────┬─────────┘
              │
              ▼
    ┌───────────────────┐
    │       EDA         │
    └─────────┬─────────┘
              │
       ┌──────┴──────┐
       │             │
       ▼             ▼
    Popularity    Collaborative
    Based         Filtering
       │             │
       │       ┌─────┴─────┐
       │       ▼           ▼
       │    Cosine        KNN
       │   Similarity
       │       │           │
       └───────┴───────────┘
               │
               ▼
       📚 Recommendations

---

## 🧠 Recommendation Approaches

| Approach | How It Works | Main Use |
|---|---|---|
| 🔥 Popularity-Based | Uses rating count and average rating | General recommendations |
| 🤝 Collaborative Filtering | Uses user-rating patterns | Similar book recommendations |

### 🔥 Popularity-Based Recommendation

This method recommends books based on their overall popularity and rating activity.

### 🤝 Collaborative Filtering

This method finds books that have similar rating patterns based on user interactions.

---

## 📊 Project Metrics

| Metric | Value |
|---|---:|
| Recommendation Approaches | **2** |
| Main Datasets | **3** |
| Similarity Method | **Cosine Similarity** |
| Neighbourhood Algorithm | **KNN** |
| Recommendation Output | **Top 5 Books** |
| Filtering Technique | **Collaborative Filtering** |
| Data Analysis | **EDA + Visualization** |

---

## 📈 Analysis Performed

The project includes analysis of:

- Book publication years
- Authors
- Publishers
- Book popularity
- User ages
- Rating distribution
- User-book interactions
- Rating frequency

The analysis helps in understanding the available data before applying recommendation techniques.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| 🐍 **Python** | Core programming |
| 🐼 **Pandas** | Data manipulation and preprocessing |
| 🔢 **NumPy** | Numerical operations |
| 📊 **Matplotlib** | Data visualization |
| 📈 **Seaborn** | Statistical visualization |
| 🤖 **Scikit-learn** | Cosine Similarity and KNN |
| ⚡ **SciPy** | Sparse matrix processing |
| ☁️ **Google Colab** | Development environment |

---

## 📁 Project Structure

    Books-Recommendation-System/
    │
    ├── dataset/
    │   ├── Books.csv
    │   ├── Users.csv
    │   └── Ratings.csv
    │
    ├── notebooks/
    │   └── Books_Recommendation_System.ipynb
    │
    ├── images/
    │   ├── dataset-analysis.png
    │   ├── rating-distribution.png
    │   ├── popularity-analysis.png
    │   ├── similarity.png
    │   └── recommendations.png
    │
    ├── requirements.txt
    │
    └── README.md

> Update the file and folder names according to your actual repository.

---

## 🚀 Getting Started

### 1. Clone the Repository

    git clone <YOUR_REPOSITORY_URL>
    cd Books-Recommendation-System

### 2. Install Dependencies

    pip install numpy pandas matplotlib seaborn scikit-learn scipy

Or:

    pip install -r requirements.txt

### 3. Start Jupyter Notebook

    jupyter notebook

### 4. Open the Notebook

    Books_Recommendation_System.ipynb

Run the notebook cells in order.

---

## 💻 Example

A book can be passed to the recommendation function:

    recommend_similar_books(
        'A Walk to Remember',
        pt,
        model
    )

The system processes the selected book and finds books with similar rating patterns.

    Input
      ↓
    A Walk to Remember
      ↓
    User × Book Matrix
      ↓
    Similarity Calculation
      ↓
    KNN
      ↓
    Top 5 Similar Books

The project also demonstrates recommendations using books such as:

- `A Walk to Remember`
- `Nights in Rodanthe`
- `Year of Wonders`
- `Harry Potter and the Chamber of Secrets`
- `Message in a Bottle`

---

## 📚 Sample Recommendation

For example:

    Input:
    A Walk to Remember

The collaborative filtering model searches the user-book matrix and finds books with similar rating patterns.

    A Walk to Remember
             │
             ▼
       Rating Vector
             │
             ▼
      Similarity Search
             │
             ▼
          KNN Model
             │
             ▼
       Similar Books
             │
             ▼
        Top 5 Results

---

## 📷 Screenshots

### Dataset Analysis

![Dataset Analysis](images/dataset-analysis.png)

### Rating Distribution

![Rating Distribution](images/rating-distribution.png)

### Popularity Analysis

![Popularity Analysis](images/popularity-analysis.png)

### Similarity Analysis

![Similarity Analysis](images/similarity.png)

### Book Recommendations

![Book Recommendations](images/recommendations.png)

> Make sure the image files are present in the `images` folder.

---

## ⚠️ Limitations

### 1. Cold Start Problem

New users or books with very few ratings are difficult to recommend because there is not enough historical information.

### 2. Data Sparsity

Most users rate only a small portion of the available books, resulting in a sparse user-book matrix.

### 3. Popularity Bias

Popularity-based recommendations may produce similar recommendations for different users because they rely mainly on overall rating activity.

### 4. Dataset Dependency

The quality of recommendations depends on the quality and quantity of available user-rating data.

### 5. Limited Personalization

The current implementation mainly focuses on book similarity and does not provide a complete personalized user-profile-based recommendation system.

---

## 🔮 Future Improvements

Some improvements that can be added to the project:

- [ ] Add Content-Based Filtering
- [ ] Build a Hybrid Recommendation System
- [ ] Add user login and personalized profiles
- [ ] Allow users to rate books
- [ ] Add book search functionality
- [ ] Add personalized reading lists
- [ ] Improve cold-start handling
- [ ] Add book genres and descriptions
- [ ] Add book cover images
- [ ] Build a web interface
- [ ] Deploy the recommendation system online
- [ ] Experiment with deep learning-based recommendation models

---

## 💡 What I Learned

Working on this project helped me understand how recommendation systems work with user interaction data.

Through this project, I worked with:

- Recommendation Systems
- Popularity-Based Filtering
- Collaborative Filtering
- Cosine Similarity
- K-Nearest Neighbours
- User-Item Matrices
- Sparse Matrices
- Data Preprocessing
- Exploratory Data Analysis
- Data Visualization
- Handling Missing Values

---

## 📌 Key Takeaways

    3 Datasets
         ↓
    Data Cleaning
         ↓
    Exploratory Data Analysis
         ↓
    Popularity Analysis
         ↓
    User × Book Matrix
         ↓
    Cosine Similarity
         ↓
    KNN
         ↓
    Top 5 Similar Books

This project gave me practical experience in taking raw book-rating data and building a recommendation pipeline using popularity analysis and collaborative filtering.

---

## 📚 References

- Book Recommendation System Dataset — Kaggle
- Scikit-learn Documentation
- Recommendation System concepts
- Collaborative Filtering resources

---

## 👩‍💻 Author

### Akanksha Singh

**MCA — Computer Applications**  
**National Institute of Technology, Tiruchirappalli**

---

