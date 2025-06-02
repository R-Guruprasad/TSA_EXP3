### DEVELOPED BY: R Guruprasad
### REGISTER NO: 212222240033
### DATE:

# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Load the india's gdp data
file_path = 'india-gdp.csv'  # Ensure this is the correct path to your CSV file
gdp_data = pd.read_csv(file_path,nrows=50)


# Extract the 'AnnualChange' column (Change data)
change_data = gdp_data['AnnualChange'].values

# Calculate mean and variance
mean_change = np.mean(change_data)
var_change = np.var(change_data)


# Normalize the data (subtract mean and divide by standard deviation)
normalized_change = (change_data - mean_change) / np.sqrt(var_change)

# Compute the ACF for the first 35 lags
def compute_acf(data, max_lag):
    acf_values = []
    n = len(data)
    for lag in range(max_lag + 1):
        if lag == 0:
            acf_values.append(1)  # ACF at lag 0 is always 1
        else:
            acf = np.corrcoef(data[:-lag], data[lag:])[0, 1]
            acf_values.append(acf)
    return acf_values

lags = range(35)
acf_values = compute_acf(normalized_change, 34)

# Plot the ACF results
plt.figure(figsize=(10, 6))
plt.stem(lags, acf_values, use_line_collection=True)
plt.title('Autocorrelation Function (ACF) for India"s GDP')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```
### OUTPUT:

![Screenshot 2024-09-13 092857](https://github.com/user-attachments/assets/6a2072a1-d4aa-4f59-9597-96a4ac7bfa38)

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
