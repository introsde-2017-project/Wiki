# Introsde-project-2017.   

NAME: Cheema Danish Asghar  
EMAIL: danishasghar.cheema@studenti.unitn.it  

Group Partner by:  
NAME: Jan Main muhammad Faheem  
EMAIL: main.jan@unitn.it 

app URL: https://knowyourcity123.herokuapp.com/  

## introduction:  
`KnowYourCity` is an app which is used to suggest different food and movie recommendations to registered users based on there preferences, for recommendations a remote `Recombee` API is used, where we used two different Databases one for Food and another one for Movies In order to save the personal data of a user local `sqlite` DataBase is used. For the Quotes, a Remote Rest API is used which gives a random Quote with author name, each time its called.  
 

## FrontEnd Structure:  
1) A new User can easily Register and use all the services in the app, for registration a user select type of movie and food to select the preferences. username and at least 3 digit password are mandatory, rest of the field is optional.  
2) After successful signup user can login, the home page is consist of 4 tabs as follows.  

| Search | Recommandation | My Ratings | Analysis |
|--------|----------------|------------|----------|
3) In search tab, a user can select food/movie type and get all the Items save in the DB.  
4) Recommendation tab is used to get Recommendation for a user based on preferences.  
5) My Ratings show all the rating added by a user.  
6) The analysis tab shows all the items with the average rating given by different users.  
7) Detail shows the user preferences and other details.  
8) with each refresh a new random quote is displayed on the top of the page.  

## Implementation and Project Structure
As you can see in the diagram below project is consist of different layers, and multiple Rest And Soap based services. 
![alt text](https://github.com/introsde-2017-project/Wiki/blob/master/Diagram1.png)

### Food Process Centric Layer
API Documantation: 

This layers is responsible for handling all the request coming from front-end user interface and process/redirect the requests accordingly to lower layers, all the required authentication are handled in this layer for each individual user.
Each time a user login it gets a unique Bearer token which he has to use for all the further requests in the future.

Here is a list of services availabe for Api consumer:
#### User Resource         
![alt text](https://github.com/introsde-2017-project/documentation/blob/master/User_Resource.png)


