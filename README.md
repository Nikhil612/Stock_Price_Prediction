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
![image](https://user-images.githubusercontent.com/34812655/117249485-7ca9e080-adf6-11eb-8dff-c4bb561b87e3.png)


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

**EMA:
Exponential Moving Average

```
df_aapl["EMA10"] = df_aapl.Close.ewm(span=10, adjust=False).mean()
df_aapl["EMA50"] = df_aapl.Close.ewm(span=50, adjust=False).mean()
df_aapl["EMA100"] = df_aapl.Close.ewm(span=100, adjust=False).mean()
```
![image](https://user-images.githubusercontent.com/34812655/117249539-9519fb00-adf6-11eb-93b9-990d05a0169d.png)


Upper and lower boundary using the concept of Bollinger Bands


```
df_osb = df.iloc[:500]
df_osb["MA20"] = df_osb.Close.rolling(window = 20).mean()
df_osb["std20"] = df_osb.Close.rolling(window = 20).std()
df_osb.dropna(inplace=True)


df_osb["Upper limit"] = df_osb["MA20"] + 2*df_osb["std20"]
df_osb["Lower limit"] = df_osb["MA20"] - 2*df_osb["std20"]

df_osb["Upper limit"].plot()
df_osb["Lower limit"].plot()
df_osb.Close.plot()
```
![image](https://user-images.githubusercontent.com/34812655/117249665-d1e5f200-adf6-11eb-929c-d62a3c7a8f0e.png)


## Creation of Oscillation Box
```
currentAxis=pd.concat([df_osb.Close,df_osb["Lower limit"],df_osb["Upper limit"]],axis=1).plot(figsize=(9,5),grid=True)
plt.title("Oscillation Box Sample")

osc_box(splitdata(df_osb , 100),currentAxis)
```
![image](https://user-images.githubusercontent.com/34812655/117249752-fcd04600-adf6-11eb-890c-58e7a40dd525.png)


**Determining the Buy-Sell of Stocks

### Function Used to define the buy-sell criteria

```
df_bns = df['Close']

MA20 = df_bns.rolling(window=20).mean()
MA20
MA80 = df_bns.rolling(window=80).mean()
MA80

def buy_sell(data):    
    PriceBuy = []
    PriceSell = []
    flag = -1
    for i in range(0,len(data)):
    #if sma30 > sma100  then buy else sell
        if data['MA20'][i] > data['MA80'][i]:
            if flag != 1:
                PriceBuy.append(data['Close'][i])
                PriceSell.append(np.nan)
                flag = 1
            else:
                PriceBuy.append(np.nan)
                PriceSell.append(np.nan)
        #print('Buy')
        elif data['MA20'][i] < data['MA80'][i]:
            if flag != 0:
                PriceSell.append(data['Close'][i])
                PriceBuy.append(np.nan)
                flag = 0
            else:
                PriceBuy.append(np.nan)
                PriceSell.append(np.nan)
        #print('sell')
        else: #Handling nan values
            PriceBuy.append(np.nan)
            PriceSell.append(np.nan)
  
    return (PriceBuy, PriceSell)
```

![image](https://user-images.githubusercontent.com/34812655/117249740-f6da6500-adf6-11eb-83cc-1d956a84dd7f.png)


