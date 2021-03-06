![AppVeyor](https://img.shields.io/appveyor/build/yu3ufff/emeraldml)
![Codacy grade](https://img.shields.io/codacy/grade/69671d82450949409d1bb72aaf750dcc)
![PyPI](https://img.shields.io/pypi/v/emeraldml?color=informational)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/emeraldml)
![PyPI - License](https://img.shields.io/pypi/l/emeraldml?color=informational)

<img src="emeraldml.png" alt="EmeraldML logo" class="center" width="200"/>

# EmeraldML
A machine learning library for streamlining the process of  
(1) cleaning and splitting data,  
(2) training, optimizing, and testing various models based on the task, and  
(3) scoring and ranking them  
during the exploratory phase for an elementary analysis of which models perform better for a specific dataset. 

## Installation
### Dependencies
- Python (>= 3.7)
- NumPy (>= 1.21.2)
- pandas (>= 1.3.3)
- scikit-learn (>= 0.24.2)
- statsmodels (>= 0.12.2)

### User installation
```
pip install emeraldml
```

## Development
### Source code
You can check the latest sources with the command:
```
git clone https://github.com/yu3ufff/emeraldml.git
```

## Demo
**Getting the data**:
```python
import pandas as pd
audi = pd.read_csv('audi.csv')
audi.head()
```
```
|    | model   |   year |   price | transmission   |   mileage | fuelType   |   tax |   mpg |   engineSize |
|---:|:--------|-------:|--------:|:---------------|----------:|:-----------|------:|------:|-------------:|
|  0 | A1      |   2017 |   12500 | Manual         |     15735 | Petrol     |   150 |  55.4 |          1.4 |
|  1 | A6      |   2016 |   16500 | Automatic      |     36203 | Diesel     |    20 |  64.2 |          2   |
|  2 | A1      |   2016 |   11000 | Manual         |     29946 | Petrol     |    30 |  55.4 |          1.4 |
|  3 | A4      |   2017 |   16800 | Automatic      |     25952 | Diesel     |   145 |  67.3 |          2   |
|  4 | A3      |   2019 |   17300 | Manual         |      1998 | Petrol     |   145 |  49.6 |          1   |
```

**Using EmeraldML**:
```python
import emerald
from emerald.boa import RegressionBoa

rboa = RegressionBoa(random_state=3)
rboa.hunt(data=audi, target='price')
rboa.ladder
```
```
[(OptimalRFRegressor, 0.9624889664024406),
 (OptimalDTRegressor, 0.9514992411732952),
 (OptimalKNRegressor, 0.9511411883559433),
 (OptimalLinearRegression, 0.8876961846248467),
 (OptimalABRegressor, 0.8491539140007975)]
```
```python
for i in range(len(rboa)):
    print(rboa.model(i))
```
```
RandomForestRegressor(min_samples_split=5, n_estimators=500, random_state=3)
DecisionTreeRegressor(max_depth=15, min_samples_split=10, random_state=3)
KNeighborsRegressor(n_neighbors=3, p=1)
LinearRegression()
AdaBoostRegressor(learning_rate=0.1, n_estimators=100, random_state=3)
```

