# nosql-challenge
## Module 12 Challenge : no-sql
### Instructions
_The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles._

### Part 1: Database and Jupyter Notebook Set Up
- Used NoSQL_setup_starter.ipynb for this section of the challenge.

- Imported the data provided in the establishments.json file from your Terminal.
- Named the database uk_food and the collection establishments.
- Copied the text used to import data from Terminal to a markdown cell in the Jupyter notebook.</br>
  _mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json_

- In the Jupyter notebook, imported the libraries : </br> PyMongo and Pretty Print (pprint) </br>
    - from pymongo import MongoClient 
    - from pprint import pprint

- Created an instance of the Mongo Client : </br>
      - mongo = MongoClient(port=27017)

-   Confirmed with these code that the database was created and data properly loaded :</br>
    - print(mongo.list_database_names())

- Listed the databases that are in MongoDB.
- Confirmed that uk_food is listed.
- Listed the collection(s) in the database to ensure that establishments is there.
- Used code find_one with pprint to Find and display one document in the establishments collection .
- Assigned the establishments collection to a variable to prepare the collection for use.

### Part 2: Update the Database
**`Used NoSQL_setup_starter.ipynb for this section of the challenge.`**

The magazine editors have requested some modifications for the database before any queries or analysis can be performed. </br>
Made the following changes to the establishments collection:

**`An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked to include it in the analysis by adding the following information to the database:`**

{
    "BusinessName":"Penang Flavours",</br>
    "BusinessType":"Restaurant/Cafe/Canteen",</br>
    "BusinessTypeID":"",</br>
    "AddressLine1":"Penang Flavours",</br>
    "AddressLine2":"146A Plumstead Rd",</br>
    "AddressLine3":"London"</br>,
    "AddressLine4":"",</br>
    "PostCode":"SE18 7DY",</br>
    "Phone":"",</br>
    "LocalAuthorityCode":"511",</br>
    "LocalAuthorityName":"Greenwich",</br>
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",</br>
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",</br>
    "scores":{</br>
        "Hygiene":"",</br>
        "Structural":"",</br>
        "ConfidenceInManagement":""</br>
    },</br>
    "SchemeType":"FHRS",</br>
    "geocode":{</br>
        "longitude":"0.08384000",</br>
        "latitude":"51.49014200"</br>
    },</br>
    "RightToReply":"",</br>
    "Distance":4623.9723280747176,</br>
    "NewRatingPending":True</br>
}</br>
### Following analysis were performed :
1. Found the BusinessTypeID for "Restaurant/Cafe/Canteen" and returned only the BusinessTypeID and BusinessType fields.</br>

2. Updated the new restaurant with the BusinessTypeID that was found./br>

3. The magazine is not interested in any establishments in Dover, so checked how many documents contained the Dover Local Authority. Then, removed all establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted./br>

4. Some of the number values are stored as strings, when they should be stored as numbers. so,/br>

  - Uses update_many to convert latitude and longitude to decimal numbers.
  - Used update_many to convert RatingValue to integer numbers.

### Part 3: Exploratory Analysis
_Eat Safe, Love has specific questions they want to be answered, which will help them find the locations they wish to visit._

**`Used NoSQL_analysis_starter.ipynb for this section of the challenge.`**

_Some notes to be aware of while you are exploring the dataset:_</br>

RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. </br>The higher the value, the better the rating.</br>
### Note: This field also included non-numeric values such as ***`'Pass'`***, where ***`'Pass'`*** means that the establishment passed their inspection but isn't given a number rating. These were converted to  non-numeric values to ***`nulls`*** during the database setup before converting ratings to integers.</br>

The scores for ***`Hygiene, Structural, and ConfidenceInManagement`*** work in reverse.</br> 
This means, the higher the value, the worse the establishment is in these areas._</br>

The database was used to answer the following questions for the magazine editors :</br>

1.  Used count_documents to display the number of documents contained in the result.

2.  Displayed the first document in the results using pprint.

3.  Converted the result to a Pandas DataFrame,
4.  Printed the number of rows in the DataFrame, and
5.  Displayed the first 10 rows.

6.  Used query to find Which establishments have a hygiene score equal to 20?

7.  Used query with regex to find Which establishments in London have a RatingValue greater than or equal to 4?

8.  Used query, sort,limit with "gte" and "lte" to find the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

9.  Used query for match, group, sort, and created pipeline with aggregation method to find how many establishments in each Local Authority area have a hygiene score of 0? Sorted the results from highest to lowest, and printed out the top ten local authority areas.


