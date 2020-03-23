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