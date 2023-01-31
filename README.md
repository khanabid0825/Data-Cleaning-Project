# DATA CLEANING PROJECT USING MICROSOFT EXCEL
For any dataset to highlight facts and figures imperative to make strategic business decisions, it is an absolute necessity that they be neat and presentable.
No pursuit to analyze data in its totality is complete by dodging the very process of data cleaning. In simpler terms, it is a process to fix or remove data that is incorrect, incomplete, or mislabeled. In this project, the dataset deals with the 

A) Inserting a new "responders_id" column to give each survey responder a unique ID using the SEQUENCE function
Since a total of 736 people responded to the survey, I used the SEQUENCE function to insert 736 values inside the "responders_id" column. 
![SEQUENCE NEW](https://user-images.githubusercontent.com/123303003/215724296-6c07e84d-1ea6-4340-8a30-d32f3ebd5342.png)



B) Extracting "Date" from the timestamp column using a range of functions:
The timestamp column maintains a combined record of the date as well as the time when the survey response was recorded and subsequently updated in the dataset.
While the initial values do seem to be of the same format, the latter half of the column lacks uniformity. A clear variance can be observed in the timestamp column from "B448".
To extract date from this column, we need to perform a range of functions. 
-> Using the left function to segregate the first 446 cells. 
![LEFT FUNCTION DATE](https://user-images.githubusercontent.com/123303003/215719757-729e4b94-1a87-4942-9012-238ece6646a6.png)

-> B448 to B644 contains date and time, preferably, date arranged in the wrong manner. Here, the system shows the first value in the date to be the day where it should have been a month.
Eg: 9/13/2022
Here, 9 (September) is supposed to be the month, 
13 is supposed to be the day,
and 2022 is supposed to be the year. 

Instead, the values are reversed. In this case, we can use the "DATE" function to rearrange values and place the month and the day accordingly.
![DATE FUNCTION ](https://user-images.githubusercontent.com/123303003/215725781-5aaa974d-9399-4ec1-b2bc-0e030d505a31.png)


However, even after executing the date function, the resultant values do not give us the desired output.
Just like the first 446 cells in our column, the order we wish to maintain in our records is mm/dd/yyyy. In order to alter these cells to match our standard date format, I decided to use a custom format. 
![DATE RESULT VALUES](https://user-images.githubusercontent.com/123303003/215726310-98df5782-6460-494e-a759-08eed91ebfb1.png)

Since the cells highlighted have zeroes preceding the actual date and month, which does not seem to be the case in the 446 cells above it, I decided to customize the date format to maintain uniformity in my data.
This can be achieved by customizing the mm/dd/yyyy into m/d/yyyy to remove zeroes that precede the day and month of our dates. 
![CUSTOM DATE](https://user-images.githubusercontent.com/123303003/215726551-624f281a-6f56-4fa0-93b0-a4f1197d8659.png)


-> The next 55 cells following B664 have been segregated from the timestamp column using text to columns. 
Like I used in the first 446 cells, I could have extracted the date from these columns using the left function but I instead decided to use the text to columns. 
To properly execute the text to column, I first copied the highlighted cells of the timestamp column into the newly created "fixed date" column. 
The next step was to go to the text to columns tool in the data tools group and then use the delimited method to split and subsequently retain only the date from the combined date and time cell.
In this case, I used space as a special character to separate the two, changed the date format to mm/dd/yyyy and avoided importing a new column for values in time format. 



C) Creating an age group column to divide age into different classes using the IFS function
Before splitting the age column into different groups, it was imperative to figure out the maximum and minimum age in the entire array of values. 
Using the MAX and MIN function, I was able to extract the highest as well as the lowest of values, in our case, the maximum as well as the minimum age. 
Here, Minimum age = 10, Maximum age = 89.
After figuring out the maximum and minimum age, I decided to divide the age column into 8 groups.

Using the IFS function, we pass on the following statements to return back
![IFS AGE](https://user-images.githubusercontent.com/123303003/215728656-4f7fd0cc-9d00-4586-834e-722f33473368.png)


= IFS(D2 <= 19, "10-19", AND(D2 >19, D2<= 29), "20-29", AND(D2>29, D2<= 39), "30-39", AND(D2 > 39, D2 <= 49), "40-49", AND(D2>49, D2 <= 59), "50-59", AND(D2>59, D2<= 69), "60-69", AND(D2 >69, D2<=79), "70-79", D2>79, "80-89")


D) Making minute adjustments in the column "Primary streaming service" using filters
Although most of the responders happen to be subscribed to a primary streaming service, some of the responses also mention people not having a go-to streaming service. 
Just for the sake of visualization process, so as to make our data more cleaner and presentable, I decided to replace "I do not have a streaming service" with "no streaming service".
![FILTER STREAMING SERVICE](https://user-images.githubusercontent.com/123303003/215729971-840a19ac-3266-4f18-b478-3e3946328455.png)

A quick way to achieve this was by filtering the primary streaming services column by the response I mentioned above and simply typing "no streaming service" before dragging it on to the cells that had the same response. 
![FILTER 2](https://user-images.githubusercontent.com/123303003/215730125-0c28a453-5f73-41a2-8217-9cc7e3445aee.png)

E) Dividing self-reported scores related to anxiety, insomnia, depression, and OCD into three different groups using the IFS function.
An IFS function, just like it was executed to perfection to populate individual age into eight classes, can also be used to group the scores reported by responders in the anxiety, insomnia, depression, and OCD columns.
Knowing that the scores are placed in between a score of 0-10, I decided to divide all the four columns into three different classes, as follows:


0-3: Mild

4-7: Moderate

7-10: Severe

![ANXIETY SCORE](https://user-images.githubusercontent.com/123303003/215730636-46792173-9a4f-44c7-a0c3-8193f9e01523.png)

F) Dealing with missing values
To check the number of missing values in our worksheet, I simply selected the entire worksheet (CTRL+A) and directed my cursor towards the editing group on Home tab to use the Find & Select tool.
Clicking on the find and select tool leads you to a different array of options to choose from. Since it was the missing cell values we needed to check, the "Go to Special" tab was selected. 
![SELECT SPECIAL](https://user-images.githubusercontent.com/123303003/215731479-380e811d-7006-43c1-94af-fb929d27c556.png)


Of all the columns, the beats per minute column had more than twice the dozen of values missing. A good way of populating the missing spaces in this particular dataset is by looking across the corresponding "Fav Genre" column to see how many of those who responded liked a particular genre.
Suppose, 17 of the 70 missing spaces submitted "Rock music" as their favourite genre. I can now calculate the average beats per minute of responders who consider rock to be their favourite genre to populate the 17 missing spaces.
The same can be done for the rest of the spaces. 
![ANALYZE DATA](https://user-images.githubusercontent.com/123303003/215732167-c5c2a2b9-de9b-4982-8d5a-8a73e8c84a5d.png)


Of the total 89 missing values, approx 35% of the responders find themselves to be an admirer of rock music whilst pop and classical share the second spot with a combined total of 24 responders.
The next step would be to calculate the average BPM of every genre that is admired and appreciated by responders with a missing "BPM" value. 

![AVERAGE ROCK BPM](https://user-images.githubusercontent.com/123303003/215735085-3f55ffc3-6b74-4030-bc55-0379621dab81.png)


Using the AVERAGE function, the blank cells were replaced with the following values:

![AVERAGE](https://user-images.githubusercontent.com/123303003/215736898-5abbeb28-ff38-4533-b71c-7564505ec98f.png)

G) Deleting unnecessary data
Every dataset that's yet to be imported into a data visualization tool goes through a wide range of processes, of which data cleaning is the first. While majority of the data is cleaned 
and adjusted to liking, data that adds little to no value needs to be removed. 
With the aim of interacting with a data that reflects all the necessary information that we set out to convey in our pursuit, several columns in this dataset have been compromised/removed for the sake of visualization.
To be more precise, the columns that described how frequently responders listen to a certain genre of music as well as the permissions column have been removed from the dataset. 


H) Shortening row values using the IF function:
In this dataset, there are several columns that have values recorded as Yes or No. 
Whilst the data is still good to work on, trimming it down to Y or N using the IF function would make the entire dataset more neat and presentable.

![YES](https://user-images.githubusercontent.com/123303003/215737633-1809b28e-3e38-47b8-ba42-c8a4703d0362.png)




