# Bike Sales
***
## Introduction
For this project I decided to look deeper into a bike sales dataset, sepcifically looking into the differences between those who have bought a bike and those who have not. I'm looking to gain more insight into learning the differences of the two groups and spot patterns that may be used to better understand the divide between those who have a bike and those who do not.
***
### The Data
I'll begin with a description of the data:
- **ID:** Unique identifier of each person
- **Marital Status:** The status of a person's marriage
- **Gender:** A person's gender
- **Income:** A person's annual income in USD
- **Children:** The number of children the person has
- **Education:** What level of education was achieved
- **Occupation:** What type of job a person does (such as manual, clerical, or management)
- **Home Owner:** Whether they own a home
- **Cars:** How many cars they own
- **Commute Distance:** Distance of daily commute to and from work in miles
- **Region:** What region on earth they reside in
- **Age:** What age they are
- **Purchased Bike:** Whether they purchased a bike or not
***
### Questions
Now that we know the data that we will be looking at, lets ask some questions about it!
**Question 1:** At what distance(s) are people more likely to buy a bike for their commute?
**Question 2:** What ages bought a bike compared to those who did not?
**Question 3:** Does income or gender affect the likelyhood of buying a bike?
With these questions in mind I'll move onto data wrangling.
***
### Remove Duplicates
I'll begin with the basics: removing duplicates. This is an extremely easy process in excel as you only need to highlight your sheet and then press the remove duplicate button. A total of 26 duplicates were found and removed.

