### chocolate.csv and chocolate_taste_dataset.csv
  The original datasets downloaded from https://www.kaggle.com/datasets/soroushghaderi/chocolate-bar-2020



### About chocolate_test_original.csv: 

Table scraped on date 5/24/22 from http://flavorsofcacao.com/chocolate_database.html
using code in https://www.kaggle.com/code/andrewmvd/chocolate-ratings-crawler



### About chocolate_test_edited.csv:

An edited version based on chocolate_test_original.csv

- Details:
  - Changed column names to be consistent with the training data's column names
    - "REF" -> "ref"
    - "Company (Manufacturer)" -> "company"     
    - "Company Location" -> "company_location"
    - "Review Date" -> "review_date"
    - "Country of Bean Origin" -> "country_of_bean_origin"
    - "Specific Bean Origin or Bar Name" -> "specific_bean_origin_or_bar_name"
    - "Cocoa Percent" -> "cocoa_percent"
    - "Rating" -> "rating"
  - Deleted the repeated data points already appeared in the training data set based on ref 
    (larger number refers to newer sample according to http://flavorsofcacao.com/chocolate_database.html)
  - Dropped "%" sign in the cocoa_percent column; made the precision to 1 decimal place
  - Separated Ingredients column into 7 new columns to be consistent with the training set, 
    i.e., counts_of_ingredients, cocoa_butter, vanilla, lecithin, salt, sugar, sweetener_without_sugar. 
    Counts_of_ingredients are integers. 
    For the other new columns, the inputs are strings stating whether or not the chocolate contains the specified ingredient
    - Observed that In test set:
      ​		counts_of_ingredients = 1,2,3,4
      ​		Nothing has salt or sweetener_without_sugar
  - Changed column name "Most Memorable Characteristics" to "taste". 
    This column consists of strings of flavors, i.e., each cell is one string with tastes and the tastes in each string are separated by ", "
  - Note: the indices have been set to 0 - length-1 for this data set



### About chocolate_edited_taste_cols.csv:

An edited data file from the original data set chocolate.csv downloaded from Kaggle

- Details:
  - Combined the first_taste, second_taste, third_taste and fourth_taste columns into a new column called "taste". 
    Each cell is a string in which the tastes are separated by ", " -- which is consistent with the test set column "taste"
  - Deleted the unuseful columns:
    - 'Unnamed: 0' - same as the indices of the dataframe
    - 'beans' - all have beans contained
    - 'first_taste', 'second_taste', 'third_taste', 'fourth_taste' - the test set does not have these distingished, but only strings are given

