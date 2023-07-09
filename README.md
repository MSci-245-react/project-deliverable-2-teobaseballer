[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/tR6jU1Yc)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-7f7980b617ed060a017424585567c406b6ee15c891e84e1186181d67ecf80aa0.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=11435540)
# MSci 245 - Project Deliverable 2

## Due: July 17, 2023, 11:59PM

## GitHub Classroom link: https://classroom.github.com/a/tR6jU1Yc

## Summary: 
Implement reading/writing of the data to/from MySQL database in the node-react- app.

## Development Tips:
- Use CodeSpaces for this project.
- In VSCode terminal on CodeSpaces start a new branch:
```git checkout -b d2```
- As you code, push daily changes to your GitHub repo's `d2` branch:
```
git add .
git commit -m "done feature xyz"
git push origin d2
```

## Deliverable 2 Guidelines

### Part 1: Load IMDB database into your own database on the AWS server and extend the database schema.

Load a copy of the imdb database into your own MySQL database on ec2-18-216-101-119.us-east-2.compute.amazonaws.com following the steps below.
1.	Open MySQL Workbench and connect to 

```
ec2-18-216-101-119.us-east-2.compute.amazonaws.com
```

with your UW username and password 'MSCI245'.

2.	Once you are connected, open a Query window and select your database: 

```
USE YourUserName;
```

where YourUserName is the same as the same as in Step 1.

3.	List all the tables visible to you.

```
SHOW TABLES;
```

Tip: Click on the icon highlighted in the figure below to only run the query with the cursor.


![image](/img/screen1.png)

4.	You will see the list of tables that are currently in your database. 

5.	Delete all listed tables, e.g.: 

```
DROP TABLE user;
```

5.	Download file `imdb.sql` from this repository (app root directory) to your local machine. 

6.	In MySQL Workbench select from the menu `File > Run SQL Script...`

7.	You will be prompted to select a file. Select `imdb.sql` file that you downloaded.

8.	You will see a preview window as shown below. From the dropdown list `Default Schema Name` select the name of your database YourUserName (the same as in Step 2 above). Click `Run`.

![image](/img/screen2.png)

9.	Verify that the tables have been imported correctly by repeating Step 3 in the Query window. 
You should see the following result:

![image](/img/screen3.png)

Tip: To refresh the list of tables on the left click Refresh icon (highlighted in the image).

10.	Augment your copy of IMDB database (loaded into YourUserName database using MySQL Workbench. See Steps 1-9 above). Specifically, create two tables listed below. In addition to the given attributes, add Foreign Keys required to join (a) User with Review and (b) Review with Movie. 

```
Table name: User
Attributes: userID (Primary Key), firstName, lastName, email, phone, dateOfBirth
```

```
Table name: Review 
Attributes: reviewID (Primary Key), reviewTitle, reviewContent (200 characters maximum), reviewScore [values: 1-5] 
```

### Part 2: Implement the following functionalities in your React/Node app

11.	For this deliverable, you will need to extend the React code that you wrote for D1. Copy the code of your D1 React components into the D2 repository. If you had any errors in your D1 code, make sure that you correct them in D2.

***Important: Do not make any changes to your D1 GitHub repository.***

12.	Read the list of movies from MySQL 

i. Upon the first render, the React code should send a request to the NodeJS POST API `getMovies` in `server.js` to retrieve the list of all movie records from the `YourUserName.movies` table in MySQL. 

ii. When the React code receives the list of movies, it should assign the received movies list to a stateful list `movies`. 

iii. Write code to populate the MUI Select element (created in D1) with the values from the stateful list. 

iv. In NodeJS (file `server.js`) create a POST API `getMovies` that will receive a POST request from React and retrieve all records of movies from the `YourUserName.movies` table in MySQL. For each movie, it must retrieve all fields (id, name, year, quality). Finally, the API must send the list of records as a JSON object to React.

13.	Write the user-created movie review to MySQL 

i. When the user clicks `Submit` button, the React should send all review data (movie id, user id, reviewTitle, reviewContent, reviewScore) to the POST API `addReview` in `server.js`. 

ii. In `server.js` implement a POST API `addReview`, which receives user-created review from React, and inserts the review data into the appropriate table(s) in the YourUserName database in MySQL. 

iii. Make sure that you add correct database login credentials in the file `config.js` (in the root project directory). 
- Set host to `ec2-18-216-101-119.us-east-2.compute.amazonaws.com`.
- Set your user name and password to the ones you use to login to the database on MySQL Workbench
- Set database name to your user name.

### Notes:
- You must use Express middleware for sending data between React and Node.
- Make sure that the D1 validation checks still work correctly in your code.
- Declare `userID` as a stateful variable in your React code and set it to '1'.
- You are not required to create the MySQL record for the user with userID='1' in User table upon each review submission. Instead, create it once directly in MySQL Workbench. 

14.	After you finish your development, make sure that the app renders in the browser and functions according to the specifications.

15.	Push changes to the GitHub:

```
git add .
git commit -m "completed"
git push origin d2
```

16.	In your GitHub repo, create new pull request and merge `d2` branch with the `main` branch.