![image](https://github.com/user-attachments/assets/a837b0ee-3d27-4be8-bdf4-7226e07ad87c)

![image](https://github.com/user-attachments/assets/b03f7e84-aa15-470c-a071-2f957d2d595b)

***
### Standardize
I'm going to make the data a little more reader friendly, I'll start with changing the values in 'Marital Status' to spell out the meanings of the values 'M' and 'S' to 'Married' and 'Single' respectively.

![image](https://github.com/user-attachments/assets/5d5fd106-abd9-46e9-9cd3-a6e11ac42389)
![image](https://github.com/user-attachments/assets/9504144b-a013-4197-b90b-56aaef64ce88)

![image](https://github.com/user-attachments/assets/d349f729-6a7a-4653-888a-16a3208ba840)
![image](https://github.com/user-attachments/assets/e005e398-1da8-413a-aade-cd0709c1c0dc)

Next I'll do a similar standardization in the 'Gender' column. I'll make 'M' become 'Male' and 'F' become 'Female'.

![image](https://github.com/user-attachments/assets/0e78a650-6670-42f8-a0e5-64a720624d61)
![image](https://github.com/user-attachments/assets/0101af15-b6e7-45a6-a2c9-c5a5fe067e53)
![image](https://github.com/user-attachments/assets/aff1abc3-55a6-4a7f-a9d5-8b37d776500f)

![image](https://github.com/user-attachments/assets/623bc7a5-8095-4651-b5e9-c76d127561ad)
![image](https://github.com/user-attachments/assets/7fdc7ff0-b10f-4183-9873-af173515780d)

Another small change I'll make is to remove the decimals from the income column as there is no income with cents and is therefore unnecessary. This will also make it look a lot better when we use this column as part of our visualization. This is also an easy change because once we select a column we can just press a button to remove the decimals.

![image](https://github.com/user-attachments/assets/d2a93c82-ee6b-4941-9a32-82ad6b5c11c4)
![image](https://github.com/user-attachments/assets/3b467baa-45bb-4f20-b052-748c5ef20899)

For my last change I'm going to change '10+ miles' to 'More than 10 Miles'. I'm doing this because I want to order by commute distance and with excel, '10+ Miles' would come after '0-1 Miles' instead of the desired '1-2 Miles'.

![image](https://github.com/user-attachments/assets/5a0eff99-8647-4455-8be3-5d3dedfd09e7)
![image](https://github.com/user-attachments/assets/f511d5e3-0c23-45dc-97cd-3548db3ed2b6)
![image](https://github.com/user-attachments/assets/2b1e5768-51b0-42e0-a146-82ca3f957b16)

This is the last of our standardization, our data is now in a format that we can use to answer our questions and manipulate cleanly.

***
### Add Age Groups
While we have a lot of good data, our second question will look better if we condense the ages into fewer groups so there aren't so many points on the graph when we visualize the data for presenting. We'll be able to do this by adding a new column and applying the following formula to the entire column. This will give us the resuling column we see next.

![image](https://github.com/user-attachments/assets/ed5e4001-ed26-47bf-bb35-b750f67bbff8)

![image](https://github.com/user-attachments/assets/09572e8c-63be-4946-9245-b2865047c996)


***
### Pivot Tables
Now that we have finished wrangling data we can get to the part of the project where we can answer the questions we asked earlier. My first pivot table will be used to answer the first question by summarizing the total number of people who have and have not bought a bike by their daily commute distance.

![image](https://github.com/user-attachments/assets/4cc217a5-3fce-4478-907c-539e216614fd)

My next pivot table will answer the second question by summing the yes and nos of each age group we made based on the data prior.

![image](https://github.com/user-attachments/assets/8ee3357b-db59-4cb9-b18e-719c6e30f25f)

My final pivot table will answer the third question by averaging the incomes of males and females who have and have not bought a bike.

![image](https://github.com/user-attachments/assets/7960cbee-396c-4264-b922-cfe575f40f81)

***
### Visualization
Because I have three pivot tables, one for each qeuestion, I think that a good way to visualize them is to make the first two into line graphs and the last one into bar graphs. Our first two questions care about distances and ages so we need multiple points which fit the usage of a line graph. My third question is much more straight forward and doesn't need as many points so I'll turn that into a bar graph. This will also help present better on the dashboard as we'll see soon.

![image](https://github.com/user-attachments/assets/7266b73d-9d3e-476f-b4c9-47b09e9cd155)

![image](https://github.com/user-attachments/assets/af04447e-a327-483b-8302-1fcc64a3ad59)

![image](https://github.com/user-attachments/assets/e5ffe17f-2a18-4b1e-918e-35ab05d2036e)

***
### Dashboard
Up next we have our dashboard, this is where the data we collected to answer the questions will be presented. Designed to be clear and consise as to not waste time answering questions or cluttering up the data. Of note, the yes and no legend refer to if the group has bought a bike or not.

![image](https://github.com/user-attachments/assets/32ed885e-0be8-4a96-b6fd-dbaef4019a48)

### Results
As you'll remember our questions were:
**Question 1:** At what distance(s) are people more likely to have a bike?
**Question 2:** What ages bought a bike compared to those who did not?
**Question 3:** Does income or gender affect the likelyhood of buying a bike?

So I'll finally be able to do what I've worked for and answer these questions. 
**1:** 
- From 0-1 miles people are much more likely to have a bike. A good result, we can't improve much on increasing that number until we see the rest of the data.
- 1-2 miles they are similar in likelihood to ride a bike but more often don't. This could be that the commute is short enough to allow people to walk to work rather than ride a bike or drive a car, so for this demographic, the bike riders could increase if the bikes were more affordable or more widely advertised, this is a good demographic to look deeper into for getting them to buy a bike.
- 2-5 miles is still more likely that someone has a bike but not as evident as 0-1 miles. Again we'll continue looking through the data.
- 5-10 miles is where the number of people who have a bike starts to decline steadily. This is likely too far of a distance to commute on bike for many people as it could take close to an hour to get to and from work depending on the person. Another aspect would be difficulty riding for so long, depending on the bike store, electric bikes would be a good way to advertise if they were looking to get people from this demographic to buy a bike.
- 10+ miles is similar to the previous distance except fewer people have bike on average. The way to get people in this range interested is the same as the previous range.

The results are that people are more likely to have a bike if they are closer to their work but at about 5 miles they are less likely to own a bike.
  
**2:**
  - Adolescent (<32) age group is not likely to own a bike but the divide is small, there are also very few adolescents compared to other age groups.
  - Middle Age (32-54) holds a majority of the data within and those in the middle age group are more likely to own a bike.
  - Old (>54) fewer people here and even fewer bike owners, this could be because it's more difficult to ride a bike as people get older so it's less convinent.

Here we can clearly see that the middle age group (32-54) is much more likely to own a bike than other age groups.

**3:**
For our final question we can see that there is a big difference in income between the two genders but there is no clear difference in ratio that would imply one gender buys more bikes than the other. There is a big difference in who bought a bike based on income, as you can see, the average income of those who buy bikes is much higher than the income of those who do not. This is likely due to the ability to spend money rather than prefernece however.
-
