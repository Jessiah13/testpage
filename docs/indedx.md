```python
# import libraries needed: 

# Automation
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Web Scraping
from bs4 import BeautifulSoup

# Pandas
import pandas as pd
import numpy as np

# Ploting
import matplotlib.pyplot as plt
import seaborn as sns

```


```python
# setup the webDriver: 
driver = webdriver.Chrome()

# Open the Webpage: 
url = 'https://www.ttps.gov.tt/Stats/Crime-Totals-By-Month'
driver.get(url)

# wait for the page to load: 
time.sleep(2)
```


```python
# get the element that contains all of the divisions data
division_td_elements = driver.find_elements(By.XPATH, "//table[@id='dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox1_DDD_L_LBT']//tbody//tr//td")

#Loop through all the divisons and place them in a list: 
divisions = []
for td  in division_td_elements:
    division_item = td.get_attribute("id")
    divisions.append(division_item)
# delete the firt item in the list as it has an 'All' value that we do not want
del divisions[0]


# get the element that contains all of the offences data
offence_td_elements = driver.find_elements(By.XPATH, "//table[@id='dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBT']//tbody//tr//td")

# Loop Through all of the offences and place them in a list" 
offences = []
for offence in offence_td_elements:
    offence_item = offence.get_attribute("id")
    offences.append(offence_item)
    print(offence_item)
# delete the firt item in the list as it has an 'All' value that we do not want
del offences[0]


# get the element that contains all of the years data
year_td_elements = driver.find_elements(By.XPATH, "//table[@id='dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBT']//tbody//tr//td")

years = []
for year_td  in year_td_elements:
    year_item = year_td.get_attribute("id")
    years.append(year_item)
    print(year_item)


# get the element that contains all of the years data
type_td_elements = driver.find_elements(By.XPATH, "//table[@id='dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox4_DDD_L_LBT']//tbody//tr//td")

types = []
for type_td  in type_td_elements:
    type_item = type_td.get_attribute("id")
    types.append(type_item)
    print(type_item)
```

    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI0T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI1T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI2T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI3T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI4T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI5T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI6T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI7T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI8T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI9T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI10T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI11T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI12T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI13T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI14T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_DDD_L_LBI15T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI0T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI1T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI2T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI3T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI4T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI5T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI6T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI7T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI8T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI9T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI10T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_DDD_L_LBI11T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox4_DDD_L_LBI0T0
    dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox4_DDD_L_LBI1T0
    


```python
# Locate and select the table tab to display tabular data: 
table = driver.find_element(By.ID, 'dnn_ctr453_TTPSCrimeMonthTotals_ASPxPageControl1_T1T')
ActionChains(driver).move_to_element(table).click(table).perform() 
```


