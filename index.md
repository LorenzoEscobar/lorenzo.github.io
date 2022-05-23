## Twitch Data Analysis

**If any of the screenshots are difficult to see or blurry, right click and open in a new tab!**

In this project, I formatted and analyzed a dataset of the Top 1000 Streamers on Twitch in 2020. I found my dataset on [kaggle](https://www.kaggle.com/datasets/aayushmishra1512/twitchdata) Then from there, I created a SQL server on Google Cloud Platform and connected to it using Microsoft SQL Server Management Studio. 

![ref1](https://user-images.githubusercontent.com/59485356/169712274-6f9f2792-8b23-44db-a908-282d8effa8eb.png)

![ref2](https://user-images.githubusercontent.com/59485356/169712288-3e2c3ad4-fd09-4f0b-9b0d-e29a3356ca3f.png)


After connecting it I used a simple SQL Query to create a database named 'twitch' 
```
CREATE DATABASE twitch;
```

From the Object Explorer in MSSQL, I selected the 'twitch' database and selected task, then imported a flat file. I then select the path to where I had downloaded the CSV and imported it. This automatically created a table with the necessary columns which I named 'topStreamers'. To make sure that everything worked correctly I used the following query to display the table.

```
select * from topStreamers	
```

![ref3](https://user-images.githubusercontent.com/59485356/169712444-8d139976-c923-4fb6-86e1-e723da94aa0b.png)

I played around with the data and tried different ways of organizing it. I found the `top` clause in SQL to be pretty useful to find the leading groups of streamers depending on what I had filtered it with. Apparently, 'top' is only used in MSSQL, so I found that to be interesting as it seems pretty useful. 


```
select top 20 Channel,Average_viewers	  -- top 20 streamers ordered by average viewer
from topStreamers	 
order by Average_viewers desc;
```
```
select top 10 Channel,Followers,Language  -- top 10 english streamers
from topStreamers
where Language = 'English'
order by Followers desc;
```
```
select top 10 Channel,Followers,Language -- top 10 japanese streamers
from topStreamers 
where Language = 'Japanese'
order by Followers desc;
```


![ref4](https://user-images.githubusercontent.com/59485356/169712860-910b9091-c6a1-4f76-8e21-b364de8eccac.png)


Another useful syntax I found was `distinct` this automatically removes duplicate values so I used it to find all the different languages that the Top 1000 Streamers were streaming in. 


```
select distinct Language  -- find all languages used by top 1000 streamers
from topStreamers
```


![ref5](https://user-images.githubusercontent.com/59485356/169713135-c744f0f2-a00f-43e0-926d-406daebd579c.png)


I wanted to find out how many of each streamer was streaming in a certain language so I used `count` to display the amount for each language out of the 1000 Streamers. I will be using these values later to confirm other calculations.


```
select count (Language) as Amount, Language -- amount of streamers streaming in different languages
from topStreamers
group by Language	
order by Amount desc;
```


![ref6](https://user-images.githubusercontent.com/59485356/169713522-ddb72699-ebca-47f2-b691-1a44bcb4d423.png)

After spending some time using SQL, I wanted to gain more experience using different tools often used by data scientsts. I researched and read that Python with pandas and matplotlib were very commonly used. Juptyer Notebooks was also a commonly used tool as well, and to incorporate all of these together I used my preferred IDE of choice, VS Code. But to make my SQL Server not go to waste I went one step further and connected to that from python. For that I used a module called pyodbc that allows connection to the database.



![ref7](https://user-images.githubusercontent.com/59485356/169714055-33d03da3-8327-408e-ac5a-a78836b7d886.png)

From there I could query SQL commands from python, but I wanted to use pandas dataframes to mess with the data. So I selected all of the table and turned it into a dataframe using pandas. I also commented a way to turn the table back into a csv and place the file on your desktop as well as read the CSV from the desktop. I thought this would be good if the server had lots of changing data.

![ref8](https://user-images.githubusercontent.com/59485356/169714585-398f08dd-8ce8-492c-94be-517a7ec70cc5.png)

I found pandas is useful for finding things about a dataset quickly, here I found the mean and the range for Followers. I also found I can get the percentages for each language streamed. If you refer to the SQL query I made earlier about languages you will see that it is accurate. I tried checking percentages for some other categories such as Mature and Partnered.
 

![ref9](https://user-images.githubusercontent.com/59485356/169737355-0a9c6ed7-a4d1-4f2a-8733-a1314d51b350.png)



![ref10](https://user-images.githubusercontent.com/59485356/169737404-ed4901f4-69e4-470a-a1b4-23714657198f.png)



![ref11](https://user-images.githubusercontent.com/59485356/169737522-ef7e19ee-fa3d-4942-b35c-5ee1f8f05eaf.png)


I thought it would be interesting to see the percentages of the languages in a chart. So I used matplotlib, and counted each lanaguage and put it into a pie chart. I used optional parameters such as `explode` to make the smaller values easier to see. I also used `autopct` to round the percentages up in the chart. 

```
#language pie chart
English         =df.loc[df['Language'] == 'English'].count()[0]   
Korean          =df.loc[df['Language'] == 'Korean'].count()[0]
Russian         =df.loc[df['Language'] == 'Russian'].count()[0]
Spanish         =df.loc[df['Language'] == 'Spanish'].count()[0]          
French          =df.loc[df['Language'] == 'French'].count()[0]
Portuguese      =df.loc[df['Language'] == 'Portuguese'].count()[0]
German          =df.loc[df['Language'] == 'German'].count()[0]
Chinese         =df.loc[df['Language'] == 'Chinese'].count()[0]
Turkish         =df.loc[df['Language'] == 'Turkish'].count()[0]
Italian         =df.loc[df['Language'] == 'Italian'].count()[0]         
Polish          =df.loc[df['Language'] == 'Polish'].count()[0]
Thai            =df.loc[df['Language'] == 'Thai'].count()[0]
Japanese        =df.loc[df['Language'] == 'Japanese'].count()[0]
#Other
Other  =df.loc[df['Language'] == 'Other'].count()[0] + df.loc[df['Language'] == 'Czech'].count()[0]   #adds all "Other" languages to other because they are less than 10
+df.loc[df['Language'] == 'Greek'].count()[0] + df.loc[df['Language'] == 'Arabic'].count()[0]  
+df.loc[df['Language'] == 'Hungarian'].count()[0] + df.loc[df['Language'] == 'Slovak'].count()[0]  
+df.loc[df['Language'] == 'Swedish'].count()[0] + df.loc[df['Language'] == 'Finnish'].count()[0]  


labels =['English','Korean','Russian','Spanish','French','Portuguese','German','Chinese','Turkish','Italian','Polish','Thai','Japanese','Other']
explode =(0,0,0,0,0,0,0,0,0,0,.5,.5,.5,.5) #explode distances, to make the smaller values easier to see

plt.pie([English,Korean,Russian,Spanish,French,Portuguese,German,Chinese,Turkish,Italian,Polish,Thai,Japanese,Other],labels=labels,autopct ='%.01f %%',pctdistance= .8,explode = explode) #auto pct rounded percentage
plt.show()   
```



![piechart](https://user-images.githubusercontent.com/59485356/169876533-0cf75190-57ea-49a9-b3ca-db8c9d7754ed.png)

The last tool for this project I wanted to use was Tableau, I downloaded the software and found it easy to quickly connect my SQL server to the program.

![ref13](https://user-images.githubusercontent.com/59485356/169878266-179aaa86-fbd8-4697-abfb-6d892a443aab.png)

I found Tableau to be very intuitive and easy to use. I liked how my tables attributes showed up on the left side and every setting was easy to change with just dragging and dropping.

![ref14](https://user-images.githubusercontent.com/59485356/169878789-e9fa340e-cc32-4e00-909a-d1fd13f562f0.png)

I quickly made a dashboard showing the partnered mature english streamers with the most average viewers. There was also filters on the right so it was easy to change the chart completely if needed.

![Dashboard 1](https://user-images.githubusercontent.com/59485356/169879098-0e446e21-cb7f-43e4-b53a-f4ccad00cb78.png)

I made another dashboard that sorted Twitch Followers per language as well.

![Dashboard 2](https://user-images.githubusercontent.com/59485356/169880307-853049a5-8076-4760-81e0-df6ea913ede3.png)


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3
 
- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/LorenzoEscobar/lorenzo.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
