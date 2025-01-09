# Nosql-challenge

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

## Part 1: Database and Jupyter Notebook Set Up

1. Import the data provided in the establishments.json file from your Terminal.
   
   ```mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json```
2. Name the database uk_food and the collection establishments. Copy the text you used to import your data from your Terminal to a markdown cell in your notebook.
3. . Within your notebook, import the libraries you need: PyMongo and Pretty Print (pprint).
4. Create an instance of the Mongo Client.
5. Confirm that you created the database and loaded the data properly:
6. List the databases you have in MongoDB. Confirm that uk_food is listed.
7. List the collection(s) in the database to ensure that establishments is there.
8. Find and display one document in the establishments collection using find_one and display with pprint.
9. Assign the establishments collection to a variable to prepare the collection for use.

## Part 2: Update the Database

Use NoSQL_setup_starter.ipynb for this section of the challenge.

The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the establishments collection.
An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. 

1. Add the following information to the database:
   
```
{
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}
```

2. Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.
3. Update the new restaurant with the BusinessTypeID you found.

![image](https://github.com/user-attachments/assets/614480cf-05b1-4790-a0f5-151c9d277399)

![image](https://github.com/user-attachments/assets/4d772e66-0230-47b7-a5ba-1d45e8953578)

5. The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.
![image](https://github.com/user-attachments/assets/385b2db1-14a4-4af2-a7cf-bfe1180d4a1a)

6. Some number values are stored as strings, when they should be stored as numbers.
   
7. Use update_many to convert latitude and longitude to decimal numbers.
   
8. Use update_many to convert RatingValue to integer numbers.
![image](https://github.com/user-attachments/assets/cdd593d4-0af3-4bf7-be49-97d59b52b960)


![image](https://github.com/user-attachments/assets/0ea50a0d-a5a4-4229-84ce-f6a5db84b13f)

## Part 3: Exploratory Analysis

Eat Safe, Love has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Use NoSQL_analysis_starter.ipynb for this section of the challenge.

Some notes to be aware of while you are exploring the dataset:

RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We will coerce non-numeric values to nulls during the database setup before converting ratings to integers.

The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.

Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors.

Unless otherwise stated, for each question:

Use count_documents to display the number of documents contained in the result.

Display the first document in the results using pprint.

Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

1. Which establishments have a hygiene score equal to 20?
   ![image](https://github.com/user-attachments/assets/f65e02da-1211-491e-ad4f-dad06f4fe1aa)

   There are 41 establishments with a hygiene score of 20.
   
3. Which establishments in London have a RatingValue greater than or equal to 4?
   Hint: The London Local Authority has a longer name than "London" so you will need to use $regex as part of your search.
   
4. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"
   Hint: You will need to compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.
   
5. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.

![image](https://github.com/user-attachments/assets/57d8d6e6-80ef-4d76-965a-88e832976cee)

55 local establishments in each Local Authority area have a hygiene score of 0. 
These are the 10 local authority areas with the greatest number of establishments with a hygiene score of 0 
