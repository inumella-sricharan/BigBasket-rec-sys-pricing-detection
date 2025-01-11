# BigBasket-rec-sys-pricing-detection
 Making a content based recommendation system for BigBasket dataset of 28k products. ML Model to predict change in pricing.

## <ins>👉 Intro:</ins><br>

This project is made primarily for the following tasks that can be performed on e-commerce products data:
1) Building a content based recommender system to showcase similar set of products based on the current product selected by the user.
2) Based on historical data of sale price and market price, detecting the opportunity of imposing discount on a certain product using machine learning. <br><br>

## <ins>🛠️ Approach:</ins><br><br>
### <ins>🗂️ Recommender System:</ins><br>
To build a recommender system in this scenario, I made use of the categorical information present in the columns : 'category', 'sub-category' and 'type'.<br>
Due to the high-cardinality nature of these columns, technqiues other than simple one-hot encoding are needed.<br>
Frequency encoding does not really capture meaningful semantic information from these categories so I decided to treat the sequence of categories from the three columns for each product as a sentence, i.e for 28k products, I will have 28k sentences. <br>
Now I can make use of word2vec algorithm to generate embeddings for each word(category) in these sentences.
main advantage of word2vec is that it can capture semantical information, generates dense low dimensional representations of words.

Finally the embedding for an entire sentence is created as the average of embeddings of the words that make up the sentence.

given a query(product) the criteria for selecting top-k similar products is simply the ***'dot product'*** between the embeddings of the products.


Note : This can be further improved by filtering out top-k products by generating embeddings out of product descriptions as well, so we can do a sort of a two-step similarity measure technique here.

### <ins>₹💸🇮🇳 Pricing detection:</ins><br>

To detect an oppurtunity of discount thats guided by historical data, we need to form a target variable which indicates wether there is any difference between sale price and market price (1) or not (0) (binary). 

Then I chose to train a XGBoostClassifier with features as the previously generated embeddings, along with market price and ratings.

Attach the results here.