```python
table_info = []

# Now we try to loop through each division, for each offence, for each year, for each type

for division in divisions: 
    #Locate and Select Division: 
    division_dropdown = driver.find_element(By.ID, "dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox1_I")
    ActionChains(driver).move_to_element(division_dropdown).click(division_dropdown).perform()
    time.sleep(2)
    #Find and Select the desired division: 
    division_select = driver.find_element(By.ID, division)
    # extract the text from the element
    division_text = division_select.text
    time.sleep(2)
    ActionChains(driver).move_to_element(division_select).click(division_select).perform()
    time.sleep(2)

    for offence_list_item in offences: 
        # locate and select the offence dropdown:
        offence_dropdown = driver.find_element(By.ID, "dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox2_B-1")
        ActionChains(driver).move_to_element(offence_dropdown).click(offence_dropdown).perform()
        time.sleep(2)
        
        offence_select = driver.find_element(By.ID, f"{offence_list_item}")
        # extract the text from the element
        offence_text = offence_select.text
        time.sleep(2)
        ActionChains(driver).move_to_element(offence_select).click(offence_select).perform()
        time.sleep(2)

        for year_list_item in years: 
            # locate and select the offence dropdown:
            year_dropdown = driver.find_element(By.ID, "dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox3_B-1")
            time.sleep(2)
            ActionChains(driver).move_to_element(year_dropdown).click(year_dropdown).perform()
            time.sleep(2)
                
            year_select = driver.find_element(By.ID, f"{year_list_item}")
            # extract the text from the element
            year_text = year_select.text
            time.sleep(2)
            ActionChains(driver).move_to_element(year_select).click(year_select).perform()
            time.sleep(2)

            
            for type_list_item in types: 
                # locate and select the offence dropdown:
                type_dropdown = driver.find_element(By.ID, "dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxComboBox4_B-1")
                time.sleep(2)
                ActionChains(driver).move_to_element(year_dropdown).click(type_dropdown).perform()
                time.sleep(2)
                                
                type_select = driver.find_element(By.ID, type_list_item)
                # extract the text from the element
                type_text = type_select.text
                time.sleep(2)
                ActionChains(driver).move_to_element(type_select).click(type_select).perform()
                time.sleep(2)

                # find the generate report button: 
                generate = driver.find_element(By.ID, 'dnn_ctr453_TTPSCrimeMonthTotals_ASPxRoundPanel1_ASPxButton1_CD')
                # select generate report: 
                ActionChains(driver).move_to_element(generate).click(generate).perform()
                time.sleep(3)



################### HERE WE ARE SWITCIHING FROM SELENIUM TO BS4 ###########################


              # get the page source: 
                page_source = driver.page_source
                # parse with bs4
                soup = BeautifulSoup(page_source, 'html.parser')
                
                # get the table location: 
                page_table = soup.find('table', id='dnn_ctr453_TTPSCrimeMonthTotals_ASPxPageControl1_ASPxGridView1_DXMainTable')
                # there is no tagged table headers so we will skip this step and create our own headers later.
                
                # get the table rows: 
                rows = page_table.find_all('tr')#[3:-1]  Here you can skip rows if needed, but we will keep all rows and clean later in the data cleaning section.
                
                # loop through all the rows and extract the info then store them in the empty list we created
                for row in rows: 
                    cells = row.find_all('td')
                    #strip the text in each cell of any whitespace.
                    cell_data = [cell.text.strip() for cell in cells]
                    #add the extracted text from each loop in the selenium section
                    cell_data.extend([division_text, offence_text, year_text, type_text])
                    # Add the data to the empty list: 
                    table_info.append(cell_data)
```


```python
# transfer the collected table info to a dataframe: 
crime_df = pd.DataFrame(table_info)

crime_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 51030 entries, 0 to 51029
    Data columns (total 8 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   0       51030 non-null  object
     1   1       51030 non-null  object
     2   2       51030 non-null  object
     3   3       51030 non-null  object
     4   4       51030 non-null  object
     5   5       44550 non-null  object
     6   6       3240 non-null   object
     7   7       3240 non-null   object
    dtypes: object(8)
    memory usage: 3.1+ MB
    


```python
# remove unwanted columns: 
crime_df = crime_df[[4, 0, 2, 3, 5, 1]]

# Rename columns: 
crime_df.rename(columns={4: 'Year', 0: 'Month' 
                         ,2: 'Division', 3: 'Offence'
                         ,5: 'Type', 1: 'Total'}, inplace=True)

# filter df to only keep wanted rows: 
crime_df = crime_df[crime_df['Month'] != 'Month']
crime_df = crime_df[crime_df['Month'] != 'Total']
crime_df = crime_df[~crime_df['Total'].str.contains('Sum')]

crime_df.reset_index(drop=True, inplace=True)

# the last two months appear to have no date, we'll remove them since it would create outliers
crime_df = crime_df.iloc[: -1]
```


```python
crime_df
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
      <th>Month</th>
      <th>Division</th>
      <th>Offence</th>
      <th>Type</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013</td>
      <td>Jan</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013</td>
      <td>Feb</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013</td>
      <td>Mar</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>Apr</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013</td>
      <td>May</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>36</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38064</th>
      <td>2024</td>
      <td>Apr</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>6</td>
    </tr>
    <tr>
      <th>38065</th>
      <td>2024</td>
      <td>May</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>17</td>
    </tr>
    <tr>
      <th>38066</th>
      <td>2024</td>
      <td>Jun</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>5</td>
    </tr>
    <tr>
      <th>38067</th>
      <td>2024</td>
      <td>Jul</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>7</td>
    </tr>
    <tr>
      <th>38068</th>
      <td>2024</td>
      <td>Aug</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>38069 rows × 6 columns</p>
