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

Frequency encoding does not really capture meaningful semantic information from these categories so I decided to treat the sequence of categories from the three columns for each product as a sentence, i.e for 28k products, I will have 28k sentences. They are processed in the following way: <br><br>

1) Use of word2vec algorithm to generate embeddings for each word(category) in these sentences. Main advantage of word2vec here is that it can capture semantical information and generates dense low dimensional representations of words.<br>
2) Finally the embedding for an entire sentence is created as the average of embeddings of the words that make up the sentence.<br>
3) Given a query(product) the criteria for selecting top-k similar products is simply the ***'dot product'*** between the embeddings of the products.<br>

***Note : This can be further improved by filtering out top-k products by generating embeddings out of product descriptions as well, so we can do a sort of a two-step similarity measure technique here.*** <br><br>

### <ins>₹💸 Pricing detection:</ins><br>

To detect an oppurtunity of applying discount thats guided by historical data, we need to form a target variable which indicates wether there is any difference between sale price and market price (1) or not (0) (binary). This can help the e-commerce website to generate potential products to apply discount upon from historical trends, in a way if the past product discounting strategy was yeilding positive impacts such as:
1) Decrease in customer attrition.
2) Increase in product sales.
3) Increase in customer engagement time.
4) Increase in overall revenue. And more.

And if a ML model identifies patterns in the discounting strategy from historical data, we can gain additional insights and assistance by combining :<br>
(Domain knowledge driven discounting strategy + Insights from the ML model)

I trained a XGBoostClassifier with features as : previously generated embeddings, market price and ratings.

## <ins>📊 Results:</ins><br>

|***train metrics***| |
|:------------:|:------------:|
|precision | 0.779259726935522|
|recall | 0.8098089067497745|
|F1 Score |0.7942406692406693|
|validation metrics||
|precision | 0.7480680061823802|
|recall | 0.7973640856672158|
|F1 Score |0.7719298245614036|

