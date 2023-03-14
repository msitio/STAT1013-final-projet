
<div class="cell markdown" id="LdJW_o4CQKkp">

# CUHK STAT1013 Project Assignment Part 1

</div>

<div class="cell markdown" id="GqevtWQ7RHCY">

## Dataset Background **Description**

The dataset describes details of various car models which comprise the
majority of automobiles that are for sale in the USA, with a focus on
the fuel economy (expressed in miles per gallon) of the cars.

**Github:**
<https://github.com/msitio/FuelEconomy/blob/main/vehicles.csv>

**Sample Size:** 46017 (Raw Dataset Total). 30256(Relevant Total (FWD
and RWD))

</div>

<div class="cell markdown" id="e84XN2PpSaFj">

## Hypothesis

1.  Idea and reasons for pursuing:

-   This project will examine the fuel efficiency of front wheel drive
    (FWD) cars, where power is delivered through front wheels, and rear
    wheel drive (RWD) cars, where power is delivered through the rear
    wheels. The fuel efficiency of FWDs are hypothesized to be greater
    than that of RWDs as car engines are usually located in the front,
    so FWDs are hypothesized to be more fuel efficient due to lower
    transmission losses. As fuel efficiency is of importance due to both
    economic and environmental reasons, analysing the factors that lead
    to greater fuel efficiency is worthwhile.

2.  Groups being compared:

-   The two groups being compared in this project are front wheel drive
    cars (FWD) and rear wheel drive cars (RWD)

3.  Response variable being measured

-   `comb08`. Combined miles per gallon.

4.  Response variable type

-   The response variable is a quantitative measure

5.  Prediction

-   Front wheel drives will have higher fuel efficiency measured in
    miles per gallon than rear wheel drives

6.  Data gathering

-   The data was obtained from the website fueleconomy.gov which is run
    by the American government body, the Environmental Protection Agency
    (EPA) which was responsible for the collection of the data. The raw
    data was then uploaded to github for use in the colab.

7.  Data collection with unlimited resources

-   As the fuel economy of a vehicle can be affected by many different
    factors such as weight, engine type, etc, these factors should be
    taken into consideration when comparing the fuel economy of vehicles
    (ie. only comparing cars with a similar weight).

-   If possible, it might be better to find other sources for fuel
    efficiency data such as from the car's manufacturer or government
    agencies in different countries as the miles per gallon values can
    vary depending on the method of measurement.

</div>

<div class="cell code" execution_count="3"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:560}"
id="yLRlSAVmQGoR" outputId="6ad5f83f-c58b-4549-e8c2-cb32d3d5e88f">

``` python
import pandas as pd
df = pd.read_csv('https://raw.githubusercontent.com/msitio/FuelEconomy/main/vehicles.csv')
df.head(5) 

```

**Groups Being Compared**

The two groups being compared are front wheel drive cars
(`['drive']=='Front-Wheel Drive']`) and rear wheel drive cars
(`['drive']=='Rear-Wheel Drive']`)

First five outputs for each group:

</div>

<div class="cell code" id="aJh8OM_pBkQA">

``` python
df[df['drive']=='Front-Wheel Drive'].head(5)
```

</div>

<div class="cell code" id="0kDXLK5lBkbf">

``` python
df[df['drive']=='Rear-Wheel Drive'].head(5)
```

</div>

<div class="cell code" execution_count="71" id="GnhFOHdUtn1_">


</div>

<div class="cell code" execution_count="84"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="MMxQIgjSuBIe" outputId="c3128840-a93a-436e-b645-e440fa1ab9c3">

``` python
#Finding mean MPG of each type of car.
print("MPG of Front Wheel Drives: ",df[df['drive']=='Front-Wheel Drive']['comb08'].mean())
print("MPG of Reart Wheel Drives: ",df[df['drive']=='Rear-Wheel Drive']['comb08'].mean())
```

<div class="output stream stdout">

    MPG of Front Wheel Drives:  25.16192790071574
    MPG of Reart Wheel Drives:  18.539096293338655

</div>

</div>

<div class="cell code" execution_count="87" id="eRUz_F8FDeOR">

``` python
#Creating a new dataset that only contains FWD and RWD cars, the only drive types relevant to our project
df2=df[df['drive'].isin(['Front-Wheel Drive' ,'Rear-Wheel Drive'])]
```

</div>

<div class="cell markdown" id="6zPfsN_cFYxu">

### Additional Data Info

Dataset has data on the majority of vehicles that are for sale in the
USA, with car models for as far back as 1984 to as recent as this year.

Dataset also contains copious amounts of data is not relevant to the
current inquiry, but that may be useful for further investigation. Data
provides weight classes (ie. midsize, compact, etc), Fuel types
(Regular, Premium, Dieseil, Electric, etc) and many others.

Data for 4 wheel drives and some other drive subtypes are provided but
do not make up most of the data as these vehicles are relatively
uncommon compared to FWDs and RWDs.

</div>

<div class="cell code" execution_count="89"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="LlpBMoeGIyIq" outputId="94b93485-eb5c-41d8-9776-fb4e4fb9ea55">

``` python
#Number of cars of each group in the dataset. Roughly equal numbers.
print("Number of Front Wheel Drives in Dataset: ",df[df['drive']=='Front-Wheel Drive']['comb08'].count())
print("Number of Reart Wheel Drives in Dataset: ",df[df['drive']=='Rear-Wheel Drive']['comb08'].count())
```

<div class="output stream stdout">

    Number of Front Wheel Drives in Dataset:  15229
    Number of Reart Wheel Drives in Dataset:  15027

</div>

</div>

<div class="cell code" execution_count="5"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:252}"
id="EbWiEKC44Wgo" outputId="b40bc5a8-1dae-48bb-c838-99eb4fab2805">

``` python
#Some Visualizations comparing the fuel efficiency of both groups (Warning! Very slow due to the amount of data)
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(12,8)) 
sns.violinplot(x='drive', y='comb08', data=df)
sns.swarmplot(x='drive', y='comb08', data=df) 
          

```

</div>

<div class="cell code" execution_count="93"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="ed_5XJzuKc6B" outputId="6870f29b-b0af-40af-92ab-586d6a28802b">

``` python
#Basic description of the relevant data

print(df[df['drive']=='Front-Wheel Drive']['comb08'].describe())

print(df[df['drive']=='Rear-Wheel Drive']['comb08'].describe())
```

<div class="output stream stdout">

    count    15229.000000
    mean        25.161928
    std          9.000039
    min         14.000000
    25%         21.000000
    50%         24.000000
    75%         27.000000
    max        136.000000
    Name: comb08, dtype: float64
    count    15027.000000
    mean        18.539096
    std          8.281821
    min          7.000000
    25%         15.000000
    50%         18.000000
    75%         20.000000
    max        142.000000
    Name: comb08, dtype: float64

</div>

</div>
