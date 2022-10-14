# WeRateDogs_Twitter
Analyzing data from WeRateDogs twitter data using python to find interesting insights

## Reporting: wrangle_report
### Data Gathering
Three dataset were used in the project. The three dataset were gathered using different methods
* The twitter archive enhanced dataset was provided by udacity. It was downloaded and loaded in to a dataframe using the pandas to_Dataframe function
* The image prediction dataset was downloaded programatically using the python request library
* Extra tweet data such as retweet counts and favorite count was gathered by querying twitter API using the tweepy library

### Data assessing
The three dataset were assessed both visually and prgrammatically. The following data quality issues and tidiness issues were detected
#### Quality issues
1. There are unnecessary columns that need to be dropped in all the datasets

2. Wrong datatype for the Timestamp and tweet_id column in the tweeter archive dataset

3. 'a' as name in the name column of the tweeter archive dataset(wrongly extracted names)

4. some tweets are retweeted

5. rating denominators below and above 10

6. inconsitency in the name column in the image prediction table

7. some tweets are not dogs

8. rating numerators above 15

9. some column names are not descriptive

#### Tidiness issues
1. there should be a dog_stages column that will contain the four dog stages represented in the tweeter archive table

2. the data_json should be part of the tweeter archive table

3. A tweet rating two dogs

### Data cleaning
The issues detecting in the data assessing stage were clean using various pandas funtions and methods

#### Issue #1: There are unnecessary columns that need to be dropped in all the datasets
The columns not needed for the analysis were dropped using the pandas .drop method

#### Issue #2: Wrong datatype for the Timestamp and tweet_id column in the tweeter archive dataset
The datatype of the timestamp column was changed to datetime and datatype of the tweet_id column was changed to object using the pandas to_datetime function and the pandas .astype method respectively

#### Issue #3: 'a' as name in the name column of the tweeter archive dataset(wrongly extracted names)
The wrongly extracted names( names that started with lowercase) were changed to None using the pandas .replace method

#### Issue #4: some tweets are retweeted
Retweets are not needed for the analyses. Retweets were dropped using pandas ~

#### Issue #5: rating numerators above 15
This issue was resolved following the steps below
1. Re-extract the ratings from the text using the pandas .extract method  
2. Split it into `rating_num` and `rating_dem` columns using the pandas .split  method
3. drop the `rating_numerator` and `rating_denominator`columns using the pandas .drop method
4. drop any row with `rating_num` greater than 15 using the pandas .drop method

#### Issue #6: rating denominators below and above 10
Rows with rating denominator less than 10 were dropped using the pandas .drop  method

#### Issue #7: inconsitency in the dog_breed column in the image prediction table
The names in the dog_breeds column were formatted to lowercase using the pandas str.lower method

#### Issue #8: some tweets are not dogs
The rows with p_dog as False were dropped using the pandas .drop method before the tables were merged

#### Issue #9: some column names are not descriptive
Non descriptive column names, p1 and id_str were renamed to dog_breeds and tweet_id in the image prediction and data_json table respectively

#### Issue #10: there should be a dog_stages column that will contain the four dog stages represented in the tweeter archive table
The issue was resolved following the step below

1. replacing the None with empty string using the pandas .replace method
2. concatenating the 4 dog stages column into a new column, dog_stages, using the + operator
3. dropping the four dog stages columns using the pandas .drop method
4. replacing the empty stings with None

#### Issue #11: the data_json should be part of the tweeter archive table
After cleaning, this tidiness issue was resolved by merging the two tables on tweet_id column using the pandas merge function


#### Issue #12: A tweet rating two dogs
The tweets rating two dogs were identified and the names of the dogs separeted with 'and' in the name column

## Report: act_report
Dogs are amazing! From puppo, doggo, floofer, pupper, the dog stages, to the various dog breeds. After gathering, cleaning and analysing the three dataset produced, the following insights were gotten.

The dog stage with the highest average dog rating.
