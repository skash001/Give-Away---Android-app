

ESE 543: MOBILE CLOUD COMPUTING

PROJECT REPORT: Give Away

PROJECT MEMBER:   Sachin Kashyap   
SBU ID        :   110529918


1 Idea:
The basic idea of the app is to provide a platform to the users of the app where they can give away things that are no longer required by them to those users that require these items. The giver inputs the information of the item that he want to give away and this information is published to all other users the app. The taker can browse through these items and can select 


2 Motivation:

In the Apartment that I live in, usually at the end of the semester, the graduating students give away the stuff they don’t want, to the students in that area. Stuff like books, electronics and household items save a lot of money for the students. I think that it is a great way to reuse stuff that are in working condition instead of throwing it away. 
Benefits of giving away things:
Promotes reuse.
It will help the people who really need them.
Promotes the joy of giving.

3 Design

Amazon Cognito

I used Amazon Cognito to provide sign up and sign in functionalities for the app using my own solution to store the user information. With Cognito Identity, one can easily and securely add sign-up and sign-in functionality to your mobile and web apps. Cognito Identity is fully managed and can scale to support hundreds of millions of users. One also implemented enhanced security features, such as email and phone number verification.

Amazon DynamoDB

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. I used key-value store models to store user information as well as the details of the items that are listed on the app.

I used two database table to store the above information. 

While signing up for the app, the user is prompted to enter his personal information like
email id, phone number and set a password for his account in this app. This information is stored separately on two tables.

This table is used to store the user personal details such as name, email id and phone number. The primary key of this table is Facebook user id. Table 1 shows all the fields and their data types. To access the data in the application two java classes are created for the two tables in the database. Each program contains private variables that map to columns of the table. Each variable has its own getter, setter and constructors. For retrieving the data, we create an object of the class and using the query we get the data directly from the table. In the case of multiple rows we create an array list and access the data. To query the database in the cloud, we first create objects following objects, 
• MobileServiceClient – to connect to the database service.
• MobileServiceTable – to map the java class to the table in the database.
• ArrayList object of the class created.
final ArrayList results =mTableDb.where().field("userId").eq(UserId).and(mTableDb.where().field("isactive").eq("0")).execute().get();
A sample query is as shown above. All the data that is matching this query is retrieved and is saved in the arraylist variable object. Using getter methods we can retrieve the data from each of the fields. Similarly we can use different queries to insert/update or delete the data from the tables. All these queries will be embedded in async tasks and run as separate threads over main thread.
4  APP Walkthrough
When the app is launched for the first time, it opens up a sign-in page. It also has a sign-up button to register the first time users. First time users have to input their details        along with the email id and create an account. The password follows standard password policy. An email with a confirmation code is sent to the user email id. The user is then prompted to enter this code to complete the registration and is then redirected to sign in page. Once the user signs in, he is sent to the Home Page.
Home Page
Home Page is the main activity of this app. This activity houses 3 main tabs modelled as fragments.
On the GiveAway tab, the user can enter the details of the item he wants to donate. Once he enters relevant information and submits, The database is updated with this new item.
The Browse tab is for browsing through the items available. It displays the items as a list in recycler view. Once the user selects any item in that list, the details of that item are shown in a new view. 
The My Items tab displays the items that are listed by the user for giving away.The user is provided with an option to delete an item that has already been donated to take it off the list. This is done by long pressing the item in that list.
5 TECHNOLOGIES USED
5.1 RECYCLER VIEW
To create complex lists and cards with material design style in the app, Recycler View has been used. Recycler View replaces the List View that was previously used. Recycler View was newly introduced in android Lollipop. It has many advantages over list view like it is very easy to modify the data in the recycle view compared to the list view. And like list view this also uses an adapter to bind data to a fragment. Recycler view together with card view make the appearance more elegant.
5.2 ANDROID STUDIO
I have developed the android app using the android development application Android Studio. Android Studio is the new application that provides the environment for developing android application. I used Android Studio because of the additional features compared to Eclipse and are easy to develop apps as compared to Eclipse.

5.3 MATERIAL DESIGN
This app is built based on the Google’s design language called Material Design. Material design is a comprehensive guide for visual, motion, and interaction design across platforms and devices. It has an increased use of grid layouts, responsive animations and transitions, depth effects and padding. App built using Material Design is more attractive, more user-friendly. The icons used in this app are the ones present in Material Design.

5.4 APIS USED IN THE APP
Amazon DynamoDB 
The APIs of DynamoDB is most important and predominantly used API in this app. The database operations involving the creation of the database table, insertion of items into the database, querying of the database to display item details, and deletion of the items that are no longer on the list are all handled by DyanmoDB APIs provided by Amazon AWS services.
Amazon Cognito
Amazon cognito was mainly used to enable user sign-in and sign-up. The implementation is fairly easy and since the app involves transactions of items physical in nature, it becomes all the more important to register the users and store their information to prevent shady dealings.
Google Maps geo-code API
This API is provided by the Google. This API is used to get the latitude and longitude of a place by giving the address of the place as the input. This is a JSON request and a url is created using the address entered by the user. After we get the JSON feed back, we parse it to get the latitude and longitude values. In the app, we use this API to get the latitude and longitude of the starting point address and destination point address which are then stored in database on the cloud.

6 TECHNICAL CHALLENGES
Following are some of the technical challenges we faced,
There are many cloud providers like Google, Amazon and Microsoft. But there are no proper tutorials for setting up the cloud and creating database. In few setting up the cloud was easy but creating databases in it was not.
Storing images in Database is not at all a good idea. However references to images can be stored on the database while the actual images can themselves be stored on filesystems using services like the Amazon S3.
There were restrictions on the cloud usage such as number of days it could be used for free, number of requests per day, amount of data that can be stored on the cloud, etc. So selecting the right cloud provider for our app considering all these was important.
Also all these cloud provider provide these trial services only for 1 or 2 months. In our project since we used Azure which provides 1 month free trial services, we had to migrate services three times to new accounts. And also there is no proper way to migrate the data. Everything was supposed to be done manually and was time consuming.
Another challenge that I faced was handling the async tasks and threads. Since we had a lot of interactions with the cloud database and to access a service we have to either user async task or threads. The main issue was to keep everything in sync. We faced issues where some tasks took longer time to finish and some took less time. It was hard to keep them in sync unless you delay the other.
Also since we are using trial versions, the service are very slow and response time is unpredictable.

7  EVALUATION
We created a number of test cases to validate the functionality of our application. The test cases also included a number of negative scenarios like can we select a date in the past, or can we leave all the edit texts blank and save the data etc. All these scenarios are now covered in the application. Since our application has lot of cloud and api interaction, the performance of our application solely depends on the response times of the cloud api’s. We tried to find the average time of response but as said before since we are using free trial services the service are very slow and response time is unpredictable. We also evaluated the performance of each of the threads these again depend on services. Also amount of on mobile device memory for storing data is minimal in our application since all the data is stored inside the cloud.





















 

