#   Project structure

## Overview

An online news anchor for journalists and publishers.

## Project Structure

The project is a modular application made up from 3 services
1.	24news-backend: A Spring Boot service for fetching data from the database
2.	24news-web:	A React web app for displaying news articles to the end user
3.	24news-db:	A PostgreSQL database containing user/article data

User requests in this system function in the following pattern:
1.	The user submits a request through the webpage (24news-web)
2.	The request is sent to the backend (24news-backend)
3.	The backend fetches the requested data from the database (24news-db)
4.	The query result is returned recursively through the abovementioned functions to the user

## System entities

### User
+   Can view news articles
+	Can like/dislike articles
+	Can comment on articles; a temporary username is required for this
+   Doesn't need login/registration

### Journalist
+   Subclass of User
+   Can make and send drafts in their categories

### Publisher
+   Subclass of Journalist
+   Is assigned one/more categories
+   Can view and approve received drafts
+   Can delete articles from assigned categories
+   Can assign categories to Journalists

### Main Publisher
+   Subclass of Publisher
+   Can assign categories to Publishers
+   Can promote Journalists and demote Publishers
+   Can administrate all categories

## System data

### Articles:
+   Contain textual data
+   Can be modified by their Journalist
    -   After approval cannot be modified
+   Can be approved; will be published to frontpage afterwards

## Database management

### Entities
+   Article
    -   ID
    -   Journalist ID
    -   Publisher ID
    -   Title
    -   Content (plain-text or file)
    -   Date published
    -   Category                            required 1
    -   Likes/dislikes & rating
    -   Tags
    -   Comments
+   Draft
    -   ID
    -   Journalist ID
    -   Publisher ID
    -   Title
    -   Content
    -   Category                            required 1
+   Journalist
    -   ID
    -   Name, Surname
    -   Categories                          required 1+
+   Publisher
    -   ID
    -   Name, Surname
    -   Categories                          required 1+
+   Main Publisher
    -   ID
    -   Name, Surname

### Links
+   Like
    -   ID
    -   Article ID
    -   User ID; not in database, created from user IP address
+   Category
    -   ID
    -   Name

## Software technology stack

Tech Stack:
-   Front-End:              React
-   Back-End:               Java/Spring Boot
-	Database:				PostgreSQL

Selected CASE Tools: 
-   IDE:                    VSCode
-   Project Management:     Draw.io

## Front-End

### Websites

1.  Front Page:
    -   Displays news in several rows
        +   Row for popular news
        +   Rows for a few categories
	-	Clicking on news redirects the 'Article' page
    -   Navigation bar to other sites
    -   Login/Register/Account redirect
	-   Search functionality
    -   Category fields for quick search
2.	Article page:
	-	Displays article contents
	-	Displays some Journalist information
	-	Contains Like & Dislike buttons
	-	Contains Comment form
3.  Login Page:
	-   Contains login form
	-   Contains redirect to 'Register' page
4.  Registration page:
	-   Contains registration form
	-   Contains redirect to 'Login' page
5.  Account page:
	-   Displays account information
	-   Contains redirect to draft 'Make Article' page
	-   Contains redirect to 'User Articles' page
	-   Contains redirect to 'User Drafts' page
6.	User Articles page:
	-	Displays a list of articles by Journalist
	-	Clicking on a list element redirects to the 'Article' page
7.	User Drafts page:
	-	Displays a list of drafts by Journalist
	-	Clicking on a list element redirects to the 'Edit Draft' page
8.	Edit Draft page:
	-	Displays the contents of the draft
	-	Displays the approval status of the draft
	-	Contains a send form
	-	Contains a load form

## Back-End

### DB Connections

Using PDO database connection tools.

Each entity and link will have their own database connectors.
Each database connectors will have execution scripts for their every functionality.

***DBC system***
1.	ArticleDB
	-	Insert article
	-	Get article by ID
	-	Get articles by Journalist
	-	Get articles by Publisher
	-	Get articles by name
	-	Get articles by Category
	-	Delete article
2.	DraftDB
	-	Insert draft
	-	Get draft by ID
	-	Get draft by Journalist
	-	Update draft
	-	Delete draft
3.	JournalistDB:
	-	Insert journalist
	-	Get journalist by ID
	-	Get journalist of Article
	-	Get journalists by Publisher
	-	Promote journalist
	-	Delete journalist
4.	LikeDB:
	-	Insert Like
	-	Delete Like
5.	CategoryDB:
	-	Insert category
	-	Get category by ID
	-	Get category by name
	-	Update category

## API

Using JavaScript and AJAX.

Each DBC functionality will have its' own JS script.
Each of these scripts may contain one or more functions:
*	Necessary:	a function that delivers the DBC functionality
*	Optional:	selection/sorting function based on DBC result

