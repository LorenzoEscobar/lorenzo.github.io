## Twitch Data Analysis

In this project, I formatted and analyzed a dataset of the Top 1000 Streamers on Twitch in 2020. I found my dataset on [kaggle](https://www.kaggle.com/datasets/aayushmishra1512/twitchdata) From there, I created a SQL server on Google Cloud Platform and connected to it using Microsoft SQL Server Management Studio. After connecting it I used a simple SQL Query to create a database named 'twitch' 
```
CREATE DATABASE twitch;
```

From the Object Explorer in MSSQL, I selected the 'twitch' database and selected task, then imported a flat file. I then select the path to where I had downloaded the CSV and imported it. This automatically created a table with the necessary columns which I named 'topStreamers'. To make sure that everything worked correctly I used the following query to display the table.

```
select * from topStreamers		
```

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

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
