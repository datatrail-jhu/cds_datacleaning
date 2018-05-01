Tidy data generally exist in two forms: wide data and long data. Both types of data are used and needed in data analyisis, and fortunately, there are tools that can take you from wide-to-long and from long-to-wide. This makes it easy to work with any tidy data set. We'll discuss the basics of what wide and long data are and how to go back and forth between the two in RStudio.

Wide data has a column for each variable and a row for each observation. Data are often entered and stored in this manner. This is because wide data are often easy to understand at a glance. For example, this is a wide data set. This particular dataset is one we looked at in a previous lesson. Previously we discussed that it's a rectangular and tidy dataset. Now, we can also state that it is a wide dataset. Here you can clearly see what measurements were taken for each individual and can get a sense of how many individuals are contained in the dataset. Specifically, each individual is in a different row with each variable in a different column. At a glance we can quickly see that we have information about four different people and that each person was measured in four different ways. 

Long data, on the other hand, has a column for what type of variable is contained in that row and then a separate row for the value for that variable. Each row contains a single observation for a single variable.  This is an example of a long data set. This long dataset includes the exact same information as the previous wide datset; it is just stored differently. It's harder to see visually how many different measurements were taken and on how many different people, but the same information is there. While long data formats are less readable than wide data at a glance, they are a lot easier to work with during analysis. Most of the tools we'll be working with use long data. Thus, to go from how data are often stored (wide) to working with the data during analysis (long), we'll need to understand what tools are needed to do this and how to work with them.

Converting your data from wide-to-long or from long-to-wide data formats is referred to as reshaping your data. There are two primary packages in R that will help you reshape your data: tidyr and reshape2. We'll walk through the important functions of these two packages and work through a few examples using the functions in each. However, as with most really helpful packages in R, there is more functionality than what is discussed here, so feel free to explore online documentation for these packages as well. 

For these examples, we'll again use a dataset that is available in R. This time we'll work with the airquality dataset.  The data in this dataset includes "Daily air quality measurements in New York, May to September 1973" This is a wide dataset because each day is in a separate row and there are multiple columns with each including information about a different variable. We can see the first few lines of this dataset using this code. Again, wide data are easy to deciper at a glance. We can see that we have six different variables for each day, with each one of these variables (measurements) being stored in a separate column.

Within tidyr, there are two functions to help you reshape your data: gather, which makes wide data long and spread, which makes long data wide. To get started, you'll need to be sure that the tidyr package is installed and loaded into your RStudio session. 

As data are often stored in wide formats, you'll likely use gather a lot more frequently than you'll use spread. This will allow you to get the data into an easy-to-use-for-analysis format (long). In tidyr, gather will take the quakes dataset from wide to long, putting each column name into the first column and each corresponding value into the second column. 

Here, the first column will be called key. The second column will be value.

However, it's very easy to change the names of these columns within gather. To do so you define what the key and value columns names should be within gather.

However, you're likely not interested in your day and month variable being separated out into their own variabiles within the key column. In fact, knowing the day and month from which a data point came helps identify that particular data point. To account for this, you can exclude day and month from the variables being included in the key column by specifying all the variables that you do want inclued in the key column.  Here, that means specifying ozone, solar.r, wind, and temp. This will keep day and month in their own columns, allowing each row to be identified by the specific day and month being discussed. Now, when you look at the top of this object, you'll see that month and day remain in the data frame and that variable combines information from the other columns in airquality (ozone, solar.r, wind, temp). This is still a long format dataset; however, it has used month and day as IDs when melting the data frame.

To return your long data back to its original form, you can use spread. Here you specify which column has the names of what your wide data columns should be (key=variable) and which column has the values that should go in these columns (value=value). 

And, the resulting spread data frame will have the original information back in the wide format (but, the columns will be in a different order). But, we'll discuss how to rearrange columns in the next lesson!
  
As with many things in R, there is more than one way to solve a problem. While tidyr provides a more general solution for reshaping data, reshape2 was specifically designed for reshaping data. The details aren't particularly important yet, but later on as you carry out your own analyses it will be good to know about both packages. To get started using reshape2, you'll have to first install the library and load it into your R session. 

There are two main functions within the reshape2 package: melt, which makes wide data long and dcast, which makes long data wide. When you just generally melt a data set, melt will take every column, put the column name put it into a variable column, and then put that variables value into a value column. For the quakes data set, below we first assign the melted data frame to the object df. Then we take a look at the top and bottom of this melted data frame (df). 

When you run this code you see that each column from the original data frame (ozone, solar.r, wind, temp,month, and day) are now repeated in the variables column, and each days' value for that variable is now in the value column. This is now a long format dataset!

Now, to use month and day as identifiers as we did with tidyr above, the approach is slightly different. Rather than specificing the columns to be used as keys (as you did with gather), to melt your dataset, you will instead specify these two values (day and month) as identifiers for the dataset. You'll want to use this syntax.

Despite the slight change in how the code was specified, the result here using melt is the same as what was achieved above using gather.

You'll likely have to go from long-to-short format less frequently; however, it's good to know there are two approaches to accomplishing this within reshape2 whenever it is necessary. You'll want to use acast to take a long frame and returning a matrix, array, or vector and dcast to take a long frame and returning a data frame. To return our melted data back into its original wide form, we'll use dcast. The syntax here separates what should be used as an identifier for each row in the resulting wide format (month + day below) and which column includes the values that should be the column headers (variable below). These two pieces of information are separated by a tilde (~).

As you can see, aside from the column order changing, the information in original is the same as what was in the data frame we started with (airquality). While reshaping data may not be the most exciting topic, having this skill will be indispensible as you start working with data. It's best to get these skills down early!