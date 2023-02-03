---
layout: default
title: Pandas - Part 2
parent: Prerequisites
nav_order: 2
has_children: false
permalink: /lectures/Prerequisites/prerequisites/pandas
---




## Pandas GroupBy Operations

### Understanding GroupBy objects


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv")
```


```python
titanic.head()
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>deck</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>C</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.tail()
```


```python
titanic.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 9 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   survived  891 non-null    int64  
     1   pclass    891 non-null    int64  
     2   sex       891 non-null    object 
     3   age       714 non-null    float64
     4   sibsp     891 non-null    int64  
     5   parch     891 non-null    int64  
     6   fare      891 non-null    float64
     7   embarked  889 non-null    object 
     8   deck      203 non-null    object 
    dtypes: float64(2), int64(4), object(3)
    memory usage: 62.8+ KB
    


```python
titanic_slice = titanic.iloc[:10, [2,3]]
```


```python
titanic_slice
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>male</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>male</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>male</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>male</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>female</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>female</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_slice.groupby("sex")
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x0000027661634B20>




```python
gbo = titanic_slice.groupby("sex")
```


```python
type(gbo)
```




    pandas.core.groupby.generic.DataFrameGroupBy




```python
gbo.groups
```




    {'female': [1, 2, 3, 8, 9], 'male': [0, 4, 5, 6, 7]}




```python
l = list(gbo)
```


```python
l
```




    [('female',
            sex   age
      1  female  38.0
      2  female  26.0
      3  female  35.0
      8  female  27.0
      9  female  14.0),
     ('male',
          sex   age
      0  male  22.0
      4  male  35.0
      5  male   NaN
      6  male  54.0
      7  male   2.0)]




```python
len(l)
```




    2




```python
l[0]
```




    ('female',
           sex   age
     1  female  38.0
     2  female  26.0
     3  female  35.0
     8  female  27.0
     9  female  14.0)




```python
type(l[0])
```




    tuple




```python
l[0][0]
```




    'female'




```python
l[0][1]
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>female</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>female</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(l[0][1])
```




    pandas.core.frame.DataFrame




```python
l[1]
```




    ('male',
         sex   age
     0  male  22.0
     4  male  35.0
     5  male   NaN
     6  male  54.0
     7  male   2.0)




```python
titanic_slice.loc[titanic_slice.sex == "female"]
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>female</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>female</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_slice_f = titanic_slice.loc[titanic_slice.sex == "female"]
titanic_slice_f
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>female</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>female</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_slice_m = titanic_slice.loc[titanic_slice.sex == "male"]
titanic_slice_m
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>male</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>male</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>male</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>male</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_slice_f.equals(l[0][1])
```




    True




```python
for element in gbo:
    print(element[1])
```

          sex   age
    1  female  38.0
    2  female  26.0
    3  female  35.0
    8  female  27.0
    9  female  14.0
        sex   age
    0  male  22.0
    4  male  35.0
    5  male   NaN
    6  male  54.0
    7  male   2.0
    


```python

```

### Splitting with many Keys


```python
import pandas as pd
```


```python
summer = pd.read_csv("summer.csv")
```


```python
summer.head()
```


```python
summer.info()
```


```python
summer.Country.nunique()
```




    147




```python
split1 = summer.groupby("Country")
```


```python
l = list(split1)
l
```




    [('AFG',
             Year     City      Sport Discipline           Athlete Country Gender  \
      28965  2008  Beijing  Taekwondo  Taekwondo  NIKPAI, Rohullah     AFG    Men   
      30929  2012   London  Taekwondo  Taekwondo  NIKPAI, Rohullah     AFG    Men   
      
                  Event   Medal  
      28965     - 58 KG  Bronze  
      30929  58 - 68 KG  Bronze  ),
     ('AHO',
             Year   City    Sport Discipline          Athlete Country Gender  \
      19323  1988  Seoul  Sailing    Sailing  BOERSMA, Jan D.     AHO    Men   
      
                           Event   Medal  
      19323  Board (Division Ii)  Silver  ),
     ('ALG',
             Year         City      Sport Discipline               Athlete Country  \
      17060  1984  Los Angeles     Boxing     Boxing        ZAOUI, Mohamed     ALG   
      17064  1984  Los Angeles     Boxing     Boxing      MOUSSA, Mustapha     ALG   
      19874  1992    Barcelona  Athletics  Athletics    BOULMERKA, Hassiba     ALG   
      20200  1992    Barcelona     Boxing     Boxing       SOLTANI, Hocine     ALG   
      21610  1996      Atlanta  Athletics  Athletics   MORCELI, Nourredine     ALG   
      21946  1996      Atlanta     Boxing     Boxing       SOLTANI, Hocine     ALG   
      21960  1996      Atlanta     Boxing     Boxing       BAHARI, Mohamed     ALG   
      23536  2000       Sydney  Athletics  Athletics  MERAH-BENIDA, Nouria     ALG   
      23624  2000       Sydney  Athletics  Athletics       SAIDI-SIEF, Ali     ALG   
      23631  2000       Sydney  Athletics  Athletics   SAID GUERNI, Djabir     ALG   
      23655  2000       Sydney  Athletics  Athletics  HAMMAD, Abderrahmane     ALG   
      23890  2000       Sydney     Boxing     Boxing      ALLALOU, Mohamed     ALG   
      28602  2008      Beijing       Judo       Judo        HADDAD, Soraya     ALG   
      28637  2008      Beijing       Judo       Judo       BENIKHLEF, Amar     ALG   
      29600  2012       London  Athletics  Athletics    MAKHLOUFI, Taoufik     ALG   
      
            Gender                             Event   Medal  
      17060    Men                           71-75KG  Bronze  
      17064    Men     75 - 81KG (Light-Heavyweight)  Bronze  
      19874  Women                             1500M    Gold  
      20200    Men         54 - 57KG (Featherweight)  Bronze  
      21610    Men                             1500M    Gold  
      21946    Men           57 - 60KG (Lightweight)    Gold  
      21960    Men                           71-75KG  Bronze  
      23536  Women                             1500M    Gold  
      23624    Men                             5000M  Silver  
      23631    Men                              800M  Bronze  
      23655    Men                         High Jump  Bronze  
      23890    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      28602  Women      48 - 52KG (Half-Lightweight)  Bronze  
      28637    Men          81 - 90KG (Middleweight)  Silver  
      29600    Men                             1500M    Gold  ),
     ('ANZ',
            Year       City      Sport Discipline                     Athlete  \
      1146  1908     London   Aquatics   Swimming       BEAUREPAIRE, Frank E.   
      1154  1908     London   Aquatics   Swimming       BEAUREPAIRE, Frank E.   
      1208  1908     London  Athletics  Athletics              KERR, Harry E.   
      1298  1908     London     Boxing     Boxing          BAKER, Reginald L.   
      1648  1908     London      Rugby      Rugby              BARNETT, Jumbo   
      1649  1908     London      Rugby      Rugby           BEDE-SMITH, Frank   
      1650  1908     London      Rugby      Rugby         CARMICHAEL, Philipp   
      1651  1908     London      Rugby      Rugby     CARROLL, Daniel Brendan   
      1652  1908     London      Rugby      Rugby            CRAIG, Robert R.   
      1653  1908     London      Rugby      Rugby             GRIFFEN, Thomas   
      1654  1908     London      Rugby      Rugby                HICKEY, John   
      1655  1908     London      Rugby      Rugby          MCARTHUR, Emmanuel   
      1656  1908     London      Rugby      Rugby           MCCABE, Arthur J.   
      1657  1908     London      Rugby      Rugby              MCCUE, Patrick   
      1658  1908     London      Rugby      Rugby       MCKIVATT, Christopher   
      1659  1908     London      Rugby      Rugby          MCMURTRIE, Charles   
      1660  1908     London      Rugby      Rugby    MIDDLETON, Albert Sidney   
      1661  1908     London      Rugby      Rugby            RICHARDS, Thomas   
      1662  1908     London      Rugby      Rugby            RUSSELL, Charles   
      1954  1912  Stockholm   Aquatics   Swimming                HEALY, Cecil   
      1956  1912  Stockholm   Aquatics   Swimming               DURACK, Fanny   
      1957  1912  Stockholm   Aquatics   Swimming           WYLIE, Wilhelmina   
      1958  1912  Stockholm   Aquatics   Swimming         HARDWICK, Harold H.   
      1967  1912  Stockholm   Aquatics   Swimming         HARDWICK, Harold H.   
      1986  1912  Stockholm   Aquatics   Swimming            BOARDMAN, Leslie   
      1987  1912  Stockholm   Aquatics   Swimming           CHAMPION, Malcolm   
      1988  1912  Stockholm   Aquatics   Swimming         HARDWICK, Harold H.   
      1989  1912  Stockholm   Aquatics   Swimming                HEALY, Cecil   
      2785  1912  Stockholm     Tennis     Tennis  WILDING, Anthony Frederick   
      
           Country Gender                          Event   Medal  
      1146     ANZ    Men                1500M Freestyle  Bronze  
      1154     ANZ    Men                 400M Freestyle  Silver  
      1208     ANZ    Men                     3500M Walk  Bronze  
      1298     ANZ    Men  63.5 - 71.67KG (Middleweight)  Silver  
      1648     ANZ    Men                          Rugby    Gold  
      1649     ANZ    Men                          Rugby    Gold  
      1650     ANZ    Men                          Rugby    Gold  
      1651     ANZ    Men                          Rugby    Gold  
      1652     ANZ    Men                          Rugby    Gold  
      1653     ANZ    Men                          Rugby    Gold  
      1654     ANZ    Men                          Rugby    Gold  
      1655     ANZ    Men                          Rugby    Gold  
      1656     ANZ    Men                          Rugby    Gold  
      1657     ANZ    Men                          Rugby    Gold  
      1658     ANZ    Men                          Rugby    Gold  
      1659     ANZ    Men                          Rugby    Gold  
      1660     ANZ    Men                          Rugby    Gold  
      1661     ANZ    Men                          Rugby    Gold  
      1662     ANZ    Men                          Rugby    Gold  
      1954     ANZ    Men                 100M Freestyle  Silver  
      1956     ANZ  Women                 100M Freestyle    Gold  
      1957     ANZ  Women                 100M Freestyle  Silver  
      1958     ANZ    Men                1500M Freestyle  Bronze  
      1967     ANZ    Men                 400M Freestyle  Bronze  
      1986     ANZ    Men         4X200M Freestyle Relay    Gold  
      1987     ANZ    Men         4X200M Freestyle Relay    Gold  
      1988     ANZ    Men         4X200M Freestyle Relay    Gold  
      1989     ANZ    Men         4X200M Freestyle Relay    Gold  
      2785     ANZ    Men                 Singles Indoor  Bronze  ),
     ('ARG',
             Year    City      Sport Discipline                        Athlete  \
      4356   1924   Paris  Athletics  Athletics                  BRUNETO, Luis   
      4360   1924   Paris     Boxing     Boxing                PORZIO, Alfredo   
      4366   1924   Paris     Boxing     Boxing               QUARTUCCI, Pedro   
      4371   1924   Paris     Boxing     Boxing               COPELLO, Alfredo   
      4374   1924   Paris     Boxing     Boxing                 MENDEZ, Hector   
      ...     ...     ...        ...        ...                            ...   
      30562  2012  London     Hockey     Hockey               SRUOGA, Josefina   
      30789  2012  London    Sailing    Sailing               CALABRESE, Lucas   
      30790  2012  London    Sailing    Sailing             DE LA FUENTE, Juan   
      30930  2012  London  Taekwondo  Taekwondo  CRISMANICH, Sebastian Eduardo   
      30954  2012  London     Tennis     Tennis         DEL POTRO, Juan Martin   
      
            Country Gender                            Event   Medal  
      4356      ARG    Men                      Triple Jump  Silver  
      4360      ARG    Men          + 79.38KG (Heavyweight)  Bronze  
      4366      ARG    Men  53.52 - 57.15KG (Featherweight)  Bronze  
      4371      ARG    Men    57.15 - 61.24KG (Lightweight)  Silver  
      4374      ARG    Men   61.24 - 66.68KG (Welterweight)  Silver  
      ...       ...    ...                              ...     ...  
      30562     ARG  Women                           Hockey  Silver  
      30789     ARG    Men                              470  Bronze  
      30790     ARG    Men                              470  Bronze  
      30930     ARG    Men                       68 - 80 KG    Gold  
      30954     ARG    Men                          Singles  Bronze  
      
      [259 rows x 9 columns]),
     ('ARM',
             Year     City          Sport           Discipline  \
      23103  1996  Atlanta      Wrestling      Wrestling Free.   
      23138  1996  Atlanta      Wrestling      Wrestling Gre-R   
      25119  2000   Sydney  Weightlifting        Weightlifting   
      27910  2008  Beijing         Boxing               Boxing   
      29127  2008  Beijing  Weightlifting        Weightlifting   
      29136  2008  Beijing  Weightlifting        Weightlifting   
      29139  2008  Beijing  Weightlifting        Weightlifting   
      29189  2008  Beijing      Wrestling      Wrestling Gre-R   
      29213  2008  Beijing      Wrestling      Wrestling Gre-R   
      31154  2012   London      Wrestling  Wrestling Freestyle   
      31163  2012   London      Wrestling  Wrestling Freestyle   
      
                                Athlete Country Gender                     Event  \
      23103             MKRCHYAN, Armen     ARM    Men  - 48KG (Light-Flyweight)   
      23138             NAZARYAN, Armen     ARM    Men     48 - 52KG (Flyweight)   
      25119             MELIKYAN, Arsen     ARM    Men                      77KG   
      27910          JAVAKHYAN, Hrachik     ARM    Men   57 - 60KG (Lightweight)   
      29127  MARTIROSYAN, Tigran Gevorg     ARM    Men                      69KG   
      29136             DAVTYAN, Gevorg     ARM    Men                      77KG   
      29139  MARTIROSYAN, Tigran Varban     ARM    Men                      85KG   
      29189               AMOYAN, Roman     ARM    Men                    - 55KG   
      29213             PATRIKEEV, Yuri     ARM    Men                96 - 120KG   
      31154          JULFALAKYAN, Arsen     ARM    Men                  Wg 74 KG   
      31163           ALEKSANYAN, Artur     ARM    Men                  Wg 96 KG   
      
              Medal  
      23103  Silver  
      23138    Gold  
      25119  Bronze  
      27910  Bronze  
      29127  Bronze  
      29136  Bronze  
      29139  Bronze  
      29189  Bronze  
      29213  Bronze  
      31154  Silver  
      31163  Bronze  ),
     ('AUS',
             Year    City      Sport Discipline               Athlete Country  \
      18     1896  Athens  Athletics  Athletics          FLACK, Edwin     AUS   
      24     1896  Athens  Athletics  Athletics          FLACK, Edwin     AUS   
      158    1900   Paris   Aquatics   Swimming  LANE, Frederick C.V.     AUS   
      161    1900   Paris   Aquatics   Swimming  LANE, Frederick C.V.     AUS   
      230    1900   Paris  Athletics  Athletics       ROWLEY, Stanley     AUS   
      ...     ...     ...        ...        ...                   ...     ...   
      30806  2012  London    Sailing    Sailing          CURTIS, Nina     AUS   
      30807  2012  London    Sailing    Sailing         PRICE, Olivia     AUS   
      30808  2012  London    Sailing    Sailing       WHITTY, Lucinda     AUS   
      30815  2012  London    Sailing    Sailing         SLINGSBY, Tom     AUS   
      30963  2012  London  Triathlon  Triathlon         DENSHAM, Erin     AUS   
      
            Gender                Event   Medal  
      18       Men                1500M    Gold  
      24       Men                 800M    Gold  
      158      Men       200M Freestyle    Gold  
      161      Men  200M Obstacle Event    Gold  
      230      Men                 100M  Bronze  
      ...      ...                  ...     ...  
      30806  Women           Elliott 6M  Silver  
      30807  Women           Elliott 6M  Silver  
      30808  Women           Elliott 6M  Silver  
      30815    Men                Laser    Gold  
      30963  Women           Individual  Bronze  
      
      [1189 rows x 9 columns]),
     ('AUT',
             Year     City          Sport       Discipline  \
      1      1896   Athens       Aquatics         Swimming   
      9      1896   Athens       Aquatics         Swimming   
      53     1896   Athens        Cycling    Cycling Track   
      56     1896   Athens        Cycling    Cycling Track   
      58     1896   Athens        Cycling    Cycling Track   
      ...     ...      ...            ...              ...   
      26859  2004   Athens       Shooting         Shooting   
      26990  2004   Athens      Triathlon        Triathlon   
      27220  2008  Beijing       Aquatics         Swimming   
      28015  2008  Beijing  Canoe / Kayak  Canoe / Kayak S   
      28593  2008  Beijing           Judo             Judo   
      
                               Athlete Country Gender  \
      1               HERSCHMANN, Otto     AUT    Men   
      9                  NEUMANN, Paul     AUT    Men   
      53                 SCHMAL, Adolf     AUT    Men   
      56                 SCHMAL, Adolf     AUT    Men   
      58                 SCHMAL, Adolf     AUT    Men   
      ...                          ...     ...    ...   
      26859          PLANER, Christian     AUT    Men   
      26990                ALLEN, Kate     AUT  Women   
      27220               JUKIC, Mirna     AUT  Women   
      28015  OBLINGER PETERS, Violetta     AUT  Women   
      28593           PAISCHER, Ludwig     AUT    Men   
      
                                          Event   Medal  
      1                          100M Freestyle  Silver  
      9                          400M Freestyle    Gold  
      53                                   10KM  Bronze  
      56                           12-Hour Race    Gold  
      58                         1KM Time Trial  Bronze  
      ...                                   ...     ...  
      26859  50M Rifle 3 Positions (3X40 Shots)  Bronze  
      26990                          Individual    Gold  
      27220                   100M Breaststroke  Bronze  
      28015                  K-1 (Kayak Single)  Bronze  
      28593                             - 60 KG  Silver  
      
      [146 rows x 9 columns]),
     ('AZE',
             Year     City          Sport           Discipline  \
      23109  1996  Atlanta      Wrestling      Wrestling Free.   
      23902  2000   Sydney         Boxing               Boxing   
      24880  2000   Sydney       Shooting             Shooting   
      25129  2000   Sydney      Wrestling      Wrestling Free.   
      25884  2004   Athens         Boxing               Boxing   
      25892  2004   Athens         Boxing               Boxing   
      26847  2004   Athens       Shooting             Shooting   
      26874  2004   Athens       Shooting             Shooting   
      27160  2004   Athens      Wrestling      Wrestling Gre-R   
      27906  2008  Beijing         Boxing               Boxing   
      28624  2008  Beijing           Judo                 Judo   
      28639  2008  Beijing           Judo                 Judo   
      29146  2008  Beijing      Wrestling      Wrestling Free.   
      29181  2008  Beijing      Wrestling      Wrestling Free.   
      29192  2008  Beijing      Wrestling      Wrestling Gre-R   
      29196  2008  Beijing      Wrestling      Wrestling Gre-R   
      29871  2012   London         Boxing               Boxing   
      29918  2012   London         Boxing               Boxing   
      31065  2012   London  Weightlifting        Weightlifting   
      31098  2012   London      Wrestling  Wrestling Freestyle   
      31107  2012   London      Wrestling  Wrestling Freestyle   
      31109  2012   London      Wrestling  Wrestling Freestyle   
      31129  2012   London      Wrestling  Wrestling Freestyle   
      31135  2012   London      Wrestling  Wrestling Freestyle   
      31142  2012   London      Wrestling  Wrestling Freestyle   
      31155  2012   London      Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                          Event  \
      23109         ABDULLAYEV, Namig     AZE    Men          48 - 52KG (Flyweight)   
      23902          ALAKPAROV, Vugar     AZE    Men                        71-75KG   
      24880  MEFTAKHETDINOVA, Zemfira     AZE  Women             Skeet (75 Targets)   
      25129         ABDULLAYEV, Namig     AZE    Men                      48 - 54KG   
      25884             ASLANOV, Fuad     AZE    Men          48 - 51KG (Flyweight)   
      25892          MAMMADOV, Aghasi     AZE    Men       51 - 54KG (Bantamweight)   
      26847           ASHUMOVA, Irada     AZE  Women       25M Pistol (30+30 Shots)   
      26874  MEFTAKHETDINOVA, Zemfira     AZE  Women             Skeet (75 Targets)   
      27160           MANSUROV, Farid     AZE    Men                      60 - 66KG   
      27906           IMRANOV, Shahin     AZE    Men      54 - 57KG (Featherweight)   
      28624           MAMMADLI, Elnur     AZE    Men        66 - 73KG (Lightweight)   
      28639         MIRALIYEV, Movlud     AZE    Men  90 - 100KG (Half-Heavyweight)   
      29146           STADNIK, Mariya     AZE  Women                         - 48KG   
      29181          GAZYUMOV, Khetag     AZE    Men                      84 - 96KG   
      29192         BAYRAMOV, Rovshan     AZE    Men                         - 55KG   
      29196          RAHIMOV, Vitaliy     AZE    Men                      55 - 60KG   
      29871   MEDZHIDOV, Magomedrasul     AZE    Men                         + 91KG   
      29918          MAMMADOV, Teymur     AZE    Men                      81 - 91KG   
      31065         HRISTOV, Valentin     AZE    Men                          -56KG   
      31098           STADNYK, Mariya     AZE  Women                       Wf 48 KG   
      31107         RATKEVICH, Yuliya     AZE  Women                       Wf 55 KG   
      31109          ASGAROV, Toghrul     AZE    Men                       Wf 60 KG   
      31129          SHARIFOV, Sharif     AZE    Men                       Wf 84 KG   
      31135          GAZYUMOV, Khetag     AZE    Men                       Wf 96 KG   
      31142         BAYRAMOV, Rovshan     AZE    Men                       Wg 55 KG   
      31155             AHMADOV, Emin     AZE    Men                       Wg 74 KG   
      
              Medal  
      23109  Silver  
      23902  Bronze  
      24880    Gold  
      25129    Gold  
      25884  Bronze  
      25892  Bronze  
      26847  Bronze  
      26874  Bronze  
      27160    Gold  
      27906  Bronze  
      28624    Gold  
      28639  Bronze  
      29146  Bronze  
      29181  Bronze  
      29192  Silver  
      29196  Silver  
      29871  Bronze  
      29918  Bronze  
      31065  Bronze  
      31098  Silver  
      31107  Bronze  
      31109    Gold  
      31129    Gold  
      31135  Bronze  
      31142  Silver  
      31155  Bronze  ),
     ('BAH',
             Year                   City      Sport Discipline  \
      9696   1956  Melbourne / Stockholm    Sailing    Sailing   
      9697   1956  Melbourne / Stockholm    Sailing    Sailing   
      11521  1964                  Tokyo    Sailing    Sailing   
      11522  1964                  Tokyo    Sailing    Sailing   
      20024  1992              Barcelona  Athletics  Athletics   
      21664  1996                Atlanta  Athletics  Athletics   
      21665  1996                Atlanta  Athletics  Athletics   
      21666  1996                Atlanta  Athletics  Athletics   
      21667  1996                Atlanta  Athletics  Athletics   
      21668  1996                Atlanta  Athletics  Athletics   
      23542  2000                 Sydney  Athletics  Athletics   
      23584  2000                 Sydney  Athletics  Athletics   
      23585  2000                 Sydney  Athletics  Athletics   
      23586  2000                 Sydney  Athletics  Athletics   
      23587  2000                 Sydney  Athletics  Athletics   
      23588  2000                 Sydney  Athletics  Athletics   
      25559  2004                 Athens  Athletics  Athletics   
      25575  2004                 Athens  Athletics  Athletics   
      27631  2008                Beijing  Athletics  Athletics   
      27632  2008                Beijing  Athletics  Athletics   
      27633  2008                Beijing  Athletics  Athletics   
      27634  2008                Beijing  Athletics  Athletics   
      27716  2008                Beijing  Athletics  Athletics   
      29665  2012                 London  Athletics  Athletics   
      29666  2012                 London  Athletics  Athletics   
      29667  2012                 London  Athletics  Athletics   
      29668  2012                 London  Athletics  Athletics   
      
                               Athlete Country Gender  \
      9696     FARRINGTON, Sloane Elmo     BAH    Men   
      9697   KNOWLES, Durward Randolph     BAH    Men   
      11521        COOKE, Cecil George     BAH    Men   
      11522  KNOWLES, Durward Randolph     BAH    Men   
      20024          RUTHERFORD, Frank     BAH    Men   
      21664             CLARKE, Eldece     BAH  Women   
      21665      DAVIS, Pauline Elaine     BAH  Women   
      21666  FERGUSON-MCKENZIE, Debbie     BAH  Women   
      21667           FYNES, Sevatheda     BAH  Women   
      21668           STURRUP, Chandra     BAH  Women   
      23542      DAVIS, Pauline Elaine     BAH  Women   
      23584      DAVIS, Pauline Elaine     BAH  Women   
      23585  FERGUSON-MCKENZIE, Debbie     BAH  Women   
      23586           FYNES, Sevatheda     BAH  Women   
      23587              LEWIS, Eldice     BAH  Women   
      23588           STURRUP, Chandra     BAH  Women   
      25559  FERGUSON-MCKENZIE, Debbie     BAH  Women   
      25575  WILLIAMS-DARLING, Tonique     BAH  Women   
      27631             BAIN, Andretti     BAH    Men   
      27632         BROWN, Christopher     BAH    Men   
      27633           MATHIEU, Michael     BAH    Men   
      27634           WILLIAMS, Andrae     BAH    Men   
      27716              SANDS, Leevan     BAH    Men   
      29665               BROWN, Chris     BAH    Men   
      29666           MATHIEU, Michael     BAH    Men   
      29667              MILLER, Ramon     BAH    Men   
      29668          PINDER, Demetrius     BAH    Men   
      
                                       Event   Medal  
      9696   Two-Person Keelboat Open (Star)  Bronze  
      9697   Two-Person Keelboat Open (Star)  Bronze  
      11521  Two-Person Keelboat Open (Star)    Gold  
      11522  Two-Person Keelboat Open (Star)    Gold  
      20024                      Triple Jump  Bronze  
      21664                     4X100M Relay  Silver  
      21665                     4X100M Relay  Silver  
      21666                     4X100M Relay  Silver  
      21667                     4X100M Relay  Silver  
      21668                     4X100M Relay  Silver  
      23542                             200M    Gold  
      23584                     4X100M Relay    Gold  
      23585                     4X100M Relay    Gold  
      23586                     4X100M Relay    Gold  
      23587                     4X100M Relay    Gold  
      23588                     4X100M Relay    Gold  
      25559                             200M  Bronze  
      25575                             400M    Gold  
      27631                     4X400M Relay  Silver  
      27632                     4X400M Relay  Silver  
      27633                     4X400M Relay  Silver  
      27634                     4X400M Relay  Silver  
      27716                      Triple Jump  Bronze  
      29665                     4X400M Relay    Gold  
      29666                     4X400M Relay    Gold  
      29667                     4X400M Relay    Gold  
      29668                     4X400M Relay    Gold  ),
     ('BAR',
             Year    City      Sport Discipline            Athlete Country Gender  \
      23520  2000  Sydney  Athletics  Athletics  THOMPSON, Obadele     BAR    Men   
      
            Event   Medal  
      23520  100M  Bronze  ),
     ('BDI',
             Year     City      Sport Discipline             Athlete Country Gender  \
      21700  1996  Atlanta  Athletics  Athletics  NIYONGABO, Venuste     BDI    Men   
      
             Event Medal  
      21700  5000M  Gold  ),
     ('BEL',
             Year     City      Sport  Discipline              Athlete Country  \
      205    1900    Paris   Aquatics  Water polo         COHEN, Henri     BEL   
      206    1900    Paris   Aquatics  Water polo      DE BACKER, Jean     BEL   
      207    1900    Paris   Aquatics  Water polo      DE BEHR, Victor     BEL   
      208    1900    Paris   Aquatics  Water polo    FEYAERTS, Fernand     BEL   
      209    1900    Paris   Aquatics  Water polo      GREGOIRE, Oscar     BEL   
      ...     ...      ...        ...         ...                  ...     ...   
      27622  2008  Beijing  Athletics   Athletics    OUEDRAOGO, Elodie     BEL   
      27684  2008  Beijing  Athletics   Athletics       HELLEBAUT, Tia     BEL   
      30582  2012   London       Judo        Judo  VAN SNICK, Charline     BEL   
      30820  2012   London    Sailing     Sailing       VAN ACKER, Evi     BEL   
      30861  2012   London   Shooting    Shooting          COX, Lionel     BEL   
      
            Gender            Event   Medal  
      205      Men       Water Polo  Silver  
      206      Men       Water Polo  Silver  
      207      Men       Water Polo  Silver  
      208      Men       Water Polo  Silver  
      209      Men       Water Polo  Silver  
      ...      ...              ...     ...  
      27622  Women     4X100M Relay  Silver  
      27684  Women        High Jump    Gold  
      30582  Women          - 48 KG  Bronze  
      30820  Women     Laser Radial  Bronze  
      30861    Men  50M Rifle Prone  Silver  
      
      [411 rows x 9 columns]),
     ('BER',
             Year      City   Sport Discipline         Athlete Country Gender  \
      14288  1976  Montreal  Boxing     Boxing  HILL, Clarence     BER    Men   
      
                            Event   Medal  
      14288  + 81KG (Heavyweight)  Bronze  ),
     ('BLR',
             Year     City       Sport           Discipline                 Athlete  \
      21717  1996  Atlanta   Athletics            Athletics       KAPTYUKH, Vasiliy   
      21719  1996  Atlanta   Athletics            Athletics  DUBROVSHCHIK, Vladimir   
      21720  1996  Atlanta   Athletics            Athletics         ZVEREVA, Ellina   
      21728  1996  Atlanta   Athletics            Athletics     SAZANOVICH, Natalya   
      22328  1996  Atlanta  Gymnastics          Artistic G.         SCHERBO, Vitaly   
      ...     ...      ...         ...                  ...                     ...   
      30388  2012   London  Gymnastics  Gymnastics Rhythmic     CHARKASHYNA, Liubou   
      30860  2012   London    Shooting             Shooting        MARTYNOV, Sergei   
      30946  2012   London      Tennis               Tennis      AZARENKA, Victoria   
      30947  2012   London      Tennis               Tennis             MIRNYI, Max   
      30957  2012   London      Tennis               Tennis      AZARENKA, Victoria   
      
            Country Gender                  Event   Medal  
      21717     BLR    Men           Discus Throw  Bronze  
      21719     BLR    Men           Discus Throw  Silver  
      21720     BLR  Women           Discus Throw  Bronze  
      21728     BLR  Women             Heptathlon  Silver  
      22328     BLR    Men         Horizontal Bar  Bronze  
      ...       ...    ...                    ...     ...  
      30388     BLR  Women  Individual All-Around  Bronze  
      30860     BLR    Men        50M Rifle Prone    Gold  
      30946     BLR  Women          Mixed Doubles    Gold  
      30947     BLR    Men          Mixed Doubles    Gold  
      30957     BLR  Women                Singles  Bronze  
      
      [113 rows x 9 columns]),
     ('BOH',
            Year    City      Sport Discipline                     Athlete Country  \
      275   1900   Paris  Athletics  Athletics            JANDA, Frantisek     BOH   
      648   1900   Paris     Tennis     Tennis           ROSENBAUM, Hedwig     BOH   
      1345  1908  London    Fencing    Fencing  GOPPOLD DE LOBSDORF, Vilem     BOH   
      1348  1908  London    Fencing    Fencing  GOPPOLD DE LOBSDORF, Vilem     BOH   
      1349  1908  London    Fencing    Fencing             LADA, Vlastimil     BOH   
      1350  1908  London    Fencing    Fencing           SCHEJBAL, Bedrich     BOH   
      1351  1908  London    Fencing    Fencing            TUCEK, Frantisek     BOH   
      
           Gender             Event   Medal  
      275     Men      Discus Throw  Silver  
      648   Women           Singles  Bronze  
      1345    Men  Sabre Individual  Bronze  
      1348    Men        Sabre Team  Bronze  
      1349    Men        Sabre Team  Bronze  
      1350    Men        Sabre Team  Bronze  
      1351    Men        Sabre Team  Bronze  ),
     ('BOT',
             Year    City      Sport Discipline      Athlete Country Gender Event  \
      29705  2012  London  Athletics  Athletics  AMOS, Nijel     BOT    Men  800M   
      
              Medal  
      29705  Silver  ),
     ('BRA',
             Year     City       Sport  Discipline                    Athlete  \
      3853   1920  Antwerp    Shooting    Shooting        PARAENSE, Guilherme   
      3918   1920  Antwerp    Shooting    Shooting             BARBOSA, Dario   
      3919   1920  Antwerp    Shooting    Shooting  DA COSTA, Afranio Antonio   
      3920   1920  Antwerp    Shooting    Shooting        PARAENSE, Guilherme   
      3921   1920  Antwerp    Shooting    Shooting         SOLEDADE, Fernando   
      ...     ...      ...         ...         ...                        ...   
      31019  2012   London  Volleyball  Volleyball          OLIVEIRA, Fabiana   
      31020  2012   London  Volleyball  Volleyball             PEQUENO, Paula   
      31021  2012   London  Volleyball  Volleyball           PEREIRA, Natalia   
      31022  2012   London  Volleyball  Volleyball        RODRIGUES, Fernanda   
      31023  2012   London  Volleyball  Volleyball            SILVA, Adenizia   
      
            Country Gender                             Event   Medal  
      3853      BRA    Men  25M Rapid Fire Pistol (60 Shots)    Gold  
      3918      BRA    Men             50M Army Pistol, Team  Bronze  
      3919      BRA    Men             50M Army Pistol, Team  Bronze  
      3920      BRA    Men             50M Army Pistol, Team  Bronze  
      3921      BRA    Men             50M Army Pistol, Team  Bronze  
      ...       ...    ...                               ...     ...  
      31019     BRA  Women                        Volleyball    Gold  
      31020     BRA  Women                        Volleyball    Gold  
      31021     BRA  Women                        Volleyball    Gold  
      31022     BRA  Women                        Volleyball    Gold  
      31023     BRA  Women                        Volleyball    Gold  
      
      [431 rows x 9 columns]),
     ('BRN',
             Year    City      Sport Discipline              Athlete Country Gender  \
      29605  2012  London  Athletics  Athletics  JAMAL, Maryam Yusuf     BRN  Women   
      
             Event   Medal  
      29605  1500M  Bronze  ),
     ('BUL',
             Year                   City      Sport           Discipline  \
      8312   1952               Helsinki     Boxing               Boxing   
      9390   1956  Melbourne / Stockholm   Football             Football   
      9391   1956  Melbourne / Stockholm   Football             Football   
      9392   1956  Melbourne / Stockholm   Football             Football   
      9393   1956  Melbourne / Stockholm   Football             Football   
      ...     ...                    ...        ...                  ...   
      29172  2008                Beijing  Wrestling      Wrestling Free.   
      29174  2008                Beijing  Wrestling      Wrestling Free.   
      29202  2008                Beijing  Wrestling      Wrestling Gre-R   
      29919  2012                 London     Boxing               Boxing   
      31122  2012                 London  Wrestling  Wrestling Freestyle   
      
                                 Athlete Country Gender      Event   Medal  
      8312       NIKOLOV, Boris Georgiev     BUL    Men    71-75KG  Bronze  
      9390         DIEV, Todor Nedyalkov     BUL    Men   Football  Bronze  
      9391            KOLEV, Ivan Petkov     BUL    Men   Football  Bronze  
      9392   KOVATCHEV, Nikolai Dimitrov     BUL    Men   Football  Bronze  
      9393          MANOLOV, Manol Tomov     BUL    Men   Football  Bronze  
      ...                            ...     ...    ...        ...     ...  
      29172              ZLATEVA, Stanka     BUL  Women  63 - 72KG  Silver  
      29174               TERZIEV, Kiril     BUL    Men  66 - 74KG  Bronze  
      29202              YANAKIEV, Yavor     BUL    Men  66 - 74KG  Bronze  
      29919                PULEV, Tervel     BUL    Men  81 - 91KG  Bronze  
      31122     HRISTOVA, Stanka Zlateva     BUL  Women   Wf 72 KG  Silver  
      
      [333 rows x 9 columns]),
     ('BWI',
            Year  City      Sport Discipline                     Athlete Country  \
      9977  1960  Rome  Athletics  Athletics  GARDNER, Keith Alvin Saint     BWI   
      9978  1960  Rome  Athletics  Athletics        KERR, George Ezekiel     BWI   
      9979  1960  Rome  Athletics  Athletics        SPENCE, Malcolm A.E.     BWI   
      9980  1960  Rome  Athletics  Athletics           WEDDERBURN, James     BWI   
      9995  1960  Rome  Athletics  Athletics        KERR, George Ezekiel     BWI   
      
           Gender         Event   Medal  
      9977    Men  4X400M Relay  Bronze  
      9978    Men  4X400M Relay  Bronze  
      9979    Men  4X400M Relay  Bronze  
      9980    Men  4X400M Relay  Bronze  
      9995    Men          800M  Bronze  ),
     ('CAN',
             Year      City          Sport           Discipline  \
      246    1900     Paris      Athletics            Athletics   
      254    1900     Paris      Athletics            Athletics   
      771    1904  St Louis      Athletics            Athletics   
      898    1904  St Louis       Football             Football   
      899    1904  St Louis       Football             Football   
      ...     ...       ...            ...                  ...   
      30720  2012    London         Rowing               Rowing   
      30721  2012    London         Rowing               Rowing   
      31074  2012    London  Weightlifting        Weightlifting   
      31100  2012    London      Wrestling  Wrestling Freestyle   
      31106  2012    London      Wrestling  Wrestling Freestyle   
      
                            Athlete Country Gender                       Event  \
      246             ORTON, George     CAN    Men          3000M Steeplechase   
      254             ORTON, George     CAN    Men                400M Hurdles   
      771       DESMARTEAU, Etienne     CAN    Men  56LB Weight Throw (25.4KG)   
      898            DUCKER, George     CAN    Men                    Football   
      899    FRASER, John Alexander     CAN    Men                    Football   
      ...                       ...     ...    ...                         ...   
      30720      VIINBERG, Rachelle     CAN  Women         Eight With Coxswain   
      30721       WILKINSON, Lauren     CAN  Women         Eight With Coxswain   
      31074       GIRARD, Christine     CAN  Women                        63KG   
      31100            HUYNH, Carol     CAN  Women                    Wf 48 KG   
      31106     VERBEEK, Tonya Lynn     CAN  Women                    Wf 55 KG   
      
              Medal  
      246      Gold  
      254    Bronze  
      771      Gold  
      898      Gold  
      899      Gold  
      ...       ...  
      30720  Silver  
      30721  Silver  
      31074  Bronze  
      31100  Bronze  
      31106  Silver  
      
      [649 rows x 9 columns]),
     ('CHI',
             Year                   City       Sport Discipline  \
      5189   1928              Amsterdam   Athletics  Athletics   
      8421   1952               Helsinki  Equestrian    Jumping   
      8428   1952               Helsinki  Equestrian    Jumping   
      8429   1952               Helsinki  Equestrian    Jumping   
      8430   1952               Helsinki  Equestrian    Jumping   
      9110   1956  Melbourne / Stockholm   Athletics  Athletics   
      9176   1956  Melbourne / Stockholm      Boxing     Boxing   
      9203   1956  Melbourne / Stockholm      Boxing     Boxing   
      9204   1956  Melbourne / Stockholm      Boxing     Boxing   
      19389  1988                  Seoul    Shooting   Shooting   
      24184  2000                 Sydney    Football   Football   
      24185  2000                 Sydney    Football   Football   
      24186  2000                 Sydney    Football   Football   
      24187  2000                 Sydney    Football   Football   
      24188  2000                 Sydney    Football   Football   
      24189  2000                 Sydney    Football   Football   
      24190  2000                 Sydney    Football   Football   
      24191  2000                 Sydney    Football   Football   
      24192  2000                 Sydney    Football   Football   
      24193  2000                 Sydney    Football   Football   
      24194  2000                 Sydney    Football   Football   
      24195  2000                 Sydney    Football   Football   
      24196  2000                 Sydney    Football   Football   
      24197  2000                 Sydney    Football   Football   
      24198  2000                 Sydney    Football   Football   
      24199  2000                 Sydney    Football   Football   
      24200  2000                 Sydney    Football   Football   
      24201  2000                 Sydney    Football   Football   
      26972  2004                 Athens      Tennis     Tennis   
      26973  2004                 Athens      Tennis     Tennis   
      26980  2004                 Athens      Tennis     Tennis   
      26981  2004                 Athens      Tennis     Tennis   
      29006  2008                Beijing      Tennis     Tennis   
      
                              Athlete Country Gender                          Event  \
      5189        PLAZA REYES, Manuel     CHI    Men                       Marathon   
      8421        CRISTI-GALLO, Oscar     CHI    Men                     Individual   
      8428        CRISTI-GALLO, Oscar     CHI    Men                           Team   
      8429        ECHEVERRIA, Ricardo     CHI    Men                           Team   
      8430             MENDOZA, Cesar     CHI    Men                           Team   
      9110            AHRENS, Marlene     CHI  Women                  Javelin Throw   
      9176        BARRIENTOS, Claudio     CHI    Men       51 - 54KG (Bantamweight)   
      9203               TAPIA, Ramon     CHI    Men                        71-75KG   
      9204              LUCAS, Carlos     CHI    Men  75 - 81KG (Light-Heavyweight)   
      19389  DE IRRUARRIZAGA, Alfonso     CHI    Men            Skeet (125 Targets)   
      24184         ALVAREZ, Cristian     CHI    Men                       Football   
      24185          ARRUE, Francisco     CHI    Men                       Football   
      24186          CONTRERAS, Pablo     CHI    Men                       Football   
      24187       DI GREGORIO, Javier     CHI    Men                       Football   
      24188       GONZALEZ, Sebastian     CHI    Men                       Football   
      24189          HENRIQUEZ, David     CHI    Men                       Football   
      24190            IBARRA, Manuel     CHI    Men                       Football   
      24191        MALDONADO, Claudio     CHI    Men                       Football   
      24192           NAVIA, Reinaldo     CHI    Men                       Football   
      24193            NUNEZ, Rodrigo     CHI    Men                       Football   
      24194            OLARRA, Rafael     CHI    Men                       Football   
      24195       ORMAZABAL, Patricio     CHI    Men                       Football   
      24196            PIZARRO, David     CHI    Men                       Football   
      24197              REYES, Pedro     CHI    Men                       Football   
      24198           ROJAS, Mauricio     CHI    Men                       Football   
      24199             TAPIA, Nelson     CHI    Men                       Football   
      24200            TELLO, Rodrigo     CHI    Men                       Football   
      24201            ZAMORANO, Ivan     CHI    Men                       Football   
      26972        GONZALEZ, Fernando     CHI    Men                        Doubles   
      26973            MASSU, Nicolas     CHI    Men                        Doubles   
      26980        GONZALEZ, Fernando     CHI    Men                        Singles   
      26981            MASSU, Nicolas     CHI    Men                        Singles   
      29006        GONZALEZ, Fernando     CHI    Men                        Singles   
      
              Medal  
      5189   Silver  
      8421   Silver  
      8428   Silver  
      8429   Silver  
      8430   Silver  
      9110   Silver  
      9176   Bronze  
      9203   Silver  
      9204   Bronze  
      19389  Silver  
      24184  Bronze  
      24185  Bronze  
      24186  Bronze  
      24187  Bronze  
      24188  Bronze  
      24189  Bronze  
      24190  Bronze  
      24191  Bronze  
      24192  Bronze  
      24193  Bronze  
      24194  Bronze  
      24195  Bronze  
      24196  Bronze  
      24197  Bronze  
      24198  Bronze  
      24199  Bronze  
      24200  Bronze  
      24201  Bronze  
      26972    Gold  
      26973    Gold  
      26980  Bronze  
      26981    Gold  
      29006  Silver  ),
     ('CHN',
             Year         City          Sport           Discipline         Athlete  \
      16592  1984  Los Angeles       Aquatics               Diving  LI, Kong-Zheng   
      16596  1984  Los Angeles       Aquatics               Diving   ZHOU, Ji-Hong   
      16600  1984  Los Angeles       Aquatics               Diving   TAN, Liang-De   
      16789  1984  Los Angeles        Archery              Archery   LI, Ling-Juan   
      16914  1984  Los Angeles      Athletics            Athletics   ZHU, Jian-Hua   
      ...     ...          ...            ...                  ...             ...   
      31066  2012       London  Weightlifting        Weightlifting     LI, Xueying   
      31075  2012       London  Weightlifting        Weightlifting   LIN, Qingfeng   
      31084  2012       London  Weightlifting        Weightlifting     LU, Xiaojun   
      31085  2012       London  Weightlifting        Weightlifting      LU, Haojie   
      31114  2012       London      Wrestling  Wrestling Freestyle    JING, Ruixue   
      
            Country Gender                  Event   Medal  
      16592     CHN    Men           10M Platform  Bronze  
      16596     CHN  Women           10M Platform    Gold  
      16600     CHN    Men         3M Springboard  Silver  
      16789     CHN  Women  Individual Fita Round  Silver  
      16914     CHN    Men              High Jump  Bronze  
      ...       ...    ...                    ...     ...  
      31066     CHN  Women                   58KG    Gold  
      31075     CHN    Men                   69KG    Gold  
      31084     CHN    Men                   77KG    Gold  
      31085     CHN    Men                   77KG  Silver  
      31114     CHN  Women               Wf 63 KG  Silver  
      
      [807 rows x 9 columns]),
     ('CIV',
             Year         City      Sport Discipline          Athlete Country  \
      16829  1984  Los Angeles  Athletics  Athletics  TIACOH, Gabriel     CIV   
      
            Gender Event   Medal  
      16829    Men  400M  Silver  ),
     ('CMR',
             Year         City          Sport     Discipline  \
      12063  1968       Mexico         Boxing         Boxing   
      17044  1984  Los Angeles         Boxing         Boxing   
      24202  2000       Sydney       Football       Football   
      24203  2000       Sydney       Football       Football   
      24204  2000       Sydney       Football       Football   
      24205  2000       Sydney       Football       Football   
      24206  2000       Sydney       Football       Football   
      24207  2000       Sydney       Football       Football   
      24208  2000       Sydney       Football       Football   
      24209  2000       Sydney       Football       Football   
      24210  2000       Sydney       Football       Football   
      24211  2000       Sydney       Football       Football   
      24212  2000       Sydney       Football       Football   
      24213  2000       Sydney       Football       Football   
      24214  2000       Sydney       Football       Football   
      24215  2000       Sydney       Football       Football   
      24216  2000       Sydney       Football       Football   
      24217  2000       Sydney       Football       Football   
      24218  2000       Sydney       Football       Football   
      24219  2000       Sydney       Football       Football   
      25713  2004       Athens      Athletics      Athletics   
      27720  2008      Beijing      Athletics      Athletics   
      31083  2012       London  Weightlifting  Weightlifting   
      
                               Athlete Country Gender                       Event  \
      12063            BESSALA, Joseph     CMR    Men  63.5 - 67KG (Welterweight)   
      17044      NDONGO-EBANGA, Martin     CMR    Men     57 - 60KG (Lightweight)   
      24202      ABANDA ETONG, Patrice     CMR    Men                    Football   
      24203          ALNOUDJI, Nicolas     CMR    Men                    Football   
      24204             BEAUD, Clement     CMR    Men                    Football   
      24205       BEKONO NDENE, Daniel     CMR    Men                    Football   
      24206              BRANCO, Serge     CMR    Men                    Football   
      24207               EPALLE, Joel     CMR    Men                    Football   
      24208        ETAME MAYER, Lawren     CMR    Men                    Football   
      24209         ETO'O FILS, Samuel     CMR    Men                    Football   
      24210           KAMENI, Idriss C     CMR    Men                    Football   
      24211             MBAMI, Modeste     CMR    Men                    Football   
      24212         MBOMA DEM, Patrick     CMR    Men                    Football   
      24213          MEYONG ZE, Albert     CMR    Men                    Football   
      24214               MIMPO, Serge     CMR    Men                    Football   
      24215         NGOME KOME, Daniel     CMR    Men                    Football   
      24216            NGUIMBAT, Aaron     CMR    Men                    Football   
      24217       NJITAP FOTSO, Geremi     CMR    Men                    Football   
      24218           SUFFO K, Patrick     CMR    Men                    Football   
      24219         WOME NLEND, Pierre     CMR    Men                    Football   
      25713    MBANGO ETONE, Francoise     CMR  Women                 Triple Jump   
      27720    MBANGO ETONE, Francoise     CMR  Women                 Triple Jump   
      31083  NZESSO NGAKE, Madias Dodo     CMR  Women                        75KG   
      
              Medal  
      12063  Silver  
      17044  Bronze  
      24202    Gold  
      24203    Gold  
      24204    Gold  
      24205    Gold  
      24206    Gold  
      24207    Gold  
      24208    Gold  
      24209    Gold  
      24210    Gold  
      24211    Gold  
      24212    Gold  
      24213    Gold  
      24214    Gold  
      24215    Gold  
      24216    Gold  
      24217    Gold  
      24218    Gold  
      24219    Gold  
      25713    Gold  
      27720    Gold  
      31083  Bronze  ),
     ('COL',
             Year         City          Sport           Discipline  \
      13101  1972       Munich         Boxing               Boxing   
      13105  1972       Munich         Boxing               Boxing   
      13735  1972       Munich       Shooting             Shooting   
      17882  1984  Los Angeles       Shooting             Shooting   
      18524  1988        Seoul         Boxing               Boxing   
      19894  1992    Barcelona      Athletics            Athletics   
      25117  2000       Sydney  Weightlifting        Weightlifting   
      26044  2004       Athens        Cycling        Cycling Track   
      27090  2004       Athens  Weightlifting        Weightlifting   
      29123  2008      Beijing  Weightlifting        Weightlifting   
      29153  2008      Beijing      Wrestling      Wrestling Free.   
      29770  2012       London      Athletics            Athletics   
      30003  2012       London        Cycling          Cycling BMX   
      30004  2012       London        Cycling          Cycling BMX   
      30008  2012       London        Cycling         Cycling Road   
      30613  2012       London           Judo                 Judo   
      30909  2012       London      Taekwondo            Taekwondo   
      31070  2012       London  Weightlifting        Weightlifting   
      31108  2012       London      Wrestling  Wrestling Freestyle   
      
                                      Athlete Country Gender  \
      13101                   ROJAS, Clemente     COL    Men   
      13105                    PEREZ, Alfonso     COL    Men   
      13735               BELLINGRODT, Helmut     COL    Men   
      17882               BELLINGRODT, Helmut     COL    Men   
      18524        JULIO ROCHA, Jorge Eliecer     COL    Men   
      19894          RESTREPO GAVIRIA, Ximena     COL  Women   
      25117             URRUTIA, Maria Isabel     COL  Women   
      26044       CALLE WILLIAMS, Maria Luisa     COL  Women   
      27090                   MOSQUERA, Mabel     COL  Women   
      29123                    SALAZAR, Diego     COL    Men   
      29153               RENTERIA, Jackeline     COL  Women   
      29770                IBARGUEN, Caterine     COL  Women   
      30003      OQUENDO ZABALA, Carlos Mario     COL    Men   
      30004                    PAJON, Mariana     COL  Women   
      30008              URAN URAN, Rigoberto     COL    Men   
      30613                      ALVEAR, Yuri     COL  Women   
      30909               MUNOZ OVIEDO, Oscar     COL    Men   
      31070  FIGUEROA MOSQUERA, Oscar Albeiro     COL    Men   
      31108      RENTERIA CASTILLO, Jackeline     COL  Women   
      
                                        Event   Medal  
      13101         54 - 57KG (Featherweight)  Bronze  
      13105           57 - 60KG (Lightweight)  Bronze  
      13735  50M Running Target (30+30 Shots)  Silver  
      17882  50M Running Target (30+30 Shots)  Silver  
      18524          51 - 54KG (Bantamweight)  Bronze  
      19894                              400M  Bronze  
      25117                              75KG    Gold  
      26044                       Points Race  Bronze  
      27090                              53KG  Bronze  
      29123                              62KG  Silver  
      29153                         48 - 55KG  Bronze  
      29770                       Triple Jump  Silver  
      30003                        Individual  Bronze  
      30004                        Individual    Gold  
      30008                   Individual Road  Silver  
      30613                         63 - 70KG  Bronze  
      30909                           - 58 KG  Bronze  
      31070                              62KG  Silver  
      31108                          Wf 55 KG  Bronze  ),
     ('CRC',
             Year     City     Sport Discipline               Athlete Country  \
      18113  1988    Seoul  Aquatics   Swimming   POLL AHRENS, Silvia     CRC   
      21363  1996  Atlanta  Aquatics   Swimming  POLL AHRENS, Claudia     CRC   
      23246  2000   Sydney  Aquatics   Swimming  POLL AHRENS, Claudia     CRC   
      23258  2000   Sydney  Aquatics   Swimming  POLL AHRENS, Claudia     CRC   
      
            Gender           Event   Medal  
      18113  Women  200M Freestyle  Silver  
      21363  Women  200M Freestyle    Gold  
      23246  Women  200M Freestyle  Bronze  
      23258  Women  400M Freestyle  Bronze  ),
     ('CRO',
             Year       City       Sport  Discipline               Athlete Country  \
      20135  1992  Barcelona  Basketball  Basketball      ALANOVIC, Vladan     CRO   
      20136  1992  Barcelona  Basketball  Basketball      ARAPOVIC, Franjo     CRO   
      20137  1992  Barcelona  Basketball  Basketball    CVJETICANIN, Danko     CRO   
      20138  1992  Barcelona  Basketball  Basketball          GREGOV, Alan     CRO   
      20139  1992  Barcelona  Basketball  Basketball       KOMAZEC, Arijan     CRO   
      ...     ...        ...         ...         ...                   ...     ...   
      30760  2012     London      Rowing      Rowing           SAIN, David     CRO   
      30761  2012     London      Rowing      Rowing      SINKOVIC, Martin     CRO   
      30762  2012     London      Rowing      Rowing      SINKOVIC, Valent     CRO   
      30872  2012     London    Shooting    Shooting  CERNOGORAZ, Giovanni     CRO   
      30905  2012     London   Taekwondo   Taekwondo     ZANINOVIC, Lucija     CRO   
      
            Gender             Event   Medal  
      20135    Men        Basketball  Silver  
      20136    Men        Basketball  Silver  
      20137    Men        Basketball  Silver  
      20138    Men        Basketball  Silver  
      20139    Men        Basketball  Silver  
      ...      ...               ...     ...  
      30760    Men  Quadruple Sculls  Silver  
      30761    Men  Quadruple Sculls  Silver  
      30762    Men  Quadruple Sculls  Silver  
      30872    Men              Trap    Gold  
      30905  Women           - 49 KG  Bronze  
      
      [114 rows x 9 columns]),
     ('CUB',
             Year      City          Sport           Discipline  \
      358    1900     Paris        Fencing              Fencing   
      362    1900     Paris        Fencing              Fencing   
      858    1904  St Louis        Fencing              Fencing   
      859    1904  St Louis        Fencing              Fencing   
      860    1904  St Louis        Fencing              Fencing   
      ...     ...       ...            ...                  ...   
      30848  2012    London       Shooting             Shooting   
      30916  2012    London      Taekwondo            Taekwondo   
      31086  2012    London  Weightlifting        Weightlifting   
      31119  2012    London      Wrestling  Wrestling Freestyle   
      31137  2012    London      Wrestling  Wrestling Freestyle   
      
                            Athlete Country Gender                       Event  \
      358              FONST, Ramon     CUB    Men             Épée Individual   
      362              FONST, Ramon     CUB    Men  Épée, Amateurs And Masters   
      858    VAN ZO POST, Albertson     CUB    Men             Épée Individual   
      859              FONST, Ramon     CUB    Men             Épée Individual   
      860           TATHAM, Charles     CUB    Men             Épée Individual   
      ...                       ...     ...    ...                         ...   
      30848            PUPO, Leuris     CUB    Men            25M Rapid Pistol   
      30916      DESPAIGNE, Robelis     CUB    Men                     + 80 KG   
      31086  CAMBAR RODRIGUEZ, Ivan     CUB    Men                        77KG   
      31119      LOPEZ AZCUY, Livan     CUB    Men                    Wf 66 KG   
      31137     LOPEZ NUNEZ, Mijain     CUB    Men                   Wg 120 KG   
      
              Medal  
      358      Gold  
      362    Silver  
      858    Bronze  
      859      Gold  
      860    Silver  
      ...       ...  
      30848    Gold  
      30916  Bronze  
      31086  Bronze  
      31119  Bronze  
      31137    Gold  
      
      [410 rows x 9 columns]),
     ('CYP',
             Year    City    Sport Discipline           Athlete Country Gender  \
      30816  2012  London  Sailing    Sailing  KONTIDES, Pavlos     CYP    Men   
      
             Event   Medal  
      30816  Laser  Silver  ),
     ('CZE',
             Year     City              Sport         Discipline  \
      21714  1996  Atlanta          Athletics          Athletics   
      21736  1996  Atlanta          Athletics          Athletics   
      21765  1996  Atlanta          Athletics          Athletics   
      21973  1996  Atlanta      Canoe / Kayak    Canoe / Kayak F   
      21976  1996  Atlanta      Canoe / Kayak    Canoe / Kayak F   
      22043  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22048  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22049  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22054  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22891  1996  Atlanta           Shooting           Shooting   
      22979  1996  Atlanta             Tennis             Tennis   
      22980  1996  Atlanta             Tennis             Tennis   
      22984  1996  Atlanta             Tennis             Tennis   
      23639  2000   Sydney          Athletics          Athletics   
      23663  2000   Sydney          Athletics          Athletics   
      23909  2000   Sydney             Boxing             Boxing   
      23986  2000   Sydney      Canoe / Kayak    Canoe / Kayak S   
      23987  2000   Sydney      Canoe / Kayak    Canoe / Kayak S   
      23996  2000   Sydney      Canoe / Kayak    Canoe / Kayak S   
      24858  2000   Sydney           Shooting           Shooting   
      24878  2000   Sydney           Shooting           Shooting   
      24993  2000   Sydney          Triathlon          Triathlon   
      25656  2004   Athens          Athletics          Athletics   
      25673  2004   Athens          Athletics          Athletics   
      25996  2004   Athens      Canoe / Kayak    Canoe / Kayak S   
      25997  2004   Athens      Canoe / Kayak    Canoe / Kayak S   
      26628  2004   Athens  Modern Pentathlon    Modern Pentath.   
      26756  2004   Athens             Rowing             Rowing   
      26757  2004   Athens             Rowing             Rowing   
      26758  2004   Athens             Rowing             Rowing   
      26759  2004   Athens             Rowing             Rowing   
      26804  2004   Athens            Sailing            Sailing   
      26838  2004   Athens           Shooting           Shooting   
      26849  2004   Athens           Shooting           Shooting   
      27690  2008  Beijing          Athletics          Athletics   
      28010  2008  Beijing      Canoe / Kayak    Canoe / Kayak S   
      28011  2008  Beijing      Canoe / Kayak    Canoe / Kayak S   
      28788  2008  Beijing             Rowing             Rowing   
      28853  2008  Beijing           Shooting           Shooting   
      28869  2008  Beijing           Shooting           Shooting   
      28886  2008  Beijing           Shooting           Shooting   
      29635  2012   London          Athletics          Athletics   
      29738  2012   London          Athletics          Athletics   
      29739  2012   London          Athletics          Athletics   
      29930  2012   London              Canoe       Canoe Slalom   
      29985  2012   London              Canoe       Canoe Sprint   
      29986  2012   London              Canoe       Canoe Sprint   
      29987  2012   London              Canoe       Canoe Sprint   
      29988  2012   London              Canoe       Canoe Sprint   
      30075  2012   London            Cycling      Mountain Bike   
      30635  2012   London  Modern Pentathlon  Modern Pentathlon   
      30780  2012   London             Rowing             Rowing   
      30782  2012   London             Rowing             Rowing   
      30859  2012   London           Shooting           Shooting   
      30942  2012   London             Tennis             Tennis   
      30943  2012   London             Tennis             Tennis   
      
                          Athlete Country Gender  \
      21714         DVORAK, Tomas     CZE    Men   
      21736          ZELEZNY, Jan     CZE    Men   
      21765     KASPARKOVA, Sarka     CZE  Women   
      21973        DOKTOR, Martin     CZE    Men   
      21976        DOKTOR, Martin     CZE    Men   
      22043        POLLERT, Lukas     CZE    Men   
      22048           ROHAN, Jiri     CZE    Men   
      22049       SIMEK, Miroslav     CZE    Men   
      22054  HILGERTOVA, Stepanka     CZE  Women   
      22891       JANUS, Miroslav     CZE    Men   
      22979         NOVOTNA, Jana     CZE  Women   
      22980        SUKOVA, Helena     CZE  Women   
      22984         NOVOTNA, Jana     CZE  Women   
      23639         SEBRLE, Roman     CZE    Men   
      23663          ZELEZNY, Jan     CZE    Men   
      23909          KRAJ, Rudolf     CZE    Men   
      23986          JIRAS, Marek     CZE    Men   
      23987          MADER, Tomas     CZE    Men   
      23996  HILGERTOVA, Stepanka     CZE  Women   
      24858          TENK, Martin     CZE    Men   
      24878           MALEK, Petr     CZE    Men   
      24993           REHULA, Jan     CZE    Men   
      25656         SEBRLE, Roman     CZE    Men   
      25673        BABA, Jaroslav     CZE    Men   
      25996      STEPANEK, Ondrej     CZE    Men   
      25997        VOLF, Jaroslav     CZE    Men   
      26628       CAPALINI, Libor     CZE    Men   
      26756          HANAK, Jakub     CZE    Men   
      26757          JIRKA, David     CZE    Men   
      26758          KARAS, Tomas     CZE    Men   
      26759        KOPRIVA, David     CZE    Men   
      26804        SMIDOVA, Lenka     CZE  Women   
      26838      EMMONS, Katerina     CZE  Women   
      26849         HYKOVA, Lenka     CZE  Women   
      27690    SPOTAKOVA, Barbora     CZE  Women   
      28010      STEPANEK, Ondrej     CZE    Men   
      28011        VOLF, Jaroslav     CZE    Men   
      28788         SYNEK, Ondrej     CZE    Men   
      28853      EMMONS, Katerina     CZE  Women   
      28869      EMMONS, Katerina     CZE  Women   
      28886     KOSTELECKY, David     CZE    Men   
      29635       HEJNOVA, Zuzana     CZE  Women   
      29738     VESELY, Vitezslav     CZE    Men   
      29739    SPOTAKOVA, Barbora     CZE  Women   
      29930    HRADILEK, Vavrinec     CZE    Men   
      29985         DOSTAL, Josef     CZE    Men   
      29986         HAVEL, Daniel     CZE    Men   
      29987           STERBA, Jan     CZE    Men   
      29988         TREFIL, Lukas     CZE    Men   
      30075     KULHAVY, Jaroslav     CZE    Men   
      30635        SVOBODA, David     CZE    Men   
      30780         SYNEK, Ondrej     CZE    Men   
      30782       KNAPKOVA, Mirka     CZE  Women   
      30859       SYKOROVA, Adela     CZE  Women   
      30942    HLAVACKOVA, Andrea     CZE  Women   
      30943       HRADECKA, Lucie     CZE  Women   
      
                                              Event   Medal  
      21714                               Decathlon  Bronze  
      21736                           Javelin Throw    Gold  
      21765                             Triple Jump  Bronze  
      21973                C-1 1000M (Canoe Single)    Gold  
      21976                 C-1 500M (Canoe Single)    Gold  
      22043                      C-1 (Canoe Single)  Silver  
      22048                      C-2 (Canoe Double)  Silver  
      22049                      C-2 (Canoe Double)  Silver  
      22054                      K-1 (Kayak Single)    Gold  
      22891        50M Running Target (30+30 Shots)  Bronze  
      22979                                 Doubles  Silver  
      22980                                 Doubles  Silver  
      22984                                 Singles  Bronze  
      23639                               Decathlon  Silver  
      23663                           Javelin Throw    Gold  
      23909           75 - 81KG (Light-Heavyweight)  Silver  
      23986                      C-2 (Canoe Double)  Bronze  
      23987                      C-2 (Canoe Double)  Bronze  
      23996                      K-1 (Kayak Single)    Gold  
      24858                   50M Pistol (60 Shots)  Bronze  
      24878                     Skeet (125 Targets)  Silver  
      24993                              Individual  Bronze  
      25656                               Decathlon    Gold  
      25673                               High Jump  Bronze  
      25996                      C-2 (Canoe Double)  Bronze  
      25997                      C-2 (Canoe Double)  Bronze  
      26628                  Individual Competition  Bronze  
      26756  Quadruple Sculls Without Coxswain (4X)  Silver  
      26757  Quadruple Sculls Without Coxswain (4X)  Silver  
      26758  Quadruple Sculls Without Coxswain (4X)  Silver  
      26759  Quadruple Sculls Without Coxswain (4X)  Silver  
      26804           Single-Handed Dinghy (Europe)  Silver  
      26838                10M Air Rifle (40 Shots)  Bronze  
      26849                25M Pistol (30+30 Shots)  Silver  
      27690                           Javelin Throw    Gold  
      28010                      C-2 (Canoe Double)  Silver  
      28011                      C-2 (Canoe Double)  Silver  
      28788                      Single Sculls (1X)  Silver  
      28853                10M Air Rifle (40 Shots)    Gold  
      28869      50M Rifle 3 Positions (3X20 Shots)  Silver  
      28886                      Trap (125 Targets)    Gold  
      29635                            400M Hurdles  Bronze  
      29738                           Javelin Throw  Bronze  
      29739                           Javelin Throw    Gold  
      29930                            K-1 (Single)  Silver  
      29985                               K-4 1000M  Bronze  
      29986                               K-4 1000M  Bronze  
      29987                               K-4 1000M  Bronze  
      29988                               K-4 1000M  Bronze  
      30075                           Cross-Country    Gold  
      30635                              Individual    Gold  
      30780                           Single Sculls  Silver  
      30782                           Single Sculls    Gold  
      30859                   50M Rifle 3 Positions  Bronze  
      30942                                 Doubles  Silver  
      30943                                 Doubles  Silver  ),
     ('DEN',
             Year    City          Sport     Discipline                  Athlete  \
      69     1896  Athens        Fencing        Fencing          NIELSEN, Holger   
      120    1896  Athens       Shooting       Shooting          NIELSEN, Holger   
      125    1896  Athens       Shooting       Shooting          NIELSEN, Holger   
      129    1896  Athens       Shooting       Shooting            JENSEN, Viggo   
      144    1896  Athens  Weightlifting  Weightlifting            JENSEN, Viggo   
      ...     ...     ...            ...            ...                      ...   
      30783  2012  London         Rowing         Rowing       ERICHSEN, Fie Udby   
      30801  2012  London        Sailing        Sailing              LANG, Peter   
      30802  2012  London        Sailing        Sailing        NORREGAARD, Allan   
      30813  2012  London        Sailing        Sailing  HOGH-CHRISTENSEN, Jonas   
      30867  2012  London       Shooting       Shooting          GOLDING, Anders   
      
            Country Gender                             Event   Medal  
      69        DEN    Men                  Sabre Individual  Bronze  
      120       DEN    Men  25M Rapid Fire Pistol (60 Shots)  Bronze  
      125       DEN    Men             50M Pistol (60 Shots)  Silver  
      129       DEN    Men                  Army Rifle, 300M  Bronze  
      144       DEN    Men       Heavyweight - One Hand Lift  Silver  
      ...       ...    ...                               ...     ...  
      30783     DEN  Women                     Single Sculls  Silver  
      30801     DEN    Men                      49Er - Skiff  Bronze  
      30802     DEN    Men                      49Er - Skiff  Bronze  
      30813     DEN    Men                              Finn  Silver  
      30867     DEN    Men                             Skeet  Silver  
      
      [507 rows x 9 columns]),
     ('DJI',
             Year   City      Sport Discipline               Athlete Country Gender  \
      18422  1988  Seoul  Athletics  Athletics  AHMED SALAH, Hussein     DJI    Men   
      
                Event   Medal  
      18422  Marathon  Bronze  ),
     ('DOM',
             Year         City      Sport Discipline                  Athlete  \
      17035  1984  Los Angeles     Boxing     Boxing          NOLASCO, Pedres   
      25578  2004       Athens  Athletics  Athletics           SANCHEZ, Felix   
      27916  2008      Beijing     Boxing     Boxing              DIAZ, Felix   
      28967  2008      Beijing  Taekwondo  Taekwondo  MERCEDES, Yulis Gabriel   
      29625  2012       London  Athletics  Athletics         SANTOS, Luguelin   
      29630  2012       London  Athletics  Athletics           SANCHEZ, Felix   
      
            Country Gender                     Event   Medal  
      17035     DOM    Men  51 - 54KG (Bantamweight)  Bronze  
      25578     DOM    Men              400M Hurdles    Gold  
      27916     DOM    Men                60 - 64 KG    Gold  
      28967     DOM    Men                   - 58 KG  Silver  
      29625     DOM    Men                      400M  Silver  
      29630     DOM    Men              400M Hurdles    Gold  ),
     ('ECU',
             Year     City      Sport Discipline           Athlete Country Gender  \
      21622  1996  Atlanta  Athletics  Athletics  PEREZ, Jefferson     ECU    Men   
      27580  2008  Beijing  Athletics  Athletics  PEREZ, Jefferson     ECU    Men   
      
                 Event   Medal  
      21622  20KM Walk    Gold  
      27580  20KM Walk  Silver  ),
     ('EGY',
             Year         City          Sport           Discipline  \
      5006   1928    Amsterdam       Aquatics               Diving   
      5010   1928    Amsterdam       Aquatics               Diving   
      5673   1928    Amsterdam  Weightlifting        Weightlifting   
      5712   1928    Amsterdam      Wrestling      Wrestling Gre-R   
      7147   1936       Berlin  Weightlifting        Weightlifting   
      7149   1936       Berlin  Weightlifting        Weightlifting   
      7155   1936       Berlin  Weightlifting        Weightlifting   
      7157   1936       Berlin  Weightlifting        Weightlifting   
      7159   1936       Berlin  Weightlifting        Weightlifting   
      7959   1948       London  Weightlifting        Weightlifting   
      7962   1948       London  Weightlifting        Weightlifting   
      7963   1948       London  Weightlifting        Weightlifting   
      8002   1948       London      Wrestling      Wrestling Gre-R   
      8015   1948       London      Wrestling      Wrestling Gre-R   
      8892   1952     Helsinki      Wrestling      Wrestling Gre-R   
      10085  1960         Rome         Boxing               Boxing   
      10652  1960         Rome      Wrestling      Wrestling Gre-R   
      17642  1984  Los Angeles           Judo                 Judo   
      25883  2004       Athens         Boxing               Boxing   
      25917  2004       Athens         Boxing               Boxing   
      25921  2004       Athens         Boxing               Boxing   
      26949  2004       Athens      Taekwondo            Taekwondo   
      27169  2004       Athens      Wrestling      Wrestling Gre-R   
      28635  2008      Beijing           Judo                 Judo   
      30145  2012       London        Fencing              Fencing   
      31082  2012       London  Weightlifting        Weightlifting   
      31089  2012       London  Weightlifting        Weightlifting   
      31158  2012       London      Wrestling  Wrestling Freestyle   
      
                                         Athlete Country Gender  \
      5006                        SIMAIKA, Farid     EGY    Men   
      5010                        SIMAIKA, Farid     EGY    Men   
      5673             NOSSEIR, El Sayed Mohamed     EGY    Men   
      5712                    MOUSTAPHA, Ibrahim     EGY    Men   
      7147              SHAMS, Ibrahim Hassanein     EGY    Men   
      7149                SOLIMAN, Saleh Mohamed     EGY    Men   
      7155           MESBAH, Anwar Mohamed Ahmed     EGY    Men   
      7157              EL TOUNY, Khadr El Sayed     EGY    Men   
      7159                        WASIF, Ibrahim     EGY    Men   
      7959                        FAYAD, Mahmoud     EGY    Men   
      7962              SHAMS, Ibrahim Hassanein     EGY    Men   
      7963                HAMOUDA, Attia Mohamed     EGY    Men   
      8002                   HASSAN ALI, Mahmoud     EGY    Men   
      8015                        ORABI, Ibrahim     EGY    Men   
      8892               RASHED, Abdel Aal Ahmed     EGY    Men   
      10085               EL GINDY, Abdel Moneim     EGY    Men   
      10652                         SAYED, Osman     EGY    Men   
      17642                     RASHWAN, Mohamed     EGY    Men   
      25883                         ALY, Mohamed     EGY    Men   
      25917                        ISMAIL, Ahmed     EGY    Men   
      25921                     ELSAYED, Mohamed     EGY    Men   
      26949                       BAYOUMI, Tamer     EGY    Men   
      27169                 GABER IBRAHIM, Karam     EGY    Men   
      28635                       MESBAH, Hesham     EGY    Men   
      30145              ABOUELKASSEM, Alaaeldin     EGY    Men   
      31082  ABIR ABDELRAHMAN, Khalil Mahmoud K.     EGY  Women   
      31089         ABDELAZIM, Tarek Yehia Fouad     EGY    Men   
      31158         EBRAHIM, Karam Mohamed Gaber     EGY    Men   
      
                                              Event   Medal  
      5006                             10M Platform  Silver  
      5010                           3M Springboard  Bronze  
      5673   75 - 82.5KG, Total (Light-Heavyweight)    Gold  
      5712          75 - 82.5KG (Light-Heavyweight)    Gold  
      7147            - 60KG, Total (Featherweight)  Bronze  
      7149            - 60KG, Total (Featherweight)  Silver  
      7155         60 - 67.5KG, Total (Lightweight)    Gold  
      7157        67.5 - 75KG, Total (Middleweight)    Gold  
      7159   75 - 82.5KG, Total (Light-Heavyweight)  Bronze  
      7959         56 - 60KG, Total (Featherweight)    Gold  
      7962         60 - 67.5KG, Total (Lightweight)    Gold  
      7963         60 - 67.5KG, Total (Lightweight)  Silver  
      8002                 52 - 57KG (Bantamweight)  Silver  
      8015            79 - 87KG (Light-Heavyweight)  Bronze  
      8892                57 - 61KG (Featherweight)  Bronze  
      10085                      - 51KG (Flyweight)  Bronze  
      10652                      - 52KG (Flyweight)  Silver  
      17642                           Open Category  Silver  
      25883              + 91KG (Super Heavyweight)  Silver  
      25917           75 - 81KG (Light-Heavyweight)  Bronze  
      25921                 81 - 91KG (Heavyweight)  Bronze  
      26949                                 - 58 KG  Bronze  
      27169                               84 - 96KG    Gold  
      28635                81 - 90KG (Middleweight)  Bronze  
      30145                         Foil Individual  Silver  
      31082                                    75KG  Silver  
      31089                                    85KG  Bronze  
      31158                                Wg 84 KG  Silver  ),
     ('ERI',
             Year    City      Sport Discipline            Athlete Country Gender  \
      25532  2004  Athens  Athletics  Athletics  TADESSE, Zersenay     ERI    Men   
      
              Event   Medal  
      25532  10000M  Bronze  ),
     ('ESP',
             Year     City          Sport           Discipline  \
      306    1900    Paris  Basque Pelota        Basque Pelota   
      307    1900    Paris  Basque Pelota        Basque Pelota   
      3315   1920  Antwerp       Football             Football   
      3316   1920  Antwerp       Football             Football   
      3317   1920  Antwerp       Football             Football   
      ...     ...      ...            ...                  ...   
      30906  2012   London      Taekwondo            Taekwondo   
      30931  2012   London      Taekwondo            Taekwondo   
      30959  2012   London      Triathlon            Triathlon   
      31081  2012   London  Weightlifting        Weightlifting   
      31124  2012   London      Wrestling  Wrestling Freestyle   
      
                                 Athlete Country Gender        Event   Medal  
      306     De AMEZOLA y ASPIZUA, José     ESP    Men  Cesta Punta    Gold  
      307    VILLOTA BAQUIOLA, Francisco     ESP    Men  Cesta Punta    Gold  
      3315                ACEDO, Domingo     ESP    Men     Football  Silver  
      3316           ARABOLAZA, Patricio     ESP    Men     Football  Silver  
      3317               ARRATE, Mariano     ESP    Men     Football  Silver  
      ...                            ...     ...    ...          ...     ...  
      30906       GONZALEZ BONILLA, Joel     ESP    Men      - 58 KG    Gold  
      30931        GARCIA HEMME, Nicolas     ESP    Men   68 - 80 KG  Silver  
      30959                GOMEZ, Javier     ESP    Men   Individual  Silver  
      31081        VALENTIN PEREZ, Lidia     ESP  Women         75KG    Gold  
      31124                 UNDA, Maider     ESP  Women     Wf 72 KG  Bronze  
      
      [442 rows x 9 columns]),
     ('EST',
             Year       City          Sport           Discipline  \
      3093   1920    Antwerp      Athletics            Athletics   
      4076   1920    Antwerp  Weightlifting        Weightlifting   
      4081   1920    Antwerp  Weightlifting        Weightlifting   
      4324   1924      Paris      Athletics            Athletics   
      4953   1924      Paris  Weightlifting        Weightlifting   
      4959   1924      Paris  Weightlifting        Weightlifting   
      4961   1924      Paris  Weightlifting        Weightlifting   
      4987   1924      Paris      Wrestling      Wrestling Gre-R   
      4998   1924      Paris      Wrestling      Wrestling Gre-R   
      5633   1928  Amsterdam        Sailing              Sailing   
      5634   1928  Amsterdam        Sailing              Sailing   
      5635   1928  Amsterdam        Sailing              Sailing   
      5636   1928  Amsterdam        Sailing              Sailing   
      5637   1928  Amsterdam        Sailing              Sailing   
      5665   1928  Amsterdam  Weightlifting        Weightlifting   
      5685   1928  Amsterdam      Wrestling      Wrestling Free.   
      5703   1928  Amsterdam      Wrestling      Wrestling Gre-R   
      5708   1928  Amsterdam      Wrestling      Wrestling Gre-R   
      6585   1936     Berlin         Boxing               Boxing   
      7150   1936     Berlin  Weightlifting        Weightlifting   
      7166   1936     Berlin      Wrestling      Wrestling Free.   
      7182   1936     Berlin      Wrestling      Wrestling Free.   
      7187   1936     Berlin      Wrestling      Wrestling Gre-R   
      7192   1936     Berlin      Wrestling      Wrestling Gre-R   
      7201   1936     Berlin      Wrestling      Wrestling Gre-R   
      20346  1992  Barcelona        Cycling        Cycling Track   
      21003  1992  Barcelona        Sailing              Sailing   
      21004  1992  Barcelona        Sailing              Sailing   
      23638  2000     Sydney      Athletics            Athletics   
      24585  2000     Sydney           Judo                 Judo   
      24621  2000     Sydney           Judo                 Judo   
      25658  2004     Athens      Athletics            Athletics   
      26580  2004     Athens           Judo                 Judo   
      26774  2004     Athens         Rowing               Rowing   
      27666  2008    Beijing      Athletics            Athletics   
      28658  2008    Beijing         Rowing               Rowing   
      28659  2008    Beijing         Rowing               Rowing   
      29715  2012     London      Athletics            Athletics   
      31138  2012     London      Wrestling  Wrestling Freestyle   
      
                                  Athlete Country Gender  \
      3093                 LOSSMANN, Jüri     EST    Men   
      4076                SCHMIDT, Alfred     EST    Men   
      4081                NEULAND, Alfred     EST    Men   
      4324   KLUMBERG-KOLMPERE, Alexander     EST    Men   
      4953                 TAMMER, Harald     EST    Men   
      4959                   KIKKAS, Jaan     EST    Men   
      4961                NEULAND, Alfred     EST    Men   
      4987                 PÜTSEP, Eduard     EST    Men   
      4998               STEINBERG, Roman     EST    Men   
      5633                  FAEHLMANN, A.     EST    Men   
      5634                  FAEHLMANN, G.     EST    Men   
      5635                      VOGDT, E.     EST    Men   
      5636                  VON WIREN, W.     EST    Men   
      5637                   WEKSCHIN, N.     EST    Men   
      5665                LUHAÄÄR, Arnold     EST    Men   
      5685                   KAPP, Osvald     EST    Men   
      5703                       WALI, W.     EST    Men   
      5708                KUSNETS, Albert     EST    Men   
      6585              STEPULOV, Nikolai     EST    Men   
      7150                LUHAÄÄR, Arnold     EST    Men   
      7166             PALUSALU, Kristjan     EST    Men   
      7182              NEO, Ago (August)     EST    Men   
      7187             PALUSALU, Kristjan     EST    Men   
      7192                 VÄLI, Voldemar     EST    Men   
      7201              NEO, Ago (August)     EST    Men   
      20346                SALUMAE, Erika     EST  Women   
      21003                 TONISTE, Tonu     EST    Men   
      21004               TONISTE, Toomas     EST    Men   
      23638                    NOOL, Erki     EST    Men   
      24585             PERTELSON, Indrek     EST    Men   
      24621              BUDOLIN, Aleksei     EST    Men   
      25658           TAMMERT, Aleksander     EST    Men   
      26580             PERTELSON, Indrek     EST    Men   
      26774                JAANSON, Jueri     EST    Men   
      27666                  KANTER, Gerd     EST    Men   
      28658               ENDREKSON, Tonu     EST    Men   
      28659                 JAANSON, Juri     EST    Men   
      29715                  KANTER, Gerd     EST    Men   
      31138                   NABI, Heiki     EST    Men   
      
                                                         Event   Medal  
      3093                                            Marathon  Silver  
      4076       - 60KG, One-Two Hand 3 Events (Featherweight)  Silver  
      4081    60 - 67.5KG, One-Two Hand 3 Events (Lightweight)    Gold  
      4324                                           Decathlon  Bronze  
      4953       + 82.5KG, One-Two Hand 5 Events (Heavyweight)  Bronze  
      4959   67.5 - 75KG, One-Two Hand 5 Events (Middleweight)  Bronze  
      4961   67.5 - 75KG, One-Two Hand 5 Events (Middleweight)  Silver  
      4987                               - 58KG (Bantamweight)    Gold  
      4998                          67.5 - 75KG (Middleweight)  Bronze  
      5633                                                  6M  Bronze  
      5634                                                  6M  Bronze  
      5635                                                  6M  Bronze  
      5636                                                  6M  Bronze  
      5637                                                  6M  Bronze  
      5665                       + 82.5KG, Total (Heavyweight)  Silver  
      5685                             61 - 66KG (Lightweight)    Gold  
      5703                           58 - 60KG (Featherweight)    Gold  
      5708                          67.5 - 75KG (Middleweight)  Bronze  
      6585                       57.15 - 61.24KG (Lightweight)  Silver  
      7150                       + 82.5KG, Total (Heavyweight)  Bronze  
      7166                                + 87KG (Heavyweight)    Gold  
      7182                       79 - 87KG (Light-Heavyweight)  Silver  
      7187                          + 87KG (Super Heavyweight)    Gold  
      7192                             61 - 66KG (Lightweight)  Bronze  
      7201                       79 - 87KG (Light-Heavyweight)  Bronze  
      20346                                             Sprint    Gold  
      21003                            470 - Two Person Dinghy  Bronze  
      21004                            470 - Two Person Dinghy  Bronze  
      23638                                          Decathlon    Gold  
      24585                              + 100KG (Heavyweight)  Bronze  
      24621                      73 - 81KG (Half-Middleweight)  Bronze  
      25658                                       Discus Throw  Bronze  
      26580                              + 100KG (Heavyweight)  Bronze  
      26774                                 Single Sculls (1X)  Silver  
      27666                                       Discus Throw    Gold  
      28658                                 Double Sculls (2X)  Silver  
      28659                                 Double Sculls (2X)  Silver  
      29715                                       Discus Throw  Bronze  
      31138                                          Wg 120 KG  Silver  ),
     ('ETH',
             Year       City      Sport Discipline              Athlete Country  \
      10035  1960       Rome  Athletics  Athletics        BIKILA, Abebe     ETH   
      10937  1964      Tokyo  Athletics  Athletics        BIKILA, Abebe     ETH   
      11863  1968     Mexico  Athletics  Athletics          WOLDE, Mamo     ETH   
      11979  1968     Mexico  Athletics  Athletics          WOLDE, Mamo     ETH   
      12898  1972     Munich  Athletics  Athletics       YIFTER, Miruts     ETH   
      13030  1972     Munich  Athletics  Athletics          WOLDE, Mamo     ETH   
      15370  1980     Moscow  Athletics  Athletics      KEDIR, Mohammed     ETH   
      15371  1980     Moscow  Athletics  Athletics       YIFTER, Miruts     ETH   
      15400  1980     Moscow  Athletics  Athletics         TURA, Eshetu     ETH   
      15461  1980     Moscow  Athletics  Athletics       YIFTER, Miruts     ETH   
      19849  1992  Barcelona  Athletics  Athletics         ABEBE, Addis     ETH   
      19853  1992  Barcelona  Athletics  Athletics        TULU, Derartu     ETH   
      19962  1992  Barcelona  Athletics  Athletics         BAYISA, Fita     ETH   
      21589  1996    Atlanta  Athletics  Athletics  GEBRSELASSIE, Haile     ETH   
      21591  1996    Atlanta  Athletics  Athletics           WAMI, Gete     ETH   
      21751  1996    Atlanta  Athletics  Athletics         ROBA, Fatuma     ETH   
      23514  2000     Sydney  Athletics  Athletics      MEZGEBU, Assefa     ETH   
      23515  2000     Sydney  Athletics  Athletics  GEBRSELASSIE, Haile     ETH   
      23518  2000     Sydney  Athletics  Athletics        TULU, Derartu     ETH   
      23519  2000     Sydney  Athletics  Athletics           WAMI, Gete     ETH   
      23623  2000     Sydney  Athletics  Athletics        WOLDE, Millon     ETH   
      23625  2000     Sydney  Athletics  Athletics           WAMI, Gete     ETH   
      23674  2000     Sydney  Athletics  Athletics        TOLA, Tesfaye     ETH   
      23676  2000     Sydney  Athletics  Athletics     ABERA, Gezahegne     ETH   
      25533  2004     Athens  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      25534  2004     Athens  Athletics  Athletics      SIHINE, Sileshi     ETH   
      25535  2004     Athens  Athletics  Athletics        TULU, Derartu     ETH   
      25537  2004     Athens  Athletics  Athletics    DIBABA, Ejegayehu     ETH   
      25642  2004     Athens  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      25643  2004     Athens  Athletics  Athletics     DIBABA, Tirunesh     ETH   
      25644  2004     Athens  Athletics  Athletics       DEFAR, Meseret     ETH   
      27546  2008    Beijing  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      27547  2008    Beijing  Athletics  Athletics      SIHINE, Sileshi     ETH   
      27549  2008    Beijing  Athletics  Athletics     DIBABA, Tirunesh     ETH   
      27648  2008    Beijing  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      27650  2008    Beijing  Athletics  Athletics       DEFAR, Meseret     ETH   
      27651  2008    Beijing  Athletics  Athletics     DIBABA, Tirunesh     ETH   
      27698  2008    Beijing  Athletics  Athletics       KEBEDE, Tsegay     ETH   
      29584  2012     London  Athletics  Athletics       BEKELE, Tariku     ETH   
      29585  2012     London  Athletics  Athletics     DIBABA, Tirunesh     ETH   
      29622  2012     London  Athletics  Athletics        ASSEFA, Sofia     ETH   
      29696  2012     London  Athletics  Athletics   GEBREMESKEL, Dejen     ETH   
      29698  2012     London  Athletics  Athletics       DEFAR, Meseret     ETH   
      29700  2012     London  Athletics  Athletics     DIBABA, Tirunesh     ETH   
      29751  2012     London  Athletics  Athletics         GELANA, Tiki     ETH   
      
            Gender               Event   Medal  
      10035    Men            Marathon    Gold  
      10937    Men            Marathon    Gold  
      11863    Men              10000M  Silver  
      11979    Men            Marathon    Gold  
      12898    Men              10000M  Bronze  
      13030    Men            Marathon  Bronze  
      15370    Men              10000M  Bronze  
      15371    Men              10000M    Gold  
      15400    Men  3000M Steeplechase  Bronze  
      15461    Men               5000M    Gold  
      19849    Men              10000M  Bronze  
      19853  Women              10000M    Gold  
      19962    Men               5000M  Bronze  
      21589    Men              10000M    Gold  
      21591  Women              10000M  Bronze  
      21751  Women            Marathon    Gold  
      23514    Men              10000M  Bronze  
      23515    Men              10000M    Gold  
      23518  Women              10000M    Gold  
      23519  Women              10000M  Silver  
      23623    Men               5000M    Gold  
      23625  Women               5000M  Bronze  
      23674    Men            Marathon  Bronze  
      23676    Men            Marathon    Gold  
      25533    Men              10000M    Gold  
      25534    Men              10000M  Silver  
      25535  Women              10000M  Bronze  
      25537  Women              10000M  Silver  
      25642    Men               5000M  Silver  
      25643  Women               5000M  Bronze  
      25644  Women               5000M    Gold  
      27546    Men              10000M    Gold  
      27547    Men              10000M  Silver  
      27549  Women              10000M    Gold  
      27648    Men               5000M    Gold  
      27650  Women               5000M  Bronze  
      27651  Women               5000M    Gold  
      27698    Men            Marathon  Bronze  
      29584    Men              10000M  Bronze  
      29585  Women              10000M    Gold  
      29622  Women       3000M Steeple  Silver  
      29696    Men               5000M  Silver  
      29698  Women               5000M    Gold  
      29700  Women               5000M  Bronze  
      29751  Women            Marathon    Gold  ),
     ('EUA',
             Year                   City      Sport       Discipline  \
      8940   1956  Melbourne / Stockholm   Aquatics         Swimming   
      8941   1956  Melbourne / Stockholm   Aquatics         Swimming   
      9013   1956  Melbourne / Stockholm  Athletics        Athletics   
      9019   1956  Melbourne / Stockholm  Athletics        Athletics   
      9025   1956  Melbourne / Stockholm  Athletics        Athletics   
      ...     ...                    ...        ...              ...   
      11517  1964                  Tokyo    Sailing          Sailing   
      11650  1964                  Tokyo  Wrestling  Wrestling Free.   
      11663  1964                  Tokyo  Wrestling  Wrestling Gre-R   
      11678  1964                  Tokyo  Wrestling  Wrestling Gre-R   
      11681  1964                  Tokyo  Wrestling  Wrestling Gre-R   
      
                          Athlete Country Gender                          Event  \
      8940   TEN ELSEN, Eva-Maria     EUA  Women              200M Breaststroke   
      8941     HAPPE-KREY, Ursula     EUA  Women              200M Breaststroke   
      9013      STUBNICK, Christa     EUA  Women                           100M   
      9019    RICHTZENHAIN, Klaus     EUA    Men                          1500M   
      9025      STUBNICK, Christa     EUA  Women                           200M   
      ...                     ...     ...    ...                            ...   
      11517     KUHWEIDE, Wilhelm     EUA    Men    Single-Handed Dinghy (Finn)   
      11650    ROST, Klaus-Jürgen     EUA    Men        63 - 70KG (Lightweight)   
      11663    DIETRICH, Wilfried     EUA    Men     + 97KG (Super Heavyweight)   
      11678          METZ, Lothar     EUA    Men       78 - 87KG (Middleweight)   
      11681          KIEHL, Heinz     EUA    Men  87 - 97KG (Light-Heavyweight)   
      
              Medal  
      8940   Bronze  
      8941     Gold  
      9013   Silver  
      9019   Silver  
      9025   Silver  
      ...       ...  
      11517    Gold  
      11650  Silver  
      11663  Bronze  
      11678  Bronze  
      11681  Bronze  
      
      [260 rows x 9 columns]),
     ('EUN',
             Year       City      Sport       Discipline                   Athlete  \
      19602  1992  Barcelona   Aquatics           Diving          MIROCHINA, Elena   
      19603  1992  Barcelona   Aquatics           Diving            SAUTIN, Dmitry   
      19608  1992  Barcelona   Aquatics           Diving             LACHKO, Irina   
      19619  1992  Barcelona   Aquatics         Swimming        RUDKOVSKAYA, Elena   
      19628  1992  Barcelona   Aquatics         Swimming          POPOV, Alexander   
      ...     ...        ...        ...              ...                       ...   
      21289  1992  Barcelona  Wrestling  Wrestling Gre-R       DOUGOUTCHIEV, Islam   
      21291  1992  Barcelona  Wrestling  Wrestling Gre-R    ISKANDARIAN, Mnatsakan   
      21293  1992  Barcelona  Wrestling  Wrestling Gre-R     TOURLYKHANOV, Daoulet   
      21296  1992  Barcelona  Wrestling  Wrestling Gre-R       KOGOUACHVILI, Gogui   
      21299  1992  Barcelona  Wrestling  Wrestling Gre-R  DEMIACHKIEVITCH, Serguei   
      
            Country Gender                          Event   Medal  
      19602     EUN  Women                   10M Platform  Silver  
      19603     EUN    Men                 3M Springboard  Bronze  
      19608     EUN  Women                 3M Springboard  Silver  
      19619     EUN  Women              100M Breaststroke    Gold  
      19628     EUN    Men                 100M Freestyle    Gold  
      ...       ...    ...                            ...     ...  
      21289     EUN    Men        62 - 68KG (Lightweight)  Silver  
      21291     EUN    Men       68 - 74KG (Welterweight)    Gold  
      21293     EUN    Men       74 - 82KG (Middleweight)  Bronze  
      21296     EUN    Men  82 - 90KG (Light-Heavyweight)  Bronze  
      21299     EUN    Men       90 - 100KG (Heavyweight)  Bronze  
      
      [223 rows x 9 columns]),
     ('FIN',
             Year    City       Sport   Discipline                Athlete Country  \
      1245   1908  London   Athletics    Athletics       JÄRVINEN, Werner     FIN   
      1396   1908  London  Gymnastics  Artistic G.  FORSSTRÖM, Eino Vilho     FIN   
      1397   1908  London  Gymnastics  Artistic G.        GRANSTRÖM, Otto     FIN   
      1398   1908  London  Gymnastics  Artistic G.   KEMP, Johan Valdemar     FIN   
      1399   1908  London  Gymnastics  Artistic G.       KYYKOSKI, Livara     FIN   
      ...     ...     ...         ...          ...                    ...     ...   
      29737  2012  London   Athletics    Athletics       RUUSKANEN, Antti     FIN   
      30809  2012  London     Sailing      Sailing         KANERVA, Silja     FIN   
      30810  2012  London     Sailing      Sailing        LEHTINEN, Silja     FIN   
      30811  2012  London     Sailing      Sailing         WULFF, Mikaela     FIN   
      30825  2012  London     Sailing      Sailing          PETAJA, Tuuli     FIN   
      
            Gender                       Event   Medal  
      1245     Men  Discus Throw Ancient Style  Bronze  
      1396     Men            Team Competition  Bronze  
      1397     Men            Team Competition  Bronze  
      1398     Men            Team Competition  Bronze  
      1399     Men            Team Competition  Bronze  
      ...      ...                         ...     ...  
      29737    Men               Javelin Throw  Silver  
      30809  Women                  Elliott 6M  Bronze  
      30810  Women                  Elliott 6M  Bronze  
      30811  Women                  Elliott 6M  Bronze  
      30825  Women                        Rs:X  Silver  
      
      [456 rows x 9 columns]),
     ('FRA',
             Year    City      Sport           Discipline              Athlete  \
      17     1896  Athens  Athletics            Athletics    LERMUSIAUX, Albin   
      47     1896  Athens  Athletics            Athletics   TUFFERI, Alexandre   
      51     1896  Athens    Cycling        Cycling Track        FLAMENG, Léon   
      54     1896  Athens    Cycling        Cycling Track         MASSON, Paul   
      55     1896  Athens    Cycling        Cycling Track        FLAMENG, Léon   
      ...     ...     ...        ...                  ...                  ...   
      30936  2012  London     Tennis               Tennis      LLODRA, Michael   
      30937  2012  London     Tennis               Tennis  TSONGA, Jo-Wilfried   
      30938  2012  London     Tennis               Tennis    BENNETEAU, Julien   
      30939  2012  London     Tennis               Tennis     GASQUET, Richard   
      31151  2012  London  Wrestling  Wrestling Freestyle       GUENOT, Steeve   
      
            Country Gender        Event   Medal  
      17        FRA    Men        1500M  Bronze  
      47        FRA    Men  Triple Jump  Silver  
      51        FRA    Men        100KM    Gold  
      54        FRA    Men         10KM    Gold  
      55        FRA    Men         10KM  Silver  
      ...       ...    ...          ...     ...  
      30936     FRA    Men      Doubles  Silver  
      30937     FRA    Men      Doubles  Silver  
      30938     FRA    Men      Doubles  Bronze  
      30939     FRA    Men      Doubles  Bronze  
      31151     FRA    Men     Wg 66 KG  Bronze  
      
      [1396 rows x 9 columns]),
     ('FRG',
             Year    City          Sport       Discipline               Athlete  \
      11759  1968  Mexico       Aquatics         Swimming     HOLTHAUS, Michael   
      11801  1968  Mexico       Aquatics         Swimming        FROMMATER, Uta   
      11802  1968  Mexico       Aquatics         Swimming  HUSTEDE-NAGEL, Heike   
      11803  1968  Mexico       Aquatics         Swimming       KRAUS, Angelika   
      11804  1968  Mexico       Aquatics         Swimming   REINECK, Heidemarie   
      ...     ...     ...            ...              ...                   ...   
      19433  1988   Seoul         Tennis           Tennis          GRAF, Steffi   
      19513  1988   Seoul  Weightlifting    Weightlifting       ZAWIEJA, Martin   
      19515  1988   Seoul  Weightlifting    Weightlifting    NERLINGER, Manfred   
      19534  1988   Seoul  Weightlifting    Weightlifting    IMMESBERGER, Peter   
      19596  1988   Seoul      Wrestling  Wrestling Gre-R       HIMMEL, Gerhard   
      
            Country Gender                                  Event   Medal  
      11759     FRG    Men                 400M Individual Medley  Bronze  
      11801     FRG  Women                    4X100M Medley Relay  Bronze  
      11802     FRG  Women                    4X100M Medley Relay  Bronze  
      11803     FRG  Women                    4X100M Medley Relay  Bronze  
      11804     FRG  Women                    4X100M Medley Relay  Bronze  
      ...       ...    ...                                    ...     ...  
      19433     FRG  Women                                Singles    Gold  
      19513     FRG    Men     + 110KG, Total (Super Heavyweight)  Bronze  
      19515     FRG    Men     + 110KG, Total (Super Heavyweight)  Silver  
      19534     FRG    Men  90 - 100KG, Total (First-Heavyweight)  Bronze  
      19596     FRG    Men               90 - 100KG (Heavyweight)  Silver  
      
      [490 rows x 9 columns]),
     ('GAB',
             Year    City      Sport Discipline         Athlete Country Gender  \
      30915  2012  London  Taekwondo  Taekwondo  OBAME, Anthony     GAB    Men   
      
               Event   Medal  
      30915  + 80 KG  Silver  ),
     ('GBR',
             Year    City      Sport     Discipline             Athlete Country  \
      16     1896  Athens  Athletics      Athletics  GOULDING, Grantley     GBR   
      20     1896  Athens  Athletics      Athletics     GMELIN, Charles     GBR   
      48     1896  Athens    Cycling   Cycling Road      BATTEL, Edward     GBR   
      57     1896  Athens    Cycling  Cycling Track      KEEPING, Frank     GBR   
      140    1896  Athens     Tennis         Tennis        BOLAND, John     GBR   
      ...     ...     ...        ...            ...                 ...     ...   
      30948  2012  London     Tennis         Tennis        MURRAY, Andy     GBR   
      30949  2012  London     Tennis         Tennis       ROBSON, Laura     GBR   
      30952  2012  London     Tennis         Tennis        MURRAY, Andy     GBR   
      30958  2012  London  Triathlon      Triathlon  BROWNLEE, Alistair     GBR   
      30960  2012  London  Triathlon      Triathlon  BROWNLEE, Jonathan     GBR   
      
            Gender                 Event   Medal  
      16       Men          110M Hurdles  Silver  
      20       Men                  400M  Bronze  
      48       Men  Individual Road Race  Bronze  
      57       Men          12-Hour Race  Silver  
      140      Men               Singles    Gold  
      ...      ...                   ...     ...  
      30948    Men         Mixed Doubles  Silver  
      30949  Women         Mixed Doubles  Silver  
      30952    Men               Singles    Gold  
      30958    Men            Individual    Gold  
      30960    Men            Individual  Bronze  
      
      [1720 rows x 9 columns]),
     ('GDR',
             Year    City          Sport       Discipline            Athlete  \
      11697  1968  Mexico       Aquatics         Swimming    MATTHES, Roland   
      11724  1968  Mexico       Aquatics         Swimming    MATTHES, Roland   
      11740  1968  Mexico       Aquatics         Swimming     LINDNER, Helga   
      11762  1968  Mexico       Aquatics         Swimming  STEINBACH, Sabine   
      11785  1968  Mexico       Aquatics         Swimming   KRAUSE, Roswitha   
      ...     ...     ...            ...              ...                ...   
      19388  1988   Seoul       Shooting         Shooting       WEGNER, Axel   
      19516  1988   Seoul  Weightlifting    Weightlifting      WELLER, Ronny   
      19523  1988   Seoul  Weightlifting    Weightlifting      KUNZ, Joachim   
      19527  1988   Seoul  Weightlifting    Weightlifting  STEINHOEFEL, Ingo   
      19540  1988   Seoul      Wrestling  Wrestling Free.  SCHRÖDER, Andreas   
      
            Country Gender                              Event   Medal  
      11697     GDR    Men                    100M Backstroke    Gold  
      11724     GDR    Men                    200M Backstroke    Gold  
      11740     GDR  Women                     200M Butterfly  Silver  
      11762     GDR  Women             400M Individual Medley  Bronze  
      11785     GDR  Women             4X100M Freestyle Relay  Silver  
      ...       ...    ...                                ...     ...  
      19388     GDR    Men                Skeet (125 Targets)    Gold  
      19516     GDR    Men   100 - 110KG, Total (Heavyweight)  Bronze  
      19523     GDR    Men   60 - 67.5KG, Total (Lightweight)    Gold  
      19527     GDR    Men  67.5 - 75KG, Total (Middleweight)  Silver  
      19540     GDR    Men    100 - 130KG (Super Heavyweight)  Bronze  
      
      [825 rows x 9 columns]),
     ('GEO',
             Year     City          Sport           Discipline  \
      22655  1996  Atlanta           Judo                 Judo   
      23125  1996  Atlanta      Wrestling      Wrestling Free.   
      23911  2000   Sydney         Boxing               Boxing   
      24606  2000   Sydney           Judo                 Judo   
      25122  2000   Sydney  Weightlifting        Weightlifting   
      25146  2000   Sydney      Wrestling      Wrestling Free.   
      25158  2000   Sydney      Wrestling      Wrestling Gre-R   
      25167  2000   Sydney      Wrestling      Wrestling Gre-R   
      26579  2004   Athens           Judo                 Judo   
      26622  2004   Athens           Judo                 Judo   
      27115  2004   Athens  Weightlifting        Weightlifting   
      27170  2004   Athens      Wrestling      Wrestling Gre-R   
      28636  2008  Beijing           Judo                 Judo   
      28846  2008  Beijing       Shooting             Shooting   
      29166  2008  Beijing      Wrestling      Wrestling Free.   
      29179  2008  Beijing      Wrestling      Wrestling Free.   
      29182  2008  Beijing      Wrestling      Wrestling Free.   
      29203  2008  Beijing      Wrestling      Wrestling Gre-R   
      30607  2012   London           Judo                 Judo   
      31094  2012   London      Wrestling  Wrestling Freestyle   
      31102  2012   London      Wrestling  Wrestling Freestyle   
      31132  2012   London      Wrestling  Wrestling Freestyle   
      31136  2012   London      Wrestling  Wrestling Freestyle   
      31146  2012   London      Wrestling  Wrestling Freestyle   
      31152  2012   London      Wrestling  Wrestling Freestyle   
      
                               Athlete Country Gender  \
      22655         LIPARTELIANI, Soso     GEO    Men   
      23125         KURTANIDZE, Eldari     GEO    Men   
      23911       TCHANTURIA, Vladimer     GEO    Men   
      24606       VAZAGASHVILI, Giorgi     GEO    Men   
      25122           ASANIDZE, George     GEO    Men   
      25146         KURTANIDZE, Eldari     GEO    Men   
      25158             CHACHUA, Akaki     GEO    Men   
      25167      VAKHTANGADZE, Mukhran     GEO    Men   
      26579          KHERGIANI, Nestor     GEO    Men   
      26622           ZVIADAURI, Zurab     GEO    Men   
      27115           ASANIDZE, George     GEO    Men   
      27170             NOZADZE, Ramaz     GEO    Men   
      28636         TSIREKIDZE, Irakli     GEO    Men   
      28846           SALUKVADZE, Nino     GEO  Women   
      29166          TUSHISHVILI, Otar     GEO    Men   
      29179      MINDORASHVILI, Revazi     GEO    Men   
      29182        GOGSHELIDZE, George     GEO    Men   
      29203        KVIRKELIA, Manuchar     GEO    Men   
      30607     SHAVDATUASHVILI, Lasha     GEO    Men   
      31094      MODZMANASHVILI, Davit     GEO    Men   
      31102  KHINCHEGASHVILI, Vladimer     GEO    Men   
      31132        MARSAGISHVILI, Dato     GEO    Men   
      31136        GOGSHELIDZE, George     GEO    Men   
      31146             LASHKHI, Revaz     GEO    Men   
      31152        TSKHADAIA, Manuchar     GEO    Men   
      
                                     Event   Medal  
      22655  73 - 81KG (Half-Middleweight)  Bronze  
      23125  82 - 90KG (Light-Heavyweight)  Bronze  
      23911        81 - 91KG (Heavyweight)  Bronze  
      24606   60 - 66KG (Half-Lightweight)  Bronze  
      25122                           85KG  Bronze  
      25146                      85 - 97KG  Bronze  
      25158                      58 - 63KG  Bronze  
      25167                      76 - 85KG  Bronze  
      26579                        - 60 KG  Silver  
      26622       81 - 90KG (Middleweight)    Gold  
      27115                           85KG    Gold  
      27170                      84 - 96KG  Silver  
      28636       81 - 90KG (Middleweight)    Gold  
      28846      10M Air Pistol (40 Shots)  Bronze  
      29166                      60 - 66KG  Bronze  
      29179                      74 - 84KG    Gold  
      29182                      84 - 96KG  Bronze  
      29203                      66 - 74KG    Gold  
      30607                      60 - 66KG    Gold  
      31094                       Wf 120KG  Silver  
      31102                       Wf 55 KG  Silver  
      31132                       Wf 84 KG  Bronze  
      31136                       Wf 96 KG  Bronze  
      31146                       Wg 60 KG  Silver  
      31152                       Wg 66 KG  Bronze  ),
     ('GER',
             Year    City         Sport        Discipline               Athlete  \
      14     1896  Athens     Athletics         Athletics        HOFMANN, Fritz   
      50     1896  Athens       Cycling      Cycling Road      GOEDRICH, August   
      72     1896  Athens    Gymnastics       Artistic G.  WEINGÄRTNER, Hermann   
      73     1896  Athens    Gymnastics       Artistic G.        FLATOW, Alfred   
      74     1896  Athens    Gymnastics       Artistic G.        FLATOW, Alfred   
      ...     ...     ...           ...               ...                   ...   
      30891  2012  London  Table Tennis      Table Tennis   OVTCHAROV, Dimitrij   
      30892  2012  London  Table Tennis      Table Tennis       STEGER, Bastian   
      30924  2012  London     Taekwondo         Taekwondo         FROMM, Helena   
      30964  2012  London    Volleyball  Beach Volleyball         BRINK, Julius   
      30965  2012  London    Volleyball  Beach Volleyball     RECKERMANN, Jonas   
      
            Country Gender                 Event   Medal  
      14        GER    Men                  100M  Silver  
      50        GER    Men  Individual Road Race  Silver  
      72        GER    Men        Horizontal Bar    Gold  
      73        GER    Men        Horizontal Bar  Silver  
      74        GER    Men         Parallel Bars    Gold  
      ...       ...    ...                   ...     ...  
      30891     GER    Men                  Team  Bronze  
      30892     GER    Men                  Team  Bronze  
      30924     GER  Women            57 - 67 KG  Bronze  
      30964     GER    Men      Beach Volleyball    Gold  
      30965     GER    Men      Beach Volleyball    Gold  
      
      [1305 rows x 9 columns]),
     ('GHA',
             Year       City     Sport Discipline                  Athlete Country  \
      10108  1960       Rome    Boxing     Boxing         QUARTEY, Clement     GHA   
      11010  1964      Tokyo    Boxing     Boxing             BLAY, Edward     GHA   
      13120  1972     Munich    Boxing     Boxing          AMARTEY, Prince     GHA   
      20482  1992  Barcelona  Football   Football  ACHEAMPONG, Joachin Yaw     GHA   
      20483  1992  Barcelona  Football   Football              ADDO, Simon     GHA   
      20484  1992  Barcelona  Football   Football             ADJEI, Sammi     GHA   
      20485  1992  Barcelona  Football   Football          AMANKWAH, Frank     GHA   
      20486  1992  Barcelona  Football   Football       ARYEE, Bernard Nii     GHA   
      20487  1992  Barcelona  Football   Football             ASARE, Isaac     GHA   
      20488  1992  Barcelona  Football   Football              AYEW, Kwame     GHA   
      20489  1992  Barcelona  Football   Football          DOSSEY, Ibrahim     GHA   
      20490  1992  Barcelona  Football   Football          GARGO, Mohammed     GHA   
      20491  1992  Barcelona  Football   Football     KUMAH, Samuel Ablade     GHA   
      20492  1992  Barcelona  Football   Football     LAMPTEY, Nii Odartey     GHA   
      20493  1992  Barcelona  Football   Football               PREKO, Yaw     GHA   
      20494  1992  Barcelona  Football   Football             QUAYE, Shamo     GHA   
      
            Gender                             Event   Medal  
      10108    Men  60 - 63.5KG (Light-Welterweight)  Silver  
      11010    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      13120    Men                           71-75KG  Bronze  
      20482    Men                          Football  Bronze  
      20483    Men                          Football  Bronze  
      20484    Men                          Football  Bronze  
      20485    Men                          Football  Bronze  
      20486    Men                          Football  Bronze  
      20487    Men                          Football  Bronze  
      20488    Men                          Football  Bronze  
      20489    Men                          Football  Bronze  
      20490    Men                          Football  Bronze  
      20491    Men                          Football  Bronze  
      20492    Men                          Football  Bronze  
      20493    Men                          Football  Bronze  
      20494    Men                          Football  Bronze  ),
     ('GRE',
             Year     City      Sport Discipline                 Athlete Country  \
      2      1896   Athens   Aquatics   Swimming       DRIVAS, Dimitrios     GRE   
      3      1896   Athens   Aquatics   Swimming      MALOKINIS, Ioannis     GRE   
      4      1896   Athens   Aquatics   Swimming      CHASAPIS, Spiridon     GRE   
      5      1896   Athens   Aquatics   Swimming   CHOROPHAS, Efstathios     GRE   
      7      1896   Athens   Aquatics   Swimming        ANDREOU, Joannis     GRE   
      ...     ...      ...        ...        ...                     ...     ...   
      28839  2008  Beijing    Sailing    Sailing     PAPADOPOULOU, Sofia     GRE   
      28975  2008  Beijing  Taekwondo  Taekwondo  NIKOLAIDIS, Alexandros     GRE   
      30629  2012   London       Judo       Judo          ILIADIS, Ilias     GRE   
      30753  2012   London     Rowing     Rowing  GIAZITZIDOU, Christina     GRE   
      30754  2012   London     Rowing     Rowing      TSIAVOU, Alexandra     GRE   
      
            Gender                       Event   Medal  
      2        Men  100M Freestyle For Sailors  Bronze  
      3        Men  100M Freestyle For Sailors    Gold  
      4        Men  100M Freestyle For Sailors  Silver  
      5        Men             1200M Freestyle  Bronze  
      7        Men             1200M Freestyle  Silver  
      ...      ...                         ...     ...  
      28839  Women          Yngling - Keelboat  Bronze  
      28975    Men                     + 80 KG  Silver  
      30629    Men                   81 - 90KG  Bronze  
      30753  Women         Lightweight Doubles  Bronze  
      30754  Women         Lightweight Doubles  Bronze  
      
      [148 rows x 9 columns]),
     ('GRN',
             Year    City      Sport Discipline        Athlete Country Gender Event  \
      29624  2012  London  Athletics  Athletics  JAMES, Kirani     GRN    Men  400M   
      
            Medal  
      29624  Gold  ),
     ('GUA',
             Year    City      Sport Discipline          Athlete Country Gender  \
      29616  2012  London  Athletics  Athletics  BARRONDO, Erick     GUA    Men   
      
                 Event   Medal  
      29616  20KM Walk  Silver  ),
     ('GUY',
             Year    City   Sport Discipline           Athlete Country Gender  \
      15604  1980  Moscow  Boxing     Boxing  ANTHONY, Michael     GUY    Men   
      
                                Event   Medal  
      15604  51 - 54KG (Bantamweight)  Bronze  ),
     ('HAI',
            Year       City      Sport Discipline            Athlete Country Gender  \
      4881  1924      Paris   Shooting   Shooting  AUGUSTIN, Ludovic     HAI    Men   
      4882  1924      Paris   Shooting   Shooting    CLERMONT, L. H.     HAI    Men   
      4883  1924      Paris   Shooting   Shooting    DESTINE, Destin     HAI    Men   
      4884  1924      Paris   Shooting   Shooting          DUPRE, C.     HAI    Men   
      4885  1924      Paris   Shooting   Shooting  METULLUS, St Eloi     HAI    Men   
      4886  1924      Paris   Shooting   Shooting    ROLLAND, Astrel     HAI    Men   
      4887  1924      Paris   Shooting   Shooting  VALBORGE, Ludovic     HAI    Men   
      5186  1928  Amsterdam  Athletics  Athletics   CATOR, Silvio M.     HAI    Men   
      
                                      Event   Medal  
      4881  400, 600, 800M Free Rifle, Team  Bronze  
      4882  400, 600, 800M Free Rifle, Team  Bronze  
      4883  400, 600, 800M Free Rifle, Team  Bronze  
      4884  400, 600, 800M Free Rifle, Team  Bronze  
      4885  400, 600, 800M Free Rifle, Team  Bronze  
      4886  400, 600, 800M Free Rifle, Team  Bronze  
      4887  400, 600, 800M Free Rifle, Team  Bronze  
      5186                        Long Jump  Silver  ),
     ('HKG',
             Year     City         Sport     Discipline        Athlete Country  \
      22829  1996  Atlanta       Sailing        Sailing  LEE, Lai Shan     HKG   
      26932  2004   Athens  Table Tennis   Table Tennis   KO, Lai Chak     HKG   
      26933  2004   Athens  Table Tennis   Table Tennis      LI, Ching     HKG   
      30025  2012   London       Cycling  Cycling Track   LEE, Wai Sze     HKG   
      
            Gender            Event   Medal  
      22829  Women  Board (Mistral)    Gold  
      26932    Men          Doubles  Silver  
      26933    Men          Doubles  Silver  
      30025  Women           Keirin  Bronze  ),
     ('HUN',
             Year    City              Sport           Discipline           Athlete  \
      0      1896  Athens           Aquatics             Swimming     HAJOS, Alfred   
      6      1896  Athens           Aquatics             Swimming     HAJOS, Alfred   
      12     1896  Athens          Athletics            Athletics  SZOKOLYI, Alajos   
      25     1896  Athens          Athletics            Athletics      DANI, Nandor   
      35     1896  Athens          Athletics            Athletics    KELLNER, Gyula   
      ...     ...     ...                ...                  ...               ...   
      30608  2012  London               Judo                 Judo   UNGVARI, Miklos   
      30637  2012  London  Modern Pentathlon    Modern Pentathlon      MAROSI, Adam   
      31127  2012  London          Wrestling  Wrestling Freestyle      HATOS, Gabor   
      31143  2012  London          Wrestling  Wrestling Freestyle      MODOS, Peter   
      31150  2012  London          Wrestling  Wrestling Freestyle    LORINCZ, Tamas   
      
            Country Gender            Event   Medal  
      0         HUN    Men   100M Freestyle    Gold  
      6         HUN    Men  1200M Freestyle    Gold  
      12        HUN    Men             100M  Bronze  
      25        HUN    Men             800M  Silver  
      35        HUN    Men         Marathon  Bronze  
      ...       ...    ...              ...     ...  
      30608     HUN    Men        60 - 66KG  Silver  
      30637     HUN    Men       Individual  Bronze  
      31127     HUN    Men         Wf 74 KG  Bronze  
      31143     HUN    Men         Wg 55 KG  Bronze  
      31150     HUN    Men         Wg 66 KG  Silver  
      
      [1079 rows x 9 columns]),
     ('INA',
             Year       City          Sport     Discipline  \
      18274  1988      Seoul        Archery        Archery   
      18275  1988      Seoul        Archery        Archery   
      18276  1988      Seoul        Archery        Archery   
      20033  1992  Barcelona      Badminton      Badminton   
      20034  1992  Barcelona      Badminton      Badminton   
      20044  1992  Barcelona      Badminton      Badminton   
      20045  1992  Barcelona      Badminton      Badminton   
      20046  1992  Barcelona      Badminton      Badminton   
      20049  1992  Barcelona      Badminton      Badminton   
      21768  1996    Atlanta      Badminton      Badminton   
      21769  1996    Atlanta      Badminton      Badminton   
      21771  1996    Atlanta      Badminton      Badminton   
      21772  1996    Atlanta      Badminton      Badminton   
      21789  1996    Atlanta      Badminton      Badminton   
      21791  1996    Atlanta      Badminton      Badminton   
      23701  2000     Sydney      Badminton      Badminton   
      23702  2000     Sydney      Badminton      Badminton   
      23706  2000     Sydney      Badminton      Badminton   
      23715  2000     Sydney      Badminton      Badminton   
      23718  2000     Sydney      Badminton      Badminton   
      25092  2000     Sydney  Weightlifting  Weightlifting   
      25094  2000     Sydney  Weightlifting  Weightlifting   
      25095  2000     Sydney  Weightlifting  Weightlifting   
      25715  2004     Athens      Badminton      Badminton   
      25716  2004     Athens      Badminton      Badminton   
      25733  2004     Athens      Badminton      Badminton   
      25734  2004     Athens      Badminton      Badminton   
      27092  2004     Athens  Weightlifting  Weightlifting   
      27725  2008    Beijing      Badminton      Badminton   
      27726  2008    Beijing      Badminton      Badminton   
      27730  2008    Beijing      Badminton      Badminton   
      27739  2008    Beijing      Badminton      Badminton   
      27743  2008    Beijing      Badminton      Badminton   
      29100  2008    Beijing  Weightlifting  Weightlifting   
      29121  2008    Beijing  Weightlifting  Weightlifting   
      31061  2012     London  Weightlifting  Weightlifting   
      31071  2012     London  Weightlifting  Weightlifting   
      31076  2012     London  Weightlifting  Weightlifting   
      
                              Athlete Country Gender                         Event  \
      18274         HANDAYANI, Lilies     INA  Women              Teams Fita Round   
      18275      SAIMAN, Nurfitriyana     INA  Women              Teams Fita Round   
      18276          WARDHANI, Kusuma     INA  Women              Teams Fita Round   
      20033             GUNAWAN, Rudy     INA    Men                       Doubles   
      20034             HARTONO, Eddy     INA    Men                       Doubles   
      20044         SUSANTO, Hermawan     INA    Men                       Singles   
      20045         BUDI KUSUMA, Alan     INA    Men                       Singles   
      20046  WIRANATA, Ardy Bernardus     INA    Men                       Singles   
      20049             SUSANTI, Susi     INA  Women                       Singles   
      21768         IRIANTO, Antonius     INA    Men                       Doubles   
      21769            KANTONO, Denny     INA    Men                       Doubles   
      21771      MAINAKY, Rexy Ronald     INA    Men                       Doubles   
      21772     SUBAGJA, Ricky Achmad     INA    Men                       Doubles   
      21789             SUSANTI, Susi     INA  Women                       Singles   
      21791               AUDINA, Mia     INA  Women                       Singles   
      23701             GUNAWAN, Tony     INA    Men                       Doubles   
      23702            WIJAYA, Candra     INA    Men                       Doubles   
      23706          KUSHANJANTO, Tri     INA    Men                       Doubles   
      23715            TIMUR, Minarti     INA  Women                       Doubles   
      23718                 HENDRAWAN     INA    Men                       Singles   
      25092            INDRIYANI, Sri     INA  Women                          48KG   
      25094      RUMBEWAS, Raema Lisa     INA  Women                          48KG   
      25095     SLAMET, Winarni Binti     INA  Women                          53KG   
      25715                 HIAN, Eng     INA    Men                       Doubles   
      25716           LIMPELE, Flandy     INA    Men                       Doubles   
      25733         KUNCORO, Soni Dwi     INA    Men                       Singles   
      25734           HIDAYAT, Taufik     INA    Men                       Singles   
      27092      RUMBEWAS, Raema Lisa     INA  Women                          53KG   
      27725              KIDO, Markis     INA    Men                       Doubles   
      27726          SETIAWAN, Hendra     INA    Men                       Doubles   
      27730            WIDIANTO, Nova     INA    Men                       Doubles   
      27739                  LILIYANA     INA  Women                       Doubles   
      27743   YULIANTI, Maria Kristin     INA  Women                       Singles   
      29100          IRAWAN, Eko Yuli     INA    Men  - 56KG, Total (Bantamweight)   
      29121                  TRIYATNO     INA    Men                          62KG   
      31061          FEBRIANTI, Citra     INA  Women                          53KG   
      31071          IRAWAN, Eko Yuli     INA    Men                          62KG   
      31076        TRIYATNO, Triyatno     INA    Men                          69KG   
      
              Medal  
      18274  Silver  
      18275  Silver  
      18276  Silver  
      20033  Silver  
      20034  Silver  
      20044  Bronze  
      20045    Gold  
      20046  Silver  
      20049    Gold  
      21768  Bronze  
      21769  Bronze  
      21771    Gold  
      21772    Gold  
      21789  Bronze  
      21791  Silver  
      23701    Gold  
      23702    Gold  
      23706  Silver  
      23715  Silver  
      23718  Silver  
      25092  Bronze  
      25094  Silver  
      25095  Bronze  
      25715  Bronze  
      25716  Bronze  
      25733  Bronze  
      25734    Gold  
      27092  Silver  
      27725    Gold  
      27726    Gold  
      27730  Silver  
      27739  Silver  
      27743  Bronze  
      29100  Bronze  
      29121  Bronze  
      31061  Silver  
      31071  Bronze  
      31076  Silver  ),
     ('IND',
             Year       City      Sport           Discipline               Athlete  \
      241    1900      Paris  Athletics            Athletics     PRITCHARD, Norman   
      244    1900      Paris  Athletics            Athletics     PRITCHARD, Norman   
      5512   1928  Amsterdam     Hockey               Hockey  ALLEN, Richard James   
      5513   1928  Amsterdam     Hockey               Hockey           CHAND, Dyan   
      5514   1928  Amsterdam     Hockey               Hockey   GATELEY, Maurice A.   
      ...     ...        ...        ...                  ...                   ...   
      29879  2012     London     Boxing               Boxing             KOM, Mary   
      30841  2012     London   Shooting             Shooting         NARANG, Gagan   
      30849  2012     London   Shooting             Shooting          KUMAR, Vijay   
      31111  2012     London  Wrestling  Wrestling Freestyle       DUTT, Yogeshwar   
      31118  2012     London  Wrestling  Wrestling Freestyle         KUMAR, Sushil   
      
            Country Gender             Event   Medal  
      241       IND    Men              200M  Silver  
      244       IND    Men      200M Hurdles  Silver  
      5512      IND    Men            Hockey    Gold  
      5513      IND    Men            Hockey    Gold  
      5514      IND    Men            Hockey    Gold  
      ...       ...    ...               ...     ...  
      29879     IND  Women             51 KG  Bronze  
      30841     IND    Men     10M Air Rifle  Bronze  
      30849     IND    Men  25M Rapid Pistol  Silver  
      31111     IND    Men          Wf 60 KG  Bronze  
      31118     IND    Men          Wf 66 KG  Silver  
      
      [184 rows x 9 columns]),
     ('IOP',
             Year       City     Sport Discipline             Athlete Country  \
      21056  1992  Barcelona  Shooting   Shooting      SEKARIC, Jasna     IOP   
      21060  1992  Barcelona  Shooting   Shooting      BINDER, Aranka     IOP   
      21081  1992  Barcelona  Shooting   Shooting  PLETIKOSIC, Stevan     IOP   
      
            Gender                       Event   Medal  
      21056  Women   10M Air Pistol (40 Shots)  Silver  
      21060  Women    10M Air Rifle (40 Shots)  Bronze  
      21081    Men  50M Rifle Prone (60 Shots)  Bronze  ),
     ('IRI',
             Year      City          Sport           Discipline  \
      7958   1948    London  Weightlifting        Weightlifting   
      8838   1952  Helsinki  Weightlifting        Weightlifting   
      8840   1952  Helsinki  Weightlifting        Weightlifting   
      8859   1952  Helsinki      Wrestling      Wrestling Free.   
      8870   1952  Helsinki      Wrestling      Wrestling Free.   
      ...     ...       ...            ...                  ...   
      31126  2012    London      Wrestling  Wrestling Freestyle   
      31131  2012    London      Wrestling  Wrestling Freestyle   
      31141  2012    London      Wrestling  Wrestling Freestyle   
      31145  2012    London      Wrestling  Wrestling Freestyle   
      31161  2012    London      Wrestling  Wrestling Freestyle   
      
                                       Athlete Country Gender  \
      7958            SALMASSI, Jafar Mohammad     IRI    Men   
      8838                         MIRZAI, Ali     IRI    Men   
      8840                    NAMDJOU, Mahmoud     IRI    Men   
      8859              MOLLAGHASSEMI, Mahmoud     IRI    Men   
      8870                  GUIVEGTCHI, Nasser     IRI    Men   
      ...                                  ...     ...    ...   
      31126             GOUDARZI, Sadegh Saeed     IRI    Men   
      31131              LASHGARI, Ehsan Naser     IRI    Men   
      31141  SORYAN REIHANPOUR, Hamid Mohammad     IRI    Men   
      31145                 NOROOZI, Omid Haji     IRI    Men   
      31161          REZAEI, Ghasem Gholamreza     IRI    Men   
      
                                        Event   Medal  
      7958   56 - 60KG, Total (Featherweight)  Bronze  
      8838       - 56KG, Total (Bantamweight)  Bronze  
      8840       - 56KG, Total (Bantamweight)  Silver  
      8859                 - 52KG (Flyweight)  Bronze  
      8870          57 - 63KG (Featherweight)  Silver  
      ...                                 ...     ...  
      31126                          Wf 74 KG  Silver  
      31131                          Wf 84 KG  Bronze  
      31141                          Wg 55 KG    Gold  
      31145                          Wg 60 KG    Gold  
      31161                          Wg 96 KG    Gold  
      
      [61 rows x 9 columns]),
     ('IRL',
             Year                   City       Sport Discipline  \
      5173   1928              Amsterdam   Athletics  Athletics   
      5827   1932            Los Angeles   Athletics  Athletics   
      5887   1932            Los Angeles   Athletics  Athletics   
      8291   1952               Helsinki      Boxing     Boxing   
      9018   1956  Melbourne / Stockholm   Athletics  Athletics   
      9168   1956  Melbourne / Stockholm      Boxing     Boxing   
      9177   1956  Melbourne / Stockholm      Boxing     Boxing   
      9184   1956  Melbourne / Stockholm      Boxing     Boxing   
      9195   1956  Melbourne / Stockholm      Boxing     Boxing   
      11007  1964                  Tokyo      Boxing     Boxing   
      15600  1980                 Moscow      Boxing     Boxing   
      16392  1980                 Moscow     Sailing    Sailing   
      16393  1980                 Moscow     Sailing    Sailing   
      16934  1984            Los Angeles   Athletics  Athletics   
      20198  1992              Barcelona      Boxing     Boxing   
      20213  1992              Barcelona      Boxing     Boxing   
      21356  1996                Atlanta    Aquatics   Swimming   
      21369  1996                Atlanta    Aquatics   Swimming   
      21375  1996                Atlanta    Aquatics   Swimming   
      21381  1996                Atlanta    Aquatics   Swimming   
      23627  2000                 Sydney   Athletics  Athletics   
      27898  2008                Beijing      Boxing     Boxing   
      27923  2008                Beijing      Boxing     Boxing   
      27929  2008                Beijing      Boxing     Boxing   
      29703  2012                 London   Athletics  Athletics   
      29875  2012                 London      Boxing     Boxing   
      29883  2012                 London      Boxing     Boxing   
      29885  2012                 London      Boxing     Boxing   
      29896  2012                 London      Boxing     Boxing   
      30113  2012                 London  Equestrian    Jumping   
      
                                     Athlete Country Gender  \
      5173              O'CALLAGHAN, Patrick     IRL    Men   
      5827   TISDALL, Robert Morton Newburgh     IRL    Men   
      5887              O'CALLAGHAN, Patrick     IRL    Men   
      8291                     MCNALLY, John     IRL    Men   
      9018            DELANY, Ronald Michael     IRL    Men   
      9168                    CALDWELL, John     IRL    Men   
      9177                 GILROY, Frederick     IRL    Men   
      9184                    BYRNE, Anthony     IRL    Men   
      9195                       TIEDT, Fred     IRL    Men   
      11007           MCCOURT, James Vincent     IRL    Men   
      15600                    RUSSELL, Hugh     IRL    Men   
      16392                   WILKINS, David     IRL    Men   
      16393                 WILKINSON, James     IRL    Men   
      16934                     TREACY, John     IRL    Men   
      20198                MCCULLOUGH, Wayne     IRL    Men   
      20213                 CARRUTH, Michael     IRL    Men   
      21356            SMITH, Michelle Marie     IRL  Women   
      21369            SMITH, Michelle Marie     IRL  Women   
      21375            SMITH, Michelle Marie     IRL  Women   
      21381            SMITH, Michelle Marie     IRL  Women   
      23627                O'SULLIVAN, Sonia     IRL  Women   
      27898                    BARNES, Paddy     IRL    Men   
      27923          SUTHERLAND, Darren John     IRL    Men   
      27929                      EGAN, Kenny     IRL    Men   
      29703                HEFFERNAN, Robert     IRL    Men   
      29875                    BARNES, Paddy     IRL    Men   
      29883                  CONLAN, Michael     IRL    Men   
      29885                  NEVIN, John Joe     IRL    Men   
      29896                    TAYLOR, Katie     IRL  Women   
      30113                    OCONNOR, Cian     IRL    Men   
      
                                     Event   Medal  
      5173                    Hammer Throw    Gold  
      5827                    400M Hurdles    Gold  
      5887                    Hammer Throw    Gold  
      8291        51 - 54KG (Bantamweight)  Silver  
      9018                           1500M    Gold  
      9168              - 51KG (Flyweight)  Bronze  
      9177        51 - 54KG (Bantamweight)  Bronze  
      9184         57 - 60KG (Lightweight)  Bronze  
      9195      63.5 - 67KG (Welterweight)  Silver  
      11007        57 - 60KG (Lightweight)  Bronze  
      15600          48 - 51KG (Flyweight)  Bronze  
      16392                Flying Dutchman  Silver  
      16393                Flying Dutchman  Silver  
      16934                       Marathon  Silver  
      20198       51 - 54KG (Bantamweight)  Silver  
      20213     63.5 - 67KG (Welterweight)    Gold  
      21356                 200M Butterfly  Bronze  
      21369         200M Individual Medley    Gold  
      21375                 400M Freestyle    Gold  
      21381         400M Individual Medley    Gold  
      23627                          5000M  Silver  
      27898         48KG (Light Flywieght)  Bronze  
      27923                     69 - 75 KG  Bronze  
      27929  75 - 81KG (Light-Heavyweight)  Silver  
      29703                      50KM Walk  Bronze  
      29875                      46 - 49KG  Bronze  
      29883                           52KG  Bronze  
      29885                           56KG  Silver  
      29896                          60 KG    Gold  
      30113                     Individual  Bronze  ),
     ('IRQ',
             Year  City          Sport     Discipline            Athlete Country  \
      10614  1960  Rome  Weightlifting  Weightlifting  WAHID AZIZ, Abdul     IRQ   
      
            Gender                             Event   Medal  
      10614    Men  60 - 67.5KG, Total (Lightweight)  Bronze  ),
     ('ISL',
             Year                   City      Sport Discipline  \
      9131   1956  Melbourne / Stockholm  Athletics  Athletics   
      17635  1984            Los Angeles       Judo       Judo   
      23683  2000                 Sydney  Athletics  Athletics   
      28432  2008                Beijing   Handball   Handball   
      28433  2008                Beijing   Handball   Handball   
      28434  2008                Beijing   Handball   Handball   
      28435  2008                Beijing   Handball   Handball   
      28436  2008                Beijing   Handball   Handball   
      28437  2008                Beijing   Handball   Handball   
      28438  2008                Beijing   Handball   Handball   
      28439  2008                Beijing   Handball   Handball   
      28440  2008                Beijing   Handball   Handball   
      28441  2008                Beijing   Handball   Handball   
      28442  2008                Beijing   Handball   Handball   
      28443  2008                Beijing   Handball   Handball   
      28444  2008                Beijing   Handball   Handball   
      28445  2008                Beijing   Handball   Handball   
      
                               Athlete Country Gender                         Event  \
      9131       EINARSSON, Vilhjalmur     ISL    Men                   Triple Jump   
      17635        FRIDRIKSSON, Bjarni     ISL    Men  86 - 95KG (Half-Heavyweight)   
      23683          FLOSADOTTIR, Vala     ISL  Women                    Pole Vault   
      28432         ASGEIRSSON, Sturla     ISL    Men                      Handball   
      28433             ATLASON, Arnor     ISL    Men                      Handball   
      28434             GEIRSSON, Logi     ISL    Men                      Handball   
      28435  GUDJONSSON, Snorri Steinn     ISL    Men                      Handball   
      28436  GUDMUNDSSON, Hreidar Levy     ISL    Men                      Handball   
      28437         GUNNARSSON, Robert     ISL    Men                      Handball   
      28438  GUSTAVSSON, Bjorgvin Pall     ISL    Men                      Handball   
      28439   HALLGRIMSSON, Asgeir Orn     ISL    Men                      Handball   
      28440  INGIMUNDARSON, Ingimundur     ISL    Men                      Handball   
      28441  JAKOBSSON, Sverre Andreas     ISL    Men                      Handball   
      28442       PETERSSON, Alexander     ISL    Men                      Handball   
      28443   SIGURDSSON, Gudjon Valur     ISL    Men                      Handball   
      28444         SIGURDSSON, Sigfus     ISL    Men                      Handball   
      28445         STEFANSSON, Olafur     ISL    Men                      Handball   
      
              Medal  
      9131   Silver  
      17635  Bronze  
      23683  Bronze  
      28432  Silver  
      28433  Silver  
      28434  Silver  
      28435  Silver  
      28436  Silver  
      28437  Silver  
      28438  Silver  
      28439  Silver  
      28440  Silver  
      28441  Silver  
      28442  Silver  
      28443  Silver  
      28444  Silver  
      28445  Silver  ),
     ('ISR',
             Year       City          Sport       Discipline            Athlete  \
      20806  1992  Barcelona           Judo             Judo         ARAD, Yael   
      20816  1992  Barcelona           Judo             Judo  SMADJA, Shay Oren   
      22825  1996    Atlanta        Sailing          Sailing       FRIDMAN, Gal   
      23935  2000     Sydney  Canoe / Kayak  Canoe / Kayak F  KOLGANOV, Michael   
      26625  2004     Athens           Judo             Judo       ZEEVI, Ariel   
      26797  2004     Athens        Sailing          Sailing       FRIDMAN, Gal   
      28819  2008    Beijing        Sailing          Sailing     ZUBARI, Shahar   
      
            Country Gender                          Event   Medal  
      20806     ISR  Women  56 - 61KG (Half-Middleweight)  Silver  
      20816     ISR    Men        65 - 71KG (Lightweight)  Bronze  
      22825     ISR    Men                Board (Mistral)  Bronze  
      23935     ISR    Men        K-1 500M (Kayak Single)  Bronze  
      26625     ISR    Men  90 - 100KG (Half-Heavyweight)  Bronze  
      26797     ISR    Men                Board (Mistral)    Gold  
      28819     ISR    Men              Rs:X - Windsurfer  Bronze  ),
     ('ISV',
             Year   City    Sport Discipline          Athlete Country Gender  \
      19341  1988  Seoul  Sailing    Sailing  HOLMBERG, Peter     ISV    Men   
      
                                   Event   Medal  
      19341  Single-Handed Dinghy (Finn)  Silver  ),
     ('ITA',
             Year    City       Sport  Discipline                 Athlete Country  \
      350    1900   Paris  Equestrian     Jumping  TRISSINO, Gian Giorgio     ITA   
      356    1900   Paris  Equestrian     Jumping  TRISSINO, Gian Giorgio     ITA   
      376    1900   Paris     Fencing     Fencing          CONTE, Antonio     ITA   
      377    1900   Paris     Fencing     Fencing         SANTELLI, Italo     ITA   
      1241   1908  London   Athletics   Athletics          LUNGHI, Emilio     ITA   
      ...     ...     ...         ...         ...                     ...     ...   
      31007  2012  London  Volleyball  Volleyball           PAPI, Samuele     ITA   
      31008  2012  London  Volleyball  Volleyball          PARODI, Simone     ITA   
      31009  2012  London  Volleyball  Volleyball        SAVANI, Cristian     ITA   
      31010  2012  London  Volleyball  Volleyball         TRAVICA, Dragan     ITA   
      31011  2012  London  Volleyball  Volleyball           ZAYTSEV, Ivan     ITA   
      
            Gender                 Event   Medal  
      350      Men             High Jump    Gold  
      356      Men  Long Jump Individual  Silver  
      376      Men        Sabre, Masters    Gold  
      377      Men        Sabre, Masters  Silver  
      1241     Men                  800M  Silver  
      ...      ...                   ...     ...  
      31007    Men            Volleyball  Bronze  
      31008    Men            Volleyball  Bronze  
      31009    Men            Volleyball  Bronze  
      31010    Men            Volleyball  Bronze  
      31011    Men            Volleyball  Bronze  
      
      [1296 rows x 9 columns]),
     ('JAM',
             Year      City      Sport Discipline                  Athlete Country  \
      7323   1948    London  Athletics  Athletics             WINT, Arthur     JAM   
      7324   1948    London  Athletics  Athletics        MCKENLEY, Herbert     JAM   
      7372   1948    London  Athletics  Athletics             WINT, Arthur     JAM   
      8122   1952  Helsinki  Athletics  Athletics        MCKENLEY, Herbert     JAM   
      8142   1952  Helsinki  Athletics  Athletics   RHODEN, Vincent George     JAM   
      ...     ...       ...        ...        ...                      ...     ...   
      29690  2012    London  Athletics  Athletics           DAY, Christine     JAM   
      29691  2012    London  Athletics  Athletics          LLOYD, Shereefa     JAM   
      29692  2012    London  Athletics  Athletics         WHYTE, Rosemarie     JAM   
      29693  2012    London  Athletics  Athletics       WILLIAMS, Shericka     JAM   
      29694  2012    London  Athletics  Athletics  WILLIAMS-MILLS, Novlene     JAM   
      
            Gender         Event   Medal  
      7323     Men          400M    Gold  
      7324     Men          400M  Silver  
      7372     Men          800M  Silver  
      8122     Men          100M  Silver  
      8142     Men          400M    Gold  
      ...      ...           ...     ...  
      29690  Women  4X400M Relay  Bronze  
      29691  Women  4X400M Relay  Bronze  
      29692  Women  4X400M Relay  Bronze  
      29693  Women  4X400M Relay  Bronze  
      29694  Women  4X400M Relay  Bronze  
      
      [127 rows x 9 columns]),
     ('JPN',
             Year       City      Sport           Discipline               Athlete  \
      4030   1920    Antwerp     Tennis               Tennis     KASHIO, Seiichiro   
      4031   1920    Antwerp     Tennis               Tennis       KUMAGAE, Ichiya   
      4046   1920    Antwerp     Tennis               Tennis       KUMAGAE, Ichiya   
      4971   1924      Paris  Wrestling      Wrestling Free.     NAITO, Katsutoshi   
      5022   1928  Amsterdam   Aquatics             Swimming      TAKAISHI, Katsuo   
      ...     ...        ...        ...                  ...                   ...   
      31104  2012     London  Wrestling  Wrestling Freestyle      YUMOTO, Shinichi   
      31105  2012     London  Wrestling  Wrestling Freestyle        YOSHIDA, Saori   
      31113  2012     London  Wrestling  Wrestling Freestyle           ICHO, Kaori   
      31117  2012     London  Wrestling  Wrestling Freestyle  YONEMITSU, Tatsuhiro   
      31148  2012     London  Wrestling  Wrestling Freestyle    MATSUMOTO, Ryutaro   
      
            Country Gender                      Event   Medal  
      4030      JPN    Men                    Doubles  Silver  
      4031      JPN    Men                    Doubles  Silver  
      4046      JPN    Men                    Singles  Silver  
      4971      JPN    Men  56 - 61KG (Featherweight)  Bronze  
      5022      JPN    Men             100M Freestyle  Bronze  
      ...       ...    ...                        ...     ...  
      31104     JPN    Men                   Wf 55 KG  Bronze  
      31105     JPN  Women                   Wf 55 KG    Gold  
      31113     JPN  Women                   Wf 63 KG    Gold  
      31117     JPN    Men                   Wf 66 KG    Gold  
      31148     JPN    Men                   Wg 60 KG  Bronze  
      
      [788 rows x 9 columns]),
     ('KAZ',
             Year     City              Sport           Discipline  \
      21935  1996  Atlanta             Boxing               Boxing   
      21949  1996  Atlanta             Boxing               Boxing   
      21956  1996  Atlanta             Boxing               Boxing   
      21966  1996  Atlanta             Boxing               Boxing   
      22667  1996  Atlanta  Modern Pentathlon      Modern Pentath.   
      22876  1996  Atlanta           Shooting             Shooting   
      22887  1996  Atlanta           Shooting             Shooting   
      22890  1996  Atlanta           Shooting             Shooting   
      23097  1996  Atlanta      Weightlifting        Weightlifting   
      23107  1996  Atlanta          Wrestling      Wrestling Free.   
      23141  1996  Atlanta          Wrestling      Wrestling Gre-R   
      23527  2000   Sydney          Athletics            Athletics   
      23873  2000   Sydney             Boxing               Boxing   
      23877  2000   Sydney             Boxing               Boxing   
      23884  2000   Sydney             Boxing               Boxing   
      23900  2000   Sydney             Boxing               Boxing   
      24000  2000   Sydney            Cycling         Cycling Road   
      25148  2000   Sydney          Wrestling      Wrestling Free.   
      25655  2004   Athens          Athletics            Athletics   
      25901  2004   Athens             Boxing               Boxing   
      25910  2004   Athens             Boxing               Boxing   
      25915  2004   Athens             Boxing               Boxing   
      27113  2004   Athens      Weightlifting        Weightlifting   
      27143  2004   Athens          Wrestling      Wrestling Free.   
      27159  2004   Athens          Wrestling      Wrestling Gre-R   
      27173  2004   Athens          Wrestling      Wrestling Gre-R   
      27920  2008  Beijing             Boxing               Boxing   
      27927  2008  Beijing             Boxing               Boxing   
      28641  2008  Beijing               Judo                 Judo   
      28972  2008  Beijing          Taekwondo            Taekwondo   
      29106  2008  Beijing      Weightlifting        Weightlifting   
      29126  2008  Beijing      Weightlifting        Weightlifting   
      29135  2008  Beijing      Weightlifting        Weightlifting   
      29143  2008  Beijing      Weightlifting        Weightlifting   
      29162  2008  Beijing          Wrestling      Wrestling Free.   
      29184  2008  Beijing          Wrestling      Wrestling Free.   
      29186  2008  Beijing          Wrestling      Wrestling Free.   
      29193  2008  Beijing          Wrestling      Wrestling Gre-R   
      29208  2008  Beijing          Wrestling      Wrestling Gre-R   
      29769  2012   London          Athletics            Athletics   
      29870  2012   London             Boxing               Boxing   
      29900  2012   London             Boxing               Boxing   
      29909  2012   London             Boxing               Boxing   
      29915  2012   London             Boxing               Boxing   
      30007  2012   London            Cycling         Cycling Road   
      31080  2012   London      Weightlifting        Weightlifting   
      31120  2012   London          Wrestling  Wrestling Freestyle   
      31123  2012   London          Wrestling  Wrestling Freestyle   
      31159  2012   London          Wrestling  Wrestling Freestyle   
      
                             Athlete Country Gender  \
      21935        DZUMADILOV, Bulat     KAZ    Men   
      21949      NIYAZYMBETOV, Bolat     KAZ    Men   
      21956       IBZAIMOV, Ezmouhan     KAZ    Men   
      21966           JIROV, Vasilii     KAZ    Men   
      22667       PARYGIN, Alexander     KAZ    Men   
      22876    VOKHMIANINE, Vladimir     KAZ    Men   
      22887          BELIAEV, Sergey     KAZ    Men   
      22890          BELIAEV, Sergey     KAZ    Men   
      23097        KHRAPATY, Anatoli     KAZ    Men   
      23107          MAMYROV, Maulen     KAZ    Men   
      23141       MELNICHENKO, Yuriy     KAZ    Men   
      23527         SHISHIGINA, Olga     KAZ  Women   
      23873  DILDABEKOV, Mukhtarkhan     KAZ    Men   
      23877         JUMADILOV, Bulat     KAZ    Men   
      23884     SATTARKHANOV, Bekzat     KAZ    Men   
      23900      IBRAIMOV, Yermakhan     KAZ    Men   
      24000      VINOKUROV, Alexandr     KAZ    Men   
      25148        BAIRAMUKOV, Islam     KAZ    Men   
      25655          KARPOV, Dmitriy     KAZ    Men   
      25901           YELEUOV, Serik     KAZ    Men   
      25910       ARTAYEV, Bakhtiyar     KAZ    Men   
      25915       GOLOVKIN, Gennadiy     KAZ    Men   
      27113        FILIMONOV, Sergey     KAZ    Men   
      27143        LALIYEV, Gennadiy     KAZ    Men   
      27159       MANUKYAN, Mkkhitar     KAZ    Men   
      27173      TSURTSUMIA, Georgiy     KAZ    Men   
      27920      SARSEKBAYEV, Bakhyt     KAZ    Men   
      27927   SHYNALIYEV, Yerkebulan     KAZ    Men   
      28641        ZHITKEYEV, Askhat     KAZ    Men   
      28972         CHILMANOV, Arman     KAZ    Men   
      29106    GRABOVETSKAYA, Mariya     KAZ  Women   
      29126        NEKRASSOVA, Irina     KAZ  Women   
      29135          VAZHENINA, Alla     KAZ  Women   
      29143               ILIN, Ilya     KAZ    Men   
      29162        SHALYGINA, Yelena     KAZ  Women   
      29184        TIGIYEV, Taimuraz     KAZ    Men   
      29186         MUTALIMOV, Marid     KAZ    Men   
      29193    TENGIZBAYEV, Nurbakyt     KAZ    Men   
      29208          MAMBETOV, Asset     KAZ    Men   
      29769           RYPAKOVA, Olga     KAZ  Women   
      29870             DYCHKO, Ivan     KAZ    Men   
      29900           SAPIYEV, Serik     KAZ    Men   
      29909    NIYAZYMBETOV, Adilbek     KAZ    Men   
      29915          VOLNOVA, Marina     KAZ  Women   
      30007      VINOKUROV, Alexandr     KAZ    Men   
      31080    NURMUKHAMBETOVA, Anna     KAZ  Women   
      31120      TANATAROV, Akzhurek     KAZ    Men   
      31123         MANYUROVA, Guzel     KAZ  Women   
      31159          GAJIYEV, Danyal     KAZ    Men   
      
                                            Event   Medal  
      21935                 48 - 51KG (Flyweight)  Silver  
      21949      60 - 63.5KG (Light-Welterweight)  Bronze  
      21956        67 - 71KG (Light-Middleweight)  Bronze  
      21966         75 - 81KG (Light-Heavyweight)    Gold  
      22667                Individual Competition    Gold  
      22876      25M Rapid Fire Pistol (60 Shots)  Bronze  
      22887    50M Rifle 3 Positions (3X40 Shots)  Silver  
      22890            50M Rifle Prone (60 Shots)  Silver  
      23097  91 - 99KG, Total (First-Heavyweight)  Silver  
      23107                 48 - 52KG (Flyweight)  Bronze  
      23141              52 - 57KG (Bantamweight)    Gold  
      23527                          100M Hurdles    Gold  
      23873            + 91KG (Super Heavyweight)  Silver  
      23877                 48 - 51KG (Flyweight)  Silver  
      23884             54 - 57KG (Featherweight)    Gold  
      23900        67 - 71KG (Light-Middleweight)    Gold  
      24000                  Individual Road Race  Silver  
      25148                             85 - 97KG  Silver  
      25655                             Decathlon  Bronze  
      25901               57 - 60KG (Lightweight)  Bronze  
      25910                            64 - 69 KG    Gold  
      25915                            69 - 75 KG  Silver  
      27113                                  77KG  Silver  
      27143                             66 - 74KG  Silver  
      27159                             60 - 66KG  Bronze  
      27173                            96 - 120KG  Silver  
      27920                            64 - 69 KG    Gold  
      27927         75 - 81KG (Light-Heavyweight)  Bronze  
      28641         90 - 100KG (Half-Heavyweight)  Silver  
      28972                               + 80 KG  Bronze  
      29106                                + 75KG  Bronze  
      29126                                  63KG  Silver  
      29135                                  75KG  Silver  
      29143                                  94KG    Gold  
      29162                             55 - 63KG  Bronze  
      29184                             84 - 96KG  Silver  
      29186                            96 - 120KG  Bronze  
      29193                             55 - 60KG  Bronze  
      29208                             84 - 96KG  Bronze  
      29769                           Triple Jump    Gold  
      29870                                + 91KG  Bronze  
      29900                            64 - 69 KG    Gold  
      29909                             75 - 81KG  Silver  
      29915                                 75 KG  Bronze  
      30007                       Individual Road    Gold  
      31080                                  69KG  Bronze  
      31120                              Wf 66 KG  Bronze  
      31123                              Wf 72 KG  Bronze  
      31159                              Wg 84 KG  Bronze  ),
     ('KEN',
             Year    City      Sport Discipline                    Athlete Country  \
      10897  1964   Tokyo  Athletics  Athletics     KIPRUGUT, Wilson Chuma     KEN   
      11862  1968  Mexico  Athletics  Athletics       TEMU, Nabiba Naftali     KEN   
      11874  1968  Mexico  Athletics  Athletics            KEINO, Kipchoge     KEN   
      11886  1968  Mexico  Athletics  Athletics      BIWOTT, Amos Kipwabok     KEN   
      11887  1968  Mexico  Athletics  Athletics             KOGO, Benjamin     KEN   
      ...     ...     ...        ...        ...                        ...     ...   
      29704  2012  London  Athletics  Athletics      RUDISHA, David Lekuta     KEN   
      29706  2012  London  Athletics  Athletics             KITUM, Timothy     KEN   
      29749  2012  London  Athletics  Athletics                KIRUI, Abel     KEN   
      29750  2012  London  Athletics  Athletics  KIPROTICH, Wilson Kipsang     KEN   
      29752  2012  London  Athletics  Athletics            JEPTOO, Priscah     KEN   
      
            Gender               Event   Medal  
      10897    Men                800M  Bronze  
      11862    Men              10000M    Gold  
      11874    Men               1500M    Gold  
      11886    Men  3000M Steeplechase    Gold  
      11887    Men  3000M Steeplechase  Silver  
      ...      ...                 ...     ...  
      29704    Men                800M    Gold  
      29706    Men                800M  Bronze  
      29749    Men            Marathon  Silver  
      29750    Men            Marathon  Bronze  
      29752  Women            Marathon  Silver  
      
      [93 rows x 9 columns]),
     ('KGZ',
             Year     City      Sport       Discipline             Athlete Country  \
      24582  2000   Sydney       Judo             Judo     SMAGULOV, Aidyn     KGZ   
      29194  2008  Beijing  Wrestling  Wrestling Gre-R  TIUMENBAEV, Ruslan     KGZ   
      29200  2008  Beijing  Wrestling  Wrestling Gre-R  BEGALIEV, Kanatbek     KGZ   
      
            Gender      Event   Medal  
      24582    Men    - 60 KG  Bronze  
      29194    Men  55 - 60KG  Bronze  
      29200    Men  60 - 66KG  Silver  ),
     ('KOR',
             Year                   City          Sport           Discipline  \
      7461   1948                 London         Boxing               Boxing   
      7964   1948                 London  Weightlifting        Weightlifting   
      8289   1952               Helsinki         Boxing               Boxing   
      8850   1952               Helsinki  Weightlifting        Weightlifting   
      9179   1956  Melbourne / Stockholm         Boxing               Boxing   
      ...     ...                    ...            ...                  ...   
      30907  2012                 London      Taekwondo            Taekwondo   
      30922  2012                 London      Taekwondo            Taekwondo   
      31053  2012                 London  Weightlifting        Weightlifting   
      31092  2012                 London  Weightlifting        Weightlifting   
      31149  2012                 London      Wrestling  Wrestling Freestyle   
      
                       Athlete Country Gender                              Event  \
      7461         HAN, Soo-An     KOR    Men                 - 51KG (Flyweight)   
      7964       KIM, Sung-Jip     KOR    Men  67.5 - 75KG, Total (Middleweight)   
      8289       KANG, Joon-Ho     KOR    Men           51 - 54KG (Bantamweight)   
      8850       KIM, Sung-Jip     KOR    Men  67.5 - 75KG, Total (Middleweight)   
      9179     SONG, Soon-Chun     KOR    Men           51 - 54KG (Bantamweight)   
      ...                  ...     ...    ...                                ...   
      30907       LEE, Daehoon     KOR    Men                            - 58 KG   
      30922  HWANG, Kyung Seon     KOR  Women                         57 - 67 KG   
      31053       JANG, Mi-ran     KOR  Women                              +75KG   
      31092        KIM, Minjae     KOR    Men                               94KG   
      31149      KIM, Hyeonwoo     KOR    Men                           Wg 66 KG   
      
              Medal  
      7461   Bronze  
      7964   Bronze  
      8289   Bronze  
      8850   Bronze  
      9179   Silver  
      ...       ...  
      30907  Silver  
      30922    Gold  
      31053  Bronze  
      31092  Bronze  
      31149    Gold  
      
      [529 rows x 9 columns]),
     ('KSA',
             Year    City       Sport Discipline                       Athlete  \
      23561  2000  Sydney   Athletics  Athletics                 SOMAYLI, Hadi   
      24103  2000  Sydney  Equestrian    Jumping                 ALEID, Khaled   
      30122  2012  London  Equestrian    Jumping              AL DUHAMI, Ramzy   
      30123  2012  London  Equestrian    Jumping  AL SAUD, HRH Prince Abdullah   
      30124  2012  London  Equestrian    Jumping               BAHAMDAN, Kamal   
      30125  2012  London  Equestrian    Jumping    SHARBATLY, Abdullah Waleed   
      
            Country Gender         Event   Medal  
      23561     KSA    Men  400M Hurdles  Silver  
      24103     KSA    Men    Individual  Bronze  
      30122     KSA    Men          Team  Bronze  
      30123     KSA    Men          Team  Bronze  
      30124     KSA    Men          Team  Bronze  
      30125     KSA    Men          Team  Bronze  ),
     ('KUW',
             Year    City     Sport Discipline            Athlete Country Gender  \
      24873  2000  Sydney  Shooting   Shooting  ALDEEHANI, Fehaid     KUW    Men   
      30874  2012  London  Shooting   Shooting  ALDEEHANI, Fehaid     KUW    Men   
      
                                 Event   Medal  
      24873  Double Trap (150 Targets)  Bronze  
      30874                       Trap  Bronze  ),
     ('LAT',
             Year         City              Sport        Discipline  \
      5870   1932  Los Angeles          Athletics         Athletics   
      6489   1936       Berlin          Athletics         Athletics   
      7203   1936       Berlin          Wrestling   Wrestling Gre-R   
      20233  1992    Barcelona      Canoe / Kayak   Canoe / Kayak F   
      20315  1992    Barcelona            Cycling      Cycling Road   
      21071  1992    Barcelona           Shooting          Shooting   
      21974  1996      Atlanta      Canoe / Kayak   Canoe / Kayak F   
      23630  2000       Sydney          Athletics         Athletics   
      24296  2000       Sydney         Gymnastics       Artistic G.   
      24614  2000       Sydney               Judo              Judo   
      25681  2004       Athens          Athletics         Athletics   
      26358  2004       Athens         Gymnastics       Artistic G.   
      26633  2004       Athens  Modern Pentathlon   Modern Pentath.   
      27080  2004       Athens      Weightlifting     Weightlifting   
      27688  2008      Beijing          Athletics         Athletics   
      28019  2008      Beijing            Cycling               BMX   
      29103  2008      Beijing      Weightlifting     Weightlifting   
      30001  2012       London            Cycling       Cycling BMX   
      30968  2012       London         Volleyball  Beach Volleyball   
      30969  2012       London         Volleyball  Beach Volleyball   
      
                         Athlete Country Gender                             Event  \
      5870         DALINS, Janis     LAT    Men                         50KM Walk   
      6489    BUBENKO, Adalberts     LAT    Men                         50KM Walk   
      7203       BIETAGS, Edwins     LAT    Men     79 - 87KG (Light-Heavyweight)   
      20233    KLEMENTYEV, Ivans     LAT    Men          C-1 1000M (Canoe Single)   
      20315        OZOLS, Dainis     LAT    Men              Individual Road Race   
      21071   KUZMINS, Afanasijs     LAT    Men  25M Rapid Fire Pistol (60 Shots)   
      21974    KLEMENTYEV, Ivans     LAT    Men          C-1 1000M (Canoe Single)   
      23630     FADEJEVS, Aigars     LAT    Men                         50KM Walk   
      24296       VIHROVS, Igors     LAT    Men                   Floor Exercises   
      24614  ZELONIJS, Vsevolods     LAT    Men           66 - 73KG (Lightweight)   
      25681  VASILEVSKIS, Vadims     LAT    Men                     Javelin Throw   
      26358   SAPRONENKO, Evgeni     LAT    Men                             Vault   
      26633     RUBLEVSKA, Elena     LAT  Women            Individual Competition   
      27080  SCERBATIHS, Viktors     LAT    Men                           + 105KG   
      27688       KOVALS, Ainars     LAT    Men                     Javelin Throw   
      28019    STROMBERGS, Maris     LAT    Men                        Individual   
      29103  SCERBATIHS, Viktors     LAT    Men                           + 105KG   
      30001    STROMBERGS, Maris     LAT    Men                        Individual   
      30968     PLAVINS, Martins     LAT    Men                  Beach Volleyball   
      30969       SMEDINS, Janis     LAT    Men                  Beach Volleyball   
      
              Medal  
      5870   Silver  
      6489   Bronze  
      7203   Silver  
      20233  Silver  
      20315  Bronze  
      21071  Silver  
      21974  Silver  
      23630  Silver  
      24296    Gold  
      24614  Bronze  
      25681  Silver  
      26358  Silver  
      26633  Silver  
      27080  Silver  
      27688  Silver  
      28019    Gold  
      29103  Bronze  
      30001    Gold  
      30968  Bronze  
      30969  Bronze  ),
     ('LIB',
             Year      City          Sport       Discipline  \
      8891   1952  Helsinki      Wrestling  Wrestling Gre-R   
      8898   1952  Helsinki      Wrestling  Wrestling Gre-R   
      13830  1972    Munich  Weightlifting    Weightlifting   
      16565  1980    Moscow      Wrestling  Wrestling Gre-R   
      
                              Athlete Country Gender  \
      8891            CHIHAB, Zakaria     LIB    Men   
      8898               TAHA, Khalil     LIB    Men   
      13830  TARABULSI, Kheir Mohamed     LIB    Men   
      16565            BCHARA, Hassan     LIB    Men   
      
                                         Event   Medal  
      8891            52 - 57KG (Bantamweight)  Silver  
      8898            67 - 73KG (Welterweight)  Bronze  
      13830  67.5 - 75KG, Total (Middleweight)  Silver  
      16565        + 100KG (Super Heavyweight)  Bronze  ),
     ('LTU',
             Year       City              Sport           Discipline  \
      19978  1992  Barcelona          Athletics            Athletics   
      20111  1992  Barcelona         Basketball           Basketball   
      20112  1992  Barcelona         Basketball           Basketball   
      20113  1992  Barcelona         Basketball           Basketball   
      20114  1992  Barcelona         Basketball           Basketball   
      20115  1992  Barcelona         Basketball           Basketball   
      20116  1992  Barcelona         Basketball           Basketball   
      20117  1992  Barcelona         Basketball           Basketball   
      20118  1992  Barcelona         Basketball           Basketball   
      20119  1992  Barcelona         Basketball           Basketball   
      20120  1992  Barcelona         Basketball           Basketball   
      20121  1992  Barcelona         Basketball           Basketball   
      20122  1992  Barcelona         Basketball           Basketball   
      21852  1996    Atlanta         Basketball           Basketball   
      21853  1996    Atlanta         Basketball           Basketball   
      21854  1996    Atlanta         Basketball           Basketball   
      21855  1996    Atlanta         Basketball           Basketball   
      21856  1996    Atlanta         Basketball           Basketball   
      21857  1996    Atlanta         Basketball           Basketball   
      21858  1996    Atlanta         Basketball           Basketball   
      21859  1996    Atlanta         Basketball           Basketball   
      21860  1996    Atlanta         Basketball           Basketball   
      21861  1996    Atlanta         Basketball           Basketball   
      21862  1996    Atlanta         Basketball           Basketball   
      21863  1996    Atlanta         Basketball           Basketball   
      23641  2000     Sydney          Athletics            Athletics   
      23794  2000     Sydney         Basketball           Basketball   
      23795  2000     Sydney         Basketball           Basketball   
      23796  2000     Sydney         Basketball           Basketball   
      23797  2000     Sydney         Basketball           Basketball   
      23798  2000     Sydney         Basketball           Basketball   
      23799  2000     Sydney         Basketball           Basketball   
      23800  2000     Sydney         Basketball           Basketball   
      23801  2000     Sydney         Basketball           Basketball   
      23802  2000     Sydney         Basketball           Basketball   
      23803  2000     Sydney         Basketball           Basketball   
      23804  2000     Sydney         Basketball           Basketball   
      23805  2000     Sydney         Basketball           Basketball   
      24001  2000     Sydney            Cycling         Cycling Road   
      24651  2000     Sydney             Rowing               Rowing   
      24652  2000     Sydney             Rowing               Rowing   
      24886  2000     Sydney           Shooting             Shooting   
      25659  2004     Athens          Athletics            Athletics   
      25672  2004     Athens          Athletics            Athletics   
      26630  2004     Athens  Modern Pentathlon      Modern Pentath.   
      27665  2008    Beijing          Athletics            Athletics   
      28642  2008    Beijing  Modern Pentathlon      Modern Pentath.   
      28644  2008    Beijing  Modern Pentathlon      Modern Pentath.   
      28818  2008    Beijing            Sailing              Sailing   
      29212  2008    Beijing          Wrestling      Wrestling Gre-R   
      29267  2012     London           Aquatics             Swimming   
      29890  2012     London             Boxing               Boxing   
      29939  2012     London              Canoe         Canoe Sprint   
      30638  2012     London  Modern Pentathlon    Modern Pentathlon   
      31156  2012     London          Wrestling  Wrestling Freestyle   
      
                             Athlete Country Gender  \
      19978           UBARTAS, Romas     LTU    Men   
      20111     BRAZDAUSKIS, Romanas     LTU    Men   
      20112    CHOMICIUS, Valdemaras     LTU    Men   
      20113       DIMAVICIUS, Darius     LTU    Men   
      20114        EINIKIS, Gintaras     LTU    Men   
      20115        JOVAISA, Sergejus     LTU    Men   
      20116      KARNISOVAS, Arturas     LTU    Men   
      20117       KRAPIKAS, Gintaras     LTU    Men   
      20118       KURTINAITIS, Rimas     LTU    Men   
      20119    MARCIULIONIS, Sarunas     LTU    Men   
      20120      PAZDRAZDIS, Alvydas     LTU    Men   
      20121         SABONIS, Arvydas     LTU    Men   
      20122         VISOCKAS, Arunas     LTU    Men   
      21852        EINIKIS, Gintaras     LTU    Men   
      21853        JURKUNAS, Andrius     LTU    Men   
      21854      KARNISOVAS, Arturas     LTU    Men   
      21855       KURTINAITIS, Rimas     LTU    Men   
      21856         LUKMINAS, Darius     LTU    Men   
      21857    MARCIULIONIS, Sarunas     LTU    Men   
      21858           PACESAS, Tomas     LTU    Men   
      21859         SABONIS, Arvydas     LTU    Men   
      21860      STOMBERGAS, Saulius     LTU    Men   
      21861          VAISVILA, Rytis     LTU    Men   
      21862     ZUKAUSKAS, Eurelijus     LTU    Men   
      21863     ZUKAUSKAS, Mindaugas     LTU    Men   
      23641       ALEKNA, Virgilijus     LTU    Men   
      23794       ADOMAITIS, Dainius     LTU    Men   
      23795        EINIKIS, Gintaras     LTU    Men   
      23796      GIEDRAITIS, Audrius     LTU    Men   
      23797    JASIKEVICIUS, Sarunas     LTU    Men   
      23798   MARCIULIONIS, Kestutis     LTU    Men   
      23799          MASIULIS, Tomas     LTU    Men   
      23800      MASKOLIUNAS, Darius     LTU    Men   
      23801      SISKAUSKAS, Ramunas     LTU    Men   
      23802         SONGAILA, Darius     LTU    Men   
      23803      STOMBERGAS, Saulius     LTU    Men   
      23804     TIMINSKAS, Mindaugas     LTU    Men   
      23805     ZUKAUSKAS, Eurelijus     LTU    Men   
      24001           ZILIUTE, Diana     LTU  Women   
      24651    POPLAVSKAJA, Kristina     LTU  Women   
      24652       SAKICKIENE, Birute     LTU  Women   
      24886    GUDZINEVICIUTE, Daina     LTU  Women   
      25659       ALEKNA, Virgilijus     LTU    Men   
      25672          SKUJYTE, Austra     LTU  Women   
      26630  ZADNEPROVSKIS, Andrejus     LTU    Men   
      27665       ALEKNA, Virgilijus     LTU    Men   
      28642  ZADNEPROVSKIS, Andrejus     LTU    Men   
      28644      KRUNGOLCAS, Edvinas     LTU    Men   
      28818  VOLUNGEVICIUTE, Gintare     LTU  Women   
      29212     MIZGAITIS, Mindaugas     LTU    Men   
      29267          MEILUTYTE, Ruta     LTU  Women   
      29890      PETRAUSKAS, Evaldas     LTU    Men   
      29939        SHUKLIN, Jevgenij     LTU    Men   
      30638      ASADAUSKAITE, Laura     LTU  Women   
      31156     KAZAKEVIC, Aleksandr     LTU    Men   
      
                                        Event   Medal  
      19978                      Discus Throw    Gold  
      20111                        Basketball  Bronze  
      20112                        Basketball  Bronze  
      20113                        Basketball  Bronze  
      20114                        Basketball  Bronze  
      20115                        Basketball  Bronze  
      20116                        Basketball  Bronze  
      20117                        Basketball  Bronze  
      20118                        Basketball  Bronze  
      20119                        Basketball  Bronze  
      20120                        Basketball  Bronze  
      20121                        Basketball  Bronze  
      20122                        Basketball  Bronze  
      21852                        Basketball  Bronze  
      21853                        Basketball  Bronze  
      21854                        Basketball  Bronze  
      21855                        Basketball  Bronze  
      21856                        Basketball  Bronze  
      21857                        Basketball  Bronze  
      21858                        Basketball  Bronze  
      21859                        Basketball  Bronze  
      21860                        Basketball  Bronze  
      21861                        Basketball  Bronze  
      21862                        Basketball  Bronze  
      21863                        Basketball  Bronze  
      23641                      Discus Throw    Gold  
      23794                        Basketball  Bronze  
      23795                        Basketball  Bronze  
      23796                        Basketball  Bronze  
      23797                        Basketball  Bronze  
      23798                        Basketball  Bronze  
      23799                        Basketball  Bronze  
      23800                        Basketball  Bronze  
      23801                        Basketball  Bronze  
      23802                        Basketball  Bronze  
      23803                        Basketball  Bronze  
      23804                        Basketball  Bronze  
      23805                        Basketball  Bronze  
      24001              Individual Road Race  Bronze  
      24651                Double Sculls (2X)  Bronze  
      24652                Double Sculls (2X)  Bronze  
      24886                 Trap (75 Targets)    Gold  
      25659                      Discus Throw    Gold  
      25672                        Heptathlon  Silver  
      26630            Individual Competition  Silver  
      27665                      Discus Throw  Bronze  
      28642            Individual Competition  Bronze  
      28644            Individual Competition  Silver  
      28818  Laser Radial - One Person Dinghy  Silver  
      29212                        96 - 120KG  Bronze  
      29267                 100M Breaststroke    Gold  
      29890                         57 - 60KG  Bronze  
      29939                          C-1 200M  Silver  
      30638                        Individual    Gold  
      31156                          Wg 74 KG  Bronze  ),
     ('LUX',
            Year      City          Sport     Discipline          Athlete Country  \
      4079  1920   Antwerp  Weightlifting  Weightlifting    ALZIN, Joseph     LUX   
      8130  1952  Helsinki      Athletics      Athletics  BARTHEL, Joseph     LUX   
      
           Gender                                          Event   Medal  
      4079    Men  + 82.5KG, One-Two Hand 3 Events (Heavyweight)  Silver  
      8130    Men                                          1500M    Gold  ),
     ('MAR',
             Year         City      Sport Discipline  \
      10036  1960         Rome  Athletics  Athletics   
      16837  1984  Los Angeles  Athletics  Athletics   
      16888  1984  Los Angeles  Athletics  Athletics   
      18278  1988        Seoul  Athletics  Athletics   
      18382  1988        Seoul  Athletics  Athletics   
      18528  1988        Seoul     Boxing     Boxing   
      19850  1992    Barcelona  Athletics  Athletics   
      19872  1992    Barcelona  Athletics  Athletics   
      20195  1992    Barcelona     Boxing     Boxing   
      21588  1996      Atlanta  Athletics  Athletics   
      21699  1996      Atlanta  Athletics  Athletics   
      23534  2000       Sydney  Athletics  Athletics   
      23550  2000       Sydney  Athletics  Athletics   
      23562  2000       Sydney  Athletics  Athletics   
      23622  2000       Sydney  Athletics  Athletics   
      23883  2000       Sydney     Boxing     Boxing   
      25551  2004       Athens  Athletics  Athletics   
      25641  2004       Athens  Athletics  Athletics   
      25654  2004       Athens  Athletics  Athletics   
      27659  2008      Beijing  Athletics  Athletics   
      27700  2008      Beijing  Athletics  Athletics   
      29602  2012       London  Athletics  Athletics   
      
                                    Athlete Country Gender  \
      10036  RHADI BEN ABDESSELEM, Abdesiem     MAR    Men   
      16837            EL MOUTAWAKEL, Nawal     MAR  Women   
      16888                    AOUITA, Said     MAR    Men   
      18278         BOUTAYEB, Moulay Brahim     MAR    Men   
      18382                    AOUITA, Said     MAR    Men   
      18528                 ACHIK, Abdelhak     MAR    Men   
      19850                    SKAH, Khalid     MAR    Men   
      19872                EL BASIR, Rachid     MAR    Men   
      20195                  ACHIK, Mohamed     MAR    Men   
      21588                   HISSOU, Salah     MAR    Men   
      21699                 BOULAMI, Khalid     MAR    Men   
      23534             EL GUERROUJ, Hicham     MAR    Men   
      23550                     EZZINE, Ali     MAR    Men   
      23562                BIDOUANE, Nouzha     MAR  Women   
      23622                 LAHLAFI, Brahim     MAR    Men   
      23883                TAMSAMANI, Tahar     MAR    Men   
      25551             EL GUERROUJ, Hicham     MAR    Men   
      25641             EL GUERROUJ, Hicham     MAR    Men   
      25654                 BENHASSI, Hasna     MAR  Women   
      27659                 BENHASSI, Hasna     MAR  Women   
      27700                  GHARIB, Jaouad     MAR    Men   
      29602              IGUIDER, Abdalaati     MAR    Men   
      
                                 Event   Medal  
      10036                   Marathon  Silver  
      16837               400M Hurdles    Gold  
      16888                      5000M    Gold  
      18278                     10000M    Gold  
      18382                       800M  Bronze  
      18528  54 - 57KG (Featherweight)  Bronze  
      19850                     10000M    Gold  
      19872                      1500M  Silver  
      20195   51 - 54KG (Bantamweight)  Bronze  
      21588                     10000M  Bronze  
      21699                      5000M  Bronze  
      23534                      1500M  Silver  
      23550         3000M Steeplechase  Bronze  
      23562               400M Hurdles  Bronze  
      23622                      5000M  Bronze  
      23883  54 - 57KG (Featherweight)  Bronze  
      25551                      1500M    Gold  
      25641                      5000M    Gold  
      25654                       800M  Silver  
      27659                       800M  Bronze  
      27700                   Marathon  Silver  
      29602                      1500M  Bronze  ),
     ('MAS',
             Year       City      Sport Discipline                 Athlete Country  \
      20028  1992  Barcelona  Badminton  Badminton           SIDEK, Rashid     MAS   
      20029  1992  Barcelona  Badminton  Badminton            SIDEK, Razif     MAS   
      21774  1996    Atlanta  Badminton  Badminton         CHEAH, Soon Kit     MAS   
      21775  1996    Atlanta  Badminton  Badminton           YAP, Kim Hock     MAS   
      21786  1996    Atlanta  Badminton  Badminton           SIDEK, Rashid     MAS   
      27742  2008    Beijing  Badminton  Badminton          LEE, Chong Wei     MAS   
      29221  2012     London   Aquatics     Diving  PAMG, Pandelela Rinong     MAS   
      29791  2012     London  Badminton  Badminton          LEE, Chong Wei     MAS   
      
            Gender         Event   Medal  
      20028    Men       Doubles  Bronze  
      20029    Men       Doubles  Bronze  
      21774    Men       Doubles  Silver  
      21775    Men       Doubles  Silver  
      21786    Men       Singles  Bronze  
      27742    Men       Singles  Silver  
      29221  Women  10M Platform  Bronze  
      29791    Men       Singles  Silver  ),
     ('MDA',
             Year     City          Sport       Discipline             Athlete  \
      21988  1996  Atlanta  Canoe / Kayak  Canoe / Kayak F  JURAVSCHI, Nikolai   
      21989  1996  Atlanta  Canoe / Kayak  Canoe / Kayak F   RENEYSKIY, Viktor   
      23134  1996  Atlanta      Wrestling  Wrestling Gre-R   MOUREIKO, Serguei   
      23894  2000   Sydney         Boxing           Boxing     GRUSAC, Vitalie   
      24851  2000   Sydney       Shooting         Shooting      MOLDOVAN, Oleg   
      27902  2008  Beijing         Boxing           Boxing    GOJAN, Veaceslav   
      
            Country Gender                             Event   Medal  
      21988     MDA    Men           C-2 500M (Canoe Double)  Silver  
      21989     MDA    Men           C-2 500M (Canoe Double)  Silver  
      23134     MDA    Men   100 - 130KG (Super Heavyweight)  Bronze  
      23894     MDA    Men        63.5 - 67KG (Welterweight)  Bronze  
      24851     MDA    Men  10M Running Target (30+30 Shots)  Silver  
      27902     MDA    Men          51 - 54KG (Bantamweight)  Bronze  ),
     ('MEX',
             Year         City       Sport  Discipline                      Athlete  \
      5918   1932  Los Angeles      Boxing      Boxing           CABANAS, Francisco   
      6271   1932  Los Angeles    Shooting    Shooting      HUET BOBADILLA, Gustavo   
      6537   1936       Berlin  Basketball  Basketball          BORJA MORCA, Carlos   
      6538   1936       Berlin  Basketball  Basketball     BORJA MORCA, Victor Hugo   
      6539   1936       Berlin  Basketball  Basketball  CHOPERENA IRIZARRI, Rodolfo   
      ...     ...          ...         ...         ...                          ...   
      30206  2012       London    Football    Football                 REYES, Diego   
      30207  2012       London    Football    Football              RODRIGUEZ, Jose   
      30208  2012       London    Football    Football              SALCIDO, Carlos   
      30209  2012       London    Football    Football               VIDRIO, Nestor   
      30913  2012       London   Taekwondo   Taekwondo  ESPINOZA, Maria del Rosario   
      
            Country Gender                       Event   Medal  
      5918      MEX    Men        - 50.8KG (Flyweight)  Silver  
      6271      MEX    Men  50M Rifle Prone (60 Shots)  Silver  
      6537      MEX    Men                  Basketball  Bronze  
      6538      MEX    Men                  Basketball  Bronze  
      6539      MEX    Men                  Basketball  Bronze  
      ...       ...    ...                         ...     ...  
      30206     MEX    Men                    Football    Gold  
      30207     MEX    Men                    Football    Gold  
      30208     MEX    Men                    Football    Gold  
      30209     MEX    Men                    Football    Gold  
      30913     MEX  Women                     + 67 KG  Bronze  
      
      [106 rows x 9 columns]),
     ('MGL',
             Year       City      Sport           Discipline  \
      12667  1968     Mexico  Wrestling      Wrestling Free.   
      12679  1968     Mexico  Wrestling      Wrestling Free.   
      12682  1968     Mexico  Wrestling      Wrestling Free.   
      12687  1968     Mexico  Wrestling      Wrestling Free.   
      13869  1972     Munich  Wrestling      Wrestling Free.   
      15159  1976   Montreal  Wrestling      Wrestling Free.   
      16178  1980     Moscow       Judo                 Judo   
      16179  1980     Moscow       Judo                 Judo   
      16541  1980     Moscow  Wrestling      Wrestling Free.   
      16552  1980     Moscow  Wrestling      Wrestling Free.   
      18533  1988      Seoul     Boxing               Boxing   
      20203  1992  Barcelona     Boxing               Boxing   
      21066  1992  Barcelona   Shooting             Shooting   
      22614  1996    Atlanta       Judo                 Judo   
      26577  2004     Athens       Judo                 Judo   
      27901  2008    Beijing     Boxing               Boxing   
      27904  2008    Beijing     Boxing               Boxing   
      28640  2008    Beijing       Judo                 Judo   
      28860  2008    Beijing   Shooting             Shooting   
      29881  2012     London     Boxing               Boxing   
      29895  2012     London     Boxing               Boxing   
      30618  2012     London       Judo                 Judo   
      30632  2012     London       Judo                 Judo   
      31115  2012     London  Wrestling  Wrestling Freestyle   
      
                                Athlete Country Gender  \
      12667        SURENJAV, Sukhbaatar     MGL    Men   
      12679      DANZANDARJAA, Sereeter     MGL    Men   
      12682           PUREV, Dagvasuren     MGL    Men   
      12687           JIGJIDYM, Munkbat     MGL    Men   
      13869          BAYANMUNK, Khorloo     MGL    Men   
      15159            OIDOV, Zevegying     MGL    Men   
      16178           DAMDIN, Tsendying     MGL    Men   
      16179          DAVAADALAI, Ravdan     MGL    Men   
      16541        OUINBOLD, Dugarsuren     MGL    Men   
      16552         DAVAAJAV, Jamtsying     MGL    Men   
      18533             ENKHBAT, Nerguy     MGL    Men   
      20203        BAYARSAIKHAN, Namjil     MGL    Men   
      21066      MUNKHBAYAR, Dorzhsuren     MGL  Women   
      22614       NARMANDAKH, Dorjpalam     MGL    Men   
      26577  TSAGAANBAATAR, Khashbaatar     MGL    Men   
      27901         PUREVDORJ, Serdamba     MGL    Men   
      27904        ENKHBAT, Badar-Uugan     MGL    Men   
      28640        NAIDAN, Tuvshinbayar     MGL    Men   
      28860           OTRYAD, Gundegmaa     MGL  Women   
      29881        NYAMBAYAR, Tugstsogt     MGL    Men   
      29895    URANCHIMEG, Munkh-Erdene     MGL    Men   
      30618      SAINJARGAL, Nyam-Ochir     MGL    Men   
      30632        NAIDAN, Tuvshinbayar     MGL    Men   
      31115    SORONZONBOLD, Battsetseg     MGL  Women   
      
                                     Event   Medal  
      12667             - 52KG (Flyweight)  Bronze  
      12679        63 - 70KG (Lightweight)  Bronze  
      12682       70 - 78KG (Welterweight)  Bronze  
      12687       78 - 87KG (Middleweight)  Silver  
      13869       90 - 100KG (Heavyweight)  Silver  
      15159      57 - 62KG (Featherweight)  Silver  
      16178   60 - 65KG (Half-Lightweight)  Silver  
      16179        65 - 71KG (Lightweight)  Bronze  
      16541       52 - 57KG (Bantamweight)  Bronze  
      16552       68 - 74KG (Welterweight)  Silver  
      18533        57 - 60KG (Lightweight)  Bronze  
      20203        57 - 60KG (Lightweight)  Bronze  
      21066       25M Pistol (30+30 Shots)  Bronze  
      22614                        - 60 KG  Bronze  
      26577                        - 60 KG  Bronze  
      27901         48KG (Light Flywieght)  Silver  
      27904       51 - 54KG (Bantamweight)    Gold  
      28640  90 - 100KG (Half-Heavyweight)    Gold  
      28860       25M Pistol (30+30 Shots)  Silver  
      29881                           52KG  Silver  
      29895                     60 - 64 KG  Bronze  
      30618                      66 - 73KG  Bronze  
      30632                     90 - 100KG  Silver  
      31115                       Wf 63 KG  Bronze  ),
     ('MKD',
             Year    City      Sport       Discipline             Athlete Country  \
      25143  2000  Sydney  Wrestling  Wrestling Free.  IBRAGIMOV, Mogamed     MKD   
      
            Gender      Event   Medal  
      25143    Men  76 - 85KG  Bronze  ),
     ('MNE',
             Year    City     Sport Discipline               Athlete Country Gender  \
      30454  2012  London  Handball   Handball  BARJAKTAROVIC, Sonja     MNE  Women   
      30455  2012  London  Handball   Handball     BULATOVIC, Andela     MNE  Women   
      30456  2012  London  Handball   Handball   BULATOVIC, Katarina     MNE  Women   
      30457  2012  London  Handball   Handball            DOKIC, Ana     MNE  Women   
      30458  2012  London  Handball   Handball     JOVANOVIC, Marija     MNE  Women   
      30459  2012  London  Handball   Handball      KNEZEVIC, Milena     MNE  Women   
      30460  2012  London  Handball   Handball       LAZOVIC, Suzana     MNE  Women   
      30461  2012  London  Handball   Handball     MEHMEDOVIC, Majda     MNE  Women   
      30462  2012  London  Handball   Handball     MILJANIC, Radmila     MNE  Women   
      30463  2012  London  Handball   Handball       POPOVIC, Bojana     MNE  Women   
      30464  2012  London  Handball   Handball    RADICEVIC, Jovanka     MNE  Women   
      30465  2012  London  Handball   Handball          RADOVIC, Ana     MNE  Women   
      30466  2012  London  Handball   Handball           SAVIC, Maja     MNE  Women   
      30467  2012  London  Handball   Handball      VUKCEVIC, Marina     MNE  Women   
      
                Event   Medal  
      30454  Handball  Silver  
      30455  Handball  Silver  
      30456  Handball  Silver  
      30457  Handball  Silver  
      30458  Handball  Silver  
      30459  Handball  Silver  
      30460  Handball  Silver  
      30461  Handball  Silver  
      30462  Handball  Silver  
      30463  Handball  Silver  
      30464  Handball  Silver  
      30465  Handball  Silver  
      30466  Handball  Silver  
      30467  Handball  Silver  ),
     ('MOZ',
             Year     City      Sport Discipline        Athlete Country Gender  \
      21711  1996  Atlanta  Athletics  Athletics  MUTOLA, Maria     MOZ  Women   
      23635  2000   Sydney  Athletics  Athletics  MUTOLA, Maria     MOZ  Women   
      
            Event   Medal  
      21711  800M  Bronze  
      23635  800M    Gold  ),
     ('MRI',
             Year     City   Sport Discipline       Athlete Country Gender  \
      27903  2008  Beijing  Boxing     Boxing  JULIE, Bruno     MRI    Men   
      
                                Event   Medal  
      27903  51 - 54KG (Bantamweight)  Bronze  ),
     ('NAM',
             Year       City      Sport Discipline            Athlete Country  \
      19860  1992  Barcelona  Athletics  Athletics  FREDERICKS, Frank     NAM   
      19878  1992  Barcelona  Athletics  Athletics  FREDERICKS, Frank     NAM   
      21599  1996    Atlanta  Athletics  Athletics  FREDERICKS, Frank     NAM   
      21617  1996    Atlanta  Athletics  Athletics  FREDERICKS, Frank     NAM   
      
            Gender Event   Medal  
      19860    Men  100M  Silver  
      19878    Men  200M  Silver  
      21599    Men  100M  Silver  
      21617    Men  200M  Silver  ),
     ('NED',
             Year    City     Sport Discipline                       Athlete  \
      154    1900   Paris  Aquatics   Swimming               DROST, Johannes   
      434    1900   Paris    Rowing     Rowing      BRANDT, Francois Antoine   
      435    1900   Paris    Rowing     Rowing  BROCKMANN, Hermanus Gerardus   
      436    1900   Paris    Rowing     Rowing                 KLEIN, Roelof   
      437    1900   Paris    Rowing     Rowing        LEEGSTRA, Ruud Gerbens   
      ...     ...     ...       ...        ...                           ...   
      30730  2012  London    Rowing     Rowing           VEENHOVEN, Jacobine   
      30795  2012  London   Sailing    Sailing               BERKHOUT, Lobke   
      30796  2012  London   Sailing    Sailing               WESTERHOF, Lisa   
      30819  2012  London   Sailing    Sailing            BOUWMEESTER, Marit   
      30821  2012  London   Sailing    Sailing      VAN RIJSSELBERGE, Dorian   
      
            Country Gender                     Event   Medal  
      154       NED    Men           200M Backstroke  Bronze  
      434       NED    Men  Eight With Coxswain (8+)  Bronze  
      435       NED    Men  Eight With Coxswain (8+)  Bronze  
      436       NED    Men  Eight With Coxswain (8+)  Bronze  
      437       NED    Men  Eight With Coxswain (8+)  Bronze  
      ...       ...    ...                       ...     ...  
      30730     NED  Women       Eight With Coxswain  Bronze  
      30795     NED  Women                       470  Bronze  
      30796     NED  Women                       470  Bronze  
      30819     NED  Women              Laser Radial  Silver  
      30821     NED    Men                      Rs:X    Gold  
      
      [851 rows x 9 columns]),
     ('NGR',
             Year         City      Sport Discipline                      Athlete  \
      11019  1964        Tokyo     Boxing     Boxing              MAIYEGUN, Nojim   
      13125  1972       Munich     Boxing     Boxing              IKHOURIA, Isaac   
      16863  1984  Los Angeles  Athletics  Athletics           EGBUNIKE, Innocent   
      16864  1984  Los Angeles  Athletics  Athletics               PETERS, Rotimi   
      16865  1984  Los Angeles  Athletics  Athletics              UGBUSIEN, Moses   
      ...     ...          ...        ...        ...                          ...   
      28246  2008      Beijing   Football   Football            OKONKWO, Chibuzor   
      28247  2008      Beijing   Football   Football           OKORONKWO, Solomon   
      28248  2008      Beijing   Football   Football             OLUFEMI, Oladapo   
      28249  2008      Beijing   Football   Football            VANZEKIN, Ambruse   
      28973  2008      Beijing  Taekwondo  Taekwondo  CHUKWUMERIJE, Chika Yagazie   
      
            Country Gender                           Event   Medal  
      11019     NGR    Men  67 - 71KG (Light-Middleweight)  Bronze  
      13125     NGR    Men   75 - 81KG (Light-Heavyweight)  Bronze  
      16863     NGR    Men                    4X400M Relay  Bronze  
      16864     NGR    Men                    4X400M Relay  Bronze  
      16865     NGR    Men                    4X400M Relay  Bronze  
      ...       ...    ...                             ...     ...  
      28246     NGR    Men                        Football  Silver  
      28247     NGR    Men                        Football  Silver  
      28248     NGR    Men                        Football  Silver  
      28249     NGR    Men                        Football  Silver  
      28973     NGR    Men                         + 80 KG  Bronze  
      
      [84 rows x 9 columns]),
     ('NIG',
             Year    City   Sport Discipline         Athlete Country Gender  \
      13108  1972  Munich  Boxing     Boxing  DABORG, Issaka     NIG    Men   
      
                                        Event   Medal  
      13108  60 - 63.5KG (Light-Welterweight)  Bronze  ),
     ('NOR',
             Year    City      Sport Discipline                    Athlete Country  \
      294    1900   Paris  Athletics  Athletics      ANDERSEN, Carl Albert     NOR   
      596    1900   Paris   Shooting   Shooting                 ÖSTMO, Ole     NOR   
      603    1900   Paris   Shooting   Shooting                 ÖSTMO, Ole     NOR   
      608    1900   Paris   Shooting   Shooting                 ÖSTMO, Ole     NOR   
      619    1900   Paris   Shooting   Shooting      FRYDENLUND, Olaf Emil     NOR   
      ...     ...     ...        ...        ...                        ...     ...   
      30449  2012  London   Handball   Handball  LUNDE-BORGERSEN, Kristine     NOR   
      30450  2012  London   Handball   Handball            NOSTVOLD, Tonje     NOR   
      30451  2012  London   Handball   Handball   RIEGELHUTH, Linn-Kristin     NOR   
      30452  2012  London   Handball   Handball        SNORROEGGEN, Goeril     NOR   
      30453  2012  London   Handball   Handball        SULLAND, Linn Jorum     NOR   
      
            Gender                          Event   Medal  
      294      Men                     Pole Vault  Bronze  
      596      Men  Army Rifle, 300M, 3 Positions  Bronze  
      603      Men        Army Rifle, 300M, Prone  Bronze  
      608      Men     Army Rifle, 300M, Standing  Silver  
      619      Men               Free Rifle, Team  Silver  
      ...      ...                            ...     ...  
      30449  Women                       Handball    Gold  
      30450  Women                       Handball    Gold  
      30451  Women                       Handball    Gold  
      30452  Women                       Handball    Gold  
      30453  Women                       Handball    Gold  
      
      [554 rows x 9 columns]),
     ('NZL',
             Year         City      Sport Discipline                       Athlete  \
      3678   1920      Antwerp     Rowing     Rowing  HADFIELD D'ARCY, D. Clarence   
      4235   1924        Paris  Athletics  Athletics               PORRITT, Arthur   
      5215   1928    Amsterdam     Boxing     Boxing                MORGAN, Edward   
      6151   1932  Los Angeles     Rowing     Rowing            STILES, Cyril Alec   
      6152   1932  Los Angeles     Rowing     Rowing       THOMPSON, Fred Houghton   
      ...     ...          ...        ...        ...                           ...   
      30779  2012       London     Rowing     Rowing                DRYSDALE, Mahe   
      30791  2012       London    Sailing    Sailing                      ALEH, Jo   
      30792  2012       London    Sailing    Sailing                POWRIE, Olivia   
      30799  2012       London    Sailing    Sailing                BURLING, Peter   
      30800  2012       London    Sailing    Sailing                   TUKE, Blair   
      
            Country Gender                           Event   Medal  
      3678      NZL    Men              Single Sculls (1X)  Bronze  
      4235      NZL    Men                            100M  Bronze  
      5215      NZL    Men  61.24 - 66.68KG (Welterweight)    Gold  
      6151      NZL    Men               Coxless Pair (2-)  Silver  
      6152      NZL    Men               Coxless Pair (2-)  Silver  
      ...       ...    ...                             ...     ...  
      30779     NZL    Men                   Single Sculls    Gold  
      30791     NZL  Women                             470    Gold  
      30792     NZL  Women                             470    Gold  
      30799     NZL    Men                    49Er - Skiff  Silver  
      30800     NZL    Men                    49Er - Skiff  Silver  
      
      [190 rows x 9 columns]),
     ('PAK',
             Year                   City   Sport Discipline            Athlete  \
      9564   1956  Melbourne / Stockholm  Hockey     Hockey       ABDUL, Hamid   
      9565   1956  Melbourne / Stockholm  Hockey     Hockey    AHKTAR, Hussain   
      9566   1956  Melbourne / Stockholm  Hockey     Hockey   DAR, Munir Ahmad   
      9567   1956  Melbourne / Stockholm  Hockey     Hockey      GHULAM, Rasul   
      9568   1956  Melbourne / Stockholm  Hockey     Hockey   HABIB, Ur Rehman   
      ...     ...                    ...     ...        ...                ...   
      20694  1992              Barcelona  Hockey     Hockey     SHAHBAZ, Ahmed   
      20695  1992              Barcelona  Hockey     Hockey  SHAHBAZ, Muhammad   
      20696  1992              Barcelona  Hockey     Hockey   SHAHID, Ali Khan   
      20697  1992              Barcelona  Hockey     Hockey       TAHIR, Zaman   
      20698  1992              Barcelona  Hockey     Hockey       WASIM, Feroz   
      
            Country Gender   Event   Medal  
      9564      PAK    Men  Hockey  Silver  
      9565      PAK    Men  Hockey  Silver  
      9566      PAK    Men  Hockey  Silver  
      9567      PAK    Men  Hockey  Silver  
      9568      PAK    Men  Hockey  Silver  
      ...       ...    ...     ...     ...  
      20694     PAK    Men  Hockey  Bronze  
      20695     PAK    Men  Hockey  Bronze  
      20696     PAK    Men  Hockey  Bronze  
      20697     PAK    Men  Hockey  Bronze  
      20698     PAK    Men  Hockey  Bronze  
      
      [121 rows x 9 columns]),
     ('PAN',
             Year     City      Sport Discipline                        Athlete  \
      7301   1948   London  Athletics  Athletics                 LABEACH, Lloyd   
      7313   1948   London  Athletics  Athletics                 LABEACH, Lloyd   
      27693  2008  Beijing  Athletics  Athletics  SALADINO ARANDA, Irving Jahir   
      
            Country Gender      Event   Medal  
      7301      PAN    Men       100M  Bronze  
      7313      PAN    Men       200M  Bronze  
      27693     PAN    Men  Long Jump    Gold  ),
     ('PAR',
             Year    City     Sport Discipline              Athlete Country Gender  \
      26223  2004  Athens  Football   Football       BAREIRO, Fredy     PAR    Men   
      26224  2004  Athens  Football   Football       BARRETO, Diego     PAR    Men   
      26225  2004  Athens  Football   Football       BARRETO, Edgar     PAR    Men   
      26226  2004  Athens  Football   Football       BENITEZ, Pedro     PAR    Men   
      26227  2004  Athens  Football   Football        CARDOZO, Jose     PAR    Men   
      26228  2004  Athens  Football   Football   CRISTALDO, Ernesto     PAR    Men   
      26229  2004  Athens  Football   Football         DEVACA, Jose     PAR    Men   
      26230  2004  Athens  Football   Football        DIAZ, Osvaldo     PAR    Men   
      26231  2004  Athens  Football   Football  ENCISO, Julio Cesar     PAR    Men   
      26232  2004  Athens  Football   Football      ESQUIVEL, Celso     PAR    Men   
      26233  2004  Athens  Football   Football     FIGUEREDO, Diego     PAR    Men   
      26234  2004  Athens  Football   Football      GAMARRA, Carlos     PAR    Men   
      26235  2004  Athens  Football   Football       GIMENEZ, Pablo     PAR    Men   
      26236  2004  Athens  Football   Football      GONZALEZ, Julio     PAR    Men   
      26237  2004  Athens  Football   Football        MANZUR, Julio     PAR    Men   
      26238  2004  Athens  Football   Football     MARTINEZ, Emilio     PAR    Men   
      26239  2004  Athens  Football   Football    TORRES, Aureliano     PAR    Men   
      
                Event   Medal  
      26223  Football  Silver  
      26224  Football  Silver  
      26225  Football  Silver  
      26226  Football  Silver  
      26227  Football  Silver  
      26228  Football  Silver  
      26229  Football  Silver  
      26230  Football  Silver  
      26231  Football  Silver  
      26232  Football  Silver  
      26233  Football  Silver  
      26234  Football  Silver  
      26235  Football  Silver  
      26236  Football  Silver  
      26237  Football  Silver  
      26238  Football  Silver  
      26239  Football  Silver  ),
     ('PER',
             Year         City       Sport  Discipline                     Athlete  \
      7947   1948       London    Shooting    Shooting          VASQUEZ CAM, Edwin   
      17888  1984  Los Angeles    Shooting    Shooting             BOZA, Francisco   
      19495  1988        Seoul  Volleyball  Volleyball              CERVERA, Luisa   
      19496  1988        Seoul  Volleyball  Volleyball     DE LA GUERRA, Alejandra   
      19497  1988        Seoul  Volleyball  Volleyball            FAJARDO, Denisse   
      19498  1988        Seoul  Volleyball  Volleyball            GALLARDO, Miriam   
      19499  1988        Seoul  Volleyball  Volleyball                GARCIA, Rosa   
      19500  1988        Seoul  Volleyball  Volleyball             HEREDIA, Isabel   
      19501  1988        Seoul  Volleyball  Volleyball            HORNY, Katherine   
      19502  1988        Seoul  Volleyball  Volleyball             MALAGA, Natalia   
      19503  1988        Seoul  Volleyball  Volleyball   PEREZ DEL SOLAR, Gabriela   
      19504  1988        Seoul  Volleyball  Volleyball               TAIT, Cecilia   
      19505  1988        Seoul  Volleyball  Volleyball             TORREALVA, Gina   
      19506  1988        Seoul  Volleyball  Volleyball              URIBE, Cenaida   
      21088  1992    Barcelona    Shooting    Shooting  GIHA, Juan Jorge Yarve Jr.   
      
            Country Gender                  Event   Medal  
      7947      PER    Men  50M Pistol (60 Shots)    Gold  
      17888     PER    Men     Trap (125 Targets)  Silver  
      19495     PER  Women             Volleyball  Silver  
      19496     PER  Women             Volleyball  Silver  
      19497     PER  Women             Volleyball  Silver  
      19498     PER  Women             Volleyball  Silver  
      19499     PER  Women             Volleyball  Silver  
      19500     PER  Women             Volleyball  Silver  
      19501     PER  Women             Volleyball  Silver  
      19502     PER  Women             Volleyball  Silver  
      19503     PER  Women             Volleyball  Silver  
      19504     PER  Women             Volleyball  Silver  
      19505     PER  Women             Volleyball  Silver  
      19506     PER  Women             Volleyball  Silver  
      21088     PER    Men    Skeet (125 Targets)  Silver  ),
     ('PHI',
             Year         City      Sport Discipline                 Athlete  \
      5031   1928    Amsterdam   Aquatics   Swimming      YLDEFONSO, Teofilo   
      5741   1932  Los Angeles   Aquatics   Swimming      YLDEFONSO, Teofilo   
      5889   1932  Los Angeles  Athletics  Athletics  TORIBIO, Simeon Galvez   
      5922   1932  Los Angeles     Boxing     Boxing        VILLANUEVA, Jose   
      6447   1936       Berlin  Athletics  Athletics        WHITE, Miguel S.   
      11005  1964        Tokyo     Boxing     Boxing  VILLANUEVA, Anthony N.   
      18513  1988        Seoul     Boxing     Boxing      SERANTES, Leopoldo   
      20184  1992    Barcelona     Boxing     Boxing           VELASCO, Roel   
      21927  1996      Atlanta     Boxing     Boxing       VELASCO, Mansueto   
      
            Country Gender                       Event   Medal  
      5031      PHI    Men           200M Breaststroke  Bronze  
      5741      PHI    Men           200M Breaststroke  Bronze  
      5889      PHI    Men                   High Jump  Bronze  
      5922      PHI    Men  50.8 - 54KG (Bantamweight)  Bronze  
      6447      PHI    Men                400M Hurdles  Bronze  
      11005     PHI    Men   54 - 57KG (Featherweight)  Silver  
      18513     PHI    Men    - 48KG (Light-Flyweight)  Bronze  
      20184     PHI    Men    - 48KG (Light-Flyweight)  Bronze  
      21927     PHI    Men    - 48KG (Light-Flyweight)  Silver  ),
     ('POL',
             Year    City          Sport           Discipline  \
      4413   1924   Paris        Cycling        Cycling Track   
      4414   1924   Paris        Cycling        Cycling Track   
      4415   1924   Paris        Cycling        Cycling Track   
      4416   1924   Paris        Cycling        Cycling Track   
      4436   1924   Paris     Equestrian              Jumping   
      ...     ...     ...            ...                  ...   
      30826  2012  London        Sailing              Sailing   
      30843  2012  London       Shooting             Shooting   
      31056  2012  London  Weightlifting        Weightlifting   
      31087  2012  London  Weightlifting        Weightlifting   
      31160  2012  London      Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                 Event   Medal  
      4413               LANGE, Jozef     POL    Men  Team Pursuit (4000M)  Silver  
      4414              LAZARSKI, Jan     POL    Men  Team Pursuit (4000M)  Silver  
      4415        STANKIEWICZ, Tomasz     POL    Men  Team Pursuit (4000M)  Silver  
      4416       SZYMCZYK, Franciszek     POL    Men  Team Pursuit (4000M)  Silver  
      4436         KROLIKIEWICZ, Adam     POL    Men            Individual  Bronze  
      ...                         ...     ...    ...                   ...     ...  
      30826           KLEPACKA, Zofia     POL  Women                  Rs:X  Bronze  
      30843           BOGACKA, Sylwia     POL  Women         10M Air Rifle  Silver  
      31056          BONK, Bartlomiej     POL    Men                 105KG  Bronze  
      31087  ZIELINSKI, Adrian Edward     POL    Men                  85KG    Gold  
      31160        JANIKOWSKI, Damian     POL    Men              Wg 84 KG  Bronze  
      
      [511 rows x 9 columns]),
     ('POR',
             Year         City       Sport    Discipline  \
      4439   1924        Paris  Equestrian       Jumping   
      4440   1924        Paris  Equestrian       Jumping   
      4441   1924        Paris  Equestrian       Jumping   
      6703   1936       Berlin  Equestrian       Jumping   
      6704   1936       Berlin  Equestrian       Jumping   
      6705   1936       Berlin  Equestrian       Jumping   
      7563   1948       London  Equestrian      Dressage   
      7564   1948       London  Equestrian      Dressage   
      7565   1948       London  Equestrian      Dressage   
      7932   1948       London     Sailing       Sailing   
      7933   1948       London     Sailing       Sailing   
      8811   1952     Helsinki     Sailing       Sailing   
      8812   1952     Helsinki     Sailing       Sailing   
      10585  1960         Rome     Sailing       Sailing   
      10586  1960         Rome     Sailing       Sailing   
      14067  1976     Montreal   Athletics     Athletics   
      15045  1976     Montreal    Shooting      Shooting   
      16887  1984  Los Angeles   Athletics     Athletics   
      16933  1984  Los Angeles   Athletics     Athletics   
      16935  1984  Los Angeles   Athletics     Athletics   
      18426  1988        Seoul   Athletics     Athletics   
      21592  1996      Atlanta   Athletics     Athletics   
      22813  1996      Atlanta     Sailing       Sailing   
      22814  1996      Atlanta     Sailing       Sailing   
      23517  2000       Sydney   Athletics     Athletics   
      24622  2000       Sydney        Judo          Judo   
      25540  2004       Athens   Athletics     Athletics   
      25550  2004       Athens   Athletics     Athletics   
      26010  2004       Athens     Cycling  Cycling Road   
      27717  2008      Beijing   Athletics     Athletics   
      29015  2008      Beijing   Triathlon     Triathlon   
      29961  2012       London       Canoe  Canoe Sprint   
      29962  2012       London       Canoe  Canoe Sprint   
      
                                                      Athlete Country Gender  \
      4439                          BORGES D'ALMEIDA, Antonio     POR    Men   
      4440                           DE SOUZA MARTINS, Helder     POR    Men   
      4441                       MOUZINHO D'ALBUQUERQUE, José     POR    Men   
      6703                                      BELTRAO, Jose     POR    Men   
      6704   COUTINHO (MARQUES DO FUNCHAL), Domingos De Sousa     POR    Men   
      6705                                        SILVA, Luiz     POR    Men   
      7563                               PAES, Fernando Silva     POR    Men   
      7564                                        SILVA, Luiz     POR    Men   
      7565                                 VALADAS, Francisco     POR    Men   
      7932                          BELLO, Duarte M.D'Almeida     POR    Men   
      7933                       BELLO, Fernando Pinto Coelho     POR    Men   
      8811                      ANDRADE, Francisco Rebello De     POR    Men   
      8812                   FIUZA, Joaquim Mascarenhas De M.     POR    Men   
      10585                         QUINA, Jose Manuel Gentil     POR    Men   
      10586                               QUINA, Mario Gentil     POR    Men   
      14067                                     LOPES, Carlos     POR    Men   
      15045                         MARQUES, Armando Da Silva     POR    Men   
      16887                                   LEITAO, Antonio     POR    Men   
      16933                                     LOPES, Carlos     POR    Men   
      16935                                        MOTA, Rosa     POR  Women   
      18426                                        MOTA, Rosa     POR  Women   
      21592                                 RIBEIRO, Fernanda     POR  Women   
      22813                                     BARRETO, Nuno     POR    Men   
      22814                                ROCHA, Victor Hugo     POR    Men   
      23517                                 RIBEIRO, Fernanda     POR  Women   
      24622                                     DELGADO, Nuno     POR    Men   
      25540                                 OBIKWELU, Francis     POR    Men   
      25550                                        SILVA, Rui     POR    Men   
      26010                                  PAULINHO, Sergio     POR    Men   
      27717                                     EVORA, Nelson     POR    Men   
      29015                                FERNANDES, Vanessa     POR  Women   
      29961                                 PIMENTA, Fernando     POR    Men   
      29962                                    SILVA, Emanuel     POR    Men   
      
                                       Event   Medal  
      4439                              Team  Bronze  
      4440                              Team  Bronze  
      4441                              Team  Bronze  
      6703                              Team  Bronze  
      6704                              Team  Bronze  
      6705                              Team  Bronze  
      7563                              Team  Bronze  
      7564                              Team  Bronze  
      7565                              Team  Bronze  
      7932              Swallow (Golondrina)  Silver  
      7933              Swallow (Golondrina)  Silver  
      8811   Two-Person Keelboat Open (Star)  Bronze  
      8812   Two-Person Keelboat Open (Star)  Bronze  
      10585  Two-Person Keelboat Open (Star)  Silver  
      10586  Two-Person Keelboat Open (Star)  Silver  
      14067                           10000M  Silver  
      15045               Trap (125 Targets)  Silver  
      16887                            5000M  Bronze  
      16933                         Marathon    Gold  
      16935                         Marathon  Bronze  
      18426                         Marathon    Gold  
      21592                           10000M    Gold  
      22813          470 - Two Person Dinghy  Bronze  
      22814          470 - Two Person Dinghy  Bronze  
      23517                           10000M  Bronze  
      24622    73 - 81KG (Half-Middleweight)  Bronze  
      25540                             100M  Silver  
      25550                            1500M  Bronze  
      26010             Individual Road Race  Silver  
      27717                      Triple Jump    Gold  
      29015                       Individual  Silver  
      29961                        K-2 1000M  Silver  
      29962                        K-2 1000M  Silver  ),
     ('PRK',
             Year       City          Sport           Discipline           Athlete  \
      13087  1972     Munich         Boxing               Boxing        KIM, U Gil   
      13566  1972     Munich           Judo                 Judo      KIM, Yong Ik   
      13731  1972     Munich       Shooting             Shooting        LI, Ho-Jun   
      13778  1972     Munich     Volleyball           Volleyball     CHANG, Ok Rim   
      13779  1972     Munich     Volleyball           Volleyball     CHONG, Ok Jin   
      13780  1972     Munich     Volleyball           Volleyball    HWANG, Hye Suk   
      13781  1972     Munich     Volleyball           Volleyball      KANG, Ok Sun   
      13782  1972     Munich     Volleyball           Volleyball     KIM, Jung Bok   
      13783  1972     Munich     Volleyball           Volleyball    KIM, Myong Suk   
      13784  1972     Munich     Volleyball           Volleyball       KIM, Su Dae   
      13785  1972     Munich     Volleyball           Volleyball        KIM, Un Ja   
      13786  1972     Munich     Volleyball           Volleyball   PAEK, Myong Suk   
      13787  1972     Munich     Volleyball           Volleyball       RI, Chun Ok   
      13788  1972     Munich     Volleyball           Volleyball     RYOM, Chun Ja   
      13846  1972     Munich      Wrestling      Wrestling Free.  KIM, Gwong Hyong   
      14287  1976   Montreal         Boxing               Boxing      LI, Byong Uk   
      14298  1976   Montreal         Boxing               Boxing      GU, Young Jo   
      15592  1980     Moscow         Boxing               Boxing      LI, Byong Uk   
      16502  1980     Moscow  Weightlifting        Weightlifting     HAN, Gyong Si   
      16504  1980     Moscow  Weightlifting        Weightlifting     HO, Bong Chol   
      16534  1980     Moscow      Wrestling      Wrestling Free.     JANG, Se Hong   
      16543  1980     Moscow      Wrestling      Wrestling Free.      LI, Ho Pyong   
      20193  1992  Barcelona         Boxing               Boxing     CHOI, Chol Su   
      20196  1992  Barcelona         Boxing               Boxing     LI, Gwang Sik   
      20545  1992  Barcelona     Gymnastics          Artistic G.       PAE, Gil-Su   
      21103  1992  Barcelona   Table Tennis         Table Tennis       LI, Bun Hui   
      21104  1992  Barcelona   Table Tennis         Table Tennis       YU, Sun Bok   
      21114  1992  Barcelona   Table Tennis         Table Tennis       LI, Bun Hui   
      21231  1992  Barcelona  Weightlifting        Weightlifting    KIM, Myong Nam   
      21243  1992  Barcelona      Wrestling      Wrestling Free.           KIM, Il   
      21249  1992  Barcelona      Wrestling      Wrestling Free.       LI, Hak-Son   
      21251  1992  Barcelona      Wrestling      Wrestling Free.     KIM, Yong Sik   
      22612  1996    Atlanta           Judo                 Judo      KYE, Sun Hui   
      23085  1996    Atlanta  Weightlifting        Weightlifting    KIM, Myong Nam   
      23086  1996    Atlanta  Weightlifting        Weightlifting      JON, Chol Ho   
      23102  1996    Atlanta      Wrestling      Wrestling Free.           KIM, Il   
      23110  1996    Atlanta      Wrestling      Wrestling Free.      RI, Yong Sam   
      23866  2000     Sydney         Boxing               Boxing      KIM, Un Chol   
      24593  2000     Sydney           Judo                 Judo      KYE, Sun Hui   
      25103  2000     Sydney  Weightlifting        Weightlifting      RI, Song Hui   
      25152  2000     Sydney      Wrestling      Wrestling Gre-R   KANG, Yong Gyun   
      25899  2004     Athens         Boxing               Boxing     KIM, Song Guk   
      26595  2004     Athens           Judo                 Judo      KYE, Sun Hui   
      26853  2004     Athens       Shooting             Shooting      KIM, Jong Su   
      26945  2004     Athens   Table Tennis         Table Tennis     KIM, Hyang Mi   
      27095  2004     Athens  Weightlifting        Weightlifting      RI, Song Hui   
      28374  2008    Beijing     Gymnastics          Artistic G.     HONG, Un Jong   
      28605  2008    Beijing           Judo                 Judo        AN, Kum Ae   
      28611  2008    Beijing           Judo                 Judo        WON, Ok Im   
      28615  2008    Beijing           Judo                 Judo     PAK, Chol Min   
      29118  2008    Beijing  Weightlifting        Weightlifting        O, Jong Ae   
      29125  2008    Beijing  Weightlifting        Weightlifting     PAK, Hyon Suk   
      30595  2012     London           Judo                 Judo        AN, Kum Ae   
      31059  2012     London  Weightlifting        Weightlifting   RYANG, Chun Hwa   
      31063  2012     London  Weightlifting        Weightlifting      OM, Yun Chol   
      31069  2012     London  Weightlifting        Weightlifting       KIM, Un Guk   
      31078  2012     London  Weightlifting        Weightlifting     RIM, Jong Sim   
      31103  2012     London      Wrestling  Wrestling Freestyle    YANG, Kyong Il   
      
            Country Gender                              Event   Medal  
      13087     PRK    Men           - 48KG (Light-Flyweight)  Silver  
      13566     PRK    Men               - 63KG (Lightweight)  Bronze  
      13731     PRK    Men         50M Rifle Prone (60 Shots)    Gold  
      13778     PRK  Women                         Volleyball  Bronze  
      13779     PRK  Women                         Volleyball  Bronze  
      13780     PRK  Women                         Volleyball  Bronze  
      13781     PRK  Women                         Volleyball  Bronze  
      13782     PRK  Women                         Volleyball  Bronze  
      13783     PRK  Women                         Volleyball  Bronze  
      13784     PRK  Women                         Volleyball  Bronze  
      13785     PRK  Women                         Volleyball  Bronze  
      13786     PRK  Women                         Volleyball  Bronze  
      13787     PRK  Women                         Volleyball  Bronze  
      13788     PRK  Women                         Volleyball  Bronze  
      13846     PRK    Men              48 - 52KG (Flyweight)  Bronze  
      14287     PRK    Men           - 48KG (Light-Flyweight)  Silver  
      14298     PRK    Men           51 - 54KG (Bantamweight)    Gold  
      15592     PRK    Men           - 48KG (Light-Flyweight)  Bronze  
      16502     PRK    Men          - 52KG, Total (Flyweight)  Bronze  
      16504     PRK    Men          - 52KG, Total (Flyweight)  Silver  
      16534     PRK    Men           - 48KG (Light-Flyweight)  Silver  
      16543     PRK    Men           52 - 57KG (Bantamweight)  Silver  
      20193     PRK    Men              48 - 51KG (Flyweight)    Gold  
      20196     PRK    Men           51 - 54KG (Bantamweight)  Bronze  
      20545     PRK    Men                       Pommel Horse    Gold  
      21103     PRK  Women                            Doubles  Bronze  
      21104     PRK  Women                            Doubles  Bronze  
      21114     PRK  Women                            Singles  Bronze  
      21231     PRK    Men  67.5 - 75KG, Total (Middleweight)  Bronze  
      21243     PRK    Men           - 48KG (Light-Flyweight)    Gold  
      21249     PRK    Men              48 - 52KG (Flyweight)    Gold  
      21251     PRK    Men           52 - 57KG (Bantamweight)  Bronze  
      22612     PRK  Women         - 48KG (Extra-Lightweight)    Gold  
      23085     PRK    Men     64 - 70KG, Total (Lightweight)  Silver  
      23086     PRK    Men    70 - 76KG, Total (Middleweight)  Bronze  
      23102     PRK    Men           - 48KG (Light-Flyweight)    Gold  
      23110     PRK    Men           52 - 57KG (Bantamweight)  Bronze  
      23866     PRK    Men           - 48KG (Light-Flyweight)  Bronze  
      24593     PRK  Women       48 - 52KG (Half-Lightweight)  Bronze  
      25103     PRK  Women                               58KG  Silver  
      25152     PRK    Men                          48 - 54KG  Bronze  
      25899     PRK    Men          54 - 57KG (Featherweight)  Silver  
      26595     PRK  Women            52 - 57KG (Lightweight)  Silver  
      26853     PRK    Men              50M Pistol (60 Shots)  Bronze  
      26945     PRK  Women                            Singles  Silver  
      27095     PRK  Women                               58KG  Silver  
      28374     PRK  Women                              Vault    Gold  
      28605     PRK  Women       48 - 52KG (Half-Lightweight)  Silver  
      28611     PRK  Women      57 - 63KG (Half-Middleweight)  Bronze  
      28615     PRK    Men       60 - 66KG (Half-Lightweight)  Bronze  
      29118     PRK  Women                               58KG  Bronze  
      29125     PRK  Women                               63KG    Gold  
      30595     PRK  Women                          48 - 52KG    Gold  
      31059     PRK  Women                               48KG  Bronze  
      31063     PRK    Men                              -56KG    Gold  
      31069     PRK    Men                               62KG    Gold  
      31078     PRK  Women                               69KG    Gold  
      31103     PRK    Men                           Wf 55 KG  Bronze  ),
     ('PUR',
             Year         City      Sport           Discipline  \
      7467   1948       London     Boxing               Boxing   
      14284  1976     Montreal     Boxing               Boxing   
      17046  1984  Los Angeles     Boxing               Boxing   
      17059  1984  Los Angeles     Boxing               Boxing   
      20211  1992    Barcelona     Boxing               Boxing   
      21952  1996      Atlanta     Boxing               Boxing   
      29632  2012       London  Athletics            Athletics   
      31130  2012       London  Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                       Event  \
      7467           VENEGAS, Juan E.     PUR    Men    51 - 54KG (Bantamweight)   
      14284        MALDONADO, Orlando     PUR    Men    - 48KG (Light-Flyweight)   
      17046            ORTIZ, Luis F.     PUR    Men     57 - 60KG (Lightweight)   
      17059       GONZALEZ, Aristides     PUR    Men                     71-75KG   
      20211  ACEVEDO SANTIAGO, Anibal     PUR    Men  63.5 - 67KG (Welterweight)   
      21952            SANTOS, Daniel     PUR    Men  63.5 - 67KG (Welterweight)   
      29632            CULSON, Javier     PUR    Men                400M Hurdles   
      31130     ESPINAL, Jaime Yusept     PUR    Men                    Wf 84 KG   
      
              Medal  
      7467   Bronze  
      14284  Bronze  
      17046  Silver  
      17059  Bronze  
      20211  Bronze  
      21952  Bronze  
      29632  Bronze  
      31130  Silver  ),
     ('QAT',
             Year       City          Sport     Discipline                  Athlete  \
      19870  1992  Barcelona      Athletics      Athletics  SULAIMAN, Mohamed Ahmed   
      25089  2000     Sydney  Weightlifting  Weightlifting         ASAAD, Said Saif   
      29730  2012     London      Athletics      Athletics      BARSHIM, Mutaz Essa   
      30868  2012     London       Shooting       Shooting       AL-ATTIYAH, Nasser   
      
            Country Gender      Event   Medal  
      19870     QAT    Men      1500M  Bronze  
      25089     QAT    Men      105KG  Bronze  
      29730     QAT    Men  High Jump  Bronze  
      30868     QAT    Men      Skeet  Bronze  ),
     ('ROU',
             Year    City          Sport     Discipline                    Athlete  \
      4730   1924   Paris          Rugby          Rugby            ANASTASIADE, N.   
      4731   1924   Paris          Rugby          Rugby           ARMASEL, Dumitru   
      4732   1924   Paris          Rugby          Rugby           BENTIA, Gheorghe   
      4733   1924   Paris          Rugby          Rugby             COCIOCIAHO, J.   
      4734   1924   Paris          Rugby          Rugby             CRATUNESCO, C.   
      ...     ...     ...            ...            ...                        ...   
      30580  2012  London           Judo           Judo             DUMITRU, Alina   
      30600  2012  London           Judo           Judo          CAPRIORIU, Corina   
      30839  2012  London       Shooting       Shooting    MOLDOVEANU, Alin George   
      31077  2012  London  Weightlifting  Weightlifting  MARTIN, Razvan Constantin   
      31079  2012  London  Weightlifting  Weightlifting      COCOS, Roxana Daniela   
      
            Country Gender          Event   Medal  
      4730      ROU    Men          Rugby  Bronze  
      4731      ROU    Men          Rugby  Bronze  
      4732      ROU    Men          Rugby  Bronze  
      4733      ROU    Men          Rugby  Bronze  
      4734      ROU    Men          Rugby  Bronze  
      ...       ...    ...            ...     ...  
      30580     ROU  Women        - 48 KG  Silver  
      30600     ROU  Women      52 - 57KG  Silver  
      30839     ROU    Men  10M Air Rifle    Gold  
      31077     ROU    Men           69KG  Bronze  
      31079     ROU  Women           69KG  Silver  
      
      [640 rows x 9 columns]),
     ('RSA',
             Year       City      Sport    Discipline                 Athlete  \
      1191   1908     London  Athletics     Athletics        WALKER, Reginald   
      1272   1908     London  Athletics     Athletics    HEFFERON, Charles A.   
      2121   1912  Stockholm  Athletics     Athletics  MCARTHUR, Kennedy Kane   
      2122   1912  Stockholm  Athletics     Athletics   GITSHAM, Christian W.   
      2143   1912  Stockholm    Cycling  Cycling Road          LEWIS, Rudolph   
      ...     ...        ...        ...           ...                     ...   
      29958  2012     London      Canoe  Canoe Sprint      HARTLEY, Bridgitte   
      30731  2012     London     Rowing        Rowing       BRITTAIN, Matthew   
      30732  2012     London     Rowing        Rowing           NDLOVU, Sizwe   
      30733  2012     London     Rowing        Rowing             SMITH, John   
      30734  2012     London     Rowing        Rowing         THOMPSON, James   
      
            Country Gender                  Event   Medal  
      1191      RSA    Men                   100M    Gold  
      1272      RSA    Men               Marathon  Silver  
      2121      RSA    Men               Marathon    Gold  
      2122      RSA    Men               Marathon  Silver  
      2143      RSA    Men  Individual Time Trial    Gold  
      ...       ...    ...                    ...     ...  
      29958     RSA  Women               K-1 500M  Bronze  
      30731     RSA    Men          Lightweight 4    Gold  
      30732     RSA    Men          Lightweight 4    Gold  
      30733     RSA    Men          Lightweight 4    Gold  
      30734     RSA    Men          Lightweight 4    Gold  
      
      [106 rows x 9 columns]),
     ('RU1',
            Year       City      Sport       Discipline  \
      1852  1908     London    Skating   Figure skating   
      1927  1908     London  Wrestling  Wrestling Gre-R   
      1930  1908     London  Wrestling  Wrestling Gre-R   
      2535  1912  Stockholm     Rowing           Rowing   
      2538  1912  Stockholm    Sailing          Sailing   
      2539  1912  Stockholm    Sailing          Sailing   
      2540  1912  Stockholm    Sailing          Sailing   
      2541  1912  Stockholm    Sailing          Sailing   
      2542  1912  Stockholm    Sailing          Sailing   
      2543  1912  Stockholm    Sailing          Sailing   
      2544  1912  Stockholm    Sailing          Sailing   
      2658  1912  Stockholm   Shooting         Shooting   
      2659  1912  Stockholm   Shooting         Shooting   
      2660  1912  Stockholm   Shooting         Shooting   
      2661  1912  Stockholm   Shooting         Shooting   
      2752  1912  Stockholm   Shooting         Shooting   
      2818  1912  Stockholm  Wrestling  Wrestling Gre-R   
      
                                                 Athlete Country Gender  \
      1852                                PANIN, Nikolay     RU1    Men   
      1927                               ORLOFF, Nikolaï     RU1    Men   
      1930                           PETROFF, Aleksander     RU1    Men   
      2535                    KUSIK, Mikhaïl Maksimilian     RU1    Men   
      2538  Beloselsky-Belozersky, Esper Konstantinovich     RU1    Men   
      2539                               BRASCHE, Ernest     RU1    Men   
      2540                                LINDBLOM, Karl     RU1    Men   
      2541                          PUSCHNITSKY, Nikolaï     RU1    Men   
      2542                           RODIONOV, Aleksandr     RU1    Men   
      2543                             SCHOMAKER, Iossif     RU1    Men   
      2544                                STRAUCH, Filip     RU1    Men   
      2658                                DE KACHE, Amos     RU1    Men   
      2659                         DE MELNITSKY, Nikolaï     RU1    Men   
      2660                     DE PANTELEYMONOFF, Georgi     RU1    Men   
      2661                       DE WEYLOCHNIKOFF, Pavel     RU1    Men   
      2752                                   BLAU, Harry     RU1    Men   
      2818                                 KLEIN, Martin     RU1    Men   
      
                                 Event   Medal  
      1852             Special Figures    Gold  
      1927      - 66.6KG (Lightweight)  Silver  
      1930  + 93KG (Super Heavyweight)  Silver  
      2535          Single Sculls (1X)  Bronze  
      2538                         10M  Bronze  
      2539                         10M  Bronze  
      2540                         10M  Bronze  
      2541                         10M  Bronze  
      2542                         10M  Bronze  
      2543                         10M  Bronze  
      2544                         10M  Bronze  
      2658       30M Army Pistol, Team  Silver  
      2659       30M Army Pistol, Team  Silver  
      2660       30M Army Pistol, Team  Silver  
      2661       30M Army Pistol, Team  Silver  
      2752          Trap (125 Targets)  Bronze  
      2818  67.5 - 75KG (Middleweight)  Silver  ),
     ('RUS',
             Year     City      Sport           Discipline              Athlete  \
      21303  1996  Atlanta   Aquatics               Diving       SAUTIN, Dmitry   
      21313  1996  Atlanta   Aquatics               Diving        LASHKO, Irina   
      21326  1996  Atlanta   Aquatics             Swimming   KULIKOV, Vladislav   
      21327  1996  Atlanta   Aquatics             Swimming     PANKRATOV, Denis   
      21333  1996  Atlanta   Aquatics             Swimming     POPOV, Alexander   
      ...     ...      ...        ...                  ...                  ...   
      31144  2012   London  Wrestling  Wrestling Freestyle    SEMENOV, Mingiyan   
      31147  2012   London  Wrestling  Wrestling Freestyle  KURAMAGOMEDOV, Zaur   
      31153  2012   London  Wrestling  Wrestling Freestyle        VLASOV, Roman   
      31157  2012   London  Wrestling  Wrestling Freestyle        KHUGAEV, Alan   
      31162  2012   London  Wrestling  Wrestling Freestyle       TOTROV, Rustam   
      
            Country Gender           Event   Medal  
      21303     RUS    Men    10M Platform    Gold  
      21313     RUS  Women  3M Springboard  Silver  
      21326     RUS    Men  100M Butterfly  Bronze  
      21327     RUS    Men  100M Butterfly    Gold  
      21333     RUS    Men  100M Freestyle    Gold  
      ...       ...    ...             ...     ...  
      31144     RUS    Men        Wg 55 KG  Bronze  
      31147     RUS    Men        Wg 60 KG  Bronze  
      31153     RUS    Men        Wg 74 KG    Gold  
      31157     RUS    Men        Wg 84 KG    Gold  
      31162     RUS    Men        Wg 96 KG  Silver  
      
      [768 rows x 9 columns]),
     ('SCG',
             Year    City     Sport  Discipline                Athlete Country  \
      25456  2004  Athens  Aquatics  Water polo      CIRIC, Aleksandar     SCG   
      25457  2004  Athens  Aquatics  Water polo     GOJKOVIC, Vladimir     SCG   
      25458  2004  Athens  Aquatics  Water polo     IKODINOVIC, Danilo     SCG   
      25459  2004  Athens  Aquatics  Water polo        JELENIC, Viktor     SCG   
      25460  2004  Athens  Aquatics  Water polo         JOKIC, Predrag     SCG   
      25461  2004  Athens  Aquatics  Water polo        KULJACA, Nikola     SCG   
      25462  2004  Athens  Aquatics  Water polo        NIKIC, Slobodan     SCG   
      25463  2004  Athens  Aquatics  Water polo      SAPIC, Aleksandar     SCG   
      25464  2004  Athens  Aquatics  Water polo           SAVIC, Dejan     SCG   
      25465  2004  Athens  Aquatics  Water polo           SEFIK, Denis     SCG   
      25466  2004  Athens  Aquatics  Water polo       TRBOJEVIC, Petar     SCG   
      25467  2004  Athens  Aquatics  Water polo        UDOVICIC, Vanja     SCG   
      25468  2004  Athens  Aquatics  Water polo  VUJASINOVIC, Vladimir     SCG   
      26834  2004  Athens  Shooting    Shooting         SEKARIC, Jasna     SCG   
      
            Gender                      Event   Medal  
      25456    Men                 Water Polo  Silver  
      25457    Men                 Water Polo  Silver  
      25458    Men                 Water Polo  Silver  
      25459    Men                 Water Polo  Silver  
      25460    Men                 Water Polo  Silver  
      25461    Men                 Water Polo  Silver  
      25462    Men                 Water Polo  Silver  
      25463    Men                 Water Polo  Silver  
      25464    Men                 Water Polo  Silver  
      25465    Men                 Water Polo  Silver  
      25466    Men                 Water Polo  Silver  
      25467    Men                 Water Polo  Silver  
      25468    Men                 Water Polo  Silver  
      26834  Women  10M Air Pistol (40 Shots)  Silver  ),
     ('SEN',
             Year   City      Sport Discipline                  Athlete Country  \
      18324  1988  Seoul  Athletics  Athletics  DIA BA, El Hadji Amadou     SEN   
      
            Gender         Event   Medal  
      18324    Men  400M Hurdles  Silver  ),
     ('SGP',
             Year    City         Sport    Discipline         Athlete Country  \
      30883  2012  London  Table Tennis  Table Tennis  FENG, Tian Wei     SGP   
      30899  2012  London  Table Tennis  Table Tennis  FENG, Tian Wei     SGP   
      30900  2012  London  Table Tennis  Table Tennis     LI, Jia Wei     SGP   
      30901  2012  London  Table Tennis  Table Tennis     WANG, Yuegu     SGP   
      
            Gender    Event   Medal  
      30883  Women  Singles  Bronze  
      30899  Women     Team  Bronze  
      30900  Women     Team  Bronze  
      30901  Women     Team  Bronze  ),
     ('SIN',
             Year     City          Sport     Discipline                  Athlete  \
      10616  1960     Rome  Weightlifting  Weightlifting  TAN, Howe-Liang (Tiger)   
      28957  2008  Beijing   Table Tennis   Table Tennis           FENG, Tian Wei   
      28958  2008  Beijing   Table Tennis   Table Tennis               LI, Jiawei   
      28959  2008  Beijing   Table Tennis   Table Tennis             WANG, Yue Gu   
      
            Country Gender                             Event   Medal  
      10616     SIN    Men  60 - 67.5KG, Total (Lightweight)  Silver  
      28957     SIN  Women                              Team  Silver  
      28958     SIN  Women                              Team  Silver  
      28959     SIN  Women                              Team  Silver  ),
     ('SLO',
             Year       City          Sport       Discipline            Athlete  \
      20859  1992  Barcelona         Rowing           Rowing         COP, Iztok   
      20860  1992  Barcelona         Rowing           Rowing     ZVEGELJ, Denis   
      20931  1992  Barcelona         Rowing           Rowing       JANSA, Milan   
      20932  1992  Barcelona         Rowing           Rowing   KLEMENCIC, Janez   
      20933  1992  Barcelona         Rowing           Rowing     MIRJANIC, Saso   
      20934  1992  Barcelona         Rowing           Rowing      MUJKIC, Sadik   
      21605  1996    Atlanta      Athletics        Athletics  BUKOVEC, Brigitta   
      22052  1996    Atlanta  Canoe / Kayak  Canoe / Kayak S    VEHOVAR, Andraz   
      24647  2000     Sydney         Rowing           Rowing         COP, Iztok   
      24648  2000     Sydney         Rowing           Rowing         SPIK, Luka   
      24865  2000     Sydney       Shooting         Shooting   DEBEVEC, Rajmond   
      25652  2004     Athens      Athletics        Athletics    CEPLAK, Jolanda   
      26597  2004     Athens           Judo             Judo      ZOLNIR, Urska   
      26644  2004     Athens         Rowing           Rowing         COP, Iztok   
      26645  2004     Athens         Rowing           Rowing         SPIK, Luka   
      26808  2004     Athens        Sailing          Sailing    ZBOGAR, Vasilij   
      27262  2008    Beijing       Aquatics         Swimming     ISAKOVIC, Sara   
      27672  2008    Beijing      Athletics        Athletics     KOZMUS, Primoz   
      28599  2008    Beijing           Judo             Judo   POLAVDER, Lucija   
      28815  2008    Beijing        Sailing          Sailing    ZBOGAR, Vasilij   
      28870  2008    Beijing       Shooting         Shooting   DEBEVEC, Rajmond   
      29720  2012     London      Athletics        Athletics     KOZMUS, Primoz   
      30603  2012     London           Judo             Judo      ZOLNIR, Urska   
      30669  2012     London         Rowing           Rowing         COP, Iztok   
      30670  2012     London         Rowing           Rowing         SPIK, Luka   
      30862  2012     London       Shooting         Shooting   DEBEVEC, Rajmond   
      
            Country Gender                               Event   Medal  
      20859     SLO    Men                   Coxless Pair (2-)  Bronze  
      20860     SLO    Men                   Coxless Pair (2-)  Bronze  
      20931     SLO    Men          Four Without Coxswain (4-)  Bronze  
      20932     SLO    Men          Four Without Coxswain (4-)  Bronze  
      20933     SLO    Men          Four Without Coxswain (4-)  Bronze  
      20934     SLO    Men          Four Without Coxswain (4-)  Bronze  
      21605     SLO  Women                        100M Hurdles  Silver  
      22052     SLO    Men                  K-1 (Kayak Single)  Silver  
      24647     SLO    Men                  Double Sculls (2X)    Gold  
      24648     SLO    Men                  Double Sculls (2X)    Gold  
      24865     SLO    Men  50M Rifle 3 Positions (3X40 Shots)    Gold  
      25652     SLO  Women                                800M  Bronze  
      26597     SLO  Women       57 - 63KG (Half-Middleweight)  Bronze  
      26644     SLO    Men                  Double Sculls (2X)  Silver  
      26645     SLO    Men                  Double Sculls (2X)  Silver  
      26808     SLO    Men   Single-Handed Dinghy Open (Laser)  Bronze  
      27262     SLO  Women                      200M Freestyle  Silver  
      27672     SLO    Men                        Hammer Throw    Gold  
      28599     SLO  Women                + 78KG (Heavyweight)  Bronze  
      28815     SLO    Men           Laser - One Person Dinghy  Silver  
      28870     SLO    Men  50M Rifle 3 Positions (3X40 Shots)  Bronze  
      29720     SLO    Men                        Hammer Throw  Silver  
      30603     SLO  Women                           57 - 63KG    Gold  
      30669     SLO    Men                       Double Sculls  Bronze  
      30670     SLO    Men                       Double Sculls  Bronze  
      30862     SLO    Men                     50M Rifle Prone  Bronze  ),
     ('SRB',
             Year     City      Sport  Discipline                Athlete Country  \
      27225  2008  Beijing   Aquatics    Swimming         CAVIC, Milorad     SRB   
      27443  2008  Beijing   Aquatics  Water polo      CIRIC, Aleksandar     SRB   
      27444  2008  Beijing   Aquatics  Water polo       FILIPOVIC, Filip     SRB   
      27445  2008  Beijing   Aquatics  Water polo           GOCIC, Zivko     SRB   
      27446  2008  Beijing   Aquatics  Water polo        PEKOVIC, Branko     SRB   
      27447  2008  Beijing   Aquatics  Water polo      PIJETLOVIC, Dusko     SRB   
      27448  2008  Beijing   Aquatics  Water polo    PRLAINOVIC, Andrija     SRB   
      27449  2008  Beijing   Aquatics  Water polo         RADJEN, Nikola     SRB   
      27450  2008  Beijing   Aquatics  Water polo      SAPIC, Aleksandar     SRB   
      27451  2008  Beijing   Aquatics  Water polo           SAVIC, Dejan     SRB   
      27452  2008  Beijing   Aquatics  Water polo           SEFIK, Denis     SRB   
      27453  2008  Beijing   Aquatics  Water polo         SORO, Slobodan     SRB   
      27454  2008  Beijing   Aquatics  Water polo        UDOVICIC, Vanja     SRB   
      27455  2008  Beijing   Aquatics  Water polo  VUJASINOVIC, Vladimir     SRB   
      29004  2008  Beijing     Tennis      Tennis        DJOKOVIC, Novak     SRB   
      29506  2012   London   Aquatics  Water Polo         ALEKSIC, Milan     SRB   
      29507  2012   London   Aquatics  Water Polo       FILIPOVIC, Filip     SRB   
      29508  2012   London   Aquatics  Water Polo           GOCIC, Zivko     SRB   
      29509  2012   London   Aquatics  Water Polo          MANDIC, Dusan     SRB   
      29510  2012   London   Aquatics  Water Polo       MITROVIC, Stefan     SRB   
      29511  2012   London   Aquatics  Water Polo        NIKIC, Slobodan     SRB   
      29512  2012   London   Aquatics  Water Polo      PIJETLOVIC, Dusko     SRB   
      29513  2012   London   Aquatics  Water Polo      PIJETLOVIC, Gojko     SRB   
      29514  2012   London   Aquatics  Water Polo    PRLAINOVIC, Andrija     SRB   
      29515  2012   London   Aquatics  Water Polo         RADJEN, Nikola     SRB   
      29516  2012   London   Aquatics  Water Polo       SAPONJIC, Aleksa     SRB   
      29517  2012   London   Aquatics  Water Polo         SORO, Slobodan     SRB   
      29518  2012   London   Aquatics  Water Polo        UDOVICIC, Vanja     SRB   
      30835  2012   London   Shooting    Shooting        ZLATIC, Andrija     SRB   
      30858  2012   London   Shooting    Shooting      MAKSIMOVIC, Ivana     SRB   
      30910  2012   London  Taekwondo   Taekwondo         MANDIC, Milica     SRB   
      
            Gender                  Event   Medal  
      27225    Men         100M Butterfly  Silver  
      27443    Men             Water Polo  Bronze  
      27444    Men             Water Polo  Bronze  
      27445    Men             Water Polo  Bronze  
      27446    Men             Water Polo  Bronze  
      27447    Men             Water Polo  Bronze  
      27448    Men             Water Polo  Bronze  
      27449    Men             Water Polo  Bronze  
      27450    Men             Water Polo  Bronze  
      27451    Men             Water Polo  Bronze  
      27452    Men             Water Polo  Bronze  
      27453    Men             Water Polo  Bronze  
      27454    Men             Water Polo  Bronze  
      27455    Men             Water Polo  Bronze  
      29004    Men                Singles  Bronze  
      29506    Men             Water Polo  Bronze  
      29507    Men             Water Polo  Bronze  
      29508    Men             Water Polo  Bronze  
      29509    Men             Water Polo  Bronze  
      29510    Men             Water Polo  Bronze  
      29511    Men             Water Polo  Bronze  
      29512    Men             Water Polo  Bronze  
      29513    Men             Water Polo  Bronze  
      29514    Men             Water Polo  Bronze  
      29515    Men             Water Polo  Bronze  
      29516    Men             Water Polo  Bronze  
      29517    Men             Water Polo  Bronze  
      29518    Men             Water Polo  Bronze  
      30835    Men         10M Air Pistol  Bronze  
      30858  Women  50M Rifle 3 Positions  Silver  
      30910  Women                + 67 KG    Gold  ),
     ('SRI',
             Year    City      Sport Discipline                 Athlete Country  \
      7327   1948  London  Athletics  Athletics           WHITE, Duncan     SRI   
      23543  2000  Sydney  Athletics  Athletics  JAYASINGHE, Susanthika     SRI   
      
            Gender         Event   Medal  
      7327     Men  400M Hurdles  Silver  
      23543  Women          200M  Silver  ),
     ('SUD',
             Year     City      Sport Discipline               Athlete Country  \
      27658  2008  Beijing  Athletics  Athletics  ISMAIL, Ismail Ahmed     SUD   
      
            Gender Event   Medal  
      27658    Men  800M  Silver  ),
     ('SUI',
             Year     City       Sport     Discipline              Athlete Country  \
      75     1896   Athens  Gymnastics    Artistic G.        ZUTTER, Louis     SUI   
      76     1896   Athens  Gymnastics    Artistic G.        ZUTTER, Louis     SUI   
      116    1896   Athens  Gymnastics    Artistic G.        ZUTTER, Louis     SUI   
      583    1900    Paris    Shooting       Shooting     LÜTHI, Friedrich     SUI   
      584    1900    Paris    Shooting       Shooting         PROBST, Paul     SUI   
      ...     ...      ...         ...            ...                  ...     ...   
      28995  2008  Beijing      Tennis         Tennis  WAWRINKA, Stanislas     SUI   
      30076  2012   London     Cycling  Mountain Bike       SCHURTER, Nino     SUI   
      30111  2012   London  Equestrian        Jumping       GUERDAT, Steve     SUI   
      30953  2012   London      Tennis         Tennis       FEDERER, Roger     SUI   
      30961  2012   London   Triathlon      Triathlon       SPIRIG, Nicola     SUI   
      
            Gender                  Event   Medal  
      75       Men          Parallel Bars  Silver  
      76       Men           Pommel Horse    Gold  
      116      Men                  Vault  Silver  
      583      Men  50M Army Pistol, Team    Gold  
      584      Men  50M Army Pistol, Team    Gold  
      ...      ...                    ...     ...  
      28995    Men                Doubles    Gold  
      30076    Men          Cross-Country  Silver  
      30111    Men             Individual    Gold  
      30953    Men                Singles  Silver  
      30961  Women             Individual    Gold  
      
      [380 rows x 9 columns]),
     ('SUR',
             Year       City     Sport Discipline                Athlete Country  \
      18076  1988      Seoul  Aquatics   Swimming  NESTY, Anthony Conrad     SUR   
      19621  1992  Barcelona  Aquatics   Swimming  NESTY, Anthony Conrad     SUR   
      
            Gender           Event   Medal  
      18076    Men  100M Butterfly    Gold  
      19621    Men  100M Butterfly  Bronze  ),
     ('SVK',
             Year     City          Sport       Discipline               Athlete  \
      21977  1996  Atlanta  Canoe / Kayak  Canoe / Kayak F  KNAZOVICKY, Slavomir   
      22042  1996  Atlanta  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      22888  1996  Atlanta       Shooting         Shooting          GONCI, Jozef   
      23214  2000   Sydney       Aquatics         Swimming    MORAVCOVA, Martina   
      23248  2000   Sydney       Aquatics         Swimming    MORAVCOVA, Martina   
      23983  2000   Sydney  Canoe / Kayak  Canoe / Kayak S         MINCIK, Juraj   
      23985  2000   Sydney  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      23988  2000   Sydney  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Pavol   
      23989  2000   Sydney  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Peter   
      25969  2004   Athens  Canoe / Kayak  Canoe / Kayak F           BACA, Juraj   
      25970  2004   Athens  Canoe / Kayak  Canoe / Kayak F    RISZDORFER, Michal   
      25971  2004   Athens  Canoe / Kayak  Canoe / Kayak F   RISZDORFER, Richard   
      25972  2004   Athens  Canoe / Kayak  Canoe / Kayak F           VLCEK, Erik   
      25995  2004   Athens  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      25998  2004   Athens  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Pavol   
      25999  2004   Athens  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Peter   
      26006  2004   Athens  Canoe / Kayak  Canoe / Kayak S        KALISKA, Elena   
      26603  2004   Athens           Judo             Judo          KRNAC, Jozef   
      26841  2004   Athens       Shooting         Shooting          GONCI, Jozef   
      27987  2008  Beijing  Canoe / Kayak  Canoe / Kayak F    RISZDORFER, Michal   
      27988  2008  Beijing  Canoe / Kayak  Canoe / Kayak F   RISZDORFER, Richard   
      27989  2008  Beijing  Canoe / Kayak  Canoe / Kayak F           TARR, Juraj   
      27990  2008  Beijing  Canoe / Kayak  Canoe / Kayak F           VLCEK, Erik   
      28004  2008  Beijing  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      28008  2008  Beijing  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Pavol   
      28009  2008  Beijing  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Peter   
      28016  2008  Beijing  Canoe / Kayak  Canoe / Kayak S        KALISKA, Elena   
      28890  2008  Beijing       Shooting         Shooting   STEFECEKOVA, Zuzana   
      29185  2008  Beijing      Wrestling  Wrestling Free.       MUSULBES, David   
      29922  2012   London          Canoe     Canoe Slalom      MARTIKAN, Michal   
      29927  2012   London          Canoe     Canoe Slalom   HOCHSCHORNER, Pavol   
      29928  2012   London          Canoe     Canoe Slalom   HOCHSCHORNER, Peter   
      30871  2012   London       Shooting         Shooting      BARTEKOVA, Danka   
      30876  2012   London       Shooting         Shooting   STEFECEKOVA, Zuzana   
      
            Country Gender                         Event   Medal  
      21977     SVK    Men       C-1 500M (Canoe Single)  Silver  
      22042     SVK    Men            C-1 (Canoe Single)    Gold  
      22888     SVK    Men    50M Rifle Prone (60 Shots)  Bronze  
      23214     SVK  Women                100M Butterfly  Silver  
      23248     SVK  Women                200M Freestyle  Silver  
      23983     SVK    Men            C-1 (Canoe Single)  Bronze  
      23985     SVK    Men            C-1 (Canoe Single)  Silver  
      23988     SVK    Men            C-2 (Canoe Double)    Gold  
      23989     SVK    Men            C-2 (Canoe Double)    Gold  
      25969     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25970     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25971     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25972     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25995     SVK    Men            C-1 (Canoe Single)  Silver  
      25998     SVK    Men            C-2 (Canoe Double)    Gold  
      25999     SVK    Men            C-2 (Canoe Double)    Gold  
      26006     SVK  Women            K-1 (Kayak Single)    Gold  
      26603     SVK    Men  60 - 66KG (Half-Lightweight)  Silver  
      26841     SVK    Men      10M Air Rifle (60 Shots)  Bronze  
      27987     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      27988     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      27989     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      27990     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      28004     SVK    Men            C-1 (Canoe Single)    Gold  
      28008     SVK    Men            C-2 (Canoe Double)    Gold  
      28009     SVK    Men            C-2 (Canoe Double)    Gold  
      28016     SVK  Women            K-1 (Kayak Single)    Gold  
      28890     SVK  Women             Trap (75 Targets)  Silver  
      29185     SVK    Men                    96 - 120KG  Bronze  
      29922     SVK    Men                  C-1 (Single)  Bronze  
      29927     SVK    Men                  C-2 (Double)  Bronze  
      29928     SVK    Men                  C-2 (Double)  Bronze  
      30871     SVK  Women                         Skeet  Bronze  
      30876     SVK  Women                          Trap  Silver  ),
     ('SWE',
             Year    City      Sport           Discipline             Athlete  \
      291    1900   Paris  Athletics            Athletics         FAST, Ernst   
      1133   1908  London   Aquatics               Diving    SPANGBERG, Arvid   
      1134   1908  London   Aquatics               Diving  JOHANSSON, Hjalmar   
      1135   1908  London   Aquatics               Diving     MALMSTRÖM, Karl   
      1143   1908  London   Aquatics             Swimming  JULIN, Harald S.A.   
      ...     ...     ...        ...                  ...                 ...   
      30828  2012  London    Sailing              Sailing       SALMINEN, Max   
      30864  2012  London   Shooting             Shooting       DAHLBY, Hakan   
      30962  2012  London  Triathlon            Triathlon        NORDEN, Lisa   
      31139  2012  London  Wrestling  Wrestling Freestyle        EUREN, Johan   
      31164  2012  London  Wrestling  Wrestling Freestyle      LIDBERG, Jimmy   
      
            Country Gender            Event   Medal  
      291       SWE    Men         Marathon  Bronze  
      1133      SWE    Men     10M Platform  Bronze  
      1134      SWE    Men     10M Platform    Gold  
      1135      SWE    Men     10M Platform  Silver  
      1143      SWE    Men   100M Freestyle  Bronze  
      ...       ...    ...              ...     ...  
      30828     SWE    Men             Star    Gold  
      30864     SWE    Men  Double Trap 150  Silver  
      30962     SWE  Women       Individual  Silver  
      31139     SWE    Men        Wg 120 KG  Bronze  
      31164     SWE    Men         Wg 96 KG  Bronze  
      
      [1044 rows x 9 columns]),
     ('SYR',
             Year         City      Sport       Discipline          Athlete Country  \
      18020  1984  Los Angeles  Wrestling  Wrestling Free.    ATIYEH, Josep     SYR   
      21727  1996      Atlanta  Athletics        Athletics    SHOUAA, Ghada     SYR   
      25920  2004       Athens     Boxing           Boxing  AL SHAMI, Naser     SYR   
      
            Gender                     Event   Medal  
      18020    Men  90 - 100KG (Heavyweight)  Silver  
      21727  Women                Heptathlon    Gold  
      25920    Men   81 - 91KG (Heavyweight)  Bronze  ),
     ('TAN',
             Year    City      Sport Discipline            Athlete Country Gender  \
      15402  1980  Moscow  Athletics  Athletics      BAYI, Filbert     TAN    Men   
      15462  1980  Moscow  Athletics  Athletics  NYAMBUI, Suleiman     TAN    Men   
      
                          Event   Medal  
      15402  3000M Steeplechase  Silver  
      15462               5000M  Silver  ),
     ('TCH',
             Year       City          Sport       Discipline          Athlete  \
      3577   1920    Antwerp     Ice Hockey       Ice Hockey     DUSEK, Adolf   
      3578   1920    Antwerp     Ice Hockey       Ice Hockey  HARTMANN, Karel   
      3579   1920    Antwerp     Ice Hockey       Ice Hockey      LOOS, Vilém   
      3580   1920    Antwerp     Ice Hockey       Ice Hockey      PALOUS, Jan   
      3581   1920    Antwerp     Ice Hockey       Ice Hockey        PEKA, Jan   
      ...     ...        ...            ...              ...              ...   
      20307  1992  Barcelona  Canoe / Kayak  Canoe / Kayak S      ROHAN, Jiri   
      20308  1992  Barcelona  Canoe / Kayak  Canoe / Kayak S  SIMEK, Miroslav   
      20999  1992  Barcelona         Rowing           Rowing  CHALUPA, Vaclav   
      21084  1992  Barcelona       Shooting         Shooting  RACANSKY, Lubos   
      21091  1992  Barcelona       Shooting         Shooting   HRDLICKA, Petr   
      
            Country Gender                             Event   Medal  
      3577      TCH    Men                        Ice Hockey  Bronze  
      3578      TCH    Men                        Ice Hockey  Bronze  
      3579      TCH    Men                        Ice Hockey  Bronze  
      3580      TCH    Men                        Ice Hockey  Bronze  
      3581      TCH    Men                        Ice Hockey  Bronze  
      ...       ...    ...                               ...     ...  
      20307     TCH    Men                C-2 (Canoe Double)  Silver  
      20308     TCH    Men                C-2 (Canoe Double)  Silver  
      20999     TCH    Men                Single Sculls (1X)  Silver  
      21084     TCH    Men  50M Running Target (30+30 Shots)  Bronze  
      21091     TCH    Men                Trap (125 Targets)    Gold  
      
      [329 rows x 9 columns]),
     ('TGA',
             Year     City   Sport Discipline         Athlete Country Gender  \
      21931  1996  Atlanta  Boxing     Boxing  WOLFGRAM, Paea     TGA    Men   
      
                                  Event   Medal  
      21931  + 91KG (Super Heavyweight)  Silver  ),
     ('THA',
             Year         City          Sport     Discipline  \
      14285  1976     Montreal         Boxing         Boxing   
      17050  1984  Los Angeles         Boxing         Boxing   
      18525  1988        Seoul         Boxing         Boxing   
      20212  1992    Barcelona         Boxing         Boxing   
      21936  1996      Atlanta         Boxing         Boxing   
      21942  1996      Atlanta         Boxing         Boxing   
      23876  2000       Sydney         Boxing         Boxing   
      23899  2000       Sydney         Boxing         Boxing   
      25101  2000       Sydney  Weightlifting  Weightlifting   
      25895  2004       Athens         Boxing         Boxing   
      25906  2004       Athens         Boxing         Boxing   
      25913  2004       Athens         Boxing         Boxing   
      26946  2004       Athens      Taekwondo      Taekwondo   
      27087  2004       Athens  Weightlifting  Weightlifting   
      27091  2004       Athens  Weightlifting  Weightlifting   
      27093  2004       Athens  Weightlifting  Weightlifting   
      27109  2004       Athens  Weightlifting  Weightlifting   
      27896  2008      Beijing         Boxing         Boxing   
      27917  2008      Beijing         Boxing         Boxing   
      28963  2008      Beijing      Taekwondo      Taekwondo   
      29116  2008      Beijing  Weightlifting  Weightlifting   
      29873  2012       London         Boxing         Boxing   
      30904  2012       London      Taekwondo      Taekwondo   
      31067  2012       London  Weightlifting  Weightlifting   
      31068  2012       London  Weightlifting  Weightlifting   
      
                                       Athlete Country Gender  \
      14285                   POOLTARAT, Payao     THA    Men   
      17050                  UMPONMAHA, Dhawee     THA    Men   
      18525                    MOOLSAN, Phajol     THA    Men   
      20212                    CHENGLAI, Arkom     THA    Men   
      21936                     KHADPO, Vichai     THA    Men   
      21942                   KAMSING, Somluck     THA    Men   
      23876                      PONLID, Wijan     THA    Men   
      23899               THONGBURAN, Pornchai     THA    Men   
      25101                 SUTA, Khassaraporn     THA  Women   
      25895                 PETCHKOOM, Worapoj     THA    Men   
      25906                 BOONJUMNONG, Manus     THA    Men   
      25913            PRASATHINPHIMAI, Suriya     THA    Men   
      26946              BOORAPOLCHAI, Yaowapa     THA  Women   
      27087                 WIRATTHAWORN, Aree     THA  Women   
      27091                   POLSAK, Udomporn     THA  Women   
      27093                    KAMEAIM, Wandee     THA  Women   
      27109                   THONGSUK, Pawina     THA  Women   
      27896                  JONGJOHOR, Somjit     THA    Men   
      27917                 BOONJUMNONG, Manus     THA    Men   
      28963                  PUEDPONG, Buttree     THA  Women   
      29116  JAROENRATTANATARAKOON, Prapawadee     THA  Women   
      29873                  PONGPRAYOON, Kaeo     THA    Men   
      30904                  SONKHAM, Chanatip     THA  Women   
      31067                  SIRIKAEW, Pimsiri     THA  Women   
      31068                   GULNOI, Rattikan     THA  Women   
      
                                        Event   Medal  
      14285          - 48KG (Light-Flyweight)  Bronze  
      17050  60 - 63.5KG (Light-Welterweight)  Silver  
      18525          51 - 54KG (Bantamweight)  Bronze  
      20212        63.5 - 67KG (Welterweight)  Bronze  
      21936          51 - 54KG (Bantamweight)  Bronze  
      21942         54 - 57KG (Featherweight)    Gold  
      23876             48 - 51KG (Flyweight)    Gold  
      23899    67 - 71KG (Light-Middleweight)  Bronze  
      25101                              58KG  Bronze  
      25895          51 - 54KG (Bantamweight)  Silver  
      25906                        60 - 64 KG    Gold  
      25913                        69 - 75 KG  Bronze  
      26946                           - 49 KG  Bronze  
      27087                              48KG  Bronze  
      27091                              53KG    Gold  
      27093                              58KG  Bronze  
      27109                              75KG    Gold  
      27896             48 - 51KG (Flyweight)    Gold  
      27917                        60 - 64 KG  Silver  
      28963                           - 49 KG  Silver  
      29116                              53KG    Gold  
      29873                         46 - 49KG  Silver  
      30904                           - 49 KG  Bronze  
      31067                              58KG  Silver  
      31068                              58KG  Bronze  ),
     ('TJK',
             Year     City      Sport       Discipline             Athlete Country  \
      28622  2008  Beijing       Judo             Judo       BOQIEV, Rasul     TJK   
      29180  2008  Beijing  Wrestling  Wrestling Free.  ABDUSALOMOV, Yusup     TJK   
      29899  2012   London     Boxing           Boxing   CHORIEVA, Mavzuna     TJK   
      
            Gender                    Event   Medal  
      28622    Men  66 - 73KG (Lightweight)  Bronze  
      29180    Men                74 - 84KG  Silver  
      29899  Women                    60 KG  Bronze  ),
     ('TOG',
             Year     City          Sport       Discipline             Athlete  \
      28012  2008  Beijing  Canoe / Kayak  Canoe / Kayak S  BOUKPETI, Benjamin   
      
            Country Gender               Event   Medal  
      28012     TOG    Men  K-1 (Kayak Single)  Bronze  ),
     ('TPE',
             Year         City          Sport     Discipline             Athlete  \
      10006  1960         Rome      Athletics      Athletics   YANG, Chuan-Kwang   
      11945  1968       Mexico      Athletics      Athletics          CHI, Cheng   
      17973  1984  Los Angeles  Weightlifting  Weightlifting       TSAI, Wen-Yee   
      20091  1992    Barcelona       Baseball       Baseball  CHANG, Cheng-Hsien   
      20092  1992    Barcelona       Baseball       Baseball    CHANG, Wen-Chung   
      20093  1992    Barcelona       Baseball       Baseball    CHANG, Yaw-Teing   
      20094  1992    Barcelona       Baseball       Baseball      CHEN, Chi-Hsin   
      20095  1992    Barcelona       Baseball       Baseball      CHEN, Wei-Chen   
      20096  1992    Barcelona       Baseball       Baseball   CHIANG, Tai-Chuan   
      20097  1992    Barcelona       Baseball       Baseball     HUANG, Chung-Yi   
      20098  1992    Barcelona       Baseball       Baseball       HUANG, Wen-Po   
      20099  1992    Barcelona       Baseball       Baseball      JONG, Yeu-Jeng   
      20100  1992    Barcelona       Baseball       Baseball       KU, Kuo-Chian   
      20101  1992    Barcelona       Baseball       Baseball   KUO LEE, Chien-Fu   
      20102  1992    Barcelona       Baseball       Baseball   LIAO, Ming-Hsiung   
      20103  1992    Barcelona       Baseball       Baseball     LIN, Chao-Huang   
      20104  1992    Barcelona       Baseball       Baseball        LIN, Kun-Han   
      20105  1992    Barcelona       Baseball       Baseball       LO, Chen-Jung   
      20106  1992    Barcelona       Baseball       Baseball       LO, Kuo-Chong   
      20107  1992    Barcelona       Baseball       Baseball       PAI, Kun-Hong   
      20108  1992    Barcelona       Baseball       Baseball     TSAI, Ming-Hung   
      20109  1992    Barcelona       Baseball       Baseball    WANG, Kuang-Shih   
      20110  1992    Barcelona       Baseball       Baseball       WU, Shih-Hsih   
      22968  1996      Atlanta   Table Tennis   Table Tennis          CHEN, Jing   
      24948  2000       Sydney   Table Tennis   Table Tennis          CHEN, Jing   
      24951  2000       Sydney      Taekwondo      Taekwondo         CHI, Shu-Ju   
      24954  2000       Sydney      Taekwondo      Taekwondo  HUANG, Chih Hsiung   
      25097  2000       Sydney  Weightlifting  Weightlifting       LI, Feng-Ying   
      25116  2000       Sydney  Weightlifting  Weightlifting        KUO, Yi-Hang   
      25520  2004       Athens        Archery        Archery      CHEN, Szu Yuan   
      25521  2004       Athens        Archery        Archery     LIU, Ming Huang   
      25522  2004       Athens        Archery        Archery    WANG, Cheng Pang   
      25523  2004       Athens        Archery        Archery         CHEN, Li Ju   
      25524  2004       Athens        Archery        Archery          WU, Hui Ju   
      25525  2004       Athens        Archery        Archery       YUAN, Shu Chi   
      26947  2004       Athens      Taekwondo      Taekwondo     CHEN, Shih Hsin   
      26950  2004       Athens      Taekwondo      Taekwondo         CHU, Mu Yen   
      26966  2004       Athens      Taekwondo      Taekwondo  HUANG, Chih Hsiung   
      28964  2008      Beijing      Taekwondo      Taekwondo         CHU, Mu-Yen   
      28984  2008      Beijing      Taekwondo      Taekwondo        SUNG, Yu-Chi   
      29112  2008      Beijing  Weightlifting  Weightlifting      CHEN, Wei-Ling   
      29124  2008      Beijing  Weightlifting  Weightlifting        LU, Ying-Chi   
      30921  2012       London      Taekwondo      Taekwondo     TSENG, Li-Cheng   
      31060  2012       London  Weightlifting  Weightlifting      HSU, Shu-Ching   
      
            Country Gender                             Event   Medal  
      10006     TPE    Men                         Decathlon  Silver  
      11945     TPE  Women                       80M Hurdles  Bronze  
      17973     TPE    Men  56 - 60KG, Total (Featherweight)  Bronze  
      20091     TPE    Men                          Baseball  Silver  
      20092     TPE    Men                          Baseball  Silver  
      20093     TPE    Men                          Baseball  Silver  
      20094     TPE    Men                          Baseball  Silver  
      20095     TPE    Men                          Baseball  Silver  
      20096     TPE    Men                          Baseball  Silver  
      20097     TPE    Men                          Baseball  Silver  
      20098     TPE    Men                          Baseball  Silver  
      20099     TPE    Men                          Baseball  Silver  
      20100     TPE    Men                          Baseball  Silver  
      20101     TPE    Men                          Baseball  Silver  
      20102     TPE    Men                          Baseball  Silver  
      20103     TPE    Men                          Baseball  Silver  
      20104     TPE    Men                          Baseball  Silver  
      20105     TPE    Men                          Baseball  Silver  
      20106     TPE    Men                          Baseball  Silver  
      20107     TPE    Men                          Baseball  Silver  
      20108     TPE    Men                          Baseball  Silver  
      20109     TPE    Men                          Baseball  Silver  
      20110     TPE    Men                          Baseball  Silver  
      22968     TPE  Women                           Singles  Silver  
      24948     TPE  Women                           Singles  Bronze  
      24951     TPE  Women                           - 49 KG  Bronze  
      24954     TPE    Men                           - 58 KG  Bronze  
      25097     TPE  Women                              53KG  Silver  
      25116     TPE  Women                              75KG  Bronze  
      25520     TPE    Men   Team (Fita Olympic Round - 70M)  Silver  
      25521     TPE    Men   Team (Fita Olympic Round - 70M)  Silver  
      25522     TPE    Men   Team (Fita Olympic Round - 70M)  Silver  
      25523     TPE  Women   Team (Fita Olympic Round - 70M)  Bronze  
      25524     TPE  Women   Team (Fita Olympic Round - 70M)  Bronze  
      25525     TPE  Women   Team (Fita Olympic Round - 70M)  Bronze  
      26947     TPE  Women                           - 49 KG    Gold  
      26950     TPE    Men                           - 58 KG    Gold  
      26966     TPE    Men                        58 - 68 KG  Silver  
      28964     TPE    Men                           - 58 KG  Bronze  
      28984     TPE    Men                        58 - 68 KG  Bronze  
      29112     TPE  Women                              48KG  Bronze  
      29124     TPE  Women                              63KG  Bronze  
      30921     TPE  Women                        49 - 57 KG  Bronze  
      31060     TPE  Women                              53KG    Gold  ),
     ('TRI',
             Year      City          Sport     Discipline                  Athlete  \
      7960   1948    London  Weightlifting  Weightlifting  WILKES, Rodney Adolphus   
      8844   1952  Helsinki  Weightlifting  Weightlifting  WILKES, Rodney Adolphus   
      8856   1952  Helsinki  Weightlifting  Weightlifting          KILGOUR, Lennox   
      10834  1964     Tokyo      Athletics      Athletics           ROBERTS, Edwin   
      10848  1964     Tokyo      Athletics      Athletics  MOTTLEY, Wendell Adrian   
      10879  1964     Tokyo      Athletics      Athletics       BERNARD, Kent Bede   
      10880  1964     Tokyo      Athletics      Athletics  MOTTLEY, Wendell Adrian   
      10881  1964     Tokyo      Athletics      Athletics           ROBERTS, Edwin   
      10882  1964     Tokyo      Athletics      Athletics           SKINNER, Edwin   
      14069  1976  Montreal      Athletics      Athletics         CRAWFORD, Hasely   
      21597  1996   Atlanta      Athletics      Athletics              BOLDON, Ato   
      21615  1996   Atlanta      Athletics      Athletics              BOLDON, Ato   
      23522  2000    Sydney      Athletics      Athletics              BOLDON, Ato   
      23538  2000    Sydney      Athletics      Athletics              BOLDON, Ato   
      25264  2004    Athens       Aquatics       Swimming           BOVELL, George   
      27553  2008   Beijing      Athletics      Athletics        THOMPSON, Richard   
      27607  2008   Beijing      Athletics      Athletics          BLEDMAN, Keston   
      27608  2008   Beijing      Athletics      Athletics              BURNS, Marc   
      27609  2008   Beijing      Athletics      Athletics      CALLENDER, Emmanuel   
      27610  2008   Beijing      Athletics      Athletics        THOMPSON, Richard   
      
            Country Gender                                    Event   Medal  
      7960      TRI    Men         56 - 60KG, Total (Featherweight)  Silver  
      8844      TRI    Men         56 - 60KG, Total (Featherweight)  Bronze  
      8856      TRI    Men  82.5 - 90KG, Total (Middle-Heavyweight)  Bronze  
      10834     TRI    Men                                     200M  Bronze  
      10848     TRI    Men                                     400M  Silver  
      10879     TRI    Men                             4X400M Relay  Bronze  
      10880     TRI    Men                             4X400M Relay  Bronze  
      10881     TRI    Men                             4X400M Relay  Bronze  
      10882     TRI    Men                             4X400M Relay  Bronze  
      14069     TRI    Men                                     100M    Gold  
      21597     TRI    Men                                     100M  Bronze  
      21615     TRI    Men                                     200M  Bronze  
      23522     TRI    Men                                     100M  Silver  
      23538     TRI    Men                                     200M  Bronze  
      25264     TRI    Men                   200M Individual Medley  Bronze  
      27553     TRI    Men                                     100M  Silver  
      27607     TRI    Men                             4X100M Relay  Silver  
      27608     TRI    Men                             4X100M Relay  Silver  
      27609     TRI    Men                             4X100M Relay  Silver  
      27610     TRI    Men                             4X100M Relay  Silver  ),
     ('TTO',
             Year    City      Sport Discipline              Athlete Country Gender  \
      29626  2012  London  Athletics  Athletics      GORDON, Lalonde     TTO    Men   
      29641  2012  London  Athletics  Athletics      BLEDMAN, Keston     TTO    Men   
      29642  2012  London  Athletics  Athletics          BURNS, Marc     TTO    Men   
      29643  2012  London  Athletics  Athletics  CALLENDER, Emmanuel     TTO    Men   
      29644  2012  London  Athletics  Athletics    THOMPSON, Richard     TTO    Men   
      29674  2012  London  Athletics  Athletics   ALLEYNE-FORTE, Ade     TTO    Men   
      29675  2012  London  Athletics  Athletics      GORDON, Lalonde     TTO    Men   
      29676  2012  London  Athletics  Athletics        LENDORE, Deon     TTO    Men   
      29677  2012  London  Athletics  Athletics      SOLOMON, Jarrin     TTO    Men   
      29736  2012  London  Athletics  Athletics     WALCOTT, Keshorn     TTO    Men   
      
                     Event   Medal  
      29626           400M  Bronze  
      29641   4X100M Relay  Silver  
      29642   4X100M Relay  Silver  
      29643   4X100M Relay  Silver  
      29644   4X100M Relay  Silver  
      29674   4X400M Relay  Bronze  
      29675   4X400M Relay  Bronze  
      29676   4X400M Relay  Bronze  
      29677   4X400M Relay  Bronze  
      29736  Javelin Throw    Gold  ),
     ('TUN',
             Year     City      Sport         Discipline            Athlete Country  \
      10821  1964    Tokyo  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      11011  1964    Tokyo     Boxing             Boxing      GALHIA, Habib     TUN   
      11861  1968   Mexico  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      11934  1968   Mexico  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      12990  1972   Munich  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      21948  1996  Atlanta     Boxing             Boxing    MISSAOUI, Fathi     TUN   
      27237  2008  Beijing   Aquatics           Swimming  MELLOULI, Oussama     TUN   
      29252  2012   London   Aquatics  Marathon swimming  MELLOULI, Oussama     TUN   
      29284  2012   London   Aquatics           Swimming  MELLOULI, Oussama     TUN   
      29621  2012   London  Athletics          Athletics     GHRIBI, Habiba     TUN   
      
            Gender                             Event   Medal  
      10821    Men                            10000M  Silver  
      11011    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      11861    Men                            10000M  Bronze  
      11934    Men                             5000M    Gold  
      12990    Men                             5000M  Silver  
      21948    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      27237    Men                   1500M Freestyle    Gold  
      29252    Men                              10KM    Gold  
      29284    Men                   1500M Freestyle  Bronze  
      29621  Women                     3000M Steeple    Gold  ),
     ('TUR',
             Year     City      Sport           Discipline          Athlete Country  \
      7177   1936   Berlin  Wrestling      Wrestling Free.   KIREÇÇI, Ahmet     TUR   
      7190   1936   Berlin  Wrestling      Wrestling Gre-R     ERKAN, Yasar     TUR   
      7418   1948   London  Athletics            Athletics    SARIALP, Ruhi     TUR   
      7972   1948   London  Wrestling      Wrestling Free.   BALAMIR, Halit     TUR   
      7977   1948   London  Wrestling      Wrestling Free.      AKAR, Nazuh     TUR   
      ...     ...      ...        ...                  ...              ...     ...   
      29205  2008  Beijing  Wrestling      Wrestling Gre-R    AVLUCA, Nazmi     TUR   
      29604  2012   London  Athletics            Athletics     BULUT, Gamze     TUR   
      30923  2012   London  Taekwondo            Taekwondo       TATAR, Nur     TUR   
      30926  2012   London  Taekwondo            Taekwondo  TAZEGUL, Servet     TUR   
      31140  2012   London  Wrestling  Wrestling Freestyle    KAYAALP, Riza     TUR   
      
            Gender                      Event   Medal  
      7177     Men   72 - 79KG (Middleweight)  Bronze  
      7190     Men  56 - 61KG (Featherweight)    Gold  
      7418     Men                Triple Jump  Bronze  
      7972     Men         - 52KG (Flyweight)  Silver  
      7977     Men   52 - 57KG (Bantamweight)    Gold  
      ...      ...                        ...     ...  
      29205    Men                  74 - 84KG  Bronze  
      29604  Women                      1500M  Silver  
      30923  Women                 57 - 67 KG  Silver  
      30926    Men                 58 - 68 KG    Gold  
      31140    Men                  Wg 120 KG  Bronze  
      
      [86 rows x 9 columns]),
     ('UAE',
             Year    City     Sport Discipline                  Athlete Country  \
      26869  2004  Athens  Shooting   Shooting  ALMAKTOUM, Shaikh Ahmed     UAE   
      
            Gender                      Event Medal  
      26869    Men  Double Trap (150 Targets)  Gold  ),
     ('UGA',
             Year     City      Sport Discipline             Athlete Country Gender  \
      12041  1968   Mexico     Boxing     Boxing       RWABDOGO, Leo     UGA    Men   
      12047  1968   Mexico     Boxing     Boxing   MUKWANGA, Eridadi     UGA    Men   
      12938  1972   Munich  Athletics  Athletics      AKII-BUA, John     UGA    Men   
      13095  1972   Munich     Boxing     Boxing       RWABDOGO, Leo     UGA    Men   
      15623  1980   Moscow     Boxing     Boxing        MUGABI, John     UGA    Men   
      21627  1996  Atlanta  Athletics  Athletics       KAMOGA, Davis     UGA    Men   
      29748  2012   London  Athletics  Athletics  KIPROTICH, Stephen     UGA    Men   
      
                                  Event   Medal  
      12041       48 - 51KG (Flyweight)  Bronze  
      12047    51 - 54KG (Bantamweight)  Silver  
      12938                400M Hurdles    Gold  
      13095       48 - 51KG (Flyweight)  Silver  
      15623  63.5 - 67KG (Welterweight)  Silver  
      21627                        400M  Bronze  
      29748                    Marathon    Gold  ),
     ('UKR',
             Year     City          Sport           Discipline              Athlete  \
      21567  1996  Atlanta        Archery              Archery    SADOVNYCHA, Olena   
      21723  1996  Atlanta      Athletics            Athletics      KRYKUN, Oleksiy   
      21732  1996  Atlanta      Athletics            Athletics       BABAKOVA, Inha   
      21756  1996  Atlanta      Athletics            Athletics    BAGACH, Oleksandr   
      21766  1996  Atlanta      Athletics            Athletics      KRAVETS, Inessa   
      ...     ...      ...            ...                  ...                  ...   
      30838  2012   London       Shooting             Shooting     KOSTEVYCH, Olena   
      30847  2012   London       Shooting             Shooting     KOSTEVYCH, Olena   
      31054  2012   London  Weightlifting        Weightlifting   TOROKHTIY, Oleksiy   
      31062  2012   London  Weightlifting        Weightlifting      PARATOVA, Iulia   
      31134  2012   London      Wrestling  Wrestling Freestyle  ANDRIITSEV, Valerii   
      
            Country Gender                                  Event   Medal  
      21567     UKR  Women  Individual (Fita Olympic Round - 70M)  Bronze  
      21723     UKR    Men                           Hammer Throw  Bronze  
      21732     UKR  Women                              High Jump  Bronze  
      21756     UKR    Men                               Shot Put  Bronze  
      21766     UKR  Women                            Triple Jump    Gold  
      ...       ...    ...                                    ...     ...  
      30838     UKR  Women                         10M Air Pistol  Bronze  
      30847     UKR  Women                             25M Pistol  Bronze  
      31054     UKR    Men                                  105KG    Gold  
      31062     UKR  Women                                   53KG  Bronze  
      31134     UKR    Men                               Wf 96 KG  Silver  
      
      [173 rows x 9 columns]),
     ('URS',
             Year      City      Sport       Discipline  \
      8114   1952  Helsinki  Athletics        Athletics   
      8117   1952  Helsinki  Athletics        Athletics   
      8135   1952  Helsinki  Athletics        Athletics   
      8140   1952  Helsinki  Athletics        Athletics   
      8146   1952  Helsinki  Athletics        Athletics   
      ...     ...       ...        ...              ...   
      19580  1988     Seoul  Wrestling  Wrestling Gre-R   
      19583  1988     Seoul  Wrestling  Wrestling Gre-R   
      19587  1988     Seoul  Wrestling  Wrestling Gre-R   
      19589  1988     Seoul  Wrestling  Wrestling Gre-R   
      19591  1988     Seoul  Wrestling  Wrestling Gre-R   
      
                                    Athlete Country Gender  \
      8114             ANUFRIYEV, Aleksandr     URS    Men   
      8117                      JUNK, Bruno     URS    Men   
      8135   KHNYKINA-DVALISHVILI, Nadezhda     URS  Women   
      8140              KAZANTSEV, Vladimir     URS    Men   
      8146                     LITUEV, Yuri     URS    Men   
      ...                               ...     ...    ...   
      19580             MADZHIDOV, Kamandar     URS    Men   
      19583             DJULFALAKIAN, Levon     URS    Men   
      19587             TURLYKHANOV, Daulet     URS    Men   
      19589            MAMIASHVILI, Mikhail     URS    Men   
      19591                 POPOV, Vladimir     URS    Men   
      
                                     Event   Medal  
      8114                          10000M  Bronze  
      8117                     10000M Walk  Bronze  
      8135                            200M  Bronze  
      8140              3000M Steeplechase  Silver  
      8146                    400M Hurdles  Silver  
      ...                              ...     ...  
      19580      57 - 62KG (Featherweight)    Gold  
      19583        62 - 68KG (Lightweight)    Gold  
      19587       68 - 74KG (Welterweight)  Silver  
      19589       74 - 82KG (Middleweight)    Gold  
      19591  82 - 90KG (Light-Heavyweight)  Bronze  
      
      [2049 rows x 9 columns]),
     ('URU',
             Year                   City       Sport     Discipline  \
      4542   1924                  Paris    Football       Football   
      4543   1924                  Paris    Football       Football   
      4544   1924                  Paris    Football       Football   
      4545   1924                  Paris    Football       Football   
      4546   1924                  Paris    Football       Football   
      ...     ...                    ...         ...            ...   
      9141   1956  Melbourne / Stockholm  Basketball     Basketball   
      9142   1956  Melbourne / Stockholm  Basketball     Basketball   
      9143   1956  Melbourne / Stockholm  Basketball     Basketball   
      10999  1964                  Tokyo      Boxing         Boxing   
      24042  2000                 Sydney     Cycling  Cycling Track   
      
                           Athlete Country Gender                     Event   Medal  
      4542           ANDRADE, José     URU    Men                  Football    Gold  
      4543           ARISPE, Pedro     URU    Men                  Football    Gold  
      4544             CASELLA, P.     URU    Men                  Football    Gold  
      4545              CEA, Pedro     URU    Men                  Football    Gold  
      4546           CHIAPPARA, L.     URU    Men                  Football    Gold  
      ...                      ...     ...    ...                       ...     ...  
      9141           MOGLIA, Oscar     URU    Men                Basketball  Bronze  
      9142        OLASCOAGA, Ariel     URU    Men                Basketball  Bronze  
      9143       SCARON, Milton A.     URU    Men                Basketball  Bronze  
      10999  RODRIGUEZ, Washington     URU    Men  51 - 54KG (Bantamweight)  Bronze  
      24042  WYNANTS, Milton Ariel     URU    Men               Points Race  Silver  
      
      [76 rows x 9 columns]),
     ('USA',
             Year    City       Sport           Discipline  \
      11     1896  Athens   Athletics            Athletics   
      13     1896  Athens   Athletics            Athletics   
      15     1896  Athens   Athletics            Athletics   
      19     1896  Athens   Athletics            Athletics   
      21     1896  Athens   Athletics            Athletics   
      ...     ...     ...         ...                  ...   
      31035  2012  London  Volleyball           Volleyball   
      31099  2012  London   Wrestling  Wrestling Freestyle   
      31112  2012  London   Wrestling  Wrestling Freestyle   
      31125  2012  London   Wrestling  Wrestling Freestyle   
      31133  2012  London   Wrestling  Wrestling Freestyle   
      
                                   Athlete Country Gender         Event   Medal  
      11                     LANE, Francis     USA    Men          100M  Bronze  
      13                     BURKE, Thomas     USA    Men          100M    Gold  
      15                    CURTIS, Thomas     USA    Men  110M Hurdles    Gold  
      19                     BLAKE, Arthur     USA    Men         1500M  Silver  
      21                     BURKE, Thomas     USA    Men          400M    Gold  
      ...                              ...     ...    ...           ...     ...  
      31035                     TOM, Logan     USA  Women    Volleyball  Silver  
      31099  CHUN, Clarissa Kyoko Mei Ling     USA  Women      Wf 48 KG  Bronze  
      31112                 SCOTT, Coleman     USA    Men      Wf 60 KG  Bronze  
      31125       BURROUGHS, Jordan Ernest     USA    Men      Wf 74 KG    Gold  
      31133          VARNER, Jacob Stephen     USA    Men      Wf 96 KG    Gold  
      
      [4585 rows x 9 columns]),
     ('UZB',
             Year     City       Sport           Discipline  \
      21957  1996  Atlanta      Boxing               Boxing   
      22661  1996  Atlanta        Judo                 Judo   
      23870  2000   Sydney      Boxing               Boxing   
      23892  2000   Sydney      Boxing               Boxing   
      23907  2000   Sydney      Boxing               Boxing   
      25151  2000   Sydney   Wrestling      Wrestling Free.   
      25893  2004   Athens      Boxing               Boxing   
      25916  2004   Athens      Boxing               Boxing   
      27149  2004   Athens   Wrestling      Wrestling Free.   
      27151  2004   Athens   Wrestling      Wrestling Free.   
      27163  2004   Athens   Wrestling      Wrestling Gre-R   
      28322  2008  Beijing  Gymnastics          Artistic G.   
      28400  2008  Beijing  Gymnastics           Trampoline   
      28591  2008  Beijing        Judo                 Judo   
      28597  2008  Beijing        Judo                 Judo   
      29176  2008  Beijing   Wrestling      Wrestling Free.   
      29187  2008  Beijing   Wrestling      Wrestling Free.   
      29906  2012   London      Boxing               Boxing   
      30586  2012   London        Judo                 Judo   
      31093  2012   London   Wrestling  Wrestling Freestyle   
      
                                Athlete Country Gender  \
      21957            TULAGANOV, Karim     UZB    Men   
      22661           BAGDASAROV, Armen     UZB    Men   
      23870              SAIDOV, Rustam     UZB    Men   
      23892  ABDOOLLAYEV, Mahammatkodir     UZB    Men   
      23907            MIHAYLOV, Sergey     UZB    Men   
      25151             TAYMAZOV, Artur     UZB    Men   
      25893       SOOLTONOV, Bahodirjon     UZB    Men   
      25916          HAYDAROV, Utkirbek     UZB    Men   
      27149          IBRAGIMOV, Magomed     UZB    Men   
      27151             TAYMAZOV, Artur     UZB    Men   
      27163    DOKTURISHIVILI, Alexandr     UZB    Men   
      28322                FOKIN, Anton     UZB    Men   
      28400           KHILKO, Ekaterina     UZB  Women   
      28591             SOBIROV, Rishod     UZB    Men   
      28597           TANGRIEV, Abdullo     UZB    Men   
      29176              TIGIEV, Soslan     UZB    Men   
      29187             TAYMAZOV, Artur     UZB    Men   
      29906                ATOEV, Abbos     UZB    Men   
      30586             SOBIROV, Rishod     UZB    Men   
      31093             TAYMAZOV, Artur     UZB    Men   
      
                                        Event   Medal  
      21957    67 - 71KG (Light-Middleweight)  Bronze  
      22661          81 - 90KG (Middleweight)  Silver  
      23870        + 91KG (Super Heavyweight)  Bronze  
      23892  60 - 63.5KG (Light-Welterweight)    Gold  
      23907     75 - 81KG (Light-Heavyweight)  Bronze  
      25151                        97 - 130KG  Silver  
      25893          51 - 54KG (Bantamweight)  Bronze  
      25916     75 - 81KG (Light-Heavyweight)  Bronze  
      27149                         84 - 96KG  Silver  
      27151                        96 - 120KG    Gold  
      27163                         66 - 74KG    Gold  
      28322                     Parallel Bars  Bronze  
      28400                        Individual  Bronze  
      28591                           - 60 KG  Bronze  
      28597             + 100KG (Heavyweight)  Silver  
      29176                         66 - 74KG  Silver  
      29187                        96 - 120KG    Gold  
      29906                        69 - 75 KG  Bronze  
      30586                           - 60 KG  Bronze  
      31093                          Wf 120KG    Gold  ),
     ('VEN',
             Year         City          Sport     Discipline  \
      8237   1952     Helsinki      Athletics      Athletics   
      10599  1960         Rome       Shooting       Shooting   
      12034  1968       Mexico         Boxing         Boxing   
      14315  1976     Montreal         Boxing         Boxing   
      15607  1980       Moscow         Boxing         Boxing   
      16643  1984  Los Angeles       Aquatics       Swimming   
      17023  1984  Los Angeles         Boxing         Boxing   
      17040  1984  Los Angeles         Boxing         Boxing   
      26952  2004       Athens      Taekwondo      Taekwondo   
      27096  2004       Athens  Weightlifting  Weightlifting   
      28960  2008      Beijing      Taekwondo      Taekwondo   
      30126  2012       London        Fencing        Fencing   
      
                                  Athlete Country Gender  \
      8237              DEVONISH, Arnaldo     VEN    Men   
      10599  FORCELLA PELLICCIONI, Enrico     VEN    Men   
      12034          RODRIGUEZ, Francisco     VEN    Men   
      14315           GAMARRO, Pedro José     VEN    Men   
      15607        PINANGO, Bernardo Jose     VEN    Men   
      16643  VIDAL CASTRO, Rafael Antonio     VEN    Men   
      17023       BOLIVAR, Jose Marcelino     VEN    Men   
      17040           CATARI PERAZA, Omar     VEN    Men   
      26952              CARMONA, Adriana     VEN  Women   
      27096            RUBIO, Israel Jose     VEN    Men   
      28960       CONTRERAS RIVERO, Dalia     VEN  Women   
      30126      LIMARDO GASCON, Ruben D.     VEN    Men   
      
                                  Event   Medal  
      8237                  Triple Jump  Bronze  
      10599  50M Rifle Prone (60 Shots)  Bronze  
      12034    - 48KG (Light-Flyweight)    Gold  
      14315  63.5 - 67KG (Welterweight)  Silver  
      15607    51 - 54KG (Bantamweight)  Silver  
      16643              200M Butterfly  Bronze  
      17023    - 48KG (Light-Flyweight)  Bronze  
      17040   54 - 57KG (Featherweight)  Bronze  
      26952                     + 67 KG  Bronze  
      27096                        62KG  Bronze  
      28960                     - 49 KG  Bronze  
      30126             Épée Individual    Gold  ),
     ('VIE',
             Year     City          Sport     Discipline          Athlete Country  \
      24965  2000   Sydney      Taekwondo      Taekwondo  TRAN, Hieu Ngan     VIE   
      29102  2008  Beijing  Weightlifting  Weightlifting  HOANG, Anh Tuan     VIE   
      
            Gender                         Event   Medal  
      24965  Women                    49 - 57 KG  Silver  
      29102    Men  - 56KG, Total (Bantamweight)  Silver  ),
     ('YUG',
             Year       City       Sport   Discipline           Athlete Country  \
      4587   1924      Paris  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      4590   1924      Paris  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      5415   1928  Amsterdam  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      5420   1928  Amsterdam  Gymnastics  Artistic G.   PRIMOZIC, Josip     YUG   
      5425   1928  Amsterdam  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      ...     ...        ...         ...          ...               ...     ...   
      25030  2000     Sydney  Volleyball   Volleyball       MIJIC, Vasa     YUG   
      25031  2000     Sydney  Volleyball   Volleyball   MILJKOVIC, Ivan     YUG   
      25032  2000     Sydney  Volleyball   Volleyball  PETKOVIC, Veljko     YUG   
      25033  2000     Sydney  Volleyball   Volleyball    VUJEVIC, Goran     YUG   
      25034  2000     Sydney  Volleyball   Volleyball   VUSUROVIC, Igor     YUG   
      
            Gender                 Event   Medal  
      4587     Men        Horizontal Bar    Gold  
      4590     Men  Individual All-Round    Gold  
      5415     Men  Individual All-Round  Bronze  
      5420     Men         Parallel Bars  Silver  
      5425     Men                 Rings    Gold  
      ...      ...                   ...     ...  
      25030    Men            Volleyball    Gold  
      25031    Men            Volleyball    Gold  
      25032    Men            Volleyball    Gold  
      25033    Men            Volleyball    Gold  
      25034    Men            Volleyball    Gold  
      
      [435 rows x 9 columns]),
     ('ZAM',
             Year         City      Sport Discipline         Athlete Country Gender  \
      17024  1984  Los Angeles     Boxing     Boxing    MWILA, Keith     ZAM    Men   
      21635  1996      Atlanta  Athletics  Athletics  MATETE, Samuel     ZAM    Men   
      
                                Event   Medal  
      17024  - 48KG (Light-Flyweight)  Bronze  
      21635              400M Hurdles  Silver  ),
     ('ZIM',
             Year     City     Sport Discipline                   Athlete Country  \
      16135  1980   Moscow    Hockey     Hockey    BOXHALL, Arlene Nadine     ZIM   
      16136  1980   Moscow    Hockey     Hockey   CHASE, Elizabeth Muriel     ZIM   
      16137  1980   Moscow    Hockey     Hockey             CHICK, Sandra     ZIM   
      16138  1980   Moscow    Hockey     Hockey  COWLEY, Gillian Margaret     ZIM   
      16139  1980   Moscow    Hockey     Hockey     DAVIES, Patricia Joan     ZIM   
      16140  1980   Moscow    Hockey     Hockey            ENGLISH, Sarah     ZIM   
      16141  1980   Moscow    Hockey     Hockey      GEORGE, Maureen Jean     ZIM   
      16142  1980   Moscow    Hockey     Hockey   GRANT, Ann Marry Gwynne     ZIM   
      16143  1980   Moscow    Hockey     Hockey            HUGGETT, Susan     ZIM   
      16144  1980   Moscow    Hockey     Hockey   MCKILLOP, Patricia Jean     ZIM   
      16145  1980   Moscow    Hockey     Hockey     PHILLIPS, Brenda Joan     ZIM   
      16146  1980   Moscow    Hockey     Hockey       PRINSLOO, Christine     ZIM   
      16147  1980   Moscow    Hockey     Hockey          ROBERTSON, Sonia     ZIM   
      16148  1980   Moscow    Hockey     Hockey    STEWART, Anthea Doreen     ZIM   
      16149  1980   Moscow    Hockey     Hockey               VOLK, Helen     ZIM   
      16150  1980   Moscow    Hockey     Hockey    WATSON, Linda Margaret     ZIM   
      25217  2004   Athens  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      25244  2004   Athens  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      25267  2004   Athens  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27216  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27243  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27268  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27280  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      
            Gender                   Event   Medal  
      16135  Women                  Hockey    Gold  
      16136  Women                  Hockey    Gold  
      16137  Women                  Hockey    Gold  
      16138  Women                  Hockey    Gold  
      16139  Women                  Hockey    Gold  
      16140  Women                  Hockey    Gold  
      16141  Women                  Hockey    Gold  
      16142  Women                  Hockey    Gold  
      16143  Women                  Hockey    Gold  
      16144  Women                  Hockey    Gold  
      16145  Women                  Hockey    Gold  
      16146  Women                  Hockey    Gold  
      16147  Women                  Hockey    Gold  
      16148  Women                  Hockey    Gold  
      16149  Women                  Hockey    Gold  
      16150  Women                  Hockey    Gold  
      25217  Women         100M Backstroke  Silver  
      25244  Women         200M Backstroke    Gold  
      25267  Women  200M Individual Medley  Bronze  
      27216  Women         100M Backstroke  Silver  
      27243  Women         200M Backstroke    Gold  
      27268  Women  200M Individual Medley  Silver  
      27280  Women  400M Individual Medley  Silver  ),
     ('ZZX',
           Year      City       Sport  Discipline                           Athlete  \
      132  1896    Athens      Tennis      Tennis                      FLACK, Edwin   
      133  1896    Athens      Tennis      Tennis          ROBERTSON, George Stuart   
      134  1896    Athens      Tennis      Tennis                      BOLAND, John   
      135  1896    Athens      Tennis      Tennis                  TRAUN, Friedrich   
      136  1896    Athens      Tennis      Tennis              KASDAGLIS, Dionysios   
      137  1896    Athens      Tennis      Tennis          PETROKOKKINOS, Demetrios   
      257  1900     Paris   Athletics   Athletics                  BENNETT, Charles   
      258  1900     Paris   Athletics   Athletics                      RIMMER, John   
      259  1900     Paris   Athletics   Athletics                  ROBINSON, Sidney   
      260  1900     Paris   Athletics   Athletics                   ROWLEY, Stanley   
      261  1900     Paris   Athletics   Athletics                     TYSOE, Alfred   
      422  1900     Paris        Polo        Polo                     BOUSSOD, Jean   
      423  1900     Paris        Polo        Polo            DUC DE BISACCIA, Louis   
      424  1900     Paris        Polo        Polo              FAUQUET LEMAITRE, A.   
      425  1900     Paris        Polo        Polo              RAOUL-DUVAL, Maurice   
      426  1900     Paris        Polo        Polo                      DALY, Dennis   
      427  1900     Paris        Polo        Polo             KEENE, Foxhall Parker   
      428  1900     Paris        Polo        Polo                 MACKEY, Frank Jay   
      429  1900     Paris        Polo        Polo                 RAWLINSON, Alfred   
      430  1900     Paris        Polo        Polo          BUCKMASTER, Walter Selby   
      431  1900     Paris        Polo        Polo  COMTE DE MADRE, José Pierre M.J.   
      432  1900     Paris        Polo        Polo        FREAKE, Frederick Maitland   
      433  1900     Paris        Polo        Polo           MCCREERY, Walter Adolph   
      493  1900     Paris      Rowing      Rowing          BRANDT, Francois Antoine   
      494  1900     Paris      Rowing      Rowing      BROCKMANN, Hermanus Gerardus   
      495  1900     Paris      Rowing      Rowing                     KLEIN, Roelof   
      633  1900     Paris      Tennis      Tennis      DE GARMENDIA, Basil Spalding   
      634  1900     Paris      Tennis      Tennis                      DECUGIS, Max   
      635  1900     Paris      Tennis      Tennis            DOHERTY, Hugh Lawrence   
      636  1900     Paris      Tennis      Tennis              WARDEN, Archibald A.   
      638  1900     Paris      Tennis      Tennis          MAHONY, Harold Sergerson   
      639  1900     Paris      Tennis      Tennis                     JONES, Marion   
      640  1900     Paris      Tennis      Tennis                 ROSENBAUM, Hedwig   
      642  1900     Paris      Tennis      Tennis                   PREVOST, Hélène   
      651  1900     Paris  Tug of War  Tug of War                      AABYE, Edgar   
      652  1900     Paris  Tug of War  Tug of War                   NILSSON, August   
      653  1900     Paris  Tug of War  Tug of War                    SCHMIDT, Eugen   
      654  1900     Paris  Tug of War  Tug of War                SÖDERSTRÖM, Gustaf   
      655  1900     Paris  Tug of War  Tug of War                STAAF, Karl Gustav   
      656  1900     Paris  Tug of War  Tug of War                 WINCKLER, Charles   
      765  1904  St Louis   Athletics   Athletics                     CORAY, Albert   
      766  1904  St Louis   Athletics   Athletics                     HATCH, Sidney   
      767  1904  St Louis   Athletics   Athletics                      HEARN, Lacey   
      768  1904  St Louis   Athletics   Athletics                  LIGHTBODY, James   
      769  1904  St Louis   Athletics   Athletics             VERNER, William Frank   
      864  1904  St Louis     Fencing     Fencing                      DIAZ, Manuel   
      865  1904  St Louis     Fencing     Fencing                      FONST, Ramon   
      866  1904  St Louis     Fencing     Fencing            VAN ZO POST, Albertson   
      
          Country Gender                                Event   Medal  
      132     ZZX    Men                              Doubles  Bronze  
      133     ZZX    Men                              Doubles  Bronze  
      134     ZZX    Men                              Doubles    Gold  
      135     ZZX    Men                              Doubles    Gold  
      136     ZZX    Men                              Doubles  Silver  
      137     ZZX    Men                              Doubles  Silver  
      257     ZZX    Men                           5000M Team    Gold  
      258     ZZX    Men                           5000M Team    Gold  
      259     ZZX    Men                           5000M Team    Gold  
      260     ZZX    Men                           5000M Team    Gold  
      261     ZZX    Men                           5000M Team    Gold  
      422     ZZX    Men                                 Polo  Bronze  
      423     ZZX    Men                                 Polo  Bronze  
      424     ZZX    Men                                 Polo  Bronze  
      425     ZZX    Men                                 Polo  Bronze  
      426     ZZX    Men                                 Polo    Gold  
      427     ZZX    Men                                 Polo    Gold  
      428     ZZX    Men                                 Polo    Gold  
      429     ZZX    Men                                 Polo    Gold  
      430     ZZX    Men                                 Polo  Silver  
      431     ZZX    Men                                 Polo  Silver  
      432     ZZX    Men                                 Polo  Silver  
      433     ZZX    Men                                 Polo  Silver  
      493     ZZX    Men  Pair-Oared Shell With Coxswain (2+)    Gold  
      494     ZZX    Men  Pair-Oared Shell With Coxswain (2+)    Gold  
      495     ZZX    Men  Pair-Oared Shell With Coxswain (2+)    Gold  
      633     ZZX    Men                              Doubles  Silver  
      634     ZZX    Men                              Doubles  Silver  
      635     ZZX    Men                        Mixed Doubles  Bronze  
      636     ZZX    Men                        Mixed Doubles  Bronze  
      638     ZZX    Men                        Mixed Doubles  Silver  
      639     ZZX  Women                        Mixed Doubles  Bronze  
      640     ZZX  Women                        Mixed Doubles  Bronze  
      642     ZZX  Women                        Mixed Doubles  Silver  
      651     ZZX    Men                           Tug Of War    Gold  
      652     ZZX    Men                           Tug Of War    Gold  
      653     ZZX    Men                           Tug Of War    Gold  
      654     ZZX    Men                           Tug Of War    Gold  
      655     ZZX    Men                           Tug Of War    Gold  
      656     ZZX    Men                           Tug Of War    Gold  
      765     ZZX    Men                          4Miles Team  Silver  
      766     ZZX    Men                          4Miles Team  Silver  
      767     ZZX    Men                          4Miles Team  Silver  
      768     ZZX    Men                          4Miles Team  Silver  
      769     ZZX    Men                          4Miles Team  Silver  
      864     ZZX    Men                            Foil Team    Gold  
      865     ZZX    Men                            Foil Team    Gold  
      866     ZZX    Men                            Foil Team    Gold  )]




```python
len(l)
```




    147




```python
l[100][1]
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
      <th>Year</th>
      <th>City</th>
      <th>Sport</th>
      <th>Discipline</th>
      <th>Athlete</th>
      <th>Country</th>
      <th>Gender</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5031</th>
      <td>1928</td>
      <td>Amsterdam</td>
      <td>Aquatics</td>
      <td>Swimming</td>
      <td>YLDEFONSO, Teofilo</td>
      <td>PHI</td>
      <td>Men</td>
      <td>200M Breaststroke</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>5741</th>
      <td>1932</td>
      <td>Los Angeles</td>
      <td>Aquatics</td>
      <td>Swimming</td>
      <td>YLDEFONSO, Teofilo</td>
      <td>PHI</td>
      <td>Men</td>
      <td>200M Breaststroke</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>5889</th>
      <td>1932</td>
      <td>Los Angeles</td>
      <td>Athletics</td>
      <td>Athletics</td>
      <td>TORIBIO, Simeon Galvez</td>
      <td>PHI</td>
      <td>Men</td>
      <td>High Jump</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>5922</th>
      <td>1932</td>
      <td>Los Angeles</td>
      <td>Boxing</td>
      <td>Boxing</td>
      <td>VILLANUEVA, Jose</td>
      <td>PHI</td>
      <td>Men</td>
      <td>50.8 - 54KG (Bantamweight)</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>6447</th>
      <td>1936</td>
      <td>Berlin</td>
      <td>Athletics</td>
      <td>Athletics</td>
      <td>WHITE, Miguel S.</td>
      <td>PHI</td>
      <td>Men</td>
      <td>400M Hurdles</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>11005</th>
      <td>1964</td>
      <td>Tokyo</td>
      <td>Boxing</td>
      <td>Boxing</td>
      <td>VILLANUEVA, Anthony N.</td>
      <td>PHI</td>
      <td>Men</td>
      <td>54 - 57KG (Featherweight)</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>18513</th>
      <td>1988</td>
      <td>Seoul</td>
      <td>Boxing</td>
      <td>Boxing</td>
      <td>SERANTES, Leopoldo</td>
      <td>PHI</td>
      <td>Men</td>
      <td>- 48KG (Light-Flyweight)</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>20184</th>
      <td>1992</td>
      <td>Barcelona</td>
      <td>Boxing</td>
      <td>Boxing</td>
      <td>VELASCO, Roel</td>
      <td>PHI</td>
      <td>Men</td>
      <td>- 48KG (Light-Flyweight)</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>21927</th>
      <td>1996</td>
      <td>Atlanta</td>
      <td>Boxing</td>
      <td>Boxing</td>
      <td>VELASCO, Mansueto</td>
      <td>PHI</td>
      <td>Men</td>
      <td>- 48KG (Light-Flyweight)</td>
      <td>Silver</td>
    </tr>
  </tbody>
</table>
</div>




```python
split2 = summer.groupby(by = ["Country", "Gender"])
```


```python
l2 = list(split2)
l2
```




    [(('AFG', 'Men'),
             Year     City      Sport Discipline           Athlete Country Gender  \
      28965  2008  Beijing  Taekwondo  Taekwondo  NIKPAI, Rohullah     AFG    Men   
      30929  2012   London  Taekwondo  Taekwondo  NIKPAI, Rohullah     AFG    Men   
      
                  Event   Medal  
      28965     - 58 KG  Bronze  
      30929  58 - 68 KG  Bronze  ),
     (('AHO', 'Men'),
             Year   City    Sport Discipline          Athlete Country Gender  \
      19323  1988  Seoul  Sailing    Sailing  BOERSMA, Jan D.     AHO    Men   
      
                           Event   Medal  
      19323  Board (Division Ii)  Silver  ),
     (('ALG', 'Men'),
             Year         City      Sport Discipline               Athlete Country  \
      17060  1984  Los Angeles     Boxing     Boxing        ZAOUI, Mohamed     ALG   
      17064  1984  Los Angeles     Boxing     Boxing      MOUSSA, Mustapha     ALG   
      20200  1992    Barcelona     Boxing     Boxing       SOLTANI, Hocine     ALG   
      21610  1996      Atlanta  Athletics  Athletics   MORCELI, Nourredine     ALG   
      21946  1996      Atlanta     Boxing     Boxing       SOLTANI, Hocine     ALG   
      21960  1996      Atlanta     Boxing     Boxing       BAHARI, Mohamed     ALG   
      23624  2000       Sydney  Athletics  Athletics       SAIDI-SIEF, Ali     ALG   
      23631  2000       Sydney  Athletics  Athletics   SAID GUERNI, Djabir     ALG   
      23655  2000       Sydney  Athletics  Athletics  HAMMAD, Abderrahmane     ALG   
      23890  2000       Sydney     Boxing     Boxing      ALLALOU, Mohamed     ALG   
      28637  2008      Beijing       Judo       Judo       BENIKHLEF, Amar     ALG   
      29600  2012       London  Athletics  Athletics    MAKHLOUFI, Taoufik     ALG   
      
            Gender                             Event   Medal  
      17060    Men                           71-75KG  Bronze  
      17064    Men     75 - 81KG (Light-Heavyweight)  Bronze  
      20200    Men         54 - 57KG (Featherweight)  Bronze  
      21610    Men                             1500M    Gold  
      21946    Men           57 - 60KG (Lightweight)    Gold  
      21960    Men                           71-75KG  Bronze  
      23624    Men                             5000M  Silver  
      23631    Men                              800M  Bronze  
      23655    Men                         High Jump  Bronze  
      23890    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      28637    Men          81 - 90KG (Middleweight)  Silver  
      29600    Men                             1500M    Gold  ),
     (('ALG', 'Women'),
             Year       City      Sport Discipline               Athlete Country  \
      19874  1992  Barcelona  Athletics  Athletics    BOULMERKA, Hassiba     ALG   
      23536  2000     Sydney  Athletics  Athletics  MERAH-BENIDA, Nouria     ALG   
      28602  2008    Beijing       Judo       Judo        HADDAD, Soraya     ALG   
      
            Gender                         Event   Medal  
      19874  Women                         1500M    Gold  
      23536  Women                         1500M    Gold  
      28602  Women  48 - 52KG (Half-Lightweight)  Bronze  ),
     (('ANZ', 'Men'),
            Year       City      Sport Discipline                     Athlete  \
      1146  1908     London   Aquatics   Swimming       BEAUREPAIRE, Frank E.   
      1154  1908     London   Aquatics   Swimming       BEAUREPAIRE, Frank E.   
      1208  1908     London  Athletics  Athletics              KERR, Harry E.   
      1298  1908     London     Boxing     Boxing          BAKER, Reginald L.   
      1648  1908     London      Rugby      Rugby              BARNETT, Jumbo   
      1649  1908     London      Rugby      Rugby           BEDE-SMITH, Frank   
      1650  1908     London      Rugby      Rugby         CARMICHAEL, Philipp   
      1651  1908     London      Rugby      Rugby     CARROLL, Daniel Brendan   
      1652  1908     London      Rugby      Rugby            CRAIG, Robert R.   
      1653  1908     London      Rugby      Rugby             GRIFFEN, Thomas   
      1654  1908     London      Rugby      Rugby                HICKEY, John   
      1655  1908     London      Rugby      Rugby          MCARTHUR, Emmanuel   
      1656  1908     London      Rugby      Rugby           MCCABE, Arthur J.   
      1657  1908     London      Rugby      Rugby              MCCUE, Patrick   
      1658  1908     London      Rugby      Rugby       MCKIVATT, Christopher   
      1659  1908     London      Rugby      Rugby          MCMURTRIE, Charles   
      1660  1908     London      Rugby      Rugby    MIDDLETON, Albert Sidney   
      1661  1908     London      Rugby      Rugby            RICHARDS, Thomas   
      1662  1908     London      Rugby      Rugby            RUSSELL, Charles   
      1954  1912  Stockholm   Aquatics   Swimming                HEALY, Cecil   
      1958  1912  Stockholm   Aquatics   Swimming         HARDWICK, Harold H.   
      1967  1912  Stockholm   Aquatics   Swimming         HARDWICK, Harold H.   
      1986  1912  Stockholm   Aquatics   Swimming            BOARDMAN, Leslie   
      1987  1912  Stockholm   Aquatics   Swimming           CHAMPION, Malcolm   
      1988  1912  Stockholm   Aquatics   Swimming         HARDWICK, Harold H.   
      1989  1912  Stockholm   Aquatics   Swimming                HEALY, Cecil   
      2785  1912  Stockholm     Tennis     Tennis  WILDING, Anthony Frederick   
      
           Country Gender                          Event   Medal  
      1146     ANZ    Men                1500M Freestyle  Bronze  
      1154     ANZ    Men                 400M Freestyle  Silver  
      1208     ANZ    Men                     3500M Walk  Bronze  
      1298     ANZ    Men  63.5 - 71.67KG (Middleweight)  Silver  
      1648     ANZ    Men                          Rugby    Gold  
      1649     ANZ    Men                          Rugby    Gold  
      1650     ANZ    Men                          Rugby    Gold  
      1651     ANZ    Men                          Rugby    Gold  
      1652     ANZ    Men                          Rugby    Gold  
      1653     ANZ    Men                          Rugby    Gold  
      1654     ANZ    Men                          Rugby    Gold  
      1655     ANZ    Men                          Rugby    Gold  
      1656     ANZ    Men                          Rugby    Gold  
      1657     ANZ    Men                          Rugby    Gold  
      1658     ANZ    Men                          Rugby    Gold  
      1659     ANZ    Men                          Rugby    Gold  
      1660     ANZ    Men                          Rugby    Gold  
      1661     ANZ    Men                          Rugby    Gold  
      1662     ANZ    Men                          Rugby    Gold  
      1954     ANZ    Men                 100M Freestyle  Silver  
      1958     ANZ    Men                1500M Freestyle  Bronze  
      1967     ANZ    Men                 400M Freestyle  Bronze  
      1986     ANZ    Men         4X200M Freestyle Relay    Gold  
      1987     ANZ    Men         4X200M Freestyle Relay    Gold  
      1988     ANZ    Men         4X200M Freestyle Relay    Gold  
      1989     ANZ    Men         4X200M Freestyle Relay    Gold  
      2785     ANZ    Men                 Singles Indoor  Bronze  ),
     (('ANZ', 'Women'),
            Year       City     Sport Discipline            Athlete Country Gender  \
      1956  1912  Stockholm  Aquatics   Swimming      DURACK, Fanny     ANZ  Women   
      1957  1912  Stockholm  Aquatics   Swimming  WYLIE, Wilhelmina     ANZ  Women   
      
                     Event   Medal  
      1956  100M Freestyle    Gold  
      1957  100M Freestyle  Silver  ),
     (('ARG', 'Men'),
             Year     City      Sport Discipline                        Athlete  \
      4356   1924    Paris  Athletics  Athletics                  BRUNETO, Luis   
      4360   1924    Paris     Boxing     Boxing                PORZIO, Alfredo   
      4366   1924    Paris     Boxing     Boxing               QUARTUCCI, Pedro   
      4371   1924    Paris     Boxing     Boxing               COPELLO, Alfredo   
      4374   1924    Paris     Boxing     Boxing                 MENDEZ, Hector   
      ...     ...      ...        ...        ...                            ...   
      28832  2008  Beijing    Sailing    Sailing                LANGE, Santiago   
      30789  2012   London    Sailing    Sailing               CALABRESE, Lucas   
      30790  2012   London    Sailing    Sailing             DE LA FUENTE, Juan   
      30930  2012   London  Taekwondo  Taekwondo  CRISMANICH, Sebastian Eduardo   
      30954  2012   London     Tennis     Tennis         DEL POTRO, Juan Martin   
      
            Country Gender                            Event   Medal  
      4356      ARG    Men                      Triple Jump  Silver  
      4360      ARG    Men          + 79.38KG (Heavyweight)  Bronze  
      4366      ARG    Men  53.52 - 57.15KG (Featherweight)  Bronze  
      4371      ARG    Men    57.15 - 61.24KG (Lightweight)  Silver  
      4374      ARG    Men   61.24 - 66.68KG (Welterweight)  Silver  
      ...       ...    ...                              ...     ...  
      28832     ARG    Men              Tornado - Multihull  Bronze  
      30789     ARG    Men                              470  Bronze  
      30790     ARG    Men                              470  Bronze  
      30930     ARG    Men                       68 - 80 KG    Gold  
      30954     ARG    Men                          Singles  Bronze  
      
      [187 rows x 9 columns]),
     (('ARG', 'Women'),
             Year    City      Sport Discipline                      Athlete  \
      6352   1936  Berlin   Aquatics   Swimming    CAMPBELL, Jeanette Morven   
      7405   1948  London  Athletics  Athletics  SIMONETTO DE PORTELA, Noemi   
      19434  1988   Seoul     Tennis     Tennis           SABATINI, Gabriela   
      24561  2000  Sydney     Hockey     Hockey            AICEGA, Magdalena   
      24562  2000  Sydney     Hockey     Hockey           ANTONISKA, Mariela   
      ...     ...     ...        ...        ...                          ...   
      30558  2012  London     Hockey     Hockey    RODRIGUEZ PEREZ, Macarena   
      30559  2012  London     Hockey     Hockey        SANCHEZ MOCCIA, Rocio   
      30560  2012  London     Hockey     Hockey             SCARONE, Mariela   
      30561  2012  London     Hockey     Hockey              SRUOGA, Daniela   
      30562  2012  London     Hockey     Hockey             SRUOGA, Josefina   
      
            Country Gender           Event   Medal  
      6352      ARG  Women  100M Freestyle  Silver  
      7405      ARG  Women       Long Jump  Silver  
      19434     ARG  Women         Singles  Silver  
      24561     ARG  Women          Hockey  Silver  
      24562     ARG  Women          Hockey  Silver  
      ...       ...    ...             ...     ...  
      30558     ARG  Women          Hockey  Silver  
      30559     ARG  Women          Hockey  Silver  
      30560     ARG  Women          Hockey  Silver  
      30561     ARG  Women          Hockey  Silver  
      30562     ARG  Women          Hockey  Silver  
      
      [72 rows x 9 columns]),
     (('ARM', 'Men'),
             Year     City          Sport           Discipline  \
      23103  1996  Atlanta      Wrestling      Wrestling Free.   
      23138  1996  Atlanta      Wrestling      Wrestling Gre-R   
      25119  2000   Sydney  Weightlifting        Weightlifting   
      27910  2008  Beijing         Boxing               Boxing   
      29127  2008  Beijing  Weightlifting        Weightlifting   
      29136  2008  Beijing  Weightlifting        Weightlifting   
      29139  2008  Beijing  Weightlifting        Weightlifting   
      29189  2008  Beijing      Wrestling      Wrestling Gre-R   
      29213  2008  Beijing      Wrestling      Wrestling Gre-R   
      31154  2012   London      Wrestling  Wrestling Freestyle   
      31163  2012   London      Wrestling  Wrestling Freestyle   
      
                                Athlete Country Gender                     Event  \
      23103             MKRCHYAN, Armen     ARM    Men  - 48KG (Light-Flyweight)   
      23138             NAZARYAN, Armen     ARM    Men     48 - 52KG (Flyweight)   
      25119             MELIKYAN, Arsen     ARM    Men                      77KG   
      27910          JAVAKHYAN, Hrachik     ARM    Men   57 - 60KG (Lightweight)   
      29127  MARTIROSYAN, Tigran Gevorg     ARM    Men                      69KG   
      29136             DAVTYAN, Gevorg     ARM    Men                      77KG   
      29139  MARTIROSYAN, Tigran Varban     ARM    Men                      85KG   
      29189               AMOYAN, Roman     ARM    Men                    - 55KG   
      29213             PATRIKEEV, Yuri     ARM    Men                96 - 120KG   
      31154          JULFALAKYAN, Arsen     ARM    Men                  Wg 74 KG   
      31163           ALEKSANYAN, Artur     ARM    Men                  Wg 96 KG   
      
              Medal  
      23103  Silver  
      23138    Gold  
      25119  Bronze  
      27910  Bronze  
      29127  Bronze  
      29136  Bronze  
      29139  Bronze  
      29189  Bronze  
      29213  Bronze  
      31154  Silver  
      31163  Bronze  ),
     (('AUS', 'Men'),
             Year    City      Sport Discipline               Athlete Country  \
      18     1896  Athens  Athletics  Athletics          FLACK, Edwin     AUS   
      24     1896  Athens  Athletics  Athletics          FLACK, Edwin     AUS   
      158    1900   Paris   Aquatics   Swimming  LANE, Frederick C.V.     AUS   
      161    1900   Paris   Aquatics   Swimming  LANE, Frederick C.V.     AUS   
      230    1900   Paris  Athletics  Athletics       ROWLEY, Stanley     AUS   
      ...     ...     ...        ...        ...                   ...     ...   
      30785  2012  London    Sailing    Sailing       BELCHER, Mathew     AUS   
      30786  2012  London    Sailing    Sailing         PAGE, Malcolm     AUS   
      30797  2012  London    Sailing    Sailing          JENSEN, Iain     AUS   
      30798  2012  London    Sailing    Sailing    OUTTERIDGE, Nathan     AUS   
      30815  2012  London    Sailing    Sailing         SLINGSBY, Tom     AUS   
      
            Gender                Event   Medal  
      18       Men                1500M    Gold  
      24       Men                 800M    Gold  
      158      Men       200M Freestyle    Gold  
      161      Men  200M Obstacle Event    Gold  
      230      Men                 100M  Bronze  
      ...      ...                  ...     ...  
      30785    Men                  470    Gold  
      30786    Men                  470    Gold  
      30797    Men         49Er - Skiff    Gold  
      30798    Men         49Er - Skiff    Gold  
      30815    Men                Laser    Gold  
      
      [696 rows x 9 columns]),
     (('AUS', 'Women'),
             Year         City      Sport Discipline  \
      5731   1932  Los Angeles   Aquatics   Swimming   
      5745   1932  Los Angeles   Aquatics   Swimming   
      7219   1948       London   Aquatics   Swimming   
      7236   1948       London   Aquatics   Swimming   
      7304   1948       London  Athletics  Athletics   
      ...     ...          ...        ...        ...   
      30784  2012       London     Rowing     Rowing   
      30806  2012       London    Sailing    Sailing   
      30807  2012       London    Sailing    Sailing   
      30808  2012       London    Sailing    Sailing   
      30963  2012       London  Triathlon  Triathlon   
      
                                     Athlete Country Gender              Event  \
      5731        MEALING, Philomenia Alecia     AUS  Women    100M Backstroke   
      5745                     DENNIS, Clare     AUS  Women  200M Breaststroke   
      7219                DAVIES, Judith Joy     AUS  Women    100M Backstroke   
      7236             LYONS, Beatrice Nancy     AUS  Women  200M Breaststroke   
      7304   STRICKLAND-DE LA HUNTY, Shirley     AUS  Women               100M   
      ...                                ...     ...    ...                ...   
      30784                        CROW, Kim     AUS  Women      Single Sculls   
      30806                     CURTIS, Nina     AUS  Women         Elliott 6M   
      30807                    PRICE, Olivia     AUS  Women         Elliott 6M   
      30808                  WHITTY, Lucinda     AUS  Women         Elliott 6M   
      30963                    DENSHAM, Erin     AUS  Women         Individual   
      
              Medal  
      5731   Silver  
      5745     Gold  
      7219   Bronze  
      7236   Silver  
      7304   Bronze  
      ...       ...  
      30784  Bronze  
      30806  Silver  
      30807  Silver  
      30808  Silver  
      30963  Bronze  
      
      [493 rows x 9 columns]),
     (('AUT', 'Men'),
             Year     City     Sport     Discipline                 Athlete Country  \
      1      1896   Athens  Aquatics       Swimming        HERSCHMANN, Otto     AUT   
      9      1896   Athens  Aquatics       Swimming           NEUMANN, Paul     AUT   
      53     1896   Athens   Cycling  Cycling Track           SCHMAL, Adolf     AUT   
      56     1896   Athens   Cycling  Cycling Track           SCHMAL, Adolf     AUT   
      58     1896   Athens   Cycling  Cycling Track           SCHMAL, Adolf     AUT   
      ...     ...      ...       ...            ...                     ...     ...   
      26810  2004   Athens   Sailing        Sailing       GERITZER, Andreas     AUT   
      26819  2004   Athens   Sailing        Sailing           HAGARA, Roman     AUT   
      26820  2004   Athens   Sailing        Sailing  STEINACHER, Hans Peter     AUT   
      26859  2004   Athens  Shooting       Shooting       PLANER, Christian     AUT   
      28593  2008  Beijing      Judo           Judo        PAISCHER, Ludwig     AUT   
      
            Gender                               Event   Medal  
      1        Men                      100M Freestyle  Silver  
      9        Men                      400M Freestyle    Gold  
      53       Men                                10KM  Bronze  
      56       Men                        12-Hour Race    Gold  
      58       Men                      1KM Time Trial  Bronze  
      ...      ...                                 ...     ...  
      26810    Men   Single-Handed Dinghy Open (Laser)  Silver  
      26819    Men                 Tornado - Multihull    Gold  
      26820    Men                 Tornado - Multihull    Gold  
      26859    Men  50M Rifle 3 Positions (3X40 Shots)  Bronze  
      28593    Men                             - 60 KG  Silver  
      
      [125 rows x 9 columns]),
     (('AUT', 'Women'),
             Year         City          Sport       Discipline  \
      1970   1912    Stockholm       Aquatics         Swimming   
      1971   1912    Stockholm       Aquatics         Swimming   
      1972   1912    Stockholm       Aquatics         Swimming   
      1973   1912    Stockholm       Aquatics         Swimming   
      6024   1932  Los Angeles        Fencing          Fencing   
      6736   1936       Berlin        Fencing          Fencing   
      7398   1948       London      Athletics        Athletics   
      7415   1948       London      Athletics        Athletics   
      7509   1948       London  Canoe / Kayak  Canoe / Kayak F   
      7620   1948       London        Fencing          Fencing   
      8346   1952     Helsinki  Canoe / Kayak  Canoe / Kayak F   
      11969  1968       Mexico      Athletics        Athletics   
      11983  1968       Mexico      Athletics        Athletics   
      13015  1972       Munich      Athletics        Athletics   
      15732  1980       Moscow     Equestrian         Dressage   
      21612  1996      Atlanta      Athletics        Athletics   
      23636  2000       Sydney      Athletics        Athletics   
      26599  2004       Athens           Judo             Judo   
      26990  2004       Athens      Triathlon        Triathlon   
      27220  2008      Beijing       Aquatics         Swimming   
      28015  2008      Beijing  Canoe / Kayak  Canoe / Kayak S   
      
                               Athlete Country Gender  \
      1970            ADLER, Margarete     AUT  Women   
      1971                MILCH, Klara     AUT  Women   
      1972          STICKER, Josephine     AUT  Women   
      1973            ZAHOUREK, Bertha     AUT  Women   
      6024      PREIS-MÜLLER, Ellen S.     AUT  Women   
      6736      PREIS-MÜLLER, Ellen S.     AUT  Women   
      7398      BAUMA, Hermine (Herma)     AUT  Women   
      7415         SCHÄFFER-MAYER, Ine     AUT  Women   
      7509        SCHWINGL, Friederike     AUT  Women   
      7620      PREIS-MÜLLER, Ellen S.     AUT  Women   
      8346          LIEBHART, Gertrude     AUT  Women   
      11969           JANKO-EGGER, Eva     AUT  Women   
      11983       PROKOP-SYKORA, Liese     AUT  Women   
      13015   GUSENBAUER-MAJDAN, Ilona     AUT  Women   
      15732     THEURER-MAX, Elisabeth     AUT  Women   
      21612            KIESL, Theresia     AUT  Women   
      23636            GRAF, Stephanie     AUT  Women   
      26599             HEILL, Claudia     AUT  Women   
      26990                ALLEN, Kate     AUT  Women   
      27220               JUKIC, Mirna     AUT  Women   
      28015  OBLINGER PETERS, Violetta     AUT  Women   
      
                                     Event   Medal  
      1970          4X100M Freestyle Relay  Bronze  
      1971          4X100M Freestyle Relay  Bronze  
      1972          4X100M Freestyle Relay  Bronze  
      1973          4X100M Freestyle Relay  Bronze  
      6024                 Foil Individual    Gold  
      6736                 Foil Individual  Bronze  
      7398                   Javelin Throw    Gold  
      7415                        Shot Put  Bronze  
      7509         K-1 500M (Kayak Single)  Bronze  
      7620                 Foil Individual  Bronze  
      8346         K-1 500M (Kayak Single)  Silver  
      11969                  Javelin Throw  Bronze  
      11983                     Pentathlon  Silver  
      13015                      High Jump  Bronze  
      15732                     Individual    Gold  
      21612                          1500M  Bronze  
      23636                           800M  Silver  
      26599  57 - 63KG (Half-Middleweight)  Silver  
      26990                     Individual    Gold  
      27220              100M Breaststroke  Bronze  
      28015             K-1 (Kayak Single)  Bronze  ),
     (('AZE', 'Men'),
             Year     City          Sport           Discipline  \
      23109  1996  Atlanta      Wrestling      Wrestling Free.   
      23902  2000   Sydney         Boxing               Boxing   
      25129  2000   Sydney      Wrestling      Wrestling Free.   
      25884  2004   Athens         Boxing               Boxing   
      25892  2004   Athens         Boxing               Boxing   
      27160  2004   Athens      Wrestling      Wrestling Gre-R   
      27906  2008  Beijing         Boxing               Boxing   
      28624  2008  Beijing           Judo                 Judo   
      28639  2008  Beijing           Judo                 Judo   
      29181  2008  Beijing      Wrestling      Wrestling Free.   
      29192  2008  Beijing      Wrestling      Wrestling Gre-R   
      29196  2008  Beijing      Wrestling      Wrestling Gre-R   
      29871  2012   London         Boxing               Boxing   
      29918  2012   London         Boxing               Boxing   
      31065  2012   London  Weightlifting        Weightlifting   
      31109  2012   London      Wrestling  Wrestling Freestyle   
      31129  2012   London      Wrestling  Wrestling Freestyle   
      31135  2012   London      Wrestling  Wrestling Freestyle   
      31142  2012   London      Wrestling  Wrestling Freestyle   
      31155  2012   London      Wrestling  Wrestling Freestyle   
      
                             Athlete Country Gender                          Event  \
      23109        ABDULLAYEV, Namig     AZE    Men          48 - 52KG (Flyweight)   
      23902         ALAKPAROV, Vugar     AZE    Men                        71-75KG   
      25129        ABDULLAYEV, Namig     AZE    Men                      48 - 54KG   
      25884            ASLANOV, Fuad     AZE    Men          48 - 51KG (Flyweight)   
      25892         MAMMADOV, Aghasi     AZE    Men       51 - 54KG (Bantamweight)   
      27160          MANSUROV, Farid     AZE    Men                      60 - 66KG   
      27906          IMRANOV, Shahin     AZE    Men      54 - 57KG (Featherweight)   
      28624          MAMMADLI, Elnur     AZE    Men        66 - 73KG (Lightweight)   
      28639        MIRALIYEV, Movlud     AZE    Men  90 - 100KG (Half-Heavyweight)   
      29181         GAZYUMOV, Khetag     AZE    Men                      84 - 96KG   
      29192        BAYRAMOV, Rovshan     AZE    Men                         - 55KG   
      29196         RAHIMOV, Vitaliy     AZE    Men                      55 - 60KG   
      29871  MEDZHIDOV, Magomedrasul     AZE    Men                         + 91KG   
      29918         MAMMADOV, Teymur     AZE    Men                      81 - 91KG   
      31065        HRISTOV, Valentin     AZE    Men                          -56KG   
      31109         ASGAROV, Toghrul     AZE    Men                       Wf 60 KG   
      31129         SHARIFOV, Sharif     AZE    Men                       Wf 84 KG   
      31135         GAZYUMOV, Khetag     AZE    Men                       Wf 96 KG   
      31142        BAYRAMOV, Rovshan     AZE    Men                       Wg 55 KG   
      31155            AHMADOV, Emin     AZE    Men                       Wg 74 KG   
      
              Medal  
      23109  Silver  
      23902  Bronze  
      25129    Gold  
      25884  Bronze  
      25892  Bronze  
      27160    Gold  
      27906  Bronze  
      28624    Gold  
      28639  Bronze  
      29181  Bronze  
      29192  Silver  
      29196  Silver  
      29871  Bronze  
      29918  Bronze  
      31065  Bronze  
      31109    Gold  
      31129    Gold  
      31135  Bronze  
      31142  Silver  
      31155  Bronze  ),
     (('AZE', 'Women'),
             Year     City      Sport           Discipline  \
      24880  2000   Sydney   Shooting             Shooting   
      26847  2004   Athens   Shooting             Shooting   
      26874  2004   Athens   Shooting             Shooting   
      29146  2008  Beijing  Wrestling      Wrestling Free.   
      31098  2012   London  Wrestling  Wrestling Freestyle   
      31107  2012   London  Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                     Event  \
      24880  MEFTAKHETDINOVA, Zemfira     AZE  Women        Skeet (75 Targets)   
      26847           ASHUMOVA, Irada     AZE  Women  25M Pistol (30+30 Shots)   
      26874  MEFTAKHETDINOVA, Zemfira     AZE  Women        Skeet (75 Targets)   
      29146           STADNIK, Mariya     AZE  Women                    - 48KG   
      31098           STADNYK, Mariya     AZE  Women                  Wf 48 KG   
      31107         RATKEVICH, Yuliya     AZE  Women                  Wf 55 KG   
      
              Medal  
      24880    Gold  
      26847  Bronze  
      26874  Bronze  
      29146  Bronze  
      31098  Silver  
      31107  Bronze  ),
     (('BAH', 'Men'),
             Year                   City      Sport Discipline  \
      9696   1956  Melbourne / Stockholm    Sailing    Sailing   
      9697   1956  Melbourne / Stockholm    Sailing    Sailing   
      11521  1964                  Tokyo    Sailing    Sailing   
      11522  1964                  Tokyo    Sailing    Sailing   
      20024  1992              Barcelona  Athletics  Athletics   
      27631  2008                Beijing  Athletics  Athletics   
      27632  2008                Beijing  Athletics  Athletics   
      27633  2008                Beijing  Athletics  Athletics   
      27634  2008                Beijing  Athletics  Athletics   
      27716  2008                Beijing  Athletics  Athletics   
      29665  2012                 London  Athletics  Athletics   
      29666  2012                 London  Athletics  Athletics   
      29667  2012                 London  Athletics  Athletics   
      29668  2012                 London  Athletics  Athletics   
      
                               Athlete Country Gender  \
      9696     FARRINGTON, Sloane Elmo     BAH    Men   
      9697   KNOWLES, Durward Randolph     BAH    Men   
      11521        COOKE, Cecil George     BAH    Men   
      11522  KNOWLES, Durward Randolph     BAH    Men   
      20024          RUTHERFORD, Frank     BAH    Men   
      27631             BAIN, Andretti     BAH    Men   
      27632         BROWN, Christopher     BAH    Men   
      27633           MATHIEU, Michael     BAH    Men   
      27634           WILLIAMS, Andrae     BAH    Men   
      27716              SANDS, Leevan     BAH    Men   
      29665               BROWN, Chris     BAH    Men   
      29666           MATHIEU, Michael     BAH    Men   
      29667              MILLER, Ramon     BAH    Men   
      29668          PINDER, Demetrius     BAH    Men   
      
                                       Event   Medal  
      9696   Two-Person Keelboat Open (Star)  Bronze  
      9697   Two-Person Keelboat Open (Star)  Bronze  
      11521  Two-Person Keelboat Open (Star)    Gold  
      11522  Two-Person Keelboat Open (Star)    Gold  
      20024                      Triple Jump  Bronze  
      27631                     4X400M Relay  Silver  
      27632                     4X400M Relay  Silver  
      27633                     4X400M Relay  Silver  
      27634                     4X400M Relay  Silver  
      27716                      Triple Jump  Bronze  
      29665                     4X400M Relay    Gold  
      29666                     4X400M Relay    Gold  
      29667                     4X400M Relay    Gold  
      29668                     4X400M Relay    Gold  ),
     (('BAH', 'Women'),
             Year     City      Sport Discipline                    Athlete Country  \
      21664  1996  Atlanta  Athletics  Athletics             CLARKE, Eldece     BAH   
      21665  1996  Atlanta  Athletics  Athletics      DAVIS, Pauline Elaine     BAH   
      21666  1996  Atlanta  Athletics  Athletics  FERGUSON-MCKENZIE, Debbie     BAH   
      21667  1996  Atlanta  Athletics  Athletics           FYNES, Sevatheda     BAH   
      21668  1996  Atlanta  Athletics  Athletics           STURRUP, Chandra     BAH   
      23542  2000   Sydney  Athletics  Athletics      DAVIS, Pauline Elaine     BAH   
      23584  2000   Sydney  Athletics  Athletics      DAVIS, Pauline Elaine     BAH   
      23585  2000   Sydney  Athletics  Athletics  FERGUSON-MCKENZIE, Debbie     BAH   
      23586  2000   Sydney  Athletics  Athletics           FYNES, Sevatheda     BAH   
      23587  2000   Sydney  Athletics  Athletics              LEWIS, Eldice     BAH   
      23588  2000   Sydney  Athletics  Athletics           STURRUP, Chandra     BAH   
      25559  2004   Athens  Athletics  Athletics  FERGUSON-MCKENZIE, Debbie     BAH   
      25575  2004   Athens  Athletics  Athletics  WILLIAMS-DARLING, Tonique     BAH   
      
            Gender         Event   Medal  
      21664  Women  4X100M Relay  Silver  
      21665  Women  4X100M Relay  Silver  
      21666  Women  4X100M Relay  Silver  
      21667  Women  4X100M Relay  Silver  
      21668  Women  4X100M Relay  Silver  
      23542  Women          200M    Gold  
      23584  Women  4X100M Relay    Gold  
      23585  Women  4X100M Relay    Gold  
      23586  Women  4X100M Relay    Gold  
      23587  Women  4X100M Relay    Gold  
      23588  Women  4X100M Relay    Gold  
      25559  Women          200M  Bronze  
      25575  Women          400M    Gold  ),
     (('BAR', 'Men'),
             Year    City      Sport Discipline            Athlete Country Gender  \
      23520  2000  Sydney  Athletics  Athletics  THOMPSON, Obadele     BAR    Men   
      
            Event   Medal  
      23520  100M  Bronze  ),
     (('BDI', 'Men'),
             Year     City      Sport Discipline             Athlete Country Gender  \
      21700  1996  Atlanta  Athletics  Athletics  NIYONGABO, Venuste     BDI    Men   
      
             Event Medal  
      21700  5000M  Gold  ),
     (('BEL', 'Men'),
             Year    City     Sport     Discipline            Athlete Country  \
      205    1900   Paris  Aquatics     Water polo       COHEN, Henri     BEL   
      206    1900   Paris  Aquatics     Water polo    DE BACKER, Jean     BEL   
      207    1900   Paris  Aquatics     Water polo    DE BEHR, Victor     BEL   
      208    1900   Paris  Aquatics     Water polo  FEYAERTS, Fernand     BEL   
      209    1900   Paris  Aquatics     Water polo    GREGOIRE, Oscar     BEL   
      ...     ...     ...       ...            ...                ...     ...   
      24029  2000  Sydney   Cycling  Cycling Track  DE WILDE, Etienne     BEL   
      24030  2000  Sydney   Cycling  Cycling Track   GILMORE, Matthew     BEL   
      24069  2000  Sydney   Cycling  Mountain Bike  MEIRHAEGHE, Filip     BEL   
      26008  2004  Athens   Cycling   Cycling Road       MERCKX, Axel     BEL   
      30861  2012  London  Shooting       Shooting        COX, Lionel     BEL   
      
            Gender                 Event   Medal  
      205      Men            Water Polo  Silver  
      206      Men            Water Polo  Silver  
      207      Men            Water Polo  Silver  
      208      Men            Water Polo  Silver  
      209      Men            Water Polo  Silver  
      ...      ...                   ...     ...  
      24029    Men               Madison  Silver  
      24030    Men               Madison  Silver  
      24069    Men         Cross-Country  Silver  
      26008    Men  Individual Road Race  Bronze  
      30861    Men       50M Rifle Prone  Silver  
      
      [391 rows x 9 columns]),
     (('BEL', 'Women'),
             Year         City      Sport Discipline                  Athlete  \
      16640  1984  Los Angeles   Aquatics   Swimming        LEMPEREUR, Ingrid   
      17814  1984  Los Angeles     Rowing     Rowing         HAESEBROUCK, Ann   
      20812  1992    Barcelona       Judo       Judo            RAKELS, Heidi   
      21002  1992    Barcelona     Rowing     Rowing        BREDAEL, Annelies   
      22631  1996      Atlanta       Judo       Judo         LOMBA, Marisabel   
      22637  1996      Atlanta       Judo       Judo       VANDECAVEYE, Gella   
      22648  1996      Atlanta       Judo       Judo          WERBROUCK, Ulla   
      24578  2000       Sydney       Judo       Judo              SIMONS, Ann   
      24602  2000       Sydney       Judo       Judo       VANDECAVEYE, Gella   
      24981  2000       Sydney     Tennis     Tennis             CALLENS, Els   
      24982  2000       Sydney     Tennis     Tennis     VAN ROOST, Dominique   
      26588  2004       Athens       Judo       Judo             HEYLEN, Ilse   
      26984  2004       Athens     Tennis     Tennis  HENIN-HARDENNE, Justine   
      27619  2008      Beijing  Athletics  Athletics           BORLEE, Olivia   
      27620  2008      Beijing  Athletics  Athletics             GEVAERT, Kim   
      27621  2008      Beijing  Athletics  Athletics            MARIEN, Hanna   
      27622  2008      Beijing  Athletics  Athletics        OUEDRAOGO, Elodie   
      27684  2008      Beijing  Athletics  Athletics           HELLEBAUT, Tia   
      30582  2012       London       Judo       Judo      VAN SNICK, Charline   
      30820  2012       London    Sailing    Sailing           VAN ACKER, Evi   
      
            Country Gender                          Event   Medal  
      16640     BEL  Women              200M Breaststroke  Bronze  
      17814     BEL  Women             Single Sculls (1X)  Bronze  
      20812     BEL  Women       61 - 66KG (Middleweight)  Bronze  
      21002     BEL  Women             Single Sculls (1X)  Silver  
      22631     BEL  Women        52 - 56KG (Lightweight)  Bronze  
      22637     BEL  Women  56 - 61KG (Half-Middleweight)  Silver  
      22648     BEL  Women   66 - 72KG (Half-Heavyweight)    Gold  
      24578     BEL  Women     - 48KG (Extra-Lightweight)  Bronze  
      24602     BEL  Women  57 - 63KG (Half-Middleweight)  Bronze  
      24981     BEL  Women                        Doubles  Bronze  
      24982     BEL  Women                        Doubles  Bronze  
      26588     BEL  Women   48 - 52KG (Half-Lightweight)  Bronze  
      26984     BEL  Women                        Singles    Gold  
      27619     BEL  Women                   4X100M Relay  Silver  
      27620     BEL  Women                   4X100M Relay  Silver  
      27621     BEL  Women                   4X100M Relay  Silver  
      27622     BEL  Women                   4X100M Relay  Silver  
      27684     BEL  Women                      High Jump    Gold  
      30582     BEL  Women                        - 48 KG  Bronze  
      30820     BEL  Women                   Laser Radial  Bronze  ),
     (('BER', 'Men'),
             Year      City   Sport Discipline         Athlete Country Gender  \
      14288  1976  Montreal  Boxing     Boxing  HILL, Clarence     BER    Men   
      
                            Event   Medal  
      14288  + 81KG (Heavyweight)  Bronze  ),
     (('BLR', 'Men'),
             Year     City              Sport       Discipline  \
      21717  1996  Atlanta          Athletics        Athletics   
      21719  1996  Atlanta          Athletics        Athletics   
      22328  1996  Atlanta         Gymnastics      Artistic G.   
      22331  1996  Atlanta         Gymnastics      Artistic G.   
      22338  1996  Atlanta         Gymnastics      Artistic G.   
      22391  1996  Atlanta         Gymnastics      Artistic G.   
      22881  1996  Atlanta           Shooting         Shooting   
      23106  1996  Atlanta          Wrestling  Wrestling Free.   
      23133  1996  Atlanta          Wrestling  Wrestling Gre-R   
      23152  1996  Atlanta          Wrestling  Wrestling Gre-R   
      23160  1996  Atlanta          Wrestling  Wrestling Gre-R   
      23646  2000   Sydney          Athletics        Athletics   
      24613  2000   Sydney               Judo             Judo   
      24633  2000   Sydney  Modern Pentathlon  Modern Pentath.   
      24840  2000   Sydney           Shooting         Shooting   
      24860  2000   Sydney           Shooting         Shooting   
      24867  2000   Sydney           Shooting         Shooting   
      25104  2000   Sydney      Weightlifting    Weightlifting   
      25110  2000   Sydney      Weightlifting    Weightlifting   
      25173  2000   Sydney          Wrestling  Wrestling Gre-R   
      25666  2004   Athens          Athletics        Athletics   
      25919  2004   Athens             Boxing           Boxing   
      25923  2004   Athens             Boxing           Boxing   
      25957  2004   Athens      Canoe / Kayak  Canoe / Kayak F   
      25958  2004   Athens      Canoe / Kayak  Canoe / Kayak F   
      26626  2004   Athens               Judo             Judo   
      26862  2004   Athens           Shooting         Shooting   
      27116  2004   Athens      Weightlifting    Weightlifting   
      27165  2004   Athens          Wrestling  Wrestling Gre-R   
      27664  2008  Beijing          Athletics        Athletics   
      27671  2008  Beijing          Athletics        Athletics   
      27673  2008  Beijing          Athletics        Athletics   
      27710  2008  Beijing          Athletics        Athletics   
      27942  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27943  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27967  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27968  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27983  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27984  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27985  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      27986  2008  Beijing      Canoe / Kayak  Canoe / Kayak F   
      29110  2008  Beijing      Weightlifting    Weightlifting   
      29141  2008  Beijing      Weightlifting    Weightlifting   
      29173  2008  Beijing          Wrestling  Wrestling Free.   
      29197  2008  Beijing          Wrestling  Wrestling Gre-R   
      29943  2012   London              Canoe     Canoe Sprint   
      29944  2012   London              Canoe     Canoe Sprint   
      29967  2012   London              Canoe     Canoe Sprint   
      29968  2012   London              Canoe     Canoe Sprint   
      30860  2012   London           Shooting         Shooting   
      30947  2012   London             Tennis           Tennis   
      
                             Athlete Country Gender  \
      21717        KAPTYUKH, Vasiliy     BLR    Men   
      21719   DUBROVSHCHIK, Vladimir     BLR    Men   
      22328          SCHERBO, Vitaly     BLR    Men   
      22331          SCHERBO, Vitaly     BLR    Men   
      22338          SCHERBO, Vitaly     BLR    Men   
      22391          SCHERBO, Vitaly     BLR    Men   
      22881           BASINSKI, Igor     BLR    Men   
      23106        MEDVEDEV, Aleksey     BLR    Men   
      23133        PAVLOV, Aleksandr     BLR    Men   
      23152         TSILENT, Valeriy     BLR    Men   
      23160         LISHTVAN, Sergey     BLR    Men   
      23646        ASTAPKOVICH, Igor     BLR    Men   
      24613        LARYUKOV, Anatoly     BLR    Men   
      24633            DOVGAL, Pavel     BLR    Men   
      24840           BASINSKI, Igor     BLR    Men   
      24860           BASINSKI, Igor     BLR    Men   
      24867         MARTYNOV, Sergei     BLR    Men   
      25104       OLESHCHUK, Gennady     BLR    Men   
      25110         LAVRENOV, Sergei     BLR    Men   
      25173          DEBELKA, Dmitry     BLR    Men   
      25666             TIKHON, Ivan     BLR    Men   
      25919     ARIPGADJIEV, Magomed     BLR    Men   
      25923            ZUYEV, Viktar     BLR    Men   
      25957          MAKHNEU, Vadzim     BLR    Men   
      25958      PIATRUSHENKA, Raman     BLR    Men   
      26626            MAKARAU, Ihar     BLR    Men   
      26862         MARTYNOV, Sergei     BLR    Men   
      27116          RYBAKOU, Andrei     BLR    Men   
      27165    MAKARANKA, Viachaslau     BLR    Men   
      27664       KRAUCHANKA, Andrei     BLR    Men   
      27671            TSIKHAN, Ivan     BLR    Men   
      27673      DEVYATOVSKIY, Vadim     BLR    Men   
      27710       MIKHNEVICH, Andrei     BLR    Men   
      27942  BAHDANOVICH, Aliaksandr     BLR    Men   
      27943      BAHDANOVICH, Andrei     BLR    Men   
      27967          MAKHNEU, Vadzim     BLR    Men   
      27968      PIATRUSHENKA, Raman     BLR    Men   
      27983      ABALMASAU, Aliaksei     BLR    Men   
      27984        LITVINCHUK, Artur     BLR    Men   
      27985          MAKHNEU, Vadzim     BLR    Men   
      27986      PIATRUSHENKA, Raman     BLR    Men   
      29110          ARAMNAU, Andrei     BLR    Men   
      29141          RYBAKOU, Andrei     BLR    Men   
      29173          GAIDAROV, Murad     BLR    Men   
      29197       SIAMIONAU, Mikhail     BLR    Men   
      29943  BAHDANOVICH, Aliaksandr     BLR    Men   
      29944      BAHDANOVICH, Andrei     BLR    Men   
      29967          MAKHNEU, Vadzim     BLR    Men   
      29968      PIATRUSHENKA, Raman     BLR    Men   
      30860         MARTYNOV, Sergei     BLR    Men   
      30947              MIRNYI, Max     BLR    Men   
      
                                       Event   Medal  
      21717                     Discus Throw  Bronze  
      21719                     Discus Throw  Silver  
      22328                   Horizontal Bar  Bronze  
      22331             Individual All-Round  Bronze  
      22338                    Parallel Bars  Bronze  
      22391                            Vault  Bronze  
      22881            50M Pistol (60 Shots)  Silver  
      23106  100 - 130KG (Super Heavyweight)  Silver  
      23133         - 48KG (Light-Flyweight)  Silver  
      23152         74 - 82KG (Middleweight)  Bronze  
      23160         90 - 100KG (Heavyweight)  Silver  
      23646                     Hammer Throw  Bronze  
      24613          66 - 73KG (Lightweight)  Bronze  
      24633           Individual Competition  Bronze  
      24840        10M Air Pistol (60 Shots)  Bronze  
      24860            50M Pistol (60 Shots)  Silver  
      24867       50M Rifle Prone (60 Shots)  Bronze  
      25104                             62KG  Bronze  
      25110                             69KG  Bronze  
      25173                       97 - 130KG  Bronze  
      25666                     Hammer Throw  Silver  
      25919    75 - 81KG (Light-Heavyweight)  Silver  
      25923          81 - 91KG (Heavyweight)  Silver  
      25957          K-2 500M (Kayak Double)  Bronze  
      25958          K-2 500M (Kayak Double)  Bronze  
      26626    90 - 100KG (Half-Heavyweight)    Gold  
      26862       50M Rifle Prone (60 Shots)  Bronze  
      27116                             85KG  Silver  
      27165                        74 - 84KG  Bronze  
      27664                        Decathlon  Silver  
      27671                     Hammer Throw  Bronze  
      27673                     Hammer Throw  Silver  
      27710                         Shot Put  Bronze  
      27942         C-2 1000M (Canoe Double)    Gold  
      27943         C-2 1000M (Canoe Double)    Gold  
      27967          K-2 500M (Kayak Double)  Bronze  
      27968          K-2 500M (Kayak Double)  Bronze  
      27983           K-4 1000M (Kayak Four)    Gold  
      27984           K-4 1000M (Kayak Four)    Gold  
      27985           K-4 1000M (Kayak Four)    Gold  
      27986           K-4 1000M (Kayak Four)    Gold  
      29110                            105KG    Gold  
      29141                             85KG  Silver  
      29173                        66 - 74KG  Bronze  
      29197                        60 - 66KG  Bronze  
      29943                        C-2 1000M  Silver  
      29944                        C-2 1000M  Silver  
      29967                         K-2 200M  Silver  
      29968                         K-2 200M  Silver  
      30860                  50M Rifle Prone    Gold  
      30947                    Mixed Doubles    Gold  ),
     (('BLR', 'Women'),
             Year     City       Sport           Discipline              Athlete  \
      21720  1996  Atlanta   Athletics            Athletics      ZVEREVA, Ellina   
      21728  1996  Atlanta   Athletics            Athletics  SAZANOVICH, Natalya   
      22714  1996  Atlanta      Rowing               Rowing    DAVYDENKO, Tamara   
      22715  1996  Atlanta      Rowing               Rowing  LAVRINENKO, Natalya   
      22716  1996  Atlanta      Rowing               Rowing     MIKULICH, Yelena   
      ...     ...      ...         ...                  ...                  ...   
      30378  2012   London  Gymnastics  Gymnastics Rhythmic   SANKOVICH, Kseniya   
      30379  2012   London  Gymnastics  Gymnastics Rhythmic    TUMILOVICH, Alina   
      30388  2012   London  Gymnastics  Gymnastics Rhythmic  CHARKASHYNA, Liubou   
      30946  2012   London      Tennis               Tennis   AZARENKA, Victoria   
      30957  2012   London      Tennis               Tennis   AZARENKA, Victoria   
      
            Country Gender                     Event   Medal  
      21720     BLR  Women              Discus Throw  Bronze  
      21728     BLR  Women                Heptathlon  Silver  
      22714     BLR  Women  Eight With Coxswain (8+)  Bronze  
      22715     BLR  Women  Eight With Coxswain (8+)  Bronze  
      22716     BLR  Women  Eight With Coxswain (8+)  Bronze  
      ...       ...    ...                       ...     ...  
      30378     BLR  Women         Group Competition  Silver  
      30379     BLR  Women         Group Competition  Silver  
      30388     BLR  Women     Individual All-Around  Bronze  
      30946     BLR  Women             Mixed Doubles    Gold  
      30957     BLR  Women                   Singles  Bronze  
      
      [62 rows x 9 columns]),
     (('BOH', 'Men'),
            Year    City      Sport Discipline                     Athlete Country  \
      275   1900   Paris  Athletics  Athletics            JANDA, Frantisek     BOH   
      1345  1908  London    Fencing    Fencing  GOPPOLD DE LOBSDORF, Vilem     BOH   
      1348  1908  London    Fencing    Fencing  GOPPOLD DE LOBSDORF, Vilem     BOH   
      1349  1908  London    Fencing    Fencing             LADA, Vlastimil     BOH   
      1350  1908  London    Fencing    Fencing           SCHEJBAL, Bedrich     BOH   
      1351  1908  London    Fencing    Fencing            TUCEK, Frantisek     BOH   
      
           Gender             Event   Medal  
      275     Men      Discus Throw  Silver  
      1345    Men  Sabre Individual  Bronze  
      1348    Men        Sabre Team  Bronze  
      1349    Men        Sabre Team  Bronze  
      1350    Men        Sabre Team  Bronze  
      1351    Men        Sabre Team  Bronze  ),
     (('BOH', 'Women'),
           Year   City   Sport Discipline            Athlete Country Gender  \
      648  1900  Paris  Tennis     Tennis  ROSENBAUM, Hedwig     BOH  Women   
      
             Event   Medal  
      648  Singles  Bronze  ),
     (('BOT', 'Men'),
             Year    City      Sport Discipline      Athlete Country Gender Event  \
      29705  2012  London  Athletics  Athletics  AMOS, Nijel     BOT    Men  800M   
      
              Medal  
      29705  Silver  ),
     (('BRA', 'Men'),
             Year     City       Sport  Discipline                    Athlete  \
      3853   1920  Antwerp    Shooting    Shooting        PARAENSE, Guilherme   
      3918   1920  Antwerp    Shooting    Shooting             BARBOSA, Dario   
      3919   1920  Antwerp    Shooting    Shooting  DA COSTA, Afranio Antonio   
      3920   1920  Antwerp    Shooting    Shooting        PARAENSE, Guilherme   
      3921   1920  Antwerp    Shooting    Shooting         SOLEDADE, Fernando   
      ...     ...      ...         ...         ...                        ...   
      30995  2012   London  Volleyball  Volleyball             REZENDE, Bruno   
      30996  2012   London  Volleyball  Volleyball            SAATKAMP, Lucas   
      30997  2012   London  Volleyball  Volleyball           SANTANA, Rodrigo   
      30998  2012   London  Volleyball  Volleyball             SANTOS, Sergio   
      30999  2012   London  Volleyball  Volleyball    VISSOTTO NEVES, Leandro   
      
            Country Gender                             Event   Medal  
      3853      BRA    Men  25M Rapid Fire Pistol (60 Shots)    Gold  
      3918      BRA    Men             50M Army Pistol, Team  Bronze  
      3919      BRA    Men             50M Army Pistol, Team  Bronze  
      3920      BRA    Men             50M Army Pistol, Team  Bronze  
      3921      BRA    Men             50M Army Pistol, Team  Bronze  
      ...       ...    ...                               ...     ...  
      30995     BRA    Men                        Volleyball  Silver  
      30996     BRA    Men                        Volleyball  Silver  
      30997     BRA    Men                        Volleyball  Silver  
      30998     BRA    Men                        Volleyball  Silver  
      30999     BRA    Men                        Volleyball  Silver  
      
      [303 rows x 9 columns]),
     (('BRA', 'Women'),
             Year     City       Sport  Discipline                   Athlete  \
      21912  1996  Atlanta  Basketball  Basketball           ANGELICA, Maria   
      21913  1996  Atlanta  Basketball  Basketball            ARCAIN, Janeth   
      21914  1996  Atlanta  Basketball  Basketball           GUSTAVO, Roseli   
      21915  1996  Atlanta  Basketball  Basketball               LUZ, Silvia   
      21916  1996  Atlanta  Basketball  Basketball  OLIVA, Hortencia Marcari   
      ...     ...      ...         ...         ...                       ...   
      31019  2012   London  Volleyball  Volleyball         OLIVEIRA, Fabiana   
      31020  2012   London  Volleyball  Volleyball            PEQUENO, Paula   
      31021  2012   London  Volleyball  Volleyball          PEREIRA, Natalia   
      31022  2012   London  Volleyball  Volleyball       RODRIGUES, Fernanda   
      31023  2012   London  Volleyball  Volleyball           SILVA, Adenizia   
      
            Country Gender       Event   Medal  
      21912     BRA  Women  Basketball  Silver  
      21913     BRA  Women  Basketball  Silver  
      21914     BRA  Women  Basketball  Silver  
      21915     BRA  Women  Basketball  Silver  
      21916     BRA  Women  Basketball  Silver  
      ...       ...    ...         ...     ...  
      31019     BRA  Women  Volleyball    Gold  
      31020     BRA  Women  Volleyball    Gold  
      31021     BRA  Women  Volleyball    Gold  
      31022     BRA  Women  Volleyball    Gold  
      31023     BRA  Women  Volleyball    Gold  
      
      [128 rows x 9 columns]),
     (('BRN', 'Women'),
             Year    City      Sport Discipline              Athlete Country Gender  \
      29605  2012  London  Athletics  Athletics  JAMAL, Maryam Yusuf     BRN  Women   
      
             Event   Medal  
      29605  1500M  Bronze  ),
     (('BUL', 'Men'),
             Year                   City      Sport       Discipline  \
      8312   1952               Helsinki     Boxing           Boxing   
      9390   1956  Melbourne / Stockholm   Football         Football   
      9391   1956  Melbourne / Stockholm   Football         Football   
      9392   1956  Melbourne / Stockholm   Football         Football   
      9393   1956  Melbourne / Stockholm   Football         Football   
      ...     ...                    ...        ...              ...   
      27156  2004                 Athens  Wrestling  Wrestling Gre-R   
      29150  2008                Beijing  Wrestling  Wrestling Free.   
      29174  2008                Beijing  Wrestling  Wrestling Free.   
      29202  2008                Beijing  Wrestling  Wrestling Gre-R   
      29919  2012                 London     Boxing           Boxing   
      
                                 Athlete Country Gender      Event   Medal  
      8312       NIKOLOV, Boris Georgiev     BUL    Men    71-75KG  Bronze  
      9390         DIEV, Todor Nedyalkov     BUL    Men   Football  Bronze  
      9391            KOLEV, Ivan Petkov     BUL    Men   Football  Bronze  
      9392   KOVATCHEV, Nikolai Dimitrov     BUL    Men   Football  Bronze  
      9393          MANOLOV, Manol Tomov     BUL    Men   Football  Bronze  
      ...                            ...     ...    ...        ...     ...  
      27156              NAZARIAN, Armen     BUL    Men  55 - 60KG  Bronze  
      29150            VELIKOV, Radoslav     BUL    Men     - 55KG  Bronze  
      29174               TERZIEV, Kiril     BUL    Men  66 - 74KG  Bronze  
      29202              YANAKIEV, Yavor     BUL    Men  66 - 74KG  Bronze  
      29919                PULEV, Tervel     BUL    Men  81 - 91KG  Bronze  
      
      [215 rows x 9 columns]),
     (('BUL', 'Women'),
             Year      City      Sport           Discipline  \
      13006  1972    Munich  Athletics            Athletics   
      13017  1972    Munich  Athletics            Athletics   
      13029  1972    Munich  Athletics            Athletics   
      13042  1972    Munich  Athletics            Athletics   
      14163  1976  Montreal  Athletics            Athletics   
      ...     ...       ...        ...                  ...   
      26832  2004    Athens   Shooting             Shooting   
      26848  2004    Athens   Shooting             Shooting   
      28790  2008   Beijing     Rowing               Rowing   
      29172  2008   Beijing  Wrestling      Wrestling Free.   
      31122  2012    London  Wrestling  Wrestling Freestyle   
      
                                          Athlete Country Gender  \
      13006                      STOEVA, Vassilka     BUL  Women   
      13017          BLAGOEVA-DIMITROVA, Yordanka     BUL  Women   
      13029              CHRISTOVA-YORGOVA, Diana     BUL  Women   
      13042  CHRISTOVA-TODOROVA, Ivanka Mikailova     BUL  Women   
      14163                    CHTEREVA, Nikolina     BUL  Women   
      ...                                     ...     ...    ...   
      26832                       GROZDEVA, Maria     BUL  Women   
      26848                       GROZDEVA, Maria     BUL  Women   
      28790                      NEYKOVA, Rumyana     BUL  Women   
      29172                       ZLATEVA, Stanka     BUL  Women   
      31122              HRISTOVA, Stanka Zlateva     BUL  Women   
      
                                 Event   Medal  
      13006               Discus Throw  Bronze  
      13017                  High Jump  Silver  
      13029                  Long Jump  Silver  
      13042                   Shot Put  Bronze  
      14163                       800M  Silver  
      ...                          ...     ...  
      26832  10M Air Pistol (40 Shots)  Bronze  
      26848   25M Pistol (30+30 Shots)    Gold  
      28790         Single Sculls (1X)    Gold  
      29172                  63 - 72KG  Silver  
      31122                   Wf 72 KG  Silver  
      
      [118 rows x 9 columns]),
     (('BWI', 'Men'),
            Year  City      Sport Discipline                     Athlete Country  \
      9977  1960  Rome  Athletics  Athletics  GARDNER, Keith Alvin Saint     BWI   
      9978  1960  Rome  Athletics  Athletics        KERR, George Ezekiel     BWI   
      9979  1960  Rome  Athletics  Athletics        SPENCE, Malcolm A.E.     BWI   
      9980  1960  Rome  Athletics  Athletics           WEDDERBURN, James     BWI   
      9995  1960  Rome  Athletics  Athletics        KERR, George Ezekiel     BWI   
      
           Gender         Event   Medal  
      9977    Men  4X400M Relay  Bronze  
      9978    Men  4X400M Relay  Bronze  
      9979    Men  4X400M Relay  Bronze  
      9980    Men  4X400M Relay  Bronze  
      9995    Men          800M  Bronze  ),
     (('CAN', 'Men'),
             Year      City      Sport Discipline                 Athlete Country  \
      246    1900     Paris  Athletics  Athletics           ORTON, George     CAN   
      254    1900     Paris  Athletics  Athletics           ORTON, George     CAN   
      771    1904  St Louis  Athletics  Athletics     DESMARTEAU, Etienne     CAN   
      898    1904  St Louis   Football   Football          DUCKER, George     CAN   
      899    1904  St Louis   Football   Football  FRASER, John Alexander     CAN   
      ...     ...       ...        ...        ...                     ...     ...   
      30690  2012    London     Rowing     Rowing          CSIMA, Douglas     CAN   
      30691  2012    London     Rowing     Rowing             GIBSON, Rob     CAN   
      30692  2012    London     Rowing     Rowing         HOWARD, Malcolm     CAN   
      30693  2012    London     Rowing     Rowing          MCCABE, Conlin     CAN   
      30694  2012    London     Rowing     Rowing            PRICE, Brian     CAN   
      
            Gender                       Event   Medal  
      246      Men          3000M Steeplechase    Gold  
      254      Men                400M Hurdles  Bronze  
      771      Men  56LB Weight Throw (25.4KG)    Gold  
      898      Men                    Football    Gold  
      899      Men                    Football    Gold  
      ...      ...                         ...     ...  
      30690    Men         Eight With Coxswain  Silver  
      30691    Men         Eight With Coxswain  Silver  
      30692    Men         Eight With Coxswain  Silver  
      30693    Men         Eight With Coxswain  Silver  
      30694    Men         Eight With Coxswain  Silver  
      
      [428 rows x 9 columns]),
     (('CAN', 'Women'),
             Year       City          Sport           Discipline  \
      5097   1928  Amsterdam      Athletics            Athletics   
      5099   1928  Amsterdam      Athletics            Athletics   
      5134   1928  Amsterdam      Athletics            Athletics   
      5135   1928  Amsterdam      Athletics            Athletics   
      5136   1928  Amsterdam      Athletics            Athletics   
      ...     ...        ...            ...                  ...   
      30720  2012     London         Rowing               Rowing   
      30721  2012     London         Rowing               Rowing   
      31074  2012     London  Weightlifting        Weightlifting   
      31100  2012     London      Wrestling  Wrestling Freestyle   
      31106  2012     London      Wrestling  Wrestling Freestyle   
      
                         Athlete Country Gender                Event   Medal  
      5097       SMITH, Ethel M.     CAN  Women                 100M  Bronze  
      5099      ROSENFELD, Fanny     CAN  Women                 100M  Silver  
      5134    COOK, Myrtle Alice     CAN  Women         4X100M Relay    Gold  
      5135      ROSENFELD, Fanny     CAN  Women         4X100M Relay    Gold  
      5136       SMITH, Ethel M.     CAN  Women         4X100M Relay    Gold  
      ...                    ...     ...    ...                  ...     ...  
      30720   VIINBERG, Rachelle     CAN  Women  Eight With Coxswain  Silver  
      30721    WILKINSON, Lauren     CAN  Women  Eight With Coxswain  Silver  
      31074    GIRARD, Christine     CAN  Women                 63KG  Bronze  
      31100         HUYNH, Carol     CAN  Women             Wf 48 KG  Bronze  
      31106  VERBEEK, Tonya Lynn     CAN  Women             Wf 55 KG  Silver  
      
      [221 rows x 9 columns]),
     (('CHI', 'Men'),
             Year                   City       Sport Discipline  \
      5189   1928              Amsterdam   Athletics  Athletics   
      8421   1952               Helsinki  Equestrian    Jumping   
      8428   1952               Helsinki  Equestrian    Jumping   
      8429   1952               Helsinki  Equestrian    Jumping   
      8430   1952               Helsinki  Equestrian    Jumping   
      9176   1956  Melbourne / Stockholm      Boxing     Boxing   
      9203   1956  Melbourne / Stockholm      Boxing     Boxing   
      9204   1956  Melbourne / Stockholm      Boxing     Boxing   
      19389  1988                  Seoul    Shooting   Shooting   
      24184  2000                 Sydney    Football   Football   
      24185  2000                 Sydney    Football   Football   
      24186  2000                 Sydney    Football   Football   
      24187  2000                 Sydney    Football   Football   
      24188  2000                 Sydney    Football   Football   
      24189  2000                 Sydney    Football   Football   
      24190  2000                 Sydney    Football   Football   
      24191  2000                 Sydney    Football   Football   
      24192  2000                 Sydney    Football   Football   
      24193  2000                 Sydney    Football   Football   
      24194  2000                 Sydney    Football   Football   
      24195  2000                 Sydney    Football   Football   
      24196  2000                 Sydney    Football   Football   
      24197  2000                 Sydney    Football   Football   
      24198  2000                 Sydney    Football   Football   
      24199  2000                 Sydney    Football   Football   
      24200  2000                 Sydney    Football   Football   
      24201  2000                 Sydney    Football   Football   
      26972  2004                 Athens      Tennis     Tennis   
      26973  2004                 Athens      Tennis     Tennis   
      26980  2004                 Athens      Tennis     Tennis   
      26981  2004                 Athens      Tennis     Tennis   
      29006  2008                Beijing      Tennis     Tennis   
      
                              Athlete Country Gender                          Event  \
      5189        PLAZA REYES, Manuel     CHI    Men                       Marathon   
      8421        CRISTI-GALLO, Oscar     CHI    Men                     Individual   
      8428        CRISTI-GALLO, Oscar     CHI    Men                           Team   
      8429        ECHEVERRIA, Ricardo     CHI    Men                           Team   
      8430             MENDOZA, Cesar     CHI    Men                           Team   
      9176        BARRIENTOS, Claudio     CHI    Men       51 - 54KG (Bantamweight)   
      9203               TAPIA, Ramon     CHI    Men                        71-75KG   
      9204              LUCAS, Carlos     CHI    Men  75 - 81KG (Light-Heavyweight)   
      19389  DE IRRUARRIZAGA, Alfonso     CHI    Men            Skeet (125 Targets)   
      24184         ALVAREZ, Cristian     CHI    Men                       Football   
      24185          ARRUE, Francisco     CHI    Men                       Football   
      24186          CONTRERAS, Pablo     CHI    Men                       Football   
      24187       DI GREGORIO, Javier     CHI    Men                       Football   
      24188       GONZALEZ, Sebastian     CHI    Men                       Football   
      24189          HENRIQUEZ, David     CHI    Men                       Football   
      24190            IBARRA, Manuel     CHI    Men                       Football   
      24191        MALDONADO, Claudio     CHI    Men                       Football   
      24192           NAVIA, Reinaldo     CHI    Men                       Football   
      24193            NUNEZ, Rodrigo     CHI    Men                       Football   
      24194            OLARRA, Rafael     CHI    Men                       Football   
      24195       ORMAZABAL, Patricio     CHI    Men                       Football   
      24196            PIZARRO, David     CHI    Men                       Football   
      24197              REYES, Pedro     CHI    Men                       Football   
      24198           ROJAS, Mauricio     CHI    Men                       Football   
      24199             TAPIA, Nelson     CHI    Men                       Football   
      24200            TELLO, Rodrigo     CHI    Men                       Football   
      24201            ZAMORANO, Ivan     CHI    Men                       Football   
      26972        GONZALEZ, Fernando     CHI    Men                        Doubles   
      26973            MASSU, Nicolas     CHI    Men                        Doubles   
      26980        GONZALEZ, Fernando     CHI    Men                        Singles   
      26981            MASSU, Nicolas     CHI    Men                        Singles   
      29006        GONZALEZ, Fernando     CHI    Men                        Singles   
      
              Medal  
      5189   Silver  
      8421   Silver  
      8428   Silver  
      8429   Silver  
      8430   Silver  
      9176   Bronze  
      9203   Silver  
      9204   Bronze  
      19389  Silver  
      24184  Bronze  
      24185  Bronze  
      24186  Bronze  
      24187  Bronze  
      24188  Bronze  
      24189  Bronze  
      24190  Bronze  
      24191  Bronze  
      24192  Bronze  
      24193  Bronze  
      24194  Bronze  
      24195  Bronze  
      24196  Bronze  
      24197  Bronze  
      24198  Bronze  
      24199  Bronze  
      24200  Bronze  
      24201  Bronze  
      26972    Gold  
      26973    Gold  
      26980  Bronze  
      26981    Gold  
      29006  Silver  ),
     (('CHI', 'Women'),
            Year                   City      Sport Discipline          Athlete  \
      9110  1956  Melbourne / Stockholm  Athletics  Athletics  AHRENS, Marlene   
      
           Country Gender          Event   Medal  
      9110     CHI  Women  Javelin Throw  Silver  ),
     (('CHN', 'Men'),
             Year         City          Sport     Discipline         Athlete  \
      16592  1984  Los Angeles       Aquatics         Diving  LI, Kong-Zheng   
      16600  1984  Los Angeles       Aquatics         Diving   TAN, Liang-De   
      16914  1984  Los Angeles      Athletics      Athletics   ZHU, Jian-Hua   
      17357  1984  Los Angeles     Gymnastics    Artistic G.        LI, Ning   
      17358  1984  Los Angeles     Gymnastics    Artistic G.        LOU, Yun   
      ...     ...          ...            ...            ...             ...   
      30917  2012       London      Taekwondo      Taekwondo     LIU, Xiaobo   
      31064  2012       London  Weightlifting  Weightlifting    WU, Jingbiao   
      31075  2012       London  Weightlifting  Weightlifting   LIN, Qingfeng   
      31084  2012       London  Weightlifting  Weightlifting     LU, Xiaojun   
      31085  2012       London  Weightlifting  Weightlifting      LU, Haojie   
      
            Country Gender            Event   Medal  
      16592     CHN    Men     10M Platform  Bronze  
      16600     CHN    Men   3M Springboard  Silver  
      16914     CHN    Men        High Jump  Bronze  
      17357     CHN    Men  Floor Exercises    Gold  
      17358     CHN    Men  Floor Exercises  Silver  
      ...       ...    ...              ...     ...  
      30917     CHN    Men          + 80 KG  Bronze  
      31064     CHN    Men            -56KG  Silver  
      31075     CHN    Men             69KG    Gold  
      31084     CHN    Men             77KG    Gold  
      31085     CHN    Men             77KG  Silver  
      
      [270 rows x 9 columns]),
     (('CHN', 'Women'),
             Year         City          Sport           Discipline         Athlete  \
      16596  1984  Los Angeles       Aquatics               Diving   ZHOU, Ji-Hong   
      16789  1984  Los Angeles        Archery              Archery   LI, Ling-Juan   
      16987  1984  Los Angeles     Basketball           Basketball         BA, Yan   
      16988  1984  Los Angeles     Basketball           Basketball  CHEN, Yue-Fang   
      16989  1984  Los Angeles     Basketball           Basketball     CONG, Xuedi   
      ...     ...          ...            ...                  ...             ...   
      30919  2012       London      Taekwondo            Taekwondo     HOU, Yuzhuo   
      31051  2012       London  Weightlifting        Weightlifting      ZHOU, Lulu   
      31057  2012       London  Weightlifting        Weightlifting  WANG, Mingjuan   
      31066  2012       London  Weightlifting        Weightlifting     LI, Xueying   
      31114  2012       London      Wrestling  Wrestling Freestyle    JING, Ruixue   
      
            Country Gender                  Event   Medal  
      16596     CHN  Women           10M Platform    Gold  
      16789     CHN  Women  Individual Fita Round  Silver  
      16987     CHN  Women             Basketball  Bronze  
      16988     CHN  Women             Basketball  Bronze  
      16989     CHN  Women             Basketball  Bronze  
      ...       ...    ...                    ...     ...  
      30919     CHN  Women             49 - 57 KG  Silver  
      31051     CHN  Women                  +75KG    Gold  
      31057     CHN  Women                   48KG    Gold  
      31066     CHN  Women                   58KG    Gold  
      31114     CHN  Women               Wf 63 KG  Silver  
      
      [537 rows x 9 columns]),
     (('CIV', 'Men'),
             Year         City      Sport Discipline          Athlete Country  \
      16829  1984  Los Angeles  Athletics  Athletics  TIACOH, Gabriel     CIV   
      
            Gender Event   Medal  
      16829    Men  400M  Silver  ),
     (('CMR', 'Men'),
             Year         City     Sport Discipline                Athlete Country  \
      12063  1968       Mexico    Boxing     Boxing        BESSALA, Joseph     CMR   
      17044  1984  Los Angeles    Boxing     Boxing  NDONGO-EBANGA, Martin     CMR   
      24202  2000       Sydney  Football   Football  ABANDA ETONG, Patrice     CMR   
      24203  2000       Sydney  Football   Football      ALNOUDJI, Nicolas     CMR   
      24204  2000       Sydney  Football   Football         BEAUD, Clement     CMR   
      24205  2000       Sydney  Football   Football   BEKONO NDENE, Daniel     CMR   
      24206  2000       Sydney  Football   Football          BRANCO, Serge     CMR   
      24207  2000       Sydney  Football   Football           EPALLE, Joel     CMR   
      24208  2000       Sydney  Football   Football    ETAME MAYER, Lawren     CMR   
      24209  2000       Sydney  Football   Football     ETO'O FILS, Samuel     CMR   
      24210  2000       Sydney  Football   Football       KAMENI, Idriss C     CMR   
      24211  2000       Sydney  Football   Football         MBAMI, Modeste     CMR   
      24212  2000       Sydney  Football   Football     MBOMA DEM, Patrick     CMR   
      24213  2000       Sydney  Football   Football      MEYONG ZE, Albert     CMR   
      24214  2000       Sydney  Football   Football           MIMPO, Serge     CMR   
      24215  2000       Sydney  Football   Football     NGOME KOME, Daniel     CMR   
      24216  2000       Sydney  Football   Football        NGUIMBAT, Aaron     CMR   
      24217  2000       Sydney  Football   Football   NJITAP FOTSO, Geremi     CMR   
      24218  2000       Sydney  Football   Football       SUFFO K, Patrick     CMR   
      24219  2000       Sydney  Football   Football     WOME NLEND, Pierre     CMR   
      
            Gender                       Event   Medal  
      12063    Men  63.5 - 67KG (Welterweight)  Silver  
      17044    Men     57 - 60KG (Lightweight)  Bronze  
      24202    Men                    Football    Gold  
      24203    Men                    Football    Gold  
      24204    Men                    Football    Gold  
      24205    Men                    Football    Gold  
      24206    Men                    Football    Gold  
      24207    Men                    Football    Gold  
      24208    Men                    Football    Gold  
      24209    Men                    Football    Gold  
      24210    Men                    Football    Gold  
      24211    Men                    Football    Gold  
      24212    Men                    Football    Gold  
      24213    Men                    Football    Gold  
      24214    Men                    Football    Gold  
      24215    Men                    Football    Gold  
      24216    Men                    Football    Gold  
      24217    Men                    Football    Gold  
      24218    Men                    Football    Gold  
      24219    Men                    Football    Gold  ),
     (('CMR', 'Women'),
             Year     City          Sport     Discipline                    Athlete  \
      25713  2004   Athens      Athletics      Athletics    MBANGO ETONE, Francoise   
      27720  2008  Beijing      Athletics      Athletics    MBANGO ETONE, Francoise   
      31083  2012   London  Weightlifting  Weightlifting  NZESSO NGAKE, Madias Dodo   
      
            Country Gender        Event   Medal  
      25713     CMR  Women  Triple Jump    Gold  
      27720     CMR  Women  Triple Jump    Gold  
      31083     CMR  Women         75KG  Bronze  ),
     (('COL', 'Men'),
             Year         City          Sport     Discipline  \
      13101  1972       Munich         Boxing         Boxing   
      13105  1972       Munich         Boxing         Boxing   
      13735  1972       Munich       Shooting       Shooting   
      17882  1984  Los Angeles       Shooting       Shooting   
      18524  1988        Seoul         Boxing         Boxing   
      29123  2008      Beijing  Weightlifting  Weightlifting   
      30003  2012       London        Cycling    Cycling BMX   
      30008  2012       London        Cycling   Cycling Road   
      30909  2012       London      Taekwondo      Taekwondo   
      31070  2012       London  Weightlifting  Weightlifting   
      
                                      Athlete Country Gender  \
      13101                   ROJAS, Clemente     COL    Men   
      13105                    PEREZ, Alfonso     COL    Men   
      13735               BELLINGRODT, Helmut     COL    Men   
      17882               BELLINGRODT, Helmut     COL    Men   
      18524        JULIO ROCHA, Jorge Eliecer     COL    Men   
      29123                    SALAZAR, Diego     COL    Men   
      30003      OQUENDO ZABALA, Carlos Mario     COL    Men   
      30008              URAN URAN, Rigoberto     COL    Men   
      30909               MUNOZ OVIEDO, Oscar     COL    Men   
      31070  FIGUEROA MOSQUERA, Oscar Albeiro     COL    Men   
      
                                        Event   Medal  
      13101         54 - 57KG (Featherweight)  Bronze  
      13105           57 - 60KG (Lightweight)  Bronze  
      13735  50M Running Target (30+30 Shots)  Silver  
      17882  50M Running Target (30+30 Shots)  Silver  
      18524          51 - 54KG (Bantamweight)  Bronze  
      29123                              62KG  Silver  
      30003                        Individual  Bronze  
      30008                   Individual Road  Silver  
      30909                           - 58 KG  Bronze  
      31070                              62KG  Silver  ),
     (('COL', 'Women'),
             Year       City          Sport           Discipline  \
      19894  1992  Barcelona      Athletics            Athletics   
      25117  2000     Sydney  Weightlifting        Weightlifting   
      26044  2004     Athens        Cycling        Cycling Track   
      27090  2004     Athens  Weightlifting        Weightlifting   
      29153  2008    Beijing      Wrestling      Wrestling Free.   
      29770  2012     London      Athletics            Athletics   
      30004  2012     London        Cycling          Cycling BMX   
      30613  2012     London           Judo                 Judo   
      31108  2012     London      Wrestling  Wrestling Freestyle   
      
                                  Athlete Country Gender        Event   Medal  
      19894      RESTREPO GAVIRIA, Ximena     COL  Women         400M  Bronze  
      25117         URRUTIA, Maria Isabel     COL  Women         75KG    Gold  
      26044   CALLE WILLIAMS, Maria Luisa     COL  Women  Points Race  Bronze  
      27090               MOSQUERA, Mabel     COL  Women         53KG  Bronze  
      29153           RENTERIA, Jackeline     COL  Women    48 - 55KG  Bronze  
      29770            IBARGUEN, Caterine     COL  Women  Triple Jump  Silver  
      30004                PAJON, Mariana     COL  Women   Individual    Gold  
      30613                  ALVEAR, Yuri     COL  Women    63 - 70KG  Bronze  
      31108  RENTERIA CASTILLO, Jackeline     COL  Women     Wf 55 KG  Bronze  ),
     (('CRC', 'Women'),
             Year     City     Sport Discipline               Athlete Country  \
      18113  1988    Seoul  Aquatics   Swimming   POLL AHRENS, Silvia     CRC   
      21363  1996  Atlanta  Aquatics   Swimming  POLL AHRENS, Claudia     CRC   
      23246  2000   Sydney  Aquatics   Swimming  POLL AHRENS, Claudia     CRC   
      23258  2000   Sydney  Aquatics   Swimming  POLL AHRENS, Claudia     CRC   
      
            Gender           Event   Medal  
      18113  Women  200M Freestyle  Silver  
      21363  Women  200M Freestyle    Gold  
      23246  Women  200M Freestyle  Bronze  
      23258  Women  400M Freestyle  Bronze  ),
     (('CRO', 'Men'),
             Year       City       Sport  Discipline               Athlete Country  \
      20135  1992  Barcelona  Basketball  Basketball      ALANOVIC, Vladan     CRO   
      20136  1992  Barcelona  Basketball  Basketball      ARAPOVIC, Franjo     CRO   
      20137  1992  Barcelona  Basketball  Basketball    CVJETICANIN, Danko     CRO   
      20138  1992  Barcelona  Basketball  Basketball          GREGOV, Alan     CRO   
      20139  1992  Barcelona  Basketball  Basketball       KOMAZEC, Arijan     CRO   
      ...     ...        ...         ...         ...                   ...     ...   
      30759  2012     London      Rowing      Rowing         MARTIN, Damir     CRO   
      30760  2012     London      Rowing      Rowing           SAIN, David     CRO   
      30761  2012     London      Rowing      Rowing      SINKOVIC, Martin     CRO   
      30762  2012     London      Rowing      Rowing      SINKOVIC, Valent     CRO   
      30872  2012     London    Shooting    Shooting  CERNOGORAZ, Giovanni     CRO   
      
            Gender             Event   Medal  
      20135    Men        Basketball  Silver  
      20136    Men        Basketball  Silver  
      20137    Men        Basketball  Silver  
      20138    Men        Basketball  Silver  
      20139    Men        Basketball  Silver  
      ...      ...               ...     ...  
      30759    Men  Quadruple Sculls  Silver  
      30760    Men  Quadruple Sculls  Silver  
      30761    Men  Quadruple Sculls  Silver  
      30762    Men  Quadruple Sculls  Silver  
      30872    Men              Trap    Gold  
      
      [108 rows x 9 columns]),
     (('CRO', 'Women'),
             Year     City      Sport Discipline            Athlete Country Gender  \
      27685  2008  Beijing  Athletics  Athletics     VLASIC, Blanka     CRO  Women   
      28852  2008  Beijing   Shooting   Shooting   PEJCIC, Snjezana     CRO  Women   
      28977  2008  Beijing  Taekwondo  Taekwondo    ZUBCIC, Martina     CRO  Women   
      28981  2008  Beijing  Taekwondo  Taekwondo      SARIC, Sandra     CRO  Women   
      29716  2012   London  Athletics  Athletics   PERKOVIC, Sandra     CRO  Women   
      30905  2012   London  Taekwondo  Taekwondo  ZANINOVIC, Lucija     CRO  Women   
      
                                Event   Medal  
      27685                 High Jump  Silver  
      28852  10M Air Rifle (40 Shots)  Bronze  
      28977                49 - 57 KG  Bronze  
      28981                57 - 67 KG  Bronze  
      29716              Discus Throw    Gold  
      30905                   - 49 KG  Bronze  ),
     (('CUB', 'Men'),
             Year      City          Sport           Discipline  \
      358    1900     Paris        Fencing              Fencing   
      362    1900     Paris        Fencing              Fencing   
      858    1904  St Louis        Fencing              Fencing   
      859    1904  St Louis        Fencing              Fencing   
      860    1904  St Louis        Fencing              Fencing   
      ...     ...       ...            ...                  ...   
      30848  2012    London       Shooting             Shooting   
      30916  2012    London      Taekwondo            Taekwondo   
      31086  2012    London  Weightlifting        Weightlifting   
      31119  2012    London      Wrestling  Wrestling Freestyle   
      31137  2012    London      Wrestling  Wrestling Freestyle   
      
                            Athlete Country Gender                       Event  \
      358              FONST, Ramon     CUB    Men             Épée Individual   
      362              FONST, Ramon     CUB    Men  Épée, Amateurs And Masters   
      858    VAN ZO POST, Albertson     CUB    Men             Épée Individual   
      859              FONST, Ramon     CUB    Men             Épée Individual   
      860           TATHAM, Charles     CUB    Men             Épée Individual   
      ...                       ...     ...    ...                         ...   
      30848            PUPO, Leuris     CUB    Men            25M Rapid Pistol   
      30916      DESPAIGNE, Robelis     CUB    Men                     + 80 KG   
      31086  CAMBAR RODRIGUEZ, Ivan     CUB    Men                        77KG   
      31119      LOPEZ AZCUY, Livan     CUB    Men                    Wf 66 KG   
      31137     LOPEZ NUNEZ, Mijain     CUB    Men                   Wg 120 KG   
      
              Medal  
      358      Gold  
      362    Silver  
      858    Bronze  
      859      Gold  
      860    Silver  
      ...       ...  
      30848    Gold  
      30916  Bronze  
      31086  Bronze  
      31119  Bronze  
      31137    Gold  
      
      [310 rows x 9 columns]),
     (('CUB', 'Women'),
             Year     City      Sport Discipline                        Athlete  \
      11917  1968   Mexico  Athletics  Athletics  COBIAN HECHEVARRIA, Miguelina   
      11918  1968   Mexico  Athletics  Athletics         ELEJALDE DIAZ, Marlene   
      11919  1968   Mexico  Athletics  Athletics         QUESADA DIAZ, Violetta   
      11920  1968   Mexico  Athletics  Athletics      ROMAY MARTINEZ, Fulgencia   
      12904  1972   Munich  Athletics  Athletics            CHIVAS BARO, Silvia   
      ...     ...      ...        ...        ...                            ...   
      28961  2008  Beijing  Taekwondo  Taekwondo             MONTEJO, Daynellis   
      29718  2012   London  Athletics  Athletics               BARRIOS, Yarelys   
      29758  2012   London  Athletics  Athletics                SILVA, Yarisley   
      30591  2012   London       Judo       Judo                  ORTIZ, Idalys   
      30596  2012   London       Judo       Judo           BERMOY ACOSTA, Yanet   
      
            Country Gender         Event   Medal  
      11917     CUB  Women  4X100M Relay  Silver  
      11918     CUB  Women  4X100M Relay  Silver  
      11919     CUB  Women  4X100M Relay  Silver  
      11920     CUB  Women  4X100M Relay  Silver  
      12904     CUB  Women          100M  Bronze  
      ...       ...    ...           ...     ...  
      28961     CUB  Women       - 49 KG  Bronze  
      29718     CUB  Women  Discus Throw  Bronze  
      29758     CUB  Women    Pole Vault  Silver  
      30591     CUB  Women        + 78KG    Gold  
      30596     CUB  Women     48 - 52KG  Silver  
      
      [100 rows x 9 columns]),
     (('CYP', 'Men'),
             Year    City    Sport Discipline           Athlete Country Gender  \
      30816  2012  London  Sailing    Sailing  KONTIDES, Pavlos     CYP    Men   
      
             Event   Medal  
      30816  Laser  Silver  ),
     (('CZE', 'Men'),
             Year     City              Sport         Discipline  \
      21714  1996  Atlanta          Athletics          Athletics   
      21736  1996  Atlanta          Athletics          Athletics   
      21973  1996  Atlanta      Canoe / Kayak    Canoe / Kayak F   
      21976  1996  Atlanta      Canoe / Kayak    Canoe / Kayak F   
      22043  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22048  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22049  1996  Atlanta      Canoe / Kayak    Canoe / Kayak S   
      22891  1996  Atlanta           Shooting           Shooting   
      23639  2000   Sydney          Athletics          Athletics   
      23663  2000   Sydney          Athletics          Athletics   
      23909  2000   Sydney             Boxing             Boxing   
      23986  2000   Sydney      Canoe / Kayak    Canoe / Kayak S   
      23987  2000   Sydney      Canoe / Kayak    Canoe / Kayak S   
      24858  2000   Sydney           Shooting           Shooting   
      24878  2000   Sydney           Shooting           Shooting   
      24993  2000   Sydney          Triathlon          Triathlon   
      25656  2004   Athens          Athletics          Athletics   
      25673  2004   Athens          Athletics          Athletics   
      25996  2004   Athens      Canoe / Kayak    Canoe / Kayak S   
      25997  2004   Athens      Canoe / Kayak    Canoe / Kayak S   
      26628  2004   Athens  Modern Pentathlon    Modern Pentath.   
      26756  2004   Athens             Rowing             Rowing   
      26757  2004   Athens             Rowing             Rowing   
      26758  2004   Athens             Rowing             Rowing   
      26759  2004   Athens             Rowing             Rowing   
      28010  2008  Beijing      Canoe / Kayak    Canoe / Kayak S   
      28011  2008  Beijing      Canoe / Kayak    Canoe / Kayak S   
      28788  2008  Beijing             Rowing             Rowing   
      28886  2008  Beijing           Shooting           Shooting   
      29738  2012   London          Athletics          Athletics   
      29930  2012   London              Canoe       Canoe Slalom   
      29985  2012   London              Canoe       Canoe Sprint   
      29986  2012   London              Canoe       Canoe Sprint   
      29987  2012   London              Canoe       Canoe Sprint   
      29988  2012   London              Canoe       Canoe Sprint   
      30075  2012   London            Cycling      Mountain Bike   
      30635  2012   London  Modern Pentathlon  Modern Pentathlon   
      30780  2012   London             Rowing             Rowing   
      
                        Athlete Country Gender  \
      21714       DVORAK, Tomas     CZE    Men   
      21736        ZELEZNY, Jan     CZE    Men   
      21973      DOKTOR, Martin     CZE    Men   
      21976      DOKTOR, Martin     CZE    Men   
      22043      POLLERT, Lukas     CZE    Men   
      22048         ROHAN, Jiri     CZE    Men   
      22049     SIMEK, Miroslav     CZE    Men   
      22891     JANUS, Miroslav     CZE    Men   
      23639       SEBRLE, Roman     CZE    Men   
      23663        ZELEZNY, Jan     CZE    Men   
      23909        KRAJ, Rudolf     CZE    Men   
      23986        JIRAS, Marek     CZE    Men   
      23987        MADER, Tomas     CZE    Men   
      24858        TENK, Martin     CZE    Men   
      24878         MALEK, Petr     CZE    Men   
      24993         REHULA, Jan     CZE    Men   
      25656       SEBRLE, Roman     CZE    Men   
      25673      BABA, Jaroslav     CZE    Men   
      25996    STEPANEK, Ondrej     CZE    Men   
      25997      VOLF, Jaroslav     CZE    Men   
      26628     CAPALINI, Libor     CZE    Men   
      26756        HANAK, Jakub     CZE    Men   
      26757        JIRKA, David     CZE    Men   
      26758        KARAS, Tomas     CZE    Men   
      26759      KOPRIVA, David     CZE    Men   
      28010    STEPANEK, Ondrej     CZE    Men   
      28011      VOLF, Jaroslav     CZE    Men   
      28788       SYNEK, Ondrej     CZE    Men   
      28886   KOSTELECKY, David     CZE    Men   
      29738   VESELY, Vitezslav     CZE    Men   
      29930  HRADILEK, Vavrinec     CZE    Men   
      29985       DOSTAL, Josef     CZE    Men   
      29986       HAVEL, Daniel     CZE    Men   
      29987         STERBA, Jan     CZE    Men   
      29988       TREFIL, Lukas     CZE    Men   
      30075   KULHAVY, Jaroslav     CZE    Men   
      30635      SVOBODA, David     CZE    Men   
      30780       SYNEK, Ondrej     CZE    Men   
      
                                              Event   Medal  
      21714                               Decathlon  Bronze  
      21736                           Javelin Throw    Gold  
      21973                C-1 1000M (Canoe Single)    Gold  
      21976                 C-1 500M (Canoe Single)    Gold  
      22043                      C-1 (Canoe Single)  Silver  
      22048                      C-2 (Canoe Double)  Silver  
      22049                      C-2 (Canoe Double)  Silver  
      22891        50M Running Target (30+30 Shots)  Bronze  
      23639                               Decathlon  Silver  
      23663                           Javelin Throw    Gold  
      23909           75 - 81KG (Light-Heavyweight)  Silver  
      23986                      C-2 (Canoe Double)  Bronze  
      23987                      C-2 (Canoe Double)  Bronze  
      24858                   50M Pistol (60 Shots)  Bronze  
      24878                     Skeet (125 Targets)  Silver  
      24993                              Individual  Bronze  
      25656                               Decathlon    Gold  
      25673                               High Jump  Bronze  
      25996                      C-2 (Canoe Double)  Bronze  
      25997                      C-2 (Canoe Double)  Bronze  
      26628                  Individual Competition  Bronze  
      26756  Quadruple Sculls Without Coxswain (4X)  Silver  
      26757  Quadruple Sculls Without Coxswain (4X)  Silver  
      26758  Quadruple Sculls Without Coxswain (4X)  Silver  
      26759  Quadruple Sculls Without Coxswain (4X)  Silver  
      28010                      C-2 (Canoe Double)  Silver  
      28011                      C-2 (Canoe Double)  Silver  
      28788                      Single Sculls (1X)  Silver  
      28886                      Trap (125 Targets)    Gold  
      29738                           Javelin Throw  Bronze  
      29930                            K-1 (Single)  Silver  
      29985                               K-4 1000M  Bronze  
      29986                               K-4 1000M  Bronze  
      29987                               K-4 1000M  Bronze  
      29988                               K-4 1000M  Bronze  
      30075                           Cross-Country    Gold  
      30635                              Individual    Gold  
      30780                           Single Sculls  Silver  ),
     (('CZE', 'Women'),
             Year     City          Sport       Discipline               Athlete  \
      21765  1996  Atlanta      Athletics        Athletics     KASPARKOVA, Sarka   
      22054  1996  Atlanta  Canoe / Kayak  Canoe / Kayak S  HILGERTOVA, Stepanka   
      22979  1996  Atlanta         Tennis           Tennis         NOVOTNA, Jana   
      22980  1996  Atlanta         Tennis           Tennis        SUKOVA, Helena   
      22984  1996  Atlanta         Tennis           Tennis         NOVOTNA, Jana   
      23996  2000   Sydney  Canoe / Kayak  Canoe / Kayak S  HILGERTOVA, Stepanka   
      26804  2004   Athens        Sailing          Sailing        SMIDOVA, Lenka   
      26838  2004   Athens       Shooting         Shooting      EMMONS, Katerina   
      26849  2004   Athens       Shooting         Shooting         HYKOVA, Lenka   
      27690  2008  Beijing      Athletics        Athletics    SPOTAKOVA, Barbora   
      28853  2008  Beijing       Shooting         Shooting      EMMONS, Katerina   
      28869  2008  Beijing       Shooting         Shooting      EMMONS, Katerina   
      29635  2012   London      Athletics        Athletics       HEJNOVA, Zuzana   
      29739  2012   London      Athletics        Athletics    SPOTAKOVA, Barbora   
      30782  2012   London         Rowing           Rowing       KNAPKOVA, Mirka   
      30859  2012   London       Shooting         Shooting       SYKOROVA, Adela   
      30942  2012   London         Tennis           Tennis    HLAVACKOVA, Andrea   
      30943  2012   London         Tennis           Tennis       HRADECKA, Lucie   
      
            Country Gender                               Event   Medal  
      21765     CZE  Women                         Triple Jump  Bronze  
      22054     CZE  Women                  K-1 (Kayak Single)    Gold  
      22979     CZE  Women                             Doubles  Silver  
      22980     CZE  Women                             Doubles  Silver  
      22984     CZE  Women                             Singles  Bronze  
      23996     CZE  Women                  K-1 (Kayak Single)    Gold  
      26804     CZE  Women       Single-Handed Dinghy (Europe)  Silver  
      26838     CZE  Women            10M Air Rifle (40 Shots)  Bronze  
      26849     CZE  Women            25M Pistol (30+30 Shots)  Silver  
      27690     CZE  Women                       Javelin Throw    Gold  
      28853     CZE  Women            10M Air Rifle (40 Shots)    Gold  
      28869     CZE  Women  50M Rifle 3 Positions (3X20 Shots)  Silver  
      29635     CZE  Women                        400M Hurdles  Bronze  
      29739     CZE  Women                       Javelin Throw    Gold  
      30782     CZE  Women                       Single Sculls    Gold  
      30859     CZE  Women               50M Rifle 3 Positions  Bronze  
      30942     CZE  Women                             Doubles  Silver  
      30943     CZE  Women                             Doubles  Silver  ),
     (('DEN', 'Men'),
             Year    City          Sport     Discipline                  Athlete  \
      69     1896  Athens        Fencing        Fencing          NIELSEN, Holger   
      120    1896  Athens       Shooting       Shooting          NIELSEN, Holger   
      125    1896  Athens       Shooting       Shooting          NIELSEN, Holger   
      129    1896  Athens       Shooting       Shooting            JENSEN, Viggo   
      144    1896  Athens  Weightlifting  Weightlifting            JENSEN, Viggo   
      ...     ...     ...            ...            ...                      ...   
      30744  2012  London         Rowing         Rowing          RASMUSSEN, Mads   
      30801  2012  London        Sailing        Sailing              LANG, Peter   
      30802  2012  London        Sailing        Sailing        NORREGAARD, Allan   
      30813  2012  London        Sailing        Sailing  HOGH-CHRISTENSEN, Jonas   
      30867  2012  London       Shooting       Shooting          GOLDING, Anders   
      
            Country Gender                             Event   Medal  
      69        DEN    Men                  Sabre Individual  Bronze  
      120       DEN    Men  25M Rapid Fire Pistol (60 Shots)  Bronze  
      125       DEN    Men             50M Pistol (60 Shots)  Silver  
      129       DEN    Men                  Army Rifle, 300M  Bronze  
      144       DEN    Men       Heavyweight - One Hand Lift  Silver  
      ...       ...    ...                               ...     ...  
      30744     DEN    Men               Lightweight Doubles    Gold  
      30801     DEN    Men                      49Er - Skiff  Bronze  
      30802     DEN    Men                      49Er - Skiff  Bronze  
      30813     DEN    Men                              Finn  Silver  
      30867     DEN    Men                             Skeet  Silver  
      
      [416 rows x 9 columns]),
     (('DEN', 'Women'),
             Year         City       Sport Discipline  \
      2790   1912    Stockholm      Tennis     Tennis   
      2826   1920      Antwerp    Aquatics     Diving   
      4473   1924        Paris     Fencing    Fencing   
      4474   1924        Paris     Fencing    Fencing   
      5744   1932  Los Angeles    Aquatics   Swimming   
      ...     ...          ...         ...        ...   
      27401  2008      Beijing    Aquatics   Swimming   
      28094  2008      Beijing  Equestrian   Dressage   
      28095  2008      Beijing  Equestrian   Dressage   
      29789  2012       London   Badminton  Badminton   
      30783  2012       London      Rowing     Rowing   
      
                                       Athlete Country Gender              Event  \
      2790   CASTENSCHIOLD, Thora Gerda Sophie     DEN  Women     Singles Indoor   
      2826            FRYLAND CLAUSEN, Stefani     DEN  Women       10M Platform   
      4473                    HECKSCHER, Grete     DEN  Women    Foil Individual   
      4474               OSIIER, Ellen Ottilia     DEN  Women    Foil Individual   
      5744           JACOBSEN, Else Agnes Ella     DEN  Women  200M Breaststroke   
      ...                                  ...     ...    ...                ...   
      27401                       FRIIS, Lotte     DEN  Women     800M Freestyle   
      28094                     VAN OLST, Anne     DEN  Women               Team   
      28095     ZU-SAYN WITTGENSTEIN, Nathalie     DEN  Women               Team   
      29789               PEDERSEN, Christinna     DEN  Women            Doubles   
      30783                 ERICHSEN, Fie Udby     DEN  Women      Single Sculls   
      
              Medal  
      2790   Silver  
      2826     Gold  
      4473   Bronze  
      4474     Gold  
      5744   Bronze  
      ...       ...  
      27401  Bronze  
      28094  Bronze  
      28095  Bronze  
      29789  Bronze  
      30783  Silver  
      
      [91 rows x 9 columns]),
     (('DJI', 'Men'),
             Year   City      Sport Discipline               Athlete Country Gender  \
      18422  1988  Seoul  Athletics  Athletics  AHMED SALAH, Hussein     DJI    Men   
      
                Event   Medal  
      18422  Marathon  Bronze  ),
     (('DOM', 'Men'),
             Year         City      Sport Discipline                  Athlete  \
      17035  1984  Los Angeles     Boxing     Boxing          NOLASCO, Pedres   
      25578  2004       Athens  Athletics  Athletics           SANCHEZ, Felix   
      27916  2008      Beijing     Boxing     Boxing              DIAZ, Felix   
      28967  2008      Beijing  Taekwondo  Taekwondo  MERCEDES, Yulis Gabriel   
      29625  2012       London  Athletics  Athletics         SANTOS, Luguelin   
      29630  2012       London  Athletics  Athletics           SANCHEZ, Felix   
      
            Country Gender                     Event   Medal  
      17035     DOM    Men  51 - 54KG (Bantamweight)  Bronze  
      25578     DOM    Men              400M Hurdles    Gold  
      27916     DOM    Men                60 - 64 KG    Gold  
      28967     DOM    Men                   - 58 KG  Silver  
      29625     DOM    Men                      400M  Silver  
      29630     DOM    Men              400M Hurdles    Gold  ),
     (('ECU', 'Men'),
             Year     City      Sport Discipline           Athlete Country Gender  \
      21622  1996  Atlanta  Athletics  Athletics  PEREZ, Jefferson     ECU    Men   
      27580  2008  Beijing  Athletics  Athletics  PEREZ, Jefferson     ECU    Men   
      
                 Event   Medal  
      21622  20KM Walk    Gold  
      27580  20KM Walk  Silver  ),
     (('EGY', 'Men'),
             Year         City          Sport           Discipline  \
      5006   1928    Amsterdam       Aquatics               Diving   
      5010   1928    Amsterdam       Aquatics               Diving   
      5673   1928    Amsterdam  Weightlifting        Weightlifting   
      5712   1928    Amsterdam      Wrestling      Wrestling Gre-R   
      7147   1936       Berlin  Weightlifting        Weightlifting   
      7149   1936       Berlin  Weightlifting        Weightlifting   
      7155   1936       Berlin  Weightlifting        Weightlifting   
      7157   1936       Berlin  Weightlifting        Weightlifting   
      7159   1936       Berlin  Weightlifting        Weightlifting   
      7959   1948       London  Weightlifting        Weightlifting   
      7962   1948       London  Weightlifting        Weightlifting   
      7963   1948       London  Weightlifting        Weightlifting   
      8002   1948       London      Wrestling      Wrestling Gre-R   
      8015   1948       London      Wrestling      Wrestling Gre-R   
      8892   1952     Helsinki      Wrestling      Wrestling Gre-R   
      10085  1960         Rome         Boxing               Boxing   
      10652  1960         Rome      Wrestling      Wrestling Gre-R   
      17642  1984  Los Angeles           Judo                 Judo   
      25883  2004       Athens         Boxing               Boxing   
      25917  2004       Athens         Boxing               Boxing   
      25921  2004       Athens         Boxing               Boxing   
      26949  2004       Athens      Taekwondo            Taekwondo   
      27169  2004       Athens      Wrestling      Wrestling Gre-R   
      28635  2008      Beijing           Judo                 Judo   
      30145  2012       London        Fencing              Fencing   
      31089  2012       London  Weightlifting        Weightlifting   
      31158  2012       London      Wrestling  Wrestling Freestyle   
      
                                  Athlete Country Gender  \
      5006                 SIMAIKA, Farid     EGY    Men   
      5010                 SIMAIKA, Farid     EGY    Men   
      5673      NOSSEIR, El Sayed Mohamed     EGY    Men   
      5712             MOUSTAPHA, Ibrahim     EGY    Men   
      7147       SHAMS, Ibrahim Hassanein     EGY    Men   
      7149         SOLIMAN, Saleh Mohamed     EGY    Men   
      7155    MESBAH, Anwar Mohamed Ahmed     EGY    Men   
      7157       EL TOUNY, Khadr El Sayed     EGY    Men   
      7159                 WASIF, Ibrahim     EGY    Men   
      7959                 FAYAD, Mahmoud     EGY    Men   
      7962       SHAMS, Ibrahim Hassanein     EGY    Men   
      7963         HAMOUDA, Attia Mohamed     EGY    Men   
      8002            HASSAN ALI, Mahmoud     EGY    Men   
      8015                 ORABI, Ibrahim     EGY    Men   
      8892        RASHED, Abdel Aal Ahmed     EGY    Men   
      10085        EL GINDY, Abdel Moneim     EGY    Men   
      10652                  SAYED, Osman     EGY    Men   
      17642              RASHWAN, Mohamed     EGY    Men   
      25883                  ALY, Mohamed     EGY    Men   
      25917                 ISMAIL, Ahmed     EGY    Men   
      25921              ELSAYED, Mohamed     EGY    Men   
      26949                BAYOUMI, Tamer     EGY    Men   
      27169          GABER IBRAHIM, Karam     EGY    Men   
      28635                MESBAH, Hesham     EGY    Men   
      30145       ABOUELKASSEM, Alaaeldin     EGY    Men   
      31089  ABDELAZIM, Tarek Yehia Fouad     EGY    Men   
      31158  EBRAHIM, Karam Mohamed Gaber     EGY    Men   
      
                                              Event   Medal  
      5006                             10M Platform  Silver  
      5010                           3M Springboard  Bronze  
      5673   75 - 82.5KG, Total (Light-Heavyweight)    Gold  
      5712          75 - 82.5KG (Light-Heavyweight)    Gold  
      7147            - 60KG, Total (Featherweight)  Bronze  
      7149            - 60KG, Total (Featherweight)  Silver  
      7155         60 - 67.5KG, Total (Lightweight)    Gold  
      7157        67.5 - 75KG, Total (Middleweight)    Gold  
      7159   75 - 82.5KG, Total (Light-Heavyweight)  Bronze  
      7959         56 - 60KG, Total (Featherweight)    Gold  
      7962         60 - 67.5KG, Total (Lightweight)    Gold  
      7963         60 - 67.5KG, Total (Lightweight)  Silver  
      8002                 52 - 57KG (Bantamweight)  Silver  
      8015            79 - 87KG (Light-Heavyweight)  Bronze  
      8892                57 - 61KG (Featherweight)  Bronze  
      10085                      - 51KG (Flyweight)  Bronze  
      10652                      - 52KG (Flyweight)  Silver  
      17642                           Open Category  Silver  
      25883              + 91KG (Super Heavyweight)  Silver  
      25917           75 - 81KG (Light-Heavyweight)  Bronze  
      25921                 81 - 91KG (Heavyweight)  Bronze  
      26949                                 - 58 KG  Bronze  
      27169                               84 - 96KG    Gold  
      28635                81 - 90KG (Middleweight)  Bronze  
      30145                         Foil Individual  Silver  
      31089                                    85KG  Bronze  
      31158                                Wg 84 KG  Silver  ),
     (('EGY', 'Women'),
             Year    City          Sport     Discipline  \
      31082  2012  London  Weightlifting  Weightlifting   
      
                                         Athlete Country Gender Event   Medal  
      31082  ABIR ABDELRAHMAN, Khalil Mahmoud K.     EGY  Women  75KG  Silver  ),
     (('ERI', 'Men'),
             Year    City      Sport Discipline            Athlete Country Gender  \
      25532  2004  Athens  Athletics  Athletics  TADESSE, Zersenay     ERI    Men   
      
              Event   Medal  
      25532  10000M  Bronze  ),
     (('ESP', 'Men'),
             Year     City          Sport     Discipline  \
      306    1900    Paris  Basque Pelota  Basque Pelota   
      307    1900    Paris  Basque Pelota  Basque Pelota   
      3315   1920  Antwerp       Football       Football   
      3316   1920  Antwerp       Football       Football   
      3317   1920  Antwerp       Football       Football   
      ...     ...      ...            ...            ...   
      29936  2012   London          Canoe   Canoe Sprint   
      29951  2012   London          Canoe   Canoe Sprint   
      30906  2012   London      Taekwondo      Taekwondo   
      30931  2012   London      Taekwondo      Taekwondo   
      30959  2012   London      Triathlon      Triathlon   
      
                                 Athlete Country Gender        Event   Medal  
      306     De AMEZOLA y ASPIZUA, José     ESP    Men  Cesta Punta    Gold  
      307    VILLOTA BAQUIOLA, Francisco     ESP    Men  Cesta Punta    Gold  
      3315                ACEDO, Domingo     ESP    Men     Football  Silver  
      3316           ARABOLAZA, Patricio     ESP    Men     Football  Silver  
      3317               ARRATE, Mariano     ESP    Men     Football  Silver  
      ...                            ...     ...    ...          ...     ...  
      29936                   CAL, David     ESP    Men    C-1 1000M  Silver  
      29951       CRAVIOTTO RIVERO, Saul     ESP    Men     K-1 200M  Silver  
      30906       GONZALEZ BONILLA, Joel     ESP    Men      - 58 KG    Gold  
      30931        GARCIA HEMME, Nicolas     ESP    Men   68 - 80 KG  Silver  
      30959                GOMEZ, Javier     ESP    Men   Individual  Silver  
      
      [332 rows x 9 columns]),
     (('ESP', 'Women'),
             Year       City          Sport           Discipline  \
      20598  1992  Barcelona     Gymnastics          Rhythmic G.   
      20747  1992  Barcelona         Hockey               Hockey   
      20748  1992  Barcelona         Hockey               Hockey   
      20749  1992  Barcelona         Hockey               Hockey   
      20750  1992  Barcelona         Hockey               Hockey   
      ...     ...        ...            ...                  ...   
      30805  2012     London        Sailing              Sailing   
      30824  2012     London        Sailing              Sailing   
      30903  2012     London      Taekwondo            Taekwondo   
      31081  2012     London  Weightlifting        Weightlifting   
      31124  2012     London      Wrestling  Wrestling Freestyle   
      
                                 Athlete Country Gender                 Event  \
      20598     PASCUAL GRACIA, Carolina     ESP  Women  Individual All-Round   
      20747     BAREA, Maria Del Carme N     ESP  Women                Hockey   
      20748                BARRIO, Sonia     ESP  Women                Hockey   
      20749  COGHEN ALBERDINGO, Mercedes     ESP  Women                Hockey   
      20750          CORRES GINER, Celia     ESP  Women                Hockey   
      ...                            ...     ...    ...                   ...   
      30805      TORO PRIETO PUGA, Sofia     ESP  Women            Elliott 6M   
      30824               ALABAU, Marina     ESP  Women                  Rs:X   
      30903      YAGUE ENRIQUE, Brigitte     ESP  Women               - 49 KG   
      31081        VALENTIN PEREZ, Lidia     ESP  Women                  75KG   
      31124                 UNDA, Maider     ESP  Women              Wf 72 KG   
      
              Medal  
      20598  Silver  
      20747    Gold  
      20748    Gold  
      20749    Gold  
      20750    Gold  
      ...       ...  
      30805    Gold  
      30824    Gold  
      30903  Silver  
      31081    Gold  
      31124  Bronze  
      
      [110 rows x 9 columns]),
     (('EST', 'Men'),
             Year       City          Sport           Discipline  \
      3093   1920    Antwerp      Athletics            Athletics   
      4076   1920    Antwerp  Weightlifting        Weightlifting   
      4081   1920    Antwerp  Weightlifting        Weightlifting   
      4324   1924      Paris      Athletics            Athletics   
      4953   1924      Paris  Weightlifting        Weightlifting   
      4959   1924      Paris  Weightlifting        Weightlifting   
      4961   1924      Paris  Weightlifting        Weightlifting   
      4987   1924      Paris      Wrestling      Wrestling Gre-R   
      4998   1924      Paris      Wrestling      Wrestling Gre-R   
      5633   1928  Amsterdam        Sailing              Sailing   
      5634   1928  Amsterdam        Sailing              Sailing   
      5635   1928  Amsterdam        Sailing              Sailing   
      5636   1928  Amsterdam        Sailing              Sailing   
      5637   1928  Amsterdam        Sailing              Sailing   
      5665   1928  Amsterdam  Weightlifting        Weightlifting   
      5685   1928  Amsterdam      Wrestling      Wrestling Free.   
      5703   1928  Amsterdam      Wrestling      Wrestling Gre-R   
      5708   1928  Amsterdam      Wrestling      Wrestling Gre-R   
      6585   1936     Berlin         Boxing               Boxing   
      7150   1936     Berlin  Weightlifting        Weightlifting   
      7166   1936     Berlin      Wrestling      Wrestling Free.   
      7182   1936     Berlin      Wrestling      Wrestling Free.   
      7187   1936     Berlin      Wrestling      Wrestling Gre-R   
      7192   1936     Berlin      Wrestling      Wrestling Gre-R   
      7201   1936     Berlin      Wrestling      Wrestling Gre-R   
      21003  1992  Barcelona        Sailing              Sailing   
      21004  1992  Barcelona        Sailing              Sailing   
      23638  2000     Sydney      Athletics            Athletics   
      24585  2000     Sydney           Judo                 Judo   
      24621  2000     Sydney           Judo                 Judo   
      25658  2004     Athens      Athletics            Athletics   
      26580  2004     Athens           Judo                 Judo   
      26774  2004     Athens         Rowing               Rowing   
      27666  2008    Beijing      Athletics            Athletics   
      28658  2008    Beijing         Rowing               Rowing   
      28659  2008    Beijing         Rowing               Rowing   
      29715  2012     London      Athletics            Athletics   
      31138  2012     London      Wrestling  Wrestling Freestyle   
      
                                  Athlete Country Gender  \
      3093                 LOSSMANN, Jüri     EST    Men   
      4076                SCHMIDT, Alfred     EST    Men   
      4081                NEULAND, Alfred     EST    Men   
      4324   KLUMBERG-KOLMPERE, Alexander     EST    Men   
      4953                 TAMMER, Harald     EST    Men   
      4959                   KIKKAS, Jaan     EST    Men   
      4961                NEULAND, Alfred     EST    Men   
      4987                 PÜTSEP, Eduard     EST    Men   
      4998               STEINBERG, Roman     EST    Men   
      5633                  FAEHLMANN, A.     EST    Men   
      5634                  FAEHLMANN, G.     EST    Men   
      5635                      VOGDT, E.     EST    Men   
      5636                  VON WIREN, W.     EST    Men   
      5637                   WEKSCHIN, N.     EST    Men   
      5665                LUHAÄÄR, Arnold     EST    Men   
      5685                   KAPP, Osvald     EST    Men   
      5703                       WALI, W.     EST    Men   
      5708                KUSNETS, Albert     EST    Men   
      6585              STEPULOV, Nikolai     EST    Men   
      7150                LUHAÄÄR, Arnold     EST    Men   
      7166             PALUSALU, Kristjan     EST    Men   
      7182              NEO, Ago (August)     EST    Men   
      7187             PALUSALU, Kristjan     EST    Men   
      7192                 VÄLI, Voldemar     EST    Men   
      7201              NEO, Ago (August)     EST    Men   
      21003                 TONISTE, Tonu     EST    Men   
      21004               TONISTE, Toomas     EST    Men   
      23638                    NOOL, Erki     EST    Men   
      24585             PERTELSON, Indrek     EST    Men   
      24621              BUDOLIN, Aleksei     EST    Men   
      25658           TAMMERT, Aleksander     EST    Men   
      26580             PERTELSON, Indrek     EST    Men   
      26774                JAANSON, Jueri     EST    Men   
      27666                  KANTER, Gerd     EST    Men   
      28658               ENDREKSON, Tonu     EST    Men   
      28659                 JAANSON, Juri     EST    Men   
      29715                  KANTER, Gerd     EST    Men   
      31138                   NABI, Heiki     EST    Men   
      
                                                         Event   Medal  
      3093                                            Marathon  Silver  
      4076       - 60KG, One-Two Hand 3 Events (Featherweight)  Silver  
      4081    60 - 67.5KG, One-Two Hand 3 Events (Lightweight)    Gold  
      4324                                           Decathlon  Bronze  
      4953       + 82.5KG, One-Two Hand 5 Events (Heavyweight)  Bronze  
      4959   67.5 - 75KG, One-Two Hand 5 Events (Middleweight)  Bronze  
      4961   67.5 - 75KG, One-Two Hand 5 Events (Middleweight)  Silver  
      4987                               - 58KG (Bantamweight)    Gold  
      4998                          67.5 - 75KG (Middleweight)  Bronze  
      5633                                                  6M  Bronze  
      5634                                                  6M  Bronze  
      5635                                                  6M  Bronze  
      5636                                                  6M  Bronze  
      5637                                                  6M  Bronze  
      5665                       + 82.5KG, Total (Heavyweight)  Silver  
      5685                             61 - 66KG (Lightweight)    Gold  
      5703                           58 - 60KG (Featherweight)    Gold  
      5708                          67.5 - 75KG (Middleweight)  Bronze  
      6585                       57.15 - 61.24KG (Lightweight)  Silver  
      7150                       + 82.5KG, Total (Heavyweight)  Bronze  
      7166                                + 87KG (Heavyweight)    Gold  
      7182                       79 - 87KG (Light-Heavyweight)  Silver  
      7187                          + 87KG (Super Heavyweight)    Gold  
      7192                             61 - 66KG (Lightweight)  Bronze  
      7201                       79 - 87KG (Light-Heavyweight)  Bronze  
      21003                            470 - Two Person Dinghy  Bronze  
      21004                            470 - Two Person Dinghy  Bronze  
      23638                                          Decathlon    Gold  
      24585                              + 100KG (Heavyweight)  Bronze  
      24621                      73 - 81KG (Half-Middleweight)  Bronze  
      25658                                       Discus Throw  Bronze  
      26580                              + 100KG (Heavyweight)  Bronze  
      26774                                 Single Sculls (1X)  Silver  
      27666                                       Discus Throw    Gold  
      28658                                 Double Sculls (2X)  Silver  
      28659                                 Double Sculls (2X)  Silver  
      29715                                       Discus Throw  Bronze  
      31138                                          Wg 120 KG  Silver  ),
     (('EST', 'Women'),
             Year       City    Sport     Discipline         Athlete Country Gender  \
      20346  1992  Barcelona  Cycling  Cycling Track  SALUMAE, Erika     EST  Women   
      
              Event Medal  
      20346  Sprint  Gold  ),
     (('ETH', 'Men'),
             Year       City      Sport Discipline              Athlete Country  \
      10035  1960       Rome  Athletics  Athletics        BIKILA, Abebe     ETH   
      10937  1964      Tokyo  Athletics  Athletics        BIKILA, Abebe     ETH   
      11863  1968     Mexico  Athletics  Athletics          WOLDE, Mamo     ETH   
      11979  1968     Mexico  Athletics  Athletics          WOLDE, Mamo     ETH   
      12898  1972     Munich  Athletics  Athletics       YIFTER, Miruts     ETH   
      13030  1972     Munich  Athletics  Athletics          WOLDE, Mamo     ETH   
      15370  1980     Moscow  Athletics  Athletics      KEDIR, Mohammed     ETH   
      15371  1980     Moscow  Athletics  Athletics       YIFTER, Miruts     ETH   
      15400  1980     Moscow  Athletics  Athletics         TURA, Eshetu     ETH   
      15461  1980     Moscow  Athletics  Athletics       YIFTER, Miruts     ETH   
      19849  1992  Barcelona  Athletics  Athletics         ABEBE, Addis     ETH   
      19962  1992  Barcelona  Athletics  Athletics         BAYISA, Fita     ETH   
      21589  1996    Atlanta  Athletics  Athletics  GEBRSELASSIE, Haile     ETH   
      23514  2000     Sydney  Athletics  Athletics      MEZGEBU, Assefa     ETH   
      23515  2000     Sydney  Athletics  Athletics  GEBRSELASSIE, Haile     ETH   
      23623  2000     Sydney  Athletics  Athletics        WOLDE, Millon     ETH   
      23674  2000     Sydney  Athletics  Athletics        TOLA, Tesfaye     ETH   
      23676  2000     Sydney  Athletics  Athletics     ABERA, Gezahegne     ETH   
      25533  2004     Athens  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      25534  2004     Athens  Athletics  Athletics      SIHINE, Sileshi     ETH   
      25642  2004     Athens  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      27546  2008    Beijing  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      27547  2008    Beijing  Athletics  Athletics      SIHINE, Sileshi     ETH   
      27648  2008    Beijing  Athletics  Athletics     BEKELE, Kenenisa     ETH   
      27698  2008    Beijing  Athletics  Athletics       KEBEDE, Tsegay     ETH   
      29584  2012     London  Athletics  Athletics       BEKELE, Tariku     ETH   
      29696  2012     London  Athletics  Athletics   GEBREMESKEL, Dejen     ETH   
      
            Gender               Event   Medal  
      10035    Men            Marathon    Gold  
      10937    Men            Marathon    Gold  
      11863    Men              10000M  Silver  
      11979    Men            Marathon    Gold  
      12898    Men              10000M  Bronze  
      13030    Men            Marathon  Bronze  
      15370    Men              10000M  Bronze  
      15371    Men              10000M    Gold  
      15400    Men  3000M Steeplechase  Bronze  
      15461    Men               5000M    Gold  
      19849    Men              10000M  Bronze  
      19962    Men               5000M  Bronze  
      21589    Men              10000M    Gold  
      23514    Men              10000M  Bronze  
      23515    Men              10000M    Gold  
      23623    Men               5000M    Gold  
      23674    Men            Marathon  Bronze  
      23676    Men            Marathon    Gold  
      25533    Men              10000M    Gold  
      25534    Men              10000M  Silver  
      25642    Men               5000M  Silver  
      27546    Men              10000M    Gold  
      27547    Men              10000M  Silver  
      27648    Men               5000M    Gold  
      27698    Men            Marathon  Bronze  
      29584    Men              10000M  Bronze  
      29696    Men               5000M  Silver  ),
     (('ETH', 'Women'),
             Year       City      Sport Discipline            Athlete Country  \
      19853  1992  Barcelona  Athletics  Athletics      TULU, Derartu     ETH   
      21591  1996    Atlanta  Athletics  Athletics         WAMI, Gete     ETH   
      21751  1996    Atlanta  Athletics  Athletics       ROBA, Fatuma     ETH   
      23518  2000     Sydney  Athletics  Athletics      TULU, Derartu     ETH   
      23519  2000     Sydney  Athletics  Athletics         WAMI, Gete     ETH   
      23625  2000     Sydney  Athletics  Athletics         WAMI, Gete     ETH   
      25535  2004     Athens  Athletics  Athletics      TULU, Derartu     ETH   
      25537  2004     Athens  Athletics  Athletics  DIBABA, Ejegayehu     ETH   
      25643  2004     Athens  Athletics  Athletics   DIBABA, Tirunesh     ETH   
      25644  2004     Athens  Athletics  Athletics     DEFAR, Meseret     ETH   
      27549  2008    Beijing  Athletics  Athletics   DIBABA, Tirunesh     ETH   
      27650  2008    Beijing  Athletics  Athletics     DEFAR, Meseret     ETH   
      27651  2008    Beijing  Athletics  Athletics   DIBABA, Tirunesh     ETH   
      29585  2012     London  Athletics  Athletics   DIBABA, Tirunesh     ETH   
      29622  2012     London  Athletics  Athletics      ASSEFA, Sofia     ETH   
      29698  2012     London  Athletics  Athletics     DEFAR, Meseret     ETH   
      29700  2012     London  Athletics  Athletics   DIBABA, Tirunesh     ETH   
      29751  2012     London  Athletics  Athletics       GELANA, Tiki     ETH   
      
            Gender          Event   Medal  
      19853  Women         10000M    Gold  
      21591  Women         10000M  Bronze  
      21751  Women       Marathon    Gold  
      23518  Women         10000M    Gold  
      23519  Women         10000M  Silver  
      23625  Women          5000M  Bronze  
      25535  Women         10000M  Bronze  
      25537  Women         10000M  Silver  
      25643  Women          5000M  Bronze  
      25644  Women          5000M    Gold  
      27549  Women         10000M    Gold  
      27650  Women          5000M  Bronze  
      27651  Women          5000M    Gold  
      29585  Women         10000M    Gold  
      29622  Women  3000M Steeple  Silver  
      29698  Women          5000M    Gold  
      29700  Women          5000M  Bronze  
      29751  Women       Marathon    Gold  ),
     (('EUA', 'Men'),
             Year                   City      Sport       Discipline  \
      9019   1956  Melbourne / Stockholm  Athletics        Athletics   
      9035   1956  Melbourne / Stockholm  Athletics        Athletics   
      9039   1956  Melbourne / Stockholm  Athletics        Athletics   
      9040   1956  Melbourne / Stockholm  Athletics        Athletics   
      9041   1956  Melbourne / Stockholm  Athletics        Athletics   
      ...     ...                    ...        ...              ...   
      11517  1964                  Tokyo    Sailing          Sailing   
      11650  1964                  Tokyo  Wrestling  Wrestling Free.   
      11663  1964                  Tokyo  Wrestling  Wrestling Gre-R   
      11678  1964                  Tokyo  Wrestling  Wrestling Gre-R   
      11681  1964                  Tokyo  Wrestling  Wrestling Gre-R   
      
                          Athlete Country Gender                          Event  \
      9019    RICHTZENHAIN, Klaus     EUA    Men                          1500M   
      9035   HAAS, Karl-Friedrich     EUA    Men                           400M   
      9039        FÜTTERER, Heinz     EUA    Men                   4X100M Relay   
      9040        GERMAR, Manfred     EUA    Men                   4X100M Relay   
      9041        KNÖRZER, Lothar     EUA    Men                   4X100M Relay   
      ...                     ...     ...    ...                            ...   
      11517     KUHWEIDE, Wilhelm     EUA    Men    Single-Handed Dinghy (Finn)   
      11650    ROST, Klaus-Jürgen     EUA    Men        63 - 70KG (Lightweight)   
      11663    DIETRICH, Wilfried     EUA    Men     + 97KG (Super Heavyweight)   
      11678          METZ, Lothar     EUA    Men       78 - 87KG (Middleweight)   
      11681          KIEHL, Heinz     EUA    Men  87 - 97KG (Light-Heavyweight)   
      
              Medal  
      9019   Silver  
      9035   Silver  
      9039   Bronze  
      9040   Bronze  
      9041   Bronze  
      ...       ...  
      11517    Gold  
      11650  Silver  
      11663  Bronze  
      11678  Bronze  
      11681  Bronze  
      
      [205 rows x 9 columns]),
     (('EUA', 'Women'),
             Year                   City          Sport       Discipline  \
      8940   1956  Melbourne / Stockholm       Aquatics         Swimming   
      8941   1956  Melbourne / Stockholm       Aquatics         Swimming   
      9013   1956  Melbourne / Stockholm      Athletics        Athletics   
      9025   1956  Melbourne / Stockholm      Athletics        Athletics   
      9086   1956  Melbourne / Stockholm      Athletics        Athletics   
      9126   1956  Melbourne / Stockholm      Athletics        Athletics   
      9234   1956  Melbourne / Stockholm  Canoe / Kayak  Canoe / Kayak F   
      9284   1956  Melbourne / Stockholm     Equestrian         Dressage   
      9293   1956  Melbourne / Stockholm     Equestrian         Dressage   
      9294   1956  Melbourne / Stockholm     Equestrian         Dressage   
      9295   1956  Melbourne / Stockholm     Equestrian         Dressage   
      9296   1956  Melbourne / Stockholm     Equestrian         Dressage   
      9309   1956  Melbourne / Stockholm     Equestrian         Eventing   
      9310   1956  Melbourne / Stockholm     Equestrian         Eventing   
      9314   1956  Melbourne / Stockholm     Equestrian          Jumping   
      9324   1956  Melbourne / Stockholm     Equestrian          Jumping   
      9325   1956  Melbourne / Stockholm     Equestrian          Jumping   
      9796   1960                   Rome       Aquatics           Diving   
      9802   1960                   Rome       Aquatics           Diving   
      9825   1960                   Rome       Aquatics         Swimming   
      9827   1960                   Rome       Aquatics         Swimming   
      9837   1960                   Rome       Aquatics         Swimming   
      9838   1960                   Rome       Aquatics         Swimming   
      9839   1960                   Rome       Aquatics         Swimming   
      9840   1960                   Rome       Aquatics         Swimming   
      9861   1960                   Rome       Aquatics         Swimming   
      9862   1960                   Rome       Aquatics         Swimming   
      9863   1960                   Rome       Aquatics         Swimming   
      9864   1960                   Rome       Aquatics         Swimming   
      9940   1960                   Rome      Athletics        Athletics   
      9973   1960                   Rome      Athletics        Athletics   
      9974   1960                   Rome      Athletics        Athletics   
      9975   1960                   Rome      Athletics        Athletics   
      9976   1960                   Rome      Athletics        Athletics   
      9998   1960                   Rome      Athletics        Athletics   
      10001  1960                   Rome      Athletics        Athletics   
      10031  1960                   Rome      Athletics        Athletics   
      10045  1960                   Rome      Athletics        Athletics   
      10151  1960                   Rome  Canoe / Kayak  Canoe / Kayak F   
      10162  1960                   Rome  Canoe / Kayak  Canoe / Kayak F   
      10163  1960                   Rome  Canoe / Kayak  Canoe / Kayak F   
      10254  1960                   Rome        Fencing          Fencing   
      10679  1964                  Tokyo       Aquatics           Diving   
      10684  1964                  Tokyo       Aquatics           Diving   
      10904  1964                  Tokyo      Athletics        Athletics   
      10914  1964                  Tokyo      Athletics        Athletics   
      10950  1964                  Tokyo      Athletics        Athletics   
      11053  1964                  Tokyo  Canoe / Kayak  Canoe / Kayak F   
      11054  1964                  Tokyo  Canoe / Kayak  Canoe / Kayak F   
      11170  1964                  Tokyo        Fencing          Fencing   
      11186  1964                  Tokyo        Fencing          Fencing   
      11187  1964                  Tokyo        Fencing          Fencing   
      11188  1964                  Tokyo        Fencing          Fencing   
      11189  1964                  Tokyo        Fencing          Fencing   
      11340  1964                  Tokyo     Gymnastics      Artistic G.   
      
                                         Athlete Country Gender  \
      8940                  TEN ELSEN, Eva-Maria     EUA  Women   
      8941                    HAPPE-KREY, Ursula     EUA  Women   
      9013                     STUBNICK, Christa     EUA  Women   
      9025                     STUBNICK, Christa     EUA  Women   
      9086             KÖHLER-BIRKEMEYER, Gisela     EUA  Women   
      9126       WERNER-SCHULZE-ENTRUP, Marianne     EUA  Women   
      9234                         ZENZ, Therese     EUA  Women   
      9284                  LINSENHOFF, Liselott     EUA  Women   
      9293                                AFRIKA     EUA  Women   
      9294                    KÜPPERS, Anneliese     EUA  Women   
      9295                  LINSENHOFF, Liselott     EUA  Women   
      9296                    WEYGAND, Hannelore     EUA  Women   
      9309                              PRINZESS     EUA  Women   
      9310                                 SISSI     EUA  Women   
      9314                                 HALLA     EUA  Women   
      9324                                   ALA     EUA  Women   
      9325                                 HALLA     EUA  Women   
      9796           KRÄMER-ENGEL-GULBIN, Ingrid     EUA  Women   
      9802           KRÄMER-ENGEL-GULBIN, Ingrid     EUA  Women   
      9825                        GÖBEL, Barbara     EUA  Women   
      9827                    URSELMANN, Wiltrud     EUA  Women   
      9837                       BRUNNER, Ursula     EUA  Women   
      9838                      PECHSTEIN, Heidi     EUA  Women   
      9839                     STEFFIN, Christel     EUA  Women   
      9840                         WEISS, Gisela     EUA  Women   
      9861                       BRUNNER, Ursula     EUA  Women   
      9862                      FUHRMANN, Bärbel     EUA  Women   
      9863                         KÜPER, Ursula     EUA  Women   
      9864                       SCHMIDT, Ingrid     EUA  Women   
      9940                 HEINE, Judith (Jutta)     EUA  Women   
      9973                          BIECHL, Anni     EUA  Women   
      9974                 HEINE, Judith (Jutta)     EUA  Women   
      9975                    HENDRIX, Brunhilde     EUA  Women   
      9976           PENSBERGER-LANGBEIN, Martha     EUA  Women   
      9998                        DONATH, Ursula     EUA  Women   
      10001            KÖHLER-BIRKEMEYER, Gisela     EUA  Women   
      10031                CLAUS-LAUFER, Hildrun     EUA  Women   
      10045               LÜTTGE-HÜBNER, Johanna     EUA  Women   
      10151                        ZENZ, Therese     EUA  Women   
      10162                     HARTMANN, Ingrid     EUA  Women   
      10163                        ZENZ, Therese     EUA  Women   
      10254             SCHMID, Adelheid Barbara     EUA  Women   
      10679          KRÄMER-ENGEL-GULBIN, Ingrid     EUA  Women   
      10684          KRÄMER-ENGEL-GULBIN, Ingrid     EUA  Women   
      10904                RICHERT-BALZER, Karin     EUA  Women   
      10914                         LOTZ, Ingrid     EUA  Women   
      10950       GARISCH-CULMBERGER-BOY, Renate     EUA  Women   
      11053                      ESSER, Roswitha     EUA  Women   
      11054                ZIMMERMANN, Annemarie     EUA  Women   
      11170              MEES-VOLZ, Helga Margot     EUA  Women   
      11186              MEES-VOLZ, Helga Margot     EUA  Women   
      11187             SCHMID, Adelheid Barbara     EUA  Women   
      11188         THEUERKAUFF-VORBRICH, Gudrun     EUA  Women   
      11189  WEISS-SCHERBERGER, Rosemarie (Romy)     EUA  Women   
      11340                     RADOCHLA, Birgit     EUA  Women   
      
                               Event   Medal  
      8940         200M Breaststroke  Bronze  
      8941         200M Breaststroke    Gold  
      9013                      100M  Silver  
      9025                      200M  Silver  
      9086               80M Hurdles  Silver  
      9126                  Shot Put  Bronze  
      9234   K-1 500M (Kayak Single)  Silver  
      9284                Individual  Bronze  
      9293                      Team  Silver  
      9294                      Team  Silver  
      9295                      Team  Silver  
      9296                      Team  Silver  
      9309                      Team  Silver  
      9310                      Team  Silver  
      9314                Individual    Gold  
      9324                      Team    Gold  
      9325                      Team    Gold  
      9796              10M Platform    Gold  
      9802            3M Springboard    Gold  
      9825         200M Breaststroke  Bronze  
      9827         200M Breaststroke  Silver  
      9837    4X100M Freestyle Relay  Bronze  
      9838    4X100M Freestyle Relay  Bronze  
      9839    4X100M Freestyle Relay  Bronze  
      9840    4X100M Freestyle Relay  Bronze  
      9861       4X100M Medley Relay  Bronze  
      9862       4X100M Medley Relay  Bronze  
      9863       4X100M Medley Relay  Bronze  
      9864       4X100M Medley Relay  Bronze  
      9940                      200M  Silver  
      9973              4X100M Relay  Silver  
      9974              4X100M Relay  Silver  
      9975              4X100M Relay  Silver  
      9976              4X100M Relay  Silver  
      9998                      800M  Bronze  
      10001              80M Hurdles  Bronze  
      10031                Long Jump  Bronze  
      10045                 Shot Put  Silver  
      10151  K-1 500M (Kayak Single)  Silver  
      10162  K-2 500M (Kayak Double)  Silver  
      10163  K-2 500M (Kayak Double)  Silver  
      10254          Foil Individual    Gold  
      10679             10M Platform  Silver  
      10684           3M Springboard    Gold  
      10904              80M Hurdles    Gold  
      10914             Discus Throw  Silver  
      10950                 Shot Put  Silver  
      11053  K-2 500M (Kayak Double)    Gold  
      11054  K-2 500M (Kayak Double)    Gold  
      11170          Foil Individual  Silver  
      11186                Foil Team  Bronze  
      11187                Foil Team  Bronze  
      11188                Foil Team  Bronze  
      11189                Foil Team  Bronze  
      11340                    Vault  Silver  ),
     (('EUN', 'Men'),
             Year       City      Sport       Discipline                   Athlete  \
      19603  1992  Barcelona   Aquatics           Diving            SAUTIN, Dmitry   
      19628  1992  Barcelona   Aquatics         Swimming          POPOV, Alexander   
      19638  1992  Barcelona   Aquatics         Swimming          SELKOV, Vladimir   
      19655  1992  Barcelona   Aquatics         Swimming          SADOVYI, Evgueni   
      19667  1992  Barcelona   Aquatics         Swimming          SADOVYI, Evgueni   
      ...     ...        ...        ...              ...                       ...   
      21289  1992  Barcelona  Wrestling  Wrestling Gre-R       DOUGOUTCHIEV, Islam   
      21291  1992  Barcelona  Wrestling  Wrestling Gre-R    ISKANDARIAN, Mnatsakan   
      21293  1992  Barcelona  Wrestling  Wrestling Gre-R     TOURLYKHANOV, Daoulet   
      21296  1992  Barcelona  Wrestling  Wrestling Gre-R       KOGOUACHVILI, Gogui   
      21299  1992  Barcelona  Wrestling  Wrestling Gre-R  DEMIACHKIEVITCH, Serguei   
      
            Country Gender                          Event   Medal  
      19603     EUN    Men                 3M Springboard  Bronze  
      19628     EUN    Men                 100M Freestyle    Gold  
      19638     EUN    Men                200M Backstroke  Silver  
      19655     EUN    Men                 200M Freestyle    Gold  
      19667     EUN    Men                 400M Freestyle    Gold  
      ...       ...    ...                            ...     ...  
      21289     EUN    Men        62 - 68KG (Lightweight)  Silver  
      21291     EUN    Men       68 - 74KG (Welterweight)    Gold  
      21293     EUN    Men       74 - 82KG (Middleweight)  Bronze  
      21296     EUN    Men  82 - 90KG (Light-Heavyweight)  Bronze  
      21299     EUN    Men       90 - 100KG (Heavyweight)  Bronze  
      
      [129 rows x 9 columns]),
     (('EUN', 'Women'),
             Year       City       Sport  Discipline                  Athlete  \
      19602  1992  Barcelona    Aquatics      Diving         MIROCHINA, Elena   
      19608  1992  Barcelona    Aquatics      Diving            LACHKO, Irina   
      19619  1992  Barcelona    Aquatics    Swimming       RUDKOVSKAYA, Elena   
      19733  1992  Barcelona    Aquatics    Swimming          CHOUBINA, Elena   
      19734  1992  Barcelona    Aquatics    Swimming        KIRITCHENKO, Olga   
      ...     ...        ...         ...         ...                      ...   
      21208  1992  Barcelona  Volleyball  Volleyball       SIDORENKO, Tatyana   
      21209  1992  Barcelona  Volleyball  Volleyball          SMIRNOVA, Irina   
      21210  1992  Barcelona  Volleyball  Volleyball       TCHEBOUKINA, Elena   
      21211  1992  Barcelona  Volleyball  Volleyball           TYURINA, Elena   
      21212  1992  Barcelona  Volleyball  Volleyball  VASSILEVSKAIA, Svetlana   
      
            Country Gender                Event   Medal  
      19602     EUN  Women         10M Platform  Silver  
      19608     EUN  Women       3M Springboard  Silver  
      19619     EUN  Women    100M Breaststroke    Gold  
      19733     EUN  Women  4X100M Medley Relay  Bronze  
      19734     EUN  Women  4X100M Medley Relay  Bronze  
      ...       ...    ...                  ...     ...  
      21208     EUN  Women           Volleyball  Silver  
      21209     EUN  Women           Volleyball  Silver  
      21210     EUN  Women           Volleyball  Silver  
      21211     EUN  Women           Volleyball  Silver  
      21212     EUN  Women           Volleyball  Silver  
      
      [94 rows x 9 columns]),
     (('FIN', 'Men'),
             Year     City       Sport       Discipline                Athlete  \
      1245   1908   London   Athletics        Athletics       JÄRVINEN, Werner   
      1396   1908   London  Gymnastics      Artistic G.  FORSSTRÖM, Eino Vilho   
      1397   1908   London  Gymnastics      Artistic G.        GRANSTRÖM, Otto   
      1398   1908   London  Gymnastics      Artistic G.   KEMP, Johan Valdemar   
      1399   1908   London  Gymnastics      Artistic G.       KYYKOSKI, Livara   
      ...     ...      ...         ...              ...                    ...   
      26873  2004   Athens    Shooting         Shooting      KEMPPAINEN, Marko   
      27164  2004   Athens   Wrestling  Wrestling Gre-R  YLI-HANNUKSELA, Marko   
      27686  2008  Beijing   Athletics        Athletics        PITKAMAKI, Tero   
      28855  2008  Beijing    Shooting         Shooting        HAKKINEN, Henri   
      29737  2012   London   Athletics        Athletics       RUUSKANEN, Antti   
      
            Country Gender                       Event   Medal  
      1245      FIN    Men  Discus Throw Ancient Style  Bronze  
      1396      FIN    Men            Team Competition  Bronze  
      1397      FIN    Men            Team Competition  Bronze  
      1398      FIN    Men            Team Competition  Bronze  
      1399      FIN    Men            Team Competition  Bronze  
      ...       ...    ...                         ...     ...  
      26873     FIN    Men         Skeet (125 Targets)  Silver  
      27164     FIN    Men                   66 - 74KG  Silver  
      27686     FIN    Men               Javelin Throw  Bronze  
      28855     FIN    Men    10M Air Rifle (60 Shots)  Bronze  
      29737     FIN    Men               Javelin Throw  Silver  
      
      [443 rows x 9 columns]),
     (('FIN', 'Women'),
             Year         City          Sport       Discipline  \
      4024   1920      Antwerp        Skating   Figure skating   
      7399   1948       London      Athletics        Athletics   
      8345   1952     Helsinki  Canoe / Kayak  Canoe / Kayak F   
      15367  1980       Moscow        Archery          Archery   
      16925  1984  Los Angeles      Athletics        Athletics   
      21739  1996      Atlanta      Athletics        Athletics   
      28754  2008      Beijing         Rowing           Rowing   
      28755  2008      Beijing         Rowing           Rowing   
      28889  2008      Beijing       Shooting         Shooting   
      30809  2012       London        Sailing          Sailing   
      30810  2012       London        Sailing          Sailing   
      30811  2012       London        Sailing          Sailing   
      30825  2012       London        Sailing          Sailing   
      
                               Athlete Country Gender  \
      4024         JAKOBSSON, Ludowika     FIN  Women   
      7399           PARVIAINEN, Kaisa     FIN  Women   
      8345         SAIMO, Sylvi Riitta     FIN  Women   
      15367  MERILUOTO-AALTONEN, Paivi     FIN  Women   
      16925          LILLAK, Kristiina     FIN  Women   
      21739     RANTANEN, Heli Orvokki     FIN  Women   
      28754            NIEMINEN, Minna     FIN  Women   
      28755                STEN, Sanna     FIN  Women   
      28889       MAKELA-NUMMELA, Satu     FIN  Women   
      30809             KANERVA, Silja     FIN  Women   
      30810            LEHTINEN, Silja     FIN  Women   
      30811             WULFF, Mikaela     FIN  Women   
      30825              PETAJA, Tuuli     FIN  Women   
      
                                      Event   Medal  
      4024                            Pairs    Gold  
      7399                    Javelin Throw  Silver  
      8345          K-1 500M (Kayak Single)    Gold  
      15367           Individual Fita Round  Bronze  
      16925                   Javelin Throw  Silver  
      21739                   Javelin Throw    Gold  
      28754  Lightweight Double Sculls (2X)  Silver  
      28755  Lightweight Double Sculls (2X)  Silver  
      28889               Trap (75 Targets)    Gold  
      30809                      Elliott 6M  Bronze  
      30810                      Elliott 6M  Bronze  
      30811                      Elliott 6M  Bronze  
      30825                            Rs:X  Silver  ),
     (('FRA', 'Men'),
             Year    City      Sport           Discipline              Athlete  \
      17     1896  Athens  Athletics            Athletics    LERMUSIAUX, Albin   
      47     1896  Athens  Athletics            Athletics   TUFFERI, Alexandre   
      51     1896  Athens    Cycling        Cycling Track        FLAMENG, Léon   
      54     1896  Athens    Cycling        Cycling Track         MASSON, Paul   
      55     1896  Athens    Cycling        Cycling Track        FLAMENG, Léon   
      ...     ...     ...        ...                  ...                  ...   
      30936  2012  London     Tennis               Tennis      LLODRA, Michael   
      30937  2012  London     Tennis               Tennis  TSONGA, Jo-Wilfried   
      30938  2012  London     Tennis               Tennis    BENNETEAU, Julien   
      30939  2012  London     Tennis               Tennis     GASQUET, Richard   
      31151  2012  London  Wrestling  Wrestling Freestyle       GUENOT, Steeve   
      
            Country Gender        Event   Medal  
      17        FRA    Men        1500M  Bronze  
      47        FRA    Men  Triple Jump  Silver  
      51        FRA    Men        100KM    Gold  
      54        FRA    Men         10KM    Gold  
      55        FRA    Men         10KM  Silver  
      ...       ...    ...          ...     ...  
      30936     FRA    Men      Doubles  Silver  
      30937     FRA    Men      Doubles  Silver  
      30938     FRA    Men      Doubles  Bronze  
      30939     FRA    Men      Doubles  Bronze  
      31151     FRA    Men     Wg 66 KG  Bronze  
      
      [1254 rows x 9 columns]),
     (('FRA', 'Women'),
             Year       City      Sport Discipline                Athlete Country  \
      650    1900      Paris     Tennis     Tennis        PREVOST, Hélène     FRA   
      2770   1912  Stockholm     Tennis     Tennis  BROQUEDIS, Marguerite     FRA   
      2783   1912  Stockholm     Tennis     Tennis  BROQUEDIS, Marguerite     FRA   
      4032   1920    Antwerp     Tennis     Tennis      D'AYEN, Elisabeth     FRA   
      4033   1920    Antwerp     Tennis     Tennis       LENGLEN, Suzanne     FRA   
      ...     ...        ...        ...        ...                    ...     ...   
      30622  2012     London       Judo       Judo       TCHEUMEO, Audrey     FRA   
      30837  2012     London   Shooting   Shooting     GOBERVILLE, Celine     FRA   
      30877  2012     London   Shooting   Shooting      RACINET, Delphine     FRA   
      30911  2012     London  Taekwondo  Taekwondo  GRAFFE, Anne-Caroline     FRA   
      30920  2012     London  Taekwondo  Taekwondo       HARNOIS, Marlene     FRA   
      
            Gender           Event   Medal  
      650    Women         Singles  Silver  
      2770   Women   Mixed Doubles  Bronze  
      2783   Women         Singles    Gold  
      4032   Women         Doubles  Bronze  
      4033   Women         Doubles  Bronze  
      ...      ...             ...     ...  
      30622  Women       70 - 78KG  Bronze  
      30837  Women  10M Air Pistol  Silver  
      30877  Women            Trap  Bronze  
      30911  Women         + 67 KG  Silver  
      30920  Women      49 - 57 KG  Bronze  
      
      [142 rows x 9 columns]),
     (('FRG', 'Men'),
             Year    City          Sport       Discipline              Athlete  \
      11759  1968  Mexico       Aquatics         Swimming    HOLTHAUS, Michael   
      11873  1968  Mexico      Athletics        Athletics        TÜMMLER, Bodo   
      11896  1968  Mexico      Athletics        Athletics     HENNIGE, Gerhard   
      11921  1968  Mexico      Athletics        Athletics     HENNIGE, Gerhard   
      11922  1968  Mexico      Athletics        Athletics  JELLINGHAUS, Martin   
      ...     ...     ...            ...              ...                  ...   
      19363  1988   Seoul       Shooting         Shooting     RIEDERER, Johann   
      19513  1988   Seoul  Weightlifting    Weightlifting      ZAWIEJA, Martin   
      19515  1988   Seoul  Weightlifting    Weightlifting   NERLINGER, Manfred   
      19534  1988   Seoul  Weightlifting    Weightlifting   IMMESBERGER, Peter   
      19596  1988   Seoul      Wrestling  Wrestling Gre-R      HIMMEL, Gerhard   
      
            Country Gender                                  Event   Medal  
      11759     FRG    Men                 400M Individual Medley  Bronze  
      11873     FRG    Men                                  1500M  Bronze  
      11896     FRG    Men                           400M Hurdles  Silver  
      11921     FRG    Men                           4X400M Relay  Bronze  
      11922     FRG    Men                           4X400M Relay  Bronze  
      ...       ...    ...                                    ...     ...  
      19363     FRG    Men               10M Air Rifle (60 Shots)  Bronze  
      19513     FRG    Men     + 110KG, Total (Super Heavyweight)  Bronze  
      19515     FRG    Men     + 110KG, Total (Super Heavyweight)  Silver  
      19534     FRG    Men  90 - 100KG, Total (First-Heavyweight)  Bronze  
      19596     FRG    Men               90 - 100KG (Heavyweight)  Silver  
      
      [375 rows x 9 columns]),
     (('FRG', 'Women'),
             Year    City      Sport Discipline                         Athlete  \
      11801  1968  Mexico   Aquatics   Swimming                  FROMMATER, Uta   
      11802  1968  Mexico   Aquatics   Swimming            HUSTEDE-NAGEL, Heike   
      11803  1968  Mexico   Aquatics   Swimming                 KRAUS, Angelika   
      11804  1968  Mexico   Aquatics   Swimming             REINECK, Heidemarie   
      11956  1968  Mexico  Athletics  Athletics  WESTERMANN, Liselotte (Liesel)   
      ...     ...     ...        ...        ...                             ...   
      19362  1988   Seoul   Shooting   Shooting                 SPERBER, Silvia   
      19376  1988   Seoul   Shooting   Shooting                 SPERBER, Silvia   
      19419  1988   Seoul     Tennis     Tennis                    GRAF, Steffi   
      19420  1988   Seoul     Tennis     Tennis           KOHDE-KILSCH, Claudia   
      19433  1988   Seoul     Tennis     Tennis                    GRAF, Steffi   
      
            Country Gender                               Event   Medal  
      11801     FRG  Women                 4X100M Medley Relay  Bronze  
      11802     FRG  Women                 4X100M Medley Relay  Bronze  
      11803     FRG  Women                 4X100M Medley Relay  Bronze  
      11804     FRG  Women                 4X100M Medley Relay  Bronze  
      11956     FRG  Women                        Discus Throw  Silver  
      ...       ...    ...                                 ...     ...  
      19362     FRG  Women            10M Air Rifle (40 Shots)  Silver  
      19376     FRG  Women  50M Rifle 3 Positions (3X20 Shots)    Gold  
      19419     FRG  Women                             Doubles  Bronze  
      19420     FRG  Women                             Doubles  Bronze  
      19433     FRG  Women                             Singles    Gold  
      
      [115 rows x 9 columns]),
     (('GAB', 'Men'),
             Year    City      Sport Discipline         Athlete Country Gender  \
      30915  2012  London  Taekwondo  Taekwondo  OBAME, Anthony     GAB    Men   
      
               Event   Medal  
      30915  + 80 KG  Silver  ),
     (('GBR', 'Men'),
             Year    City      Sport     Discipline             Athlete Country  \
      16     1896  Athens  Athletics      Athletics  GOULDING, Grantley     GBR   
      20     1896  Athens  Athletics      Athletics     GMELIN, Charles     GBR   
      48     1896  Athens    Cycling   Cycling Road      BATTEL, Edward     GBR   
      57     1896  Athens    Cycling  Cycling Track      KEEPING, Frank     GBR   
      140    1896  Athens     Tennis         Tennis        BOLAND, John     GBR   
      ...     ...     ...        ...            ...                 ...     ...   
      30932  2012  London  Taekwondo      Taekwondo    MUHAMMAD, Lutalo     GBR   
      30948  2012  London     Tennis         Tennis        MURRAY, Andy     GBR   
      30952  2012  London     Tennis         Tennis        MURRAY, Andy     GBR   
      30958  2012  London  Triathlon      Triathlon  BROWNLEE, Alistair     GBR   
      30960  2012  London  Triathlon      Triathlon  BROWNLEE, Jonathan     GBR   
      
            Gender                 Event   Medal  
      16       Men          110M Hurdles  Silver  
      20       Men                  400M  Bronze  
      48       Men  Individual Road Race  Bronze  
      57       Men          12-Hour Race  Silver  
      140      Men               Singles    Gold  
      ...      ...                   ...     ...  
      30932    Men            68 - 80 KG  Bronze  
      30948    Men         Mixed Doubles  Silver  
      30952    Men               Singles    Gold  
      30958    Men            Individual    Gold  
      30960    Men            Individual  Bronze  
      
      [1412 rows x 9 columns]),
     (('GBR', 'Women'),
             Year    City      Sport Discipline                        Athlete  \
      641    1900   Paris     Tennis     Tennis              COOPER, Charlotte   
      649    1900   Paris     Tennis     Tennis              COOPER, Charlotte   
      1184   1908  London    Archery    Archery  HILL-LOWE, Beatrice Geraldine   
      1185   1908  London    Archery    Archery    NEWALL, Sybil Fenton Quenni   
      1186   1908  London    Archery    Archery                 DOD, Charlotte   
      ...     ...     ...        ...        ...                            ...   
      30750  2012  London     Rowing     Rowing                HOSKING, Sophie   
      30793  2012  London    Sailing    Sailing                  CLARK, Saskia   
      30794  2012  London    Sailing    Sailing                  MILLS, Hannah   
      30918  2012  London  Taekwondo  Taekwondo                    JONES, Jade   
      30949  2012  London     Tennis     Tennis                  ROBSON, Laura   
      
            Country Gender                       Event   Medal  
      641       GBR  Women               Mixed Doubles    Gold  
      649       GBR  Women                     Singles    Gold  
      1184      GBR  Women  National Round (60Y - 50Y)  Bronze  
      1185      GBR  Women  National Round (60Y - 50Y)    Gold  
      1186      GBR  Women  National Round (60Y - 50Y)  Silver  
      ...       ...    ...                         ...     ...  
      30750     GBR  Women         Lightweight Doubles    Gold  
      30793     GBR  Women                         470  Silver  
      30794     GBR  Women                         470  Silver  
      30918     GBR  Women                  49 - 57 KG    Gold  
      30949     GBR  Women               Mixed Doubles  Silver  
      
      [308 rows x 9 columns]),
     (('GDR', 'Men'),
             Year    City          Sport       Discipline                Athlete  \
      11697  1968  Mexico       Aquatics         Swimming        MATTHES, Roland   
      11724  1968  Mexico       Aquatics         Swimming        MATTHES, Roland   
      11797  1968  Mexico       Aquatics         Swimming  GREGOR, Horst-Günther   
      11798  1968  Mexico       Aquatics         Swimming        HENNINGER, Egon   
      11799  1968  Mexico       Aquatics         Swimming        MATTHES, Roland   
      ...     ...     ...            ...              ...                    ...   
      19388  1988   Seoul       Shooting         Shooting           WEGNER, Axel   
      19516  1988   Seoul  Weightlifting    Weightlifting          WELLER, Ronny   
      19523  1988   Seoul  Weightlifting    Weightlifting          KUNZ, Joachim   
      19527  1988   Seoul  Weightlifting    Weightlifting      STEINHOEFEL, Ingo   
      19540  1988   Seoul      Wrestling  Wrestling Free.      SCHRÖDER, Andreas   
      
            Country Gender                              Event   Medal  
      11697     GDR    Men                    100M Backstroke    Gold  
      11724     GDR    Men                    200M Backstroke    Gold  
      11797     GDR    Men                4X100M Medley Relay  Silver  
      11798     GDR    Men                4X100M Medley Relay  Silver  
      11799     GDR    Men                4X100M Medley Relay  Silver  
      ...       ...    ...                                ...     ...  
      19388     GDR    Men                Skeet (125 Targets)    Gold  
      19516     GDR    Men   100 - 110KG, Total (Heavyweight)  Bronze  
      19523     GDR    Men   60 - 67.5KG, Total (Lightweight)    Gold  
      19527     GDR    Men  67.5 - 75KG, Total (Middleweight)  Silver  
      19540     GDR    Men    100 - 130KG (Super Heavyweight)  Bronze  
      
      [456 rows x 9 columns]),
     (('GDR', 'Women'),
             Year    City     Sport Discipline            Athlete Country Gender  \
      11740  1968  Mexico  Aquatics   Swimming     LINDNER, Helga     GDR  Women   
      11762  1968  Mexico  Aquatics   Swimming  STEINBACH, Sabine     GDR  Women   
      11785  1968  Mexico  Aquatics   Swimming   KRAUSE, Roswitha     GDR  Women   
      11786  1968  Mexico  Aquatics   Swimming  PERTHES, Gabriele     GDR  Women   
      11787  1968  Mexico  Aquatics   Swimming       SCHMUCK, Uta     GDR  Women   
      ...     ...     ...       ...        ...                ...     ...    ...   
      19295  1988   Seoul    Rowing     Rowing   FÖRSTER, Kerstin     GDR  Women   
      19296  1988   Seoul    Rowing     Rowing    MUNDT, Kristina     GDR  Women   
      19297  1988   Seoul    Rowing     Rowing     SCHRAMM, Beate     GDR  Women   
      19298  1988   Seoul    Rowing     Rowing      SORGERS, Jana     GDR  Women   
      19307  1988   Seoul    Rowing     Rowing    BEHRENDT, Jutta     GDR  Women   
      
                                              Event   Medal  
      11740                          200M Butterfly  Silver  
      11762                  400M Individual Medley  Bronze  
      11785                  4X100M Freestyle Relay  Silver  
      11786                  4X100M Freestyle Relay  Silver  
      11787                  4X100M Freestyle Relay  Silver  
      ...                                       ...     ...  
      19295  Quadruple Sculls Without Coxswain (4X)    Gold  
      19296  Quadruple Sculls Without Coxswain (4X)    Gold  
      19297  Quadruple Sculls Without Coxswain (4X)    Gold  
      19298  Quadruple Sculls Without Coxswain (4X)    Gold  
      19307                      Single Sculls (1X)    Gold  
      
      [369 rows x 9 columns]),
     (('GEO', 'Men'),
             Year     City          Sport           Discipline  \
      22655  1996  Atlanta           Judo                 Judo   
      23125  1996  Atlanta      Wrestling      Wrestling Free.   
      23911  2000   Sydney         Boxing               Boxing   
      24606  2000   Sydney           Judo                 Judo   
      25122  2000   Sydney  Weightlifting        Weightlifting   
      25146  2000   Sydney      Wrestling      Wrestling Free.   
      25158  2000   Sydney      Wrestling      Wrestling Gre-R   
      25167  2000   Sydney      Wrestling      Wrestling Gre-R   
      26579  2004   Athens           Judo                 Judo   
      26622  2004   Athens           Judo                 Judo   
      27115  2004   Athens  Weightlifting        Weightlifting   
      27170  2004   Athens      Wrestling      Wrestling Gre-R   
      28636  2008  Beijing           Judo                 Judo   
      29166  2008  Beijing      Wrestling      Wrestling Free.   
      29179  2008  Beijing      Wrestling      Wrestling Free.   
      29182  2008  Beijing      Wrestling      Wrestling Free.   
      29203  2008  Beijing      Wrestling      Wrestling Gre-R   
      30607  2012   London           Judo                 Judo   
      31094  2012   London      Wrestling  Wrestling Freestyle   
      31102  2012   London      Wrestling  Wrestling Freestyle   
      31132  2012   London      Wrestling  Wrestling Freestyle   
      31136  2012   London      Wrestling  Wrestling Freestyle   
      31146  2012   London      Wrestling  Wrestling Freestyle   
      31152  2012   London      Wrestling  Wrestling Freestyle   
      
                               Athlete Country Gender  \
      22655         LIPARTELIANI, Soso     GEO    Men   
      23125         KURTANIDZE, Eldari     GEO    Men   
      23911       TCHANTURIA, Vladimer     GEO    Men   
      24606       VAZAGASHVILI, Giorgi     GEO    Men   
      25122           ASANIDZE, George     GEO    Men   
      25146         KURTANIDZE, Eldari     GEO    Men   
      25158             CHACHUA, Akaki     GEO    Men   
      25167      VAKHTANGADZE, Mukhran     GEO    Men   
      26579          KHERGIANI, Nestor     GEO    Men   
      26622           ZVIADAURI, Zurab     GEO    Men   
      27115           ASANIDZE, George     GEO    Men   
      27170             NOZADZE, Ramaz     GEO    Men   
      28636         TSIREKIDZE, Irakli     GEO    Men   
      29166          TUSHISHVILI, Otar     GEO    Men   
      29179      MINDORASHVILI, Revazi     GEO    Men   
      29182        GOGSHELIDZE, George     GEO    Men   
      29203        KVIRKELIA, Manuchar     GEO    Men   
      30607     SHAVDATUASHVILI, Lasha     GEO    Men   
      31094      MODZMANASHVILI, Davit     GEO    Men   
      31102  KHINCHEGASHVILI, Vladimer     GEO    Men   
      31132        MARSAGISHVILI, Dato     GEO    Men   
      31136        GOGSHELIDZE, George     GEO    Men   
      31146             LASHKHI, Revaz     GEO    Men   
      31152        TSKHADAIA, Manuchar     GEO    Men   
      
                                     Event   Medal  
      22655  73 - 81KG (Half-Middleweight)  Bronze  
      23125  82 - 90KG (Light-Heavyweight)  Bronze  
      23911        81 - 91KG (Heavyweight)  Bronze  
      24606   60 - 66KG (Half-Lightweight)  Bronze  
      25122                           85KG  Bronze  
      25146                      85 - 97KG  Bronze  
      25158                      58 - 63KG  Bronze  
      25167                      76 - 85KG  Bronze  
      26579                        - 60 KG  Silver  
      26622       81 - 90KG (Middleweight)    Gold  
      27115                           85KG    Gold  
      27170                      84 - 96KG  Silver  
      28636       81 - 90KG (Middleweight)    Gold  
      29166                      60 - 66KG  Bronze  
      29179                      74 - 84KG    Gold  
      29182                      84 - 96KG  Bronze  
      29203                      66 - 74KG    Gold  
      30607                      60 - 66KG    Gold  
      31094                       Wf 120KG  Silver  
      31102                       Wf 55 KG  Silver  
      31132                       Wf 84 KG  Bronze  
      31136                       Wf 96 KG  Bronze  
      31146                       Wg 60 KG  Silver  
      31152                       Wg 66 KG  Bronze  ),
     (('GEO', 'Women'),
             Year     City     Sport Discipline           Athlete Country Gender  \
      28846  2008  Beijing  Shooting   Shooting  SALUKVADZE, Nino     GEO  Women   
      
                                 Event   Medal  
      28846  10M Air Pistol (40 Shots)  Bronze  ),
     (('GER', 'Men'),
             Year    City         Sport        Discipline               Athlete  \
      14     1896  Athens     Athletics         Athletics        HOFMANN, Fritz   
      50     1896  Athens       Cycling      Cycling Road      GOEDRICH, August   
      72     1896  Athens    Gymnastics       Artistic G.  WEINGÄRTNER, Hermann   
      73     1896  Athens    Gymnastics       Artistic G.        FLATOW, Alfred   
      74     1896  Athens    Gymnastics       Artistic G.        FLATOW, Alfred   
      ...     ...     ...           ...               ...                   ...   
      30890  2012  London  Table Tennis      Table Tennis            BOLL, Timo   
      30891  2012  London  Table Tennis      Table Tennis   OVTCHAROV, Dimitrij   
      30892  2012  London  Table Tennis      Table Tennis       STEGER, Bastian   
      30964  2012  London    Volleyball  Beach Volleyball         BRINK, Julius   
      30965  2012  London    Volleyball  Beach Volleyball     RECKERMANN, Jonas   
      
            Country Gender                 Event   Medal  
      14        GER    Men                  100M  Silver  
      50        GER    Men  Individual Road Race  Silver  
      72        GER    Men        Horizontal Bar    Gold  
      73        GER    Men        Horizontal Bar  Silver  
      74        GER    Men         Parallel Bars    Gold  
      ...       ...    ...                   ...     ...  
      30890     GER    Men                  Team  Bronze  
      30891     GER    Men                  Team  Bronze  
      30892     GER    Men                  Team  Bronze  
      30964     GER    Men      Beach Volleyball    Gold  
      30965     GER    Men      Beach Volleyball    Gold  
      
      [916 rows x 9 columns]),
     (('GER', 'Women'),
             Year       City      Sport      Discipline                    Athlete  \
      1842   1908     London    Skating  Figure skating  GREENHOUGH-SMITH, Dorothy   
      1844   1908     London    Skating  Figure skating          RENDSCHMIDT, Else   
      1849   1908     London    Skating  Figure skating               HÜBLER, Anna   
      1978   1912  Stockholm   Aquatics        Swimming             DRESSEL, Wally   
      1979   1912  Stockholm   Aquatics        Swimming               OTTO, Louise   
      ...     ...        ...        ...             ...                        ...   
      30771  2012     London     Rowing          Rowing               BAER, Carina   
      30772  2012     London     Rowing          Rowing             OPPELT, Britta   
      30773  2012     London     Rowing          Rowing             RICHTER, Julia   
      30774  2012     London     Rowing          Rowing         THIELE, Annekatrin   
      30924  2012     London  Taekwondo       Taekwondo              FROMM, Helena   
      
            Country Gender                   Event   Medal  
      1842      GER  Women              Individual  Bronze  
      1844      GER  Women              Individual  Silver  
      1849      GER  Women                   Pairs    Gold  
      1978      GER  Women  4X100M Freestyle Relay  Silver  
      1979      GER  Women  4X100M Freestyle Relay  Silver  
      ...       ...    ...                     ...     ...  
      30771     GER  Women        Quadruple Sculls  Silver  
      30772     GER  Women        Quadruple Sculls  Silver  
      30773     GER  Women        Quadruple Sculls  Silver  
      30774     GER  Women        Quadruple Sculls  Silver  
      30924     GER  Women              57 - 67 KG  Bronze  
      
      [389 rows x 9 columns]),
     (('GHA', 'Men'),
             Year       City     Sport Discipline                  Athlete Country  \
      10108  1960       Rome    Boxing     Boxing         QUARTEY, Clement     GHA   
      11010  1964      Tokyo    Boxing     Boxing             BLAY, Edward     GHA   
      13120  1972     Munich    Boxing     Boxing          AMARTEY, Prince     GHA   
      20482  1992  Barcelona  Football   Football  ACHEAMPONG, Joachin Yaw     GHA   
      20483  1992  Barcelona  Football   Football              ADDO, Simon     GHA   
      20484  1992  Barcelona  Football   Football             ADJEI, Sammi     GHA   
      20485  1992  Barcelona  Football   Football          AMANKWAH, Frank     GHA   
      20486  1992  Barcelona  Football   Football       ARYEE, Bernard Nii     GHA   
      20487  1992  Barcelona  Football   Football             ASARE, Isaac     GHA   
      20488  1992  Barcelona  Football   Football              AYEW, Kwame     GHA   
      20489  1992  Barcelona  Football   Football          DOSSEY, Ibrahim     GHA   
      20490  1992  Barcelona  Football   Football          GARGO, Mohammed     GHA   
      20491  1992  Barcelona  Football   Football     KUMAH, Samuel Ablade     GHA   
      20492  1992  Barcelona  Football   Football     LAMPTEY, Nii Odartey     GHA   
      20493  1992  Barcelona  Football   Football               PREKO, Yaw     GHA   
      20494  1992  Barcelona  Football   Football             QUAYE, Shamo     GHA   
      
            Gender                             Event   Medal  
      10108    Men  60 - 63.5KG (Light-Welterweight)  Silver  
      11010    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      13120    Men                           71-75KG  Bronze  
      20482    Men                          Football  Bronze  
      20483    Men                          Football  Bronze  
      20484    Men                          Football  Bronze  
      20485    Men                          Football  Bronze  
      20486    Men                          Football  Bronze  
      20487    Men                          Football  Bronze  
      20488    Men                          Football  Bronze  
      20489    Men                          Football  Bronze  
      20490    Men                          Football  Bronze  
      20491    Men                          Football  Bronze  
      20492    Men                          Football  Bronze  
      20493    Men                          Football  Bronze  
      20494    Men                          Football  Bronze  ),
     (('GRE', 'Men'),
             Year     City      Sport       Discipline                 Athlete  \
      2      1896   Athens   Aquatics         Swimming       DRIVAS, Dimitrios   
      3      1896   Athens   Aquatics         Swimming      MALOKINIS, Ioannis   
      4      1896   Athens   Aquatics         Swimming      CHASAPIS, Spiridon   
      5      1896   Athens   Aquatics         Swimming   CHOROPHAS, Efstathios   
      7      1896   Athens   Aquatics         Swimming        ANDREOU, Joannis   
      ...     ...      ...        ...              ...                     ...   
      27153  2004   Athens  Wrestling  Wrestling Gre-R     KIOUREGKIAN, Artiom   
      28748  2008  Beijing     Rowing           Rowing      MOUGIOS, Dimitrios   
      28749  2008  Beijing     Rowing           Rowing    POLYMEROS, Vasileios   
      28975  2008  Beijing  Taekwondo        Taekwondo  NIKOLAIDIS, Alexandros   
      30629  2012   London       Judo             Judo          ILIADIS, Ilias   
      
            Country Gender                           Event   Medal  
      2         GRE    Men      100M Freestyle For Sailors  Bronze  
      3         GRE    Men      100M Freestyle For Sailors    Gold  
      4         GRE    Men      100M Freestyle For Sailors  Silver  
      5         GRE    Men                 1200M Freestyle  Bronze  
      7         GRE    Men                 1200M Freestyle  Silver  
      ...       ...    ...                             ...     ...  
      27153     GRE    Men                          - 55KG  Bronze  
      28748     GRE    Men  Lightweight Double Sculls (2X)  Silver  
      28749     GRE    Men  Lightweight Double Sculls (2X)  Silver  
      28975     GRE    Men                         + 80 KG  Silver  
      30629     GRE    Men                       81 - 90KG  Bronze  
      
      [109 rows x 9 columns]),
     (('GRE', 'Women'),
             Year       City          Sport     Discipline  \
      19865  1992  Barcelona      Athletics      Athletics   
      21734  1996    Atlanta      Athletics      Athletics   
      23525  2000     Sydney      Athletics      Athletics   
      23645  2000     Sydney      Athletics      Athletics   
      23667  2000     Sydney      Athletics      Athletics   
      24364  2000     Sydney     Gymnastics    Rhythmic G.   
      24365  2000     Sydney     Gymnastics    Rhythmic G.   
      24366  2000     Sydney     Gymnastics    Rhythmic G.   
      24367  2000     Sydney     Gymnastics    Rhythmic G.   
      24368  2000     Sydney     Gymnastics    Rhythmic G.   
      24369  2000     Sydney     Gymnastics    Rhythmic G.   
      25107  2000     Sydney  Weightlifting  Weightlifting   
      25495  2004     Athens       Aquatics     Water polo   
      25496  2004     Athens       Aquatics     Water polo   
      25497  2004     Athens       Aquatics     Water polo   
      25498  2004     Athens       Aquatics     Water polo   
      25499  2004     Athens       Aquatics     Water polo   
      25500  2004     Athens       Aquatics     Water polo   
      25501  2004     Athens       Aquatics     Water polo   
      25502  2004     Athens       Aquatics     Water polo   
      25503  2004     Athens       Aquatics     Water polo   
      25504  2004     Athens       Aquatics     Water polo   
      25505  2004     Athens       Aquatics     Water polo   
      25506  2004     Athens       Aquatics     Water polo   
      25507  2004     Athens       Aquatics     Water polo   
      25563  2004     Athens      Athletics      Athletics   
      25581  2004     Athens      Athletics      Athletics   
      25663  2004     Athens      Athletics      Athletics   
      25682  2004     Athens      Athletics      Athletics   
      25714  2004     Athens      Athletics      Athletics   
      26786  2004     Athens        Sailing        Sailing   
      26787  2004     Athens        Sailing        Sailing   
      26963  2004     Athens      Taekwondo      Taekwondo   
      27719  2008    Beijing      Athletics      Athletics   
      28837  2008    Beijing        Sailing        Sailing   
      28838  2008    Beijing        Sailing        Sailing   
      28839  2008    Beijing        Sailing        Sailing   
      30753  2012     London         Rowing         Rowing   
      30754  2012     London         Rowing         Rowing   
      
                                 Athlete Country Gender                    Event  \
      19865  PATOULIDOU, Paraskevi Voula     GRE  Women             100M Hurdles   
      21734             BAKOGIANNI, Niki     GRE  Women                High Jump   
      23525            THANOU, Ekaterini     GRE  Women                     100M   
      23645         KELESIDOU, Anastasia     GRE  Women             Discus Throw   
      23667     MANIANI-TZELILI, Mirella     GRE  Women            Javelin Throw   
      24364              AINDILI, Eirini     GRE  Women        Group Competition   
      24365     CHRISTODOULOU, Evangelia     GRE  Women        Group Competition   
      24366             GEORGATOU, Maria     GRE  Women        Group Competition   
      24367          KARYAMI, Zacharoula     GRE  Women        Group Competition   
      24368          PANTAZI, Charikleia     GRE  Women        Group Competition   
      24369               POLLATOU, Anna     GRE  Women        Group Competition   
      25107        CHATZIIOANNOU, Ioanna     GRE  Women                     63KG   
      25495             ASILIAN, Dimitra     GRE  Women               Water Polo   
      25496            ELLINAKI, Georgia     GRE  Women               Water Polo   
      25497         KARAGIANNI, Eftychia     GRE  Women               Water Polo   
      25498         KARAPATAKI, Angeliki     GRE  Women               Water Polo   
      25499         KOZOMPOLI, Stavroula     GRE  Women               Water Polo   
      25500                LARA, Georgia     GRE  Women               Water Polo   
      25501               LIOSI, Kyriaki     GRE  Women               Water Polo   
      25502             MELIDONI, Aniopi     GRE  Women               Water Polo   
      25503             MORAITI, Antonia     GRE  Women               Water Polo   
      25504        MORAITIDOU, Evangelia     GRE  Women               Water Polo   
      25505           MYLONAKI, Anthoula     GRE  Women               Water Polo   
      25506   OIKONOMOPOULOU, Aikaterini     GRE  Women               Water Polo   
      25507           ROUMPESI, Antigoni     GRE  Women               Water Polo   
      25563        TSOUMELEKA, Athanasia     GRE  Women           20KM Race Walk   
      25581                CHALKIA, Fani     GRE  Women             400M Hurdles   
      25663         KELESIDOU, Anastasia     GRE  Women             Discus Throw   
      25682     MANIANI-TZELILI, Mirella     GRE  Women            Javelin Throw   
      25714           DEVETZI, Hrysopiyi     GRE  Women              Triple Jump   
      26786             BEKATOROU, Sofia     GRE  Women  470 - Two Person Dinghy   
      26787             TSOULFA, Aimilia     GRE  Women  470 - Two Person Dinghy   
      26963         MYSTAKIDOU, Elisavet     GRE  Women               57 - 67 KG   
      27719           DEVETZI, Hrysopiyi     GRE  Women              Triple Jump   
      28837             BEKATOROU, Sofia     GRE  Women       Yngling - Keelboat   
      28838         KRAVARIOTI, Virginia     GRE  Women       Yngling - Keelboat   
      28839          PAPADOPOULOU, Sofia     GRE  Women       Yngling - Keelboat   
      30753       GIAZITZIDOU, Christina     GRE  Women      Lightweight Doubles   
      30754           TSIAVOU, Alexandra     GRE  Women      Lightweight Doubles   
      
              Medal  
      19865    Gold  
      21734  Silver  
      23525  Silver  
      23645  Silver  
      23667  Silver  
      24364  Bronze  
      24365  Bronze  
      24366  Bronze  
      24367  Bronze  
      24368  Bronze  
      24369  Bronze  
      25107  Bronze  
      25495  Silver  
      25496  Silver  
      25497  Silver  
      25498  Silver  
      25499  Silver  
      25500  Silver  
      25501  Silver  
      25502  Silver  
      25503  Silver  
      25504  Silver  
      25505  Silver  
      25506  Silver  
      25507  Silver  
      25563    Gold  
      25581    Gold  
      25663  Silver  
      25682  Bronze  
      25714  Silver  
      26786    Gold  
      26787    Gold  
      26963  Silver  
      27719  Bronze  
      28837  Bronze  
      28838  Bronze  
      28839  Bronze  
      30753  Bronze  
      30754  Bronze  ),
     (('GRN', 'Men'),
             Year    City      Sport Discipline        Athlete Country Gender Event  \
      29624  2012  London  Athletics  Athletics  JAMES, Kirani     GRN    Men  400M   
      
            Medal  
      29624  Gold  ),
     (('GUA', 'Men'),
             Year    City      Sport Discipline          Athlete Country Gender  \
      29616  2012  London  Athletics  Athletics  BARRONDO, Erick     GUA    Men   
      
                 Event   Medal  
      29616  20KM Walk  Silver  ),
     (('GUY', 'Men'),
             Year    City   Sport Discipline           Athlete Country Gender  \
      15604  1980  Moscow  Boxing     Boxing  ANTHONY, Michael     GUY    Men   
      
                                Event   Medal  
      15604  51 - 54KG (Bantamweight)  Bronze  ),
     (('HAI', 'Men'),
            Year       City      Sport Discipline            Athlete Country Gender  \
      4881  1924      Paris   Shooting   Shooting  AUGUSTIN, Ludovic     HAI    Men   
      4882  1924      Paris   Shooting   Shooting    CLERMONT, L. H.     HAI    Men   
      4883  1924      Paris   Shooting   Shooting    DESTINE, Destin     HAI    Men   
      4884  1924      Paris   Shooting   Shooting          DUPRE, C.     HAI    Men   
      4885  1924      Paris   Shooting   Shooting  METULLUS, St Eloi     HAI    Men   
      4886  1924      Paris   Shooting   Shooting    ROLLAND, Astrel     HAI    Men   
      4887  1924      Paris   Shooting   Shooting  VALBORGE, Ludovic     HAI    Men   
      5186  1928  Amsterdam  Athletics  Athletics   CATOR, Silvio M.     HAI    Men   
      
                                      Event   Medal  
      4881  400, 600, 800M Free Rifle, Team  Bronze  
      4882  400, 600, 800M Free Rifle, Team  Bronze  
      4883  400, 600, 800M Free Rifle, Team  Bronze  
      4884  400, 600, 800M Free Rifle, Team  Bronze  
      4885  400, 600, 800M Free Rifle, Team  Bronze  
      4886  400, 600, 800M Free Rifle, Team  Bronze  
      4887  400, 600, 800M Free Rifle, Team  Bronze  
      5186                        Long Jump  Silver  ),
     (('HKG', 'Men'),
             Year    City         Sport    Discipline       Athlete Country Gender  \
      26932  2004  Athens  Table Tennis  Table Tennis  KO, Lai Chak     HKG    Men   
      26933  2004  Athens  Table Tennis  Table Tennis     LI, Ching     HKG    Men   
      
               Event   Medal  
      26932  Doubles  Silver  
      26933  Doubles  Silver  ),
     (('HKG', 'Women'),
             Year     City    Sport     Discipline        Athlete Country Gender  \
      22829  1996  Atlanta  Sailing        Sailing  LEE, Lai Shan     HKG  Women   
      30025  2012   London  Cycling  Cycling Track   LEE, Wai Sze     HKG  Women   
      
                       Event   Medal  
      22829  Board (Mistral)    Gold  
      30025           Keirin  Bronze  ),
     (('HUN', 'Men'),
             Year    City              Sport           Discipline           Athlete  \
      0      1896  Athens           Aquatics             Swimming     HAJOS, Alfred   
      6      1896  Athens           Aquatics             Swimming     HAJOS, Alfred   
      12     1896  Athens          Athletics            Athletics  SZOKOLYI, Alajos   
      25     1896  Athens          Athletics            Athletics      DANI, Nandor   
      35     1896  Athens          Athletics            Athletics    KELLNER, Gyula   
      ...     ...     ...                ...                  ...               ...   
      30608  2012  London               Judo                 Judo   UNGVARI, Miklos   
      30637  2012  London  Modern Pentathlon    Modern Pentathlon      MAROSI, Adam   
      31127  2012  London          Wrestling  Wrestling Freestyle      HATOS, Gabor   
      31143  2012  London          Wrestling  Wrestling Freestyle      MODOS, Peter   
      31150  2012  London          Wrestling  Wrestling Freestyle    LORINCZ, Tamas   
      
            Country Gender            Event   Medal  
      0         HUN    Men   100M Freestyle    Gold  
      6         HUN    Men  1200M Freestyle    Gold  
      12        HUN    Men             100M  Bronze  
      25        HUN    Men             800M  Silver  
      35        HUN    Men         Marathon  Bronze  
      ...       ...    ...              ...     ...  
      30608     HUN    Men        60 - 66KG  Silver  
      30637     HUN    Men       Individual  Bronze  
      31127     HUN    Men         Wf 74 KG  Bronze  
      31143     HUN    Men         Wg 55 KG  Bronze  
      31150     HUN    Men         Wg 66 KG  Silver  
      
      [834 rows x 9 columns]),
     (('HUN', 'Women'),
             Year         City       Sport    Discipline                 Athlete  \
      6023   1932  Los Angeles     Fencing       Fencing             BOGEN, Erna   
      6514   1936       Berlin   Athletics     Athletics            CSAK, Ibolya   
      6737   1936       Berlin     Fencing       Fencing             ELEK, Ilona   
      6862   1936       Berlin  Gymnastics   Artistic G.         CSILLIK, Margit   
      6863   1936       Berlin  Gymnastics   Artistic G.        KALOCSAI, Margit   
      ...     ...          ...         ...           ...                     ...   
      29989  2012       London       Canoe  Canoe Sprint      FAZEKAS, Krisztina   
      29990  2012       London       Canoe  Canoe Sprint         KOVACS, Katalin   
      29991  2012       London       Canoe  Canoe Sprint           KOZAK, Danuta   
      29992  2012       London       Canoe  Canoe Sprint  SZABO, Gabriella Timea   
      30581  2012       London        Judo          Judo       CSERNOVICZKI, Eva   
      
            Country Gender             Event   Medal  
      6023      HUN  Women   Foil Individual  Bronze  
      6514      HUN  Women         High Jump    Gold  
      6737      HUN  Women   Foil Individual    Gold  
      6862      HUN  Women  Team Competition  Bronze  
      6863      HUN  Women  Team Competition  Bronze  
      ...       ...    ...               ...     ...  
      29989     HUN  Women          K-4 500M    Gold  
      29990     HUN  Women          K-4 500M    Gold  
      29991     HUN  Women          K-4 500M    Gold  
      29992     HUN  Women          K-4 500M    Gold  
      30581     HUN  Women           - 48 KG  Bronze  
      
      [245 rows x 9 columns]),
     (('INA', 'Men'),
             Year       City          Sport     Discipline  \
      20033  1992  Barcelona      Badminton      Badminton   
      20034  1992  Barcelona      Badminton      Badminton   
      20044  1992  Barcelona      Badminton      Badminton   
      20045  1992  Barcelona      Badminton      Badminton   
      20046  1992  Barcelona      Badminton      Badminton   
      21768  1996    Atlanta      Badminton      Badminton   
      21769  1996    Atlanta      Badminton      Badminton   
      21771  1996    Atlanta      Badminton      Badminton   
      21772  1996    Atlanta      Badminton      Badminton   
      23701  2000     Sydney      Badminton      Badminton   
      23702  2000     Sydney      Badminton      Badminton   
      23706  2000     Sydney      Badminton      Badminton   
      23718  2000     Sydney      Badminton      Badminton   
      25715  2004     Athens      Badminton      Badminton   
      25716  2004     Athens      Badminton      Badminton   
      25733  2004     Athens      Badminton      Badminton   
      25734  2004     Athens      Badminton      Badminton   
      27725  2008    Beijing      Badminton      Badminton   
      27726  2008    Beijing      Badminton      Badminton   
      27730  2008    Beijing      Badminton      Badminton   
      29100  2008    Beijing  Weightlifting  Weightlifting   
      29121  2008    Beijing  Weightlifting  Weightlifting   
      31071  2012     London  Weightlifting  Weightlifting   
      31076  2012     London  Weightlifting  Weightlifting   
      
                              Athlete Country Gender                         Event  \
      20033             GUNAWAN, Rudy     INA    Men                       Doubles   
      20034             HARTONO, Eddy     INA    Men                       Doubles   
      20044         SUSANTO, Hermawan     INA    Men                       Singles   
      20045         BUDI KUSUMA, Alan     INA    Men                       Singles   
      20046  WIRANATA, Ardy Bernardus     INA    Men                       Singles   
      21768         IRIANTO, Antonius     INA    Men                       Doubles   
      21769            KANTONO, Denny     INA    Men                       Doubles   
      21771      MAINAKY, Rexy Ronald     INA    Men                       Doubles   
      21772     SUBAGJA, Ricky Achmad     INA    Men                       Doubles   
      23701             GUNAWAN, Tony     INA    Men                       Doubles   
      23702            WIJAYA, Candra     INA    Men                       Doubles   
      23706          KUSHANJANTO, Tri     INA    Men                       Doubles   
      23718                 HENDRAWAN     INA    Men                       Singles   
      25715                 HIAN, Eng     INA    Men                       Doubles   
      25716           LIMPELE, Flandy     INA    Men                       Doubles   
      25733         KUNCORO, Soni Dwi     INA    Men                       Singles   
      25734           HIDAYAT, Taufik     INA    Men                       Singles   
      27725              KIDO, Markis     INA    Men                       Doubles   
      27726          SETIAWAN, Hendra     INA    Men                       Doubles   
      27730            WIDIANTO, Nova     INA    Men                       Doubles   
      29100          IRAWAN, Eko Yuli     INA    Men  - 56KG, Total (Bantamweight)   
      29121                  TRIYATNO     INA    Men                          62KG   
      31071          IRAWAN, Eko Yuli     INA    Men                          62KG   
      31076        TRIYATNO, Triyatno     INA    Men                          69KG   
      
              Medal  
      20033  Silver  
      20034  Silver  
      20044  Bronze  
      20045    Gold  
      20046  Silver  
      21768  Bronze  
      21769  Bronze  
      21771    Gold  
      21772    Gold  
      23701    Gold  
      23702    Gold  
      23706  Silver  
      23718  Silver  
      25715  Bronze  
      25716  Bronze  
      25733  Bronze  
      25734    Gold  
      27725    Gold  
      27726    Gold  
      27730  Silver  
      29100  Bronze  
      29121  Bronze  
      31071  Bronze  
      31076  Silver  ),
     (('INA', 'Women'),
             Year       City          Sport     Discipline                  Athlete  \
      18274  1988      Seoul        Archery        Archery        HANDAYANI, Lilies   
      18275  1988      Seoul        Archery        Archery     SAIMAN, Nurfitriyana   
      18276  1988      Seoul        Archery        Archery         WARDHANI, Kusuma   
      20049  1992  Barcelona      Badminton      Badminton            SUSANTI, Susi   
      21789  1996    Atlanta      Badminton      Badminton            SUSANTI, Susi   
      21791  1996    Atlanta      Badminton      Badminton              AUDINA, Mia   
      23715  2000     Sydney      Badminton      Badminton           TIMUR, Minarti   
      25092  2000     Sydney  Weightlifting  Weightlifting           INDRIYANI, Sri   
      25094  2000     Sydney  Weightlifting  Weightlifting     RUMBEWAS, Raema Lisa   
      25095  2000     Sydney  Weightlifting  Weightlifting    SLAMET, Winarni Binti   
      27092  2004     Athens  Weightlifting  Weightlifting     RUMBEWAS, Raema Lisa   
      27739  2008    Beijing      Badminton      Badminton                 LILIYANA   
      27743  2008    Beijing      Badminton      Badminton  YULIANTI, Maria Kristin   
      31061  2012     London  Weightlifting  Weightlifting         FEBRIANTI, Citra   
      
            Country Gender             Event   Medal  
      18274     INA  Women  Teams Fita Round  Silver  
      18275     INA  Women  Teams Fita Round  Silver  
      18276     INA  Women  Teams Fita Round  Silver  
      20049     INA  Women           Singles    Gold  
      21789     INA  Women           Singles  Bronze  
      21791     INA  Women           Singles  Silver  
      23715     INA  Women           Doubles  Silver  
      25092     INA  Women              48KG  Bronze  
      25094     INA  Women              48KG  Silver  
      25095     INA  Women              53KG  Bronze  
      27092     INA  Women              53KG  Silver  
      27739     INA  Women           Doubles  Silver  
      27743     INA  Women           Singles  Bronze  
      31061     INA  Women              53KG  Silver  ),
     (('IND', 'Men'),
             Year       City      Sport           Discipline               Athlete  \
      241    1900      Paris  Athletics            Athletics     PRITCHARD, Norman   
      244    1900      Paris  Athletics            Athletics     PRITCHARD, Norman   
      5512   1928  Amsterdam     Hockey               Hockey  ALLEN, Richard James   
      5513   1928  Amsterdam     Hockey               Hockey           CHAND, Dyan   
      5514   1928  Amsterdam     Hockey               Hockey   GATELEY, Maurice A.   
      ...     ...        ...        ...                  ...                   ...   
      29165  2008    Beijing  Wrestling      Wrestling Free.         KUMAR, Sushil   
      30841  2012     London   Shooting             Shooting         NARANG, Gagan   
      30849  2012     London   Shooting             Shooting          KUMAR, Vijay   
      31111  2012     London  Wrestling  Wrestling Freestyle       DUTT, Yogeshwar   
      31118  2012     London  Wrestling  Wrestling Freestyle         KUMAR, Sushil   
      
            Country Gender             Event   Medal  
      241       IND    Men              200M  Silver  
      244       IND    Men      200M Hurdles  Silver  
      5512      IND    Men            Hockey    Gold  
      5513      IND    Men            Hockey    Gold  
      5514      IND    Men            Hockey    Gold  
      ...       ...    ...               ...     ...  
      29165     IND    Men         60 - 66KG  Bronze  
      30841     IND    Men     10M Air Rifle  Bronze  
      30849     IND    Men  25M Rapid Pistol  Silver  
      31111     IND    Men          Wf 60 KG  Bronze  
      31118     IND    Men          Wf 66 KG  Silver  
      
      [181 rows x 9 columns]),
     (('IND', 'Women'),
             Year    City          Sport     Discipline             Athlete Country  \
      25113  2000  Sydney  Weightlifting  Weightlifting  MALLESWARI, Karnam     IND   
      29795  2012  London      Badminton      Badminton       NEHWAL, Saina     IND   
      29879  2012  London         Boxing         Boxing           KOM, Mary     IND   
      
            Gender    Event   Medal  
      25113  Women     69KG  Bronze  
      29795  Women  Singles  Bronze  
      29879  Women    51 KG  Bronze  ),
     (('IOP', 'Men'),
             Year       City     Sport Discipline             Athlete Country  \
      21081  1992  Barcelona  Shooting   Shooting  PLETIKOSIC, Stevan     IOP   
      
            Gender                       Event   Medal  
      21081    Men  50M Rifle Prone (60 Shots)  Bronze  ),
     (('IOP', 'Women'),
             Year       City     Sport Discipline         Athlete Country Gender  \
      21056  1992  Barcelona  Shooting   Shooting  SEKARIC, Jasna     IOP  Women   
      21060  1992  Barcelona  Shooting   Shooting  BINDER, Aranka     IOP  Women   
      
                                 Event   Medal  
      21056  10M Air Pistol (40 Shots)  Silver  
      21060   10M Air Rifle (40 Shots)  Bronze  ),
     (('IRI', 'Men'),
             Year      City          Sport           Discipline  \
      7958   1948    London  Weightlifting        Weightlifting   
      8838   1952  Helsinki  Weightlifting        Weightlifting   
      8840   1952  Helsinki  Weightlifting        Weightlifting   
      8859   1952  Helsinki      Wrestling      Wrestling Free.   
      8870   1952  Helsinki      Wrestling      Wrestling Free.   
      ...     ...       ...            ...                  ...   
      31126  2012    London      Wrestling  Wrestling Freestyle   
      31131  2012    London      Wrestling  Wrestling Freestyle   
      31141  2012    London      Wrestling  Wrestling Freestyle   
      31145  2012    London      Wrestling  Wrestling Freestyle   
      31161  2012    London      Wrestling  Wrestling Freestyle   
      
                                       Athlete Country Gender  \
      7958            SALMASSI, Jafar Mohammad     IRI    Men   
      8838                         MIRZAI, Ali     IRI    Men   
      8840                    NAMDJOU, Mahmoud     IRI    Men   
      8859              MOLLAGHASSEMI, Mahmoud     IRI    Men   
      8870                  GUIVEGTCHI, Nasser     IRI    Men   
      ...                                  ...     ...    ...   
      31126             GOUDARZI, Sadegh Saeed     IRI    Men   
      31131              LASHGARI, Ehsan Naser     IRI    Men   
      31141  SORYAN REIHANPOUR, Hamid Mohammad     IRI    Men   
      31145                 NOROOZI, Omid Haji     IRI    Men   
      31161          REZAEI, Ghasem Gholamreza     IRI    Men   
      
                                        Event   Medal  
      7958   56 - 60KG, Total (Featherweight)  Bronze  
      8838       - 56KG, Total (Bantamweight)  Bronze  
      8840       - 56KG, Total (Bantamweight)  Silver  
      8859                 - 52KG (Flyweight)  Bronze  
      8870          57 - 63KG (Featherweight)  Silver  
      ...                                 ...     ...  
      31126                          Wf 74 KG  Silver  
      31131                          Wf 84 KG  Bronze  
      31141                          Wg 55 KG    Gold  
      31145                          Wg 60 KG    Gold  
      31161                          Wg 96 KG    Gold  
      
      [61 rows x 9 columns]),
     (('IRL', 'Men'),
             Year                   City       Sport Discipline  \
      5173   1928              Amsterdam   Athletics  Athletics   
      5827   1932            Los Angeles   Athletics  Athletics   
      5887   1932            Los Angeles   Athletics  Athletics   
      8291   1952               Helsinki      Boxing     Boxing   
      9018   1956  Melbourne / Stockholm   Athletics  Athletics   
      9168   1956  Melbourne / Stockholm      Boxing     Boxing   
      9177   1956  Melbourne / Stockholm      Boxing     Boxing   
      9184   1956  Melbourne / Stockholm      Boxing     Boxing   
      9195   1956  Melbourne / Stockholm      Boxing     Boxing   
      11007  1964                  Tokyo      Boxing     Boxing   
      15600  1980                 Moscow      Boxing     Boxing   
      16392  1980                 Moscow     Sailing    Sailing   
      16393  1980                 Moscow     Sailing    Sailing   
      16934  1984            Los Angeles   Athletics  Athletics   
      20198  1992              Barcelona      Boxing     Boxing   
      20213  1992              Barcelona      Boxing     Boxing   
      27898  2008                Beijing      Boxing     Boxing   
      27923  2008                Beijing      Boxing     Boxing   
      27929  2008                Beijing      Boxing     Boxing   
      29703  2012                 London   Athletics  Athletics   
      29875  2012                 London      Boxing     Boxing   
      29883  2012                 London      Boxing     Boxing   
      29885  2012                 London      Boxing     Boxing   
      30113  2012                 London  Equestrian    Jumping   
      
                                     Athlete Country Gender  \
      5173              O'CALLAGHAN, Patrick     IRL    Men   
      5827   TISDALL, Robert Morton Newburgh     IRL    Men   
      5887              O'CALLAGHAN, Patrick     IRL    Men   
      8291                     MCNALLY, John     IRL    Men   
      9018            DELANY, Ronald Michael     IRL    Men   
      9168                    CALDWELL, John     IRL    Men   
      9177                 GILROY, Frederick     IRL    Men   
      9184                    BYRNE, Anthony     IRL    Men   
      9195                       TIEDT, Fred     IRL    Men   
      11007           MCCOURT, James Vincent     IRL    Men   
      15600                    RUSSELL, Hugh     IRL    Men   
      16392                   WILKINS, David     IRL    Men   
      16393                 WILKINSON, James     IRL    Men   
      16934                     TREACY, John     IRL    Men   
      20198                MCCULLOUGH, Wayne     IRL    Men   
      20213                 CARRUTH, Michael     IRL    Men   
      27898                    BARNES, Paddy     IRL    Men   
      27923          SUTHERLAND, Darren John     IRL    Men   
      27929                      EGAN, Kenny     IRL    Men   
      29703                HEFFERNAN, Robert     IRL    Men   
      29875                    BARNES, Paddy     IRL    Men   
      29883                  CONLAN, Michael     IRL    Men   
      29885                  NEVIN, John Joe     IRL    Men   
      30113                    OCONNOR, Cian     IRL    Men   
      
                                     Event   Medal  
      5173                    Hammer Throw    Gold  
      5827                    400M Hurdles    Gold  
      5887                    Hammer Throw    Gold  
      8291        51 - 54KG (Bantamweight)  Silver  
      9018                           1500M    Gold  
      9168              - 51KG (Flyweight)  Bronze  
      9177        51 - 54KG (Bantamweight)  Bronze  
      9184         57 - 60KG (Lightweight)  Bronze  
      9195      63.5 - 67KG (Welterweight)  Silver  
      11007        57 - 60KG (Lightweight)  Bronze  
      15600          48 - 51KG (Flyweight)  Bronze  
      16392                Flying Dutchman  Silver  
      16393                Flying Dutchman  Silver  
      16934                       Marathon  Silver  
      20198       51 - 54KG (Bantamweight)  Silver  
      20213     63.5 - 67KG (Welterweight)    Gold  
      27898         48KG (Light Flywieght)  Bronze  
      27923                     69 - 75 KG  Bronze  
      27929  75 - 81KG (Light-Heavyweight)  Silver  
      29703                      50KM Walk  Bronze  
      29875                      46 - 49KG  Bronze  
      29883                           52KG  Bronze  
      29885                           56KG  Silver  
      30113                     Individual  Bronze  ),
     (('IRL', 'Women'),
             Year     City      Sport Discipline                Athlete Country  \
      21356  1996  Atlanta   Aquatics   Swimming  SMITH, Michelle Marie     IRL   
      21369  1996  Atlanta   Aquatics   Swimming  SMITH, Michelle Marie     IRL   
      21375  1996  Atlanta   Aquatics   Swimming  SMITH, Michelle Marie     IRL   
      21381  1996  Atlanta   Aquatics   Swimming  SMITH, Michelle Marie     IRL   
      23627  2000   Sydney  Athletics  Athletics      O'SULLIVAN, Sonia     IRL   
      29896  2012   London     Boxing     Boxing          TAYLOR, Katie     IRL   
      
            Gender                   Event   Medal  
      21356  Women          200M Butterfly  Bronze  
      21369  Women  200M Individual Medley    Gold  
      21375  Women          400M Freestyle    Gold  
      21381  Women  400M Individual Medley    Gold  
      23627  Women                   5000M  Silver  
      29896  Women                   60 KG    Gold  ),
     (('IRQ', 'Men'),
             Year  City          Sport     Discipline            Athlete Country  \
      10614  1960  Rome  Weightlifting  Weightlifting  WAHID AZIZ, Abdul     IRQ   
      
            Gender                             Event   Medal  
      10614    Men  60 - 67.5KG, Total (Lightweight)  Bronze  ),
     (('ISL', 'Men'),
             Year                   City      Sport Discipline  \
      9131   1956  Melbourne / Stockholm  Athletics  Athletics   
      17635  1984            Los Angeles       Judo       Judo   
      28432  2008                Beijing   Handball   Handball   
      28433  2008                Beijing   Handball   Handball   
      28434  2008                Beijing   Handball   Handball   
      28435  2008                Beijing   Handball   Handball   
      28436  2008                Beijing   Handball   Handball   
      28437  2008                Beijing   Handball   Handball   
      28438  2008                Beijing   Handball   Handball   
      28439  2008                Beijing   Handball   Handball   
      28440  2008                Beijing   Handball   Handball   
      28441  2008                Beijing   Handball   Handball   
      28442  2008                Beijing   Handball   Handball   
      28443  2008                Beijing   Handball   Handball   
      28444  2008                Beijing   Handball   Handball   
      28445  2008                Beijing   Handball   Handball   
      
                               Athlete Country Gender                         Event  \
      9131       EINARSSON, Vilhjalmur     ISL    Men                   Triple Jump   
      17635        FRIDRIKSSON, Bjarni     ISL    Men  86 - 95KG (Half-Heavyweight)   
      28432         ASGEIRSSON, Sturla     ISL    Men                      Handball   
      28433             ATLASON, Arnor     ISL    Men                      Handball   
      28434             GEIRSSON, Logi     ISL    Men                      Handball   
      28435  GUDJONSSON, Snorri Steinn     ISL    Men                      Handball   
      28436  GUDMUNDSSON, Hreidar Levy     ISL    Men                      Handball   
      28437         GUNNARSSON, Robert     ISL    Men                      Handball   
      28438  GUSTAVSSON, Bjorgvin Pall     ISL    Men                      Handball   
      28439   HALLGRIMSSON, Asgeir Orn     ISL    Men                      Handball   
      28440  INGIMUNDARSON, Ingimundur     ISL    Men                      Handball   
      28441  JAKOBSSON, Sverre Andreas     ISL    Men                      Handball   
      28442       PETERSSON, Alexander     ISL    Men                      Handball   
      28443   SIGURDSSON, Gudjon Valur     ISL    Men                      Handball   
      28444         SIGURDSSON, Sigfus     ISL    Men                      Handball   
      28445         STEFANSSON, Olafur     ISL    Men                      Handball   
      
              Medal  
      9131   Silver  
      17635  Bronze  
      28432  Silver  
      28433  Silver  
      28434  Silver  
      28435  Silver  
      28436  Silver  
      28437  Silver  
      28438  Silver  
      28439  Silver  
      28440  Silver  
      28441  Silver  
      28442  Silver  
      28443  Silver  
      28444  Silver  
      28445  Silver  ),
     (('ISL', 'Women'),
             Year    City      Sport Discipline            Athlete Country Gender  \
      23683  2000  Sydney  Athletics  Athletics  FLOSADOTTIR, Vala     ISL  Women   
      
                  Event   Medal  
      23683  Pole Vault  Bronze  ),
     (('ISR', 'Men'),
             Year       City          Sport       Discipline            Athlete  \
      20816  1992  Barcelona           Judo             Judo  SMADJA, Shay Oren   
      22825  1996    Atlanta        Sailing          Sailing       FRIDMAN, Gal   
      23935  2000     Sydney  Canoe / Kayak  Canoe / Kayak F  KOLGANOV, Michael   
      26625  2004     Athens           Judo             Judo       ZEEVI, Ariel   
      26797  2004     Athens        Sailing          Sailing       FRIDMAN, Gal   
      28819  2008    Beijing        Sailing          Sailing     ZUBARI, Shahar   
      
            Country Gender                          Event   Medal  
      20816     ISR    Men        65 - 71KG (Lightweight)  Bronze  
      22825     ISR    Men                Board (Mistral)  Bronze  
      23935     ISR    Men        K-1 500M (Kayak Single)  Bronze  
      26625     ISR    Men  90 - 100KG (Half-Heavyweight)  Bronze  
      26797     ISR    Men                Board (Mistral)    Gold  
      28819     ISR    Men              Rs:X - Windsurfer  Bronze  ),
     (('ISR', 'Women'),
             Year       City Sport Discipline     Athlete Country Gender  \
      20806  1992  Barcelona  Judo       Judo  ARAD, Yael     ISR  Women   
      
                                     Event   Medal  
      20806  56 - 61KG (Half-Middleweight)  Silver  ),
     (('ISV', 'Men'),
             Year   City    Sport Discipline          Athlete Country Gender  \
      19341  1988  Seoul  Sailing    Sailing  HOLMBERG, Peter     ISV    Men   
      
                                   Event   Medal  
      19341  Single-Handed Dinghy (Finn)  Silver  ),
     (('ITA', 'Men'),
             Year    City       Sport  Discipline                 Athlete Country  \
      350    1900   Paris  Equestrian     Jumping  TRISSINO, Gian Giorgio     ITA   
      356    1900   Paris  Equestrian     Jumping  TRISSINO, Gian Giorgio     ITA   
      376    1900   Paris     Fencing     Fencing          CONTE, Antonio     ITA   
      377    1900   Paris     Fencing     Fencing         SANTELLI, Italo     ITA   
      1241   1908  London   Athletics   Athletics          LUNGHI, Emilio     ITA   
      ...     ...     ...         ...         ...                     ...     ...   
      31007  2012  London  Volleyball  Volleyball           PAPI, Samuele     ITA   
      31008  2012  London  Volleyball  Volleyball          PARODI, Simone     ITA   
      31009  2012  London  Volleyball  Volleyball        SAVANI, Cristian     ITA   
      31010  2012  London  Volleyball  Volleyball         TRAVICA, Dragan     ITA   
      31011  2012  London  Volleyball  Volleyball           ZAYTSEV, Ivan     ITA   
      
            Gender                 Event   Medal  
      350      Men             High Jump    Gold  
      356      Men  Long Jump Individual  Silver  
      376      Men        Sabre, Masters    Gold  
      377      Men        Sabre, Masters  Silver  
      1241     Men                  800M  Silver  
      ...      ...                   ...     ...  
      31007    Men            Volleyball  Bronze  
      31008    Men            Volleyball  Bronze  
      31009    Men            Volleyball  Bronze  
      31010    Men            Volleyball  Bronze  
      31011    Men            Volleyball  Bronze  
      
      [1161 rows x 9 columns]),
     (('ITA', 'Women'),
             Year       City       Sport           Discipline              Athlete  \
      5475   1928  Amsterdam  Gymnastics          Artistic G.   AMBROSETTI, Bianca   
      5476   1928  Amsterdam  Gymnastics          Artistic G.     GIANONI, Lavinia   
      5477   1928  Amsterdam  Gymnastics          Artistic G.    GIAVOTTI, Luigina   
      5478   1928  Amsterdam  Gymnastics          Artistic G.     GIORGI, Virginia   
      5479   1928  Amsterdam  Gymnastics          Artistic G.   MALABARBA, Germana   
      ...     ...        ...         ...                  ...                  ...   
      30383  2012     London  Gymnastics  Gymnastics Rhythmic       SANTONI, Elisa   
      30384  2012     London  Gymnastics  Gymnastics Rhythmic  SAVRAYUK, Anzhelika   
      30385  2012     London  Gymnastics  Gymnastics Rhythmic  STEFANESCU, Andreea   
      30597  2012     London        Judo                 Judo   FORCINITI, Rosalba   
      30875  2012     London    Shooting             Shooting       ROSSI, Jessica   
      
            Country Gender              Event   Medal  
      5475      ITA  Women   Team Competition  Silver  
      5476      ITA  Women   Team Competition  Silver  
      5477      ITA  Women   Team Competition  Silver  
      5478      ITA  Women   Team Competition  Silver  
      5479      ITA  Women   Team Competition  Silver  
      ...       ...    ...                ...     ...  
      30383     ITA  Women  Group Competition  Bronze  
      30384     ITA  Women  Group Competition  Bronze  
      30385     ITA  Women  Group Competition  Bronze  
      30597     ITA  Women          48 - 52KG  Bronze  
      30875     ITA  Women               Trap    Gold  
      
      [135 rows x 9 columns]),
     (('JAM', 'Men'),
             Year         City      Sport     Discipline                 Athlete  \
      7323   1948       London  Athletics      Athletics            WINT, Arthur   
      7324   1948       London  Athletics      Athletics       MCKENLEY, Herbert   
      7372   1948       London  Athletics      Athletics            WINT, Arthur   
      8122   1952     Helsinki  Athletics      Athletics       MCKENLEY, Herbert   
      8142   1952     Helsinki  Athletics      Athletics  RHODEN, Vincent George   
      8143   1952     Helsinki  Athletics      Athletics       MCKENLEY, Herbert   
      8175   1952     Helsinki  Athletics      Athletics           LAING, Leslie   
      8176   1952     Helsinki  Athletics      Athletics       MCKENLEY, Herbert   
      8177   1952     Helsinki  Athletics      Athletics  RHODEN, Vincent George   
      8178   1952     Helsinki  Athletics      Athletics            WINT, Arthur   
      8191   1952     Helsinki  Athletics      Athletics            WINT, Arthur   
      11866  1968       Mexico  Athletics      Athletics          MILLER, Lennox   
      12901  1972       Munich  Athletics      Athletics          MILLER, Lennox   
      14070  1976     Montreal  Athletics      Athletics         QUARRIE, Donald   
      14087  1976     Montreal  Athletics      Athletics         QUARRIE, Donald   
      15391  1980       Moscow  Athletics      Athletics         QUARRIE, Donald   
      15708  1980       Moscow    Cycling  Cycling Track           WELLER, David   
      16847  1984  Los Angeles  Athletics      Athletics        LAWRENCE, Albert   
      16848  1984  Los Angeles  Athletics      Athletics         MEGHOO, Gregory   
      16849  1984  Los Angeles  Athletics      Athletics         QUARRIE, Donald   
      16850  1984  Los Angeles  Athletics      Athletics            STEWART, Ray   
      18360  1988        Seoul  Athletics      Athletics       CAMERON, Bertland   
      18361  1988        Seoul  Athletics      Athletics           DAVIS, Howard   
      18362  1988        Seoul  Athletics      Athletics        GRAHAM, Winthrop   
      18363  1988        Seoul  Athletics      Athletics           MORRIS, Devon   
      19899  1992    Barcelona  Athletics      Athletics        GRAHAM, Winthrop   
      21669  1996      Atlanta  Athletics      Athletics   BLAKE, Dennis Anthony   
      21670  1996      Atlanta  Athletics      Athletics          CLARKE, Davian   
      21671  1996      Atlanta  Athletics      Athletics          HAUGHTON, Greg   
      21672  1996      Atlanta  Athletics      Athletics         MARTIN, Roxbert   
      21673  1996      Atlanta  Athletics      Athletics       MCDONALD, Michael   
      21674  1996      Atlanta  Athletics      Athletics         ROBINSON, Garth   
      21743  1996      Atlanta  Athletics      Athletics         BECKFORD, James   
      23553  2000       Sydney  Athletics      Athletics          HAUGHTON, Greg   
      23594  2000       Sydney  Athletics      Athletics            AYRE, Sanjay   
      23595  2000       Sydney  Athletics      Athletics      BLACKWOOD, Michael   
      23596  2000       Sydney  Athletics      Athletics          HAUGHTON, Greg   
      23597  2000       Sydney  Athletics      Athletics       MCDONALD, Michael   
      23598  2000       Sydney  Athletics      Athletics        MCFARLANE, Danny   
      23599  2000       Sydney  Athletics      Athletics   WILLIAMS, Christopher   
      25579  2004       Athens  Athletics      Athletics        MCFARLANE, Danny   
      27552  2008      Beijing  Athletics      Athletics             BOLT, Usain   
      27570  2008      Beijing  Athletics      Athletics             BOLT, Usain   
      27603  2008      Beijing  Athletics      Athletics             BOLT, Usain   
      27604  2008      Beijing  Athletics      Athletics           CARTER, Nesta   
      27605  2008      Beijing  Athletics      Athletics         FRATER, Michael   
      27606  2008      Beijing  Athletics      Athletics           POWELL, Asafa   
      29588  2012       London  Athletics      Athletics             BOLT, Usain   
      29589  2012       London  Athletics      Athletics            BLAKE, Yohan   
      29599  2012       London  Athletics      Athletics       PARCHMENT, Hansle   
      29606  2012       London  Athletics      Athletics             BOLT, Usain   
      29607  2012       London  Athletics      Athletics            BLAKE, Yohan   
      29608  2012       London  Athletics      Athletics            WEIR, Warren   
      29636  2012       London  Athletics      Athletics      BAILEY-COLE, Kemar   
      29637  2012       London  Athletics      Athletics            BLAKE, Yohan   
      29638  2012       London  Athletics      Athletics             BOLT, Usain   
      29639  2012       London  Athletics      Athletics           CARTER, Nesta   
      29640  2012       London  Athletics      Athletics         FRATER, Michael   
      
            Country Gender           Event   Medal  
      7323      JAM    Men            400M    Gold  
      7324      JAM    Men            400M  Silver  
      7372      JAM    Men            800M  Silver  
      8122      JAM    Men            100M  Silver  
      8142      JAM    Men            400M    Gold  
      8143      JAM    Men            400M  Silver  
      8175      JAM    Men    4X400M Relay    Gold  
      8176      JAM    Men    4X400M Relay    Gold  
      8177      JAM    Men    4X400M Relay    Gold  
      8178      JAM    Men    4X400M Relay    Gold  
      8191      JAM    Men            800M  Silver  
      11866     JAM    Men            100M  Silver  
      12901     JAM    Men            100M  Bronze  
      14070     JAM    Men            100M  Silver  
      14087     JAM    Men            200M    Gold  
      15391     JAM    Men            200M  Bronze  
      15708     JAM    Men  1KM Time Trial  Bronze  
      16847     JAM    Men    4X100M Relay  Silver  
      16848     JAM    Men    4X100M Relay  Silver  
      16849     JAM    Men    4X100M Relay  Silver  
      16850     JAM    Men    4X100M Relay  Silver  
      18360     JAM    Men    4X400M Relay  Silver  
      18361     JAM    Men    4X400M Relay  Silver  
      18362     JAM    Men    4X400M Relay  Silver  
      18363     JAM    Men    4X400M Relay  Silver  
      19899     JAM    Men    400M Hurdles  Silver  
      21669     JAM    Men    4X400M Relay  Bronze  
      21670     JAM    Men    4X400M Relay  Bronze  
      21671     JAM    Men    4X400M Relay  Bronze  
      21672     JAM    Men    4X400M Relay  Bronze  
      21673     JAM    Men    4X400M Relay  Bronze  
      21674     JAM    Men    4X400M Relay  Bronze  
      21743     JAM    Men       Long Jump  Silver  
      23553     JAM    Men            400M  Bronze  
      23594     JAM    Men    4X400M Relay  Bronze  
      23595     JAM    Men    4X400M Relay  Bronze  
      23596     JAM    Men    4X400M Relay  Bronze  
      23597     JAM    Men    4X400M Relay  Bronze  
      23598     JAM    Men    4X400M Relay  Bronze  
      23599     JAM    Men    4X400M Relay  Bronze  
      25579     JAM    Men    400M Hurdles  Silver  
      27552     JAM    Men            100M    Gold  
      27570     JAM    Men            200M    Gold  
      27603     JAM    Men    4X100M Relay    Gold  
      27604     JAM    Men    4X100M Relay    Gold  
      27605     JAM    Men    4X100M Relay    Gold  
      27606     JAM    Men    4X100M Relay    Gold  
      29588     JAM    Men            100M    Gold  
      29589     JAM    Men            100M  Silver  
      29599     JAM    Men    110M Hurdles  Bronze  
      29606     JAM    Men            200M    Gold  
      29607     JAM    Men            200M  Silver  
      29608     JAM    Men            200M  Bronze  
      29636     JAM    Men    4X100M Relay    Gold  
      29637     JAM    Men    4X100M Relay    Gold  
      29638     JAM    Men    4X100M Relay    Gold  
      29639     JAM    Men    4X100M Relay    Gold  
      29640     JAM    Men    4X100M Relay    Gold  ),
     (('JAM', 'Women'),
             Year         City      Sport Discipline                  Athlete  \
      15394  1980       Moscow  Athletics  Athletics      OTTEY-PAGE, Merlene   
      16796  1984  Los Angeles  Athletics  Athletics      OTTEY-PAGE, Merlene   
      16815  1984  Los Angeles  Athletics  Athletics      OTTEY-PAGE, Merlene   
      18306  1988        Seoul  Athletics  Athletics     JACKSON SMALL, Grace   
      19863  1992    Barcelona  Athletics  Athletics         CUTHBERT, Juliet   
      ...     ...          ...        ...        ...                      ...   
      29690  2012       London  Athletics  Athletics           DAY, Christine   
      29691  2012       London  Athletics  Athletics          LLOYD, Shereefa   
      29692  2012       London  Athletics  Athletics         WHYTE, Rosemarie   
      29693  2012       London  Athletics  Athletics       WILLIAMS, Shericka   
      29694  2012       London  Athletics  Athletics  WILLIAMS-MILLS, Novlene   
      
            Country Gender         Event   Medal  
      15394     JAM  Women          200M  Bronze  
      16796     JAM  Women          100M  Bronze  
      16815     JAM  Women          200M  Bronze  
      18306     JAM  Women          200M  Silver  
      19863     JAM  Women          100M  Silver  
      ...       ...    ...           ...     ...  
      29690     JAM  Women  4X400M Relay  Bronze  
      29691     JAM  Women  4X400M Relay  Bronze  
      29692     JAM  Women  4X400M Relay  Bronze  
      29693     JAM  Women  4X400M Relay  Bronze  
      29694     JAM  Women  4X400M Relay  Bronze  
      
      [69 rows x 9 columns]),
     (('JPN', 'Men'),
             Year       City      Sport           Discipline               Athlete  \
      4030   1920    Antwerp     Tennis               Tennis     KASHIO, Seiichiro   
      4031   1920    Antwerp     Tennis               Tennis       KUMAGAE, Ichiya   
      4046   1920    Antwerp     Tennis               Tennis       KUMAGAE, Ichiya   
      4971   1924      Paris  Wrestling      Wrestling Free.     NAITO, Katsutoshi   
      5022   1928  Amsterdam   Aquatics             Swimming      TAKAISHI, Katsuo   
      ...     ...        ...        ...                  ...                   ...   
      30616  2012     London       Judo                 Judo          NAKAYA, Riki   
      30630  2012     London       Judo                 Judo    NISHIYAMA, Masashi   
      31104  2012     London  Wrestling  Wrestling Freestyle      YUMOTO, Shinichi   
      31117  2012     London  Wrestling  Wrestling Freestyle  YONEMITSU, Tatsuhiro   
      31148  2012     London  Wrestling  Wrestling Freestyle    MATSUMOTO, Ryutaro   
      
            Country Gender                      Event   Medal  
      4030      JPN    Men                    Doubles  Silver  
      4031      JPN    Men                    Doubles  Silver  
      4046      JPN    Men                    Singles  Silver  
      4971      JPN    Men  56 - 61KG (Featherweight)  Bronze  
      5022      JPN    Men             100M Freestyle  Bronze  
      ...       ...    ...                        ...     ...  
      30616     JPN    Men                  66 - 73KG  Silver  
      30630     JPN    Men                  81 - 90KG  Bronze  
      31104     JPN    Men                   Wf 55 KG  Bronze  
      31117     JPN    Men                   Wf 66 KG    Gold  
      31148     JPN    Men                   Wg 60 KG  Bronze  
      
      [525 rows x 9 columns]),
     (('JPN', 'Women'),
             Year         City          Sport           Discipline  \
      5162   1928    Amsterdam      Athletics            Athletics   
      5746   1932  Los Angeles       Aquatics             Swimming   
      6360   1936       Berlin       Aquatics             Swimming   
      9807   1960         Rome       Aquatics             Swimming   
      11314  1964        Tokyo     Gymnastics          Artistic G.   
      ...     ...          ...            ...                  ...   
      31047  2012       London     Volleyball           Volleyball   
      31058  2012       London  Weightlifting        Weightlifting   
      31097  2012       London      Wrestling  Wrestling Freestyle   
      31105  2012       London      Wrestling  Wrestling Freestyle   
      31113  2012       London      Wrestling  Wrestling Freestyle   
      
                          Athlete Country Gender              Event   Medal  
      5162          HITOMI, Kinue     JPN  Women               800M  Silver  
      5746        MAEHATA, Hideko     JPN  Women  200M Breaststroke  Silver  
      6360        MAEHATA, Hideko     JPN  Women  200M Breaststroke    Gold  
      9807         TANAKA, Satoko     JPN  Women    100M Backstroke  Bronze  
      11314  ABUKAWA-CHIBA, Ginko     JPN  Women   Team Competition  Bronze  
      ...                     ...     ...    ...                ...     ...  
      31047        YAMAGUCHI, Mai     JPN  Women         Volleyball  Bronze  
      31058        MIYAKE, Hiromi     JPN  Women               48KG  Silver  
      31097         OBARA, Hitomi     JPN  Women           Wf 48 KG    Gold  
      31105        YOSHIDA, Saori     JPN  Women           Wf 55 KG    Gold  
      31113           ICHO, Kaori     JPN  Women           Wf 63 KG    Gold  
      
      [263 rows x 9 columns]),
     (('KAZ', 'Men'),
             Year     City              Sport           Discipline  \
      21935  1996  Atlanta             Boxing               Boxing   
      21949  1996  Atlanta             Boxing               Boxing   
      21956  1996  Atlanta             Boxing               Boxing   
      21966  1996  Atlanta             Boxing               Boxing   
      22667  1996  Atlanta  Modern Pentathlon      Modern Pentath.   
      22876  1996  Atlanta           Shooting             Shooting   
      22887  1996  Atlanta           Shooting             Shooting   
      22890  1996  Atlanta           Shooting             Shooting   
      23097  1996  Atlanta      Weightlifting        Weightlifting   
      23107  1996  Atlanta          Wrestling      Wrestling Free.   
      23141  1996  Atlanta          Wrestling      Wrestling Gre-R   
      23873  2000   Sydney             Boxing               Boxing   
      23877  2000   Sydney             Boxing               Boxing   
      23884  2000   Sydney             Boxing               Boxing   
      23900  2000   Sydney             Boxing               Boxing   
      24000  2000   Sydney            Cycling         Cycling Road   
      25148  2000   Sydney          Wrestling      Wrestling Free.   
      25655  2004   Athens          Athletics            Athletics   
      25901  2004   Athens             Boxing               Boxing   
      25910  2004   Athens             Boxing               Boxing   
      25915  2004   Athens             Boxing               Boxing   
      27113  2004   Athens      Weightlifting        Weightlifting   
      27143  2004   Athens          Wrestling      Wrestling Free.   
      27159  2004   Athens          Wrestling      Wrestling Gre-R   
      27173  2004   Athens          Wrestling      Wrestling Gre-R   
      27920  2008  Beijing             Boxing               Boxing   
      27927  2008  Beijing             Boxing               Boxing   
      28641  2008  Beijing               Judo                 Judo   
      28972  2008  Beijing          Taekwondo            Taekwondo   
      29143  2008  Beijing      Weightlifting        Weightlifting   
      29184  2008  Beijing          Wrestling      Wrestling Free.   
      29186  2008  Beijing          Wrestling      Wrestling Free.   
      29193  2008  Beijing          Wrestling      Wrestling Gre-R   
      29208  2008  Beijing          Wrestling      Wrestling Gre-R   
      29870  2012   London             Boxing               Boxing   
      29900  2012   London             Boxing               Boxing   
      29909  2012   London             Boxing               Boxing   
      30007  2012   London            Cycling         Cycling Road   
      31120  2012   London          Wrestling  Wrestling Freestyle   
      31159  2012   London          Wrestling  Wrestling Freestyle   
      
                             Athlete Country Gender  \
      21935        DZUMADILOV, Bulat     KAZ    Men   
      21949      NIYAZYMBETOV, Bolat     KAZ    Men   
      21956       IBZAIMOV, Ezmouhan     KAZ    Men   
      21966           JIROV, Vasilii     KAZ    Men   
      22667       PARYGIN, Alexander     KAZ    Men   
      22876    VOKHMIANINE, Vladimir     KAZ    Men   
      22887          BELIAEV, Sergey     KAZ    Men   
      22890          BELIAEV, Sergey     KAZ    Men   
      23097        KHRAPATY, Anatoli     KAZ    Men   
      23107          MAMYROV, Maulen     KAZ    Men   
      23141       MELNICHENKO, Yuriy     KAZ    Men   
      23873  DILDABEKOV, Mukhtarkhan     KAZ    Men   
      23877         JUMADILOV, Bulat     KAZ    Men   
      23884     SATTARKHANOV, Bekzat     KAZ    Men   
      23900      IBRAIMOV, Yermakhan     KAZ    Men   
      24000      VINOKUROV, Alexandr     KAZ    Men   
      25148        BAIRAMUKOV, Islam     KAZ    Men   
      25655          KARPOV, Dmitriy     KAZ    Men   
      25901           YELEUOV, Serik     KAZ    Men   
      25910       ARTAYEV, Bakhtiyar     KAZ    Men   
      25915       GOLOVKIN, Gennadiy     KAZ    Men   
      27113        FILIMONOV, Sergey     KAZ    Men   
      27143        LALIYEV, Gennadiy     KAZ    Men   
      27159       MANUKYAN, Mkkhitar     KAZ    Men   
      27173      TSURTSUMIA, Georgiy     KAZ    Men   
      27920      SARSEKBAYEV, Bakhyt     KAZ    Men   
      27927   SHYNALIYEV, Yerkebulan     KAZ    Men   
      28641        ZHITKEYEV, Askhat     KAZ    Men   
      28972         CHILMANOV, Arman     KAZ    Men   
      29143               ILIN, Ilya     KAZ    Men   
      29184        TIGIYEV, Taimuraz     KAZ    Men   
      29186         MUTALIMOV, Marid     KAZ    Men   
      29193    TENGIZBAYEV, Nurbakyt     KAZ    Men   
      29208          MAMBETOV, Asset     KAZ    Men   
      29870             DYCHKO, Ivan     KAZ    Men   
      29900           SAPIYEV, Serik     KAZ    Men   
      29909    NIYAZYMBETOV, Adilbek     KAZ    Men   
      30007      VINOKUROV, Alexandr     KAZ    Men   
      31120      TANATAROV, Akzhurek     KAZ    Men   
      31159          GAJIYEV, Danyal     KAZ    Men   
      
                                            Event   Medal  
      21935                 48 - 51KG (Flyweight)  Silver  
      21949      60 - 63.5KG (Light-Welterweight)  Bronze  
      21956        67 - 71KG (Light-Middleweight)  Bronze  
      21966         75 - 81KG (Light-Heavyweight)    Gold  
      22667                Individual Competition    Gold  
      22876      25M Rapid Fire Pistol (60 Shots)  Bronze  
      22887    50M Rifle 3 Positions (3X40 Shots)  Silver  
      22890            50M Rifle Prone (60 Shots)  Silver  
      23097  91 - 99KG, Total (First-Heavyweight)  Silver  
      23107                 48 - 52KG (Flyweight)  Bronze  
      23141              52 - 57KG (Bantamweight)    Gold  
      23873            + 91KG (Super Heavyweight)  Silver  
      23877                 48 - 51KG (Flyweight)  Silver  
      23884             54 - 57KG (Featherweight)    Gold  
      23900        67 - 71KG (Light-Middleweight)    Gold  
      24000                  Individual Road Race  Silver  
      25148                             85 - 97KG  Silver  
      25655                             Decathlon  Bronze  
      25901               57 - 60KG (Lightweight)  Bronze  
      25910                            64 - 69 KG    Gold  
      25915                            69 - 75 KG  Silver  
      27113                                  77KG  Silver  
      27143                             66 - 74KG  Silver  
      27159                             60 - 66KG  Bronze  
      27173                            96 - 120KG  Silver  
      27920                            64 - 69 KG    Gold  
      27927         75 - 81KG (Light-Heavyweight)  Bronze  
      28641         90 - 100KG (Half-Heavyweight)  Silver  
      28972                               + 80 KG  Bronze  
      29143                                  94KG    Gold  
      29184                             84 - 96KG  Silver  
      29186                            96 - 120KG  Bronze  
      29193                             55 - 60KG  Bronze  
      29208                             84 - 96KG  Bronze  
      29870                                + 91KG  Bronze  
      29900                            64 - 69 KG    Gold  
      29909                             75 - 81KG  Silver  
      30007                       Individual Road    Gold  
      31120                              Wf 66 KG  Bronze  
      31159                              Wg 84 KG  Bronze  ),
     (('KAZ', 'Women'),
             Year     City          Sport           Discipline  \
      23527  2000   Sydney      Athletics            Athletics   
      29106  2008  Beijing  Weightlifting        Weightlifting   
      29126  2008  Beijing  Weightlifting        Weightlifting   
      29135  2008  Beijing  Weightlifting        Weightlifting   
      29162  2008  Beijing      Wrestling      Wrestling Free.   
      29769  2012   London      Athletics            Athletics   
      29915  2012   London         Boxing               Boxing   
      31080  2012   London  Weightlifting        Weightlifting   
      31123  2012   London      Wrestling  Wrestling Freestyle   
      
                           Athlete Country Gender         Event   Medal  
      23527       SHISHIGINA, Olga     KAZ  Women  100M Hurdles    Gold  
      29106  GRABOVETSKAYA, Mariya     KAZ  Women        + 75KG  Bronze  
      29126      NEKRASSOVA, Irina     KAZ  Women          63KG  Silver  
      29135        VAZHENINA, Alla     KAZ  Women          75KG  Silver  
      29162      SHALYGINA, Yelena     KAZ  Women     55 - 63KG  Bronze  
      29769         RYPAKOVA, Olga     KAZ  Women   Triple Jump    Gold  
      29915        VOLNOVA, Marina     KAZ  Women         75 KG  Bronze  
      31080  NURMUKHAMBETOVA, Anna     KAZ  Women          69KG  Bronze  
      31123       MANYUROVA, Guzel     KAZ  Women      Wf 72 KG  Bronze  ),
     (('KEN', 'Men'),
             Year    City      Sport Discipline                    Athlete Country  \
      10897  1964   Tokyo  Athletics  Athletics     KIPRUGUT, Wilson Chuma     KEN   
      11862  1968  Mexico  Athletics  Athletics       TEMU, Nabiba Naftali     KEN   
      11874  1968  Mexico  Athletics  Athletics            KEINO, Kipchoge     KEN   
      11886  1968  Mexico  Athletics  Athletics      BIWOTT, Amos Kipwabok     KEN   
      11887  1968  Mexico  Athletics  Athletics             KOGO, Benjamin     KEN   
      ...     ...     ...        ...        ...                        ...     ...   
      29697  2012  London  Athletics  Athletics   LONGOSIWA, Thomas Pkemei     KEN   
      29704  2012  London  Athletics  Athletics      RUDISHA, David Lekuta     KEN   
      29706  2012  London  Athletics  Athletics             KITUM, Timothy     KEN   
      29749  2012  London  Athletics  Athletics                KIRUI, Abel     KEN   
      29750  2012  London  Athletics  Athletics  KIPROTICH, Wilson Kipsang     KEN   
      
            Gender               Event   Medal  
      10897    Men                800M  Bronze  
      11862    Men              10000M    Gold  
      11874    Men               1500M    Gold  
      11886    Men  3000M Steeplechase    Gold  
      11887    Men  3000M Steeplechase  Silver  
      ...      ...                 ...     ...  
      29697    Men               5000M  Bronze  
      29704    Men                800M    Gold  
      29706    Men                800M  Bronze  
      29749    Men            Marathon  Silver  
      29750    Men            Marathon  Bronze  
      
      [80 rows x 9 columns]),
     (('KEN', 'Women'),
             Year     City      Sport Discipline                     Athlete  \
      21704  1996  Atlanta  Athletics  Athletics              KONGA, Pauline   
      25645  2004   Athens  Athletics  Athletics           OCHICHI, Isabella   
      25696  2004   Athens  Athletics  Athletics          NDEREBA, Catherine   
      27567  2008  Beijing  Athletics  Athletics         LANGAT, Nancy jebet   
      27586  2008  Beijing  Athletics  Athletics            JEPKORIR, Eunice   
      27660  2008  Beijing  Athletics  Athletics              JELIMO, Pamela   
      27661  2008  Beijing  Athletics  Athletics  BUSIENEI, Janeth Jepkosgei   
      27703  2008  Beijing  Athletics  Athletics          NDEREBA, Catherine   
      29586  2012   London  Athletics  Athletics    KIPYEGO, Sally Jepkosgei   
      29587  2012   London  Athletics  Athletics           CHERUIYOT, Vivian   
      29623  2012   London  Athletics  Athletics       CHEYWA, Milcah Chemos   
      29699  2012   London  Athletics  Athletics           CHERUIYOT, Vivian   
      29752  2012   London  Athletics  Athletics             JEPTOO, Priscah   
      
            Country Gender               Event   Medal  
      21704     KEN  Women               5000M  Silver  
      25645     KEN  Women               5000M  Silver  
      25696     KEN  Women            Marathon  Silver  
      27567     KEN  Women               1500M    Gold  
      27586     KEN  Women  3000M Steeplechase  Silver  
      27660     KEN  Women                800M    Gold  
      27661     KEN  Women                800M  Silver  
      27703     KEN  Women            Marathon  Silver  
      29586     KEN  Women              10000M  Silver  
      29587     KEN  Women              10000M  Bronze  
      29623     KEN  Women       3000M Steeple  Bronze  
      29699     KEN  Women               5000M  Silver  
      29752     KEN  Women            Marathon  Silver  ),
     (('KGZ', 'Men'),
             Year     City      Sport       Discipline             Athlete Country  \
      24582  2000   Sydney       Judo             Judo     SMAGULOV, Aidyn     KGZ   
      29194  2008  Beijing  Wrestling  Wrestling Gre-R  TIUMENBAEV, Ruslan     KGZ   
      29200  2008  Beijing  Wrestling  Wrestling Gre-R  BEGALIEV, Kanatbek     KGZ   
      
            Gender      Event   Medal  
      24582    Men    - 60 KG  Bronze  
      29194    Men  55 - 60KG  Bronze  
      29200    Men  60 - 66KG  Silver  ),
     (('KOR', 'Men'),
             Year                   City          Sport           Discipline  \
      7461   1948                 London         Boxing               Boxing   
      7964   1948                 London  Weightlifting        Weightlifting   
      8289   1952               Helsinki         Boxing               Boxing   
      8850   1952               Helsinki  Weightlifting        Weightlifting   
      9179   1956  Melbourne / Stockholm         Boxing               Boxing   
      ...     ...                    ...            ...                  ...   
      30888  2012                 London   Table Tennis         Table Tennis   
      30889  2012                 London   Table Tennis         Table Tennis   
      30907  2012                 London      Taekwondo            Taekwondo   
      31092  2012                 London  Weightlifting        Weightlifting   
      31149  2012                 London      Wrestling  Wrestling Freestyle   
      
                     Athlete Country Gender                              Event  \
      7461       HAN, Soo-An     KOR    Men                 - 51KG (Flyweight)   
      7964     KIM, Sung-Jip     KOR    Men  67.5 - 75KG, Total (Middleweight)   
      8289     KANG, Joon-Ho     KOR    Men           51 - 54KG (Bantamweight)   
      8850     KIM, Sung-Jip     KOR    Men  67.5 - 75KG, Total (Middleweight)   
      9179   SONG, Soon-Chun     KOR    Men           51 - 54KG (Bantamweight)   
      ...                ...     ...    ...                                ...   
      30888      OH, Sangeun     KOR    Men                               Team   
      30889    RYU, Seungmin     KOR    Men                               Team   
      30907     LEE, Daehoon     KOR    Men                            - 58 KG   
      31092      KIM, Minjae     KOR    Men                               94KG   
      31149    KIM, Hyeonwoo     KOR    Men                           Wg 66 KG   
      
              Medal  
      7461   Bronze  
      7964   Bronze  
      8289   Bronze  
      8850   Bronze  
      9179   Silver  
      ...       ...  
      30888  Silver  
      30889  Silver  
      30907  Silver  
      31092  Bronze  
      31149    Gold  
      
      [288 rows x 9 columns]),
     (('KOR', 'Women'),
             Year      City          Sport     Discipline            Athlete  \
      15082  1976  Montreal     Volleyball     Volleyball    BAIK, Myung-Sun   
      15083  1976  Montreal     Volleyball     Volleyball     BYON, Kyung-Ja   
      15084  1976  Montreal     Volleyball     Volleyball    CHANG, Hee-Sook   
      15085  1976  Montreal     Volleyball     Volleyball      JO, Hae-Chung   
      15086  1976  Montreal     Volleyball     Volleyball      JUNG, Soon-Ok   
      ...     ...       ...            ...            ...                ...   
      30173  2012    London        Fencing        Fencing          OH, Ha Na   
      30177  2012    London        Fencing        Fencing        KIM, Jiyeon   
      30845  2012    London       Shooting       Shooting        KIM, Jangmi   
      30922  2012    London      Taekwondo      Taekwondo  HWANG, Kyung Seon   
      31053  2012    London  Weightlifting  Weightlifting       JANG, Mi-ran   
      
            Country Gender             Event   Medal  
      15082     KOR  Women        Volleyball  Bronze  
      15083     KOR  Women        Volleyball  Bronze  
      15084     KOR  Women        Volleyball  Bronze  
      15085     KOR  Women        Volleyball  Bronze  
      15086     KOR  Women        Volleyball  Bronze  
      ...       ...    ...               ...     ...  
      30173     KOR  Women         Foil Team  Bronze  
      30177     KOR  Women  Sabre Individual    Gold  
      30845     KOR  Women        25M Pistol    Gold  
      30922     KOR  Women        57 - 67 KG    Gold  
      31053     KOR  Women             +75KG  Bronze  
      
      [241 rows x 9 columns]),
     (('KSA', 'Men'),
             Year    City       Sport Discipline                       Athlete  \
      23561  2000  Sydney   Athletics  Athletics                 SOMAYLI, Hadi   
      24103  2000  Sydney  Equestrian    Jumping                 ALEID, Khaled   
      30122  2012  London  Equestrian    Jumping              AL DUHAMI, Ramzy   
      30123  2012  London  Equestrian    Jumping  AL SAUD, HRH Prince Abdullah   
      30124  2012  London  Equestrian    Jumping               BAHAMDAN, Kamal   
      30125  2012  London  Equestrian    Jumping    SHARBATLY, Abdullah Waleed   
      
            Country Gender         Event   Medal  
      23561     KSA    Men  400M Hurdles  Silver  
      24103     KSA    Men    Individual  Bronze  
      30122     KSA    Men          Team  Bronze  
      30123     KSA    Men          Team  Bronze  
      30124     KSA    Men          Team  Bronze  
      30125     KSA    Men          Team  Bronze  ),
     (('KUW', 'Men'),
             Year    City     Sport Discipline            Athlete Country Gender  \
      24873  2000  Sydney  Shooting   Shooting  ALDEEHANI, Fehaid     KUW    Men   
      30874  2012  London  Shooting   Shooting  ALDEEHANI, Fehaid     KUW    Men   
      
                                 Event   Medal  
      24873  Double Trap (150 Targets)  Bronze  
      30874                       Trap  Bronze  ),
     (('LAT', 'Men'),
             Year         City          Sport        Discipline  \
      5870   1932  Los Angeles      Athletics         Athletics   
      6489   1936       Berlin      Athletics         Athletics   
      7203   1936       Berlin      Wrestling   Wrestling Gre-R   
      20233  1992    Barcelona  Canoe / Kayak   Canoe / Kayak F   
      20315  1992    Barcelona        Cycling      Cycling Road   
      21071  1992    Barcelona       Shooting          Shooting   
      21974  1996      Atlanta  Canoe / Kayak   Canoe / Kayak F   
      23630  2000       Sydney      Athletics         Athletics   
      24296  2000       Sydney     Gymnastics       Artistic G.   
      24614  2000       Sydney           Judo              Judo   
      25681  2004       Athens      Athletics         Athletics   
      26358  2004       Athens     Gymnastics       Artistic G.   
      27080  2004       Athens  Weightlifting     Weightlifting   
      27688  2008      Beijing      Athletics         Athletics   
      28019  2008      Beijing        Cycling               BMX   
      29103  2008      Beijing  Weightlifting     Weightlifting   
      30001  2012       London        Cycling       Cycling BMX   
      30968  2012       London     Volleyball  Beach Volleyball   
      30969  2012       London     Volleyball  Beach Volleyball   
      
                         Athlete Country Gender                             Event  \
      5870         DALINS, Janis     LAT    Men                         50KM Walk   
      6489    BUBENKO, Adalberts     LAT    Men                         50KM Walk   
      7203       BIETAGS, Edwins     LAT    Men     79 - 87KG (Light-Heavyweight)   
      20233    KLEMENTYEV, Ivans     LAT    Men          C-1 1000M (Canoe Single)   
      20315        OZOLS, Dainis     LAT    Men              Individual Road Race   
      21071   KUZMINS, Afanasijs     LAT    Men  25M Rapid Fire Pistol (60 Shots)   
      21974    KLEMENTYEV, Ivans     LAT    Men          C-1 1000M (Canoe Single)   
      23630     FADEJEVS, Aigars     LAT    Men                         50KM Walk   
      24296       VIHROVS, Igors     LAT    Men                   Floor Exercises   
      24614  ZELONIJS, Vsevolods     LAT    Men           66 - 73KG (Lightweight)   
      25681  VASILEVSKIS, Vadims     LAT    Men                     Javelin Throw   
      26358   SAPRONENKO, Evgeni     LAT    Men                             Vault   
      27080  SCERBATIHS, Viktors     LAT    Men                           + 105KG   
      27688       KOVALS, Ainars     LAT    Men                     Javelin Throw   
      28019    STROMBERGS, Maris     LAT    Men                        Individual   
      29103  SCERBATIHS, Viktors     LAT    Men                           + 105KG   
      30001    STROMBERGS, Maris     LAT    Men                        Individual   
      30968     PLAVINS, Martins     LAT    Men                  Beach Volleyball   
      30969       SMEDINS, Janis     LAT    Men                  Beach Volleyball   
      
              Medal  
      5870   Silver  
      6489   Bronze  
      7203   Silver  
      20233  Silver  
      20315  Bronze  
      21071  Silver  
      21974  Silver  
      23630  Silver  
      24296    Gold  
      24614  Bronze  
      25681  Silver  
      26358  Silver  
      27080  Silver  
      27688  Silver  
      28019    Gold  
      29103  Bronze  
      30001    Gold  
      30968  Bronze  
      30969  Bronze  ),
     (('LAT', 'Women'),
             Year    City              Sport       Discipline           Athlete  \
      26633  2004  Athens  Modern Pentathlon  Modern Pentath.  RUBLEVSKA, Elena   
      
            Country Gender                   Event   Medal  
      26633     LAT  Women  Individual Competition  Silver  ),
     (('LIB', 'Men'),
             Year      City          Sport       Discipline  \
      8891   1952  Helsinki      Wrestling  Wrestling Gre-R   
      8898   1952  Helsinki      Wrestling  Wrestling Gre-R   
      13830  1972    Munich  Weightlifting    Weightlifting   
      16565  1980    Moscow      Wrestling  Wrestling Gre-R   
      
                              Athlete Country Gender  \
      8891            CHIHAB, Zakaria     LIB    Men   
      8898               TAHA, Khalil     LIB    Men   
      13830  TARABULSI, Kheir Mohamed     LIB    Men   
      16565            BCHARA, Hassan     LIB    Men   
      
                                         Event   Medal  
      8891            52 - 57KG (Bantamweight)  Silver  
      8898            67 - 73KG (Welterweight)  Bronze  
      13830  67.5 - 75KG, Total (Middleweight)  Silver  
      16565        + 100KG (Super Heavyweight)  Bronze  ),
     (('LTU', 'Men'),
             Year       City              Sport           Discipline  \
      19978  1992  Barcelona          Athletics            Athletics   
      20111  1992  Barcelona         Basketball           Basketball   
      20112  1992  Barcelona         Basketball           Basketball   
      20113  1992  Barcelona         Basketball           Basketball   
      20114  1992  Barcelona         Basketball           Basketball   
      20115  1992  Barcelona         Basketball           Basketball   
      20116  1992  Barcelona         Basketball           Basketball   
      20117  1992  Barcelona         Basketball           Basketball   
      20118  1992  Barcelona         Basketball           Basketball   
      20119  1992  Barcelona         Basketball           Basketball   
      20120  1992  Barcelona         Basketball           Basketball   
      20121  1992  Barcelona         Basketball           Basketball   
      20122  1992  Barcelona         Basketball           Basketball   
      21852  1996    Atlanta         Basketball           Basketball   
      21853  1996    Atlanta         Basketball           Basketball   
      21854  1996    Atlanta         Basketball           Basketball   
      21855  1996    Atlanta         Basketball           Basketball   
      21856  1996    Atlanta         Basketball           Basketball   
      21857  1996    Atlanta         Basketball           Basketball   
      21858  1996    Atlanta         Basketball           Basketball   
      21859  1996    Atlanta         Basketball           Basketball   
      21860  1996    Atlanta         Basketball           Basketball   
      21861  1996    Atlanta         Basketball           Basketball   
      21862  1996    Atlanta         Basketball           Basketball   
      21863  1996    Atlanta         Basketball           Basketball   
      23641  2000     Sydney          Athletics            Athletics   
      23794  2000     Sydney         Basketball           Basketball   
      23795  2000     Sydney         Basketball           Basketball   
      23796  2000     Sydney         Basketball           Basketball   
      23797  2000     Sydney         Basketball           Basketball   
      23798  2000     Sydney         Basketball           Basketball   
      23799  2000     Sydney         Basketball           Basketball   
      23800  2000     Sydney         Basketball           Basketball   
      23801  2000     Sydney         Basketball           Basketball   
      23802  2000     Sydney         Basketball           Basketball   
      23803  2000     Sydney         Basketball           Basketball   
      23804  2000     Sydney         Basketball           Basketball   
      23805  2000     Sydney         Basketball           Basketball   
      25659  2004     Athens          Athletics            Athletics   
      26630  2004     Athens  Modern Pentathlon      Modern Pentath.   
      27665  2008    Beijing          Athletics            Athletics   
      28642  2008    Beijing  Modern Pentathlon      Modern Pentath.   
      28644  2008    Beijing  Modern Pentathlon      Modern Pentath.   
      29212  2008    Beijing          Wrestling      Wrestling Gre-R   
      29890  2012     London             Boxing               Boxing   
      29939  2012     London              Canoe         Canoe Sprint   
      31156  2012     London          Wrestling  Wrestling Freestyle   
      
                             Athlete Country Gender                   Event   Medal  
      19978           UBARTAS, Romas     LTU    Men            Discus Throw    Gold  
      20111     BRAZDAUSKIS, Romanas     LTU    Men              Basketball  Bronze  
      20112    CHOMICIUS, Valdemaras     LTU    Men              Basketball  Bronze  
      20113       DIMAVICIUS, Darius     LTU    Men              Basketball  Bronze  
      20114        EINIKIS, Gintaras     LTU    Men              Basketball  Bronze  
      20115        JOVAISA, Sergejus     LTU    Men              Basketball  Bronze  
      20116      KARNISOVAS, Arturas     LTU    Men              Basketball  Bronze  
      20117       KRAPIKAS, Gintaras     LTU    Men              Basketball  Bronze  
      20118       KURTINAITIS, Rimas     LTU    Men              Basketball  Bronze  
      20119    MARCIULIONIS, Sarunas     LTU    Men              Basketball  Bronze  
      20120      PAZDRAZDIS, Alvydas     LTU    Men              Basketball  Bronze  
      20121         SABONIS, Arvydas     LTU    Men              Basketball  Bronze  
      20122         VISOCKAS, Arunas     LTU    Men              Basketball  Bronze  
      21852        EINIKIS, Gintaras     LTU    Men              Basketball  Bronze  
      21853        JURKUNAS, Andrius     LTU    Men              Basketball  Bronze  
      21854      KARNISOVAS, Arturas     LTU    Men              Basketball  Bronze  
      21855       KURTINAITIS, Rimas     LTU    Men              Basketball  Bronze  
      21856         LUKMINAS, Darius     LTU    Men              Basketball  Bronze  
      21857    MARCIULIONIS, Sarunas     LTU    Men              Basketball  Bronze  
      21858           PACESAS, Tomas     LTU    Men              Basketball  Bronze  
      21859         SABONIS, Arvydas     LTU    Men              Basketball  Bronze  
      21860      STOMBERGAS, Saulius     LTU    Men              Basketball  Bronze  
      21861          VAISVILA, Rytis     LTU    Men              Basketball  Bronze  
      21862     ZUKAUSKAS, Eurelijus     LTU    Men              Basketball  Bronze  
      21863     ZUKAUSKAS, Mindaugas     LTU    Men              Basketball  Bronze  
      23641       ALEKNA, Virgilijus     LTU    Men            Discus Throw    Gold  
      23794       ADOMAITIS, Dainius     LTU    Men              Basketball  Bronze  
      23795        EINIKIS, Gintaras     LTU    Men              Basketball  Bronze  
      23796      GIEDRAITIS, Audrius     LTU    Men              Basketball  Bronze  
      23797    JASIKEVICIUS, Sarunas     LTU    Men              Basketball  Bronze  
      23798   MARCIULIONIS, Kestutis     LTU    Men              Basketball  Bronze  
      23799          MASIULIS, Tomas     LTU    Men              Basketball  Bronze  
      23800      MASKOLIUNAS, Darius     LTU    Men              Basketball  Bronze  
      23801      SISKAUSKAS, Ramunas     LTU    Men              Basketball  Bronze  
      23802         SONGAILA, Darius     LTU    Men              Basketball  Bronze  
      23803      STOMBERGAS, Saulius     LTU    Men              Basketball  Bronze  
      23804     TIMINSKAS, Mindaugas     LTU    Men              Basketball  Bronze  
      23805     ZUKAUSKAS, Eurelijus     LTU    Men              Basketball  Bronze  
      25659       ALEKNA, Virgilijus     LTU    Men            Discus Throw    Gold  
      26630  ZADNEPROVSKIS, Andrejus     LTU    Men  Individual Competition  Silver  
      27665       ALEKNA, Virgilijus     LTU    Men            Discus Throw  Bronze  
      28642  ZADNEPROVSKIS, Andrejus     LTU    Men  Individual Competition  Bronze  
      28644      KRUNGOLCAS, Edvinas     LTU    Men  Individual Competition  Silver  
      29212     MIZGAITIS, Mindaugas     LTU    Men              96 - 120KG  Bronze  
      29890      PETRAUSKAS, Evaldas     LTU    Men               57 - 60KG  Bronze  
      29939        SHUKLIN, Jevgenij     LTU    Men                C-1 200M  Silver  
      31156     KAZAKEVIC, Aleksandr     LTU    Men                Wg 74 KG  Bronze  ),
     (('LTU', 'Women'),
             Year     City              Sport         Discipline  \
      24001  2000   Sydney            Cycling       Cycling Road   
      24651  2000   Sydney             Rowing             Rowing   
      24652  2000   Sydney             Rowing             Rowing   
      24886  2000   Sydney           Shooting           Shooting   
      25672  2004   Athens          Athletics          Athletics   
      28818  2008  Beijing            Sailing            Sailing   
      29267  2012   London           Aquatics           Swimming   
      30638  2012   London  Modern Pentathlon  Modern Pentathlon   
      
                             Athlete Country Gender  \
      24001           ZILIUTE, Diana     LTU  Women   
      24651    POPLAVSKAJA, Kristina     LTU  Women   
      24652       SAKICKIENE, Birute     LTU  Women   
      24886    GUDZINEVICIUTE, Daina     LTU  Women   
      25672          SKUJYTE, Austra     LTU  Women   
      28818  VOLUNGEVICIUTE, Gintare     LTU  Women   
      29267          MEILUTYTE, Ruta     LTU  Women   
      30638      ASADAUSKAITE, Laura     LTU  Women   
      
                                        Event   Medal  
      24001              Individual Road Race  Bronze  
      24651                Double Sculls (2X)  Bronze  
      24652                Double Sculls (2X)  Bronze  
      24886                 Trap (75 Targets)    Gold  
      25672                        Heptathlon  Silver  
      28818  Laser Radial - One Person Dinghy  Silver  
      29267                 100M Breaststroke    Gold  
      30638                        Individual    Gold  ),
     (('LUX', 'Men'),
            Year      City          Sport     Discipline          Athlete Country  \
      4079  1920   Antwerp  Weightlifting  Weightlifting    ALZIN, Joseph     LUX   
      8130  1952  Helsinki      Athletics      Athletics  BARTHEL, Joseph     LUX   
      
           Gender                                          Event   Medal  
      4079    Men  + 82.5KG, One-Two Hand 3 Events (Heavyweight)  Silver  
      8130    Men                                          1500M    Gold  ),
     (('MAR', 'Men'),
             Year         City      Sport Discipline  \
      10036  1960         Rome  Athletics  Athletics   
      16888  1984  Los Angeles  Athletics  Athletics   
      18278  1988        Seoul  Athletics  Athletics   
      18382  1988        Seoul  Athletics  Athletics   
      18528  1988        Seoul     Boxing     Boxing   
      19850  1992    Barcelona  Athletics  Athletics   
      19872  1992    Barcelona  Athletics  Athletics   
      20195  1992    Barcelona     Boxing     Boxing   
      21588  1996      Atlanta  Athletics  Athletics   
      21699  1996      Atlanta  Athletics  Athletics   
      23534  2000       Sydney  Athletics  Athletics   
      23550  2000       Sydney  Athletics  Athletics   
      23622  2000       Sydney  Athletics  Athletics   
      23883  2000       Sydney     Boxing     Boxing   
      25551  2004       Athens  Athletics  Athletics   
      25641  2004       Athens  Athletics  Athletics   
      27700  2008      Beijing  Athletics  Athletics   
      29602  2012       London  Athletics  Athletics   
      
                                    Athlete Country Gender  \
      10036  RHADI BEN ABDESSELEM, Abdesiem     MAR    Men   
      16888                    AOUITA, Said     MAR    Men   
      18278         BOUTAYEB, Moulay Brahim     MAR    Men   
      18382                    AOUITA, Said     MAR    Men   
      18528                 ACHIK, Abdelhak     MAR    Men   
      19850                    SKAH, Khalid     MAR    Men   
      19872                EL BASIR, Rachid     MAR    Men   
      20195                  ACHIK, Mohamed     MAR    Men   
      21588                   HISSOU, Salah     MAR    Men   
      21699                 BOULAMI, Khalid     MAR    Men   
      23534             EL GUERROUJ, Hicham     MAR    Men   
      23550                     EZZINE, Ali     MAR    Men   
      23622                 LAHLAFI, Brahim     MAR    Men   
      23883                TAMSAMANI, Tahar     MAR    Men   
      25551             EL GUERROUJ, Hicham     MAR    Men   
      25641             EL GUERROUJ, Hicham     MAR    Men   
      27700                  GHARIB, Jaouad     MAR    Men   
      29602              IGUIDER, Abdalaati     MAR    Men   
      
                                 Event   Medal  
      10036                   Marathon  Silver  
      16888                      5000M    Gold  
      18278                     10000M    Gold  
      18382                       800M  Bronze  
      18528  54 - 57KG (Featherweight)  Bronze  
      19850                     10000M    Gold  
      19872                      1500M  Silver  
      20195   51 - 54KG (Bantamweight)  Bronze  
      21588                     10000M  Bronze  
      21699                      5000M  Bronze  
      23534                      1500M  Silver  
      23550         3000M Steeplechase  Bronze  
      23622                      5000M  Bronze  
      23883  54 - 57KG (Featherweight)  Bronze  
      25551                      1500M    Gold  
      25641                      5000M    Gold  
      27700                   Marathon  Silver  
      29602                      1500M  Bronze  ),
     (('MAR', 'Women'),
             Year         City      Sport Discipline               Athlete Country  \
      16837  1984  Los Angeles  Athletics  Athletics  EL MOUTAWAKEL, Nawal     MAR   
      23562  2000       Sydney  Athletics  Athletics      BIDOUANE, Nouzha     MAR   
      25654  2004       Athens  Athletics  Athletics       BENHASSI, Hasna     MAR   
      27659  2008      Beijing  Athletics  Athletics       BENHASSI, Hasna     MAR   
      
            Gender         Event   Medal  
      16837  Women  400M Hurdles    Gold  
      23562  Women  400M Hurdles  Bronze  
      25654  Women          800M  Silver  
      27659  Women          800M  Bronze  ),
     (('MAS', 'Men'),
             Year       City      Sport Discipline          Athlete Country Gender  \
      20028  1992  Barcelona  Badminton  Badminton    SIDEK, Rashid     MAS    Men   
      20029  1992  Barcelona  Badminton  Badminton     SIDEK, Razif     MAS    Men   
      21774  1996    Atlanta  Badminton  Badminton  CHEAH, Soon Kit     MAS    Men   
      21775  1996    Atlanta  Badminton  Badminton    YAP, Kim Hock     MAS    Men   
      21786  1996    Atlanta  Badminton  Badminton    SIDEK, Rashid     MAS    Men   
      27742  2008    Beijing  Badminton  Badminton   LEE, Chong Wei     MAS    Men   
      29791  2012     London  Badminton  Badminton   LEE, Chong Wei     MAS    Men   
      
               Event   Medal  
      20028  Doubles  Bronze  
      20029  Doubles  Bronze  
      21774  Doubles  Silver  
      21775  Doubles  Silver  
      21786  Singles  Bronze  
      27742  Singles  Silver  
      29791  Singles  Silver  ),
     (('MAS', 'Women'),
             Year    City     Sport Discipline                 Athlete Country  \
      29221  2012  London  Aquatics     Diving  PAMG, Pandelela Rinong     MAS   
      
            Gender         Event   Medal  
      29221  Women  10M Platform  Bronze  ),
     (('MDA', 'Men'),
             Year     City          Sport       Discipline             Athlete  \
      21988  1996  Atlanta  Canoe / Kayak  Canoe / Kayak F  JURAVSCHI, Nikolai   
      21989  1996  Atlanta  Canoe / Kayak  Canoe / Kayak F   RENEYSKIY, Viktor   
      23134  1996  Atlanta      Wrestling  Wrestling Gre-R   MOUREIKO, Serguei   
      23894  2000   Sydney         Boxing           Boxing     GRUSAC, Vitalie   
      24851  2000   Sydney       Shooting         Shooting      MOLDOVAN, Oleg   
      27902  2008  Beijing         Boxing           Boxing    GOJAN, Veaceslav   
      
            Country Gender                             Event   Medal  
      21988     MDA    Men           C-2 500M (Canoe Double)  Silver  
      21989     MDA    Men           C-2 500M (Canoe Double)  Silver  
      23134     MDA    Men   100 - 130KG (Super Heavyweight)  Bronze  
      23894     MDA    Men        63.5 - 67KG (Welterweight)  Bronze  
      24851     MDA    Men  10M Running Target (30+30 Shots)  Silver  
      27902     MDA    Men          51 - 54KG (Bantamweight)  Bronze  ),
     (('MEX', 'Men'),
             Year         City       Sport  Discipline                      Athlete  \
      5918   1932  Los Angeles      Boxing      Boxing           CABANAS, Francisco   
      6271   1932  Los Angeles    Shooting    Shooting      HUET BOBADILLA, Gustavo   
      6537   1936       Berlin  Basketball  Basketball          BORJA MORCA, Carlos   
      6538   1936       Berlin  Basketball  Basketball     BORJA MORCA, Victor Hugo   
      6539   1936       Berlin  Basketball  Basketball  CHOPERENA IRIZARRI, Rodolfo   
      ...     ...          ...         ...         ...                          ...   
      30205  2012       London    Football    Football                PONCE, Miguel   
      30206  2012       London    Football    Football                 REYES, Diego   
      30207  2012       London    Football    Football              RODRIGUEZ, Jose   
      30208  2012       London    Football    Football              SALCIDO, Carlos   
      30209  2012       London    Football    Football               VIDRIO, Nestor   
      
            Country Gender                       Event   Medal  
      5918      MEX    Men        - 50.8KG (Flyweight)  Silver  
      6271      MEX    Men  50M Rifle Prone (60 Shots)  Silver  
      6537      MEX    Men                  Basketball  Bronze  
      6538      MEX    Men                  Basketball  Bronze  
      6539      MEX    Men                  Basketball  Bronze  
      ...       ...    ...                         ...     ...  
      30205     MEX    Men                    Football    Gold  
      30206     MEX    Men                    Football    Gold  
      30207     MEX    Men                    Football    Gold  
      30208     MEX    Men                    Football    Gold  
      30209     MEX    Men                    Football    Gold  
      
      [89 rows x 9 columns]),
     (('MEX', 'Women'),
             Year     City          Sport     Discipline  \
      11825  1968   Mexico       Aquatics       Swimming   
      12216  1968   Mexico        Fencing        Fencing   
      15767  1980   Moscow     Equestrian       Eventing   
      15790  1980   Moscow     Equestrian        Jumping   
      25102  2000   Sydney  Weightlifting  Weightlifting   
      25576  2004   Athens      Athletics      Athletics   
      26046  2004   Athens        Cycling  Cycling Track   
      26958  2004   Athens      Taekwondo      Taekwondo   
      27192  2008  Beijing       Aquatics         Diving   
      27193  2008  Beijing       Aquatics         Diving   
      28970  2008  Beijing      Taekwondo      Taekwondo   
      29227  2012   London       Aquatics         Diving   
      29236  2012   London       Aquatics         Diving   
      29237  2012   London       Aquatics         Diving   
      29562  2012   London        Archery        Archery   
      29563  2012   London        Archery        Archery   
      30913  2012   London      Taekwondo      Taekwondo   
      
                                   Athlete Country Gender  \
      11825          RAMIREZ, Maria Teresa     MEX  Women   
      12216  DEL PILAR ROLDAN TAPIA, Maria     MEX  Women   
      15767                        BOMBONA     MEX  Women   
      15790                     LADY MIRKA     MEX  Women   
      25102       JIMENEZ MENDIVIL, Soraya     MEX  Women   
      25576                   GUEVARA, Ana     MEX  Women   
      26046         GUERRERO MENDEZ, Belem     MEX  Women   
      26958         SALAZAR BLANCO, Iridia     MEX  Women   
      27192                ESPINOSA, Paola     MEX  Women   
      27193                 ORTIZ, Tatiana     MEX  Women   
      28970    ESPINOZA, Maria del Rosario     MEX  Women   
      29227            SANCHEZ SOTO, Laura     MEX  Women   
      29236                ESPINOSA, Paola     MEX  Women   
      29237         OROZCO LOZA, Alejandra     MEX  Women   
      29562                    ROMAN, Aida     MEX  Women   
      29563                AVITIA, Mariana     MEX  Women   
      30913    ESPINOZA, Maria del Rosario     MEX  Women   
      
                                        Event   Medal  
      11825                    800M Freestyle  Bronze  
      12216                   Foil Individual  Silver  
      15767                              Team  Bronze  
      15790                              Team  Bronze  
      25102                              58KG    Gold  
      25576                              400M  Silver  
      26046                       Points Race  Silver  
      26958                        49 - 57 KG  Bronze  
      27192  Synchronized Diving 10M Platform  Bronze  
      27193  Synchronized Diving 10M Platform  Bronze  
      28970                           + 67 KG    Gold  
      29227                    3M Springboard  Bronze  
      29236                  Synchronized 10M  Silver  
      29237                  Synchronized 10M  Silver  
      29562                        Individual  Silver  
      29563                        Individual  Bronze  
      30913                           + 67 KG  Bronze  ),
     (('MGL', 'Men'),
             Year       City      Sport       Discipline  \
      12667  1968     Mexico  Wrestling  Wrestling Free.   
      12679  1968     Mexico  Wrestling  Wrestling Free.   
      12682  1968     Mexico  Wrestling  Wrestling Free.   
      12687  1968     Mexico  Wrestling  Wrestling Free.   
      13869  1972     Munich  Wrestling  Wrestling Free.   
      15159  1976   Montreal  Wrestling  Wrestling Free.   
      16178  1980     Moscow       Judo             Judo   
      16179  1980     Moscow       Judo             Judo   
      16541  1980     Moscow  Wrestling  Wrestling Free.   
      16552  1980     Moscow  Wrestling  Wrestling Free.   
      18533  1988      Seoul     Boxing           Boxing   
      20203  1992  Barcelona     Boxing           Boxing   
      22614  1996    Atlanta       Judo             Judo   
      26577  2004     Athens       Judo             Judo   
      27901  2008    Beijing     Boxing           Boxing   
      27904  2008    Beijing     Boxing           Boxing   
      28640  2008    Beijing       Judo             Judo   
      29881  2012     London     Boxing           Boxing   
      29895  2012     London     Boxing           Boxing   
      30618  2012     London       Judo             Judo   
      30632  2012     London       Judo             Judo   
      
                                Athlete Country Gender  \
      12667        SURENJAV, Sukhbaatar     MGL    Men   
      12679      DANZANDARJAA, Sereeter     MGL    Men   
      12682           PUREV, Dagvasuren     MGL    Men   
      12687           JIGJIDYM, Munkbat     MGL    Men   
      13869          BAYANMUNK, Khorloo     MGL    Men   
      15159            OIDOV, Zevegying     MGL    Men   
      16178           DAMDIN, Tsendying     MGL    Men   
      16179          DAVAADALAI, Ravdan     MGL    Men   
      16541        OUINBOLD, Dugarsuren     MGL    Men   
      16552         DAVAAJAV, Jamtsying     MGL    Men   
      18533             ENKHBAT, Nerguy     MGL    Men   
      20203        BAYARSAIKHAN, Namjil     MGL    Men   
      22614       NARMANDAKH, Dorjpalam     MGL    Men   
      26577  TSAGAANBAATAR, Khashbaatar     MGL    Men   
      27901         PUREVDORJ, Serdamba     MGL    Men   
      27904        ENKHBAT, Badar-Uugan     MGL    Men   
      28640        NAIDAN, Tuvshinbayar     MGL    Men   
      29881        NYAMBAYAR, Tugstsogt     MGL    Men   
      29895    URANCHIMEG, Munkh-Erdene     MGL    Men   
      30618      SAINJARGAL, Nyam-Ochir     MGL    Men   
      30632        NAIDAN, Tuvshinbayar     MGL    Men   
      
                                     Event   Medal  
      12667             - 52KG (Flyweight)  Bronze  
      12679        63 - 70KG (Lightweight)  Bronze  
      12682       70 - 78KG (Welterweight)  Bronze  
      12687       78 - 87KG (Middleweight)  Silver  
      13869       90 - 100KG (Heavyweight)  Silver  
      15159      57 - 62KG (Featherweight)  Silver  
      16178   60 - 65KG (Half-Lightweight)  Silver  
      16179        65 - 71KG (Lightweight)  Bronze  
      16541       52 - 57KG (Bantamweight)  Bronze  
      16552       68 - 74KG (Welterweight)  Silver  
      18533        57 - 60KG (Lightweight)  Bronze  
      20203        57 - 60KG (Lightweight)  Bronze  
      22614                        - 60 KG  Bronze  
      26577                        - 60 KG  Bronze  
      27901         48KG (Light Flywieght)  Silver  
      27904       51 - 54KG (Bantamweight)    Gold  
      28640  90 - 100KG (Half-Heavyweight)    Gold  
      29881                           52KG  Silver  
      29895                     60 - 64 KG  Bronze  
      30618                      66 - 73KG  Bronze  
      30632                     90 - 100KG  Silver  ),
     (('MGL', 'Women'),
             Year       City      Sport           Discipline  \
      21066  1992  Barcelona   Shooting             Shooting   
      28860  2008    Beijing   Shooting             Shooting   
      31115  2012     London  Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                     Event  \
      21066    MUNKHBAYAR, Dorzhsuren     MGL  Women  25M Pistol (30+30 Shots)   
      28860         OTRYAD, Gundegmaa     MGL  Women  25M Pistol (30+30 Shots)   
      31115  SORONZONBOLD, Battsetseg     MGL  Women                  Wf 63 KG   
      
              Medal  
      21066  Bronze  
      28860  Silver  
      31115  Bronze  ),
     (('MKD', 'Men'),
             Year    City      Sport       Discipline             Athlete Country  \
      25143  2000  Sydney  Wrestling  Wrestling Free.  IBRAGIMOV, Mogamed     MKD   
      
            Gender      Event   Medal  
      25143    Men  76 - 85KG  Bronze  ),
     (('MNE', 'Women'),
             Year    City     Sport Discipline               Athlete Country Gender  \
      30454  2012  London  Handball   Handball  BARJAKTAROVIC, Sonja     MNE  Women   
      30455  2012  London  Handball   Handball     BULATOVIC, Andela     MNE  Women   
      30456  2012  London  Handball   Handball   BULATOVIC, Katarina     MNE  Women   
      30457  2012  London  Handball   Handball            DOKIC, Ana     MNE  Women   
      30458  2012  London  Handball   Handball     JOVANOVIC, Marija     MNE  Women   
      30459  2012  London  Handball   Handball      KNEZEVIC, Milena     MNE  Women   
      30460  2012  London  Handball   Handball       LAZOVIC, Suzana     MNE  Women   
      30461  2012  London  Handball   Handball     MEHMEDOVIC, Majda     MNE  Women   
      30462  2012  London  Handball   Handball     MILJANIC, Radmila     MNE  Women   
      30463  2012  London  Handball   Handball       POPOVIC, Bojana     MNE  Women   
      30464  2012  London  Handball   Handball    RADICEVIC, Jovanka     MNE  Women   
      30465  2012  London  Handball   Handball          RADOVIC, Ana     MNE  Women   
      30466  2012  London  Handball   Handball           SAVIC, Maja     MNE  Women   
      30467  2012  London  Handball   Handball      VUKCEVIC, Marina     MNE  Women   
      
                Event   Medal  
      30454  Handball  Silver  
      30455  Handball  Silver  
      30456  Handball  Silver  
      30457  Handball  Silver  
      30458  Handball  Silver  
      30459  Handball  Silver  
      30460  Handball  Silver  
      30461  Handball  Silver  
      30462  Handball  Silver  
      30463  Handball  Silver  
      30464  Handball  Silver  
      30465  Handball  Silver  
      30466  Handball  Silver  
      30467  Handball  Silver  ),
     (('MOZ', 'Women'),
             Year     City      Sport Discipline        Athlete Country Gender  \
      21711  1996  Atlanta  Athletics  Athletics  MUTOLA, Maria     MOZ  Women   
      23635  2000   Sydney  Athletics  Athletics  MUTOLA, Maria     MOZ  Women   
      
            Event   Medal  
      21711  800M  Bronze  
      23635  800M    Gold  ),
     (('MRI', 'Men'),
             Year     City   Sport Discipline       Athlete Country Gender  \
      27903  2008  Beijing  Boxing     Boxing  JULIE, Bruno     MRI    Men   
      
                                Event   Medal  
      27903  51 - 54KG (Bantamweight)  Bronze  ),
     (('NAM', 'Men'),
             Year       City      Sport Discipline            Athlete Country  \
      19860  1992  Barcelona  Athletics  Athletics  FREDERICKS, Frank     NAM   
      19878  1992  Barcelona  Athletics  Athletics  FREDERICKS, Frank     NAM   
      21599  1996    Atlanta  Athletics  Athletics  FREDERICKS, Frank     NAM   
      21617  1996    Atlanta  Athletics  Athletics  FREDERICKS, Frank     NAM   
      
            Gender Event   Medal  
      19860    Men  100M  Silver  
      19878    Men  200M  Silver  
      21599    Men  100M  Silver  
      21617    Men  200M  Silver  ),
     (('NED', 'Men'),
             Year    City     Sport Discipline                       Athlete  \
      154    1900   Paris  Aquatics   Swimming               DROST, Johannes   
      434    1900   Paris    Rowing     Rowing      BRANDT, Francois Antoine   
      435    1900   Paris    Rowing     Rowing  BROCKMANN, Hermanus Gerardus   
      436    1900   Paris    Rowing     Rowing                 KLEIN, Roelof   
      437    1900   Paris    Rowing     Rowing        LEEGSTRA, Ruud Gerbens   
      ...     ...     ...       ...        ...                           ...   
      30512  2012  London    Hockey     Hockey               VERGA, Valentin   
      30513  2012  London    Hockey     Hockey              VERMEULEN, Klaas   
      30514  2012  London    Hockey     Hockey            WEUSTHOF, Roderick   
      30633  2012  London      Judo       Judo                    GROL, Henk   
      30821  2012  London   Sailing    Sailing      VAN RIJSSELBERGE, Dorian   
      
            Country Gender                     Event   Medal  
      154       NED    Men           200M Backstroke  Bronze  
      434       NED    Men  Eight With Coxswain (8+)  Bronze  
      435       NED    Men  Eight With Coxswain (8+)  Bronze  
      436       NED    Men  Eight With Coxswain (8+)  Bronze  
      437       NED    Men  Eight With Coxswain (8+)  Bronze  
      ...       ...    ...                       ...     ...  
      30512     NED    Men                    Hockey  Silver  
      30513     NED    Men                    Hockey  Silver  
      30514     NED    Men                    Hockey  Silver  
      30633     NED    Men                90 - 100KG  Bronze  
      30821     NED    Men                      Rs:X    Gold  
      
      [495 rows x 9 columns]),
     (('NED', 'Women'),
             Year       City      Sport Discipline                Athlete Country  \
      4941   1924      Paris     Tennis     Tennis       BOUMAN, Cornelia     NED   
      5020   1928  Amsterdam   Aquatics   Swimming   BRAUN, Maria Johanna     NED   
      5036   1928  Amsterdam   Aquatics   Swimming          BARON, Mietje     NED   
      5042   1928  Amsterdam   Aquatics   Swimming   BRAUN, Maria Johanna     NED   
      5180   1928  Amsterdam  Athletics  Athletics  GISOLF, Carolina Anna     NED   
      ...     ...        ...        ...        ...                    ...     ...   
      30729  2012     London     Rowing     Rowing      SCHELLEKENS, Anne     NED   
      30730  2012     London     Rowing     Rowing    VEENHOVEN, Jacobine     NED   
      30795  2012     London    Sailing    Sailing        BERKHOUT, Lobke     NED   
      30796  2012     London    Sailing    Sailing        WESTERHOF, Lisa     NED   
      30819  2012     London    Sailing    Sailing     BOUWMEESTER, Marit     NED   
      
            Gender                Event   Medal  
      4941   Women        Mixed Doubles  Bronze  
      5020   Women      100M Backstroke    Gold  
      5036   Women    200M Breaststroke  Silver  
      5042   Women       400M Freestyle  Silver  
      5180   Women            High Jump  Silver  
      ...      ...                  ...     ...  
      30729  Women  Eight With Coxswain  Bronze  
      30730  Women  Eight With Coxswain  Bronze  
      30795  Women                  470  Bronze  
      30796  Women                  470  Bronze  
      30819  Women         Laser Radial  Silver  
      
      [356 rows x 9 columns]),
     (('NGR', 'Men'),
             Year         City      Sport Discipline                      Athlete  \
      11019  1964        Tokyo     Boxing     Boxing              MAIYEGUN, Nojim   
      13125  1972       Munich     Boxing     Boxing              IKHOURIA, Isaac   
      16863  1984  Los Angeles  Athletics  Athletics           EGBUNIKE, Innocent   
      16864  1984  Los Angeles  Athletics  Athletics               PETERS, Rotimi   
      16865  1984  Los Angeles  Athletics  Athletics              UGBUSIEN, Moses   
      ...     ...          ...        ...        ...                          ...   
      28246  2008      Beijing   Football   Football            OKONKWO, Chibuzor   
      28247  2008      Beijing   Football   Football           OKORONKWO, Solomon   
      28248  2008      Beijing   Football   Football             OLUFEMI, Oladapo   
      28249  2008      Beijing   Football   Football            VANZEKIN, Ambruse   
      28973  2008      Beijing  Taekwondo  Taekwondo  CHUKWUMERIJE, Chika Yagazie   
      
            Country Gender                           Event   Medal  
      11019     NGR    Men  67 - 71KG (Light-Middleweight)  Bronze  
      13125     NGR    Men   75 - 81KG (Light-Heavyweight)  Bronze  
      16863     NGR    Men                    4X400M Relay  Bronze  
      16864     NGR    Men                    4X400M Relay  Bronze  
      16865     NGR    Men                    4X400M Relay  Bronze  
      ...       ...    ...                             ...     ...  
      28246     NGR    Men                        Football  Silver  
      28247     NGR    Men                        Football  Silver  
      28248     NGR    Men                        Football  Silver  
      28249     NGR    Men                        Football  Silver  
      28973     NGR    Men                         + 80 KG  Bronze  
      
      [66 rows x 9 columns]),
     (('NGR', 'Women'),
             Year       City          Sport     Discipline  \
      19917  1992  Barcelona      Athletics      Athletics   
      19918  1992  Barcelona      Athletics      Athletics   
      19919  1992  Barcelona      Athletics      Athletics   
      19920  1992  Barcelona      Athletics      Athletics   
      21618  1996    Atlanta      Athletics      Athletics   
      21630  1996    Atlanta      Athletics      Athletics   
      21695  1996    Atlanta      Athletics      Athletics   
      21696  1996    Atlanta      Athletics      Athletics   
      21697  1996    Atlanta      Athletics      Athletics   
      21698  1996    Atlanta      Athletics      Athletics   
      21745  1996    Atlanta      Athletics      Athletics   
      23528  2000     Sydney      Athletics      Athletics   
      25118  2000     Sydney  Weightlifting  Weightlifting   
      27611  2008    Beijing      Athletics      Athletics   
      27612  2008    Beijing      Athletics      Athletics   
      27613  2008    Beijing      Athletics      Athletics   
      27614  2008    Beijing      Athletics      Athletics   
      27695  2008    Beijing      Athletics      Athletics   
      
                                      Athlete Country Gender         Event   Medal  
      19917                     IDEHEN, Faith     NGR  Women  4X100M Relay  Bronze  
      19918                      ONYALI, Mary     NGR  Women  4X100M Relay  Bronze  
      19919  OPARA-THOMPSON, Christy Thompson     NGR  Women  4X100M Relay  Bronze  
      19920                  UTONDU, Beatrice     NGR  Women  4X100M Relay  Bronze  
      21618                      ONYALI, Mary     NGR  Women          200M  Bronze  
      21630                 OGUNKOYA, Falilat     NGR  Women          400M  Bronze  
      21695                     AFOLABI, Bisi     NGR  Women  4X400M Relay  Silver  
      21696                 OGUNKOYA, Falilat     NGR  Women  4X400M Relay  Silver  
      21697                    OPARA, Charity     NGR  Women  4X400M Relay  Silver  
      21698                     YUSUF, Fatima     NGR  Women  4X400M Relay  Silver  
      21745                    AJUNWA, Chioma     NGR  Women     Long Jump    Gold  
      23528                    ALOZIE, Gloria     NGR  Women  100M Hurdles  Silver  
      25118                     OGBEIFO, Ruth     NGR  Women          75KG  Silver  
      27611                     IDOKO, Franca     NGR  Women  4X100M Relay  Bronze  
      27612                  ISMAILA, Halimat     NGR  Women  4X100M Relay  Bronze  
      27613                 KEMASUODE, Gloria     NGR  Women  4X100M Relay  Bronze  
      27614                OSAYOMI, Oludamola     NGR  Women  4X100M Relay  Bronze  
      27695                OKAGBARE, Blessing     NGR  Women     Long Jump  Bronze  ),
     (('NIG', 'Men'),
             Year    City   Sport Discipline         Athlete Country Gender  \
      13108  1972  Munich  Boxing     Boxing  DABORG, Issaka     NIG    Men   
      
                                        Event   Medal  
      13108  60 - 63.5KG (Light-Welterweight)  Bronze  ),
     (('NOR', 'Men'),
             Year     City      Sport    Discipline                Athlete Country  \
      294    1900    Paris  Athletics     Athletics  ANDERSEN, Carl Albert     NOR   
      596    1900    Paris   Shooting      Shooting             ÖSTMO, Ole     NOR   
      603    1900    Paris   Shooting      Shooting             ÖSTMO, Ole     NOR   
      608    1900    Paris   Shooting      Shooting             ÖSTMO, Ole     NOR   
      619    1900    Paris   Shooting      Shooting  FRYDENLUND, Olaf Emil     NOR   
      ...     ...      ...        ...           ...                    ...     ...   
      28787  2008  Beijing     Rowing        Rowing            TUFTE, Olaf     NOR   
      28881  2008  Beijing   Shooting      Shooting          BROVOLD, Tore     NOR   
      29947  2012   London      Canoe  Canoe Sprint   LARSEN, Eirik Veraas     NOR   
      30009  2012   London    Cycling  Cycling Road    KRISTOFF, Alexander     NOR   
      30127  2012   London    Fencing       Fencing      PIASECKI, Bartosz     NOR   
      
            Gender                          Event   Medal  
      294      Men                     Pole Vault  Bronze  
      596      Men  Army Rifle, 300M, 3 Positions  Bronze  
      603      Men        Army Rifle, 300M, Prone  Bronze  
      608      Men     Army Rifle, 300M, Standing  Silver  
      619      Men               Free Rifle, Team  Silver  
      ...      ...                            ...     ...  
      28787    Men             Single Sculls (1X)    Gold  
      28881    Men            Skeet (125 Targets)  Silver  
      29947    Men                      K-1 1000M    Gold  
      30009    Men                Individual Road  Bronze  
      30127    Men                Épée Individual  Silver  
      
      [432 rows x 9 columns]),
     (('NOR', 'Women'),
             Year         City      Sport      Discipline  \
      2782   1912    Stockholm     Tennis          Tennis   
      4025   1920      Antwerp    Skating  Figure skating   
      8782   1952     Helsinki    Sailing         Sailing   
      16937  1984  Los Angeles  Athletics       Athletics   
      18999  1988        Seoul   Handball        Handball   
      ...     ...          ...        ...             ...   
      30449  2012       London   Handball        Handball   
      30450  2012       London   Handball        Handball   
      30451  2012       London   Handball        Handball   
      30452  2012       London   Handball        Handball   
      30453  2012       London   Handball        Handball   
      
                               Athlete Country Gender     Event   Medal  
      2782   BJURSTEDT, Anne Margrethe     NOR  Women   Singles  Bronze  
      4025                BRYN, Alexia     NOR  Women     Pairs  Silver  
      8782               LUNDE, Vibeke     NOR  Women      5.5M  Silver  
      16937      WAITZ-ANDERSEN, Grete     NOR  Women  Marathon  Silver  
      18999         ANDERSEN, Kjerstin     NOR  Women  Handball  Silver  
      ...                          ...     ...    ...       ...     ...  
      30449  LUNDE-BORGERSEN, Kristine     NOR  Women  Handball    Gold  
      30450            NOSTVOLD, Tonje     NOR  Women  Handball    Gold  
      30451   RIEGELHUTH, Linn-Kristin     NOR  Women  Handball    Gold  
      30452        SNORROEGGEN, Goeril     NOR  Women  Handball    Gold  
      30453        SULLAND, Linn Jorum     NOR  Women  Handball    Gold  
      
      [122 rows x 9 columns]),
     (('NZL', 'Men'),
             Year         City      Sport Discipline                       Athlete  \
      3678   1920      Antwerp     Rowing     Rowing  HADFIELD D'ARCY, D. Clarence   
      4235   1924        Paris  Athletics  Athletics               PORRITT, Arthur   
      5215   1928    Amsterdam     Boxing     Boxing                MORGAN, Edward   
      6151   1932  Los Angeles     Rowing     Rowing            STILES, Cyril Alec   
      6152   1932  Los Angeles     Rowing     Rowing       THOMPSON, Fred Houghton   
      ...     ...          ...        ...        ...                           ...   
      30747  2012       London     Rowing     Rowing                 TAYLOR, Peter   
      30748  2012       London     Rowing     Rowing                    URU, Storm   
      30779  2012       London     Rowing     Rowing                DRYSDALE, Mahe   
      30799  2012       London    Sailing    Sailing                BURLING, Peter   
      30800  2012       London    Sailing    Sailing                   TUKE, Blair   
      
            Country Gender                           Event   Medal  
      3678      NZL    Men              Single Sculls (1X)  Bronze  
      4235      NZL    Men                            100M  Bronze  
      5215      NZL    Men  61.24 - 66.68KG (Welterweight)    Gold  
      6151      NZL    Men               Coxless Pair (2-)  Silver  
      6152      NZL    Men               Coxless Pair (2-)  Silver  
      ...       ...    ...                             ...     ...  
      30747     NZL    Men             Lightweight Doubles  Bronze  
      30748     NZL    Men             Lightweight Doubles  Bronze  
      30779     NZL    Men                   Single Sculls    Gold  
      30799     NZL    Men                    49Er - Skiff  Silver  
      30800     NZL    Men                    49Er - Skiff  Silver  
      
      [159 rows x 9 columns]),
     (('NZL', 'Women'),
             Year       City       Sport     Discipline                    Athlete  \
      8033   1952   Helsinki    Aquatics       Swimming              STEWART, Jean   
      8223   1952   Helsinki   Athletics      Athletics  WILLIAMS, Yvette Winefred   
      10900  1964      Tokyo   Athletics      Athletics    CHAMBERLAIN, Ann Marise   
      18700  1988      Seoul  Equestrian       Eventing         KNIGHTON, Margaret   
      18701  1988      Seoul  Equestrian       Eventing           POTTINGER, Tinks   
      19264  1988      Seoul      Rowing         Rowing             HANNEN, Lynley   
      19265  1988      Seoul      Rowing         Rowing              PAYNE, Nicola   
      20012  1992  Barcelona   Athletics      Athletics      MOLLER, Lorraine Mary   
      20394  1992  Barcelona  Equestrian       Eventing       LATTA, Victoria Jean   
      21013  1992  Barcelona     Sailing        Sailing         EGNOT, Leslie Jean   
      21014  1992  Barcelona     Sailing        Sailing         SHEARER, Janet Lee   
      21019  1992  Barcelona     Sailing        Sailing           KENDALL, Barbara   
      22125  1996    Atlanta  Equestrian       Eventing               CLARK, Sally   
      22133  1996    Atlanta  Equestrian       Eventing       LATTA, Victoria Jean   
      22830  1996    Atlanta     Sailing        Sailing           KENDALL, Barbara   
      24804  2000     Sydney     Sailing        Sailing           KENDALL, Barbara   
      26030  2004     Athens     Cycling  Cycling Track               ULMER, Sarah   
      26648  2004     Athens      Rowing         Rowing   EVERS-SWINDELL, Caroline   
      26649  2004     Athens      Rowing         Rowing   EVERS-SWINDELL, Georgina   
      27714  2008    Beijing   Athletics      Athletics              VILI, Valerie   
      28662  2008    Beijing      Rowing         Rowing   EVERS-SWINDELL, Caroline   
      28663  2008    Beijing      Rowing         Rowing   EVERS-SWINDELL, Georgina   
      29763  2012     London   Athletics      Athletics             ADAMS, Valerie   
      29953  2012     London       Canoe   Canoe Sprint           CARRINGTON, Lisa   
      30005  2012     London     Cycling    Cycling BMX              WALKER, Sarah   
      30108  2012     London  Equestrian       Eventing           POWELL, Caroline   
      30109  2012     London  Equestrian       Eventing          RICHARDS, Jonelle   
      30663  2012     London      Rowing         Rowing            HAIGH, Juliette   
      30664  2012     London      Rowing         Rowing             SCOWN, Rebecca   
      30791  2012     London     Sailing        Sailing                   ALEH, Jo   
      30792  2012     London     Sailing        Sailing             POWRIE, Olivia   
      
            Country Gender                       Event   Medal  
      8033      NZL  Women             100M Backstroke  Bronze  
      8223      NZL  Women                   Long Jump    Gold  
      10900     NZL  Women                        800M  Bronze  
      18700     NZL  Women                        Team  Bronze  
      18701     NZL  Women                        Team  Bronze  
      19264     NZL  Women  Pair Without Coxswain (2-)  Bronze  
      19265     NZL  Women  Pair Without Coxswain (2-)  Bronze  
      20012     NZL  Women                    Marathon  Bronze  
      20394     NZL  Women                        Team  Silver  
      21013     NZL  Women     470 - Two Person Dinghy  Silver  
      21014     NZL  Women     470 - Two Person Dinghy  Silver  
      21019     NZL  Women             Board (Lechner)    Gold  
      22125     NZL  Women                  Individual  Silver  
      22133     NZL  Women                        Team  Bronze  
      22830     NZL  Women             Board (Mistral)  Silver  
      24804     NZL  Women             Board (Mistral)  Bronze  
      26030     NZL  Women          Individual Pursuit    Gold  
      26648     NZL  Women          Double Sculls (2X)    Gold  
      26649     NZL  Women          Double Sculls (2X)    Gold  
      27714     NZL  Women                    Shot Put    Gold  
      28662     NZL  Women          Double Sculls (2X)    Gold  
      28663     NZL  Women          Double Sculls (2X)    Gold  
      29763     NZL  Women                    Shot Put    Gold  
      29953     NZL  Women                    K-1 200M    Gold  
      30005     NZL  Women                  Individual  Silver  
      30108     NZL  Women                        Team  Bronze  
      30109     NZL  Women                        Team  Bronze  
      30663     NZL  Women             Coxless Pair 2-  Bronze  
      30664     NZL  Women             Coxless Pair 2-  Bronze  
      30791     NZL  Women                         470    Gold  
      30792     NZL  Women                         470    Gold  ),
     (('PAK', 'Men'),
             Year                   City   Sport Discipline            Athlete  \
      9564   1956  Melbourne / Stockholm  Hockey     Hockey       ABDUL, Hamid   
      9565   1956  Melbourne / Stockholm  Hockey     Hockey    AHKTAR, Hussain   
      9566   1956  Melbourne / Stockholm  Hockey     Hockey   DAR, Munir Ahmad   
      9567   1956  Melbourne / Stockholm  Hockey     Hockey      GHULAM, Rasul   
      9568   1956  Melbourne / Stockholm  Hockey     Hockey   HABIB, Ur Rehman   
      ...     ...                    ...     ...        ...                ...   
      20694  1992              Barcelona  Hockey     Hockey     SHAHBAZ, Ahmed   
      20695  1992              Barcelona  Hockey     Hockey  SHAHBAZ, Muhammad   
      20696  1992              Barcelona  Hockey     Hockey   SHAHID, Ali Khan   
      20697  1992              Barcelona  Hockey     Hockey       TAHIR, Zaman   
      20698  1992              Barcelona  Hockey     Hockey       WASIM, Feroz   
      
            Country Gender   Event   Medal  
      9564      PAK    Men  Hockey  Silver  
      9565      PAK    Men  Hockey  Silver  
      9566      PAK    Men  Hockey  Silver  
      9567      PAK    Men  Hockey  Silver  
      9568      PAK    Men  Hockey  Silver  
      ...       ...    ...     ...     ...  
      20694     PAK    Men  Hockey  Bronze  
      20695     PAK    Men  Hockey  Bronze  
      20696     PAK    Men  Hockey  Bronze  
      20697     PAK    Men  Hockey  Bronze  
      20698     PAK    Men  Hockey  Bronze  
      
      [121 rows x 9 columns]),
     (('PAN', 'Men'),
             Year     City      Sport Discipline                        Athlete  \
      7301   1948   London  Athletics  Athletics                 LABEACH, Lloyd   
      7313   1948   London  Athletics  Athletics                 LABEACH, Lloyd   
      27693  2008  Beijing  Athletics  Athletics  SALADINO ARANDA, Irving Jahir   
      
            Country Gender      Event   Medal  
      7301      PAN    Men       100M  Bronze  
      7313      PAN    Men       200M  Bronze  
      27693     PAN    Men  Long Jump    Gold  ),
     (('PAR', 'Men'),
             Year    City     Sport Discipline              Athlete Country Gender  \
      26223  2004  Athens  Football   Football       BAREIRO, Fredy     PAR    Men   
      26224  2004  Athens  Football   Football       BARRETO, Diego     PAR    Men   
      26225  2004  Athens  Football   Football       BARRETO, Edgar     PAR    Men   
      26226  2004  Athens  Football   Football       BENITEZ, Pedro     PAR    Men   
      26227  2004  Athens  Football   Football        CARDOZO, Jose     PAR    Men   
      26228  2004  Athens  Football   Football   CRISTALDO, Ernesto     PAR    Men   
      26229  2004  Athens  Football   Football         DEVACA, Jose     PAR    Men   
      26230  2004  Athens  Football   Football        DIAZ, Osvaldo     PAR    Men   
      26231  2004  Athens  Football   Football  ENCISO, Julio Cesar     PAR    Men   
      26232  2004  Athens  Football   Football      ESQUIVEL, Celso     PAR    Men   
      26233  2004  Athens  Football   Football     FIGUEREDO, Diego     PAR    Men   
      26234  2004  Athens  Football   Football      GAMARRA, Carlos     PAR    Men   
      26235  2004  Athens  Football   Football       GIMENEZ, Pablo     PAR    Men   
      26236  2004  Athens  Football   Football      GONZALEZ, Julio     PAR    Men   
      26237  2004  Athens  Football   Football        MANZUR, Julio     PAR    Men   
      26238  2004  Athens  Football   Football     MARTINEZ, Emilio     PAR    Men   
      26239  2004  Athens  Football   Football    TORRES, Aureliano     PAR    Men   
      
                Event   Medal  
      26223  Football  Silver  
      26224  Football  Silver  
      26225  Football  Silver  
      26226  Football  Silver  
      26227  Football  Silver  
      26228  Football  Silver  
      26229  Football  Silver  
      26230  Football  Silver  
      26231  Football  Silver  
      26232  Football  Silver  
      26233  Football  Silver  
      26234  Football  Silver  
      26235  Football  Silver  
      26236  Football  Silver  
      26237  Football  Silver  
      26238  Football  Silver  
      26239  Football  Silver  ),
     (('PER', 'Men'),
             Year         City     Sport Discipline                     Athlete  \
      7947   1948       London  Shooting   Shooting          VASQUEZ CAM, Edwin   
      17888  1984  Los Angeles  Shooting   Shooting             BOZA, Francisco   
      21088  1992    Barcelona  Shooting   Shooting  GIHA, Juan Jorge Yarve Jr.   
      
            Country Gender                  Event   Medal  
      7947      PER    Men  50M Pistol (60 Shots)    Gold  
      17888     PER    Men     Trap (125 Targets)  Silver  
      21088     PER    Men    Skeet (125 Targets)  Silver  ),
     (('PER', 'Women'),
             Year   City       Sport  Discipline                    Athlete Country  \
      19495  1988  Seoul  Volleyball  Volleyball             CERVERA, Luisa     PER   
      19496  1988  Seoul  Volleyball  Volleyball    DE LA GUERRA, Alejandra     PER   
      19497  1988  Seoul  Volleyball  Volleyball           FAJARDO, Denisse     PER   
      19498  1988  Seoul  Volleyball  Volleyball           GALLARDO, Miriam     PER   
      19499  1988  Seoul  Volleyball  Volleyball               GARCIA, Rosa     PER   
      19500  1988  Seoul  Volleyball  Volleyball            HEREDIA, Isabel     PER   
      19501  1988  Seoul  Volleyball  Volleyball           HORNY, Katherine     PER   
      19502  1988  Seoul  Volleyball  Volleyball            MALAGA, Natalia     PER   
      19503  1988  Seoul  Volleyball  Volleyball  PEREZ DEL SOLAR, Gabriela     PER   
      19504  1988  Seoul  Volleyball  Volleyball              TAIT, Cecilia     PER   
      19505  1988  Seoul  Volleyball  Volleyball            TORREALVA, Gina     PER   
      19506  1988  Seoul  Volleyball  Volleyball             URIBE, Cenaida     PER   
      
            Gender       Event   Medal  
      19495  Women  Volleyball  Silver  
      19496  Women  Volleyball  Silver  
      19497  Women  Volleyball  Silver  
      19498  Women  Volleyball  Silver  
      19499  Women  Volleyball  Silver  
      19500  Women  Volleyball  Silver  
      19501  Women  Volleyball  Silver  
      19502  Women  Volleyball  Silver  
      19503  Women  Volleyball  Silver  
      19504  Women  Volleyball  Silver  
      19505  Women  Volleyball  Silver  
      19506  Women  Volleyball  Silver  ),
     (('PHI', 'Men'),
             Year         City      Sport Discipline                 Athlete  \
      5031   1928    Amsterdam   Aquatics   Swimming      YLDEFONSO, Teofilo   
      5741   1932  Los Angeles   Aquatics   Swimming      YLDEFONSO, Teofilo   
      5889   1932  Los Angeles  Athletics  Athletics  TORIBIO, Simeon Galvez   
      5922   1932  Los Angeles     Boxing     Boxing        VILLANUEVA, Jose   
      6447   1936       Berlin  Athletics  Athletics        WHITE, Miguel S.   
      11005  1964        Tokyo     Boxing     Boxing  VILLANUEVA, Anthony N.   
      18513  1988        Seoul     Boxing     Boxing      SERANTES, Leopoldo   
      20184  1992    Barcelona     Boxing     Boxing           VELASCO, Roel   
      21927  1996      Atlanta     Boxing     Boxing       VELASCO, Mansueto   
      
            Country Gender                       Event   Medal  
      5031      PHI    Men           200M Breaststroke  Bronze  
      5741      PHI    Men           200M Breaststroke  Bronze  
      5889      PHI    Men                   High Jump  Bronze  
      5922      PHI    Men  50.8 - 54KG (Bantamweight)  Bronze  
      6447      PHI    Men                400M Hurdles  Bronze  
      11005     PHI    Men   54 - 57KG (Featherweight)  Silver  
      18513     PHI    Men    - 48KG (Light-Flyweight)  Bronze  
      20184     PHI    Men    - 48KG (Light-Flyweight)  Bronze  
      21927     PHI    Men    - 48KG (Light-Flyweight)  Silver  ),
     (('POL', 'Men'),
             Year    City          Sport           Discipline  \
      4413   1924   Paris        Cycling        Cycling Track   
      4414   1924   Paris        Cycling        Cycling Track   
      4415   1924   Paris        Cycling        Cycling Track   
      4416   1924   Paris        Cycling        Cycling Track   
      4436   1924   Paris     Equestrian              Jumping   
      ...     ...     ...            ...                  ...   
      29760  2012  London      Athletics            Athletics   
      30823  2012  London        Sailing              Sailing   
      31056  2012  London  Weightlifting        Weightlifting   
      31087  2012  London  Weightlifting        Weightlifting   
      31160  2012  London      Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                 Event   Medal  
      4413               LANGE, Jozef     POL    Men  Team Pursuit (4000M)  Silver  
      4414              LAZARSKI, Jan     POL    Men  Team Pursuit (4000M)  Silver  
      4415        STANKIEWICZ, Tomasz     POL    Men  Team Pursuit (4000M)  Silver  
      4416       SZYMCZYK, Franciszek     POL    Men  Team Pursuit (4000M)  Silver  
      4436         KROLIKIEWICZ, Adam     POL    Men            Individual  Bronze  
      ...                         ...     ...    ...                   ...     ...  
      29760          MAJEWSKI, Tomasz     POL    Men              Shot Put    Gold  
      30823   MIARCZYNSKI, Przemyslaw     POL    Men                  Rs:X  Bronze  
      31056          BONK, Bartlomiej     POL    Men                 105KG  Bronze  
      31087  ZIELINSKI, Adrian Edward     POL    Men                  85KG    Gold  
      31160        JANIKOWSKI, Damian     POL    Men              Wg 84 KG  Bronze  
      
      [411 rows x 9 columns]),
     (('POL', 'Women'),
             Year         City      Sport    Discipline                  Athlete  \
      5170   1928    Amsterdam  Athletics     Athletics        KONOPACKA, Halina   
      5809   1932  Los Angeles  Athletics     Athletics  WALASIEWICZ, Stanislawa   
      5883   1932  Los Angeles  Athletics     Athletics       WAJSOURNA, Jadwiga   
      6431   1936       Berlin  Athletics     Athletics  WALASIEWICZ, Stanislawa   
      6506   1936       Berlin  Athletics     Athletics       WAJSOURNA, Jadwiga   
      ...     ...          ...        ...           ...                      ...   
      29976  2012       London      Canoe  Canoe Sprint           NAJA, Karolina   
      30675  2012       London     Rowing        Rowing     FULARCZYK, Magdalena   
      30676  2012       London     Rowing        Rowing         MICHALSKA, Julia   
      30826  2012       London    Sailing       Sailing          KLEPACKA, Zofia   
      30843  2012       London   Shooting      Shooting          BOGACKA, Sylwia   
      
            Country Gender          Event   Medal  
      5170      POL  Women   Discus Throw    Gold  
      5809      POL  Women           100M    Gold  
      5883      POL  Women   Discus Throw  Bronze  
      6431      POL  Women           100M  Silver  
      6506      POL  Women   Discus Throw  Silver  
      ...       ...    ...            ...     ...  
      29976     POL  Women       K-2 500M  Bronze  
      30675     POL  Women  Double Sculls  Bronze  
      30676     POL  Women  Double Sculls  Bronze  
      30826     POL  Women           Rs:X  Bronze  
      30843     POL  Women  10M Air Rifle  Silver  
      
      [100 rows x 9 columns]),
     (('POR', 'Men'),
             Year         City       Sport    Discipline  \
      4439   1924        Paris  Equestrian       Jumping   
      4440   1924        Paris  Equestrian       Jumping   
      4441   1924        Paris  Equestrian       Jumping   
      6703   1936       Berlin  Equestrian       Jumping   
      6704   1936       Berlin  Equestrian       Jumping   
      6705   1936       Berlin  Equestrian       Jumping   
      7563   1948       London  Equestrian      Dressage   
      7564   1948       London  Equestrian      Dressage   
      7565   1948       London  Equestrian      Dressage   
      7932   1948       London     Sailing       Sailing   
      7933   1948       London     Sailing       Sailing   
      8811   1952     Helsinki     Sailing       Sailing   
      8812   1952     Helsinki     Sailing       Sailing   
      10585  1960         Rome     Sailing       Sailing   
      10586  1960         Rome     Sailing       Sailing   
      14067  1976     Montreal   Athletics     Athletics   
      15045  1976     Montreal    Shooting      Shooting   
      16887  1984  Los Angeles   Athletics     Athletics   
      16933  1984  Los Angeles   Athletics     Athletics   
      22813  1996      Atlanta     Sailing       Sailing   
      22814  1996      Atlanta     Sailing       Sailing   
      24622  2000       Sydney        Judo          Judo   
      25540  2004       Athens   Athletics     Athletics   
      25550  2004       Athens   Athletics     Athletics   
      26010  2004       Athens     Cycling  Cycling Road   
      27717  2008      Beijing   Athletics     Athletics   
      29961  2012       London       Canoe  Canoe Sprint   
      29962  2012       London       Canoe  Canoe Sprint   
      
                                                      Athlete Country Gender  \
      4439                          BORGES D'ALMEIDA, Antonio     POR    Men   
      4440                           DE SOUZA MARTINS, Helder     POR    Men   
      4441                       MOUZINHO D'ALBUQUERQUE, José     POR    Men   
      6703                                      BELTRAO, Jose     POR    Men   
      6704   COUTINHO (MARQUES DO FUNCHAL), Domingos De Sousa     POR    Men   
      6705                                        SILVA, Luiz     POR    Men   
      7563                               PAES, Fernando Silva     POR    Men   
      7564                                        SILVA, Luiz     POR    Men   
      7565                                 VALADAS, Francisco     POR    Men   
      7932                          BELLO, Duarte M.D'Almeida     POR    Men   
      7933                       BELLO, Fernando Pinto Coelho     POR    Men   
      8811                      ANDRADE, Francisco Rebello De     POR    Men   
      8812                   FIUZA, Joaquim Mascarenhas De M.     POR    Men   
      10585                         QUINA, Jose Manuel Gentil     POR    Men   
      10586                               QUINA, Mario Gentil     POR    Men   
      14067                                     LOPES, Carlos     POR    Men   
      15045                         MARQUES, Armando Da Silva     POR    Men   
      16887                                   LEITAO, Antonio     POR    Men   
      16933                                     LOPES, Carlos     POR    Men   
      22813                                     BARRETO, Nuno     POR    Men   
      22814                                ROCHA, Victor Hugo     POR    Men   
      24622                                     DELGADO, Nuno     POR    Men   
      25540                                 OBIKWELU, Francis     POR    Men   
      25550                                        SILVA, Rui     POR    Men   
      26010                                  PAULINHO, Sergio     POR    Men   
      27717                                     EVORA, Nelson     POR    Men   
      29961                                 PIMENTA, Fernando     POR    Men   
      29962                                    SILVA, Emanuel     POR    Men   
      
                                       Event   Medal  
      4439                              Team  Bronze  
      4440                              Team  Bronze  
      4441                              Team  Bronze  
      6703                              Team  Bronze  
      6704                              Team  Bronze  
      6705                              Team  Bronze  
      7563                              Team  Bronze  
      7564                              Team  Bronze  
      7565                              Team  Bronze  
      7932              Swallow (Golondrina)  Silver  
      7933              Swallow (Golondrina)  Silver  
      8811   Two-Person Keelboat Open (Star)  Bronze  
      8812   Two-Person Keelboat Open (Star)  Bronze  
      10585  Two-Person Keelboat Open (Star)  Silver  
      10586  Two-Person Keelboat Open (Star)  Silver  
      14067                           10000M  Silver  
      15045               Trap (125 Targets)  Silver  
      16887                            5000M  Bronze  
      16933                         Marathon    Gold  
      22813          470 - Two Person Dinghy  Bronze  
      22814          470 - Two Person Dinghy  Bronze  
      24622    73 - 81KG (Half-Middleweight)  Bronze  
      25540                             100M  Silver  
      25550                            1500M  Bronze  
      26010             Individual Road Race  Silver  
      27717                      Triple Jump    Gold  
      29961                        K-2 1000M  Silver  
      29962                        K-2 1000M  Silver  ),
     (('POR', 'Women'),
             Year         City      Sport Discipline             Athlete Country  \
      16935  1984  Los Angeles  Athletics  Athletics          MOTA, Rosa     POR   
      18426  1988        Seoul  Athletics  Athletics          MOTA, Rosa     POR   
      21592  1996      Atlanta  Athletics  Athletics   RIBEIRO, Fernanda     POR   
      23517  2000       Sydney  Athletics  Athletics   RIBEIRO, Fernanda     POR   
      29015  2008      Beijing  Triathlon  Triathlon  FERNANDES, Vanessa     POR   
      
            Gender       Event   Medal  
      16935  Women    Marathon  Bronze  
      18426  Women    Marathon    Gold  
      21592  Women      10000M    Gold  
      23517  Women      10000M  Bronze  
      29015  Women  Individual  Silver  ),
     (('PRK', 'Men'),
             Year       City          Sport           Discipline           Athlete  \
      13087  1972     Munich         Boxing               Boxing        KIM, U Gil   
      13566  1972     Munich           Judo                 Judo      KIM, Yong Ik   
      13731  1972     Munich       Shooting             Shooting        LI, Ho-Jun   
      13846  1972     Munich      Wrestling      Wrestling Free.  KIM, Gwong Hyong   
      14287  1976   Montreal         Boxing               Boxing      LI, Byong Uk   
      14298  1976   Montreal         Boxing               Boxing      GU, Young Jo   
      15592  1980     Moscow         Boxing               Boxing      LI, Byong Uk   
      16502  1980     Moscow  Weightlifting        Weightlifting     HAN, Gyong Si   
      16504  1980     Moscow  Weightlifting        Weightlifting     HO, Bong Chol   
      16534  1980     Moscow      Wrestling      Wrestling Free.     JANG, Se Hong   
      16543  1980     Moscow      Wrestling      Wrestling Free.      LI, Ho Pyong   
      20193  1992  Barcelona         Boxing               Boxing     CHOI, Chol Su   
      20196  1992  Barcelona         Boxing               Boxing     LI, Gwang Sik   
      20545  1992  Barcelona     Gymnastics          Artistic G.       PAE, Gil-Su   
      21231  1992  Barcelona  Weightlifting        Weightlifting    KIM, Myong Nam   
      21243  1992  Barcelona      Wrestling      Wrestling Free.           KIM, Il   
      21249  1992  Barcelona      Wrestling      Wrestling Free.       LI, Hak-Son   
      21251  1992  Barcelona      Wrestling      Wrestling Free.     KIM, Yong Sik   
      23085  1996    Atlanta  Weightlifting        Weightlifting    KIM, Myong Nam   
      23086  1996    Atlanta  Weightlifting        Weightlifting      JON, Chol Ho   
      23102  1996    Atlanta      Wrestling      Wrestling Free.           KIM, Il   
      23110  1996    Atlanta      Wrestling      Wrestling Free.      RI, Yong Sam   
      23866  2000     Sydney         Boxing               Boxing      KIM, Un Chol   
      25152  2000     Sydney      Wrestling      Wrestling Gre-R   KANG, Yong Gyun   
      25899  2004     Athens         Boxing               Boxing     KIM, Song Guk   
      26853  2004     Athens       Shooting             Shooting      KIM, Jong Su   
      28615  2008    Beijing           Judo                 Judo     PAK, Chol Min   
      31063  2012     London  Weightlifting        Weightlifting      OM, Yun Chol   
      31069  2012     London  Weightlifting        Weightlifting       KIM, Un Guk   
      31103  2012     London      Wrestling  Wrestling Freestyle    YANG, Kyong Il   
      
            Country Gender                              Event   Medal  
      13087     PRK    Men           - 48KG (Light-Flyweight)  Silver  
      13566     PRK    Men               - 63KG (Lightweight)  Bronze  
      13731     PRK    Men         50M Rifle Prone (60 Shots)    Gold  
      13846     PRK    Men              48 - 52KG (Flyweight)  Bronze  
      14287     PRK    Men           - 48KG (Light-Flyweight)  Silver  
      14298     PRK    Men           51 - 54KG (Bantamweight)    Gold  
      15592     PRK    Men           - 48KG (Light-Flyweight)  Bronze  
      16502     PRK    Men          - 52KG, Total (Flyweight)  Bronze  
      16504     PRK    Men          - 52KG, Total (Flyweight)  Silver  
      16534     PRK    Men           - 48KG (Light-Flyweight)  Silver  
      16543     PRK    Men           52 - 57KG (Bantamweight)  Silver  
      20193     PRK    Men              48 - 51KG (Flyweight)    Gold  
      20196     PRK    Men           51 - 54KG (Bantamweight)  Bronze  
      20545     PRK    Men                       Pommel Horse    Gold  
      21231     PRK    Men  67.5 - 75KG, Total (Middleweight)  Bronze  
      21243     PRK    Men           - 48KG (Light-Flyweight)    Gold  
      21249     PRK    Men              48 - 52KG (Flyweight)    Gold  
      21251     PRK    Men           52 - 57KG (Bantamweight)  Bronze  
      23085     PRK    Men     64 - 70KG, Total (Lightweight)  Silver  
      23086     PRK    Men    70 - 76KG, Total (Middleweight)  Bronze  
      23102     PRK    Men           - 48KG (Light-Flyweight)    Gold  
      23110     PRK    Men           52 - 57KG (Bantamweight)  Bronze  
      23866     PRK    Men           - 48KG (Light-Flyweight)  Bronze  
      25152     PRK    Men                          48 - 54KG  Bronze  
      25899     PRK    Men          54 - 57KG (Featherweight)  Silver  
      26853     PRK    Men              50M Pistol (60 Shots)  Bronze  
      28615     PRK    Men       60 - 66KG (Half-Lightweight)  Bronze  
      31063     PRK    Men                              -56KG    Gold  
      31069     PRK    Men                               62KG    Gold  
      31103     PRK    Men                           Wf 55 KG  Bronze  ),
     (('PRK', 'Women'),
             Year       City          Sport     Discipline          Athlete Country  \
      13778  1972     Munich     Volleyball     Volleyball    CHANG, Ok Rim     PRK   
      13779  1972     Munich     Volleyball     Volleyball    CHONG, Ok Jin     PRK   
      13780  1972     Munich     Volleyball     Volleyball   HWANG, Hye Suk     PRK   
      13781  1972     Munich     Volleyball     Volleyball     KANG, Ok Sun     PRK   
      13782  1972     Munich     Volleyball     Volleyball    KIM, Jung Bok     PRK   
      13783  1972     Munich     Volleyball     Volleyball   KIM, Myong Suk     PRK   
      13784  1972     Munich     Volleyball     Volleyball      KIM, Su Dae     PRK   
      13785  1972     Munich     Volleyball     Volleyball       KIM, Un Ja     PRK   
      13786  1972     Munich     Volleyball     Volleyball  PAEK, Myong Suk     PRK   
      13787  1972     Munich     Volleyball     Volleyball      RI, Chun Ok     PRK   
      13788  1972     Munich     Volleyball     Volleyball    RYOM, Chun Ja     PRK   
      21103  1992  Barcelona   Table Tennis   Table Tennis      LI, Bun Hui     PRK   
      21104  1992  Barcelona   Table Tennis   Table Tennis      YU, Sun Bok     PRK   
      21114  1992  Barcelona   Table Tennis   Table Tennis      LI, Bun Hui     PRK   
      22612  1996    Atlanta           Judo           Judo     KYE, Sun Hui     PRK   
      24593  2000     Sydney           Judo           Judo     KYE, Sun Hui     PRK   
      25103  2000     Sydney  Weightlifting  Weightlifting     RI, Song Hui     PRK   
      26595  2004     Athens           Judo           Judo     KYE, Sun Hui     PRK   
      26945  2004     Athens   Table Tennis   Table Tennis    KIM, Hyang Mi     PRK   
      27095  2004     Athens  Weightlifting  Weightlifting     RI, Song Hui     PRK   
      28374  2008    Beijing     Gymnastics    Artistic G.    HONG, Un Jong     PRK   
      28605  2008    Beijing           Judo           Judo       AN, Kum Ae     PRK   
      28611  2008    Beijing           Judo           Judo       WON, Ok Im     PRK   
      29118  2008    Beijing  Weightlifting  Weightlifting       O, Jong Ae     PRK   
      29125  2008    Beijing  Weightlifting  Weightlifting    PAK, Hyon Suk     PRK   
      30595  2012     London           Judo           Judo       AN, Kum Ae     PRK   
      31059  2012     London  Weightlifting  Weightlifting  RYANG, Chun Hwa     PRK   
      31078  2012     London  Weightlifting  Weightlifting    RIM, Jong Sim     PRK   
      
            Gender                          Event   Medal  
      13778  Women                     Volleyball  Bronze  
      13779  Women                     Volleyball  Bronze  
      13780  Women                     Volleyball  Bronze  
      13781  Women                     Volleyball  Bronze  
      13782  Women                     Volleyball  Bronze  
      13783  Women                     Volleyball  Bronze  
      13784  Women                     Volleyball  Bronze  
      13785  Women                     Volleyball  Bronze  
      13786  Women                     Volleyball  Bronze  
      13787  Women                     Volleyball  Bronze  
      13788  Women                     Volleyball  Bronze  
      21103  Women                        Doubles  Bronze  
      21104  Women                        Doubles  Bronze  
      21114  Women                        Singles  Bronze  
      22612  Women     - 48KG (Extra-Lightweight)    Gold  
      24593  Women   48 - 52KG (Half-Lightweight)  Bronze  
      25103  Women                           58KG  Silver  
      26595  Women        52 - 57KG (Lightweight)  Silver  
      26945  Women                        Singles  Silver  
      27095  Women                           58KG  Silver  
      28374  Women                          Vault    Gold  
      28605  Women   48 - 52KG (Half-Lightweight)  Silver  
      28611  Women  57 - 63KG (Half-Middleweight)  Bronze  
      29118  Women                           58KG  Bronze  
      29125  Women                           63KG    Gold  
      30595  Women                      48 - 52KG    Gold  
      31059  Women                           48KG  Bronze  
      31078  Women                           69KG    Gold  ),
     (('PUR', 'Men'),
             Year         City      Sport           Discipline  \
      7467   1948       London     Boxing               Boxing   
      14284  1976     Montreal     Boxing               Boxing   
      17046  1984  Los Angeles     Boxing               Boxing   
      17059  1984  Los Angeles     Boxing               Boxing   
      20211  1992    Barcelona     Boxing               Boxing   
      21952  1996      Atlanta     Boxing               Boxing   
      29632  2012       London  Athletics            Athletics   
      31130  2012       London  Wrestling  Wrestling Freestyle   
      
                              Athlete Country Gender                       Event  \
      7467           VENEGAS, Juan E.     PUR    Men    51 - 54KG (Bantamweight)   
      14284        MALDONADO, Orlando     PUR    Men    - 48KG (Light-Flyweight)   
      17046            ORTIZ, Luis F.     PUR    Men     57 - 60KG (Lightweight)   
      17059       GONZALEZ, Aristides     PUR    Men                     71-75KG   
      20211  ACEVEDO SANTIAGO, Anibal     PUR    Men  63.5 - 67KG (Welterweight)   
      21952            SANTOS, Daniel     PUR    Men  63.5 - 67KG (Welterweight)   
      29632            CULSON, Javier     PUR    Men                400M Hurdles   
      31130     ESPINAL, Jaime Yusept     PUR    Men                    Wf 84 KG   
      
              Medal  
      7467   Bronze  
      14284  Bronze  
      17046  Silver  
      17059  Bronze  
      20211  Bronze  
      21952  Bronze  
      29632  Bronze  
      31130  Silver  ),
     (('QAT', 'Men'),
             Year       City          Sport     Discipline                  Athlete  \
      19870  1992  Barcelona      Athletics      Athletics  SULAIMAN, Mohamed Ahmed   
      25089  2000     Sydney  Weightlifting  Weightlifting         ASAAD, Said Saif   
      29730  2012     London      Athletics      Athletics      BARSHIM, Mutaz Essa   
      30868  2012     London       Shooting       Shooting       AL-ATTIYAH, Nasser   
      
            Country Gender      Event   Medal  
      19870     QAT    Men      1500M  Bronze  
      25089     QAT    Men      105KG  Bronze  
      29730     QAT    Men  High Jump  Bronze  
      30868     QAT    Men      Skeet  Bronze  ),
     (('ROU', 'Men'),
             Year    City          Sport     Discipline                    Athlete  \
      4730   1924   Paris          Rugby          Rugby            ANASTASIADE, N.   
      4731   1924   Paris          Rugby          Rugby           ARMASEL, Dumitru   
      4732   1924   Paris          Rugby          Rugby           BENTIA, Gheorghe   
      4733   1924   Paris          Rugby          Rugby             COCIOCIAHO, J.   
      4734   1924   Paris          Rugby          Rugby             CRATUNESCO, C.   
      ...     ...     ...            ...            ...                        ...   
      30185  2012  London        Fencing        Fencing          DUMITRESCU, Rares   
      30186  2012  London        Fencing        Fencing       SIRITEANU, Alexandru   
      30187  2012  London        Fencing        Fencing            ZALOMIR, Florin   
      30839  2012  London       Shooting       Shooting    MOLDOVEANU, Alin George   
      31077  2012  London  Weightlifting  Weightlifting  MARTIN, Razvan Constantin   
      
            Country Gender          Event   Medal  
      4730      ROU    Men          Rugby  Bronze  
      4731      ROU    Men          Rugby  Bronze  
      4732      ROU    Men          Rugby  Bronze  
      4733      ROU    Men          Rugby  Bronze  
      4734      ROU    Men          Rugby  Bronze  
      ...       ...    ...            ...     ...  
      30185     ROU    Men     Sabre Team  Silver  
      30186     ROU    Men     Sabre Team  Silver  
      30187     ROU    Men     Sabre Team  Silver  
      30839     ROU    Men  10M Air Rifle    Gold  
      31077     ROU    Men           69KG  Bronze  
      
      [305 rows x 9 columns]),
     (('ROU', 'Women'),
             Year                   City          Sport           Discipline  \
      9351   1956  Melbourne / Stockholm        Fencing              Fencing   
      9443   1956  Melbourne / Stockholm     Gymnastics          Artistic G.   
      9484   1956  Melbourne / Stockholm     Gymnastics          Artistic G.   
      9485   1956  Melbourne / Stockholm     Gymnastics          Artistic G.   
      9486   1956  Melbourne / Stockholm     Gymnastics          Artistic G.   
      ...     ...                    ...            ...                  ...   
      30358  2012                 London     Gymnastics  Gymnastics Artistic   
      30365  2012                 London     Gymnastics  Gymnastics Artistic   
      30580  2012                 London           Judo                 Judo   
      30600  2012                 London           Judo                 Judo   
      31079  2012                 London  Weightlifting        Weightlifting   
      
                                         Athlete Country Gender             Event  \
      9351                     ORBAN-SZABO, Olga     ROU  Women   Foil Individual   
      9443   LEUSTEANU-POPESCU-TEODORESCU, Elena     ROU  Women   Floor Exercises   
      9484       HURMUZACHI-DUMITRESCU, Georgeta     ROU  Women  Team Competition   
      9485                   IOVAN-INOVAN, Sonia     ROU  Women  Team Competition   
      9486   LEUSTEANU-POPESCU-TEODORESCU, Elena     ROU  Women  Team Competition   
      ...                                    ...     ...    ...               ...   
      30358                      PONOR, Catalina     ROU  Women  Team Competition   
      30365                IZBASA, Sandra Raluca     ROU  Women             Vault   
      30580                       DUMITRU, Alina     ROU  Women           - 48 KG   
      30600                    CAPRIORIU, Corina     ROU  Women         52 - 57KG   
      31079                COCOS, Roxana Daniela     ROU  Women              69KG   
      
              Medal  
      9351   Silver  
      9443   Bronze  
      9484   Bronze  
      9485   Bronze  
      9486   Bronze  
      ...       ...  
      30358  Bronze  
      30365    Gold  
      30580  Silver  
      30600  Silver  
      31079  Silver  
      
      [335 rows x 9 columns]),
     (('RSA', 'Men'),
             Year       City      Sport    Discipline                 Athlete  \
      1191   1908     London  Athletics     Athletics        WALKER, Reginald   
      1272   1908     London  Athletics     Athletics    HEFFERON, Charles A.   
      2121   1912  Stockholm  Athletics     Athletics  MCARTHUR, Kennedy Kane   
      2122   1912  Stockholm  Athletics     Athletics   GITSHAM, Christian W.   
      2143   1912  Stockholm    Cycling  Cycling Road          LEWIS, Rudolph   
      ...     ...        ...        ...           ...                     ...   
      29297  2012     London   Aquatics      Swimming           LE CLOS, Chad   
      30731  2012     London     Rowing        Rowing       BRITTAIN, Matthew   
      30732  2012     London     Rowing        Rowing           NDLOVU, Sizwe   
      30733  2012     London     Rowing        Rowing             SMITH, John   
      30734  2012     London     Rowing        Rowing         THOMPSON, James   
      
            Country Gender                  Event   Medal  
      1191      RSA    Men                   100M    Gold  
      1272      RSA    Men               Marathon  Silver  
      2121      RSA    Men               Marathon    Gold  
      2122      RSA    Men               Marathon  Silver  
      2143      RSA    Men  Individual Time Trial    Gold  
      ...       ...    ...                    ...     ...  
      29297     RSA    Men         200M Butterfly    Gold  
      30731     RSA    Men          Lightweight 4    Gold  
      30732     RSA    Men          Lightweight 4    Gold  
      30733     RSA    Men          Lightweight 4    Gold  
      30734     RSA    Men          Lightweight 4    Gold  
      
      [84 rows x 9 columns]),
     (('RSA', 'Women'),
             Year                   City      Sport    Discipline  \
      5043   1928              Amsterdam   Aquatics      Swimming   
      5044   1928              Amsterdam   Aquatics      Swimming   
      5045   1928              Amsterdam   Aquatics      Swimming   
      5046   1928              Amsterdam   Aquatics      Swimming   
      5750   1932            Los Angeles   Aquatics      Swimming   
      5874   1932            Los Angeles  Athletics     Athletics   
      8034   1952               Helsinki   Aquatics      Swimming   
      8125   1952               Helsinki  Athletics     Athletics   
      8211   1952               Helsinki  Athletics     Athletics   
      8952   1956  Melbourne / Stockholm   Aquatics      Swimming   
      8953   1956  Melbourne / Stockholm   Aquatics      Swimming   
      8954   1956  Melbourne / Stockholm   Aquatics      Swimming   
      8955   1956  Melbourne / Stockholm   Aquatics      Swimming   
      19854  1992              Barcelona  Athletics     Athletics   
      21317  1996                Atlanta   Aquatics      Swimming   
      21324  1996                Atlanta   Aquatics      Swimming   
      21351  1996                Atlanta   Aquatics      Swimming   
      23206  2000                 Sydney   Aquatics      Swimming   
      23661  2000                 Sydney  Athletics     Athletics   
      25678  2004                 Athens  Athletics     Athletics   
      29708  2012                 London  Athletics     Athletics   
      29958  2012                 London      Canoe  Canoe Sprint   
      
                                           Athlete Country Gender  \
      5043                       REDFORD, Marie E.     RSA  Women   
      5044                           RENNIE, Rhoda     RSA  Women   
      5045                       RUSSELL, Kathleen     RSA  Women   
      5046         VAN DER GOES, Frederica Johanna     RSA  Women   
      5750                           MAAKAL, Jenny     RSA  Women   
      5874                      CLARK, Marjorie R.     RSA  Women   
      8034                  HARRISON, Joan Cynthia     RSA  Women   
      8125   ROBB-HASENJÄGER, Daphne Lilian Evelyn     RSA  Women   
      8211                  BRAND, Esther Cornelia     RSA  Women   
      8952                        ABERNETHY, Moira     RSA  Women   
      8953                MYBURGH, Jeanette Evelyn     RSA  Women   
      8954                    MYBURGH, Natalie Ann     RSA  Women   
      8955                ROBERTS, Susan Elizabeth     RSA  Women   
      19854                           MEYER, Elana     RSA  Women   
      21317                        KRIEL, Marianne     RSA  Women   
      21324                        HEYNS, Penelope     RSA  Women   
      21351                        HEYNS, Penelope     RSA  Women   
      23206                        HEYNS, Penelope     RSA  Women   
      23661                        CLOETE, Hestrie     RSA  Women   
      25678                        CLOETE, Hestrie     RSA  Women   
      29708                        SEMENYA, Caster     RSA  Women   
      29958                     HARTLEY, Bridgitte     RSA  Women   
      
                              Event   Medal  
      5043   4X100M Freestyle Relay  Bronze  
      5044   4X100M Freestyle Relay  Bronze  
      5045   4X100M Freestyle Relay  Bronze  
      5046   4X100M Freestyle Relay  Bronze  
      5750           400M Freestyle  Bronze  
      5874              80M Hurdles  Bronze  
      8034          100M Backstroke    Gold  
      8125                     100M  Silver  
      8211                High Jump    Gold  
      8952   4X100M Freestyle Relay  Bronze  
      8953   4X100M Freestyle Relay  Bronze  
      8954   4X100M Freestyle Relay  Bronze  
      8955   4X100M Freestyle Relay  Bronze  
      19854                  10000M  Silver  
      21317         100M Backstroke  Bronze  
      21324       100M Breaststroke    Gold  
      21351       200M Breaststroke    Gold  
      23206       100M Breaststroke  Bronze  
      23661               High Jump  Silver  
      25678               High Jump  Silver  
      29708                    800M  Silver  
      29958                K-1 500M  Bronze  ),
     (('RU1', 'Men'),
            Year       City      Sport       Discipline  \
      1852  1908     London    Skating   Figure skating   
      1927  1908     London  Wrestling  Wrestling Gre-R   
      1930  1908     London  Wrestling  Wrestling Gre-R   
      2535  1912  Stockholm     Rowing           Rowing   
      2538  1912  Stockholm    Sailing          Sailing   
      2539  1912  Stockholm    Sailing          Sailing   
      2540  1912  Stockholm    Sailing          Sailing   
      2541  1912  Stockholm    Sailing          Sailing   
      2542  1912  Stockholm    Sailing          Sailing   
      2543  1912  Stockholm    Sailing          Sailing   
      2544  1912  Stockholm    Sailing          Sailing   
      2658  1912  Stockholm   Shooting         Shooting   
      2659  1912  Stockholm   Shooting         Shooting   
      2660  1912  Stockholm   Shooting         Shooting   
      2661  1912  Stockholm   Shooting         Shooting   
      2752  1912  Stockholm   Shooting         Shooting   
      2818  1912  Stockholm  Wrestling  Wrestling Gre-R   
      
                                                 Athlete Country Gender  \
      1852                                PANIN, Nikolay     RU1    Men   
      1927                               ORLOFF, Nikolaï     RU1    Men   
      1930                           PETROFF, Aleksander     RU1    Men   
      2535                    KUSIK, Mikhaïl Maksimilian     RU1    Men   
      2538  Beloselsky-Belozersky, Esper Konstantinovich     RU1    Men   
      2539                               BRASCHE, Ernest     RU1    Men   
      2540                                LINDBLOM, Karl     RU1    Men   
      2541                          PUSCHNITSKY, Nikolaï     RU1    Men   
      2542                           RODIONOV, Aleksandr     RU1    Men   
      2543                             SCHOMAKER, Iossif     RU1    Men   
      2544                                STRAUCH, Filip     RU1    Men   
      2658                                DE KACHE, Amos     RU1    Men   
      2659                         DE MELNITSKY, Nikolaï     RU1    Men   
      2660                     DE PANTELEYMONOFF, Georgi     RU1    Men   
      2661                       DE WEYLOCHNIKOFF, Pavel     RU1    Men   
      2752                                   BLAU, Harry     RU1    Men   
      2818                                 KLEIN, Martin     RU1    Men   
      
                                 Event   Medal  
      1852             Special Figures    Gold  
      1927      - 66.6KG (Lightweight)  Silver  
      1930  + 93KG (Super Heavyweight)  Silver  
      2535          Single Sculls (1X)  Bronze  
      2538                         10M  Bronze  
      2539                         10M  Bronze  
      2540                         10M  Bronze  
      2541                         10M  Bronze  
      2542                         10M  Bronze  
      2543                         10M  Bronze  
      2544                         10M  Bronze  
      2658       30M Army Pistol, Team  Silver  
      2659       30M Army Pistol, Team  Silver  
      2660       30M Army Pistol, Team  Silver  
      2661       30M Army Pistol, Team  Silver  
      2752          Trap (125 Targets)  Bronze  
      2818  67.5 - 75KG (Middleweight)  Silver  ),
     (('RUS', 'Men'),
             Year     City      Sport           Discipline              Athlete  \
      21303  1996  Atlanta   Aquatics               Diving       SAUTIN, Dmitry   
      21326  1996  Atlanta   Aquatics             Swimming   KULIKOV, Vladislav   
      21327  1996  Atlanta   Aquatics             Swimming     PANKRATOV, Denis   
      21333  1996  Atlanta   Aquatics             Swimming     POPOV, Alexander   
      21347  1996  Atlanta   Aquatics             Swimming     KORNEYEV, Andrey   
      ...     ...      ...        ...                  ...                  ...   
      31144  2012   London  Wrestling  Wrestling Freestyle    SEMENOV, Mingiyan   
      31147  2012   London  Wrestling  Wrestling Freestyle  KURAMAGOMEDOV, Zaur   
      31153  2012   London  Wrestling  Wrestling Freestyle        VLASOV, Roman   
      31157  2012   London  Wrestling  Wrestling Freestyle        KHUGAEV, Alan   
      31162  2012   London  Wrestling  Wrestling Freestyle       TOTROV, Rustam   
      
            Country Gender              Event   Medal  
      21303     RUS    Men       10M Platform    Gold  
      21326     RUS    Men     100M Butterfly  Bronze  
      21327     RUS    Men     100M Butterfly    Gold  
      21333     RUS    Men     100M Freestyle    Gold  
      21347     RUS    Men  200M Breaststroke  Bronze  
      ...       ...    ...                ...     ...  
      31144     RUS    Men           Wg 55 KG  Bronze  
      31147     RUS    Men           Wg 60 KG  Bronze  
      31153     RUS    Men           Wg 74 KG    Gold  
      31157     RUS    Men           Wg 84 KG    Gold  
      31162     RUS    Men           Wg 96 KG  Silver  
      
      [409 rows x 9 columns]),
     (('RUS', 'Women'),
             Year     City          Sport           Discipline  \
      21313  1996  Atlanta       Aquatics               Diving   
      21595  1996  Atlanta      Athletics            Athletics   
      21613  1996  Atlanta      Athletics            Athletics   
      21712  1996  Atlanta      Athletics            Athletics   
      21722  1996  Atlanta      Athletics            Athletics   
      ...     ...      ...            ...                  ...   
      30956  2012   London         Tennis               Tennis   
      31052  2012   London  Weightlifting        Weightlifting   
      31073  2012   London  Weightlifting        Weightlifting   
      31116  2012   London      Wrestling  Wrestling Freestyle   
      31121  2012   London      Wrestling  Wrestling Freestyle   
      
                          Athlete Country Gender           Event   Medal  
      21313         LASHKO, Irina     RUS  Women  3M Springboard  Silver  
      21595    NIKOLAYEVA, Yelena     RUS  Women     10000M Walk    Gold  
      21613  MASTERKOVA, Svetlana     RUS  Women           1500M    Gold  
      21712  MASTERKOVA, Svetlana     RUS  Women            800M    Gold  
      21722       SADOVA, Natalya     RUS  Women    Discus Throw  Silver  
      ...                     ...     ...    ...             ...     ...  
      30956      SHARAPOVA, Maria     RUS  Women         Singles  Silver  
      31052    KASHIRINA, Tatiana     RUS  Women           +75KG  Silver  
      31073  TSARUKAEVA, Svetlana     RUS  Women            63KG  Silver  
      31116       VOLOSOVA, Lubov     RUS  Women        Wf 63 KG  Bronze  
      31121    VOROBIEVA, Natalia     RUS  Women        Wf 72 KG    Gold  
      
      [359 rows x 9 columns]),
     (('SCG', 'Men'),
             Year    City     Sport  Discipline                Athlete Country  \
      25456  2004  Athens  Aquatics  Water polo      CIRIC, Aleksandar     SCG   
      25457  2004  Athens  Aquatics  Water polo     GOJKOVIC, Vladimir     SCG   
      25458  2004  Athens  Aquatics  Water polo     IKODINOVIC, Danilo     SCG   
      25459  2004  Athens  Aquatics  Water polo        JELENIC, Viktor     SCG   
      25460  2004  Athens  Aquatics  Water polo         JOKIC, Predrag     SCG   
      25461  2004  Athens  Aquatics  Water polo        KULJACA, Nikola     SCG   
      25462  2004  Athens  Aquatics  Water polo        NIKIC, Slobodan     SCG   
      25463  2004  Athens  Aquatics  Water polo      SAPIC, Aleksandar     SCG   
      25464  2004  Athens  Aquatics  Water polo           SAVIC, Dejan     SCG   
      25465  2004  Athens  Aquatics  Water polo           SEFIK, Denis     SCG   
      25466  2004  Athens  Aquatics  Water polo       TRBOJEVIC, Petar     SCG   
      25467  2004  Athens  Aquatics  Water polo        UDOVICIC, Vanja     SCG   
      25468  2004  Athens  Aquatics  Water polo  VUJASINOVIC, Vladimir     SCG   
      
            Gender       Event   Medal  
      25456    Men  Water Polo  Silver  
      25457    Men  Water Polo  Silver  
      25458    Men  Water Polo  Silver  
      25459    Men  Water Polo  Silver  
      25460    Men  Water Polo  Silver  
      25461    Men  Water Polo  Silver  
      25462    Men  Water Polo  Silver  
      25463    Men  Water Polo  Silver  
      25464    Men  Water Polo  Silver  
      25465    Men  Water Polo  Silver  
      25466    Men  Water Polo  Silver  
      25467    Men  Water Polo  Silver  
      25468    Men  Water Polo  Silver  ),
     (('SCG', 'Women'),
             Year    City     Sport Discipline         Athlete Country Gender  \
      26834  2004  Athens  Shooting   Shooting  SEKARIC, Jasna     SCG  Women   
      
                                 Event   Medal  
      26834  10M Air Pistol (40 Shots)  Silver  ),
     (('SEN', 'Men'),
             Year   City      Sport Discipline                  Athlete Country  \
      18324  1988  Seoul  Athletics  Athletics  DIA BA, El Hadji Amadou     SEN   
      
            Gender         Event   Medal  
      18324    Men  400M Hurdles  Silver  ),
     (('SGP', 'Women'),
             Year    City         Sport    Discipline         Athlete Country  \
      30883  2012  London  Table Tennis  Table Tennis  FENG, Tian Wei     SGP   
      30899  2012  London  Table Tennis  Table Tennis  FENG, Tian Wei     SGP   
      30900  2012  London  Table Tennis  Table Tennis     LI, Jia Wei     SGP   
      30901  2012  London  Table Tennis  Table Tennis     WANG, Yuegu     SGP   
      
            Gender    Event   Medal  
      30883  Women  Singles  Bronze  
      30899  Women     Team  Bronze  
      30900  Women     Team  Bronze  
      30901  Women     Team  Bronze  ),
     (('SIN', 'Men'),
             Year  City          Sport     Discipline                  Athlete  \
      10616  1960  Rome  Weightlifting  Weightlifting  TAN, Howe-Liang (Tiger)   
      
            Country Gender                             Event   Medal  
      10616     SIN    Men  60 - 67.5KG, Total (Lightweight)  Silver  ),
     (('SIN', 'Women'),
             Year     City         Sport    Discipline         Athlete Country  \
      28957  2008  Beijing  Table Tennis  Table Tennis  FENG, Tian Wei     SIN   
      28958  2008  Beijing  Table Tennis  Table Tennis      LI, Jiawei     SIN   
      28959  2008  Beijing  Table Tennis  Table Tennis    WANG, Yue Gu     SIN   
      
            Gender Event   Medal  
      28957  Women  Team  Silver  
      28958  Women  Team  Silver  
      28959  Women  Team  Silver  ),
     (('SLO', 'Men'),
             Year       City          Sport       Discipline           Athlete  \
      20859  1992  Barcelona         Rowing           Rowing        COP, Iztok   
      20860  1992  Barcelona         Rowing           Rowing    ZVEGELJ, Denis   
      20931  1992  Barcelona         Rowing           Rowing      JANSA, Milan   
      20932  1992  Barcelona         Rowing           Rowing  KLEMENCIC, Janez   
      20933  1992  Barcelona         Rowing           Rowing    MIRJANIC, Saso   
      20934  1992  Barcelona         Rowing           Rowing     MUJKIC, Sadik   
      22052  1996    Atlanta  Canoe / Kayak  Canoe / Kayak S   VEHOVAR, Andraz   
      24647  2000     Sydney         Rowing           Rowing        COP, Iztok   
      24648  2000     Sydney         Rowing           Rowing        SPIK, Luka   
      24865  2000     Sydney       Shooting         Shooting  DEBEVEC, Rajmond   
      26644  2004     Athens         Rowing           Rowing        COP, Iztok   
      26645  2004     Athens         Rowing           Rowing        SPIK, Luka   
      26808  2004     Athens        Sailing          Sailing   ZBOGAR, Vasilij   
      27672  2008    Beijing      Athletics        Athletics    KOZMUS, Primoz   
      28815  2008    Beijing        Sailing          Sailing   ZBOGAR, Vasilij   
      28870  2008    Beijing       Shooting         Shooting  DEBEVEC, Rajmond   
      29720  2012     London      Athletics        Athletics    KOZMUS, Primoz   
      30669  2012     London         Rowing           Rowing        COP, Iztok   
      30670  2012     London         Rowing           Rowing        SPIK, Luka   
      30862  2012     London       Shooting         Shooting  DEBEVEC, Rajmond   
      
            Country Gender                               Event   Medal  
      20859     SLO    Men                   Coxless Pair (2-)  Bronze  
      20860     SLO    Men                   Coxless Pair (2-)  Bronze  
      20931     SLO    Men          Four Without Coxswain (4-)  Bronze  
      20932     SLO    Men          Four Without Coxswain (4-)  Bronze  
      20933     SLO    Men          Four Without Coxswain (4-)  Bronze  
      20934     SLO    Men          Four Without Coxswain (4-)  Bronze  
      22052     SLO    Men                  K-1 (Kayak Single)  Silver  
      24647     SLO    Men                  Double Sculls (2X)    Gold  
      24648     SLO    Men                  Double Sculls (2X)    Gold  
      24865     SLO    Men  50M Rifle 3 Positions (3X40 Shots)    Gold  
      26644     SLO    Men                  Double Sculls (2X)  Silver  
      26645     SLO    Men                  Double Sculls (2X)  Silver  
      26808     SLO    Men   Single-Handed Dinghy Open (Laser)  Bronze  
      27672     SLO    Men                        Hammer Throw    Gold  
      28815     SLO    Men           Laser - One Person Dinghy  Silver  
      28870     SLO    Men  50M Rifle 3 Positions (3X40 Shots)  Bronze  
      29720     SLO    Men                        Hammer Throw  Silver  
      30669     SLO    Men                       Double Sculls  Bronze  
      30670     SLO    Men                       Double Sculls  Bronze  
      30862     SLO    Men                     50M Rifle Prone  Bronze  ),
     (('SLO', 'Women'),
             Year     City      Sport Discipline            Athlete Country Gender  \
      21605  1996  Atlanta  Athletics  Athletics  BUKOVEC, Brigitta     SLO  Women   
      25652  2004   Athens  Athletics  Athletics    CEPLAK, Jolanda     SLO  Women   
      26597  2004   Athens       Judo       Judo      ZOLNIR, Urska     SLO  Women   
      27262  2008  Beijing   Aquatics   Swimming     ISAKOVIC, Sara     SLO  Women   
      28599  2008  Beijing       Judo       Judo   POLAVDER, Lucija     SLO  Women   
      30603  2012   London       Judo       Judo      ZOLNIR, Urska     SLO  Women   
      
                                     Event   Medal  
      21605                   100M Hurdles  Silver  
      25652                           800M  Bronze  
      26597  57 - 63KG (Half-Middleweight)  Bronze  
      27262                 200M Freestyle  Silver  
      28599           + 78KG (Heavyweight)  Bronze  
      30603                      57 - 63KG    Gold  ),
     (('SRB', 'Men'),
             Year     City     Sport  Discipline                Athlete Country  \
      27225  2008  Beijing  Aquatics    Swimming         CAVIC, Milorad     SRB   
      27443  2008  Beijing  Aquatics  Water polo      CIRIC, Aleksandar     SRB   
      27444  2008  Beijing  Aquatics  Water polo       FILIPOVIC, Filip     SRB   
      27445  2008  Beijing  Aquatics  Water polo           GOCIC, Zivko     SRB   
      27446  2008  Beijing  Aquatics  Water polo        PEKOVIC, Branko     SRB   
      27447  2008  Beijing  Aquatics  Water polo      PIJETLOVIC, Dusko     SRB   
      27448  2008  Beijing  Aquatics  Water polo    PRLAINOVIC, Andrija     SRB   
      27449  2008  Beijing  Aquatics  Water polo         RADJEN, Nikola     SRB   
      27450  2008  Beijing  Aquatics  Water polo      SAPIC, Aleksandar     SRB   
      27451  2008  Beijing  Aquatics  Water polo           SAVIC, Dejan     SRB   
      27452  2008  Beijing  Aquatics  Water polo           SEFIK, Denis     SRB   
      27453  2008  Beijing  Aquatics  Water polo         SORO, Slobodan     SRB   
      27454  2008  Beijing  Aquatics  Water polo        UDOVICIC, Vanja     SRB   
      27455  2008  Beijing  Aquatics  Water polo  VUJASINOVIC, Vladimir     SRB   
      29004  2008  Beijing    Tennis      Tennis        DJOKOVIC, Novak     SRB   
      29506  2012   London  Aquatics  Water Polo         ALEKSIC, Milan     SRB   
      29507  2012   London  Aquatics  Water Polo       FILIPOVIC, Filip     SRB   
      29508  2012   London  Aquatics  Water Polo           GOCIC, Zivko     SRB   
      29509  2012   London  Aquatics  Water Polo          MANDIC, Dusan     SRB   
      29510  2012   London  Aquatics  Water Polo       MITROVIC, Stefan     SRB   
      29511  2012   London  Aquatics  Water Polo        NIKIC, Slobodan     SRB   
      29512  2012   London  Aquatics  Water Polo      PIJETLOVIC, Dusko     SRB   
      29513  2012   London  Aquatics  Water Polo      PIJETLOVIC, Gojko     SRB   
      29514  2012   London  Aquatics  Water Polo    PRLAINOVIC, Andrija     SRB   
      29515  2012   London  Aquatics  Water Polo         RADJEN, Nikola     SRB   
      29516  2012   London  Aquatics  Water Polo       SAPONJIC, Aleksa     SRB   
      29517  2012   London  Aquatics  Water Polo         SORO, Slobodan     SRB   
      29518  2012   London  Aquatics  Water Polo        UDOVICIC, Vanja     SRB   
      30835  2012   London  Shooting    Shooting        ZLATIC, Andrija     SRB   
      
            Gender           Event   Medal  
      27225    Men  100M Butterfly  Silver  
      27443    Men      Water Polo  Bronze  
      27444    Men      Water Polo  Bronze  
      27445    Men      Water Polo  Bronze  
      27446    Men      Water Polo  Bronze  
      27447    Men      Water Polo  Bronze  
      27448    Men      Water Polo  Bronze  
      27449    Men      Water Polo  Bronze  
      27450    Men      Water Polo  Bronze  
      27451    Men      Water Polo  Bronze  
      27452    Men      Water Polo  Bronze  
      27453    Men      Water Polo  Bronze  
      27454    Men      Water Polo  Bronze  
      27455    Men      Water Polo  Bronze  
      29004    Men         Singles  Bronze  
      29506    Men      Water Polo  Bronze  
      29507    Men      Water Polo  Bronze  
      29508    Men      Water Polo  Bronze  
      29509    Men      Water Polo  Bronze  
      29510    Men      Water Polo  Bronze  
      29511    Men      Water Polo  Bronze  
      29512    Men      Water Polo  Bronze  
      29513    Men      Water Polo  Bronze  
      29514    Men      Water Polo  Bronze  
      29515    Men      Water Polo  Bronze  
      29516    Men      Water Polo  Bronze  
      29517    Men      Water Polo  Bronze  
      29518    Men      Water Polo  Bronze  
      30835    Men  10M Air Pistol  Bronze  ),
     (('SRB', 'Women'),
             Year    City      Sport Discipline            Athlete Country Gender  \
      30858  2012  London   Shooting   Shooting  MAKSIMOVIC, Ivana     SRB  Women   
      30910  2012  London  Taekwondo  Taekwondo     MANDIC, Milica     SRB  Women   
      
                             Event   Medal  
      30858  50M Rifle 3 Positions  Silver  
      30910                + 67 KG    Gold  ),
     (('SRI', 'Men'),
            Year    City      Sport Discipline        Athlete Country Gender  \
      7327  1948  London  Athletics  Athletics  WHITE, Duncan     SRI    Men   
      
                   Event   Medal  
      7327  400M Hurdles  Silver  ),
     (('SRI', 'Women'),
             Year    City      Sport Discipline                 Athlete Country  \
      23543  2000  Sydney  Athletics  Athletics  JAYASINGHE, Susanthika     SRI   
      
            Gender Event   Medal  
      23543  Women  200M  Silver  ),
     (('SUD', 'Men'),
             Year     City      Sport Discipline               Athlete Country  \
      27658  2008  Beijing  Athletics  Athletics  ISMAIL, Ismail Ahmed     SUD   
      
            Gender Event   Medal  
      27658    Men  800M  Silver  ),
     (('SUI', 'Men'),
             Year     City       Sport     Discipline              Athlete Country  \
      75     1896   Athens  Gymnastics    Artistic G.        ZUTTER, Louis     SUI   
      76     1896   Athens  Gymnastics    Artistic G.        ZUTTER, Louis     SUI   
      116    1896   Athens  Gymnastics    Artistic G.        ZUTTER, Louis     SUI   
      583    1900    Paris    Shooting       Shooting     LÜTHI, Friedrich     SUI   
      584    1900    Paris    Shooting       Shooting         PROBST, Paul     SUI   
      ...     ...      ...         ...            ...                  ...     ...   
      28994  2008  Beijing      Tennis         Tennis       FEDERER, Roger     SUI   
      28995  2008  Beijing      Tennis         Tennis  WAWRINKA, Stanislas     SUI   
      30076  2012   London     Cycling  Mountain Bike       SCHURTER, Nino     SUI   
      30111  2012   London  Equestrian        Jumping       GUERDAT, Steve     SUI   
      30953  2012   London      Tennis         Tennis       FEDERER, Roger     SUI   
      
            Gender                  Event   Medal  
      75       Men          Parallel Bars  Silver  
      76       Men           Pommel Horse    Gold  
      116      Men                  Vault  Silver  
      583      Men  50M Army Pistol, Team    Gold  
      584      Men  50M Army Pistol, Team    Gold  
      ...      ...                    ...     ...  
      28994    Men                Doubles    Gold  
      28995    Men                Doubles    Gold  
      30076    Men          Cross-Country  Silver  
      30111    Men             Individual    Gold  
      30953    Men                Singles  Silver  
      
      [353 rows x 9 columns]),
     (('SUI', 'Women'),
             Year         City          Sport       Discipline  \
      5289   1928    Amsterdam     Equestrian          Jumping   
      11122  1964        Tokyo     Equestrian         Dressage   
      12166  1968       Mexico     Equestrian         Dressage   
      14423  1976     Montreal     Equestrian         Dressage   
      14431  1976     Montreal     Equestrian         Dressage   
      14432  1976     Montreal     Equestrian         Dressage   
      17197  1984  Los Angeles     Equestrian         Dressage   
      17198  1984  Los Angeles     Equestrian         Dressage   
      17216  1984  Los Angeles     Equestrian          Jumping   
      18674  1988        Seoul     Equestrian         Dressage   
      18688  1988        Seoul     Equestrian         Dressage   
      22037  1996      Atlanta  Canoe / Kayak  Canoe / Kayak F   
      22038  1996      Atlanta  Canoe / Kayak  Canoe / Kayak F   
      22039  1996      Atlanta  Canoe / Kayak  Canoe / Kayak F   
      22040  1996      Atlanta  Canoe / Kayak  Canoe / Kayak F   
      24072  2000       Sydney        Cycling    Mountain Bike   
      24117  2000       Sydney     Equestrian          Jumping   
      24123  2000       Sydney        Fencing          Fencing   
      24141  2000       Sydney        Fencing          Fencing   
      24142  2000       Sydney        Fencing          Fencing   
      24143  2000       Sydney        Fencing          Fencing   
      24996  2000       Sydney      Triathlon        Triathlon   
      24997  2000       Sydney      Triathlon        Triathlon   
      26017  2004       Athens        Cycling     Cycling Road   
      28032  2008      Beijing        Cycling     Cycling Road   
      28130  2008      Beijing     Equestrian          Jumping   
      30961  2012       London      Triathlon        Triathlon   
      
                               Athlete Country Gender                  Event   Medal  
      5289                      PEPITA     SUI  Women             Individual  Bronze  
      11122       GOSSWEILER, Marianne     SUI  Women                   Team  Silver  
      12166       GOSSWEILER, Marianne     SUI  Women                   Team  Bronze  
      14423  STUECKELBERGER, Christine     SUI  Women             Individual    Gold  
      14431            RAMSEIER, Doris     SUI  Women                   Team  Silver  
      14432  STUECKELBERGER, Christine     SUI  Women                   Team  Silver  
      17197     DE BARY, Amy Catherine     SUI  Women                   Team  Silver  
      17198  STUECKELBERGER, Christine     SUI  Women                   Team  Silver  
      17216         ROBBIANI, Adelheid     SUI  Women             Individual  Bronze  
      18674  STUECKELBERGER, Christine     SUI  Women             Individual  Bronze  
      18688  STUECKELBERGER, Christine     SUI  Women                   Team  Silver  
      22037            BAUMER, Daniela     SUI  Women  K-4 500M (Kayak Four)  Silver  
      22038       EICHENBERGER, Sabine     SUI  Women  K-4 500M (Kayak Four)  Silver  
      22039          HARALAMOW, Ingrid     SUI  Women  K-4 500M (Kayak Four)  Silver  
      22040              MUELLER, Gabi     SUI  Women  K-4 500M (Kayak Four)  Silver  
      24072           BLATTER, Barbara     SUI  Women          Cross-Country  Silver  
      24117           MCNAUGHT, Lesley     SUI  Women                   Team  Silver  
      24123             BUERKI, Gianna     SUI  Women        Épée Individual  Silver  
      24141             BUERKI, Gianna     SUI  Women              Épée Team  Silver  
      24142              LAMON, Sophie     SUI  Women              Épée Team  Silver  
      24143           ROMAGNOLI, Diana     SUI  Women              Épée Team  Silver  
      24996            MESSMER, Magali     SUI  Women             Individual  Bronze  
      24997          MCMAHON, Brigitte     SUI  Women             Individual    Gold  
      26017             THUERIG, Karin     SUI  Women  Individual Time Trial  Bronze  
      28032              THURIG, Karin     SUI  Women  Individual Time Trial  Bronze  
      28130        LIEBHERR, Christina     SUI  Women                   Team  Bronze  
      30961             SPIRIG, Nicola     SUI  Women             Individual    Gold  ),
     (('SUR', 'Men'),
             Year       City     Sport Discipline                Athlete Country  \
      18076  1988      Seoul  Aquatics   Swimming  NESTY, Anthony Conrad     SUR   
      19621  1992  Barcelona  Aquatics   Swimming  NESTY, Anthony Conrad     SUR   
      
            Gender           Event   Medal  
      18076    Men  100M Butterfly    Gold  
      19621    Men  100M Butterfly  Bronze  ),
     (('SVK', 'Men'),
             Year     City          Sport       Discipline               Athlete  \
      21977  1996  Atlanta  Canoe / Kayak  Canoe / Kayak F  KNAZOVICKY, Slavomir   
      22042  1996  Atlanta  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      22888  1996  Atlanta       Shooting         Shooting          GONCI, Jozef   
      23983  2000   Sydney  Canoe / Kayak  Canoe / Kayak S         MINCIK, Juraj   
      23985  2000   Sydney  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      23988  2000   Sydney  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Pavol   
      23989  2000   Sydney  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Peter   
      25969  2004   Athens  Canoe / Kayak  Canoe / Kayak F           BACA, Juraj   
      25970  2004   Athens  Canoe / Kayak  Canoe / Kayak F    RISZDORFER, Michal   
      25971  2004   Athens  Canoe / Kayak  Canoe / Kayak F   RISZDORFER, Richard   
      25972  2004   Athens  Canoe / Kayak  Canoe / Kayak F           VLCEK, Erik   
      25995  2004   Athens  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      25998  2004   Athens  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Pavol   
      25999  2004   Athens  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Peter   
      26603  2004   Athens           Judo             Judo          KRNAC, Jozef   
      26841  2004   Athens       Shooting         Shooting          GONCI, Jozef   
      27987  2008  Beijing  Canoe / Kayak  Canoe / Kayak F    RISZDORFER, Michal   
      27988  2008  Beijing  Canoe / Kayak  Canoe / Kayak F   RISZDORFER, Richard   
      27989  2008  Beijing  Canoe / Kayak  Canoe / Kayak F           TARR, Juraj   
      27990  2008  Beijing  Canoe / Kayak  Canoe / Kayak F           VLCEK, Erik   
      28004  2008  Beijing  Canoe / Kayak  Canoe / Kayak S      MARTIKAN, Michal   
      28008  2008  Beijing  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Pavol   
      28009  2008  Beijing  Canoe / Kayak  Canoe / Kayak S   HOCHSCHORNER, Peter   
      29185  2008  Beijing      Wrestling  Wrestling Free.       MUSULBES, David   
      29922  2012   London          Canoe     Canoe Slalom      MARTIKAN, Michal   
      29927  2012   London          Canoe     Canoe Slalom   HOCHSCHORNER, Pavol   
      29928  2012   London          Canoe     Canoe Slalom   HOCHSCHORNER, Peter   
      
            Country Gender                         Event   Medal  
      21977     SVK    Men       C-1 500M (Canoe Single)  Silver  
      22042     SVK    Men            C-1 (Canoe Single)    Gold  
      22888     SVK    Men    50M Rifle Prone (60 Shots)  Bronze  
      23983     SVK    Men            C-1 (Canoe Single)  Bronze  
      23985     SVK    Men            C-1 (Canoe Single)  Silver  
      23988     SVK    Men            C-2 (Canoe Double)    Gold  
      23989     SVK    Men            C-2 (Canoe Double)    Gold  
      25969     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25970     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25971     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25972     SVK    Men        K-4 1000M (Kayak Four)  Bronze  
      25995     SVK    Men            C-1 (Canoe Single)  Silver  
      25998     SVK    Men            C-2 (Canoe Double)    Gold  
      25999     SVK    Men            C-2 (Canoe Double)    Gold  
      26603     SVK    Men  60 - 66KG (Half-Lightweight)  Silver  
      26841     SVK    Men      10M Air Rifle (60 Shots)  Bronze  
      27987     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      27988     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      27989     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      27990     SVK    Men        K-4 1000M (Kayak Four)  Silver  
      28004     SVK    Men            C-1 (Canoe Single)    Gold  
      28008     SVK    Men            C-2 (Canoe Double)    Gold  
      28009     SVK    Men            C-2 (Canoe Double)    Gold  
      29185     SVK    Men                    96 - 120KG  Bronze  
      29922     SVK    Men                  C-1 (Single)  Bronze  
      29927     SVK    Men                  C-2 (Double)  Bronze  
      29928     SVK    Men                  C-2 (Double)  Bronze  ),
     (('SVK', 'Women'),
             Year     City          Sport       Discipline              Athlete  \
      23214  2000   Sydney       Aquatics         Swimming   MORAVCOVA, Martina   
      23248  2000   Sydney       Aquatics         Swimming   MORAVCOVA, Martina   
      26006  2004   Athens  Canoe / Kayak  Canoe / Kayak S       KALISKA, Elena   
      28016  2008  Beijing  Canoe / Kayak  Canoe / Kayak S       KALISKA, Elena   
      28890  2008  Beijing       Shooting         Shooting  STEFECEKOVA, Zuzana   
      30871  2012   London       Shooting         Shooting     BARTEKOVA, Danka   
      30876  2012   London       Shooting         Shooting  STEFECEKOVA, Zuzana   
      
            Country Gender               Event   Medal  
      23214     SVK  Women      100M Butterfly  Silver  
      23248     SVK  Women      200M Freestyle  Silver  
      26006     SVK  Women  K-1 (Kayak Single)    Gold  
      28016     SVK  Women  K-1 (Kayak Single)    Gold  
      28890     SVK  Women   Trap (75 Targets)  Silver  
      30871     SVK  Women               Skeet  Bronze  
      30876     SVK  Women                Trap  Silver  ),
     (('SWE', 'Men'),
             Year    City      Sport           Discipline             Athlete  \
      291    1900   Paris  Athletics            Athletics         FAST, Ernst   
      1133   1908  London   Aquatics               Diving    SPANGBERG, Arvid   
      1134   1908  London   Aquatics               Diving  JOHANSSON, Hjalmar   
      1135   1908  London   Aquatics               Diving     MALMSTRÖM, Karl   
      1143   1908  London   Aquatics             Swimming  JULIN, Harald S.A.   
      ...     ...     ...        ...                  ...                 ...   
      30827  2012  London    Sailing              Sailing       LÖÖF, Fredrik   
      30828  2012  London    Sailing              Sailing       SALMINEN, Max   
      30864  2012  London   Shooting             Shooting       DAHLBY, Hakan   
      31139  2012  London  Wrestling  Wrestling Freestyle        EUREN, Johan   
      31164  2012  London  Wrestling  Wrestling Freestyle      LIDBERG, Jimmy   
      
            Country Gender            Event   Medal  
      291       SWE    Men         Marathon  Bronze  
      1133      SWE    Men     10M Platform  Bronze  
      1134      SWE    Men     10M Platform    Gold  
      1135      SWE    Men     10M Platform  Silver  
      1143      SWE    Men   100M Freestyle  Bronze  
      ...       ...    ...              ...     ...  
      30827     SWE    Men             Star    Gold  
      30828     SWE    Men             Star    Gold  
      30864     SWE    Men  Double Trap 150  Silver  
      31139     SWE    Men        Wg 120 KG  Bronze  
      31164     SWE    Men         Wg 96 KG  Bronze  
      
      [953 rows x 9 columns]),
     (('SWE', 'Women'),
             Year       City       Sport    Discipline               Athlete  \
      1875   1908     London      Tennis        Tennis  ADLERSTRAHLE, Märtha   
      1941   1912  Stockholm    Aquatics        Diving      JOHANSSON, Greta   
      1942   1912  Stockholm    Aquatics        Diving         REGNELL, Lisa   
      2772   1912  Stockholm      Tennis        Tennis          FICK, Sigrid   
      2776   1912  Stockholm      Tennis        Tennis          FICK, Sigrid   
      ...     ...        ...         ...           ...                   ...   
      26784  2004     Athens     Sailing       Sailing   TORGERSSON, Therese   
      26785  2004     Athens     Sailing       Sailing   ZACHRISSON, Vendela   
      28028  2008    Beijing     Cycling  Cycling Road       JOHANSSON, Emma   
      30094  2012     London  Equestrian      Eventing       ALGOTSSON, Sara   
      30962  2012     London   Triathlon     Triathlon          NORDEN, Lisa   
      
            Country Gender                    Event   Medal  
      1875      SWE  Women           Singles Indoor  Bronze  
      1941      SWE  Women             10M Platform    Gold  
      1942      SWE  Women             10M Platform  Silver  
      2772      SWE  Women            Mixed Doubles  Silver  
      2776      SWE  Women     Mixed Doubles Indoor  Bronze  
      ...       ...    ...                      ...     ...  
      26784     SWE  Women  470 - Two Person Dinghy  Bronze  
      26785     SWE  Women  470 - Two Person Dinghy  Bronze  
      28028     SWE  Women     Individual Road Race  Silver  
      30094     SWE  Women               Individual  Silver  
      30962     SWE  Women               Individual  Silver  
      
      [91 rows x 9 columns]),
     (('SYR', 'Men'),
             Year         City      Sport       Discipline          Athlete Country  \
      18020  1984  Los Angeles  Wrestling  Wrestling Free.    ATIYEH, Josep     SYR   
      25920  2004       Athens     Boxing           Boxing  AL SHAMI, Naser     SYR   
      
            Gender                     Event   Medal  
      18020    Men  90 - 100KG (Heavyweight)  Silver  
      25920    Men   81 - 91KG (Heavyweight)  Bronze  ),
     (('SYR', 'Women'),
             Year     City      Sport Discipline        Athlete Country Gender  \
      21727  1996  Atlanta  Athletics  Athletics  SHOUAA, Ghada     SYR  Women   
      
                  Event Medal  
      21727  Heptathlon  Gold  ),
     (('TAN', 'Men'),
             Year    City      Sport Discipline            Athlete Country Gender  \
      15402  1980  Moscow  Athletics  Athletics      BAYI, Filbert     TAN    Men   
      15462  1980  Moscow  Athletics  Athletics  NYAMBUI, Suleiman     TAN    Men   
      
                          Event   Medal  
      15402  3000M Steeplechase  Silver  
      15462               5000M  Silver  ),
     (('TCH', 'Men'),
             Year       City          Sport       Discipline          Athlete  \
      3577   1920    Antwerp     Ice Hockey       Ice Hockey     DUSEK, Adolf   
      3578   1920    Antwerp     Ice Hockey       Ice Hockey  HARTMANN, Karel   
      3579   1920    Antwerp     Ice Hockey       Ice Hockey      LOOS, Vilém   
      3580   1920    Antwerp     Ice Hockey       Ice Hockey      PALOUS, Jan   
      3581   1920    Antwerp     Ice Hockey       Ice Hockey        PEKA, Jan   
      ...     ...        ...            ...              ...              ...   
      20307  1992  Barcelona  Canoe / Kayak  Canoe / Kayak S      ROHAN, Jiri   
      20308  1992  Barcelona  Canoe / Kayak  Canoe / Kayak S  SIMEK, Miroslav   
      20999  1992  Barcelona         Rowing           Rowing  CHALUPA, Vaclav   
      21084  1992  Barcelona       Shooting         Shooting  RACANSKY, Lubos   
      21091  1992  Barcelona       Shooting         Shooting   HRDLICKA, Petr   
      
            Country Gender                             Event   Medal  
      3577      TCH    Men                        Ice Hockey  Bronze  
      3578      TCH    Men                        Ice Hockey  Bronze  
      3579      TCH    Men                        Ice Hockey  Bronze  
      3580      TCH    Men                        Ice Hockey  Bronze  
      3581      TCH    Men                        Ice Hockey  Bronze  
      ...       ...    ...                               ...     ...  
      20307     TCH    Men                C-2 (Canoe Double)  Silver  
      20308     TCH    Men                C-2 (Canoe Double)  Silver  
      20999     TCH    Men                Single Sculls (1X)  Silver  
      21084     TCH    Men  50M Running Target (30+30 Shots)  Bronze  
      21091     TCH    Men                Trap (125 Targets)    Gold  
      
      [249 rows x 9 columns]),
     (('TCH', 'Women'),
             Year     City       Sport   Discipline              Athlete Country  \
      4041   1920  Antwerp      Tennis       Tennis     SKRBKOVA, Milada     TCH   
      6878   1936   Berlin  Gymnastics  Artistic G.  BAJEROVA, Jaroslava     TCH   
      6879   1936   Berlin  Gymnastics  Artistic G.     DEKANOVA, Vlasta     TCH   
      6880   1936   Berlin  Gymnastics  Artistic G.     DOBESOVA, Bozena     TCH   
      6881   1936   Berlin  Gymnastics  Artistic G.      FOLTOVA, Vlasta     TCH   
      ...     ...      ...         ...          ...                  ...     ...   
      16164  1980   Moscow      Hockey       Hockey      SYKOROVA, Marie     TCH   
      16165  1980   Moscow      Hockey       Hockey      URBANOVA, Marta     TCH   
      16166  1980   Moscow      Hockey       Hockey    VYMAZALOVA, Lenka     TCH   
      19425  1988    Seoul      Tennis       Tennis        NOVOTNA, Jana     TCH   
      19426  1988    Seoul      Tennis       Tennis       SUKOVA, Helena     TCH   
      
            Gender             Event   Medal  
      4041   Women     Mixed Doubles  Bronze  
      6878   Women  Team Competition  Silver  
      6879   Women  Team Competition  Silver  
      6880   Women  Team Competition  Silver  
      6881   Women  Team Competition  Silver  
      ...      ...               ...     ...  
      16164  Women            Hockey  Silver  
      16165  Women            Hockey  Silver  
      16166  Women            Hockey  Silver  
      19425  Women           Doubles  Silver  
      19426  Women           Doubles  Silver  
      
      [80 rows x 9 columns]),
     (('TGA', 'Men'),
             Year     City   Sport Discipline         Athlete Country Gender  \
      21931  1996  Atlanta  Boxing     Boxing  WOLFGRAM, Paea     TGA    Men   
      
                                  Event   Medal  
      21931  + 91KG (Super Heavyweight)  Silver  ),
     (('THA', 'Men'),
             Year         City   Sport Discipline                  Athlete Country  \
      14285  1976     Montreal  Boxing     Boxing         POOLTARAT, Payao     THA   
      17050  1984  Los Angeles  Boxing     Boxing        UMPONMAHA, Dhawee     THA   
      18525  1988        Seoul  Boxing     Boxing          MOOLSAN, Phajol     THA   
      20212  1992    Barcelona  Boxing     Boxing          CHENGLAI, Arkom     THA   
      21936  1996      Atlanta  Boxing     Boxing           KHADPO, Vichai     THA   
      21942  1996      Atlanta  Boxing     Boxing         KAMSING, Somluck     THA   
      23876  2000       Sydney  Boxing     Boxing            PONLID, Wijan     THA   
      23899  2000       Sydney  Boxing     Boxing     THONGBURAN, Pornchai     THA   
      25895  2004       Athens  Boxing     Boxing       PETCHKOOM, Worapoj     THA   
      25906  2004       Athens  Boxing     Boxing       BOONJUMNONG, Manus     THA   
      25913  2004       Athens  Boxing     Boxing  PRASATHINPHIMAI, Suriya     THA   
      27896  2008      Beijing  Boxing     Boxing        JONGJOHOR, Somjit     THA   
      27917  2008      Beijing  Boxing     Boxing       BOONJUMNONG, Manus     THA   
      29873  2012       London  Boxing     Boxing        PONGPRAYOON, Kaeo     THA   
      
            Gender                             Event   Medal  
      14285    Men          - 48KG (Light-Flyweight)  Bronze  
      17050    Men  60 - 63.5KG (Light-Welterweight)  Silver  
      18525    Men          51 - 54KG (Bantamweight)  Bronze  
      20212    Men        63.5 - 67KG (Welterweight)  Bronze  
      21936    Men          51 - 54KG (Bantamweight)  Bronze  
      21942    Men         54 - 57KG (Featherweight)    Gold  
      23876    Men             48 - 51KG (Flyweight)    Gold  
      23899    Men    67 - 71KG (Light-Middleweight)  Bronze  
      25895    Men          51 - 54KG (Bantamweight)  Silver  
      25906    Men                        60 - 64 KG    Gold  
      25913    Men                        69 - 75 KG  Bronze  
      27896    Men             48 - 51KG (Flyweight)    Gold  
      27917    Men                        60 - 64 KG  Silver  
      29873    Men                         46 - 49KG  Silver  ),
     (('THA', 'Women'),
             Year     City          Sport     Discipline  \
      25101  2000   Sydney  Weightlifting  Weightlifting   
      26946  2004   Athens      Taekwondo      Taekwondo   
      27087  2004   Athens  Weightlifting  Weightlifting   
      27091  2004   Athens  Weightlifting  Weightlifting   
      27093  2004   Athens  Weightlifting  Weightlifting   
      27109  2004   Athens  Weightlifting  Weightlifting   
      28963  2008  Beijing      Taekwondo      Taekwondo   
      29116  2008  Beijing  Weightlifting  Weightlifting   
      30904  2012   London      Taekwondo      Taekwondo   
      31067  2012   London  Weightlifting  Weightlifting   
      31068  2012   London  Weightlifting  Weightlifting   
      
                                       Athlete Country Gender    Event   Medal  
      25101                 SUTA, Khassaraporn     THA  Women     58KG  Bronze  
      26946              BOORAPOLCHAI, Yaowapa     THA  Women  - 49 KG  Bronze  
      27087                 WIRATTHAWORN, Aree     THA  Women     48KG  Bronze  
      27091                   POLSAK, Udomporn     THA  Women     53KG    Gold  
      27093                    KAMEAIM, Wandee     THA  Women     58KG  Bronze  
      27109                   THONGSUK, Pawina     THA  Women     75KG    Gold  
      28963                  PUEDPONG, Buttree     THA  Women  - 49 KG  Silver  
      29116  JAROENRATTANATARAKOON, Prapawadee     THA  Women     53KG    Gold  
      30904                  SONKHAM, Chanatip     THA  Women  - 49 KG  Bronze  
      31067                  SIRIKAEW, Pimsiri     THA  Women     58KG  Silver  
      31068                   GULNOI, Rattikan     THA  Women     58KG  Bronze  ),
     (('TJK', 'Men'),
             Year     City      Sport       Discipline             Athlete Country  \
      28622  2008  Beijing       Judo             Judo       BOQIEV, Rasul     TJK   
      29180  2008  Beijing  Wrestling  Wrestling Free.  ABDUSALOMOV, Yusup     TJK   
      
            Gender                    Event   Medal  
      28622    Men  66 - 73KG (Lightweight)  Bronze  
      29180    Men                74 - 84KG  Silver  ),
     (('TJK', 'Women'),
             Year    City   Sport Discipline            Athlete Country Gender  \
      29899  2012  London  Boxing     Boxing  CHORIEVA, Mavzuna     TJK  Women   
      
             Event   Medal  
      29899  60 KG  Bronze  ),
     (('TOG', 'Men'),
             Year     City          Sport       Discipline             Athlete  \
      28012  2008  Beijing  Canoe / Kayak  Canoe / Kayak S  BOUKPETI, Benjamin   
      
            Country Gender               Event   Medal  
      28012     TOG    Men  K-1 (Kayak Single)  Bronze  ),
     (('TPE', 'Men'),
             Year         City          Sport     Discipline             Athlete  \
      10006  1960         Rome      Athletics      Athletics   YANG, Chuan-Kwang   
      17973  1984  Los Angeles  Weightlifting  Weightlifting       TSAI, Wen-Yee   
      20091  1992    Barcelona       Baseball       Baseball  CHANG, Cheng-Hsien   
      20092  1992    Barcelona       Baseball       Baseball    CHANG, Wen-Chung   
      20093  1992    Barcelona       Baseball       Baseball    CHANG, Yaw-Teing   
      20094  1992    Barcelona       Baseball       Baseball      CHEN, Chi-Hsin   
      20095  1992    Barcelona       Baseball       Baseball      CHEN, Wei-Chen   
      20096  1992    Barcelona       Baseball       Baseball   CHIANG, Tai-Chuan   
      20097  1992    Barcelona       Baseball       Baseball     HUANG, Chung-Yi   
      20098  1992    Barcelona       Baseball       Baseball       HUANG, Wen-Po   
      20099  1992    Barcelona       Baseball       Baseball      JONG, Yeu-Jeng   
      20100  1992    Barcelona       Baseball       Baseball       KU, Kuo-Chian   
      20101  1992    Barcelona       Baseball       Baseball   KUO LEE, Chien-Fu   
      20102  1992    Barcelona       Baseball       Baseball   LIAO, Ming-Hsiung   
      20103  1992    Barcelona       Baseball       Baseball     LIN, Chao-Huang   
      20104  1992    Barcelona       Baseball       Baseball        LIN, Kun-Han   
      20105  1992    Barcelona       Baseball       Baseball       LO, Chen-Jung   
      20106  1992    Barcelona       Baseball       Baseball       LO, Kuo-Chong   
      20107  1992    Barcelona       Baseball       Baseball       PAI, Kun-Hong   
      20108  1992    Barcelona       Baseball       Baseball     TSAI, Ming-Hung   
      20109  1992    Barcelona       Baseball       Baseball    WANG, Kuang-Shih   
      20110  1992    Barcelona       Baseball       Baseball       WU, Shih-Hsih   
      24954  2000       Sydney      Taekwondo      Taekwondo  HUANG, Chih Hsiung   
      25520  2004       Athens        Archery        Archery      CHEN, Szu Yuan   
      25521  2004       Athens        Archery        Archery     LIU, Ming Huang   
      25522  2004       Athens        Archery        Archery    WANG, Cheng Pang   
      26950  2004       Athens      Taekwondo      Taekwondo         CHU, Mu Yen   
      26966  2004       Athens      Taekwondo      Taekwondo  HUANG, Chih Hsiung   
      28964  2008      Beijing      Taekwondo      Taekwondo         CHU, Mu-Yen   
      28984  2008      Beijing      Taekwondo      Taekwondo        SUNG, Yu-Chi   
      
            Country Gender                             Event   Medal  
      10006     TPE    Men                         Decathlon  Silver  
      17973     TPE    Men  56 - 60KG, Total (Featherweight)  Bronze  
      20091     TPE    Men                          Baseball  Silver  
      20092     TPE    Men                          Baseball  Silver  
      20093     TPE    Men                          Baseball  Silver  
      20094     TPE    Men                          Baseball  Silver  
      20095     TPE    Men                          Baseball  Silver  
      20096     TPE    Men                          Baseball  Silver  
      20097     TPE    Men                          Baseball  Silver  
      20098     TPE    Men                          Baseball  Silver  
      20099     TPE    Men                          Baseball  Silver  
      20100     TPE    Men                          Baseball  Silver  
      20101     TPE    Men                          Baseball  Silver  
      20102     TPE    Men                          Baseball  Silver  
      20103     TPE    Men                          Baseball  Silver  
      20104     TPE    Men                          Baseball  Silver  
      20105     TPE    Men                          Baseball  Silver  
      20106     TPE    Men                          Baseball  Silver  
      20107     TPE    Men                          Baseball  Silver  
      20108     TPE    Men                          Baseball  Silver  
      20109     TPE    Men                          Baseball  Silver  
      20110     TPE    Men                          Baseball  Silver  
      24954     TPE    Men                           - 58 KG  Bronze  
      25520     TPE    Men   Team (Fita Olympic Round - 70M)  Silver  
      25521     TPE    Men   Team (Fita Olympic Round - 70M)  Silver  
      25522     TPE    Men   Team (Fita Olympic Round - 70M)  Silver  
      26950     TPE    Men                           - 58 KG    Gold  
      26966     TPE    Men                        58 - 68 KG  Silver  
      28964     TPE    Men                           - 58 KG  Bronze  
      28984     TPE    Men                        58 - 68 KG  Bronze  ),
     (('TPE', 'Women'),
             Year     City          Sport     Discipline          Athlete Country  \
      11945  1968   Mexico      Athletics      Athletics       CHI, Cheng     TPE   
      22968  1996  Atlanta   Table Tennis   Table Tennis       CHEN, Jing     TPE   
      24948  2000   Sydney   Table Tennis   Table Tennis       CHEN, Jing     TPE   
      24951  2000   Sydney      Taekwondo      Taekwondo      CHI, Shu-Ju     TPE   
      25097  2000   Sydney  Weightlifting  Weightlifting    LI, Feng-Ying     TPE   
      25116  2000   Sydney  Weightlifting  Weightlifting     KUO, Yi-Hang     TPE   
      25523  2004   Athens        Archery        Archery      CHEN, Li Ju     TPE   
      25524  2004   Athens        Archery        Archery       WU, Hui Ju     TPE   
      25525  2004   Athens        Archery        Archery    YUAN, Shu Chi     TPE   
      26947  2004   Athens      Taekwondo      Taekwondo  CHEN, Shih Hsin     TPE   
      29112  2008  Beijing  Weightlifting  Weightlifting   CHEN, Wei-Ling     TPE   
      29124  2008  Beijing  Weightlifting  Weightlifting     LU, Ying-Chi     TPE   
      30921  2012   London      Taekwondo      Taekwondo  TSENG, Li-Cheng     TPE   
      31060  2012   London  Weightlifting  Weightlifting   HSU, Shu-Ching     TPE   
      
            Gender                            Event   Medal  
      11945  Women                      80M Hurdles  Bronze  
      22968  Women                          Singles  Silver  
      24948  Women                          Singles  Bronze  
      24951  Women                          - 49 KG  Bronze  
      25097  Women                             53KG  Silver  
      25116  Women                             75KG  Bronze  
      25523  Women  Team (Fita Olympic Round - 70M)  Bronze  
      25524  Women  Team (Fita Olympic Round - 70M)  Bronze  
      25525  Women  Team (Fita Olympic Round - 70M)  Bronze  
      26947  Women                          - 49 KG    Gold  
      29112  Women                             48KG  Bronze  
      29124  Women                             63KG  Bronze  
      30921  Women                       49 - 57 KG  Bronze  
      31060  Women                             53KG    Gold  ),
     (('TRI', 'Men'),
             Year      City          Sport     Discipline                  Athlete  \
      7960   1948    London  Weightlifting  Weightlifting  WILKES, Rodney Adolphus   
      8844   1952  Helsinki  Weightlifting  Weightlifting  WILKES, Rodney Adolphus   
      8856   1952  Helsinki  Weightlifting  Weightlifting          KILGOUR, Lennox   
      10834  1964     Tokyo      Athletics      Athletics           ROBERTS, Edwin   
      10848  1964     Tokyo      Athletics      Athletics  MOTTLEY, Wendell Adrian   
      10879  1964     Tokyo      Athletics      Athletics       BERNARD, Kent Bede   
      10880  1964     Tokyo      Athletics      Athletics  MOTTLEY, Wendell Adrian   
      10881  1964     Tokyo      Athletics      Athletics           ROBERTS, Edwin   
      10882  1964     Tokyo      Athletics      Athletics           SKINNER, Edwin   
      14069  1976  Montreal      Athletics      Athletics         CRAWFORD, Hasely   
      21597  1996   Atlanta      Athletics      Athletics              BOLDON, Ato   
      21615  1996   Atlanta      Athletics      Athletics              BOLDON, Ato   
      23522  2000    Sydney      Athletics      Athletics              BOLDON, Ato   
      23538  2000    Sydney      Athletics      Athletics              BOLDON, Ato   
      25264  2004    Athens       Aquatics       Swimming           BOVELL, George   
      27553  2008   Beijing      Athletics      Athletics        THOMPSON, Richard   
      27607  2008   Beijing      Athletics      Athletics          BLEDMAN, Keston   
      27608  2008   Beijing      Athletics      Athletics              BURNS, Marc   
      27609  2008   Beijing      Athletics      Athletics      CALLENDER, Emmanuel   
      27610  2008   Beijing      Athletics      Athletics        THOMPSON, Richard   
      
            Country Gender                                    Event   Medal  
      7960      TRI    Men         56 - 60KG, Total (Featherweight)  Silver  
      8844      TRI    Men         56 - 60KG, Total (Featherweight)  Bronze  
      8856      TRI    Men  82.5 - 90KG, Total (Middle-Heavyweight)  Bronze  
      10834     TRI    Men                                     200M  Bronze  
      10848     TRI    Men                                     400M  Silver  
      10879     TRI    Men                             4X400M Relay  Bronze  
      10880     TRI    Men                             4X400M Relay  Bronze  
      10881     TRI    Men                             4X400M Relay  Bronze  
      10882     TRI    Men                             4X400M Relay  Bronze  
      14069     TRI    Men                                     100M    Gold  
      21597     TRI    Men                                     100M  Bronze  
      21615     TRI    Men                                     200M  Bronze  
      23522     TRI    Men                                     100M  Silver  
      23538     TRI    Men                                     200M  Bronze  
      25264     TRI    Men                   200M Individual Medley  Bronze  
      27553     TRI    Men                                     100M  Silver  
      27607     TRI    Men                             4X100M Relay  Silver  
      27608     TRI    Men                             4X100M Relay  Silver  
      27609     TRI    Men                             4X100M Relay  Silver  
      27610     TRI    Men                             4X100M Relay  Silver  ),
     (('TTO', 'Men'),
             Year    City      Sport Discipline              Athlete Country Gender  \
      29626  2012  London  Athletics  Athletics      GORDON, Lalonde     TTO    Men   
      29641  2012  London  Athletics  Athletics      BLEDMAN, Keston     TTO    Men   
      29642  2012  London  Athletics  Athletics          BURNS, Marc     TTO    Men   
      29643  2012  London  Athletics  Athletics  CALLENDER, Emmanuel     TTO    Men   
      29644  2012  London  Athletics  Athletics    THOMPSON, Richard     TTO    Men   
      29674  2012  London  Athletics  Athletics   ALLEYNE-FORTE, Ade     TTO    Men   
      29675  2012  London  Athletics  Athletics      GORDON, Lalonde     TTO    Men   
      29676  2012  London  Athletics  Athletics        LENDORE, Deon     TTO    Men   
      29677  2012  London  Athletics  Athletics      SOLOMON, Jarrin     TTO    Men   
      29736  2012  London  Athletics  Athletics     WALCOTT, Keshorn     TTO    Men   
      
                     Event   Medal  
      29626           400M  Bronze  
      29641   4X100M Relay  Silver  
      29642   4X100M Relay  Silver  
      29643   4X100M Relay  Silver  
      29644   4X100M Relay  Silver  
      29674   4X400M Relay  Bronze  
      29675   4X400M Relay  Bronze  
      29676   4X400M Relay  Bronze  
      29677   4X400M Relay  Bronze  
      29736  Javelin Throw    Gold  ),
     (('TUN', 'Men'),
             Year     City      Sport         Discipline            Athlete Country  \
      10821  1964    Tokyo  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      11011  1964    Tokyo     Boxing             Boxing      GALHIA, Habib     TUN   
      11861  1968   Mexico  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      11934  1968   Mexico  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      12990  1972   Munich  Athletics          Athletics  GAMMOUDI, Mohamed     TUN   
      21948  1996  Atlanta     Boxing             Boxing    MISSAOUI, Fathi     TUN   
      27237  2008  Beijing   Aquatics           Swimming  MELLOULI, Oussama     TUN   
      29252  2012   London   Aquatics  Marathon swimming  MELLOULI, Oussama     TUN   
      29284  2012   London   Aquatics           Swimming  MELLOULI, Oussama     TUN   
      
            Gender                             Event   Medal  
      10821    Men                            10000M  Silver  
      11011    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      11861    Men                            10000M  Bronze  
      11934    Men                             5000M    Gold  
      12990    Men                             5000M  Silver  
      21948    Men  60 - 63.5KG (Light-Welterweight)  Bronze  
      27237    Men                   1500M Freestyle    Gold  
      29252    Men                              10KM    Gold  
      29284    Men                   1500M Freestyle  Bronze  ),
     (('TUN', 'Women'),
             Year    City      Sport Discipline         Athlete Country Gender  \
      29621  2012  London  Athletics  Athletics  GHRIBI, Habiba     TUN  Women   
      
                     Event Medal  
      29621  3000M Steeple  Gold  ),
     (('TUR', 'Men'),
             Year     City      Sport           Discipline          Athlete Country  \
      7177   1936   Berlin  Wrestling      Wrestling Free.   KIREÇÇI, Ahmet     TUR   
      7190   1936   Berlin  Wrestling      Wrestling Gre-R     ERKAN, Yasar     TUR   
      7418   1948   London  Athletics            Athletics    SARIALP, Ruhi     TUR   
      7972   1948   London  Wrestling      Wrestling Free.   BALAMIR, Halit     TUR   
      7977   1948   London  Wrestling      Wrestling Free.      AKAR, Nazuh     TUR   
      ...     ...      ...        ...                  ...              ...     ...   
      28985  2008  Beijing  Taekwondo            Taekwondo  TAZEGUL, Servet     TUR   
      29167  2008  Beijing  Wrestling      Wrestling Free.   SAHIN, Ramazan     TUR   
      29205  2008  Beijing  Wrestling      Wrestling Gre-R    AVLUCA, Nazmi     TUR   
      30926  2012   London  Taekwondo            Taekwondo  TAZEGUL, Servet     TUR   
      31140  2012   London  Wrestling  Wrestling Freestyle    KAYAALP, Riza     TUR   
      
            Gender                      Event   Medal  
      7177     Men   72 - 79KG (Middleweight)  Bronze  
      7190     Men  56 - 61KG (Featherweight)    Gold  
      7418     Men                Triple Jump  Bronze  
      7972     Men         - 52KG (Flyweight)  Silver  
      7977     Men   52 - 57KG (Bantamweight)    Gold  
      ...      ...                        ...     ...  
      28985    Men                 58 - 68 KG  Bronze  
      29167    Men                  60 - 66KG    Gold  
      29205    Men                  74 - 84KG  Bronze  
      30926    Men                 58 - 68 KG    Gold  
      31140    Men                  Wg 120 KG  Bronze  
      
      [77 rows x 9 columns]),
     (('TUR', 'Women'),
             Year       City          Sport     Discipline             Athlete  \
      20780  1992  Barcelona           Judo           Judo      SENYURT, Hulya   
      24963  2000     Sydney      Taekwondo      Taekwondo      BIKCIN, Hamide   
      27088  2004     Athens  Weightlifting  Weightlifting      TAYLAN, Nurcan   
      27550  2008    Beijing      Athletics      Athletics  ABEYLEGESSE, Elvan   
      27652  2008    Beijing      Athletics      Athletics  ABEYLEGESSE, Elvan   
      28979  2008    Beijing      Taekwondo      Taekwondo    TANRIKULU, Azize   
      29114  2008    Beijing  Weightlifting  Weightlifting        OZKAN, Sibel   
      29604  2012     London      Athletics      Athletics        BULUT, Gamze   
      30923  2012     London      Taekwondo      Taekwondo          TATAR, Nur   
      
            Country Gender                       Event   Medal  
      20780     TUR  Women  - 48KG (Extra-Lightweight)  Bronze  
      24963     TUR  Women                  49 - 57 KG  Bronze  
      27088     TUR  Women                        48KG    Gold  
      27550     TUR  Women                      10000M  Silver  
      27652     TUR  Women                       5000M  Silver  
      28979     TUR  Women                  49 - 57 KG  Silver  
      29114     TUR  Women                        48KG  Silver  
      29604     TUR  Women                       1500M  Silver  
      30923     TUR  Women                  57 - 67 KG  Silver  ),
     (('UAE', 'Men'),
             Year    City     Sport Discipline                  Athlete Country  \
      26869  2004  Athens  Shooting   Shooting  ALMAKTOUM, Shaikh Ahmed     UAE   
      
            Gender                      Event Medal  
      26869    Men  Double Trap (150 Targets)  Gold  ),
     (('UGA', 'Men'),
             Year     City      Sport Discipline             Athlete Country Gender  \
      12041  1968   Mexico     Boxing     Boxing       RWABDOGO, Leo     UGA    Men   
      12047  1968   Mexico     Boxing     Boxing   MUKWANGA, Eridadi     UGA    Men   
      12938  1972   Munich  Athletics  Athletics      AKII-BUA, John     UGA    Men   
      13095  1972   Munich     Boxing     Boxing       RWABDOGO, Leo     UGA    Men   
      15623  1980   Moscow     Boxing     Boxing        MUGABI, John     UGA    Men   
      21627  1996  Atlanta  Athletics  Athletics       KAMOGA, Davis     UGA    Men   
      29748  2012   London  Athletics  Athletics  KIPROTICH, Stephen     UGA    Men   
      
                                  Event   Medal  
      12041       48 - 51KG (Flyweight)  Bronze  
      12047    51 - 54KG (Bantamweight)  Silver  
      12938                400M Hurdles    Gold  
      13095       48 - 51KG (Flyweight)  Silver  
      15623  63.5 - 67KG (Welterweight)  Silver  
      21627                        400M  Bronze  
      29748                    Marathon    Gold  ),
     (('UKR', 'Men'),
             Year     City          Sport           Discipline              Athlete  \
      21723  1996  Atlanta      Athletics            Athletics      KRYKUN, Oleksiy   
      21756  1996  Atlanta      Athletics            Athletics    BAGACH, Oleksandr   
      21924  1996  Atlanta         Boxing               Boxing      KIRYUKHIN, Oleg   
      21930  1996  Atlanta         Boxing               Boxing    KLICHKO, Vladimir   
      22339  1996  Atlanta     Gymnastics          Artistic G.    SHARIPOV, Roustam   
      ...     ...      ...            ...                  ...                  ...   
      29916  2012   London         Boxing               Boxing      USYK, Oleksandr   
      29938  2012   London          Canoe         Canoe Sprint        CHEBAN, Yuriy   
      30364  2012   London     Gymnastics  Gymnastics Artistic      RADIVILOV, Igor   
      31054  2012   London  Weightlifting        Weightlifting   TOROKHTIY, Oleksiy   
      31134  2012   London      Wrestling  Wrestling Freestyle  ANDRIITSEV, Valerii   
      
            Country Gender                       Event   Medal  
      21723     UKR    Men                Hammer Throw  Bronze  
      21756     UKR    Men                    Shot Put  Bronze  
      21924     UKR    Men    - 48KG (Light-Flyweight)  Bronze  
      21930     UKR    Men  + 91KG (Super Heavyweight)    Gold  
      22339     UKR    Men               Parallel Bars    Gold  
      ...       ...    ...                         ...     ...  
      29916     UKR    Men                   81 - 91KG    Gold  
      29938     UKR    Men                    C-1 200M    Gold  
      30364     UKR    Men                       Vault  Bronze  
      31054     UKR    Men                       105KG    Gold  
      31134     UKR    Men                    Wf 96 KG  Silver  
      
      [84 rows x 9 columns]),
     (('UKR', 'Women'),
             Year     City          Sport     Discipline                 Athlete  \
      21567  1996  Atlanta        Archery        Archery       SADOVNYCHA, Olena   
      21732  1996  Atlanta      Athletics      Athletics          BABAKOVA, Inha   
      21766  1996  Atlanta      Athletics      Athletics         KRAVETS, Inessa   
      22319  1996  Atlanta     Gymnastics    Artistic G.      PODKOPAYEVA, Lilia   
      22324  1996  Atlanta     Gymnastics    Artistic G.      PODKOPAYEVA, Lilia   
      ...     ...      ...            ...            ...                     ...   
      30769  2012   London         Rowing         Rowing  KOZHENKOVA, Anastasiia   
      30770  2012   London         Rowing         Rowing     TARASENKO, Kateryna   
      30838  2012   London       Shooting       Shooting        KOSTEVYCH, Olena   
      30847  2012   London       Shooting       Shooting        KOSTEVYCH, Olena   
      31062  2012   London  Weightlifting  Weightlifting         PARATOVA, Iulia   
      
            Country Gender                                  Event   Medal  
      21567     UKR  Women  Individual (Fita Olympic Round - 70M)  Bronze  
      21732     UKR  Women                              High Jump  Bronze  
      21766     UKR  Women                            Triple Jump    Gold  
      22319     UKR  Women                           Balance Beam  Silver  
      22324     UKR  Women                        Floor Exercises    Gold  
      ...       ...    ...                                    ...     ...  
      30769     UKR  Women                       Quadruple Sculls    Gold  
      30770     UKR  Women                       Quadruple Sculls    Gold  
      30838     UKR  Women                         10M Air Pistol  Bronze  
      30847     UKR  Women                             25M Pistol  Bronze  
      31062     UKR  Women                                   53KG  Bronze  
      
      [89 rows x 9 columns]),
     (('URS', 'Men'),
             Year      City      Sport       Discipline               Athlete  \
      8114   1952  Helsinki  Athletics        Athletics  ANUFRIYEV, Aleksandr   
      8117   1952  Helsinki  Athletics        Athletics           JUNK, Bruno   
      8140   1952  Helsinki  Athletics        Athletics   KAZANTSEV, Vladimir   
      8146   1952  Helsinki  Athletics        Athletics          LITUEV, Yuri   
      8155   1952  Helsinki  Athletics        Athletics          KALYAEV, Lev   
      ...     ...       ...        ...              ...                   ...   
      19580  1988     Seoul  Wrestling  Wrestling Gre-R   MADZHIDOV, Kamandar   
      19583  1988     Seoul  Wrestling  Wrestling Gre-R   DJULFALAKIAN, Levon   
      19587  1988     Seoul  Wrestling  Wrestling Gre-R   TURLYKHANOV, Daulet   
      19589  1988     Seoul  Wrestling  Wrestling Gre-R  MAMIASHVILI, Mikhail   
      19591  1988     Seoul  Wrestling  Wrestling Gre-R       POPOV, Vladimir   
      
            Country Gender                          Event   Medal  
      8114      URS    Men                         10000M  Bronze  
      8117      URS    Men                    10000M Walk  Bronze  
      8140      URS    Men             3000M Steeplechase  Silver  
      8146      URS    Men                   400M Hurdles  Silver  
      8155      URS    Men                   4X100M Relay  Silver  
      ...       ...    ...                            ...     ...  
      19580     URS    Men      57 - 62KG (Featherweight)    Gold  
      19583     URS    Men        62 - 68KG (Lightweight)    Gold  
      19587     URS    Men       68 - 74KG (Welterweight)  Silver  
      19589     URS    Men       74 - 82KG (Middleweight)    Gold  
      19591     URS    Men  82 - 90KG (Light-Heavyweight)  Bronze  
      
      [1476 rows x 9 columns]),
     (('URS', 'Women'),
             Year      City       Sport  Discipline                         Athlete  \
      8135   1952  Helsinki   Athletics   Athletics  KHNYKINA-DVALISHVILI, Nadezhda   
      8194   1952  Helsinki   Athletics   Athletics            GOLUBNICHAYA, Mariya   
      8201   1952  Helsinki   Athletics   Athletics                  DUMBADZE, Nina   
      8202   1952  Helsinki   Athletics   Athletics     ROMASHKOVA-PONOMAREVA, Nina   
      8203   1952  Helsinki   Athletics   Athletics         BAGRYANTSEVA, Elizaveta   
      ...     ...       ...         ...         ...                             ...   
      19490  1988     Seoul  Volleyball  Volleyball              PARKHOMCHUK, Irina   
      19491  1988     Seoul  Volleyball  Volleyball                 SHKURNOVA, Olga   
      19492  1988     Seoul  Volleyball  Volleyball              SIDORENKO, Tatyana   
      19493  1988     Seoul  Volleyball  Volleyball                 SMIRNOVA, Irina   
      19494  1988     Seoul  Volleyball  Volleyball                  VOLKOVA, Elena   
      
            Country Gender         Event   Medal  
      8135      URS  Women          200M  Bronze  
      8194      URS  Women   80M Hurdles  Silver  
      8201      URS  Women  Discus Throw  Bronze  
      8202      URS  Women  Discus Throw    Gold  
      8203      URS  Women  Discus Throw  Silver  
      ...       ...    ...           ...     ...  
      19490     URS  Women    Volleyball    Gold  
      19491     URS  Women    Volleyball    Gold  
      19492     URS  Women    Volleyball    Gold  
      19493     URS  Women    Volleyball    Gold  
      19494     URS  Women    Volleyball    Gold  
      
      [573 rows x 9 columns]),
     (('URU', 'Men'),
             Year                   City       Sport     Discipline  \
      4542   1924                  Paris    Football       Football   
      4543   1924                  Paris    Football       Football   
      4544   1924                  Paris    Football       Football   
      4545   1924                  Paris    Football       Football   
      4546   1924                  Paris    Football       Football   
      ...     ...                    ...         ...            ...   
      9141   1956  Melbourne / Stockholm  Basketball     Basketball   
      9142   1956  Melbourne / Stockholm  Basketball     Basketball   
      9143   1956  Melbourne / Stockholm  Basketball     Basketball   
      10999  1964                  Tokyo      Boxing         Boxing   
      24042  2000                 Sydney     Cycling  Cycling Track   
      
                           Athlete Country Gender                     Event   Medal  
      4542           ANDRADE, José     URU    Men                  Football    Gold  
      4543           ARISPE, Pedro     URU    Men                  Football    Gold  
      4544             CASELLA, P.     URU    Men                  Football    Gold  
      4545              CEA, Pedro     URU    Men                  Football    Gold  
      4546           CHIAPPARA, L.     URU    Men                  Football    Gold  
      ...                      ...     ...    ...                       ...     ...  
      9141           MOGLIA, Oscar     URU    Men                Basketball  Bronze  
      9142        OLASCOAGA, Ariel     URU    Men                Basketball  Bronze  
      9143       SCARON, Milton A.     URU    Men                Basketball  Bronze  
      10999  RODRIGUEZ, Washington     URU    Men  51 - 54KG (Bantamweight)  Bronze  
      24042  WYNANTS, Milton Ariel     URU    Men               Points Race  Silver  
      
      [76 rows x 9 columns]),
     (('USA', 'Men'),
             Year    City      Sport           Discipline                   Athlete  \
      11     1896  Athens  Athletics            Athletics             LANE, Francis   
      13     1896  Athens  Athletics            Athletics             BURKE, Thomas   
      15     1896  Athens  Athletics            Athletics            CURTIS, Thomas   
      19     1896  Athens  Athletics            Athletics             BLAKE, Arthur   
      21     1896  Athens  Athletics            Athletics             BURKE, Thomas   
      ...     ...     ...        ...                  ...                       ...   
      30935  2012  London     Tennis               Tennis               BRYAN, Mike   
      30950  2012  London     Tennis               Tennis               BRYAN, Mike   
      31112  2012  London  Wrestling  Wrestling Freestyle            SCOTT, Coleman   
      31125  2012  London  Wrestling  Wrestling Freestyle  BURROUGHS, Jordan Ernest   
      31133  2012  London  Wrestling  Wrestling Freestyle     VARNER, Jacob Stephen   
      
            Country Gender          Event   Medal  
      11        USA    Men           100M  Bronze  
      13        USA    Men           100M    Gold  
      15        USA    Men   110M Hurdles    Gold  
      19        USA    Men          1500M  Silver  
      21        USA    Men           400M    Gold  
      ...       ...    ...            ...     ...  
      30935     USA    Men        Doubles    Gold  
      30950     USA    Men  Mixed Doubles  Bronze  
      31112     USA    Men       Wf 60 KG  Bronze  
      31125     USA    Men       Wf 74 KG    Gold  
      31133     USA    Men       Wf 96 KG    Gold  
      
      [3208 rows x 9 columns]),
     (('USA', 'Women'),
             Year      City       Sport           Discipline  \
      416    1900     Paris        Golf                 Golf   
      417    1900     Paris        Golf                 Golf   
      418    1900     Paris        Golf                 Golf   
      647    1900     Paris      Tennis               Tennis   
      709    1904  St Louis     Archery              Archery   
      ...     ...       ...         ...                  ...   
      31032  2012    London  Volleyball           Volleyball   
      31033  2012    London  Volleyball           Volleyball   
      31034  2012    London  Volleyball           Volleyball   
      31035  2012    London  Volleyball           Volleyball   
      31099  2012    London   Wrestling  Wrestling Freestyle   
      
                                   Athlete Country Gender  \
      416                     PRATT, Daria     USA  Women   
      417            ABBOTT, Margaret Ives     USA  Women   
      418                WHITTIER, Pauline     USA  Women   
      647                    JONES, Marion     USA  Women   
      709                  POLLOCK, Jessie     USA  Women   
      ...                              ...     ...    ...   
      31032              MIYASHIRO, Tamari     USA  Women   
      31033                SCOTT, Danielle     USA  Women   
      31034             THOMPSON, Courtney     USA  Women   
      31035                     TOM, Logan     USA  Women   
      31099  CHUN, Clarissa Kyoko Mei Ling     USA  Women   
      
                                               Event   Medal  
      416                                 Individual  Bronze  
      417                                 Individual    Gold  
      418                                 Individual  Silver  
      647                                    Singles  Bronze  
      709    Double Columbia Round (50Y - 40Y - 30Y)  Bronze  
      ...                                        ...     ...  
      31032                               Volleyball  Silver  
      31033                               Volleyball  Silver  
      31034                               Volleyball  Silver  
      31035                               Volleyball  Silver  
      31099                                 Wf 48 KG  Bronze  
      
      [1377 rows x 9 columns]),
     (('UZB', 'Men'),
             Year     City       Sport           Discipline  \
      21957  1996  Atlanta      Boxing               Boxing   
      22661  1996  Atlanta        Judo                 Judo   
      23870  2000   Sydney      Boxing               Boxing   
      23892  2000   Sydney      Boxing               Boxing   
      23907  2000   Sydney      Boxing               Boxing   
      25151  2000   Sydney   Wrestling      Wrestling Free.   
      25893  2004   Athens      Boxing               Boxing   
      25916  2004   Athens      Boxing               Boxing   
      27149  2004   Athens   Wrestling      Wrestling Free.   
      27151  2004   Athens   Wrestling      Wrestling Free.   
      27163  2004   Athens   Wrestling      Wrestling Gre-R   
      28322  2008  Beijing  Gymnastics          Artistic G.   
      28591  2008  Beijing        Judo                 Judo   
      28597  2008  Beijing        Judo                 Judo   
      29176  2008  Beijing   Wrestling      Wrestling Free.   
      29187  2008  Beijing   Wrestling      Wrestling Free.   
      29906  2012   London      Boxing               Boxing   
      30586  2012   London        Judo                 Judo   
      31093  2012   London   Wrestling  Wrestling Freestyle   
      
                                Athlete Country Gender  \
      21957            TULAGANOV, Karim     UZB    Men   
      22661           BAGDASAROV, Armen     UZB    Men   
      23870              SAIDOV, Rustam     UZB    Men   
      23892  ABDOOLLAYEV, Mahammatkodir     UZB    Men   
      23907            MIHAYLOV, Sergey     UZB    Men   
      25151             TAYMAZOV, Artur     UZB    Men   
      25893       SOOLTONOV, Bahodirjon     UZB    Men   
      25916          HAYDAROV, Utkirbek     UZB    Men   
      27149          IBRAGIMOV, Magomed     UZB    Men   
      27151             TAYMAZOV, Artur     UZB    Men   
      27163    DOKTURISHIVILI, Alexandr     UZB    Men   
      28322                FOKIN, Anton     UZB    Men   
      28591             SOBIROV, Rishod     UZB    Men   
      28597           TANGRIEV, Abdullo     UZB    Men   
      29176              TIGIEV, Soslan     UZB    Men   
      29187             TAYMAZOV, Artur     UZB    Men   
      29906                ATOEV, Abbos     UZB    Men   
      30586             SOBIROV, Rishod     UZB    Men   
      31093             TAYMAZOV, Artur     UZB    Men   
      
                                        Event   Medal  
      21957    67 - 71KG (Light-Middleweight)  Bronze  
      22661          81 - 90KG (Middleweight)  Silver  
      23870        + 91KG (Super Heavyweight)  Bronze  
      23892  60 - 63.5KG (Light-Welterweight)    Gold  
      23907     75 - 81KG (Light-Heavyweight)  Bronze  
      25151                        97 - 130KG  Silver  
      25893          51 - 54KG (Bantamweight)  Bronze  
      25916     75 - 81KG (Light-Heavyweight)  Bronze  
      27149                         84 - 96KG  Silver  
      27151                        96 - 120KG    Gold  
      27163                         66 - 74KG    Gold  
      28322                     Parallel Bars  Bronze  
      28591                           - 60 KG  Bronze  
      28597             + 100KG (Heavyweight)  Silver  
      29176                         66 - 74KG  Silver  
      29187                        96 - 120KG    Gold  
      29906                        69 - 75 KG  Bronze  
      30586                           - 60 KG  Bronze  
      31093                          Wf 120KG    Gold  ),
     (('UZB', 'Women'),
             Year     City       Sport  Discipline            Athlete Country  \
      28400  2008  Beijing  Gymnastics  Trampoline  KHILKO, Ekaterina     UZB   
      
            Gender       Event   Medal  
      28400  Women  Individual  Bronze  ),
     (('VEN', 'Men'),
             Year         City          Sport     Discipline  \
      8237   1952     Helsinki      Athletics      Athletics   
      10599  1960         Rome       Shooting       Shooting   
      12034  1968       Mexico         Boxing         Boxing   
      14315  1976     Montreal         Boxing         Boxing   
      15607  1980       Moscow         Boxing         Boxing   
      16643  1984  Los Angeles       Aquatics       Swimming   
      17023  1984  Los Angeles         Boxing         Boxing   
      17040  1984  Los Angeles         Boxing         Boxing   
      27096  2004       Athens  Weightlifting  Weightlifting   
      30126  2012       London        Fencing        Fencing   
      
                                  Athlete Country Gender  \
      8237              DEVONISH, Arnaldo     VEN    Men   
      10599  FORCELLA PELLICCIONI, Enrico     VEN    Men   
      12034          RODRIGUEZ, Francisco     VEN    Men   
      14315           GAMARRO, Pedro José     VEN    Men   
      15607        PINANGO, Bernardo Jose     VEN    Men   
      16643  VIDAL CASTRO, Rafael Antonio     VEN    Men   
      17023       BOLIVAR, Jose Marcelino     VEN    Men   
      17040           CATARI PERAZA, Omar     VEN    Men   
      27096            RUBIO, Israel Jose     VEN    Men   
      30126      LIMARDO GASCON, Ruben D.     VEN    Men   
      
                                  Event   Medal  
      8237                  Triple Jump  Bronze  
      10599  50M Rifle Prone (60 Shots)  Bronze  
      12034    - 48KG (Light-Flyweight)    Gold  
      14315  63.5 - 67KG (Welterweight)  Silver  
      15607    51 - 54KG (Bantamweight)  Silver  
      16643              200M Butterfly  Bronze  
      17023    - 48KG (Light-Flyweight)  Bronze  
      17040   54 - 57KG (Featherweight)  Bronze  
      27096                        62KG  Bronze  
      30126             Épée Individual    Gold  ),
     (('VEN', 'Women'),
             Year     City      Sport Discipline                  Athlete Country  \
      26952  2004   Athens  Taekwondo  Taekwondo         CARMONA, Adriana     VEN   
      28960  2008  Beijing  Taekwondo  Taekwondo  CONTRERAS RIVERO, Dalia     VEN   
      
            Gender    Event   Medal  
      26952  Women  + 67 KG  Bronze  
      28960  Women  - 49 KG  Bronze  ),
     (('VIE', 'Men'),
             Year     City          Sport     Discipline          Athlete Country  \
      29102  2008  Beijing  Weightlifting  Weightlifting  HOANG, Anh Tuan     VIE   
      
            Gender                         Event   Medal  
      29102    Men  - 56KG, Total (Bantamweight)  Silver  ),
     (('VIE', 'Women'),
             Year    City      Sport Discipline          Athlete Country Gender  \
      24965  2000  Sydney  Taekwondo  Taekwondo  TRAN, Hieu Ngan     VIE  Women   
      
                  Event   Medal  
      24965  49 - 57 KG  Silver  ),
     (('YUG', 'Men'),
             Year       City       Sport   Discipline           Athlete Country  \
      4587   1924      Paris  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      4590   1924      Paris  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      5415   1928  Amsterdam  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      5420   1928  Amsterdam  Gymnastics  Artistic G.   PRIMOZIC, Josip     YUG   
      5425   1928  Amsterdam  Gymnastics  Artistic G.     STUKELJ, Leon     YUG   
      ...     ...        ...         ...          ...               ...     ...   
      25030  2000     Sydney  Volleyball   Volleyball       MIJIC, Vasa     YUG   
      25031  2000     Sydney  Volleyball   Volleyball   MILJKOVIC, Ivan     YUG   
      25032  2000     Sydney  Volleyball   Volleyball  PETKOVIC, Veljko     YUG   
      25033  2000     Sydney  Volleyball   Volleyball    VUJEVIC, Goran     YUG   
      25034  2000     Sydney  Volleyball   Volleyball   VUSUROVIC, Igor     YUG   
      
            Gender                 Event   Medal  
      4587     Men        Horizontal Bar    Gold  
      4590     Men  Individual All-Round    Gold  
      5415     Men  Individual All-Round  Bronze  
      5420     Men         Parallel Bars  Silver  
      5425     Men                 Rings    Gold  
      ...      ...                   ...     ...  
      25030    Men            Volleyball    Gold  
      25031    Men            Volleyball    Gold  
      25032    Men            Volleyball    Gold  
      25033    Men            Volleyball    Gold  
      25034    Men            Volleyball    Gold  
      
      [373 rows x 9 columns]),
     (('YUG', 'Women'),
             Year     City         Sport    Discipline               Athlete  \
      11706  1968   Mexico      Aquatics      Swimming     BJEDOV, Djurdjica   
      11734  1968   Mexico      Aquatics      Swimming     BJEDOV, Djurdjica   
      15556  1980   Moscow    Basketball    Basketball  BECIRSPAHIC, Mersada   
      15557  1980   Moscow    Basketball    Basketball          BJEDOV, Mira   
      15558  1980   Moscow    Basketball    Basketball     DESPOTOVIC, Vesna   
      ...     ...      ...           ...           ...                   ...   
      19399  1988    Seoul  Table Tennis  Table Tennis     PERKUCIN, Gordana   
      19400  1988    Seoul  Table Tennis  Table Tennis           REED, Jasna   
      22867  1996  Atlanta      Shooting      Shooting    IVOSEV, Aleksandra   
      22883  1996  Atlanta      Shooting      Shooting    IVOSEV, Aleksandra   
      24839  2000   Sydney      Shooting      Shooting        SEKARIC, Jasna   
      
            Country Gender                               Event   Medal  
      11706     YUG  Women                   100M Breaststroke    Gold  
      11734     YUG  Women                   200M Breaststroke  Silver  
      15556     YUG  Women                          Basketball  Bronze  
      15557     YUG  Women                          Basketball  Bronze  
      15558     YUG  Women                          Basketball  Bronze  
      ...       ...    ...                                 ...     ...  
      19399     YUG  Women                             Doubles  Bronze  
      19400     YUG  Women                             Doubles  Bronze  
      22867     YUG  Women            10M Air Rifle (40 Shots)  Bronze  
      22883     YUG  Women  50M Rifle 3 Positions (3X20 Shots)    Gold  
      24839     YUG  Women           10M Air Pistol (40 Shots)  Silver  
      
      [62 rows x 9 columns]),
     (('ZAM', 'Men'),
             Year         City      Sport Discipline         Athlete Country Gender  \
      17024  1984  Los Angeles     Boxing     Boxing    MWILA, Keith     ZAM    Men   
      21635  1996      Atlanta  Athletics  Athletics  MATETE, Samuel     ZAM    Men   
      
                                Event   Medal  
      17024  - 48KG (Light-Flyweight)  Bronze  
      21635              400M Hurdles  Silver  ),
     (('ZIM', 'Women'),
             Year     City     Sport Discipline                   Athlete Country  \
      16135  1980   Moscow    Hockey     Hockey    BOXHALL, Arlene Nadine     ZIM   
      16136  1980   Moscow    Hockey     Hockey   CHASE, Elizabeth Muriel     ZIM   
      16137  1980   Moscow    Hockey     Hockey             CHICK, Sandra     ZIM   
      16138  1980   Moscow    Hockey     Hockey  COWLEY, Gillian Margaret     ZIM   
      16139  1980   Moscow    Hockey     Hockey     DAVIES, Patricia Joan     ZIM   
      16140  1980   Moscow    Hockey     Hockey            ENGLISH, Sarah     ZIM   
      16141  1980   Moscow    Hockey     Hockey      GEORGE, Maureen Jean     ZIM   
      16142  1980   Moscow    Hockey     Hockey   GRANT, Ann Marry Gwynne     ZIM   
      16143  1980   Moscow    Hockey     Hockey            HUGGETT, Susan     ZIM   
      16144  1980   Moscow    Hockey     Hockey   MCKILLOP, Patricia Jean     ZIM   
      16145  1980   Moscow    Hockey     Hockey     PHILLIPS, Brenda Joan     ZIM   
      16146  1980   Moscow    Hockey     Hockey       PRINSLOO, Christine     ZIM   
      16147  1980   Moscow    Hockey     Hockey          ROBERTSON, Sonia     ZIM   
      16148  1980   Moscow    Hockey     Hockey    STEWART, Anthea Doreen     ZIM   
      16149  1980   Moscow    Hockey     Hockey               VOLK, Helen     ZIM   
      16150  1980   Moscow    Hockey     Hockey    WATSON, Linda Margaret     ZIM   
      25217  2004   Athens  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      25244  2004   Athens  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      25267  2004   Athens  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27216  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27243  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27268  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      27280  2008  Beijing  Aquatics   Swimming          COVENTRY, Kirsty     ZIM   
      
            Gender                   Event   Medal  
      16135  Women                  Hockey    Gold  
      16136  Women                  Hockey    Gold  
      16137  Women                  Hockey    Gold  
      16138  Women                  Hockey    Gold  
      16139  Women                  Hockey    Gold  
      16140  Women                  Hockey    Gold  
      16141  Women                  Hockey    Gold  
      16142  Women                  Hockey    Gold  
      16143  Women                  Hockey    Gold  
      16144  Women                  Hockey    Gold  
      16145  Women                  Hockey    Gold  
      16146  Women                  Hockey    Gold  
      16147  Women                  Hockey    Gold  
      16148  Women                  Hockey    Gold  
      16149  Women                  Hockey    Gold  
      16150  Women                  Hockey    Gold  
      25217  Women         100M Backstroke  Silver  
      25244  Women         200M Backstroke    Gold  
      25267  Women  200M Individual Medley  Bronze  
      27216  Women         100M Backstroke  Silver  
      27243  Women         200M Backstroke    Gold  
      27268  Women  200M Individual Medley  Silver  
      27280  Women  400M Individual Medley  Silver  ),
     (('ZZX', 'Men'),
           Year      City       Sport  Discipline                           Athlete  \
      132  1896    Athens      Tennis      Tennis                      FLACK, Edwin   
      133  1896    Athens      Tennis      Tennis          ROBERTSON, George Stuart   
      134  1896    Athens      Tennis      Tennis                      BOLAND, John   
      135  1896    Athens      Tennis      Tennis                  TRAUN, Friedrich   
      136  1896    Athens      Tennis      Tennis              KASDAGLIS, Dionysios   
      137  1896    Athens      Tennis      Tennis          PETROKOKKINOS, Demetrios   
      257  1900     Paris   Athletics   Athletics                  BENNETT, Charles   
      258  1900     Paris   Athletics   Athletics                      RIMMER, John   
      259  1900     Paris   Athletics   Athletics                  ROBINSON, Sidney   
      260  1900     Paris   Athletics   Athletics                   ROWLEY, Stanley   
      261  1900     Paris   Athletics   Athletics                     TYSOE, Alfred   
      422  1900     Paris        Polo        Polo                     BOUSSOD, Jean   
      423  1900     Paris        Polo        Polo            DUC DE BISACCIA, Louis   
      424  1900     Paris        Polo        Polo              FAUQUET LEMAITRE, A.   
      425  1900     Paris        Polo        Polo              RAOUL-DUVAL, Maurice   
      426  1900     Paris        Polo        Polo                      DALY, Dennis   
      427  1900     Paris        Polo        Polo             KEENE, Foxhall Parker   
      428  1900     Paris        Polo        Polo                 MACKEY, Frank Jay   
      429  1900     Paris        Polo        Polo                 RAWLINSON, Alfred   
      430  1900     Paris        Polo        Polo          BUCKMASTER, Walter Selby   
      431  1900     Paris        Polo        Polo  COMTE DE MADRE, José Pierre M.J.   
      432  1900     Paris        Polo        Polo        FREAKE, Frederick Maitland   
      433  1900     Paris        Polo        Polo           MCCREERY, Walter Adolph   
      493  1900     Paris      Rowing      Rowing          BRANDT, Francois Antoine   
      494  1900     Paris      Rowing      Rowing      BROCKMANN, Hermanus Gerardus   
      495  1900     Paris      Rowing      Rowing                     KLEIN, Roelof   
      633  1900     Paris      Tennis      Tennis      DE GARMENDIA, Basil Spalding   
      634  1900     Paris      Tennis      Tennis                      DECUGIS, Max   
      635  1900     Paris      Tennis      Tennis            DOHERTY, Hugh Lawrence   
      636  1900     Paris      Tennis      Tennis              WARDEN, Archibald A.   
      638  1900     Paris      Tennis      Tennis          MAHONY, Harold Sergerson   
      651  1900     Paris  Tug of War  Tug of War                      AABYE, Edgar   
      652  1900     Paris  Tug of War  Tug of War                   NILSSON, August   
      653  1900     Paris  Tug of War  Tug of War                    SCHMIDT, Eugen   
      654  1900     Paris  Tug of War  Tug of War                SÖDERSTRÖM, Gustaf   
      655  1900     Paris  Tug of War  Tug of War                STAAF, Karl Gustav   
      656  1900     Paris  Tug of War  Tug of War                 WINCKLER, Charles   
      765  1904  St Louis   Athletics   Athletics                     CORAY, Albert   
      766  1904  St Louis   Athletics   Athletics                     HATCH, Sidney   
      767  1904  St Louis   Athletics   Athletics                      HEARN, Lacey   
      768  1904  St Louis   Athletics   Athletics                  LIGHTBODY, James   
      769  1904  St Louis   Athletics   Athletics             VERNER, William Frank   
      864  1904  St Louis     Fencing     Fencing                      DIAZ, Manuel   
      865  1904  St Louis     Fencing     Fencing                      FONST, Ramon   
      866  1904  St Louis     Fencing     Fencing            VAN ZO POST, Albertson   
      
          Country Gender                                Event   Medal  
      132     ZZX    Men                              Doubles  Bronze  
      133     ZZX    Men                              Doubles  Bronze  
      134     ZZX    Men                              Doubles    Gold  
      135     ZZX    Men                              Doubles    Gold  
      136     ZZX    Men                              Doubles  Silver  
      137     ZZX    Men                              Doubles  Silver  
      257     ZZX    Men                           5000M Team    Gold  
      258     ZZX    Men                           5000M Team    Gold  
      259     ZZX    Men                           5000M Team    Gold  
      260     ZZX    Men                           5000M Team    Gold  
      261     ZZX    Men                           5000M Team    Gold  
      422     ZZX    Men                                 Polo  Bronze  
      423     ZZX    Men                                 Polo  Bronze  
      424     ZZX    Men                                 Polo  Bronze  
      425     ZZX    Men                                 Polo  Bronze  
      426     ZZX    Men                                 Polo    Gold  
      427     ZZX    Men                                 Polo    Gold  
      428     ZZX    Men                                 Polo    Gold  
      429     ZZX    Men                                 Polo    Gold  
      430     ZZX    Men                                 Polo  Silver  
      431     ZZX    Men                                 Polo  Silver  
      432     ZZX    Men                                 Polo  Silver  
      433     ZZX    Men                                 Polo  Silver  
      493     ZZX    Men  Pair-Oared Shell With Coxswain (2+)    Gold  
      494     ZZX    Men  Pair-Oared Shell With Coxswain (2+)    Gold  
      495     ZZX    Men  Pair-Oared Shell With Coxswain (2+)    Gold  
      633     ZZX    Men                              Doubles  Silver  
      634     ZZX    Men                              Doubles  Silver  
      635     ZZX    Men                        Mixed Doubles  Bronze  
      636     ZZX    Men                        Mixed Doubles  Bronze  
      638     ZZX    Men                        Mixed Doubles  Silver  
      651     ZZX    Men                           Tug Of War    Gold  
      652     ZZX    Men                           Tug Of War    Gold  
      653     ZZX    Men                           Tug Of War    Gold  
      654     ZZX    Men                           Tug Of War    Gold  
      655     ZZX    Men                           Tug Of War    Gold  
      656     ZZX    Men                           Tug Of War    Gold  
      765     ZZX    Men                          4Miles Team  Silver  
      766     ZZX    Men                          4Miles Team  Silver  
      767     ZZX    Men                          4Miles Team  Silver  
      768     ZZX    Men                          4Miles Team  Silver  
      769     ZZX    Men                          4Miles Team  Silver  
      864     ZZX    Men                            Foil Team    Gold  
      865     ZZX    Men                            Foil Team    Gold  
      866     ZZX    Men                            Foil Team    Gold  ),
     (('ZZX', 'Women'),
           Year   City   Sport Discipline            Athlete Country Gender  \
      639  1900  Paris  Tennis     Tennis      JONES, Marion     ZZX  Women   
      640  1900  Paris  Tennis     Tennis  ROSENBAUM, Hedwig     ZZX  Women   
      642  1900  Paris  Tennis     Tennis    PREVOST, Hélène     ZZX  Women   
      
                   Event   Medal  
      639  Mixed Doubles  Bronze  
      640  Mixed Doubles  Bronze  
      642  Mixed Doubles  Silver  )]




```python
len(l2)
```




    236




```python
l2[104]
```


```python
l2[104][0]
```


```python
l2[104][1]
```


```python

```

### split-apply-combine explained


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv")
```


```python
titanic_slice = titanic.iloc[:10, [2,3]]
```


```python
titanic_slice
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>male</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>male</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>male</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>male</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>female</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>female</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
list(titanic_slice.groupby("sex"))[0][1]
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
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>female</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>female</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
list(titanic_slice.groupby("sex"))[1][1]
```


```python
titanic_slice.groupby("sex").mean()
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
      <th>age</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>28.00</td>
    </tr>
    <tr>
      <th>male</th>
      <td>28.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.groupby("sex").survived.sum()
```




    sex
    female    233
    male      109
    Name: survived, dtype: int64




```python
titanic.groupby("sex")[["fare", "age"]].max()
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
      <th>fare</th>
      <th>age</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>512.3292</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>male</th>
      <td>512.3292</td>
      <td>80.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
new_df = titanic.groupby("sex").mean()
```


```python
new_df
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
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
      <td>2.159236</td>
      <td>27.915709</td>
      <td>0.694268</td>
      <td>0.649682</td>
      <td>44.479818</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
      <td>2.389948</td>
      <td>30.726645</td>
      <td>0.429809</td>
      <td>0.235702</td>
      <td>25.523893</td>
    </tr>
  </tbody>
</table>
</div>




```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use("seaborn")
```


```python
new_df.plot(kind = "bar", subplots = True, figsize = (8,15), fontsize = 13)
plt.show()
```


    
![png](pandas_part2_files/pandas_part2_58_0.png)
    



```python

```

### split-apply-combine applied


```python
import pandas as pd
```


```python
summer = pd.read_csv("summer.csv")
```


```python
summer.head()
```


```python
summer.info()
```


```python
medals_per_country = summer.groupby("Country").Medal.count().nlargest(n = 20)
medals_per_country
```




    Country
    USA    4585
    URS    2049
    GBR    1720
    FRA    1396
    GER    1305
    ITA    1296
    AUS    1189
    HUN    1079
    SWE    1044
    NED     851
    GDR     825
    CHN     807
    JPN     788
    RUS     768
    CAN     649
    ROU     640
    NOR     554
    KOR     529
    POL     511
    DEN     507
    Name: Medal, dtype: int64




```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use("seaborn")
```


```python
medals_per_country.plot(kind = "bar", figsize = (14, 8), fontsize = 14)
plt.xlabel("Country", fontsize = 13)
plt.ylabel("No. of Medals", fontsize = 13)
plt.title("Summer Olympic Games (Total Medals per Country)", fontsize = 16)
plt.show()
```


    
![png](pandas_part2_files/pandas_part2_67_0.png)
    



```python
titanic = pd.read_csv("titanic.csv")
```


```python
titanic.head()
```


```python
titanic.info()
```


```python
titanic.describe()
```


```python
titanic.fare.mean()
```




    32.204207968574636




```python
titanic.groupby("pclass").fare.mean()
```




    pclass
    1    84.154687
    2    20.662183
    3    13.675550
    Name: fare, dtype: float64




```python
titanic.survived.sum()
```




    342




```python
titanic.survived.mean()
```




    0.3838383838383838




```python
titanic.groupby("sex").survived.mean()
```




    sex
    female    0.742038
    male      0.188908
    Name: survived, dtype: float64




```python
titanic.groupby("pclass").survived.mean()
```




    pclass
    1    0.629630
    2    0.472826
    3    0.242363
    Name: survived, dtype: float64




```python
titanic["ad_chi"] = "adult"
```


```python
titanic.loc[titanic.age < 18, "ad_chi"] = "child"
```


```python
titanic.head(20)
```


```python
titanic.ad_chi.value_counts()
```




    adult    778
    child    113
    Name: ad_chi, dtype: int64




```python
titanic.groupby("ad_chi").survived.mean()
```




    ad_chi
    adult    0.361183
    child    0.539823
    Name: survived, dtype: float64




```python
titanic.groupby(["sex", "ad_chi"]).survived.count()
```




    sex     ad_chi
    female  adult     259
            child      55
    male    adult     519
            child      58
    Name: survived, dtype: int64




```python
titanic.groupby(["sex", "ad_chi"]).survived.mean().sort_values(ascending = False)
```




    sex     ad_chi
    female  adult     0.752896
            child     0.690909
    male    child     0.396552
            adult     0.165703
    Name: survived, dtype: float64




```python
w_and_c_first = titanic.groupby(["sex", "ad_chi"]).survived.mean().sort_values(ascending = False)
```


```python
w_and_c_first.plot(kind = "bar", figsize = (14,8), fontsize = 14)
plt.xlabel("Groups", fontsize = 13)
plt.ylabel("Survival Rate", fontsize = 13)
plt.title("Titanic Survival Rate by Sex/Age-Groups", fontsize = 16)
plt.show()
```


    
![png](pandas_part2_files/pandas_part2_86_0.png)
    



```python

```

### Advanced Aggregation with agg()


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv", usecols = ["survived", "pclass", "sex", "age", "fare"])
```


```python
titanic.head()
```


```python
titanic.groupby("sex").mean()
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
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
      <td>2.159236</td>
      <td>27.915709</td>
      <td>44.479818</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
      <td>2.389948</td>
      <td>30.726645</td>
      <td>25.523893</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.groupby("sex").sum()
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
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>233</td>
      <td>678</td>
      <td>7286.00</td>
      <td>13966.6628</td>
    </tr>
    <tr>
      <th>male</th>
      <td>109</td>
      <td>1379</td>
      <td>13919.17</td>
      <td>14727.2865</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.groupby("sex").agg(["mean", "sum", "min", "max"])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">survived</th>
      <th colspan="4" halign="left">pclass</th>
      <th colspan="4" halign="left">age</th>
      <th colspan="4" halign="left">fare</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>sum</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>sum</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>sum</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>sum</th>
      <th>min</th>
      <th>max</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
      <td>233</td>
      <td>0</td>
      <td>1</td>
      <td>2.159236</td>
      <td>678</td>
      <td>1</td>
      <td>3</td>
      <td>27.915709</td>
      <td>7286.00</td>
      <td>0.75</td>
      <td>63.0</td>
      <td>44.479818</td>
      <td>13966.6628</td>
      <td>6.75</td>
      <td>512.3292</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
      <td>109</td>
      <td>0</td>
      <td>1</td>
      <td>2.389948</td>
      <td>1379</td>
      <td>1</td>
      <td>3</td>
      <td>30.726645</td>
      <td>13919.17</td>
      <td>0.42</td>
      <td>80.0</td>
      <td>25.523893</td>
      <td>14727.2865</td>
      <td>0.00</td>
      <td>512.3292</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.groupby("sex").agg({"survived": ["sum", "mean"], "pclass": "mean", "age": ["mean", "median"], "fare": "max"})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">survived</th>
      <th>pclass</th>
      <th colspan="2" halign="left">age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
      <th>mean</th>
      <th>mean</th>
      <th>mean</th>
      <th>median</th>
      <th>max</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>233</td>
      <td>0.742038</td>
      <td>2.159236</td>
      <td>27.915709</td>
      <td>27.0</td>
      <td>512.3292</td>
    </tr>
    <tr>
      <th>male</th>
      <td>109</td>
      <td>0.188908</td>
      <td>2.389948</td>
      <td>30.726645</td>
      <td>29.0</td>
      <td>512.3292</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

### GroupBy Aggregation with Relabeling (new in Version 0.25)


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv", usecols = ["survived", "pclass", "sex", "age", "fare"])
```


```python
titanic.head()
```


```python
titanic.groupby("sex").survived.mean()
```




    sex
    female    0.742038
    male      0.188908
    Name: survived, dtype: float64




```python
titanic.groupby("sex").agg(survival_rate = ("survived", "mean"))
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
      <th>survival_rate</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.groupby("sex").agg({"survived": ["sum", "mean"], "age": ["mean"]})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">survived</th>
      <th>age</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
      <th>mean</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>233</td>
      <td>0.742038</td>
      <td>27.915709</td>
    </tr>
    <tr>
      <th>male</th>
      <td>109</td>
      <td>0.188908</td>
      <td>30.726645</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.groupby("sex").agg(survived_total = ("survived", "sum"), 
                           survival_rate = ("survived", "mean"), mean_age = ("age", "mean"))
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
      <th>survived_total</th>
      <th>survival_rate</th>
      <th>mean_age</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>233</td>
      <td>0.742038</td>
      <td>27.915709</td>
    </tr>
    <tr>
      <th>male</th>
      <td>109</td>
      <td>0.188908</td>
      <td>30.726645</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

### Transformation with transform()


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv")
```


```python
titanic.head()
```


```python
titanic.groupby(["sex", "pclass"]).survived.transform("mean")
```




    0      0.135447
    1      0.968085
    2      0.500000
    3      0.968085
    4      0.135447
             ...   
    886    0.157407
    887    0.968085
    888    0.500000
    889    0.368852
    890    0.135447
    Name: survived, Length: 891, dtype: float64




```python
titanic["group_surv_rate"] = titanic.groupby(["sex", "pclass"]).survived.transform("mean")
```


```python
titanic.head()
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>deck</th>
      <th>group_surv_rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>NaN</td>
      <td>0.135447</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>C</td>
      <td>0.968085</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>NaN</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>C</td>
      <td>0.968085</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>NaN</td>
      <td>0.135447</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic["outliers"] = abs(titanic.survived-titanic.group_surv_rate)
```


```python
titanic[titanic.outliers > 0.85]
```


```python

```

### Replacing NA Values by group-specific Values


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv")
```


```python
titanic.head(20)
```


```python
titanic.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 9 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   survived  891 non-null    int64  
     1   pclass    891 non-null    int64  
     2   sex       891 non-null    object 
     3   age       714 non-null    float64
     4   sibsp     891 non-null    int64  
     5   parch     891 non-null    int64  
     6   fare      891 non-null    float64
     7   embarked  889 non-null    object 
     8   deck      203 non-null    object 
    dtypes: float64(2), int64(4), object(3)
    memory usage: 62.8+ KB
    


```python
mean_age = titanic.age.mean()
mean_age
```




    29.69911764705882




```python
titanic.age.fillna(mean_age)
```




    0      22.000000
    1      38.000000
    2      26.000000
    3      35.000000
    4      35.000000
             ...    
    886    27.000000
    887    19.000000
    888    29.699118
    889    26.000000
    890    32.000000
    Name: age, Length: 891, dtype: float64




```python
titanic.groupby(["sex", "pclass"]).age.mean()
```




    sex     pclass
    female  1         34.611765
            2         28.722973
            3         21.750000
    male    1         41.281386
            2         30.740707
            3         26.507589
    Name: age, dtype: float64




```python
titanic["group_mean_age"] = titanic.groupby(["sex", "pclass"]).age.transform("mean")
```


```python
titanic.head(20)
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>deck</th>
      <th>group_mean_age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>C</td>
      <td>34.611765</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>C</td>
      <td>34.611765</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>8.4583</td>
      <td>Q</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>1</td>
      <td>male</td>
      <td>54.0</td>
      <td>0</td>
      <td>0</td>
      <td>51.8625</td>
      <td>S</td>
      <td>E</td>
      <td>41.281386</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>2.0</td>
      <td>3</td>
      <td>1</td>
      <td>21.0750</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>27.0</td>
      <td>0</td>
      <td>2</td>
      <td>11.1333</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>2</td>
      <td>female</td>
      <td>14.0</td>
      <td>1</td>
      <td>0</td>
      <td>30.0708</td>
      <td>C</td>
      <td>NaN</td>
      <td>28.722973</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>4.0</td>
      <td>1</td>
      <td>1</td>
      <td>16.7000</td>
      <td>S</td>
      <td>G</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>58.0</td>
      <td>0</td>
      <td>0</td>
      <td>26.5500</td>
      <td>S</td>
      <td>C</td>
      <td>34.611765</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>20.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>39.0</td>
      <td>1</td>
      <td>5</td>
      <td>31.2750</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>14.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.8542</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1</td>
      <td>2</td>
      <td>female</td>
      <td>55.0</td>
      <td>0</td>
      <td>0</td>
      <td>16.0000</td>
      <td>S</td>
      <td>NaN</td>
      <td>28.722973</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>2.0</td>
      <td>4</td>
      <td>1</td>
      <td>29.1250</td>
      <td>Q</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1</td>
      <td>2</td>
      <td>male</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>13.0000</td>
      <td>S</td>
      <td>NaN</td>
      <td>30.740707</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>31.0</td>
      <td>1</td>
      <td>0</td>
      <td>18.0000</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>7.2250</td>
      <td>C</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.age.fillna(titanic.group_mean_age, inplace = True)
```


```python
titanic.head(20)
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>deck</th>
      <th>group_mean_age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.000000</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.000000</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>C</td>
      <td>34.611765</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.000000</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.000000</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>C</td>
      <td>34.611765</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.000000</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>26.507589</td>
      <td>0</td>
      <td>0</td>
      <td>8.4583</td>
      <td>Q</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>1</td>
      <td>male</td>
      <td>54.000000</td>
      <td>0</td>
      <td>0</td>
      <td>51.8625</td>
      <td>S</td>
      <td>E</td>
      <td>41.281386</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>2.000000</td>
      <td>3</td>
      <td>1</td>
      <td>21.0750</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>27.000000</td>
      <td>0</td>
      <td>2</td>
      <td>11.1333</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>2</td>
      <td>female</td>
      <td>14.000000</td>
      <td>1</td>
      <td>0</td>
      <td>30.0708</td>
      <td>C</td>
      <td>NaN</td>
      <td>28.722973</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>4.000000</td>
      <td>1</td>
      <td>1</td>
      <td>16.7000</td>
      <td>S</td>
      <td>G</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>58.000000</td>
      <td>0</td>
      <td>0</td>
      <td>26.5500</td>
      <td>S</td>
      <td>C</td>
      <td>34.611765</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>20.000000</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>39.000000</td>
      <td>1</td>
      <td>5</td>
      <td>31.2750</td>
      <td>S</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>14.000000</td>
      <td>0</td>
      <td>0</td>
      <td>7.8542</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1</td>
      <td>2</td>
      <td>female</td>
      <td>55.000000</td>
      <td>0</td>
      <td>0</td>
      <td>16.0000</td>
      <td>S</td>
      <td>NaN</td>
      <td>28.722973</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>2.000000</td>
      <td>4</td>
      <td>1</td>
      <td>29.1250</td>
      <td>Q</td>
      <td>NaN</td>
      <td>26.507589</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1</td>
      <td>2</td>
      <td>male</td>
      <td>30.740707</td>
      <td>0</td>
      <td>0</td>
      <td>13.0000</td>
      <td>S</td>
      <td>NaN</td>
      <td>30.740707</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>31.000000</td>
      <td>1</td>
      <td>0</td>
      <td>18.0000</td>
      <td>S</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>21.750000</td>
      <td>0</td>
      <td>0</td>
      <td>7.2250</td>
      <td>C</td>
      <td>NaN</td>
      <td>21.750000</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 10 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   survived        891 non-null    int64  
     1   pclass          891 non-null    int64  
     2   sex             891 non-null    object 
     3   age             891 non-null    float64
     4   sibsp           891 non-null    int64  
     5   parch           891 non-null    int64  
     6   fare            891 non-null    float64
     7   embarked        889 non-null    object 
     8   deck            203 non-null    object 
     9   group_mean_age  891 non-null    float64
    dtypes: float64(3), int64(4), object(3)
    memory usage: 69.7+ KB
    


```python

```

### Generalizing split-apply-combine with apply()


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv", usecols = ["survived", "pclass", "sex", "age", "fare"])
```


```python
titanic.head()
```


```python
titanic.groupby("sex").mean()
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
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
      <td>2.159236</td>
      <td>27.915709</td>
      <td>44.479818</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
      <td>2.389948</td>
      <td>30.726645</td>
      <td>25.523893</td>
    </tr>
  </tbody>
</table>
</div>




```python
female_group = list(titanic.groupby("sex"))[0][1]
female_group
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>71.2833</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>7.9250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>53.1000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>27.0</td>
      <td>11.1333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>2</td>
      <td>female</td>
      <td>14.0</td>
      <td>30.0708</td>
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
      <th>880</th>
      <td>1</td>
      <td>2</td>
      <td>female</td>
      <td>25.0</td>
      <td>26.0000</td>
    </tr>
    <tr>
      <th>882</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>22.0</td>
      <td>10.5167</td>
    </tr>
    <tr>
      <th>885</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>39.0</td>
      <td>29.1250</td>
    </tr>
    <tr>
      <th>887</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>19.0</td>
      <td>30.0000</td>
    </tr>
    <tr>
      <th>888</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>NaN</td>
      <td>23.4500</td>
    </tr>
  </tbody>
</table>
<p>314 rows × 5 columns</p>
</div>




```python
female_group.mean().astype("float")
```

    C:\Users\LENOVO\AppData\Local\Temp/ipykernel_19564/2434558135.py:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      female_group.mean().astype("float")
    




    survived     0.742038
    pclass       2.159236
    age         27.915709
    fare        44.479818
    dtype: float64




```python
def group_mean(group):
    return group.mean()
```


```python
group_mean(female_group)
```

    C:\Users\LENOVO\AppData\Local\Temp/ipykernel_19564/359042690.py:2: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      return group.mean()
    




    survived     0.742038
    pclass       2.159236
    age         27.915709
    fare        44.479818
    dtype: float64




```python
titanic.groupby("sex").apply(group_mean)
```

    C:\Users\LENOVO\AppData\Local\Temp/ipykernel_19564/359042690.py:2: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      return group.mean()
    




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
      <th>survived</th>
      <th>pclass</th>
      <th>age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
      <td>2.159236</td>
      <td>27.915709</td>
      <td>44.479818</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
      <td>2.389948</td>
      <td>30.726645</td>
      <td>25.523893</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic.nlargest(5, "age")
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>630</th>
      <td>1</td>
      <td>1</td>
      <td>male</td>
      <td>80.0</td>
      <td>30.0000</td>
    </tr>
    <tr>
      <th>851</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>74.0</td>
      <td>7.7750</td>
    </tr>
    <tr>
      <th>96</th>
      <td>0</td>
      <td>1</td>
      <td>male</td>
      <td>71.0</td>
      <td>34.6542</td>
    </tr>
    <tr>
      <th>493</th>
      <td>0</td>
      <td>1</td>
      <td>male</td>
      <td>71.0</td>
      <td>49.5042</td>
    </tr>
    <tr>
      <th>116</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>70.5</td>
      <td>7.7500</td>
    </tr>
  </tbody>
</table>
</div>




```python
def five_oldest_surv(group):
    return group[group.survived == 1].nlargest(5, "age")
```


```python
titanic.groupby("sex").apply(five_oldest_surv)
```


```python

```

### Hierarchical Indexing (MultiIndex) with Groupby


```python
import pandas as pd
```


```python
titanic = pd.read_csv("titanic.csv", usecols = ["survived", "pclass", "sex", "age", "fare"])
```


```python
titanic
```


```python
summary = titanic.groupby(["sex", "pclass"]).mean()
```


```python
summary
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
      <th>survived</th>
      <th>age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>sex</th>
      <th>pclass</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">female</th>
      <th>1</th>
      <td>0.968085</td>
      <td>34.611765</td>
      <td>106.125798</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.921053</td>
      <td>28.722973</td>
      <td>21.970121</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.500000</td>
      <td>21.750000</td>
      <td>16.118810</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">male</th>
      <th>1</th>
      <td>0.368852</td>
      <td>41.281386</td>
      <td>67.226127</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.157407</td>
      <td>30.740707</td>
      <td>19.741782</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.135447</td>
      <td>26.507589</td>
      <td>12.661633</td>
    </tr>
  </tbody>
</table>
</div>




```python
summary.index
```




    MultiIndex([('female', 1),
                ('female', 2),
                ('female', 3),
                (  'male', 1),
                (  'male', 2),
                (  'male', 3)],
               names=['sex', 'pclass'])




```python
summary.loc[("female", 2), :]
```




    survived     0.921053
    age         28.722973
    fare        21.970121
    Name: (female, 2), dtype: float64




```python
summary.loc[("female", 2), "age"]
```


```python
summary.swaplevel().sort_index()
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
      <th>survived</th>
      <th>age</th>
      <th>fare</th>
    </tr>
    <tr>
      <th>pclass</th>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">1</th>
      <th>female</th>
      <td>0.968085</td>
      <td>34.611765</td>
      <td>106.125798</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.368852</td>
      <td>41.281386</td>
      <td>67.226127</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th>female</th>
      <td>0.921053</td>
      <td>28.722973</td>
      <td>21.970121</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.157407</td>
      <td>30.740707</td>
      <td>19.741782</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">3</th>
      <th>female</th>
      <td>0.500000</td>
      <td>21.750000</td>
      <td>16.118810</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.135447</td>
      <td>26.507589</td>
      <td>12.661633</td>
    </tr>
  </tbody>
</table>
</div>




```python
summary.reset_index()
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
      <th>sex</th>
      <th>pclass</th>
      <th>survived</th>
      <th>age</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>1</td>
      <td>0.968085</td>
      <td>34.611765</td>
      <td>106.125798</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>2</td>
      <td>0.921053</td>
      <td>28.722973</td>
      <td>21.970121</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>3</td>
      <td>0.500000</td>
      <td>21.750000</td>
      <td>16.118810</td>
    </tr>
    <tr>
      <th>3</th>
      <td>male</td>
      <td>1</td>
      <td>0.368852</td>
      <td>41.281386</td>
      <td>67.226127</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>2</td>
      <td>0.157407</td>
      <td>30.740707</td>
      <td>19.741782</td>
    </tr>
    <tr>
      <th>5</th>
      <td>male</td>
      <td>3</td>
      <td>0.135447</td>
      <td>26.507589</td>
      <td>12.661633</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

### stack() and unstack()


```python
import pandas as pd
```


```python
summer = pd.read_csv("summer.csv")
```


```python
summer.head()
```


```python
medals_by_country = summer.groupby(["Country", "Medal"]).Medal.count()
```


```python
medals_by_country
```




    Country  Medal 
    AFG      Bronze     2
    AHO      Silver     1
    ALG      Bronze     8
             Gold       5
             Silver     2
                       ..
    ZIM      Gold      18
             Silver     4
    ZZX      Bronze    10
             Gold      23
             Silver    15
    Name: Medal, Length: 347, dtype: int64




```python
medals_by_country.loc[("USA", "Gold")]
```




    2235




```python
medals_by_country.shape
```




    (347,)




```python
medals_by_country.unstack(level = -1)
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
      <th>Medal</th>
      <th>Bronze</th>
      <th>Gold</th>
      <th>Silver</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AFG</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AHO</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>ALG</th>
      <td>8.0</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>ANZ</th>
      <td>5.0</td>
      <td>20.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>ARG</th>
      <td>91.0</td>
      <td>69.0</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>VIE</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>YUG</th>
      <td>118.0</td>
      <td>143.0</td>
      <td>174.0</td>
    </tr>
    <tr>
      <th>ZAM</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>ZIM</th>
      <td>1.0</td>
      <td>18.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>ZZX</th>
      <td>10.0</td>
      <td>23.0</td>
      <td>15.0</td>
    </tr>
  </tbody>
</table>
<p>147 rows × 3 columns</p>
</div>




```python
medals_by_country = medals_by_country.unstack(level = -1, fill_value= 0)
```


```python
medals_by_country.head()
```


```python
medals_by_country.shape
```




    (147, 3)




```python
medals_by_country = medals_by_country[["Gold", "Silver", "Bronze"]]
```


```python
medals_by_country.sort_values(by = ["Gold", "Silver", "Bronze"], ascending = [False, False, False], inplace = True)
```


```python
medals_by_country.head(10)
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
      <th>Medal</th>
      <th>Gold</th>
      <th>Silver</th>
      <th>Bronze</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>USA</th>
      <td>2235</td>
      <td>1252</td>
      <td>1098</td>
    </tr>
    <tr>
      <th>URS</th>
      <td>838</td>
      <td>627</td>
      <td>584</td>
    </tr>
    <tr>
      <th>GBR</th>
      <td>546</td>
      <td>621</td>
      <td>553</td>
    </tr>
    <tr>
      <th>ITA</th>
      <td>476</td>
      <td>416</td>
      <td>404</td>
    </tr>
    <tr>
      <th>GER</th>
      <td>452</td>
      <td>378</td>
      <td>475</td>
    </tr>
    <tr>
      <th>HUN</th>
      <td>412</td>
      <td>316</td>
      <td>351</td>
    </tr>
    <tr>
      <th>FRA</th>
      <td>408</td>
      <td>491</td>
      <td>497</td>
    </tr>
    <tr>
      <th>SWE</th>
      <td>349</td>
      <td>367</td>
      <td>328</td>
    </tr>
    <tr>
      <th>GDR</th>
      <td>329</td>
      <td>271</td>
      <td>225</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>312</td>
      <td>405</td>
      <td>472</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt
plt.style.use("seaborn")
```


```python
medals_by_country.head(10).plot(kind = "bar", figsize = (12,8), fontsize = 13)
plt.xlabel("Country", fontsize = 13)
plt.ylabel("Medals", fontsize = 13)
plt.title("Medals per Country", fontsize = 16)
plt.legend(fontsize = 15)
plt.show()
```


    
![png](pandas_part2_files/pandas_part2_172_0.png)
    



```python
medals_by_country.stack().unstack()
```




    Country  Medal 
    USA      Gold      2235
             Silver    1252
             Bronze    1098
    URS      Gold       838
             Silver     627
                       ... 
    NIG      Silver       0
             Bronze       1
    TOG      Gold         0
             Silver       0
             Bronze       1
    Length: 441, dtype: int64




```python

```
