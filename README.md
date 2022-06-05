# Kickstarting with Excel
## Overview of Project
### Purpose
Louise is an aspiring playwright looking to fund her upcoming play. This project looks at past successful and failed Kickstarter campaigns to gain insights about how to run a successful campaign. Factors considered include when the campaign was launched as well as the campaign's target funding amount.
## Analysis and Challenges
The first step in the analysis was to get an understanding of the data provided. Information included campaign names and descriptions, goals, actual raised amounts, and the status of the campaign, as well as the country and currency. Other important data was the campaign launch date and deadline, as well as the campaign category and subcategory. A few things to note were that the launch date and deadline were provided as unix time stamps, and thus needed to be normalized to a date readable for humans. Also, the parent and subcategories needed to be split into separate columns for neater filtering, which was achieved trough text to columns conversion with a slash as the delimiter.
### Analysis of Outcomes Based on Launch Dates
After making the data more readable. the first analysis performed was a comparison of campaign outcomes based on the month they were launched. For an easy visualization, a pivot table and corresponding pivot chart would work. Because the dates in the data include days, months, and years, the year needed to be extracted to not clutter the pivot table. The pivot table was constructed with month names in the rows and campaign outcomes in the columns, with a count of campaign outcomes by month. The pivot table also included a filter for the parent category (in this case, theatre) and the year of the campaign. The line graph derived from the pivot table is below.

![This is an image](https://github.com/EricaEidelman/kickstarter-analysis/blob/main/Theatre_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals
The analysis of outcomes based on goals shows the percentage of successful, failed, or cancelled play campaigns, and so the raw numbers needed to be tallied up before dividing by the total to find the percentage. This was achieved with a countifs formula with criteria including the campaign outcome, the "play" subcategory, and a predefined campaign goal range. For example the formula to get the number of successful play campagins with goals between $1000 and $4999 is as follows: =COUNTIFS(Kickstarter!D:D,"<=4999",Kickstarter!D:D,">=1000", Kickstarter!F:F,"successful", Kickstarter!R:R,"plays"). Column D contains the goal data, column F the campaign outcome, and column R the subcategory. Once the raw numbers and percentages were tabled, a line graph was generated with the ranges on the x-axis, the percentages on the y-axis, and each outcome having its own line. The line graph can be seen below.

![This is an image](https://github.com/EricaEidelman/kickstarter-analysis/blob/main/Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered
There were a few difficulties encountered while cleaning the data and also while creating the graphs. As stated above, the launch and deadline dates were originally in a unix time stamp format, which required learning about the unix time stamp in order to figure out how to convert into a readable date. Because the unix time stamp is the number of seconds occurring after January 1st, 1970, the time stamp number needed to first be divided by 86,400 (the number of seconds in a day) and then added to the date of 1/1/1970. Please see the following for what that actually looks like: =(((J2/60)/60)/24)+DATE(1970,1,1), where J2 is the unix time stamp cell. Another challenge was encountered when inputting the range criteria for the countifs formula to find the number of successful, failed, or cancelled campaigns in a specific range. Most of the ranges required two criteria - greater and less than a certain number - but the formula had to follow a certain format to be readable by Excel. Unlike a human, the computer needed to see the comparison sign first always.
## Results
The first conclusion one can draw from the outcomes based on launch date is that May is the best month to launch a campaign. While the number of failed campaigns in May is second only to October, May does also have the highest number of successful campaigns. Another conclusion is that year end is the worst time to launch a campaign. Not only do November and December have the lowest number of successful campaigns, year end also has some of the smallest differences between the number of failed and successful campaigns. December, in particular, has an almost 50-50 chance of failure as well as the smallest number of successful campaigns, making it the worst month to launch a campaign. Potentially, this could be the result of people having more holiday commitments and less time to focus on donating to campaigns.

While the dataset allowed for some robust analysis, it did have its limitations. For example, there is no information for successful campaigns about the point in the campaign when the goal was reached. Having such data could allow for the identification of campaign characteristics which allow the goal to be reached much quicker. Another limitation is that there is no information about the minimum and maximum donation for each campaign. While the data does include the number of backers, which allows for a computation of average donation amount, knowing the minimum and maximum amounts would help to see if there are any outliers in the campaign donors. For example, what if all the successful campaign happened to reach their goal because there was one backer who covered the entire goal amount? Also, knowing the maximum amounts might allow for some analysis to identify which campaign characteristics spur backers to donate larger amounts.

In addition to the analysis carried out so far, there are further graphs and tables which can be made. For example, one could look at the outcomes based on whether a campaign has been selected as a staff pick or Kickstarter spotlight. Such graphs could show whether there are any trends to be identified from having the campaign stand out as either a staff pick or spotlight. Additionally, we could look at the backer count based on launch date to see if there are any periods of the year when more people are likely to donate to an individual campaign. While the outlier situation discussed previously might have an impact on campaign outcome regardless of the amount of backers, the more backers for a campaign, the more likely it is to reach its goal.
