# Footnote

### Resources:
* Presentation: https://docs.google.com/presentation/d/1C0J2M6T_B_fquxnGgjRV6K_arbpyLvmv8f2Z-C-wYa0/edit?usp=sharing
* Jira: https://badamiec.atlassian.net/jira/software/projects/CAF/boards/3/backlog

## Contents
* [Brief](#brief)
   * [Additional Requirements](#additional-requirements)
   * [My Approach](#my-approach)
* [Architecture](#architecture)
   * [Database Structure](#database-structure)
   * [CI Pipeline](#ci-pipeline)
* [Project Tracking](#project-tracking)
* [Risk Assessment](#risk-assessment)
* [Testing](#testing)
* [Front-End Design](#front-end-design)
* [Known Issues](#known-issues)
* [Future Improvements](#future-improvements)
* [Authors](#authors)

## Fuctionality

The brief provided to us for this project sets the following out as its overall objective:
"To create a CRUD application with utilisation of supporting tools, methodologies and technologies that encapsulate all core modules covered during training."

In other words, I have been tasked with creating an application that utilises create, read, update and delete functions in order to function, such that I can demonstrate that I've learnt something over the last few weeks.

### Additional Requirements
In addition to what has been set out in the brief, I am also required to include the following:
* A Trello board
* A relational database, consisting of at least two tables that model a relationship
* Clear documentation of the design phase, app architecture and risk assessment
* A python-based functional application that follows best practices and design principles
* Test suites for the application, which will include automated tests for validation of the application
* A front-end website, created using Flask
* Code integrated into a Version Control System which will be built through a CI server and deployed to a cloud-based virtual machine

### My Approach
To achieve this, I have decided to produce a simple stargazing companion app that must allow the user to do the following:
* Create a user account (satisfies 'Create') that stores:
   * *User Name*
   * *First and Last Name*
   * *Email*
   * *Password*
* Create posts of observations that they have made whilst stargazing (satisfies 'Create') with the following information:
   * *Title* of the post
   * *Author* of the post
   * *Date and time* that the post was made
   * *Observers* who also took part in this observation (essentially tagging other users in a post)
   * *Location* at which the observation took place
   * *Azimuth* coordinate of the observed object 
   * *Altitude* coordinate of the observed object
   * *Description* of the observation
* View and update their account details (satisfies 'Read' and 'Update')
* Delete their account (satisfies 'Delete')
* Read observations they and other users have created (satisfies 'Read')

Additionally, I would like to allow the user to:
* Refer to a database of stars and corresponding constellations with coordinate data
* Add/delete records of stars and constellations in the database
* Select every star that belongs to a certain constellation

## Architecture
### Database Structure
Pictured below is an entity relationship diagram (ERD) showing the structure of the database. Everything in green has been implemented into the app, while everything in red has not.

![ERD][erd1]

As shown in the ERD, the app models a many-to-many relationship between User entities and Observation entities using an association table. This allows the user to create observation posts and tag multiple users in the database with one observation. Similarly, many observations can therefore be associated with a user.


![appGif][appGif]

## Project Tracking
The progress of the project was tracked using JiraSoftware.

You can find the link to this board here: https://badamiec.atlassian.net/jira/software/projects/CAF/boards/3/backlog

The template used was a Kanban board, and a snapshot of the first sprint is shown below.


![jira][jira]

The board has been designed such that elements of the project move from left to right from their point of conception to being finished and fully implemented. Each card is also colour-coded according to which element of the project it pertains. From left to right, these lists are:
* *Project Requirements*
   A list of requirements set out in the brief in order for this to be a successful project.
* *Project Resources*
   List of relevant resources for quick access.
* *User Stories*
   Any functionality that is implemented into the project first begins as a user story. This keeps the development of every element of the web app focused on the user experience first.
* *Planning*
   The initial stages where a specific element (e.g. a block of code, a server, etc.) is being considered for implementation.
* *In Progress*
   Once the element has had any code written for it/exists in any way, it is placed in the 'in progress' list.
* *Testing*
   Once the element has been created, it moves to the 'testing' list, where its functionality is tested.
* *Finished*
   Any element that is considered to be finished (i.e. works according to its specification) lives in this list.

## Risk Assessment
The risk assessment for this project can be found in full here: https://docs.google.com/spreadsheets/d/1WfKQAjsBfErpQOywRmnZbCe6zw7yFxESFB8WhQd69Es/edit?usp=sharing

Here's a quick screenshot:

![RiskAssessment][riskassessment]

## Testing
pytest is used to run unit tests on the app. These are designed to assert that if a certain function is run, the output should be a known value. Jenkins produces console outputs (pictured below) that will inform the developer how many tests the code passed and which tests they failed.

![pytestconsole][pytestconsole]

pytest also produces a coverage report to show how much of the code in the app has been successfully tested. Jenkins automatically moves this report to the 'templates' folder so that it can be navigated to in a browser, as shown in the picture below.

![coverage][coverage]

## Front-End Design
The front-end of the app is rudimentary at this stage, as the front-end is built purely with very simple HTML. It is largely functional and stable, however.

When the user navigates to the URL, they are directed to the home page:

![homeloggedout][homeloggedout]

They are then able to log in or register an account:

![signup][signup]

![login][login]

Once they are logged in, they now have access to the 'Enter Observation' page and their account page:

![homeloggedin][homeloggedin]

Navigating to the 'Enter Observation' page allows them to post an observation and optionally tag up to two other observers, which will appear at the top of the home page:

![enterobservation][enterobservation]

![homenewobservation][homenewobservation]

Navigating to the 'Account' page allows them to view their account details, update them and delete the account if they so desire. Deleting an account will also delete any observation they are associated with:

![account][account]

## Known Issues
There are a few bugs with the current build of the app:
* If a user attempts to change their email to another email that already exists in the database, the app will inexplicably delete the account entirely
* Certain errors do not appear on the front end when they should, for example: if the user inputs incorrect login information, they should receive an 'Incorrect Username' or 'Incorrect Password' warning – instead the page merely reloads

## Future Improvements
There are several features of the application I would like to improve:
* Currently, the drop-down list for genre options is only available on the "Create" card. When a user wants to update the genre on an existing card, currently there is no drop-down list available after clicking on the input element. A possible future improvement would be to create this functionality.
* Due to the fact that the element displaying the description on an existing card is an input, there is no possibility to set an overflow attribute to scroll for longer descriptions. Instead, the user has to move along the input box to read the book description. A future improvement would be to turn the description element into a paragraph, making it possible to change the overflow attribute to display longer descriptions more clearly.
* Due to time constraints the database currently used is the h2 in-memory database. Migrating onto a cloud-based MySQL database would allow for persistent storage of note cards, which would make them accessible after the back-end and database access is restarted.
* Improving the aesthetical appearance of the front-end further is also on the agenda for future improvements using Bootstrap.
* A section could be added along the top of the page allowing the user to customise and personalise their profile picture and personal details.

The are a few known bugs which have occured during the development stages, and might occur for the user:
* A small grey pixel appears on the colour inputs. The cause of this is unknown, and its presence does not detrimentally affect the functionality of the application. 
* Very rarely the update button has been observed to update the database but not the user display. This is usually fixed immediately by reloading the page.

## Author
Basia Adamiec

[erd1]: https://i.imgur.com/p9wji5S.png
[ci]: https://i.imgur.com/2G7joFp.png
[riskassessment]: https://i.imgur.com/btY8HRY.png
[coverage]: https://i.imgur.com/WDaANiD.png
[pytestconsole]: https://i.imgur.com/qaa3uzp.png
[trello]: https://i.imgur.com/etDOlwa.png
[buildstages]: https://i.imgur.com/ba7ntAo.png
[homeloggedout]: https://i.imgur.com/91NbyWE.png
[signup]: https://i.imgur.com/71f9E6y.png
[login]: https://i.imgur.com/vzwaTtv.png
[homeloggedin]: https://i.imgur.com/F4eXJKR.png
[enterobservation]: https://i.imgur.com/WsBmL6k.png
[homenewobservation]: https://i.imgur.com/NHxV8Gi.png
[account]: https://i.imgur.com/oXDX1y3.png
[jira]:https://i.imgur.com/UAMKolj.png
[appGif]:https://i.imgur.com/1AISLGQ.gifv
