**This note is for the course "Matlab for data visulization and processing"**

# *Working with missing data*

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


# *Deleting missing data*
Some functions allow the style of "omitnan", some not. For functions which are not allowed to use omit style, we can delete the NaN observations.
    *Note*: missing values are NaN, missing datatime is NaT, missing categorical data are undefined.

    *Note*: using "ismissing" function on a table to identify the location of any missing values.

For the example table, the code should be: "ismissing(data)"

    *Note*: Using "any" function to determine which rows has any true value. e.g. trueRows = any(grid, 2)
    The 2 means search any true value in second demensions, which is row. (The first dimension is column)

    *Combine "ismissing" and "any", we could get a column vector whose each element represeant a row, if the value is 1, means there is missing value in that row, vise versa.*

We can delete rows in a table if we the index of those table, in this tutorial, we got the logical column vector from the combination of "any" and "ismissing", then we can do this:
    table(logicalV,:) = [], then all the rows incldue missing values are deleted.

# *Categories and Set Options*

# *Find and Merge Categories*
create a categorical array: x = categorical({'medium','lagre', 'small', 'medium', 'red'})

Find the categories in the x array using "categories function"
    c = categories(x)

setdiff function: setdiff(a, b), returns a variable d contains values in a but not present in b
We can use the function to remove items from category:
    for instance, we dont want to have red: sz = setdiff(c, 'red')

Merge different categories in one categorical array, the following command merge the categories q1, q2, q3 by q: a = mergecats(a, {'q1', 'q2', 'q3'}, 'q')

in our example:
    x = mergecats(x, {'small', 'medium', 'large'}, 'size'), then the category size has three values for small, medium, large repectively



# *Hurricane Exercise*

