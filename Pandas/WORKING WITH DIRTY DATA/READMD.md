# Описание
Данные имеют следующую структуру:

* записываются для каждого пользователя, совершившего покупки, каждый день
* для каждой даты есть своя папка, внутри неё – папки для каждого пользователя
* внутри каждой папки есть файл data.csv, где и хранятся данные

Например, 30 декабря три покупателя сделали покупки, 31 – два 
(папки 2020-12-30 и 2020-12-31 соответственно). Поскольку клиент FirstName_LastName1 купил товары в оба дня, для него имеется папка в папке для каждой из дат. Для других клиентов – по одной.

Note: данные в задании покрывают другой временной период, имена тоже другие. Подробности, примеры и возможные подсказки можно найти в текстах следующих шагов.

      

# Задачи
1. Соберите все данные из папки data в один датафрэйм, имеющий следующие столбцы: колонки из самих файлов (product_id, quantity), а также имя пользователя (name), и дата этих покупок (date), соответствует названию папки, где лежит папка с пользователем)
2. Выясните, какой пользователь купил больше всего товаров. Если их несколько, то перечислите имена через запятую с пробелом и в алфавитном порядке.
3. Найдите топ-10 товаров по числу проданных единиц за всё время и постройте барплот. Сколько было продано единиц товара с product_id==56?
4. Визуализируйте продажи по дням.
5. Сколько пользователей приобрели какой-либо товар повторно (более 1 раза)? Повтором будем считать покупку товара с одинаковым product_id, совершенную в разные дни. 


```python
import os
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
os.listdir('/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Alexey_Fedorov')
```




    ['data.csv']




```python
pd.read_csv('/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Alexey_Fedorov/data.csv')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>product_id</th>
      <th>quantity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>73</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>34</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>71</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>18</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>67</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
os.walk(path)
```




    <generator object walk at 0x7f2b2c4dcb10>




```python

```


```python
for dd in os.walk(path):
    d = dd[0]
    print('d is',d)
```

    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05/Petr_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05/Petr_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05/Rostislav_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05/Kirill_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05/Alexey_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-05/Alexey_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Petr_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Rostislav_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Kirill_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Alexey_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-08/Anton_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Alexey_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Anton_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Rostislav_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Anton_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Anton_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Petr_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-09/Vasiliy_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Kirill_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Alexey_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Rostislav_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Petr_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Rostislav_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Petr_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Rostislav_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Petr_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-04/Vasiliy_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-06
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-06/Vasiliy_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03/Alexey_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03/Anton_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03/Vasiliy_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03/Kirill_Petrov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03/Petr_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-03/Vasiliy_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Kirill_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Alexey_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Rostislav_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Alexey_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Petr_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Alexey_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Anton_Smirnov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Anton_Ivanov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Petr_Fedorov
    d is /mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data/2020-12-07/Vasiliy_Ivanov



```python
path = '/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data'
```


```python
path_parts = '/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/hom,s..eworks/python_ds_miniprojects/4/data/2020-12-05/Petr_Smirnov'.split('/')
name=path_parts[-1]
date=path_parts[-2]
```


```python
#create df for of data 
df = pd.DataFrame()
#read data from file
for triple in os.walk(path):
    current_path = triple[0]
    dirs = triple[1]
    file = triple[2]
    for file in file:
        #полный путь к файлу
        #print('current_path is',current_path)
        data_path = (f'{current_path}/{file}')
        #считываем файл
        temp_df = pd.read_csv(data_path)
        #name date
        path_parts = current_path.split('/')
        name=path_parts[-1]
        date=path_parts[-2]
        temp_df['date'] = date
        temp_df['name'] = name
        #объединем дф
        df = pd.concat((df, temp_df))

```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>product_id</th>
      <th>quantity</th>
      <th>date</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>27</td>
      <td>4</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>89</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>33</td>
      <td>2</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>8</td>
      <td>3</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>16</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>18</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>94</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>95</td>
      <td>2</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>83</td>
      <td>3</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>64</td>
      <td>1</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
  </tbody>
</table>
<p>161 rows × 5 columns</p>
</div>




```python
df.drop(columns = ['Unnamed: 0'], inplace = True)
```


```python
df.reset_index(drop = True, inplace = True)
```


```python
df.quantity.sum()
```




    480




```python
from pathlib import Path
```


```python
path = '/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data'
```


```python
path =Path('/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data')
```


```python
path
```




    PosixPath('/mnt/HC_Volume_18315164/home-jupyter/jupyter-d.gordeev-13/shared/homeworks/python_ds_miniprojects/4/data')




```python
#create df for of data 
df = pd.DataFrame()
#read data from file
for triple in os.walk(path):
    current_path = triple[0]
    dirs = triple[1]
    file = triple[2]
    for file in file:
        x = Path(current_path) / file
        #считываем файл
        temp_df = pd.read_csv(x)
        #name date
        #x = current_path.split('/')
        name=x.parts[-2]
        date=x.parts[-3]
        temp_df['date'] = date
        temp_df['name'] = name
        #объединем дф
        df = pd.concat((df, temp_df))
```


