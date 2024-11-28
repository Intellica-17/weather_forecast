# weather_forecast
Istanbul Weather Forecast Project
## English
This project aims to use the dataset we created with Istanbul's weather data from November 2024 to forecast December's weather and generate charts based on the predictions. 
### About The Database
- meantemp (°C): Mean Temperature
- humidity (%): Humidity
- windspeed (m/s): Wind Speed
- meanpressure (hPa): Mean Pressure
### Requirements
- Python 3.x
- Jupyter Notebook or JupyterLab
- `numpy`
- `pandas`
- `matplotlib`
- `prophet`
### To install the requried packages:
```bash 
pip install numpy pandas matplotlib prophet notebook
```
### Setup
1. Clone the project repository:
```Bash
git clone <repository-url>
cd weather_forecast
```
2. Install the required libraries:
```Bash
pip install -r requirements.txt
```
### Usage
Run the main script to train and test the model;
1. Run Jupyter from the terminal or command line:
```Bash
jupyter notebook
```
2. In the browser window that opens, find the `.ipynb` file and click on it.
3. Run the cells sequentially to review the analyses and graphs.  
NOTE: Use the Shift + Enter key combination to run the cells in the notebook sequentially.

### Code Explanation
#### Importing Libraries
```Python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from prophet import Prophet
```
#### Loading Data Set
```Python
data = pd.read_csv("ds/istanbul_weather.csv")
data.head() # Allows us to see the first five rows.
```
#### Statistical summary information for numerical data.
```Python
data.describe()
```
#### Getting information about the data.
```Python
data.info()
```
#### Formatting date data.
```Python
data['date'] = pd.to_datetime(data['date'], format='%d-%m-%Y') #Normally, Prophet interprets dates in the year-month-day format, but since our data is in the day-month-year format, we are preparing it accordingly.
```
#### We will adjust the values to make them suitable for Prophet.
```Python
meantemp_data = data[['date', 'meantemp (°C)']].rename(columns= {'date': 'ds', 'meantemp (°C)': 'y'})
humidity_data = data[['date', 'humidity (%)']].rename(columns= {'date': 'ds', 'humidity (%)': 'y'})
windspeed_data = data[['date', 'windspeed (m/s)']].rename( columns= {'date': 'ds', 'windspeed (m/s)': 'y'})
pressure_data = data[['date', 'meanpressure (hPa)']].rename(columns= {'date': 'ds', 'meanpressure (hPa)': 'y'})
```
#### We are creating and training a model for the Average Temperature (meantemp) value.
```Python
meantemp_model = Prophet()
meantemp_model.fit(meantemp_data)
```

#### Generating temperature forecast data for the next 31 days (December).
```Python
meantemp_future = meantemp_model.make_future_dataframe(periods=31)
meantemp_forecast = meantemp_model.predict(meantemp_future)
```

#### Creating a graph with temperature forecast data for December.
```Python
meantemp_model.plot(meantemp_forecast)
plt.title("December Average Temperature Forecasts")
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.show()
```

#### Performing the same steps for humidity forecast data.
```Python
humdity_model = Prophet() # Creating the model.
humdity_model.fit(humidity_data) # Training the model.

# Generating humidity forecast data for the next 31 days (December).
humidity_future = humdity_model.make_future_dataframe(periods= 31) 
humdity_forecast = humdity_model.predict(humidity_future)

# Creating a graph with the data.
humdity_model.plot(humdity_forecast)
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.title("December Humidity Forecasts")
plt.show()
```

#### Performing the same steps for wind speed forecast data.
```Python
windspeed_model = Prophet()
windspeed_model.fit(windspeed_data)

windspeed_future = windspeed_model.make_future_dataframe(periods=31)
windspeed_forecast = windspeed_model.predict(windspeed_future)

windspeed_model.plot(windspeed_forecast)
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.title("December Wind Speed Forecasts")
plt.show()
```

#### Performing the same steps for mean pressure forecast data.
```Python
pressure_model = Prophet()
pressure_model.fit(pressure_data)

pressure_future = pressure_model.make_future_dataframe(periods=31)
pressure_forecast = pressure_model.predict(pressure_future)

pressure_model.plot(pressure_forecast)
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.title("December Average Pressure Forecasts")
plt.show()
```