Number         Timestamp               Country          Windspeed    Pressure
    ______    ____________________    __________________    _________    ________

      1       18-Jun-1993 00:00:00    N/A                       29         1006  
      1       18-Jun-1993 06:00:00    N/A                       29         1005  
      1       18-Jun-1993 12:00:00    N/A                       29         1005  
      1       18-Jun-1993 18:00:00    N/A                       35         1005  
      1       19-Jun-1993 00:00:00    N/A                       35         1006  
      1       19-Jun-1993 06:00:00    N/A                       35         1006  
      1       19-Jun-1993 12:00:00    N/A                       40         1000  
      1       19-Jun-1993 18:00:00    N/A                       40         1000  
      1       20-Jun-1993 00:00:00    N/A                       40         1000  
      1       20-Jun-1993 06:00:00    N/A                       40         1001  
      1       20-Jun-1993 12:00:00    United States             35         1002  
      1       20-Jun-1993 18:00:00    United States             35         1003  
      1       21-Jun-1993 00:00:00    United States             35         1004  
      1       21-Jun-1993 06:00:00    United States             29         1006  
      2       04-Aug-1993 12:00:00    N/A                       35         1010  
      2       04-Aug-1993 18:00:00    N/A                       35         1009  
      2       05-Aug-1993 00:00:00    N/A                       40         1008  
      2       05-Aug-1993 06:00:00    N/A                       46         1007  
      2       05-Aug-1993 12:00:00    N/A                       52         1006  
      2       05-Aug-1993 18:00:00    N/A                       52         1006  
      2       06-Aug-1993 00:00:00    N/A                       52         1006  
      2       06-Aug-1993 06:00:00    N/A                       58         1005  
      2       06-Aug-1993 12:00:00    N/A                       58         1005  
      2       06-Aug-1993 18:00:00    N/A                       58         1003  
      2       07-Aug-1993 00:00:00    N/A                       58         1002  
      2       07-Aug-1993 06:00:00    N/A                       58         1002  
      2       07-Aug-1993 12:00:00    N/A                       58         1002  
      2       07-Aug-1993 18:00:00    N/A                       52         1006  
      2       08-Aug-1993 00:00:00    N/A                       46         1008  
      2       08-Aug-1993 06:00:00    N/A                       46         1007  
      2       08-Aug-1993 12:00:00    Venezuela                 46         1007  
      2       08-Aug-1993 18:00:00    Venezuela                 46         1007  
      2       09-Aug-1993 00:00:00    Colombia                  46         1006  
      2       09-Aug-1993 06:00:00    N/A                       40         1005  
      2       09-Aug-1993 12:00:00    N/A                       35         1004  
      2       09-Aug-1993 18:00:00    N/A                       35         1005  
      2       10-Aug-1993 00:00:00    N/A                       35         1004  
      2       10-Aug-1993 06:00:00    N/A                       40         1003  
      2       10-Aug-1993 12:00:00    N/A                       46         1002  
      2       10-Aug-1993 18:00:00    Nicaragua                 40         1004  
      2       11-Aug-1993 00:00:00    Nicaragua                 29         1007  
      2       11-Aug-1993 06:00:00    Nicaragua                 23         1009  
      2       11-Aug-1993 12:00:00    N/A                       23         1010  
      3       14-Aug-1993 12:00:00    N/A                       35         1012  
      3       14-Aug-1993 18:00:00    Martinique                40         1012  
      3       15-Aug-1993 00:00:00    N/A                       40         1011  
      3       15-Aug-1993 06:00:00    N/A                       40         1011  
      3       15-Aug-1993 12:00:00    N/A                       40         1013  
      3       15-Aug-1993 18:00:00    N/A                       40         1012  
      3       16-Aug-1993 00:00:00    N/A                       40         1010  
      3       16-Aug-1993 06:00:00    N/A                       40         1008  
      3       16-Aug-1993 12:00:00    N/A                       46         1007  
      3       16-Aug-1993 18:00:00    N/A                       40         1008  
      3       17-Aug-1993 00:00:00    Dominican Republic        35         1010  
      5       22-Aug-1993 18:00:00    N/A                       35         1020  
      5       23-Aug-1993 00:00:00    N/A                       35         1020  
      5       23-Aug-1993 06:00:00    N/A                       35         1020  
      4       23-Aug-1993 12:00:00    N/A                       29         1010  
      5       23-Aug-1993 12:00:00    N/A                       35         1020  
      4       23-Aug-1993 18:00:00    N/A                       35         1009  
      5       23-Aug-1993 18:00:00    N/A                       35         1020  
      4       24-Aug-1993 00:00:00    N/A                       35         1007  
      5       24-Aug-1993 00:00:00    N/A                       35         1020  
      4       24-Aug-1993 06:00:00    N/A                       35         1005  
      5       24-Aug-1993 06:00:00    N/A                       35         1020  
      4       24-Aug-1993 12:00:00    N/A                       40         1003  
      5       24-Aug-1993 12:00:00    N/A                       35         1020  
      4       24-Aug-1993 18:00:00    N/A                       46         1002  
      5       24-Aug-1993 18:00:00    N/A                       35         1019  
      4       25-Aug-1993 00:00:00    N/A                       52         1000  
      5       25-Aug-1993 00:00:00    N/A                       35         1018  
      4       25-Aug-1993 06:00:00    N/A                       52         1000  
      5       25-Aug-1993 06:00:00    N/A                       35         1017  
      4       25-Aug-1993 12:00:00    N/A                       52         1000  
      5       25-Aug-1993 12:00:00    N/A                       40         1016  
      4       25-Aug-1993 18:00:00    N/A                       52         1000  
      5       25-Aug-1993 18:00:00    N/A                       46         1015  
      4       26-Aug-1993 00:00:00    N/A                       52         1000  
      5       26-Aug-1993 00:00:00    N/A                       52         1013  
      4       26-Aug-1993 06:00:00    N/A                       52         1000  
      5       26-Aug-1993 06:00:00    N/A                       63         1010  
      4       26-Aug-1993 12:00:00    N/A                       52         1000  
      5       26-Aug-1993 12:00:00    N/A                       69         1007  
      4       26-Aug-1993 18:00:00    N/A                       46         1001  
      5       26-Aug-1993 18:00:00    N/A                       75         1004  
      4       27-Aug-1993 00:00:00    N/A                       46         1002  
      5       27-Aug-1993 00:00:00    N/A                       69         1000  
      4       27-Aug-1993 06:00:00    N/A                       40         1005  
      5       27-Aug-1993 06:00:00    N/A                       69          997  
      4       27-Aug-1993 12:00:00    N/A                       35         1006  
      5       27-Aug-1993 12:00:00    N/A                       69          992  
      4       27-Aug-1993 18:00:00    N/A                       29         1009  
      5       27-Aug-1993 18:00:00    N/A                       75          982  
      4       28-Aug-1993 00:00:00    N/A                       29         1009  
      5       28-Aug-1993 00:00:00    N/A                       86          981  
      4       28-Aug-1993 06:00:00    N/A                       29         1009  
      5       28-Aug-1993 06:00:00    N/A                       86          982  
      4       28-Aug-1993 12:00:00    N/A                       29         1010  
      5       28-Aug-1993 12:00:00    N/A                       86          981  
      5       28-Aug-1993 18:00:00    N/A                       86          976  
      5       29-Aug-1993 00:00:00    N/A                       81          973  
      5       29-Aug-1993 06:00:00    N/A                       81          978  
      5       29-Aug-1993 12:00:00    N/A                       81          979  
      5       29-Aug-1993 18:00:00    N/A                       81          978  
      5       30-Aug-1993 00:00:00    N/A                       81          977  
      5       30-Aug-1993 06:00:00    N/A                       81          976  
      5       30-Aug-1993 12:00:00    N/A                       86          975  
      5       30-Aug-1993 18:00:00    N/A                       86          974  
      5       31-Aug-1993 00:00:00    N/A                       92          972  
      5       31-Aug-1993 06:00:00    N/A                       98          970  
      5       31-Aug-1993 12:00:00    N/A                      109          965  
      5       31-Aug-1993 18:00:00    N/A                      115          962  
      5       01-Sep-1993 00:00:00    N/A                      115          960  
      5       01-Sep-1993 06:00:00    N/A                      115          962  
      5       01-Sep-1993 12:00:00    N/A                      109          965  
      5       01-Sep-1993 18:00:00    N/A                      104          969  
      5       02-Sep-1993 00:00:00    N/A                      104          971  
      5       02-Sep-1993 06:00:00    N/A                      104          972  
      5       02-Sep-1993 12:00:00    N/A                      104          973  
      5       02-Sep-1993 18:00:00    N/A                       98          974  
      5       03-Sep-1993 00:00:00    N/A                       92          975  
      5       03-Sep-1993 06:00:00    N/A                       86          979  
      5       03-Sep-1993 12:00:00    N/A                       81          985  
      5       03-Sep-1993 18:00:00    N/A                       69          994  
      5       04-Sep-1993 00:00:00    N/A                       58          999  
      5       04-Sep-1993 06:00:00    N/A                       46         1002  
      5       04-Sep-1993 12:00:00    N/A                       40         1001  
      5       04-Sep-1993 18:00:00    N/A                       35         1006  
      5       05-Sep-1993 00:00:00    N/A                       35         1008  
      5       05-Sep-1993 06:00:00    N/A                       35         1009  
      5       05-Sep-1993 12:00:00    N/A                       29         1010  
      5       05-Sep-1993 18:00:00    N/A                       29         1011  
      5       06-Sep-1993 00:00:00    N/A                       29         1012  
      5       06-Sep-1993 06:00:00    N/A                       29         1013  
      5       06-Sep-1993 12:00:00    N/A                       29         1014  
      6       07-Sep-1993 12:00:00    N/A                       29         1012  
      6       07-Sep-1993 18:00:00    N/A                       46         1010  
      6       08-Sep-1993 00:00:00    N/A                       52         1009  
      6       08-Sep-1993 06:00:00    N/A                       52         1011  
      6       08-Sep-1993 12:00:00    N/A                       46         1012  
      6       08-Sep-1993 18:00:00    N/A                       46         1011  
      6       09-Sep-1993 00:00:00    N/A                       46         1009  
      6       09-Sep-1993 06:00:00    N/A                       46         1007  
      6       09-Sep-1993 12:00:00    N/A                       58          997  
      6       09-Sep-1993 18:00:00    N/A                       75          990  
      6       10-Sep-1993 00:00:00    N/A                       75          990  
      6       10-Sep-1993 06:00:00    N/A                       75          990  
      6       10-Sep-1993 12:00:00    N/A                       75          990  
      6       10-Sep-1993 18:00:00    N/A                       75          990  
      6       11-Sep-1993 00:00:00    N/A                       75          989  
      6       11-Sep-1993 06:00:00    N/A                       75          988  
      6       11-Sep-1993 12:00:00    N/A                       75          987  
      6       11-Sep-1993 18:00:00    N/A                       75          986  
      6       12-Sep-1993 00:00:00    N/A                       75          983  
      6       12-Sep-1993 06:00:00    N/A                       75          980  
      6       12-Sep-1993 12:00:00    N/A                       81          972  
      6       12-Sep-1993 18:00:00    N/A                       81          966  
      6       13-Sep-1993 00:00:00    N/A                       81          966  
      7       14-Sep-1993 18:00:00    N/A                       29         1008  
      7       15-Sep-1993 00:00:00    N/A                       35         1005  
      7       15-Sep-1993 06:00:00    N/A                       35         1001  
      7       15-Sep-1993 12:00:00    N/A                       40         1001  
      7       15-Sep-1993 18:00:00    Nicaragua                 40         1005  
      7       16-Sep-1993 00:00:00    Nicaragua                 35         1006  
      7       16-Sep-1993 06:00:00    Nicaragua                 35         1006  
      7       16-Sep-1993 12:00:00    Nicaragua                 35         1006  
      7       16-Sep-1993 18:00:00    Nicaragua                 29         1006  
      7       17-Sep-1993 00:00:00    Nicaragua                 29         1006  
      7       17-Sep-1993 06:00:00    Honduras                  29         1006  
      7       17-Sep-1993 12:00:00    Honduras                  29         1006  
      7       17-Sep-1993 18:00:00    N/A                       40         1001  
      7       18-Sep-1993 00:00:00    N/A                       40         1000  
      7       18-Sep-1993 06:00:00    Belize                    40         1002  
      7       18-Sep-1993 12:00:00    Mexico                    35         1003  
      7       18-Sep-1993 18:00:00    Mexico                    35         1003  
      8       18-Sep-1993 18:00:00    N/A                       35         1014  
      7       19-Sep-1993 00:00:00    N/A                       35         1001  
      8       19-Sep-1993 00:00:00    N/A                       35         1013  
      7       19-Sep-1993 06:00:00    N/A                       40         1000  
      8       19-Sep-1993 06:00:00    N/A                       35         1012  
      7       19-Sep-1993 12:00:00    N/A                       46          993  
      8       19-Sep-1993 12:00:00    N/A                       35         1010  
      7       19-Sep-1993 18:00:00    N/A                       52          992  
      8       19-Sep-1993 18:00:00    N/A                       35         1009  
      7       20-Sep-1993 00:00:00    N/A                       63          990  
      8       20-Sep-1993 00:00:00    N/A                       35         1008  
      7       20-Sep-1993 06:00:00    N/A                       75          982  
      8       20-Sep-1993 06:00:00    N/A                       40         1005  
      7       20-Sep-1993 12:00:00    N/A                       92          978  
      8       20-Sep-1993 12:00:00    N/A                       58          998  
      7       20-Sep-1993 18:00:00    N/A                       98          970  
      8       20-Sep-1993 18:00:00    N/A                       75          990  
      7       21-Sep-1993 00:00:00    Mexico                    75          984  
      8       21-Sep-1993 00:00:00    N/A                       69          992  
      7       21-Sep-1993 06:00:00    Mexico                    46         1000  
      8       21-Sep-1993 06:00:00    N/A                       63          994  
      7       21-Sep-1993 12:00:00    Mexico                    29         1002  
      8       21-Sep-1993 12:00:00    N/A                       58          997  
      7       21-Sep-1993 18:00:00    Mexico                    23         1004  
      8       21-Sep-1993 18:00:00    N/A                       58          999  



