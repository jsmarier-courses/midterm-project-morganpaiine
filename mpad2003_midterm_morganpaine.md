**Thursday November 7th 2024**<br>
**MPAD 2003A Data Storytelling**<br>
**Morgan Paine**<br>
**Presented to Jean-Sébastien Marier**<br>

# Midterm Project: Exploratory Data Analysis (EDA)


## 1. Introduction

For this assignment, I am tasked with performing an Exploratory Data Analysis on a condensed version of a dataset titled "2024 Service Requests" from The City of Ottawa's Website. 
I will be focusing on the month of August. 
The method of obtaining the data is as follows: 
- 311 Contact Centre
- Client Service Centre
- 311 Email
- Web-Based Self Service Portal

Regarding how the data is presented, it is on a spreadsheet that holds columns for each section of a service request:
- Service Request ID Number
- Status
- Desc. of Request
- Type
- Opened Date
- Closed Date (if applicable)
- Address
- Longitude
- Latitude
- Ward #
- Channel (that request came from)


Throughout this assignment I will walk through my process of completing an exploratory data analysis while going through the following:

- Getting Data 
- VIMO Analysis
- Cleaning Data
- EDA (Exploratory Data Analysis)
- Potential Story
- Conclusion
- References

Links to the datasets can be found:

* [Open Ottawa Portal](https://open.ottawa.ca/documents/65fe42e2502d442b8a774fd3d954cac5/about)
* [CSV Version From GitHub Portal](https://raw.githubusercontent.com/jsmarier/course-datasets/refs/heads/main/ottawa-311-service-requests-august-2024.csv)


## 2. Getting Data

To import this dataset into Google Sheets, I first began by downloading it to my desktop and importing the data into a blank sheet. To do this, I first opened the file provided, I then downloaded this file to my "Downloads" folder. Following this, I opened a new spreadsheet on Google Sheets and clicked "File" then "Import". I then went to the "Upload" subhead and I was able to insert this file. For import location, I had "Replace spreadsheet", and for separator type I had "Comma" because the file type is .csv (comma separated values).
Now: This is what my spreadsheet looks like right after importation:
![](Right-After-Import.png)<br>
*Figure 1: This shows what my dataset looks like directly after importation.*

* [Public Link to Google Sheets Spreadsheet](https://docs.google.com/spreadsheets/d/17jAzVSvilda6E-36XpqyFkBYMfPtUzq22PJUVOuzg2w/edit?usp=sharing)

There are 11 columns and 28536 rows. The data itself does not look clean and the spreadsheet is essentially unreadable. For example, the top row, holding the headings disappears as you scroll down, data is unaligned within their columns adding to the unreadability. Another example is the lack of whitespace in the columns which is cutting off the text in the cells. The spreadsheet also holds columns that are mainly empty and unuseful minus a few values (longitude, latitude). 


Making more specific observations, I noticed that column “B” is made up of nominal values, showing if a service request has been resolved, cancelled, or active. I also noticed columns “E”and “F”  consist of ordinal variables. They show the date that requests were opened and closed (if applicable). Also, column “J” is made up of nominal variables, showing ward numbers that these requests were made in. 


A question I would love to ask is: Which ward holds the most active service requests, and why? What are the factors that could play into this? 
Many things could come into play here, such as budget issues, certain types of requests, etc.


## 3. Understanding Data

### 3.1. VIMO Analysis


VIMO analysis is a great tool for further understanding of any given dataset. The acronym stands for: Valid, Invalid, Missing, Outliers.

Valid:
The columns "Status" and "Channel" contain valid, consistent values. "Status" has only "Resolved," "Active," and "Cancelled,". "Channel" column has valid categories like "Dispatch," "Walk-In," etc.
Overall, most values seem valid.
Invalid:
Using a pivot table, I found that there are 2 \N values in the “Type” column. This is odd as every other value seems to be placed in a specific type. This value can be seen as missing or invalid. 
Missing:
There are 3,020 missing values in the "Closed_Date" column and 1,549 in the "Ward" column. These might indicate unresolved cases or cases without specific ward data, so we could flag or remove them depending on their relevance. 
Outliers:
I was unable to find any obvious outliers in this dataset. 

I find this dataset to be generally reliable, considering where it came from, and also the high percentage of valid values. Many large datasets like this one can become unreliable, fast. I find this dataset was able to stay generally organized. 

### 3.2. Cleaning Data

To begin, I froze the first row of the dataset in order to assert that it shows the titles of the data shown below. I also bolded the text of this row and added a dark grey background to make it more distinct and readable.
![](Freeze-top-row.png)<br>
*Figure 2: Showing path to successfully freezing a row.*

I also deleted four columns that are not required for my data analysis (longitude, latitude, address, service request number). 

I added white space in between all of the columns by double clicking the square in the top left corner of the dataset in order to view all of the text. 

In order to remove the french side of the description in the top row, I did some research. The `SPLIT` function could have worked in this case, but I figured it would not be the best method. After looking up a solution, I came across the [Geeks for Geeks Wesbite](https://www.geeksforgeeks.org/how-to-remove-text-before-or-after-a-specific-character-in-excel/). 
This introduced a few equations for me, but the one I ended up using was the `LEFT` function. Essentially, this function searches for a given character in a given cell, then proceeds to remove everything to the left of it including the character. Below I have included an image of the row I added to implement the equation, and the equation without the `LEFT` function applied.
![](LEFT-function.png)<br>
*Figure 3: Rows A and B before and after LEFT function.*

The equation I used is as follows:
``` r
=LEFT(A2,SEARCH("|",A2)-1)
```
After this I had to delete the row with the english and french descriptions.
To do this I had to copy the row with the results and and paste as special values. This will paste the result without causing an error when I delete the cells needed to equate the result.
![](Paste-as-Special.png)<br>
*Figure 4: Pasting results as special values*


This image below shows my dataset after the cleaning process.
![](Data-After-Cleaning.png)<br>
*Figure 5: Dataset After Cleaning*


### 3.3. Exploratory Data Analysis (EDA)

For the exploratory data analysis, I began by creating a pivot table with the following settings: rows- ward ascending, columns -Status ascending, and values - type COUNTA. This was able to show me the amount of service request per ward listed into active, cancelled, and resolved. 
I chose those variables because I was interested in seeing the contrast between wards and exploring the difference in complete requests. 
This chart can be shown below:
![](Pivot-with-numbers.png)<br>
*Figure 6: Showing a Pivot Table with the values being in numbers*
I noticed that while this shows me exact data of what I was looking for, I wanted a version that was easier to understand, making understanding the data quicker and more accessible. That’s when I thought of using % instead of default in the ‘show as’ section. Once I changed this to ‘% of row’ I was much happier with the table as I was able to really see who was leading in resolved service requests as a percentage, rather than a value, which is a much better comparison for this data story. See the new chart below:
![](Pivot-with-percent.png)<br>
*Figure 7: Pivot table after converting to percentages.*
For the chart, this is where I found myself struggling. I wanted to make something that was a clear representation of the variance of incomplete requests per ward. The axis is where the problem lies. If I were to include all three series (Resolved, Active, Cancelled) the product would look completely unreadable with the “Resolved” category taking up the majority of space. 

To solve this, I decided to only include Active and Cancelled as series. This created a chart where the Y-axis has room to show a more understandable picture. I find this chart is readable and even though "Complete" is not present, I believe it is implied and this directs the charts focus to the part of the data I want to focus on: the unresolved cases. 

The chart I decided on is found here:
![](Exploratory-Chart.png)<br>
*Figure 8: Exploratory Chart showing percentages of incomplete requests per ward.*

I decided on a stacked column chart because as stated in chapter 5 section 5.2 of 'Power from Data!' "The stacked bar chart is a preliminary data analysis tool used to show segments of totals" (Government of Canada, 2021). This is what I wanted to achieve by showing both cancelled and ongoing requests as seperate division of a whole (incomplete requests).

While viewing both the dataset and the chart, I noticed that while there are no extreme outliers, there are differences between wards that should be noted. 
The highest active comes from ward-less request at 21.17%, and the lowest incomplete comes from Ward 3 at 5.95%. Realizing that the ward-less requests being the highest may make sense considering they may be much larger issues that need inter-city collaboration. Ward 3's percentage is very low considering the average active cases per ward, in percentages, is: 10.44%
The equation I used to find this can be found here:

``` r
=AVERAGE(B3:B28)
```

As I stated earlier, while there are no outright outliers, I find it an important area to cover as that 20% matters to people in our communities. 



## 4. Potential Story

A potential story within this dataset could be created by focusing on the incomplete requests, focusing on ward. Focusing on the variables pertaining to the differences in wards and exploring how these intersect and affect the public. This could open up many potential reasons as to why this is, such as leadership, budget constraint, lack of materials, etc. 
To tell this story, I could first display this data through readable charts, with a further description as to where the lack of fulfilment is. 
I could interview the representatives of wards that have a high fulfilment rate and also ones who have a low fulfilment rate. They would be able to possibly shed light on the why. I could also interview citizens who had filled out reports and follow up on their experiences depending on if it has been fulfilled or not.  This could provide a contrasted perspective in order to show a well-rounded story that will educate the public and possibly inspire public service workers. 


## 5. Conclusion

The most challenging part(s) of this assignment for me were the VIMO analysis and the cleaning of the dataset. I had a hard time finding outliers and I found myself getting frustrated at times, but this taught me to proceed with my analytical skills even if they are still improving. As for the cleaning of the dataset, at first I was nervous to alter the dataset in any way for fear of losing ‘valuable’ information. 
The most rewarding aspect of this assignment was the lightbulb moment I had when I had cleaned my dataset, and knew which story I wanted to follow. Seeing the pivot table supply what I was looking for and being able to brainstorm this story using charts, further pivot tables etc. I found myself thoroughly enjoying this part of the process. 



## 6. References

Include a list of your references here. Please follow [APA guidelines for references](https://apastyle.apa.org/style-grammar-guidelines/references). Hanging paragraphs aren't required though.

**Here's an example:**

Bounegru, L., & Gray, J. (Eds.). (2021). *The Data Journalism Handbook 2: Towards A Critical Data Practice*. Amsterdam University Press. [https://ocul-crl.primo.exlibrisgroup.com/permalink/01OCUL_CRL/hgdufh/alma991022890087305153](https://ocul-crl.primo.exlibrisgroup.com/permalink/01OCUL_CRL/hgdufh/alma991022890087305153)

Government of Canada, S. C. (2021, September 2). 5 Data Visualization 5.2 Bar Chart. 5.2 Bar chart. https://www150.statcan.gc.ca/n1/edu/power-pouvoir/ch9/bargraph-diagrammeabarres/5214818-eng.htm 
