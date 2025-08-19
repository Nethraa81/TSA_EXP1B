# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19.08.2025

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("India_GDP.csv")

data = data.rename(columns={
    "India GDP - Historical Data": "Year",
    "India GDP - Historical Data.1": "GDP"
})

data["Year"] = pd.to_datetime(data["Year"], errors="coerce")

data.set_index("Year", inplace=True)

data["GDP"] = pd.to_numeric(data["GDP"].astype(str).str.replace(",", ""), errors="coerce")

data['gdp_diff'] = data['GDP'] - data['GDP'].shift(1)

result = seasonal_decompose(data['GDP'].dropna(), model='additive', period=1)
data['gdp_sea_diff'] = result.resid

data['gdp_log'] = np.log(data['GDP'])
data['gdp_log_diff'] = data['gdp_log'] - data['gdp_log'].shift(1)

result = seasonal_decompose(data['gdp_log_diff'].dropna(), model='additive', period=1)
data['gdp_log_sea_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['GDP'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('GDP')

plt.subplot(6, 1, 2)
plt.plot(data['gdp_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('GDP Difference')

plt.subplot(6, 1, 3)
plt.plot(data['gdp_sea_diff'], label='Seasonal Differencing')
plt.legend(loc='best')
plt.title('Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('Residual')

plt.subplot(6, 1, 4)
plt.plot(data['gdp_log'], label='Log Transformed')
plt.legend(loc='best')
plt.title('Log Transform')
plt.xlabel('Year')
plt.ylabel('Log(GDP)')

plt.subplot(6, 1, 5)
plt.plot(data['gdp_log_diff'], label='Log Differencing')
plt.legend(loc='best')
plt.title('Log Differencing')
plt.xlabel('Year')
plt.ylabel('Log GDP Diff')

plt.subplot(6, 1, 6)
plt.plot(data['gdp_log_sea_diff'], label='Log Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('Residual')

plt.tight_layout()
plt.show()
```

### OUTPUT:

Unprocessed Data:
<img width="1666" height="270" alt="Screenshot 2025-08-19 084157" src="https://github.com/user-attachments/assets/eb972bc2-3dba-42b7-8308-cb5eb2015c5b" />

After regular differencing:
<img width="1685" height="264" alt="Screenshot 2025-08-19 084209" src="https://github.com/user-attachments/assets/eaffd2d2-be49-4e45-b0d3-9d6ef3591602" />

After seasonal adjustment:
<img width="1667" height="274" alt="Screenshot 2025-08-19 084221" src="https://github.com/user-attachments/assets/6b605c06-3ee4-4fa9-a8f3-d4e1314e2179" />

After log transformation:
<img width="1630" height="278" alt="image" src="https://github.com/user-attachments/assets/1d0d83be-167b-4653-a0ef-220b46f6b59e" />

After log transformation:
<img width="1672" height="277" alt="Screenshot 2025-08-19 084243" src="https://github.com/user-attachments/assets/86a1c311-542a-40ed-8d8f-44ff13109689" />

 After log transformation, regular differencing and seasonal differencing:
 <img width="1672" height="288" alt="Screenshot 2025-08-19 084308" src="https://github.com/user-attachments/assets/4f09a8e1-9f6d-4a16-a6c2-65b28c787603" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
