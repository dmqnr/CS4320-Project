# CS4320-Project

#################### HOW TO RUN THE JUPYTER NOTEBOOK ########################

1. Make sure jupyter notebook is installed on your machine
2. Need to install these 3 libraries:
          pip install ipython-sql
          pip install sqlalchemy
          pip install psycopg2
3. Add the jupyter notebook file found in this repository.
4. Run the two cells in the notebook
5. DONE!
6. You can customize the queries if you like. They are exactly like SQL queries. 


##################### HOW TO REPLICATE THIS PROJECT #########################

CHANGES TO AUGUR

1. Augur already uses Github's API so there is only one additional line of code needed to collect whether or not a user is hireable. 

2. Access worker_base.py (augur/workers/worker_base.py)

3. In worker_base.py where the platform is GitHub (a little past line 600) add this line of code:
          
          'cntrb_hireable’: contributor['hireable'] if 'hireable' in contributor else None, (It should follow the same format as the lines of code around it)

4. Save the file and rebuild augur ('make rebuild-dev')


CHANGES TO THE DATABASE

There are two ways to make changes to the augur database if it's on a deployment server:
      1. Use Navicat and connect your database to it.
      2. Use command line

If you're using a server with postgre installed these are the commands to make changes

          '\c augur' - will switch to augur database

          'ALTER TABLE augur_data.contributors;' - alter the contributors table

          'ADD COLUMN cntrb_hireable bool;' - adds a new column to our table

          'SELECT * FROM augur_data.contributors;' will display the contributors table and its entries. This is a good way to check if the column was added. NOTE: if the tables are messed up do '\x' before running the query to enable expanded view and the tables should be organized. 
      
You can now start augur's data collection but it is likely you'll need to collect data on another repo because the current data in contributors might not change

After adding a new repo and running augur the new column should be populated with 't' for true or empty for false.

Again you can view the table with Navicat or 'SELECT * FROM augur_data.contributors;' on command line. 


USING JUPYTER NOTEBOOK (CHANGES TO AUGUR AND DATABASE NEED TO BE COMPLETED FIRST)

1. Jupyter Notebook makes it easier to write SQL queries and displays the output
2. Python and Pip need to be installed on your machine as well as Jupyter Notebook
3. Need to install these 3 libraries:
          pip install ipython-sql
          pip install sqlalchemy
          pip install psycopg2
3. Start your jupyter notebook and create a new file.
4. In one cell add the following code:
          
          %reload_ext sql
          from sqlalchemy import create_engine
          //CONNECTING TO DATABASE FORMAT
          %sql dialect+driver://username:password@host:port/database
          //EXAMPLE FORMAT
          %sql postgresql://augur:password@ec2-18-220-196-21.us-east-2.compute.amazonaws.com:5432/augur

5. In the next cell add the SQL query:
          
          //EXAMPLE
          %%sql
          SELECT 
                 *
          FROM 
                 augur_data.contributors
          WHERE
                 cntrb_hireable = 't'
6. Run each of the cells and you will get an output displayed. 

7. If you want to connect to my deployment server and skip all the changes to augur and the database here is the information you would use in jupyter notebook when connecting to the database 

          dialect+driver: postgresql
          username: augur
          password: password
          host: 
          port: 5432
          database: augur

