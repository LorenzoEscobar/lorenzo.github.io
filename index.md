## Twitch Data Analysis

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

After spending some time using SQL, I wanted to gain more experience using different tools often used by data scientsts. I researched and read that Python with pandas and matplotlib were very commonly used. Juptyer Notebooks was also a commonly used tool as well, and to incorporate all of these together I used my preferred IDE of choice, VS Code. But to make my SQL Server not go to waste I went one step further and connected to that from python.








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
