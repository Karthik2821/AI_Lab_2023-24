# Ex.No: 13 Machine Learning – Mini Project
### DATE:  24/10/2024                                                            
### REGISTER NUMBER : 212221040018
### AIM: 
To write a program to train the classifier for Movie Recommendation System.
###  Algorithm:
1. Collect the data about movies and users.
2. Clean and prepare the data and build a user-item interaction matrix.
3. Generate features for users and movies and apply techniques like TF-IDF (for movie descriptions) or embeddings.
4. Use Collaborative Filtering recommendation model for user-based and item-based.
5. Evaluate the system and tune the model.

### Program:
```
!pip install scikit-surprise
import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
from surprise import Dataset, Reader, SVD
from surprise.model_selection import train_test_split
ratings = pd.read_csv('u.data', sep='\t', names=['userId', 'movieId', 'rating', 'timestamp'])
movies = pd.read_csv('u.item', sep='|', names=['movieId', 'title', 'release_date', 'video_release_date', 'IMDb_URL', 'unknown', 'Action', 'Adventure', 'Animation',
                                               'Children', 'Comedy', 'Crime', 'Documentary', 'Drama', 'Fantasy', 'Film-Noir', 'Horror', 'Musical', 'Mystery', 'Romance',
                                               'Sci-Fi', 'Thriller', 'War', 'Western'], encoding='latin-1')
reader = Reader(rating_scale=(1, 5))
data_cf = Dataset.load_from_df(data[['userId', 'movieId', 'rating']], reader)
trainset, testset = train_test_split(data_cf, test_size=0.2)
svd = SVD()
svd.fit(trainset)
movies['genres'] = movies[genre_columns].dot(movies[genre_columns].columns + " ")
movies[['title', 'genres']].head()
tfidf = TfidfVectorizer(stop_words='english')
tfidf_matrix = tfidf.fit_transform(movies['genres'])
def get_recommendations(title, cosine_sim=cosine_sim):
    idx = movies[movies['title'] == title].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    sim_scores = sim_scores[1:11]  # Get top 10 similar movies
    movie_indices = [i[0] for i in sim_scores]
    return movies['title'].iloc[movie_indices]
def get_recommendations(title, cosine_sim=cosine_sim):
    # Make the title matching case-insensitive
    title_matches = movies[movies['title'].str.contains(title, case=False)]

    if title_matches.empty:
        return f"Movie '{title}' not found in the dataset."
print("Recommendations for 'Toy Story':")
print(get_recommendations('Toy Story'))
```


### Output:
![movies colab 1](https://github.com/user-attachments/assets/b09f48ba-fbdc-408f-9237-c0b02ceafad8)

![movies colab 2](https://github.com/user-attachments/assets/a10db842-7c9e-4426-82ad-af61e1e1a48a)

![movies colab 3](https://github.com/user-attachments/assets/bd77a80a-e4e0-4d8c-bb78-d5cd89d10b22)


### Result:
Thus the system was trained successfully and the prediction was carried out.
