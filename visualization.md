**This note is for the course "Matlab for data visulization and processing"**

*Working with missing data*

NaN: Not an Number

 Number         Timestamp               Country         Windspeed    Pressure    Location
    ______    ____________________    _________________    _________    ________    ________

      2       26-Jun-1957 06:00:00    {'N/A'          }        92         NaN       {'Sea' }
      2       26-Jun-1957 12:00:00    {'N/A'          }        92         973       {'Sea' }
      2       26-Jun-1957 18:00:00    {'N/A'          }        98         NaN       {'Sea' }
      2       27-Jun-1957 00:00:00    {'N/A'          }       109         NaN       {'Sea' }
      2       27-Jun-1957 06:00:00    {'N/A'          }       132         NaN       {'Sea' }
      2       27-Jun-1957 12:00:00    {'N/A'          }       144         946       {'Sea' }
      2       27-Jun-1957 18:00:00    {'United States'}        69         NaN       {'Land'}
      2       28-Jun-1957 00:00:00    {'United States'}        52         972       {'Land'}
      2       28-Jun-1957 06:00:00    {'United States'}        46         NaN       {'Land'}
      2       28-Jun-1957 12:00:00    {'United States'}        40         NaN       {'Land'}

if we want calculate the avaergae of Windspeed, the code should be:
    avgWS = mean(table.Windspeed)

if we want to calculate the mean value of a vector which incldue 'NaN', we could use the following code:
    avgP = mean(table.Pressure, 'omitnan')