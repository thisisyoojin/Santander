# Santander Product Recommendation

The project is from the competition hosted in Kaggle platform by Santander. The aim of the project is to predict products which customer will purchase in future based on customer’s current data. The evaluation method used for this project is Mean Average Precision @ 7 (MAP@7).


-Strategy
There are 24 products to predict but some products are not as popular as others. For this reason, I am aiming to predict only 16 products on.
As the data is time-stamped, I decided to create lagged features for models to see any changes on customers' data.
First, I trained the models with data of customers who newly purchased products, which eliminated too many data to train. I got a hint from the article posted by 1st winner on the forum, so I included data of customers with no additional products as 17th class. Multiple product additions are handled by adding duplicate rows with different targets.


-Features(60)
In the training data, 22 customer features are given. I removed columns with duplicated data, missing more than 90% of data and holding data with 1 standard derivation. For cateogiral features, I tried one-hot-encoding first but it makes data massive and there was no meaningfull improvement on the model's performance. For this reason, I chose to factorize categorical features. All features are listed below.

current customer features (17)
lagged-1 customer features(17)
lagged-1 product features(24)
2 features from fecha_alta(2)


-Models

1. XGBoost: I deisnged the model to target the 16 most popular products and 17th class indicating either no additions or an addition of one of the eight remaining products.

2. LightGBM: Like XGBoost, I designed the model for 17 multi-class classification as well.
LightGBM is key to building these models in an expeditious manner.

3. NN: This model target presence of product in a given month regardless the products are newly purchased or not. It targeted a length 16 vector of the more more popular products and are trained on all customers.product. It has two hidden layers of 512 nodes and drop out layers, and the 16 node output layer.


-The overview of simple-model

Map@7 maximum	: 0.04266
XGBoost		: 0.03609
LightGBM	: 0.03652
NN		: 0.00884


- Conclusion

XGBoos and LightGBM is showing similar performance, but in terms of the time for training, LightGBM shows better performance.
For the neural network model, it seems to need more features the model can engineer feature itself.
It is worth to proceed to create ensemble models with current features to train on different time frames and aggreagate the predictions.


