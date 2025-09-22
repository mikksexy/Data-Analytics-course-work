# Extending the course work
I started this project because I wanted to learn Power BI as it is very popular with enterprises. Additionally, in order to get some hands-on experience with Microsoft's products, I decided to move my course work's database to Azure SQL server.

My main objective was to create interactive dashboards for the operative SQL queries I had previously created. This proved to be a nice challenge as the the logic between the two is quite different.

## Operational dashboards

### Dashboard 1 

TODO

### Dashboard 2

TODO

### Dashboard 3 

TODO

### Dashboard 4 

TODO

### Dashboard 5 

TODO

# Tools and the process

## Azure SQL server
### Loading the data
Setting up the DB was quite straightforward. However, picking the right tool for loading data into the DB was more difficult. 

First, I wanted to reuse my old CREATE TABLE queries. Therefore, I wanted to use the lightest tools for DB management I could find. I tried out a VSCODE plugin which seemed to work fine for running SQL queries.

Similarly, I wanted to try out CLI tools for importing the data into the tables. I tried using bcp utility but I ended up running into connectivity issues... 

Finally, I decided to use SMSS. Its Import Wizard was easy to use. At first I was reluctant to use it as I still wanted to use my predefined table creation queries, however, I didn't have much choice. 

With the Import Wizard, I ran into data type issues. As the Wizard fails the whole import, if it rans into issues, I tried to use Excel to make changes to the data.

I converted the data from .csv to .xlsx and back and tried out different transformation options. I learned a thing or two about Excel but in the end it didn't fix the issues.

The biggest issue was with float values being treated as strings. I managed to import the data by assigning the float values a varchar data type. After a successful import, I reverted the data type back to decimal. 

### Transforming the data

I had to do some cleaning during the import process. However, even more of it followed.

Another thing I struggled with were null values. I queried the ones which shouldn't be allowed by the business logic and deleted them.

I also noticed unexpected null values in some fields which I ended up allowing. So, I made further improvements to the schema by altering the tables.

## Power BI
### Loading the data

Previously, I had tried importing the data straight as a .csv. With this I ran into problems with float values as usual. 

However, when I imported the data from SQL server, I didn't run into these issues. 

### Creating the dashboards

TODO
