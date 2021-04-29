# CS4320-Project

REQUIREMENTS FOR YOUR AUGUR INSTANCE AND DATABASE:

1. Augur already uses Github's API so there is only one additional line of code needed to collect whether or not a user is hireable. 

2. Access worker_base.py (augur/workers/worker_base.py)

3. In worker_base.py where the platform is GitHub (a little past line 600) add this line of code:
          
          'cntrb_hireable’: contributor['hireable'] if 'hireable' in contributor else None, (It should follow the same format as the lines of code around it)

4. Save the file and rebuild augur ('make rebuild-dev')

5. There are two ways to make changes to the augur database if it's on a deployment server:
      1. Use Navicat and connect your database to it.
          If your augur database is on a physical machine it should be easier to add a new column to it and it should be easier to connect to it. (NOTE: Connecting Navicat to a            database on a server is tricky and I will add instructions for that before the last sprint) 
      2. Use command line

6. If you're using ubuntu and the database is on a server these are the commands and steps for postgres

'\c augur' - will switch to augur database

'ALTER TABLE augur_data.contributors;' - alter the contributors table

'ADD COLUMN cntrb_hireable bool;' - adds a new column to our table
          
'SELECT * FROM augur_data.contributors;' will display the contributors table and its entries. This is a good way to check if the column was added. NOTE: if the tables are messed up do '\x' before running the query to enable expanded view and the tables should be organized. 
      
7. You can now start augur's data collection but it is likely you'll need to collect data on another repo because the current data in contributors might not change. In augur_data.repos you can add another repository however I'm not sure how to get augur to collect data on a different repo. I will need to consult with Prof Goggins before the next sprint.

8. After adding a new repo and running augur the new column should be populated with 't' for true or empty for false.

9. Again you can view the table with Navicat or 'SELECT * FROM augur_data.contributors;' on command line. 