</div>




```python
month_map = {
    'Jan': '01', 'Feb': '02', 'Mar': '03', 'Apr': '04',
    'May': '05', 'Jun': '06', 'Jul': '07', 'Aug': '08',
    'Sep': '09', 'Oct': '10', 'Nov': '11', 'Dec': '12'
}

# Add month numnbers to df    
crime_df['Month_Num'] = crime_df['Month'].map(month_map)  
# combine month number and year to df as a pandas datetime object.
crime_df['date'] = pd.to_datetime(crime_df['Month_Num'].astype(str) + crime_df['Year'])
#format the month_year column
crime_df['Month_Year'] = crime_df['date'].dt.strftime('%m-%Y')
```

    C:\Users\Jessiah\AppData\Local\Temp\ipykernel_22308\2348038888.py:10: UserWarning: Could not infer format, so each element will be parsed individually, falling back to `dateutil`. To ensure parsing is consistent and as-expected, please specify a format.
      crime_df['date'] = pd.to_datetime(crime_df['Month_Num'].astype(str) + crime_df['Year'])
    


```python
crime_df
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
      <th>Month</th>
      <th>Division</th>
      <th>Offence</th>
      <th>Type</th>
      <th>Total</th>
      <th>Month_Num</th>
      <th>date</th>
      <th>Month_Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013</td>
      <td>Jan</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>40</td>
      <td>01</td>
      <td>2013-01-20</td>
      <td>01-2013</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013</td>
      <td>Feb</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>30</td>
      <td>02</td>
      <td>2013-02-20</td>
      <td>02-2013</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013</td>
      <td>Mar</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>40</td>
      <td>03</td>
      <td>2013-03-20</td>
      <td>03-2013</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>Apr</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>38</td>
      <td>04</td>
      <td>2013-04-20</td>
      <td>04-2013</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013</td>
      <td>May</td>
      <td>CENTRAL</td>
      <td>Burglaries and Breakings</td>
      <td>Reported</td>
      <td>36</td>
      <td>05</td>
      <td>2013-05-20</td>
      <td>05-2013</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38064</th>
      <td>2024</td>
      <td>Apr</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>6</td>
      <td>04</td>
      <td>2024-04-20</td>
      <td>04-2024</td>
    </tr>
    <tr>
      <th>38065</th>
      <td>2024</td>
      <td>May</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>17</td>
      <td>05</td>
      <td>2024-05-20</td>
      <td>05-2024</td>
    </tr>
    <tr>
      <th>38066</th>
      <td>2024</td>
      <td>Jun</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>5</td>
      <td>06</td>
      <td>2024-06-20</td>
      <td>06-2024</td>
    </tr>
    <tr>
      <th>38067</th>
      <td>2024</td>
      <td>Jul</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>7</td>
      <td>07</td>
      <td>2024-07-20</td>
      <td>07-2024</td>
    </tr>
    <tr>
      <th>38068</th>
      <td>2024</td>
      <td>Aug</td>
      <td>WESTERN</td>
      <td>Woundings and Shootings</td>
      <td>Detected</td>
      <td>0</td>
      <td>08</td>
      <td>2024-08-20</td>
      <td>08-2024</td>
    </tr>
  </tbody>
</table>
<p>38069 rows × 9 columns</p>
</div>




```python
crime_df = crime_df[['Year', 'Month', 'Month_Num', 'date', 'Month_Year', 'Division', 'Offence', 'Type', 'Total']]
```


```python
crime_df.to_excel("C:\\Users\\Jessiah\\Documents\\Python\\Python Portfolio Projects\\Senelium\\trinidad_tobago_crime.xlsx", index=False)
```


```python
crime_df.to_csv("C:\\Users\\Jessiah\\Documents\\Python\\Python Portfolio Projects\\Senelium\\trinidad_tobago_crime.csv", index=False)
```


```python

```