#### Showing the average data created for December using November data with a line chart.
```Python
plt.figure(figsize=(12, 8)) # We set the graphic size to 12x8 (width and height units are usually in inches).

# Creating a line chart that shows the predicted values of the weather metrics we used over time.
plt.plot(meantemp_forecast['ds'], meantemp_forecast['yhat'], label= 'Temperature Forecast', color= 'red')
plt.plot(humdity_forecast['ds'], humdity_forecast['yhat'], label= 'Humidity Forecast', color='blue')
plt.plot(windspeed_forecast['ds'], windspeed_forecast['yhat'], label= 'Wind Speed Forecast', color= 'green')
plt.plot(pressure_forecast['ds'], pressure_forecast['yhat'], label="Pressure Forecast", color= "purple")

plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31')) # Editing the time interval
plt.title('December Forecasts', fontsize= 16) # Title and font
plt.xlabel('Date', fontsize=12) # Adding a label to the x-axis and adjusting its font.
plt.ylabel('Forecast Value', fontsize=12) #Adding a label to the Y-axis and adjusting its font.
plt.legend() # Labels created for the lines (e.g., Temperature Forecast) are added next to the graph.
plt.grid(True) # Adding a grid to the graph.
plt.show()
``` 


### Contributors  
The contributors to this project are:  
- Elif Nehir OĞUZ
- Cemre YAŞAR

