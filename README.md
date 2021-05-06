# Stock_Price_Prediction



## Reading DataSet

![image](https://user-images.githubusercontent.com/34812655/117249060-d067fa00-adf5-11eb-947c-157b19e364cb.png)

## Displaying Dataset

![image](https://user-images.githubusercontent.com/34812655/117249165-fe4d3e80-adf5-11eb-81e8-2543476fdff2.png)

## Calculating Following parameters like:-

**MA - Moving Average
It is a used to analyze data points by creating a series of averages of different subsets of full data set. It smooths out price trends by filtering out the noise from random short-term price fluctuations

```
df_aapl["MA20"] = df_aapl.Close.rolling(window=20).mean()

df_aapl.Close.plot()
df_aapl.MA20.plot()
plt.title("Moving Average")
plt.show()
```

**SMA
Simple Moving Average

```
df_aapl["SMA5"]  = df_aapl.Close.rolling(window=5).mean()
df_aapl["SMA10"] = df_aapl.Close.rolling(window=10).mean()
df_aapl["SMA50"] = df_aapl.Close.rolling(window=50).mean()
df_aapl["SMA100"] = df_aapl.Close.rolling(window=100).mean()
df_aapl["SMA500"] = df_aapl.Close.rolling(window=500).mean()
```
![image](https://user-images.githubusercontent.com/34812655/117249434-6e5bc480-adf6-11eb-919d-1afb091d8967.png)
