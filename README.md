# Stock OHLC Prediction with LSTM

This project uses a Long Short-Term Memory (LSTM) model to predict the next 30-minute OHLC (Open, High, Low, Close) values for stock market data. The code is designed to process historical stock data, clean and scale the features, and predict the next 30-minute OHLC values based on the past 20 candles.

## Requirements

Before running the code, you need to install the following Python libraries:

- pandas
- numpy
- sklearn
- tensorflow
- matplotlib

You can install them using pip:

```bash
pip install pandas numpy scikit-learn tensorflow matplotlib
```

## Dataset

The dataset should be in Excel format with the following columns:
- **time**: Timestamp of each data entry (in format `DD MMM YY HH:MM AM/PM`).
- **open**: The opening price of the stock.
- **high**: The highest price of the stock.
- **low**: The lowest price of the stock.
- **close**: The closing price of the stock.
- **Volume**: The trading volume in a readable format (e.g., '1K', '1M', '1B').

### Note:
The code assumes that the dataset is stored in an Excel file named `MARUTI-OHLC-30min-Data-20Mar2025(3.15PM)-28Apr2025(3.15PM).xlsx`. You may need to adjust the file name if you're using a different dataset.

## Steps:

1. **Load Data**:
   - The data is loaded from an Excel file and parsed. The timestamp column is converted to a pandas `datetime` format.

2. **Clean Data**:
   - The `Volume` column values are cleaned and converted to numeric format (K/M/B notation to actual numbers).

3. **Scaling**:
   - MinMax scaling is applied to the feature columns (`open`, `high`, `low`, `close`, `Volume`) to normalize the data between 0 and 1.

4. **Create Sequences**:
   - Sequences of 20 past candles are created to predict the next 1 candle. These sequences are used as input for the LSTM model.

5. **Train/Test Split**:
   - The dataset is split into training (80%) and testing (20%) sets.

6. **Model Training**:
   - An LSTM model with 64 units in the LSTM layer, a Dense layer with 32 units, and a final output layer predicting the OHLC values is built and trained.

7. **Evaluation**:
   - The model is evaluated on the test data, and the Mean Squared Error (MSE) is printed.

8. **Prediction**:
   - The model predicts the next 30-minute OHLC values based on the latest 20 candles in the data.
   
9. **Inverse Scaling**:
   - The predicted values are inverse transformed back to the original scale using the same scaler used during the preprocessing.

10. **Output**:
    - The predicted OHLC values are printed along with the predicted date and time.

## Example Output

The model will output a prediction for the next 30-minute candle:

```
Predicted Date & Time: 28 Apr 25 01:15 PM
Predicted Open  : 0.77
Predicted High  : 0.74
Predicted Low   : 0.81
Predicted Close : 0.80
```