The goal of this task is to add a new variable named Location to the table data. This variable is meant to indicate whether the hurricane was observed on land or on the sea.

One way to do this is to *find all the valid country names (values excluding 'N/A')* and *then merge them to create a new category named 'Land' using the function mergecats*. Assign the result to a new variable Location in the table data.

Then, use the function renamecats to rename the category 'N/A' to 'Sea'.

Instructions:
Step 1 - Find the distinct categories in the variable Country using the function *categories*.
    country = categories(data.Country)

Step 2 - Remove 'N/A' from the list of categories using the function setdiff.
    countryNoNa = setdiff(country, 'N/A')

Step 3 - Merge the remaining categories to a new category 'Land' and set the result to a new variable named Location.
    data.location  = mergecats(data.Country, countryNoNa, 'Land')
    * B = mergecats(A,oldcats) merges two or more categories in A into the first category, oldcats(1). Any values in A from oldcats become oldcats(1) in B.*
    * B = mergecats(A,{'belt' 'shoes'},'other')
      *change the caterogy belt and shoes in A to other*
      B = 3x2 categorical
        shirt      pants 
        other      shirt 
        dress      other *


    
data.Location = mergecats(data.Country,catNames,'Land')



Step 4 - In the variable Location, rename the category 'N/A' to 'Sea' using the function renamecats.
    In the variable Location, rename the category 'N/A' to sea, using the function *rename cats*
    data.Location = renamecats(data.Location, 'N/A', 'Sea') 
        *second parameter is the oldcatname, the third one is the new name*