```python
x.parts[-1]
```




    'data.csv'




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>product_id</th>
      <th>quantity</th>
      <th>date</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>27</td>
      <td>4</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>89</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>33</td>
      <td>2</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>8</td>
      <td>3</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>16</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>18</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>94</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>95</td>
      <td>2</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>83</td>
      <td>3</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>64</td>
      <td>1</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
  </tbody>
</table>
<p>161 rows × 5 columns</p>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product_id</th>
      <th>quantity</th>
      <th>date</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>27</td>
      <td>4</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>89</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>33</td>
      <td>2</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>3</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>156</th>
      <td>18</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>157</th>
      <td>94</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>158</th>
      <td>95</td>
      <td>2</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>159</th>
      <td>83</td>
      <td>3</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>160</th>
      <td>64</td>
      <td>1</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
  </tbody>
</table>
<p>161 rows × 4 columns</p>
</div>




```python
df.groupby('name', as_index = False) \
  .agg({'quantity':'sum'}) \
  .sort_values('quantity' , ascending = False) \

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>quantity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Alexey_Smirnov</td>
      <td>52</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Petr_Smirnov</td>
      <td>52</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Anton_Smirnov</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Petr_Fedorov</td>
      <td>34</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Kirill_Fedorov</td>
      <td>28</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Rostislav_Petrov</td>
      <td>28</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Vasiliy_Ivanov</td>
      <td>27</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Alexey_Fedorov</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Anton_Ivanov</td>
      <td>23</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Petr_Ivanov</td>
      <td>21</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Anton_Petrov</td>
      <td>18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kirill_Smirnov</td>
      <td>17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alexey_Ivanov</td>
      <td>17</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Rostislav_Smirnov</td>
      <td>17</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Rostislav_Fedorov</td>
      <td>16</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Vasiliy_Fedorov</td>
      <td>15</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Petr_Petrov</td>
      <td>14</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Kirill_Petrov</td>
      <td>9</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Rostislav_Ivanov</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alexey_Petrov</td>
      <td>7</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Vasiliy_Petrov</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = df.groupby('product_id', as_index = False) \
  .agg({'quantity':'sum'}) \
  .sort_values('quantity' , ascending = False) \
  .head(10)
```


```python
sns.barplot(data = df1, x='product_id', y='quantity')

```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f2b07575908>




![png](output_24_1.png)



```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product_id</th>
      <th>quantity</th>
      <th>date</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>27</td>
      <td>4</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>89</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>33</td>
      <td>2</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>3</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>156</th>
      <td>18</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>157</th>
      <td>94</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>158</th>
      <td>95</td>
      <td>2</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>159</th>
      <td>83</td>
      <td>3</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>160</th>
      <td>64</td>
      <td>1</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
  </tbody>
</table>
<p>161 rows × 4 columns</p>
</div>




```python
sell = df.groupby('date', as_index = False) \
  .agg({'quantity':'sum'}) \
  .sort_values('date') 
```


```python
plt.figure(figsize=(10, 6.5))
sns.barplot(data = sell, x='date', y='quantity')


```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f2b072caa58>




![png](output_27_1.png)



```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product_id</th>
      <th>quantity</th>
      <th>date</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>27</td>
      <td>4</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>1</th>
      <td>89</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>2</th>
      <td>33</td>
      <td>2</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>3</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>1</td>
      <td>2020-12-05</td>
      <td>Petr_Ivanov</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>156</th>
      <td>18</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>157</th>
      <td>94</td>
      <td>4</td>
      <td>2020-12-07</td>
      <td>Petr_Fedorov</td>
    </tr>
    <tr>
      <th>158</th>
      <td>95</td>
      <td>2</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>159</th>
      <td>83</td>
      <td>3</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
    <tr>
      <th>160</th>
      <td>64</td>
      <td>1</td>
      <td>2020-12-07</td>
      <td>Vasiliy_Ivanov</td>
    </tr>
  </tbody>
</table>
<p>161 rows × 4 columns</p>
</div>




```python
df.groupby(['name' , 'product_id']) \
  .agg({'date':pd.Series.nunique}) \
 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>date</th>
    </tr>
    <tr>
      <th>name</th>
      <th>product_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Alexey_Fedorov</th>
      <th>13</th>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1</td>
    </tr>
    <tr>
      <th>34</th>
      <td>1</td>
    </tr>
    <tr>
      <th>50</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Vasiliy_Ivanov</th>
      <th>83</th>
      <td>1</td>
    </tr>
    <tr>
      <th>94</th>
      <td>1</td>
    </tr>
    <tr>
      <th>95</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Vasiliy_Petrov</th>
      <th>27</th>
      <td>1</td>
    </tr>
    <tr>
      <th>78</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>158 rows × 1 columns</p>
</div>




```python

```
