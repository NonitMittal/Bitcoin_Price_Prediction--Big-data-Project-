# Course Project - Big Data Engineering

## Objective

The aim of this project has been to experiment in the field of big data which we accomplished by using [Binance Websocket](https://github.com/binance/binance-spot-api-docs/blob/master/web-socket-streams.md) to get real-time BITCOIN data and then applied ensemble method to train the chunked data based on the following models:

-   [Linear Regression](https://www.javatpoint.com/linear-regression-in-machine-learning)
-   [Support Vector Regressor](https://www.javatpoint.com/machine-learning-support-vector-machine)
-   [Random Forest](https://www.javatpoint.com/machine-learning-random-forest-algorithm)
-   [K-Nearest Neighbors](https://www.analyticsvidhya.com/blog/2018/08/k-nearest-neighbor-introduction-regression-python/)
-   [Classification and Regression Tree (CART)](https://www.analyticssteps.com/blogs/classification-and-regression-tree-cart-algorithm)

## Project FLow

The project has been carried out using the following steps:

-   **Data Collection** :
    -   First the Klines Data is collected from [Binance.client](https://python-binance.readthedocs.io/en/latest/) in '1m' interval of last3 years.
    -   The collected data is saved [BTCUSDT_1m.csv](https://github.com/NonitMittal/Bitcoin_Price_Prediction-BigDataProject/blob/master/data/BTCUSDT_1m.csv)
-   **Model Training**
    -   Now different [regressor models](https://github.com/NonitMittal/Bitcoin_Price_Prediction-BigDataProject/tree/master/models/Notebooks) are trained for the above collected data.
    -   And [trained models](https://github.com/NonitMittal/Bitcoin_Price_Prediction-BigDataProject/tree/master/models/Trained) are saved for future reference.
-   **Data Streaming**
    -   The [websocket of Binance](https://github.com/binance/binance-spot-api-docs/blob/master/web-socket-streams.md) is set up to collect the Bitcoin(USDT) KLines data in '1m' timeframe.
    -   Now window of bufferInterval(15) is created by data coming from the websocket, and saved this window as bufferData in [csv file](https://github.com/NonitMittal/Bitcoin_Price_Prediction-BigDataProject/blob/master/data/Buffer_15.csv).
-   **Ensembling of Models**
    -   Now bufferData if first ensembled using [Voting Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.VotingRegressor.html) with the models trained and then fitted with training data of buffer
    -   Then this ensembled model is again ensembled with previously [saved Ensembled Model](https://github.com/NonitMittal/Bitcoin_Price_Prediction-BigDataProject/blob/master/models/Ensembled/EnsembleModel.sav).
    -   Now this model is saved (overwrite the saved Ensembled model.
-   The process of Data Streaming and Ensembling is carried out in different [threads](https://docs.python.org/3/library/threading.html#) so that both process keep running at the same time.

## File Structure Breakdown

```output
.
|   .env                                # variables for Binance.client
|   .gitattributes
|   .gitignore
|   DataCollection.ipynb                # to collect data from Binance.client
|   DataDescription.ipynb               # to describe the data collected (EDA)
|   README.md
|   Steaming_Ensembling.ipynb           # to stream and ensemble data
|---data
|       BTCUSDT_1h.csv
|       BTCUSDT_1m.csv                  # data collected from Binance.client
|       BTCUSDT_2h.csv
|       Buffer_15.csv                   # buffer Data created by Streaming
|---log
|       ensemble.log                    # logs generated while ensemble model training
|       stream.log                      # logs generated while data streaming
|---models
    |---Ensembled
    |       EnsembleModel.sav           # updated ensembled model after every window created
    |---Notebooks                       # notebook files for individual model by their names
    |       CART_Modelling.ipynb
    |       GRU_Modelling.ipynb
    |       KNN_Modelling.ipynb
    |       LinearRegression_Modelling.ipynb
    |       LSTM_Modelling.ipynb
    |       RandomForest_Modelling.ipynb
    |       SVR_Modelling.ipynb
    |       XGBoost_Modelling.ipynb
    |---Trained                         # model trained on collected data saved
        |   CART_Model.sav
        |   KNN_Model.sav
        |   LinearRegression_Model.sav
        |   RandomForest_Model.sav
        |   XGBoost_Model.sav
        |---GRU_Model.sav
        |---LSTM_Model.sav
```

---

Finish