### License
This project is licensed under the [MIT Lisansı](https://opensource.org/licenses/MIT).

### NOTE
In this project, the README file is prepared in both English and Turkish. We used separator lines ('-------------') between sections.
--------------------------------------------------------------------------------------------------------------------------------------------------
## Türkçe
Bu projede, İstanbul 2024 Kasım Ayı hava durumu verileri ile oluşturduğumuz veri setini kullanarak Aralık Ayı hava durumu tahminlemesiyle çizelgeler oluşturmayı amaçladık. 
### Veri Seti Hakkında
- meantemp (°C): Ortalama Hava Tahmini
- humidity (%): Nem
- windspeed (m/s): Rüzgar hızı
- meanpressure (hPa): Ortalama Basınç
### Gereksinimler
- Python 3.x
- Jupyter Notebook veya JupyterLab
- `numpy`
- `pandas`
- `matplotlib`
- `prophet`
#### Gereksinimleri Yüklemek İçin
```Bash
pip install numpy pandas matplotlib prophet notebook
```
### Kurulum
1. Proje dosyalarını indirin:
```Bash
git clone <repository-url>
cd weather_forecast
```
2. Gerekli Kütüphaneleri Yükleyin:
```Bash
pip install -r requirements.txt
```

### Kullanım
Projenin ana dosyasını çalıştırarak modeli eğitip test edebilirsiniz:
1. Terminalden veya komut satırından Jupyter'i çalıştırın;
```Bash
jupyter notebook
```
2. Açılan tarayıcı penceresinde `.ipynb` dosyasını bulun ve üzerine tıklayın.
3. Hücreleri sırasıyla çalıştırarak analizleri ve grafikleri inceleyin:
NOT: Notebook'taki hücreleri sırayla çalıştırmak için Shift + Enter tuş kombinasyonunu kullanabilirsiniz.

### Kod Açıklaması
#### Kütüphaneleri İçe Aktarma
```Python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from prophet import Prophet
```
#### Veri setini yükleme
```Python
data = pd.read_csv("ds/istanbul_weather.csv")
data.head() # ilk beş satırı görmemizi sağlar
```
#### Sayısal verilerle ilgili istatistiksel özet bilgiler
```Python
data.describe()
```
#### Veriler hakkında bilgi edinme
```Python
data.info()
```
#### Tarih verilerini düzenleme
```Python
data['date'] = pd.to_datetime(data['date'], format='%d-%m-%Y') #Normalde Prophet tarihleri yıl-ay-gün olarak algılıyor ancak bizim verilerimiz gün-ay-yıl olacak formatında olduğundan düzenleme yapıyoruz.
```
#### Değerleri, Prophet için uygun hâle getiriyoruz
```Python
meantemp_data = data[['date', 'meantemp (°C)']].rename(columns= {'date': 'ds', 'meantemp (°C)': 'y'})
humidity_data = data[['date', 'humidity (%)']].rename(columns= {'date': 'ds', 'humidity (%)': 'y'})
windspeed_data = data[['date', 'windspeed (m/s)']].rename( columns= {'date': 'ds', 'windspeed (m/s)': 'y'})
pressure_data = data[['date', 'meanpressure (hPa)']].rename(columns= {'date': 'ds', 'meanpressure (hPa)': 'y'})
```
#### Ortalama Sıcaklık (meantemp) değeri için model oluşturup eğitiyoruz;
```Python
meantemp_model = Prophet()
meantemp_model.fit(meantemp_data)
```

#### Gelecek 31 Gün (Aralık Ayı) için sıcaklık tahmin verisi oluşturma
```Python
meantemp_future = meantemp_model.make_future_dataframe(periods=31)
meantemp_forecast = meantemp_model.predict(meantemp_future)
```

#### Aralık Ayı için sıcaklık tahmin verileri ile grafik oluşturma
```Python
meantemp_model.plot(meantemp_forecast)
plt.title("December Average Temperature Forecasts")
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.show()
```

#### Aynı işlemleri nem değerleri tahmin verileri için oluşturma
```Python
humdity_model = Prophet() # model oluşturma
humdity_model.fit(humidity_data) #model eğitme

# Gelecek 31 Gün (Aralık Ayı) için nem verisi oluşturma
humidity_future = humdity_model.make_future_dataframe(periods= 31) 
humdity_forecast = humdity_model.predict(humidity_future)

# verilerle grafik oluşturma
humdity_model.plot(humdity_forecast)
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.title("December Humidity Forecasts")
plt.show()
```

#### Aynı işlemleri rüzgar hızı değerleri tahmin verileri için oluşturma
```Python
windspeed_model = Prophet()
windspeed_model.fit(windspeed_data)

windspeed_future = windspeed_model.make_future_dataframe(periods=31)
windspeed_forecast = windspeed_model.predict(windspeed_future)

windspeed_model.plot(windspeed_forecast)
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.title("December Wind Speed Forecasts")
plt.show()
```

#### Aynı işlemleri ortalama basınç değerleri tahmin verileri için oluşturma
```Python
pressure_model = Prophet()
pressure_model.fit(pressure_data)

pressure_future = pressure_model.make_future_dataframe(periods=31)
pressure_forecast = pressure_model.predict(pressure_future)

pressure_model.plot(pressure_forecast)
plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31'))
plt.title("December Average Pressure Forecasts")
plt.show()
```

#### Kasım ayı verilerinden yararlanılarak Aralık ayı için oluşturulan ortalama verilerin çizgi grafiği ile gösterilmesi
```Python
plt.figure(figsize=(12, 8)) #Grafik boyutu 12x8 olacak şekilde ayarladık (genişlik ve yükseklik birimleri genellikle inç cinsindendir).

#kullandığımız hava durumu ölçütlerinin tahmin edilen değerlerini zamana karşı gösteren bir çizgi grafiğinin oluşturulması;
plt.plot(meantemp_forecast['ds'], meantemp_forecast['yhat'], label= 'Temperature Forecast', color= 'red')
plt.plot(humdity_forecast['ds'], humdity_forecast['yhat'], label= 'Humidity Forecast', color='blue')
plt.plot(windspeed_forecast['ds'], windspeed_forecast['yhat'], label= 'Wind Speed Forecast', color= 'green')
plt.plot(pressure_forecast['ds'], pressure_forecast['yhat'], label="Pressure Forecast", color= "purple")

plt.xlim(pd.to_datetime('2024-12-01'), pd.to_datetime('2024-12-31')) #zaman aralığının düzenlenmesi
plt.title('December Forecasts', fontsize= 16) #başlık ve font
plt.xlabel('Date', fontsize=12) # x eksenine etiket ekleme, fontunu ayarlama
plt.ylabel('Forecast Value', fontsize=12) # y eksenine etiket ekleme, fontu ayarlama
plt.legend() # Çizgiler için oluşturulan etiketler (örneğin, Sıcaklık Tahmini) grafiğin yanına eklenir.
plt.grid(True) # Grafikte bir ızgara (grid) ekler.
plt.show()
``` 


### Katkıda Bulunanlar
Bu projede katkıda bulunanlar:
- Elif Nehir OĞUZ
- Cemre YAŞAR

### Lisans
Bu proje [MIT Lisansı](https://opensource.org/licenses/MIT) altında lisanslanmıştır.

### NOT
Bu projede, README dosyası hem İngilizce hem de Türkçe olarak iki dilde hazırladık. Bölümler arasında ayırıcı çizgiler ('-------------') kullandık.
